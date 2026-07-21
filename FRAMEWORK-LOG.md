# FRAMEWORK-LOG.md — Bitácora del framework
> Historial de decisiones y evolución del **Product Development Framework en sí** (meta-proyecto).
> ⚠️ **Este archivo NO se copia a proyectos de cliente** — bórralo al clonar el template.
> El `PROGRESS.md` de la raíz es la plantilla limpia que sí viaja con cada clon.

## Estado del framework

| Campo | Valor |
|-------|-------|
| **Versión** | v2.2 |
| **Repo** | https://github.com/anmelz/product-framework-template |

## Pendientes
1. Probar el framework end-to-end con un proyecto real — en curso (el usuario lo gestiona fuera de este proyecto); traer las fricciones de vuelta a este log.
2. Usuario: pegar `INSTRUCCIONES-COWORK.md` en las instrucciones del proyecto del framework en Cowork.

## Descartado / en pausa
- **Starter kit repo** — en pausa. Retomar tras cerrar el piloto, para basarlo en patrones reales.
- **Pipeline central y registro win/loss** — descartados explícitamente (decisión v2.1).
- **Calibración estimado vs. real en PROGRESS.md** — eliminada del template por decisión del usuario (2026-07-10).
- **Update semanal al cliente (ex-R8)** — regla eliminada del framework (2026-07-10).
- **Fricción git/OneDrive en Windows** — en segundo plano; el usuario la revisará (locks de `.git/index` y permisos de borrado, vistos en template y piloto).

## Incorporado desde proyectos reales
> Los gaps cubiertos en v2.1→v2.2 provienen de feedback de proyectos reales del usuario (documentados y no documentados en este log).

- Template `_templates/client-proposal-slides-template.html` — propuesta en slides, alternativa al formato scroll.
- Estándar del prototipo del Gate: sin tope de 3–5 pantallas; crecimiento controlado por R8 (Scope Creep).

## Log de sesiones

### 2026-07-10 — Actualización v2.1: gaps de proceso
- Template repo actualizado a v2.1 (`_context/framework.md`, `_templates/`, README) y commiteado por Code (c49ea31).
- Análisis comparativo del piloto Bandera Travels vs. proceso estándar (override bien ejecutado; scope creep del prototipo sin regla; archivos del piloto en v2.0).
- **Entornos**: local / staging / production (staging = "Preview" en Vercel). DBs separadas, migraciones local→staging→prod, secrets por entorno, servicios en modo test fuera de production, setup obligatorio al inicio de Fase 6.
- **Handoff Design → Code**: export a `docs/design/` (prototype/, design-tokens.md, components.md, flows.md); Code lee todo antes de la primera pantalla; stop si falta.
- **Nivel de interactividad (Fase 5)**: default dinámico; Claude propone nivel según industria (muy dinámico · moderado · sobrio), usuario confirma; baja al handoff.
- **Seguridad por diseño (R9)**: perfil por producto (Fase 4) + baseline continuo + verificación como criterio de salida de 6/7. Hallazgo crítico bloquea deploy.
- **Gate con/sin prototipo**: definición prototipo (visual, no funcional) vs. MVP (funcional); Claude propone con justificación (default: con), usuario confirma.

### 2026-07-10 — Auditoría de consistencia
- Meta-bitácora separada de la plantilla: nace este archivo; `PROGRESS.md` raíz vuelve a ser plantilla limpia.
- Numeración de reglas unificada **R1–R9** (canónica, idéntica en `_context/framework.md` y el artifact): R1 verificación · R2 redirección · R3 override · R4 input libre · R5 artifact fuente de verdad · R6 herramienta correcta · R7 datos verificados · R8 scope creep · R9 seguridad. Eliminado el update semanal.
- **Fase 8 definida**: monitoreo, mantenimiento, iteraciones (menores → Code; mayores → reiniciar desde Fase 2), soporte pactado en el SOW. Con criterios de salida.
- **Input de Fase 5**: Design recibe todo lo acumulado (artifact, CLAUDE.md, PROGRESS.md, prototipo del Gate como semilla, assets de marca).
- **No-go de Fase -1**: queda en su carpeta con `NO-GO.md` (BANT, motivo, fecha) y prefijo `[NO-GO]`.
- README corregido (estructura real, sin "auto-leído por Cowork"), footers unificados, duplicados a `_trash/`.

### 2026-07-10 — Sistema de agentes + aviso de modelo
- **Agentes** en `.claude/agents/` con modelo por frontmatter: `investigador` (Sonnet, Fases 1/3, fan-out), `implementador` (Sonnet, una feature por agente), `tester` (Sonnet), `revisor-seguridad` (Opus, obligatorio pre-cierre 6/7), `verificador-qa` (Sonnet, criterios R1, todas las fases). Orquestación: paralelizar lo independiente, serializar lo compartido; el hilo principal (orquestador) decide con el usuario.
- **Aviso de cambio de modelo**: línea "Modelo" en Status Check y en "¿Qué sigue?" — Claude no puede cambiar el modelo, avisa al usuario. Disponibles: Haiku 4.5 · Sonnet 5 · Opus 4.8 · Fable 5.

### 2026-07-10 — Recomendaciones ejecutadas + bump v2.2
- **Templates de handoff de diseño**: `_templates/design/` (design-tokens, components, flows).
- **`INSTRUCCIONES-COWORK.md` recreado** (meta-proyecto): rol de mantenedor, lectura de este log al iniciar, consistencia multi-archivo.
- **Piloto Bandera sincronizado**: framework.md, framework-rules, agents/, _templates/, footers y README a v2.2; nota de sync en su PROGRESS.md (advertencia: R8 cambió de significado).
- **Bump v2.1 → v2.2** en ambos repos: los cambios son sustanciales (R1–R9, Fase 8, agentes, entornos, seguridad); el número hace visible qué proyecto corre qué contrato.

### 2026-07-10 — Gap cubierto: Fase 0 con dos modos (adopción sobre repo existente)
- La Fase 0 original solo cubría migrar desde contexto (chats/docs). Nuevo **Modo B · Adopción** para proyectos con repo y código real que nunca corrieron el framework: overlay no destructivo de los archivos del framework al repo existente (sin clonar el template, sin sobrescribir archivos del proyecto), ingeniería inversa con Code (CLAUDE.md desde el stack/arquitectura/entornos REALES del código), auditoría R9 del código existente con `revisor-seguridad` (obligatoria), mapeo retroactivo de fases (entrada típica: Fase 7 u 8) y backfill obligatorio vs. opcional. Regla de entrada: si hay repo con código, es Modo B aunque existan chats (el código manda). **Artifact retroactivo con dos fuentes**: lo funcional/técnico del escaneo del código; lo de negocio (cliente, visión, mercado, decisiones) del contexto del usuario; lo irreconstruible se marca como gap (R7 — nunca inventar). En `_context/framework.md`, README (setup paso 0), `framework-rules.md` (rol de Code en adopción) y artifact.

### 2026-07-10 — Incidente: escrituras truncadas y regeneración
- Varias escrituras de la sesión de Cowork quedaron truncadas en disco (7 archivos, ambos repos). Code lo detectó en el integrity sweep pre-commit y NO commiteó — historial limpio en c49ea31 (v2.1).
- Cowork regeneró completos: `_context/framework.md`, `framework-rules.md`, `README.md`, `CLAUDE-template.md`, `PROGRESS-template.md`, este log, y reparó la cola de `product-framework.html` (cierre de tabla backfill + footer v2.2 + script togglePhase/openPhase/switchTab + cierre válido del documento).
- Aprendizaje de proceso: Code verifica integridad antes de commitear — mantener ese paso como estándar tras sesiones largas de Cowork.

---
*Product Development Framework — meta-log. No clonar a proyectos de cliente.*
