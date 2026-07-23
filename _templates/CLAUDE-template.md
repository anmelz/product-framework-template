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
│   ├── design/           # Handoff de Fase 5: prototype/, design-tokens.md, components.md, flows.md — fuente de verdad visual
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

## Entornos

> Definidos en Fase 4. Todo desarrollo fluye **local → staging → production**. Ningún cambio llega a production sin haber pasado por los entornos anteriores.
> Nota de nomenclatura: staging es lo que Vercel llama "Preview" — mismo concepto, un entorno de verificación separado de production. Aquí lo llamamos siempre staging.

| Entorno | Propósito | URL | Base de datos | Deploy |
|---------|-----------|-----|---------------|--------|
| **Local** | Desarrollo diario | `localhost:[puerto]` | [DB local / rama dev de la DB] | Manual (`npm run dev`) |
| **Staging** | Verificación pre-producción: deploys por PR/branch, QA y demos al cliente | [URL de staging / auto-generada por PR] | [DB de staging — separada] | Automático por PR o al merge a `[branch]` |
| **Production** | Usuarios reales | [URL de producción] | [DB de producción — separada] | [Automático al merge a `main` / manual con aprobación] |

### Reglas de entornos
- **Bases de datos separadas por entorno.** Production tiene su propia DB; staging usa otra (o ramas de DB si el proveedor lo soporta, ej. Neon/Supabase/PlanetScale branching). Local usa DB local o una rama de desarrollo. NUNCA apuntar local o staging a la DB de producción.
- **Migraciones:** se prueban primero en local, luego se aplican a staging, y solo después de verificarlas ahí se aplican a production. Toda migración queda versionada en el repo.
- **Datos:** production nunca se usa como fuente de datos de prueba. Staging usa datos seed o copias anonimizadas.
- **Secrets por entorno:** cada entorno tiene sus propias keys (API keys de test vs. live, ej. Stripe test/live). Un secret de production nunca se usa en local ni staging.
- **Servicios externos:** usar modo test/sandbox de cada integración (pagos, email, storage) en local y staging; modo live solo en production.
- **Flujo de promoción:** feature branch (local) → PR con deploy de staging → QA → merge/promote a production. Los criterios de Fase 6 exigen MVP verificado en staging; los de Fase 7 exigen QA completo antes de production.

### Setup de entornos (Fase 6, antes de la primera feature)
1. Configurar el hosting con los entornos y sus branches correspondientes
2. Crear las bases de datos separadas (o ramas de DB) y registrar sus URLs en los secrets de cada entorno
3. Configurar las variables de entorno por entorno en el hosting (nunca en el repo)
4. Verificar el pipeline completo con un cambio trivial: local → staging → production
5. Documentar las URLs resultantes en la tabla de arriba

---

## Build Order — secuencia de construcción

> Definido en Fase 4. **Criterio de calidad: una instancia de Code SIN contexto previo debe poder construir el producto siguiendo esta lista, en orden, sin hacer preguntas.** El orquestador recorta specs de aquí para cada `implementador`.

| # | Paso | Entregable | Depende de |
|---|------|-----------|------------|
| 0 | Setup de entornos (ver sección Entornos) | Pipeline local→staging→production verificado con cambio trivial | — |
| 1 | Config de estilos desde `docs/design/design-tokens.md` | Tailwind config / CSS vars con los tokens aprobados | 0 |
| 2 | [Schema de DB + migración inicial] | [Tablas base migradas en local y staging] | 0 |
| 3 | [Auth: registro / login / sesión / roles] | [Flujo de auth completo y protegido] | 2 |
| 4 | [Layout base + navegación] | [Shell de la app según prototype/] | 1 |
| 5 | [Feature core 1 — nombre] | [Funcional con tests] | 3, 4 |
| 6 | [Feature core 2 — nombre] | [Funcional con tests] | [depende] |
| … | [una fila por bloque constructivo, en orden de dependencias] | | |
| N | Verificación de cierre de Fase 6 | `verificador-qa` + `revisor-seguridad` en verde | todos |

### Reglas del Build Order
- Los pasos que tocan **archivos compartidos** (schema, config global, layout) los ejecuta el hilo principal, serializados. Los pasos independientes entre sí se reparten a `implementador` en paralelo.
- Cada paso cierra con su verificación (build pasa + tests del paso) antes de arrancar el siguiente que dependa de él.
- No improvisar el orden ni agregar pasos no listados — un paso nuevo es un cambio al plan (documentar, y si expande scope: R8).

---

## Variables de entorno

> ⚠️ Nunca hardcodear valores. Local usa `.env.local` (git-ignored); staging y production usan las variables del hosting, configuradas por entorno. Cada entorno tiene sus propios valores — especialmente `DATABASE_URL` y las keys de servicios externos (test vs. live).

```bash
# Requeridas (valores distintos por entorno)
DATABASE_URL=            # DB local / staging / production — según el entorno
NEXTAUTH_SECRET=
NEXTAUTH_URL=            # localhost / URL staging / URL production

# APIs externas (keys de test en local/staging, live solo en production)
[NOMBRE_API]_KEY=

# Storage
[STORAGE_SERVICE]_URL=
[STORAGE_SERVICE]_KEY=
```

---

## Seguridad

> Definido en Fase 4. La seguridad se aplica **mientras se construye**, no como parche al final. Todo hallazgo crítico bloquea el deploy igual que un error funcional crítico.

### Perfil de seguridad del producto

| Campo | Valor |
|-------|-------|
| **Sensibilidad de datos** | [PII / datos de pago / datos de salud / datos internos / público] |
| **Modelo de auth** | [email+password / OAuth / SSO / magic link — y roles: admin, usuario, etc.] |
| **Superficie de ataque** | [web pública / API pública / solo interna / móvil] |
| **Requisitos específicos** | [PCI si hay pagos, protección de menores, regulación local, etc. — o "ninguno especial"] |

### Baseline de seguridad (aplica SIEMPRE, en todo producto)

- **Validación de inputs:** todo input del usuario se valida y sanitiza **en el servidor** (los checks del cliente son solo UX). Queries siempre parametrizadas / vía ORM — nunca concatenar SQL.
- **AuthN + AuthZ en cada endpoint:** toda ruta, API route o server action verifica sesión Y permisos (ownership/rol) en el servidor. Nunca confiar en lo que manda el cliente (IDs, roles, precios).
- **XSS y CSRF:** escape de output por defecto (no `dangerouslySetInnerHTML` sin sanitizar), tokens CSRF en mutaciones si el framework no los trae, cookies `httpOnly` + `secure` + `sameSite`.
- **Secrets:** nunca en el código ni en el repo (ya cubierto en Entornos); mínimo privilegio en credenciales de DB y servicios.
- **Base de datos:** permisos mínimos por entorno; si es Supabase/Postgres con acceso desde cliente, **RLS obligatorio en todas las tablas**.
- **Rate limiting** en auth, formularios públicos y APIs expuestas. Mensajes de error genéricos en login (no revelar si el email existe).
- **Headers de seguridad:** CSP, `X-Frame-Options`/`frame-ancestors`, `X-Content-Type-Options`, HSTS. HTTPS en todos los entornos remotos.
- **Uploads** (si hay): validar tipo y tamaño en servidor, almacenar fuera del web root / en storage dedicado, nunca servir con el content-type que declaró el cliente.
- **Errores y logs:** los errores al usuario no exponen stack traces ni internals; los logs no guardan passwords, tokens ni datos sensibles.
- **Dependencias:** auditoría (`npm audit` o equivalente) al cerrar cada fase — sin vulnerabilidades críticas en Fase 6, sin críticas ni altas para producción en Fase 7.

### Verificación por fase
- **Fase 6 (cierre):** checklist baseline aplicado + `npm audit` sin críticas + AuthZ verificada en los flujos core.
- **Fase 7 (antes de producción):** revisión completa contra este documento + auditoría de dependencias limpia + verificación de headers, rate limiting y RLS en staging. Un pendiente crítico de seguridad = no hay deploy (Override Consciente requerido para saltarlo).

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
- Seguir el **Build Order** como secuencia de construcción — no improvisar el orden
- Leer `docs/design/` antes de implementar cualquier UI — es la fuente de verdad visual (handoff de Fase 5); construir sobre el prototipo, no reinventar
- **Código mínimo**: antes de escribir, recorrer la escalera (¿necesita existir? → ¿ya existe en el codebase? → ¿stdlib? → ¿feature nativa de la plataforma? → ¿dependencia ya instalada? → recién entonces, el mínimo código que funcione). Marcar simplificaciones deliberadas: `// deuda: <qué>. techo: <límite>. upgrade: <cuándo>`
- Seguir las convenciones de naming definidas arriba
- Escribir tests para funcionalidades críticas
- Documentar funciones complejas con JSDoc/docstrings
- Verificar variables de entorno antes de hacer commit
- Actualizar PROGRESS.md al cerrar un paso o sesión

### Nunca hacer:
- Hardcodear secrets, API keys o credenciales
- Hacer cambios en producción sin pasar por staging primero
- Conectarse a la DB de producción desde local o staging, ni usarla para pruebas
- Aplicar migraciones directamente en producción sin haberlas verificado en staging
- Usar keys live de servicios externos (pagos, email) fuera de production
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

### En progreso
- [ ] [Funcionalidad actual]

### Pendiente
- [ ] [Funcionalidad pendiente]

---

## Decisiones técnicas registradas

| Fecha | Decisión | Alternativas consideradas | Motivo |
|-------|----------|--------------------------|--------|
| [fecha] | [Qué se decidió] | [Otras opciones] | [Por qué] |

---

*Generado por el Product Development Framework v2.2 — Fase 4 · Planificación Técnica*