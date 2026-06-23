# Antipatrones en la revisión de código

Las formas recurrentes en que las revisiones de código salen mal — en ambos lados del diff. La mayoría no son malas intenciones; son hábitos que parecen razonables en el momento y que erosionan silenciosamente la confianza en el proceso con el tiempo.

## Del lado del revisor

### La avalancha de detalles de pasada
Veinte comentarios, todos sobre formateo, nomenclatura y estilo, ninguno sobre si la lógica es correcta. Parece exhaustivo. No lo es — es el tipo de feedback más fácil de generar, que es exactamente por qué es tentador, y satura los comentarios que realmente importan. **Solución:** si cada comentario que estás a punto de dejar es de nivel estilo, pregúntate si un linter debería estar capturando esto en su lugar, y dedica el tiempo ahorrado a una pasada real de lógica y casos extremos.

### El sello de goma
Aprobar a los dos minutos de que aterrice un diff de 400 líneas. A veces esto es genuinamente correcto (un cambio trivial) — pero cuando se convierte en el valor por defecto independientemente del tamaño, la revisión deja de proporcionar ninguna señal real. **Solución:** adapta la profundidad de la revisión al riesgo, de forma explícita. Si estás dando el visto bueno a algo arriesgado porque estás ocupado, dilo: «apruebo pero no he revisado de cerca la lógica de la migración, lo señalo para alguien con más contexto allí.»

### La re-litigación silenciosa
Bloquear un PR por una preferencia que el equipo ya resolvió en su guía de estilo o en una decisión anterior, sin reconocer que ya se decidió. **Solución:** si no estás de acuerdo con un estándar existente, plantéalo como una conversación separada sobre el estándar — no como un bloqueante en el PR no relacionado de otra persona.

### El bloqueante vago
«Esto no me parece bien» sin especificaciones. Técnicamente es un comentario bloqueante, pero no le da al autor nada sobre lo que actuar excepto adivinar. **Solución:** si no puedes articular el fallo concreto, eso es una señal para investigar más antes de comentar, no después.

### Revisar el historial de la persona, no el diff que tienes delante
«La última vez hiciste X, así que asumo que esto tiene el mismo problema» — sin comprobar realmente si lo tiene esta vez. **Solución:** cada PR se revisa según su propia evidencia. Los patrones del historial pueden informar sobre *dónde mirar más de cerca*, nunca sustituir al hecho de mirar realmente.

## Del lado del autor

### El mega-PR
Un único PR que toca doce cosas no relacionadas porque todas resultaron hacerse en la misma semana. Revisable en teoría, agotador en práctica — y las partes no relacionadas diluyen el escrutinio sobre las partes que realmente importan. **Solución:** un PR, una razón. Si no puedes resumir el cambio en una frase sin «y», probablemente son dos PRs.

### El push silencioso
Hacer push de nuevos commits en respuesta al feedback sin ningún comentario que explique qué cambió, dejando al revisor que haga diff del diff para averiguar qué se ha atendido. **Solución:** responde a cada comentario, aunque sea brevemente. «Corregido en el último commit» cuesta diez segundos y le ahorra al revisor varios minutos de trabajo de detective.

### Defender en lugar de interactuar
Responder a cada comentario con una justificación de la elección original, en lugar de interactuar con si el comentario tiene razón. Incluso cuando la elección original era correcta, «no, esto está bien» enseña al revisor que plantear preocupaciones no merece la fricción. **Solución:** «Lo consideré — aquí está la restricción que me llevó aquí, pero abierto a revisarlo si no se sostiene» consigue el mismo resultado sin cerrar la conversación.

### Enterrar el cambio real en ruido
Autoformatear todo el archivo como parte de una corrección de lógica de una línea, de modo que el diff muestra 200 líneas cambiadas para un cambio de una línea. **Solución:** mantén los cambios de formateo en un commit o PR separado, aunque sea tentador «limpiar mientras estás por allí».

### Tratar los comentarios de revisión como un examen final que pasar
Corregir exactamente lo que se señaló, de la manera más restrictiva posible, sin abordar el patrón subyacente si aparece en otro lugar del mismo archivo. **Solución:** si un comentario señala un problema real, comprueba si el mismo problema existe cerca antes de declararlo corregido.

## En ambos lados

### Litigar el tono más que la sustancia en el propio hilo
Un comentario se lee más duro de lo que se pretendía, y en lugar de que alguna de las partes lo nombre directamente, la conversación se convierte en respuestas de una línea que se vuelven progresivamente más frías. **Solución:** si un hilo parece estar calentándose, ese es el momento de cambiar a una llamada rápida, no de escribir un comentario más afilado de vuelta.

### Tratar el checklist como el techo, no como el suelo
Recorrer un checklist mecánicamente y detenerse ahí, incluso cuando algo con forma de checklist no captura lo que realmente preocupa de un cambio específico. **Solución:** un checklist existe para asegurarse de que no te olvidas de las cosas rutinarias — no es un sustituto de pensar realmente en el PR específico que tienes delante.
