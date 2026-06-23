# Checklist de Revisión de PRs (importación para Notion)

> **Cómo importar:** En Notion, crea una nueva página y pega directamente este bloque de texto completo. Notion convierte automáticamente los encabezados `#`, las líneas `- [ ]` en bloques de tareas pendientes, y las líneas `>` en llamadas. Una vez pegado, convierte los encabezados de primer nivel en una base de datos de Notion si quieres una fila de checklist por PR.

---

# 📋 Checklist de Revisión de PRs

> Usa las listas desplegables de abajo para mantener cada categoría colapsable. Marca los ítems en cada revisión; duplica esta página para tu próximo PR si quieres una copia nueva cada vez en lugar de resetear las marcas.

## 1. Contexto y Propósito
- [ ] La descripción del PR indica claramente qué ha cambiado y por qué
- [ ] El PR enlaza con la incidencia, el ticket o la especificación correspondiente
- [ ] El tamaño del PR encaja con su alcance declarado
- [ ] El título es suficientemente específico como para ser útil en un registro de cambios
- [ ] Entiendes el problema que resuelve este PR antes de leer el código

## 2. Arquitectura y Diseño
- [ ] El cambio encaja en la arquitectura existente, o justifica desviarse de ella
- [ ] Las responsabilidades están en la capa o el módulo correcto
- [ ] No se introduce un patrón nuevo cuando uno existente ya resuelve el problema
- [ ] El acoplamiento está minimizado entre módulos no relacionados
- [ ] El nivel de abstracción es el adecuado para el problema
- [ ] Los nombres reflejan conceptos del dominio, no detalles de implementación
- [ ] Consistente con la forma en que se han resuelto problemas similares en el resto del código
- [ ] Las nuevas dependencias tienen una concesión justificada

## 3. Calidad del Código
- [ ] Las funciones hacen una sola cosa, y el nombre dice cuál es
- [ ] No hay código muerto, bloques comentados ni sentencias de depuración
- [ ] Los nombres son descriptivos sin ser verbosos
- [ ] El manejo de errores es explícito, no se traga en silencio
- [ ] No hay números ni cadenas mágicas sin una constante con nombre
- [ ] Se evita la duplicación, pero no a costa de la legibilidad
- [ ] El flujo de control es fácil de seguir
- [ ] El diff es revisable en alcance y tamaño
- [ ] Los comentarios explican el por qué, no el qué
- [ ] Los casos extremos están tratados de forma visible
- [ ] Sin dependencia de comportamiento implícito y frágil
- [ ] El formateo sigue las convenciones del proyecto

## 4. Pruebas
- [ ] El comportamiento nuevo tiene pruebas nuevas, no sólo las antiguas pasando
- [ ] Las pruebas verifican comportamiento, no detalles de implementación
- [ ] Al menos una prueba cubre el camino no feliz
- [ ] Las pruebas son deterministas
- [ ] Las correcciones de bugs incluyen una prueba de regresión
- [ ] Los nombres de las pruebas describen el escenario

## 5. Rendimiento y Seguridad
- [ ] Sin consultas N+1 evidentes ni bucles sobre colecciones grandes
- [ ] La entrada del usuario se valida antes de tocar algo sensible
- [ ] Los secretos y credenciales no están codificados en duro ni se registran en logs
- [ ] Los nuevos endpoints respetan las reglas de autorización existentes
- [ ] Sin nueva superficie de ataque sin una mitigación clara
- [ ] El uso de memoria y recursos está acotado
- [ ] Los datos de terceros se tratan como no confiables
- [ ] Los cambios en caminos calientes muestran evidencia de que el rendimiento se consideró

## 6. Documentación
- [ ] Las funciones/endpoints públicos tienen documentación donde la intención no es obvia
- [ ] El README o los docs de la API se actualizan si el uso cambia
- [ ] Los cambios con ruptura se señalan explícitamente
- [ ] Los cambios de configuración/variables de entorno están documentados
- [ ] Las nuevas dependencias tienen una nota de una línea sobre por qué

## 7. Cumplimiento de Estándares
- [ ] Sigue la guía de estilo del equipo y los ADRs
- [ ] Las comprobaciones de CI pasan, y has leído por qué, no sólo que están en verde
- [ ] Los mensajes de commit son útiles fuera de contexto
- [ ] Los fundamentos de accesibilidad se respetan para cambios orientados al usuario

## 8. Consideraciones Finales
- [ ] Estarías cómodo siendo avisado por este código a las 3 de la madrugada
- [ ] El feedback es sobre el código, no sobre la persona
- [ ] Si no has revisado algo completamente, lo has dicho

---

> 💡 Explicaciones completas para cada ítem, más una versión web interactiva con puntuación de progreso: [github.com/projekta2/pr-review-canvas](https://github.com/projekta2/pr-review-canvas)
