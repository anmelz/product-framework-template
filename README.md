# [Nombre del Proyecto]
> Creado desde el Product Development Framework Template v2.2.

## Setup rápido

### 0. Al clonar este template
Borra `FRAMEWORK-LOG.md`, `INSTRUCCIONES-COWORK.md` y `_trash/` si existen — son internos del repo del framework, no viajan con proyectos de cliente.

### 1. Code (Fases 6, 7) — automático
Abre el tab Code apuntando a esta carpeta. Lee `.claude/rules/framework-rules.md` y `CLAUDE.md` automáticamente.

### 2. Cowork (Fases -1, 1, 2, 3, 4, 8) — un paso manual
Cowork → New Project → selecciona esta carpeta → **pega el contenido de `_context/framework.md` en las instrucciones del proyecto**. (Cowork no lee archivos de instrucciones automáticamente.)

### 3. Design (Fase 5)
Usa Claude Design para wireframes, diseño visual y prototipado. Al arrancar, dale todo lo acumulado del proyecto (artifact, CLAUDE.md, prototipo del Gate, assets de marca). Al cerrar, exporta el handoff a `docs/design/` — Code construye desde ahí.

## Estructura

```
[nombre-proyecto]/
├── CLAUDE.md                  # Contexto técnico (generado en Fase 4)
├── PROGRESS.md                # Estado actual del proyecto
├── .claude/
│   ├── settings.json          # Permisos de Claude Code
│   ├── rules/
│   │   └── framework-rules.md # Reglas del framework (auto-leído por Code)
│   └── agents/                # Agentes especializados (paralelización)
│       ├── investigador.md        # Fases 1/3 · fan-out de investigación (Sonnet)
│       ├── implementador.md       # Fases 6/7 · una feature por agente (Sonnet)
│       ├── tester.md              # Fases 6/7 · tests de features terminadas (Sonnet)
│       ├── revisor-seguridad.md   # Fases 6/7 · auditoría R9 pre-cierre (Opus)
│       └── verificador-qa.md      # Todas · verificación de criterios R1 (Sonnet)
├── _context/
│   └── framework.md           # Instrucciones para Cowork (se pegan manualmente)
├── _templates/
│   ├── CLAUDE-template.md     # Base del CLAUDE.md (Fase 4)
│   ├── PROGRESS-template.md   # Base del PROGRESS.md
│   ├── client-proposal-template.html        # Propuesta formato scroll
│   ├── client-proposal-slides-template.html # Propuesta formato slides
│   ├── propuesta-comercial-template.md      # Propuesta en markdown
│   ├── sow-template.md        # Statement of Work (post-Gate)
│   └── design/                # Esqueletos del handoff de Fase 5
│       ├── design-tokens-template.md
│       ├── components-template.md
│       └── flows-template.md
└── docs/
    ├── artifact.html          # Documento vivo del proyecto (Fase 1)
    ├── design/                # Handoff de Fase 5: prototype/, design-tokens.md, components.md, flows.md
    └── decisions/             # Log de decisiones técnicas
```

## Las fases

| Fase | Nombre | Herramienta | Modelo |
|------|--------|-------------|--------|
| -1 | Calificación (30 min) | Cowork | Sonnet 5 |
| 0 | Project Audit (proyectos existentes) | Cowork | Fable 5 |
| 1 | Investigación | Cowork | Fable 5 |
| 2 | Discovery & Definición | Cowork | Fable 5 |
| 3 | Análisis de Mercado | Cowork | Fable 5 |
| — | Gate · Propuesta (+ Prototipo) | Usuario | — |
| 4 | Planificación Técnica | Cowork | Opus 4.8 |
| 5 | Diseño / UX | Design | Opus 4.8 |
| 6 | MVP | Code | Sonnet 5 |
| 7 | Desarrollo Completo | Code | Sonnet 5 |
| 8 | Post-Lanzamiento | Cowork + Code | Sonnet 5 |

*Product Development Framework v2.2*
