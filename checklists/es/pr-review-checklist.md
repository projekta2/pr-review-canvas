# El Checklist de Revisión de PRs

51 ítems distribuidos en 8 categorías. Cada ítem incluye un «por qué» en una sola línea — un checklist sin razones sólo entrena a la gente a marcar casillas sin pensar.

Esta es la versión canónica y con criterio propio. Si tu equipo quiere adaptarla, parte de [`pr-review-checklist-template.md`](pr-review-checklist-template.md) y conserva ésta como referencia. Si prefieres trabajar de forma interactiva con un indicador de progreso, usa el [checklist en vivo](https://projekta2.github.io/pr-review-canvas/es/) o [`interactive-checklist.html`](interactive-checklist.html).

---

## 1. Contexto y Propósito

- [ ] **La descripción del PR indica claramente qué ha cambiado y por qué.**
  *Por qué:* los lectores futuros (incluido tú dentro de seis meses) necesitan entender la intención sin tener que volver al gestor de incidencias.
- [ ] **El PR enlaza con la incidencia, el ticket o la especificación correspondiente.**
  *Por qué:* la trazabilidad importa más cuando el PR ya es historia antigua y alguien pregunta «¿por qué hicimos esto?»
- [ ] **El tamaño del PR encaja con su alcance declarado — sin cambios no relacionados colados de rondón.**
  *Por qué:* la expansión de alcance es la causa más frecuente de revisiones lentas y propensas a errores.
- [ ] **El título es suficientemente específico como para ser útil en un registro de cambios.**
  *Por qué:* «fix bug» no le dice nada a nadie un año después; «Corregir condición de carrera en el refresco del token de sesión» sí.
- [ ] **Entiendes el problema que resuelve este PR antes de leer una sola línea de código.**
  *Por qué:* no puedes juzgar si una solución es buena si no sabes primero qué está resolviendo.

## 2. Arquitectura y Diseño

- [ ] **El cambio encaja en la arquitectura existente, o justifica explícitamente desviarse de ella.**
  *Por qué:* la deriva arquitectónica silenciosa es como los proyectos acaban teniendo cinco formas distintas de hacer lo mismo.
- [ ] **Las responsabilidades están en la capa o el módulo correcto.**
  *Por qué:* la lógica de negocio en un componente de interfaz, o las operaciones de E/S en una función «pura», dificultan las pruebas y la reutilización posteriores.
- [ ] **La solución no introduce un patrón nuevo cuando uno existente ya resuelve el problema.**
  *Por qué:* cada patrón nuevo es algo más que todo colaborador futuro tendrá que aprender.
- [ ] **El acoplamiento está minimizado — este cambio no obliga a módulos no relacionados a conocerse entre sí.**
  *Por qué:* el acoplamiento fuerte es lo que convierte una corrección de cinco minutos en un cambio de cuatro archivos y tres equipos la próxima vez.
- [ ] **El nivel de abstracción es el adecuado para el problema.**
  *Por qué:* una interfaz para un script de un solo uso es sobreingeniería; un valor codificado en duro en algo que se reutiliza diez veces es infraingeniería.
- [ ] **Los nombres reflejan conceptos del dominio, no detalles de implementación.**
  *Por qué:* `calcularCosteDeEnvio()` sobrevive a una migración de base de datos; `obtenerFilaDeLaTablaOrdenes()` no.
- [ ] **El cambio es consistente con cómo se han resuelto problemas similares en el resto del código.**
  *Por qué:* la consistencia es lo que permite a un revisor (o a un nuevo incorporado) reconocer un patrón en lugar de tener que derivarlo de nuevo.
- [ ] **Si se introduce una nueva dependencia, la concesión está justificada.**
  *Por qué:* el tamaño del bundle, la carga de mantenimiento y las condiciones de licencia son costes reales, no una nota a pie de página.

## 3. Calidad del Código

- [ ] **Las funciones hacen una sola cosa, y el nombre dice cuál es.**
  *Por qué:* una función que hace tres cosas no puede probarse, reutilizarse ni entenderse de forma aislada.
- [ ] **No hay código muerto, bloques comentados ni sentencias de depuración olvidadas.**
  *Por qué:* el control de versiones ya recuerda el código eliminado — el código comentado no es más que ruido con pasos extra.
- [ ] **Los nombres de variables y funciones son descriptivos sin ser verbosos.**
  *Por qué:* `listaUsuarios` supera tanto a `lu` como a `elArrayQueContieneATodosLosUsuariosDelSistema`.
- [ ] **El manejo de errores es explícito — los fallos se capturan y gestionan, no se tragan en silencio.**
  *Por qué:* un bloque `catch` vacío es un informe de error de producción esperando su momento.
- [ ] **No hay números ni cadenas mágicas sin una constante con nombre.**
  *Por qué:* `if (estado === 3)` no le dice nada a la siguiente persona; `if (estado === ESTADO_PEDIDO.ENVIADO)` sí.
- [ ] **Se evita la duplicación, pero no a costa de la legibilidad.**
  *Por qué:* DRY es una guía, no una religión — una abstracción forzada para evitar tres líneas repetidas puede ser peor que la repetición en sí.
- [ ] **El flujo de control es fácil de seguir — sin anidación profunda que requiera un diagrama de flujo para entenderse.**
  *Por qué:* si necesitas contar niveles de llaves para saber qué se ejecuta, lo mismo le pasará a cada lector futuro.
- [ ] **El diff es revisable en alcance y tamaño.**
  *Por qué:* un PR de 40 archivos que «hace todo a la vez» es un fallo de proceso del lado del autor, no un reto para que el revisor esté a la altura.
- [ ] **Los comentarios explican el por qué, no el qué.**
  *Por qué:* el código ya dice lo que hace; un comentario que simplemente lo renuncia en castellano añade coste de mantenimiento sin ningún beneficio.
- [ ] **Los casos extremos — entrada vacía, null, cero, valores máximos — están tratados de forma visible.**
  *Por qué:* el camino feliz es lo que se demuestra; los casos extremos son los que te despiertan a las 2 de la madrugada.
- [ ] **El código no depende de comportamiento implícito que falla en silencio si cambia una dependencia.**
  *Por qué:* depender de ordenación no documentada, valores por defecto o efectos secundarios es una mina antipersona para quien actualice esa dependencia.
- [ ] **El formato y el estilo siguen las convenciones del proyecto.**
  *Por qué:* si el linter no lo capturó antes de abrir el PR, merece la pena arreglarlo en CI, no en cada revisión.

## 4. Pruebas

- [ ] **El comportamiento nuevo tiene pruebas nuevas — no sólo «las pruebas existentes siguen pasando».**
  *Por qué:* las pruebas que pasan demuestran que no has roto el comportamiento antiguo; no dicen nada sobre si el nuevo comportamiento funciona.
- [ ] **Las pruebas verifican comportamiento, no detalles de implementación.**
  *Por qué:* las pruebas que comprueban la estructura interna se rompen en cada refactorización, lo que entrena a la gente a dejar de refactorizar.
- [ ] **Al menos una prueba cubre el camino no feliz, no sólo el camino dorado.**
  *Por qué:* el camino dorado es el 10% de los casos que casi nunca provoca incidencias.
- [ ] **Las pruebas son deterministas — sin temporización inestable, orden dependiente ni aleatoriedad sin semilla.**
  *Por qué:* una prueba inestable que se vuelve a ejecutar hasta que pasa es peor que no tener prueba — erosiona la confianza en toda la suite.
- [ ] **Si esto corrige un bug, hay una prueba de regresión que lo habría detectado.**
  *Por qué:* de lo contrario, el mismo bug reaparece en ocho meses con una forma ligeramente distinta.
- [ ] **Los nombres de las pruebas describen el escenario, de modo que una prueba fallida te dice qué se ha roto sin abrir el archivo.**
  *Por qué:* `test_1()` fallando no te dice nada a las 11 de la noche; `rechaza_cantidad_negativa_en_checkout()` sí.

## 5. Rendimiento y Seguridad

- [ ] **No hay consultas N+1 evidentes ni bucles innecesarios sobre colecciones grandes.**
  *Por qué:* esto es invisible con diez filas de datos de prueba y catastrófico con diez millones en producción.
- [ ] **La entrada del usuario se valida y sanea antes de que toque algo sensible.**
  *Por qué:* «lo validaremos en el frontend» no es un límite de seguridad.
- [ ] **Los secretos, tokens y credenciales no están codificados en duro ni se registran en logs.**
  *Por qué:* una vez que un secreto llega al historial de control de versiones o a un agregador de logs, rotarlo es la única solución real — eliminar la línea no es suficiente.
- [ ] **Los nuevos endpoints o accesos a datos respetan las reglas de autorización existentes.**
  *Por qué:* una nueva funcionalidad que silenciosamente elude una comprobación de permisos existente es como ocurren los bugs de escalada de privilegios horizontal.
- [ ] **El cambio no introduce una nueva superficie de ataque sin una mitigación clara.**
  *Por qué:* las subidas de archivos, la deserialización de datos no confiables y el SQL en bruto son el origen de una enorme proporción de exploits reales.
- [ ] **El uso de memoria y recursos está acotado.**
  *Por qué:* una caché sin límite o una función recursiva sin caso base funciona bien en desarrollo y tumba producción bajo carga real.
- [ ] **Los datos de terceros — respuestas de API, webhooks, subidas — se tratan como no confiables.**
  *Por qué:* «viene de la API de nuestro propio socio» no es lo mismo que «es seguro confiar en ello sin validación».
- [ ] **Si esto toca un camino caliente, hay evidencia de que el rendimiento se ha tenido realmente en cuenta.**
  *Por qué:* un benchmark, una nota de perfilado, o incluso una oración de razonamiento supera a «se sentía bien en mi máquina».

## 6. Documentación

- [ ] **Las funciones, clases y endpoints públicos tienen documentación donde el «por qué» no es obvio por el nombre.**
  *Por qué:* un buen nombre reduce la necesidad de comentarios; no la elimina.
- [ ] **El README, los docs de la API o los de incorporación están actualizados si esto cambia cómo se usa el proyecto.**
  *Por qué:* la documentación desactualizada es peor que no tener documentación — desorienta activamente a la siguiente persona.
- [ ] **Los cambios con ruptura de compatibilidad se señalan explícitamente, no se entierran en el diff.**
  *Por qué:* nadie lee cada línea de cada PR; un cambio con ruptura merece una señal, no un juego de búsqueda del tesoro.
- [ ] **Los cambios en la configuración o en las variables de entorno están documentados.**
  *Por qué:* una nueva variable de entorno obligatoria sin documentar es un ticket de soporte garantizado de la siguiente persona que haga pull de main.
- [ ] **Si se añade una nueva dependencia o herramienta, hay una nota de una línea explicando por qué.**
  *Por qué:* evita que la siguiente persona tenga que descifrar la decisión a partir de un hash de commit.

## 7. Cumplimiento de Estándares

- [ ] **El cambio sigue la guía de estilo del equipo y los registros de decisiones arquitectónicas, si existen.**
  *Por qué:* una decisión que el equipo ya tomó no debería volver a debatirse en cada hilo de comentarios de PR.
- [ ] **Las comprobaciones de CI pasan — y has leído realmente por qué, no sólo que el indicador está en verde.**
  *Por qué:* un paso de CI inestable que resultó estar verde esta vez no es lo mismo que el código siendo correcto.
- [ ] **Los mensajes de commit siguen la convención del proyecto y son útiles por sí solos, fuera de contexto.**
  *Por qué:* `git blame` es más útil exactamente cuando no tienes ningún otro contexto — ese es el momento en que el mensaje de commit tiene que cargar con el peso.
- [ ] **Se respetan los fundamentos de accesibilidad en cualquier cambio orientado al usuario.**
  *Por qué:* las etiquetas, el contraste y la navegación por teclado no son «opcionales» — son la diferencia entre una funcionalidad que funciona para todos o sólo para algunos usuarios.

## 8. Consideraciones Finales

- [ ] **Estarías cómodo siendo avisado por este código a las 3 de la madrugada.**
  *Por qué:* esta es la mejor comprobación instintiva de «¿entiendo realmente lo que acabo de aprobar?»
- [ ] **El feedback que has dejado es sobre el código, no sobre la persona que lo escribió.**
  *Por qué:* «esta función está haciendo demasiado» invita a una conversación; «siempre lo complicas todo» invita a una defensa.
- [ ] **Si no has revisado algo completamente — un archivo generado, una librería de terceros — lo has dicho en lugar de aprobarlo en silencio.**
  *Por qué:* una aprobación debe significar lo que dice; dar el visto bueno silenciosamente a lo que has ojeado anula el propósito entero de la revisión.

---

**¿Quieres esto sin tener que desplazarte por un archivo markdown?** Usa la [versión interactiva](https://projekta2.github.io/pr-review-canvas/) — los mismos 51 ítems, una barra de progreso y una puntuación de «Preparación de la Revisión» por categoría.
