# Ejemplo anotado: un mal PR (y cómo corregirlo)

El mismo cambio subyacente que en [`good-pr-example.md`](good-pr-example.md) — una corrección para emails de confirmación duplicados — pero escrito tal como aparece realmente en la práctica. Cada problema que se muestra a continuación es habitual, no excepcional.

---

## Título

> **fix bug**

> 🔴 **El problema:** no le dice nada al revisor (ni al futuro lector de `git log`). ¿Es el bug del email, el del checkout, el del inicio de sesión?
> 🟢 **Corrección:** nombra el comportamiento real y el síntoma real: «Corregir condición de carrera que provoca emails de confirmación de pedido duplicados.»

## Descripción

> *(vacía)*

> 🔴 **El problema:** una descripción vacía obliga al revisor a reconstruir la intención únicamente a partir del diff. Esto por sí solo duplica aproximadamente el tiempo de revisión, porque cada pregunta de «por qué» que una frase podría haber respondido ahora tiene que inferirse o preguntarse en un hilo de comentarios.
> 🟢 **Corrección:** incluso tres frases — qué se rompió, por qué, y qué cambió — habrían evitado la mayor parte del intercambio de ida y vuelta que generó este PR en la revisión.

## El diff (abreviado)

```diff
+ const existing = await db('order_confirmations').where({ order_id: orderId }).first();
+ if (existing) return;
+ await db('order_confirmations').insert({ order_id: orderId, confirmed_at: new Date() });
+ await sendConfirmationEmail(orderId);
```

> 🔴 **El problema:** esto *parece* la misma corrección que en el buen ejemplo, pero no lo es — la comprobación y la inserción no están envueltas en una transacción. Dos peticiones concurrentes pueden pasar ambas la comprobación `if (existing) return` antes de que ninguna inserte, que es exactamente la condición de carrera que este PR afirma corregir. Sin la descripción que explique el mecanismo pretendido, esto es mucho más difícil de detectar para el revisor, porque no hay ninguna afirmación declarada contra la que verificarlo.
> 🟢 **Corrección:** envuelve la comprobación y la inserción en una transacción de base de datos (o usa una restricción única en la que la inserción pueda apoyarse), como hace el buen ejemplo. La descripción también debería indicar explícitamente que la atomicidad es el mecanismo, para que el revisor sepa exactamente qué verificar.

## Pruebas

> *(ninguna añadida)*

> 🔴 **El problema:** «corregida una condición de carrera» sin ninguna prueba que ejercite la concurrencia es una afirmación no verificada. La corrección puede funcionar por suerte en las pruebas manuales y aun así fallar bajo carga real de producción.
> 🟢 **Corrección:** una prueba que lanza dos intentos de confirmación concurrentes y verifica que sólo se envió un email — la misma del buen ejemplo — habría detectado la transacción ausente inmediatamente, antes de que un revisor humano tuviera que detectarla leyendo con atención.

## Historial de commits de este PR

```
wip
fix
arreglarlo de verdad
fix lint
```

> 🔴 **El problema:** ninguno de estos mensajes de commit es útil por sí solo. `git blame` en este código dentro de un año apuntará a un commit llamado «fix» sin ningún contexto.
> 🟢 **Corrección:** o bien haz squash en un único commit bien descrito antes del merge, o escribe mensajes de commit que se sostengan solos: «Añadir transacción alrededor de la comprobación e inserción de confirmación de pedido.»

## Tamaño

> Este PR también modificó 14 archivos no relacionados — una actualización de dependencia, un par de cambios de formateo en componentes no relacionados, y una corrección de errata en el texto de otra funcionalidad.

> 🔴 **El problema:** expansión de alcance. El revisor ahora tiene que averiguar cuáles de los 14 archivos son realmente relevantes para «corregir la condición de carrera», y cualquiera de esos cambios no relacionados podría ocultar un bug no relacionado que recibe el visto bueno porque el PR trata «sobre» otra cosa.
> 🟢 **Corrección:** divide en PRs separados. «Un PR, una razón» hace tanto la revisión como el rollback dramáticamente más simples — si la actualización de dependencia rompe algo, no querrás que esté enredada con una corrección de incidente de producción.

---

## El patrón detrás de todo esto

Cada problema aquí se puede corregir con esfuerzo que el *autor* dedica antes de abrir el PR, no con esfuerzo que el revisor dedica a detectarlo después. Esa es la lección real: un mal PR no suele significar mal código — suele significar que el empaquetado (descripción, alcance, pruebas, commits) no hizo el trabajo de hacer revisable el buen código.
