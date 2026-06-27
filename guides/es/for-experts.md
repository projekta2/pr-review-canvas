# Revisar a escala: técnicas para revisores experimentados

Una vez que estás revisando diez o más PRs a la semana, el cuello de botella deja de ser «¿sé qué buscar?» y pasa a ser «¿cómo hago esto sin que se coma todo mi día?» Esta es la guía para esa etapa.

## Clasifica antes de revisar

No todos los PRs merecen la misma profundidad de atención. Antes de leer una sola línea, clasifícalos:

- **Trivial** (errata, corrección de texto, actualización de dependencia sin cambio de comportamiento): ojéalo y aprueba. Dedicar diez minutos aquí es un coste, no diligencia.
- **Rutinario** (una funcionalidad que sigue un patrón establecido en el código): revísalo a profundidad normal, pero puedes ir rápido porque ya sabes cómo es «correcto» para este tipo de cambio.
- **De alto riesgo** (toca autenticación, facturación, migraciones de datos, o un sistema que no conoces del todo): ralentiza deliberadamente. Aquí es donde la [plantilla de PR avanzada](../../templates/es/pr-template-advanced.md) vale su peso, y merece la pena incorporar a un segundo revisor.

Clasificar erróneamente un cambio de alto riesgo como rutinario es la forma más habitual en que código malo llega a producción con una marca verde al lado.

## Lee las estadísticas del diff antes del diff en sí

`+1200 −40` en 30 archivos es una revisión distinta a `+40 −12` en 2 archivos, aunque ambos afirmen hacer «el mismo tipo de cosa». Si el tamaño de un PR no encaja con su alcance declarado, merece un comentario antes incluso de empezar a leer — o la descripción está incompleta, o el PR está haciendo más de lo que debería.

## Revisa en pasadas, no de una sola vez

Intentar detectar problemas de arquitectura, detalles de nomenclatura y preocupaciones de seguridad en una sola lectura es como los revisores se pierden cosas. Dos pasadas rápidas superan a una lenta:

1. **Pasada estructural:** ¿esto encaja donde está, tiene el tamaño correcto, tiene sentido el enfoque? No comentes sobre nomenclatura ni estilo todavía.
2. **Pasada de detalle:** ahora ve línea por línea para comprobar corrección, casos extremos, nomenclatura y pruebas.

Esto también evita que te ancles al primer problema que detectas y te pierdas el problema estructural más importante tres archivos más adelante.

## Delega la revisión, no sólo la distribuyas

En equipos grandes, «todos revisan todo» no escala, y «la persona senior revisa todo» tampoco escala — sólo mueve el cuello de botella. Lo que sí escala:

- **Propiedad de dominio.** La persona propietaria de un módulo revisa por defecto los cambios en él; otros revisan para cosas fuera de ese dominio (nomenclatura, pruebas, salud general del código).
- **Asignar revisores por contexto, no por antigüedad.** Un ingeniero de nivel medio que entregó la funcionalidad original a menudo revisa un cambio relacionado mejor que un ingeniero senior que lo ve por primera vez.
- **Establecer SLAs de tiempo de respuesta, no de profundidad de revisión.** «Responder en 4 horas» es una norma saludable. «Encontrar todos los problemas» como SLA sólo produce revisiones superficiales y apresuradas disfrazadas de exhaustivas.

## Usa las herramientas para lo que las herramientas son buenas

El linting, el formateo, la comprobación de tipos y el análisis básico de seguridad pertenecen a CI, no al tiempo de atención de un humano. Si estás dejando el mismo comentario sobre el formateo más de dos veces, eso es un hueco en CI, no un fallo de revisión.

La misma lógica aplica un nivel más arriba: la propia clasificación puede automatizarse parcialmente. Herramientas como **[PR Focus AI Pro](https://chromewebstore.google.com/detail/pr-focus-ai-pro/ememaiabefeojkccjclglcmbjmdpnaoe)** se instalan en el navegador junto a la propia interfaz de GitHub y muestran un resumen de riesgos y un orden de lectura sugerido *antes* de abrir el diff — útil exactamente para el paso de clasificación descrito antes, especialmente cuando tienes más PRs de los que puedes mantener en contexto a la vez. No está pensado para reemplazar tu criterio en la pasada de alto riesgo; está ahí para la parte del trabajo que es reconocimiento repetitivo de patrones.

## Sabe cuándo dejar de leer y empezar a hablar

Si un PR necesita más de dos o tres rondas de comentarios para converger, el intercambio asíncrono ha dejado de ser eficiente. Una llamada de 15 minutos resuelve en tiempo real lo que tardaría dos días más de hilos de comentarios — y es una señal mucho mejor para el autor de que intentas ayudarle a publicar, no sólo encontrar fallos desde la distancia.

## Calibra, no sólo apliques

Un checklist o una guía de estilo es un punto de partida, no un texto sagrado. Si te encuentras bloqueando un PR por algo que el checklist indica pero que realmente no importa para este cambio específico, dilo y sigue adelante. Los revisores que aplican reglas sin criterio entrenan a los autores a hacer trampa con el checklist en lugar de escribir buen código.
