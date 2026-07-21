# Instrucciones — Proyecto del Framework (meta-proyecto)
> Pega este contenido en las instrucciones del proyecto de Cowork del **framework** (no de clientes).
> ⚠️ **No se clona a proyectos de cliente** — bórralo al clonar el template, junto con `FRAMEWORK-LOG.md`.

## Qué es este proyecto

Este es el proyecto del **Product Development Framework en sí** — aquí se mantiene, evoluciona y documenta el framework que el equipo usa para desarrollar soluciones para clientes. NO es un proyecto de cliente: no apliques las fases del framework a este repo.

## Al iniciar cada sesión

1. Lee `FRAMEWORK-LOG.md` — estado, pendientes y decisiones del framework.
2. Presenta un resumen breve: versión actual, piloto en curso, pendientes abiertos.

## Reglas de mantenimiento

- **Consistencia multi-archivo**: todo cambio al proceso se refleja en TODOS los archivos normativos que aplique: `_context/framework.md` (Cowork), `.claude/rules/framework-rules.md` (Code), `_templates/CLAUDE-template.md`, `_templates/PROGRESS-template.md`, `README.md` y `product-framework.html` (artifact visual). Un cambio a medias crea el drift que ya hemos tenido que corregir.
- **Numeración de reglas R1–R9 es canónica** — si cambia, actualizar framework.md y artifact a la vez.
- **`PROGRESS.md` de la raíz es plantilla limpia** — nunca escribir estado del meta-proyecto ahí; eso va en `FRAMEWORK-LOG.md`.
- **Cerrar cada sesión** registrando lo hecho en `FRAMEWORK-LOG.md` (sección Log de sesiones) y recordando commit/push.
- **Cambios de versión**: cambios sustanciales al proceso (reglas, fases, mecánicas) ameritan bump de versión y actualización de todos los footers.
- Los aprendizajes de proyectos piloto se traen aquí como entradas en FRAMEWORK-LOG antes de convertirse en cambios al template.

## Recursos

- Template repo: https://github.com/anmelz/product-framework-template
- Artifact del framework: `product-framework.html`

---
*Product Development Framework — instrucciones del meta-proyecto*
