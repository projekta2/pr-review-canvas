# Plantilla de Pull Request — Avanzada

> Para cambios complejos, de alto riesgo o entre equipos — migraciones, cambios con ruptura de API, cualquier cosa que toque autenticación, facturación o infraestructura. Para cambios cotidianos, usa [`pr-template.md`](pr-template.md); ésta es intencionadamente más pesada.

## Resumen

¿Qué hace este PR, y por qué necesita el escrutinio adicional que justificó usar esta plantilla?

## Contexto

- Incidencia / ticket / RFC: [enlace]
- PRs relacionados (si esto forma parte de una serie): [enlaces]
- Partes interesadas que deben estar al tanto: [equipo/persona — y por qué]

## Problema

¿Qué estaba roto, faltaba o era arriesgado antes de este cambio? Incluye suficiente detalle para que alguien sin el trasfondo entienda la motivación.

## Solución

¿Qué enfoque has tomado, y qué alternativas has considerado y descartado? Un revisor que conoce el código preguntará «¿por qué no X?» — respóndelo aquí antes de que tenga que hacerlo.

| Alternativa considerada | Por qué se descartó |
|---|---|
| [Opción A] | [Razón] |
| [Opción B] | [Razón] |

## Alcance del cambio

- **Sistemas/servicios afectados:** [lista]
- **Migraciones de datos implicadas:** [sí/no — enlaza la migración si es que sí]
- **Compatibilidad hacia atrás:** [¿hay ruptura? ¿para quién?]
- **Feature flag / plan de despliegue:** [nombre del flag, estrategia de porcentaje de despliegue, o «sin flag, despliegue directo porque...»]

## Cómo probarlo

1. [Pasos para reproducirlo en local]
2. [Pasos de verificación en staging]
3. [Qué métricas/dashboards vigilar tras el despliegue]

## Evaluación de riesgos

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| [p. ej. «La migración bloquea la tabla de pedidos»] | [Baja/Media/Alta] | [Baja/Media/Alta] | [p. ej. «Ejecutar en ventana de bajo tráfico, probado con datos a escala de staging»] |

## Plan de rollback

Si hay que revertir esto en producción, ¿cuál es el procedimiento real? ¿Es suficiente con revertir el despliegue, o la migración de datos necesita una migración inversa por separado?

## Checklist (autor)

- [ ] Lo he probado con datos a escala de producción, no sólo con unas pocas filas locales
- [ ] Tengo un plan de rollback que no depende de recordar detalles bajo presión
- [ ] He notificado a las partes interesadas indicadas antes de hacer el merge, no después
- [ ] Hay monitorización/alertas en su lugar para el nuevo comportamiento
- [ ] He documentado el cambio con ruptura (si lo hay) en el registro de cambios y he notificado a los consumidores afectados
- [ ] Alguien ajeno a mi equipo inmediato lo ha revisado, si cruza los límites de un equipo
