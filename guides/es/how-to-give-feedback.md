# Cómo dar feedback que realmente ayude

La misma observación técnica puede llegar como útil u hostil dependiendo únicamente de cómo se formule. Esta guía trata sobre la formulación — el criterio técnico es tuyo, la entrega es lo que esto puede enseñarte realmente.

## El cambio fundamental: comenta sobre el artefacto, no sobre el autor

Compara estas dos formas de decir lo mismo:

- «Siempre haces estas funciones demasiado complicadas.»
- «Esta función gestiona la búsqueda, la validación y el formateo — dividirla en tres haría que cada una fuera individualmente testeable.»

La primera es un veredicto sobre la persona. La segunda es un hecho sobre el código con un siguiente paso concreto. El autor puede discutir la segunda en función de sus méritos. La primera sólo invita a la defensiva, porque no hay nada técnico a lo que responder — es un juicio de carácter.

## Un patrón que funciona para la mayoría del feedback: observa, explica, sugiere

1. **Observa** — describe lo que ves, de forma neutra. «Este bucle llama a la API una vez por elemento.»
2. **Explica la consecuencia** — por qué importa, concretamente. «Con una lista de 1.000 elementos, eso son 1.000 peticiones secuenciales.»
3. **Sugiere, sin imponer** — ofrece una dirección, deja margen al criterio del autor. «¿Funcionaría aquí agrupar estas peticiones en una sola, o hay alguna restricción que me estoy perdiendo?»

Esa última cláusula — «o hay alguna restricción que me estoy perdiendo» — importa más de lo que parece. Señala que estás abierto a estar equivocado, lo que suele ser verdad: no tienes todo el contexto que tiene el autor. También le facilita al autor decir «de hecho sí, por esto» sin que parezca que está cediendo.

## Calibra según la gravedad

No todos los comentarios necesitan el mismo peso. Ser explícito sobre lo serio que consideras algo evita mucho intercambio innecesario:

- **Bloqueante:** «Esto lanzará una excepción con un array vacío — hay que corregirlo antes del merge.»
- **Debería corregirse, no bloqueante:** «Vale la pena corregirlo, pero no voy a bloquear el PR por ello — a tu criterio si lo haces ahora o en un seguimiento.»
- **Detalle / opcional:** «Detalle: `listaUsuarios` se lee un poco más claro que `lu`, pero tampoco es para tanto.»

Etiquetar la gravedad evita que los autores tengan que adivinar qué comentarios son realmente críticos.

## Frases que funcionan

- «Ayúdame a entender por qué...» — genuinamente curioso, no retórico.
- «¿Qué pasa si...» — invita al autor a recorrer él mismo un caso extremo, lo que a menudo saca a la luz la respuesta (o el vacío) más rápido que si lo dices tú.
- «Cosa pequeña, pero...» — señala algo como de bajo impacto antes de que el autor lea el resto de la frase a la defensiva.
- «Puede que me esté perdiendo contexto, pero...» — útil exactamente cuando sospechas que hay una razón, y quieres preguntar en lugar de asumir que no la hay.

## Frases que hay que jubilar

- «Esto está mal.» — ¿Mal cómo? Describe el fallo concreto en lugar de emitir un veredicto.
- «¿Por qué lo harías así?» — Se lee como retórica aunque no se pretenda. «¿Qué te llevó a este enfoque?» pregunta lo mismo sin el juicio implícito.
- «Obviamente esto debería...» — Si fuera obvio, es poco probable que el autor lo pasara por alto. «Obviamente» suele señalar impaciencia, no claridad.
- «Según mi comentario anterior...» — Si hay que repetir un punto, probablemente la primera versión no fue suficientemente clara, o el desacuerdo es real y merece una conversación de verdad, no un recordatorio de tono pasivo-agresivo.

## Sobre el «sándwich de cumplidos»

El consejo clásico — envolver la crítica entre dos cumplidos — funciona bien en pequeñas dosis pero falla a escala: recibe suficientes y los cumplidos empiezan a leerse como relleno, lo que en realidad socava los genuinos. Un mejor valor por defecto es encabezar con elogios genuinos y específicos cuando se merecen («el manejo de errores aquí es realmente exhaustivo») y omitirlos cuando no, en lugar de fabricar una nota positiva sólo para suavizar cada comentario.

## Cuando no estás de acuerdo con el enfoque, no sólo con los detalles

Separa «esto tiene un bug» de «yo lo habría construido de otra manera». Lo primero merece plantearse directamente. Lo segundo merece plantearse como pregunta, porque el desacuerdo arquitectónico suele ser sobre concesiones que ninguna de las partes ha declarado del todo todavía: «Yo me habría inclinado por composición en lugar de herencia aquí — ¿había alguna razón concreta por la que necesitabas la clase base compartida?»

## Adaptar el feedback al nivel de experiencia

Un autor junior se beneficia de más contexto por comentario — no porque necesite que las cosas se le «simplifiquen», sino porque todavía no ha construido la biblioteca de patrones que un ingeniero senior usa para rellenar los huecos automáticamente. «Esto tendrá una fuga de memoria porque el listener nunca se elimina» enseña algo. Un autor senior revisando el mismo código puede necesitar sólo «fuga de listener en el camino de desmontaje» — rellena el resto, y sobre-explicar puede leerse como condescendiente.

## La prueba para cualquier comentario antes de publicarlo

¿Te sentirías cómodo diciendo esta frase exacta en voz alta, con el mismo tono, si el autor estuviera sentado a tu lado? Si la formulación sólo funciona porque hay una pantalla de por medio, reescríbela.
