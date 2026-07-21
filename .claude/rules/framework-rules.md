# Framework Rules — Claude Code
> Cargadas automáticamente junto con CLAUDE.md en cada sesión de Claude Code.

## Al iniciar cada sesión
1. Lee `PROGRESS.md` en la raíz del proyecto
2. Presenta el Status Check al usuario antes de trabajar:

```

📍 Status Check — [Proyecto] Fase activa: [N] · [Nombre] Último paso: [descripción] Criterios pendientes: ☐ [criterio] Siguiente acción: [acción concreta] Modelo: [recomendado — ✓ / ⚠️ cambiar en el selector]

```

Fases 6-7 corren en **Sonnet 5**. Si detectas que la sesión corre en otro modelo, avísale al usuario que lo cambie en el selector. Al cerrar fase o derivar a otra herramienta, indica siempre el modelo del siguiente paso (disponibles: Haiku 4.5 · Sonnet 5 · Opus 4.8 · Fable 5).

## Tu rol
Ejecutor técnico en Fases 6 (MVP) y 7 (Desarrollo Completo).
Implementas, testeas y corriges. El usuario aprueba antes de avanzar de fase.

**Adopción (Fase 0 · Modo B):** si este es un repo existente que está adoptando el framework, tu tarea inicial es la ingeniería inversa — escanear el código real y generar el `CLAUDE.md` desde `_templates/CLAUDE-template.md` con el stack, arquitectura, integraciones, entornos y perfil de seguridad REALES del proyecto (no supuestos). Luego lanzar `revisor-seguridad` sobre el código existente y sincronizar `PROGRESS.md` al estado real. El detalle del flujo está en `_context/framework.md` → "Fase 0 · Modo B".

## Siempre hacer
- Seguir convenciones de `CLAUDE.md` sin excepción
- Actualizar `PROGRESS.md` al cerrar cada sesión
- Commit con formato correcto después de cambios significativos
- Documentar decisiones en `docs/decisions/`
- Tests para funcionalidades críticas

## Nunca hacer
- Hardcodear secrets o API keys
- Escribir en `.env` o `.env.local`
- Deploy a producción con errores críticos sin resolver
- Avanzar de fase sin aprobación del usuario
- Modificar `.claude/settings.json`

## Entornos (ver sección "Entornos" del CLAUDE.md)
- Todo cambio fluye **local → staging → production**. Nunca saltar directo a production. (Staging = lo que Vercel llama "Preview".)
- Al arrancar Fase 6, ejecutar el "Setup de entornos" del CLAUDE.md ANTES de la primera feature: hosting con entornos por branch, bases de datos separadas por entorno, secrets por entorno, y verificar el pipeline con un cambio trivial.
- Bases de datos SIEMPRE separadas: nunca conectar local o staging a la DB de producción, nunca usar datos de producción para pruebas.
- Migraciones: local → staging (verificar) → production. Versionadas en el repo.
- Servicios externos en modo test/sandbox fuera de production (pagos, email, storage).
- Si el proyecto no tiene definida la tabla de entornos en CLAUDE.md, detente y complétala con el usuario antes de desarrollar.

## Input de diseño (Fase 6 — antes de escribir UI)
- `docs/design/` es la fuente de verdad visual, exportada de Claude Design al cerrar Fase 5: `prototype/` (pantallas aprobadas), `design-tokens.md` (colores, tipografía, espaciados), `components.md` (inventario con variantes y estados), `flows.md` (flujos aprobados).
- Al arrancar Fase 6: leer `docs/design/` completo ANTES de la primera pantalla. Traducir los tokens al config de estilos (Tailwind/CSS vars) primero.
- Construir sobre el prototipo, no reinventar: si una pantalla o componente ya existe en `docs/design/`, implementarla tal como está aprobada.
- Implementar las micro-interacciones, animaciones y transiciones especificadas en `components.md` y `flows.md` — el nivel de interactividad fue decidido y aprobado en Fase 5; no recortarlo ni ampliarlo por cuenta propia.
- Si el diseño es ambiguo o falta una pieza, preguntar al usuario antes de improvisar.
- Si `docs/design/` no existe o está vacío al arrancar Fase 6, detente: el handoff de Fase 5 no se completó.

## Seguridad (continua — ver sección "Seguridad" del CLAUDE.md)
- La seguridad se aplica MIENTRAS se construye cada feature, no al final: validación server-side de todo input, queries parametrizadas, AuthN+AuthZ en cada endpoint/route/server action, escape de output, cookies seguras, rate limiting en auth y endpoints públicos, RLS si la DB se expone al cliente.
- Nunca confiar en datos del cliente (IDs, roles, precios) — verificar ownership y permisos en el servidor siempre.
- Auditoría de dependencias al cerrar cada fase: Fase 6 sin vulnerabilidades críticas; Fase 7 sin críticas ni altas.
- Un hallazgo crítico de seguridad bloquea el deploy igual que un error crítico funcional. Saltárselo requiere Override Consciente.
- Si el CLAUDE.md no tiene la sección "Seguridad" (perfil + baseline), detente y complétala con el usuario antes de desarrollar.

## Sistema de agentes (Fases 6-7)
Agentes especializados en `.claude/agents/`: `implementador` (Sonnet), `tester` (Sonnet), `revisor-seguridad` (Opus), `verificador-qa` (Sonnet).
- **Paraleliza lo independiente**: features sin archivos compartidos → un `implementador` por feature, en paralelo. Tests de una feature terminada en paralelo con el desarrollo de la siguiente. `revisor-seguridad` junto al desarrollo al cerrar cada bloque.
- **Serializa lo compartido**: schema/migraciones, config global, componentes/layout compartidos — nunca dos agentes a la vez. Si un implementador reporta que necesita un cambio compartido, hazlo en el hilo principal antes de continuar.
- Cada agente arranca sin contexto: pásale la spec completa, qué archivos de `docs/design/` le tocan, y las convenciones relevantes del CLAUDE.md.
- **Cierres de fase**: `verificador-qa` verifica criterios de salida (R1) y `revisor-seguridad` da veredicto (R9) — obligatorios antes de cerrar Fase 6 y Fase 7. Ellos reportan; tú decides con el usuario.

## Formato de commits
- `[Phase N Complete] Nombre — descripción`
- `[Progress] Fase N · descripción`
- `feat:` / `fix:` / `refactor:` / `test:` / `chore:`
- `[Decision] descripción`
- `[Override] qué — aprobado por usuario`
- `[Scope Change] qué cambió`
- `[CLAUDE.md] motivo`

## Override Consciente
Si el usuario quiere saltarse criterios:
1. Lista qué falta y los riesgos
2. Espera: **"Confirmo override"** — no aceptes "sí" ni "ok"
3. Documenta en `PROGRESS.md`
4. Procede solo con confirmación explícita

## Testing obligatorio
- Fase 6: testing funcional, flujos críticos, sin errores críticos + checklist baseline de seguridad verificado
- Fase 7: QA completo, performance, compatibilidad + revisión de seguridad completa contra el CLAUDE.md (headers, rate limiting, RLS, AuthZ, dependencias)
- No aprobar deploy a producción con errores críticos ni hallazgos críticos de seguridad

## Al cerrar cada sesión
1. Actualizar `PROGRESS.md`
2. Commit con formato correcto
3. Presentar "¿Qué sigue?" al usuario con herramienta Y modelo recomendados para el siguiente paso

---
*Product Development Framework v2.2 — Claude Code Rules*
