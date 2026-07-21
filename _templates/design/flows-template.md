# Flujos de Usuario — [Nombre del Proyecto]
> Flujos aprobados en Fase 5, exportados de Claude Design.
> Code: implementar cada flujo completo, incluyendo estados vacíos, de error y transiciones.

## Índice de flujos

| # | Flujo | Prioridad | Pantallas involucradas |
|---|-------|-----------|------------------------|
| 1 | [ej. Registro y onboarding] | Core | [lista] |
| 2 | [...] | [Core / Secundario] | [...] |

---

## Flujo [N] · [Nombre]

**Objetivo del usuario:** [qué quiere lograr]
**Referencia visual:** `prototype/[archivos]`

### Camino feliz
1. **[Pantalla origen]** → [acción del usuario] → **[Pantalla destino]**
   - Transición: [según nivel de interactividad — ej. "slide lateral 300ms" / "corte directo"]
2. [...]

### Estados alternos
| Situación | Comportamiento |
|-----------|----------------|
| Estado vacío ([pantalla]) | [qué se muestra: ilustración, mensaje, CTA] |
| Error de [validación/red/servidor] | [mensaje, dónde aparece, cómo se recupera] |
| Carga | [skeleton / spinner / optimistic UI] |
| Sin permisos / sesión expirada | [redirección o mensaje] |

### Reglas de negocio del flujo
- [ej. "no se puede avanzar sin X", "el precio se recalcula al cambiar Y"]

---

*(Repetir la sección por cada flujo del índice)*
