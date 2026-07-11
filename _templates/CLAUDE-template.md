# CLAUDE.md — [Nombre del Proyecto]
> Generado automáticamente por Claude al cerrar la Fase 4 · Planificación Técnica.
> Claude Code lee este archivo al inicio de cada sesión de desarrollo.
> Actualizar con tag `[CLAUDE.md]` cuando cambien decisiones técnicas.

---

## Proyecto

| Campo | Valor |
|-------|-------|
| **Nombre** | [Nombre del producto] |
| **Cliente** | [Nombre del cliente] |
| **Descripción** | [Una línea describiendo qué hace el producto] |
| **Estado** | [Fase actual del framework] |
| **Repositorio** | [URL del repo] |

---

## Stack tecnológico

| Capa | Tecnología | Versión | Notas |
|------|-----------|---------|-------|
| **Frontend** | [Next.js / React / Vue / etc.] | [versión] | [notas si aplica] |
| **Styling** | [Tailwind CSS / etc.] | [versión] | |
| **Backend** | [Next.js API / Express / FastAPI / etc.] | [versión] | |
| **Base de datos** | [PostgreSQL / MongoDB / etc.] | [versión] | |
| **ORM / Query** | [Prisma / Drizzle / etc.] | [versión] | |
| **Auth** | [NextAuth / Clerk / Supabase Auth / etc.] | [versión] | |
| **Storage** | [S3 / Cloudinary / etc.] | [versión] | |
| **Hosting** | [Vercel / Railway / etc.] | — | |
| **CI/CD** | [GitHub Actions / etc.] | — | |

---

## Arquitectura

### Estructura de carpetas
```
[nombre-proyecto]/
├── src/
│   ├── app/              # [descripción]
│   ├── components/       # [descripción]
│   ├── lib/              # [descripción]
│   ├── hooks/            # [descripción]
│   └── types/            # [descripción]
├── docs/
│   ├── artifact.html     # Artifact central del proyecto
│   └── decisions/        # Log de decisiones técnicas
├── CLAUDE.md             # Este archivo
├── PROGRESS.md           # Estado del framework
└── [otros archivos config]
```

### Módulos principales
| Módulo | Descripción | Ruta |
|--------|-------------|------|
| [Módulo 1] | [Qué hace] | `src/[ruta]` |
| [Módulo 2] | [Qué hace] | `src/[ruta]` |
| [Módulo 3] | [Qué hace] | `src/[ruta]` |

### Flujo de datos
[Descripción breve del flujo principal: cliente → API → DB → respuesta]

---

## Variables de entorno

> ⚠️ Nunca hardcodear valores. Todos los secrets van en `.env.local` (desarrollo) y en las variables del hosting (producción).

```bash
# Requeridas
DATABASE_URL=
NEXTAUTH_SECRET=
NEXTAUTH_URL=

# APIs externas
[NOMBRE_API]_KEY=

# Storage
[STORAGE_SERVICE]_URL=
[STORAGE_SERVICE]_KEY=
```

---

## Convenciones de código

### Naming
- Componentes React: `PascalCase` (ej: `UserCard.tsx`)
- Funciones y variables: `camelCase` (ej: `getUserById`)
- Archivos de utilidades: `kebab-case` (ej: `format-date.ts`)
- Constantes: `UPPER_SNAKE_CASE` (ej: `MAX_RETRY_COUNT`)
- Tipos e interfaces: `PascalCase` con prefijo `T` o `I` (ej: `TUser`, `IApiResponse`)

### Estilo de código
- [TypeScript estricto / JavaScript / etc.]
- Prettier para formateo — config en `.prettierrc`
- ESLint para linting — config en `.eslintrc`
- [Otras convenciones específicas del proyecto]

### Git
- Branches: `feature/nombre`, `fix/nombre`, `chore/nombre`
- Commits: seguir los tags del framework para cambios de proceso, convencional para código
  - `feat:`, `fix:`, `chore:`, `docs:`, `test:`
- PRs: requerir review antes de merge a main

---

## Integraciones

| Servicio | Propósito | Documentación |
|---------|-----------|--------------|
| [Servicio 1] | [Para qué se usa] | [URL docs] |
| [Servicio 2] | [Para qué se usa] | [URL docs] |

---

## Reglas para Claude Code

### Siempre hacer:
- Leer este archivo al inicio de cada sesión
- Seguir las convenciones de naming definidas arriba
- Escribir tests para funcionalidades críticas
- Documentar funciones complejas con JSDoc/docstrings
- Verificar variables de entorno antes de hacer commit
- Actualizar PROGRESS.md al cerrar un paso o sesión

### Nunca hacer:
- Hardcodear secrets, API keys o credenciales
- Hacer cambios en producción sin pasar por staging primero
- Modificar la estructura de la base de datos sin documentar la migración
- Hacer commit de archivos `.env` o `.env.local`
- Cambiar el stack o la arquitectura sin aprobación del usuario

### Ante errores críticos:
1. Documentar el error con contexto completo
2. Proponer solución antes de implementar
3. Si el error afecta decisiones de arquitectura, escalar al usuario

---

## Estado del desarrollo

### Completado
- [x] [Funcionalidad o módulo completado]
- [x] [Funcionalidad o módulo completado]

### En progreso
- [ ] [Funcionalidad actual]

### Pendiente
- [ ] [Funcionalidad pendiente]
- [ ] [Funcionalidad pendiente]

---

## Decisiones técnicas registradas

| Fecha | Decisión | Alternativas consideradas | Motivo |
|-------|----------|--------------------------|--------|
| [fecha] | [Qué se decidió] | [Otras opciones] | [Por qué] |

---

*Generado por el Product Development Framework v2.0 — Fase 4 · Planificación Técnica*
