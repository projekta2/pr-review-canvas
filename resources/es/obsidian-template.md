---
title: Checklist de Revisión de PRs
tags: [revisión-código, checklist, ingeniería]
source: https://github.com/projekta2/pr-review-canvas
---

> [!info] Cómo usarlo
> Guarda esto como una nueva nota en tu vault (p. ej. `Plantillas/Checklist de Revisión de PRs.md`). Si usas el plugin Templater o el de Plantillas nativo, configúralo como plantilla para que se cree una copia nueva sin marcar por cada PR. Las tareas están escritas como `- [ ]` estándar para que funcionen con la búsqueda de tareas nativa de Obsidian y con el plugin Tasks si lo tienes instalado.

# 📋 Checklist de Revisión de PRs

## 1. Contexto y Propósito
- [ ] La descripción del PR indica claramente qué ha cambiado y por qué #contexto
- [ ] El PR enlaza con la incidencia, el ticket o la especificación correspondiente #contexto
- [ ] El tamaño del PR encaja con su alcance declarado #contexto
- [ ] El título es suficientemente específico como para ser útil en un registro de cambios #contexto
- [ ] Entiendes el problema que resuelve este PR antes de leer el código #contexto

## 2. Arquitectura y Diseño
- [ ] El cambio encaja en la arquitectura existente, o justifica desviarse de ella #arquitectura
- [ ] Las responsabilidades están en la capa o el módulo correcto #arquitectura
- [ ] No se introduce un patrón nuevo cuando uno existente ya resuelve el problema #arquitectura
- [ ] El acoplamiento está minimizado entre módulos no relacionados #arquitectura
- [ ] El nivel de abstracción es el adecuado para el problema #arquitectura
- [ ] Los nombres reflejan conceptos del dominio, no detalles de implementación #arquitectura
- [ ] Consistente con la forma en que se han resuelto problemas similares en el resto del código #arquitectura
- [ ] Las nuevas dependencias tienen una concesión justificada #arquitectura

## 3. Calidad del Código
- [ ] Las funciones hacen una sola cosa, y el nombre dice cuál es #calidad
- [ ] No hay código muerto, bloques comentados ni sentencias de depuración #calidad
- [ ] Los nombres son descriptivos sin ser verbosos #calidad
- [ ] El manejo de errores es explícito, no se traga en silencio #calidad
- [ ] No hay números ni cadenas mágicas sin una constante con nombre #calidad
- [ ] Se evita la duplicación, pero no a costa de la legibilidad #calidad
- [ ] El flujo de control es fácil de seguir #calidad
- [ ] El diff es revisable en alcance y tamaño #calidad
- [ ] Los comentarios explican el por qué, no el qué #calidad
- [ ] Los casos extremos están tratados de forma visible #calidad
- [ ] Sin dependencia de comportamiento implícito y frágil #calidad
- [ ] El formateo sigue las convenciones del proyecto #calidad

## 4. Pruebas
- [ ] El comportamiento nuevo tiene pruebas nuevas, no sólo las antiguas pasando #pruebas
- [ ] Las pruebas verifican comportamiento, no detalles de implementación #pruebas
- [ ] Al menos una prueba cubre el camino no feliz #pruebas
- [ ] Las pruebas son deterministas #pruebas
- [ ] Las correcciones de bugs incluyen una prueba de regresión #pruebas
- [ ] Los nombres de las pruebas describen el escenario #pruebas

## 5. Rendimiento y Seguridad
- [ ] Sin consultas N+1 evidentes ni bucles sobre colecciones grandes #seguridad
- [ ] La entrada del usuario se valida antes de tocar algo sensible #seguridad
- [ ] Los secretos y credenciales no están codificados en duro ni se registran en logs #seguridad
- [ ] Los nuevos endpoints respetan las reglas de autorización existentes #seguridad
- [ ] Sin nueva superficie de ataque sin una mitigación clara #seguridad
- [ ] El uso de memoria y recursos está acotado #seguridad
- [ ] Los datos de terceros se tratan como no confiables #seguridad
- [ ] Los cambios en caminos calientes muestran evidencia de que el rendimiento se consideró #seguridad

## 6. Documentación
- [ ] Las funciones/endpoints públicos tienen documentación donde la intención no es obvia #docs
- [ ] El README o los docs de la API se actualizan si el uso cambia #docs
- [ ] Los cambios con ruptura se señalan explícitamente #docs
- [ ] Los cambios de configuración/variables de entorno están documentados #docs
- [ ] Las nuevas dependencias tienen una nota de una línea sobre por qué #docs

## 7. Cumplimiento de Estándares
- [ ] Sigue la guía de estilo del equipo y los ADRs #estándares
- [ ] Las comprobaciones de CI pasan, y has leído por qué, no sólo que están en verde #estándares
- [ ] Los mensajes de commit son útiles fuera de contexto #estándares
- [ ] Los fundamentos de accesibilidad se respetan para cambios orientados al usuario #estándares

## 8. Consideraciones Finales
- [ ] Estarías cómodo siendo avisado por este código a las 3 de la madrugada #final
- [ ] El feedback es sobre el código, no sobre la persona #final
- [ ] Si no has revisado algo completamente, lo has dicho #final

---

> [!tip] Referencia completa
> Explicaciones para cada ítem, más una versión interactiva en vivo con puntuación de progreso, en [PR Review Canvas](https://github.com/projekta2/pr-review-canvas).
