# [Nombre del Proyecto]
> Creado desde el Product Development Framework Template v2.0.

## Setup rápido

### 1. Code (Fases 6, 7) — automático
Abre el tab Code apuntando a esta carpeta. Lee `.claude/rules/framework-rules.md` y `CLAUDE.md` automáticamente.

### 2. Cowork (Fases 1, 3)
Abre Cowork → New Project → selecciona la carpeta del proyecto.
Lee `_context/framework.md` y `PROGRESS.md` automáticamente.

### 3. Chat (Fases 2, 4, 8) — único paso manual
App de Claude → tab Chat → Projects → New Project → Settings → Project Instructions → pega el `system-prompt.md` del framework.

## Estructura


```

├── CLAUDE.md # Contexto técnico (generado en Fase 4) ├── PROGRESS.md # Estado actual del proyecto ├── .claude/ │ ├── settings.json # Permisos de Claude Code │ └── rules/ │ └── framework-rules.md # Reglas del framework (auto-leído por Code) ├── _context/ │ └── framework.md # Contexto del framework (auto-leído por Cowork) └── docs/ ├── artifact.html # Documento vivo del proyecto (generado en Fase 1) └── decisions/ # Log de decisiones técnicas

```

| Fase | Herramienta | Modelo |
|------|-------------|--------|
| 1 · Investigación | Cowork | Claude Fable 5 |
| 2 · Discovery | Chat | Claude Fable 5 |
| 3 · Análisis de Mercado | Cowork | Claude Fable 5 |
| 4 · Planificación Técnica | Chat | Claude Opus 4.8 |
| 5 · Diseño / UX | Design | Claude Opus 4.8 |
| 6 · MVP | Code | Claude Sonnet 5 |
| 7 · Desarrollo Completo | Code | Claude Sonnet 5 |
| 8 · Post-Lanzamiento | Chat / Code | Claude Sonnet 5 |

*Product Development Framework v2.0*
