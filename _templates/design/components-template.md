# Componentes — [Nombre del Proyecto]
> Inventario del design system exportado de Claude Design al cerrar Fase 5.
> Code: implementar cada componente según esta spec — variantes, estados y micro-interacciones incluidos. No recortar ni ampliar.

## Índice

| Componente | Variantes | Pantallas donde se usa |
|-----------|-----------|------------------------|
| [Button] | primary, secondary, ghost, danger | [todas] |
| [Card] | [...] | [...] |
| [Input] | [...] | [...] |

---

## [Nombre del componente]

**Descripción:** [qué es y para qué se usa]
**Referencia visual:** `prototype/[archivo]` — [pantalla(s)]

### Variantes
- **[variante 1]:** [cuándo se usa, diferencias visuales]
- **[variante 2]:** [...]

### Estados
| Estado | Spec |
|--------|------|
| Default | [descripción] |
| Hover | [cambio visual + transición, ej. "translateY(-2px), 150ms ease"] |
| Active/pressed | [...] |
| Focus | [anillo de foco — obligatorio para accesibilidad] |
| Disabled | [...] |
| Loading | [spinner/skeleton — spec] |
| Error | [...] |

### Micro-interacciones (según nivel de interactividad aprobado)
- [ej. "al agregar item: fade-in + slide 8px, 200ms"]

### Props/contenido dinámico
- [qué recibe: texto, icono, badge, etc.]

---

*(Repetir la sección por cada componente del inventario)*
