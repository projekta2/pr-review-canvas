# Ejemplo anotado: un buen PR

Este es un PR ficticio pero realista, anotado para mostrar *por qué* funciona. El objetivo no es presentar un PR impecable — es mostrar los hábitos específicos y aprendibles que separan «fácil de revisar» de «agotador de revisar».

---

## Título

> **Corregir condición de carrera que provoca correos de confirmación de pedido duplicados**

> 🟢 **Por qué funciona:** específico, nombra el bug real, y significaría algo en un registro de cambios dentro de seis meses. Compáralo con una alternativa vaga como «fix bug de email» — el mismo cambio, mucho menos útil cuando no es más que una línea en `git log`.

## Descripción

> **Resumen**
> Los pedidos realizados con ~200 ms de diferencia desde la misma sesión podían desencadenar dos correos de confirmación, porque la comprobación «¿ya se ha confirmado este pedido?» y la acción «enviar email» no eran atómicas. Esto añade un bloqueo a nivel de base de datos alrededor de esa comprobación.
>
> **Contexto**
> Cierra #482. Reportado por soporte — tres clientes recibieron emails duplicados en la última semana, todos durante reintentos de pago en conexiones lentas.
>
> **Qué ha cambiado**
> - Añadida una restricción única en `order_confirmations.order_id`
> - Envuelta la lógica de confirmar-y-enviar en una transacción
> - Añadida una prueba que lanza dos intentos de confirmación concurrentes y verifica que sólo se envía un email
>
> **Cómo probarlo**
> Ejecuta `npm test -- order-confirmation.spec.ts` — la nueva prueba (`previene_confirmacion_duplicada_bajo_peticiones_concurrentes`) ejercita específicamente esto.
>
> **Riesgos**
> Bajo. Esto sólo añade una restricción y un límite de transacción a un flujo existente; no cambia el comportamiento del camino feliz para el 99,9% de los pedidos que no estaban en carrera.

> 🟢 **Por qué funciona:** un revisor puede entender el problema completo, la corrección y el plan de validación sin abrir un solo archivo. La sección «Riesgos» en particular hace trabajo real — le dice al revisor dónde enfocarse (la nueva lógica de transacción) y dónde no preocuparse (el camino feliz no afectado).

## El diff (abreviado)

```diff
+ await db.transaction(async (trx) => {
+   const existing = await trx('order_confirmations')
+     .where({ order_id: orderId })
+     .first();
+
+   if (existing) {
+     return; // ya confirmado, nada que hacer
+   }
+
+   await trx('order_confirmations').insert({ order_id: orderId, confirmed_at: new Date() });
+   await sendConfirmationEmail(orderId);
+ });
```

> 🟢 **Por qué funciona:** el comentario `// ya confirmado, nada que hacer` explica *por qué* existe el retorno anticipado, no lo que hace (el código ya dice lo que hace — retorna). Este es exactamente el tipo de comentario que se gana su lugar.

## La prueba

```ts
it('previene confirmación duplicada bajo peticiones concurrentes', async () => {
  const [resultadoA, resultadoB] = await Promise.all([
    confirmarPedido(pedidoId),
    confirmarPedido(pedidoId),
  ]);

  const emailsEnviados = await getEmailsEnviadosA(pedido.emailCliente);
  expect(emailsEnviados).toHaveLength(1);
});
```

> 🟢 **Por qué funciona:** el nombre de la prueba describe el escenario exacto contra el que protege. Si esta prueba falla dentro de seis meses, quien vea el fallo sabe inmediatamente qué ha regresionado, sin abrir el archivo.

## Lo que el revisor no tuvo que hacer

- Preguntar «por qué se cambió esto» — la descripción lo respondía.
- Adivinar el alcance del impacto — la sección «Riesgos» lo acotaba.
- Verificar manualmente que la corrección funciona — la nueva prueba lo demuestra directamente, ejercitando la condición de carrera real en lugar de simplemente comprobar que la función no lanza una excepción.

Ese es el hilo conductor de todo «buen PR»: hace el trabajo de orientación del revisor *por él*, de modo que el tiempo real de revisión se dedica a juzgar el enfoque, no a reconstruir el contexto.
