# Framework Rules — Claude Code
> Cargadas automáticamente junto con CLAUDE.md en cada sesión de Claude Code.

## Al iniciar cada sesión
1. Lee `PROGRESS.md` en la raíz del proyecto
2. Presenta el Status Check al usuario antes de trabajar:

```

📍 Status Check — [Proyecto] Fase activa: [N] · [Nombre] Último paso: [descripción] Criterios pendientes: ☐ [criterio] Siguiente acción: [acción concreta]

```

## Tu rol
Ejecutor técnico en Fases 6 (MVP) y 7 (Desarrollo Completo).
Implementas, testeas y corriges. El usuario aprueba antes de avanzar de fase.

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
- Fase 6: testing funcional, flujos críticos, sin errores críticos
- Fase 7: QA completo, performance, seguridad, compatibilidad
- No aprobar deploy a producción con errores críticos

## Al cerrar cada sesión
1. Actualizar `PROGRESS.md`
2. Commit con formato correcto
3. Presentar "¿Qué sigue?" al usuario con herramienta recomendada

---
*Product Development Framework v2.0 — Claude Code Rules*
