# Cómo recibir feedback de revisión sin tomártelo como algo personal

La mayoría de los consejos sobre revisión de código están escritos para los revisores. Éste es para el otro lado del diff — porque cómo respondes al feedback determina si tus revisores siguen dándote comentarios honestos y útiles, o empiezan a suavizarlo todo para evitar una reacción.

## El comentario es sobre el código tal como estaba cuando lo escribiste

No sobre tu habilidad, tu inteligencia ni tu valía como ingeniero. Los comentarios de revisión de código son una instantánea: esto es lo que era visible en este diff, hoy. Leer «esta función está haciendo demasiado» como «soy malo en mi trabajo» es un salto que el propio comentario nunca dio — esa interpretación la añades tú, y vale la pena pillarte haciéndolo.

## Separa «han encontrado un problema real» de «me están juzgando»

Son dos hechos distintos, y sólo uno de ellos requiere una reacción:

- **Se ha encontrado un problema real.** Información útil. Corrígelo, o explica por qué en realidad no es un problema.
- **Se ha emitido un juicio sobre ti.** A veces esto ocurre de verdad (ver la nota sobre hostilidad real más abajo), pero con mucha más frecuencia es una lectura que estás añadiendo a un comentario neutro porque el feedback es incómodo por defecto, aunque se entregue bien.

Si te notas respondiendo a la defensiva, vale la pena hacer una pausa antes de responder — un comentario escrito en la primera oleada de defensividad raramente mejora la conversación.

## Cuando no estás de acuerdo

Explica tu razonamiento, no te limites a empujar hacia atrás. «Lo consideré, pero la restricción X significaba que el enfoque Y no funcionaría — con gusto lo explico si es útil» hace avanzar la conversación. «No, esto está bien» no le da al revisor nada con lo que interactuar, y se lee como desestimatorio aunque no sea tu intención.

Está bien no estar de acuerdo y mantener tu posición. También está bien estar equivocado y decirlo directamente — «buena observación, se me pasó» no cuesta nada y construye el tipo de confianza que hace que los revisores se sientan cómodos siendo directos contigo en el futuro.

## Cuando el feedback se siente mucho de golpe

Un PR con quince comentarios puede sentirse como un ataque en grupo, especialmente si eres más nuevo o es un cambio grande. Algunas cosas que ayudan:

- **Ordena por gravedad primero**, si tu revisor no lo hizo ya. Algunos comentarios son bloqueantes, algunos son «considera esto», algunos son detalles. Tratar los quince como igualmente urgentes es agotador y generalmente no era la intención.
- **Responde a grupos, no a cada comentario por separado**, cuando varios señalan la misma causa raíz. «Veo el mismo problema señalado en tres sitios — refactorizaré el auxiliar compartido en lugar de parchear cada lugar de llamada» suele ser una mejor corrección que tres parches individuales.
- **Está bien decir «esto es mucho, ¿podemos sincronizarnos brevemente en lugar de ir comentario a comentario?»** Los hilos de revisión no son el único medio válido, y a veces son el más lento.

## Sobre el feedback genuinamente hostil o desestimatorio

A veces el feedback se entrega realmente mal — sarcástico, condescendiente, o personal en lugar de técnico. Eso merece nombrarse directamente, separado del contenido técnico: «Me ocuparé de los puntos técnicos, pero la formulación en [comentario] se leyó como desestimativa — ¿podemos mantener el feedback centrado en el código?» No tienes que absorberlo en silencio para parecer profesional; nombrarlo con claridad y calma *es* la respuesta profesional. Consulta [`how-to-give-feedback.md`](how-to-give-feedback.md) — vale la pena compartirlo con quien te esté dando ese tipo de feedback.

## Trata los comentarios de revisión como tiempo de ingeniero senior gratuito

Reencuádralo: alguien ha dedicado tiempo real a leer tu código con suficiente atención como para encontrar ese caso extremo. Eso no es gratuito en ningún otro sitio — el tiempo de pareja, la mentoría, el coaching de calidad de código, todo tiene un coste. Una revisión exhaustiva es una de las formas más baratas de mejorar en este trabajo, incluso cuando (especialmente cuando) señala algo que te has perdido.

## Qué hacer después de haber atendido los comentarios

Responde explícitamente a cada uno — «Corregido en [commit]», «Buen punto, cambiado a X», o «No estoy de acuerdo, por esto, avísame si eso cambia las cosas» — en lugar de hacer push de nuevos commits en silencio y dejar al revisor que adivine qué cambió y por qué. Es un pequeño hábito que hace la segunda pasada de revisión dramáticamente más rápida.
