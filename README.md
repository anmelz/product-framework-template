# [Nombre del Proyecto]
> Creado desde el Product Development Framework Template v2.0.

## Setup rápido

### 1. Code (Fases 6, 7) — automático
Abre el tab Code apuntando a esta carpeta. Lee `.claude/rules/framework-rules.md` y `CLAUDE.md` automáticamente.

### 2. Cowork (Fases 1, 2, 3, 4, 8)
Cowork → New Project → selecciona esta carpeta → pega el contenido de `_context/framework.md` en las instrucciones del proyecto.

### 3. Design (Fase 5)
Usa Claude Design para wireframes, diseño visual y prototipado.

## Estructura


```

├── CLAUDE.md # Contexto técnico (generado en Fase 4) ├── PROGRESS.md # Estado actual del proyecto ├── .claude/ │ ├── settings.json # Permisos de Claude Code │ └── rules/ │ └── framework-rules.md # Reglas del framework (auto-leído por Code) ├── _context/ │ └── framework.md # Contexto del framework (auto-leído por Cowork) └── docs/ ├── artifact.html # Documento vivo del proyecto (generado en Fase 1) └── decisions/ # Log de decisiones técnicas

```

| Fase | Nombre | Herramienta | Modelo |
|------|--------|-------------|--------|
| 0 | Project Audit (proyectos existentes) | Cowork | Fable 5 |
| 1 | Investigación | Cowork | Fable 5 |
| 2 | Discovery & Definición | Cowork | Fable 5 |
| 3 | Análisis de Mercado | Cowork | Fable 5 |
| — | Gate · Presentación al Cliente | Usuario | — |
| 4 | Planificación Técnica | Cowork | Opus 4.8 |
| 5 | Diseño / UX | Design | Opus 4.8 |
| 6 | MVP | Code | Sonnet 5 |
| 7 | Desarrollo Completo | Code | Sonnet 5 |
| 8 | Post-Lanzamiento | Cowork + Code | Sonnet 5 |

*Product Development Framework v2.0*
