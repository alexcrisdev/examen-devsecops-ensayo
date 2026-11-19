---
name: backlog-jira
description: Fase 2. Convierte docs/01-analisis.md en backlog ágil para Jira - épicas, historias de usuario con criterios Gherkin, story points, prioridad y sprints - en docs/02-backlog.md y un CSV importable a Jira (docs/jira-import.csv).
---

# Backlog para Jira

## Reglas
- Épicas `EP-01..` agrupadas por funcionalidad (ej. Autenticación y roles, módulo X, Reportes, DevSecOps).
  Incluye SIEMPRE una épica **DevSecOps / Infraestructura** (pipeline CI, seguridad, despliegue, monitoreo).
- Historias `HU-01..` formato: **Como** <rol> **quiero** <acción> **para** <beneficio>.
- Cada HU: 2-4 criterios de aceptación en Gherkin (Dado/Cuando/Entonces), al menos uno de seguridad
  (ej. "Dado un usuario sin rol X, cuando intenta..., entonces recibe acceso denegado").
- Story points Fibonacci (1,2,3,5,8). Prioridad: Highest/High/Medium/Low. Etiqueta `seguridad` si aplica.
- Definition of Done común (copiar al inicio del backlog): pruebas en verde, pipeline verde,
  revisión de seguridad, desplegado en staging, criterios cumplidos.
- Sprints: Sprint 0 (setup DevSecOps: repo, pipeline, Supabase, Vercel), Sprint 1 (núcleo MVP),
  Sprint 2 (resto + reportes). Muestra objetivo y capacidad de cada sprint.
- Trazabilidad: tabla RF → HU → épica. Actualiza la columna HU de docs/01-analisis.md.

## docs/02-backlog.md
DoD, tabla de épicas, HU completas por épica, plan de sprints, matriz de trazabilidad.

## docs/jira-import.csv (UTF-8, coma, comillas dobles)
Columnas exactas:
`Issue Id,Issue Type,Summary,Description,Parent,Priority,Story Points,Labels,Sprint`
- Épicas: Issue Type `Epic`, Issue Id `1..n`, Parent vacío.
- Historias: Issue Type `Story`, Parent = Issue Id de su épica, Description = "Como... quiero... para..."
  + criterios separados por `\n`. Labels separadas por espacio.
- Subtareas opcionales: Issue Type `Sub-task`, Parent = Issue Id de la HU.
- Indica al usuario: Jira → Configuración del proyecto / Sistema → Importación externa → CSV,
  mapear `Issue Id` y `Parent` (en proyectos team-managed, `Parent` enlaza a la épica). Los sprints
  conviene crearlos antes en el tablero con el mismo nombre que la columna Sprint.
