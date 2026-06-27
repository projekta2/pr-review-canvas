# Una guía para tus primeras revisiones de código

Te acaban de asignar tu primer PR para revisar, y no tienes ni idea de por dónde empezar. Es normal — nadie nace sabiendo cómo revisar código, y la mayoría de los equipos nunca lo enseñan de verdad. Simplemente esperan que lo vayas aprendiendo observando los comentarios de otros. Esta guía es lo que nadie se sentó a explicarte.

## Antes de leer una sola línea de código

Lee primero la descripción del PR, entera, antes de abrir el diff. Si no la hay, o es demasiado escueta para entender qué está pasando, eso ya es información útil — pide contexto al autor antes de empezar, en lugar de adivinar.

Pregúntate: ¿qué problema está resolviendo esto? Si no puedes responder eso en una frase, no estás preparado para juzgar si la solución es buena. Ve a averiguarlo — lee la incidencia enlazada, pregunta por chat, lo que haga falta.

## Cómo leer el diff de verdad

No lo leas de arriba a abajo en el orden de los archivos. El orden por defecto de GitHub suele ser alfabético, que no tiene nada que ver con cómo tiene sentido el cambio. En su lugar:

1. **Encuentra el punto de entrada.** ¿Dónde empieza realmente el nuevo comportamiento — una nueva función, una nueva ruta, un nuevo componente? Empieza por ahí.
2. **Sigue la lógica, no la lista de archivos.** Si el punto de entrada llama a un auxiliar, ve a leer ese auxiliar a continuación, aunque esté tres archivos más abajo en el diff.
3. **Lee las pruebas al final, a propósito.** Las pruebas te dicen lo que el autor cree que hace el código. Lee primero la implementación y forma tu propia opinión sobre lo que debería hacer — luego contrasta las pruebas con eso, no al revés.

## Qué buscar, más o menos en este orden

1. **¿Hace esto lo que dice la descripción?** Parece obvio, pero es el paso que más se salta. Un PR puede estar bien escrito, limpio y probado, y aun así no resolver el problema declarado.
2. **¿Está en el lugar correcto?** Un trozo de lógica perfectamente válido en la capa equivocada (lógica de negocio en una vista, una consulta de base de datos en una función de utilidad) crea problemas más adelante aunque funcione hoy.
3. **¿Se gestionan los casos extremos?** Lista vacía, cero, números negativos, null, la llamada de red que falla a mitad. El camino feliz casi siempre funciona; aquí es donde se esconden los bugs de verdad.
4. **¿Está probado de una manera que signifique algo?** Una prueba que sólo comprueba que la función se ejecutó sin lanzar una excepción no está realmente probando nada.
5. **¿Podrías mantener esto dentro de seis meses?** Si la respuesta es «sólo si el autor original me lo explica de nuevo», merece la pena mencionarlo.

No tienes que revisar todo esto con la misma profundidad en cada PR. Una corrección de una línea de texto de copia no necesita el mismo escrutinio que un nuevo flujo de pago. Adapta el esfuerzo al riesgo.

## Cómo no sentirte abrumado

- **No tienes que detectarlo todo.** La revisión es una capa de defensa, no la única. CI, pruebas y staging también existen.
- **Está bien aprobar con comentarios.** «Esto tiene buena pinta, una pequeña sugerencia abajo, no es bloqueante» es una revisión completamente válida. No todo tiene que bloquear un merge.
- **Está bien decir «no tengo suficiente contexto para revisar esta parte».** Fingir que entiendes algo que no entiendes no le ayuda a nadie, y menos a ti.
- **Haz preguntas en lugar de adivinar.** «¿Por qué has elegido X en lugar de Y aquí?» se lee de manera muy diferente a «Esto debería ser Y» cuando en realidad no estás seguro de cuál es correcto — y abre una conversación en lugar de iniciar una discusión.

## Cómo escribir tus primeros comentarios

Comenta sobre el código, no sobre la persona. «Esta función gestiona tres responsabilidades diferentes» es un hecho sobre el código. «Siempre lo complicas todo» es un ataque a la persona, aunque no sea intencionado. Consulta [`how-to-give-feedback.md`](how-to-give-feedback.md) para una guía más detallada sobre cómo formular los comentarios.

Una plantilla útil para tus primeros comentarios:

> *Observación* — lo que has notado.
> *Por qué importa* — la consecuencia real, no sólo «no es como yo lo haría».
> *Sugerencia* — lo que considerarías en su lugar, formulado como pregunta si no estás 100% seguro.

Ejemplo: «Este bucle vuelve a buscar el usuario en cada iteración (observación). Con una lista de 1.000 elementos, eso son 1.000 consultas extra (por qué importa). ¿Funcionaría buscarlo una sola vez antes del bucle y pasarlo como parámetro? (sugerencia, como pregunta, ya que puede haber una razón que me estoy perdiendo).»

## Cuando no estás seguro de si algo es realmente un problema

Pregunta, no afirmes. «¿Hay alguna razón por la que esto no está en caché?» es honesto e invita a una respuesta. «Esto debería estar en caché» asume que ya conoces las restricciones con las que trabajaba el autor — y a veces no es así.

## Lo que «aprobar» significa realmente

Una aprobación es una declaración de que has revisado esto y estarías cómodo asociándote con que llegue a producción. No significa que hayas encontrado todos los problemas posibles — significa que has hecho una revisión genuina y honesta al nivel de escrutinio que merecía el cambio. Si has ojeado una sección porque se te acabó el tiempo o el contexto, dilo en lugar de aprobar en silencio.

Usa [`pr-review-checklist.md`](../../checklists/es/pr-review-checklist.md) en un par de PRs. Al principio se sentirá lento. Se vuelve rápido.
