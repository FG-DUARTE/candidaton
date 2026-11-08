# Arquitectura

Estado al 8 de noviembre de 2026, consolidado en la tarea 003. Este documento describe el sistema que existe hoy y la arquitectura que la implementación futura debe seguir. Las decisiones confirmadas, las aprobadas con condiciones y las propuestas abiertas están en [DECISIONS.md](./DECISIONS.md).

## Producto

CANDIDATON es una plataforma internacional para buscar, investigar y comparar candidatos políticos y otras figuras públicas. El primer mercado es Argentina, con vistas a las elecciones de 2027.

La arquitectura tiene que poder crecer a otros países y a otros idiomas sin rehacer el modelo de datos ni mezclar el tipo de una pieza con su verificación, con la autenticidad de la fuente o con su valoración. Ese modelo quedó aprobado con condiciones en la tarea 003. Está en `docs/DOMAIN_MODEL.md`, `docs/EDITORIAL_POLICY.md` y `docs/VERIFICATION_WORKFLOW.md`.

## Estado actual

El repositorio es el scaffold de `create-next-app`, más la documentación de producto. No hay cliente de datos ni rutas propias. La interfaz sigue siendo la plantilla.

```
candidaton/
├── src/app/                 App Router
│   ├── layout.tsx           raíz, metadata y fuentes Geist
│   ├── page.tsx             página de inicio del scaffold
│   ├── globals.css          Tailwind CSS 4
│   └── favicon.ico
├── public/                  SVG del scaffold
├── docs/                    roadmap, modelo aprobado con condiciones, política y flujo
├── supabase/migrations/     carpeta local vacía; Git no la versiona
├── scripts/                 carpeta local vacía
├── tests/                   carpeta local vacía
├── next.config.ts
├── tsconfig.json
├── eslint.config.mjs
├── package.json
├── .gitignore               ignora .env* y versiona .env.example
└── .env.example             nombres de variables y valores de ejemplo
```

La interfaz sigue siendo la plantilla en inglés (`lang="en"`, título "Create Next App"). El README describe `app/page.tsx`; el código vive en `src/app/page.tsx`.

## Stack vigente

| Pieza | Versión instalada | Declaración | Papel |
| --- | --- | --- | --- |
| Next.js | 16.4.5 | exacta | App Router, Turbopack en build y desarrollo |
| React / React DOM | 19.3.0 | exacta | UI |
| TypeScript | 5.9.3 | `^5` | `strict: true`, `noEmit: true` |
| Tailwind CSS | 4.3.5 | `^4` | `@import "tailwindcss"` en `globals.css` |
| `@tailwindcss/turbopack` | 4.3.5 | `^4` | loader CSS en `next.config.ts` |
| ESLint | 9.39.5 | `^9` | flat config |
| `eslint-config-next` | 16.4.5 | exacta | core-web-vitals y TypeScript |
| `@types/node` | 20.19.43 | `^20` | tipos de Node |
| `@types/react` y `@types/react-dom` | 19.3.0 | `^19` | tipos de React |
| Node local | 24.18.0 | Next exige `>=20.9.0` | entorno de desarrollo |
| npm local | 11.16.0 | — | gestor de paquetes |

No hay `tailwind.config`, `postcss.config` ni router `pages/`. Tailwind 4 se activa con el import de CSS y el loader de Turbopack. El build de producción usa Turbopack y completa con esa configuración.

`next.config.ts` activa dos opciones del scaffold, documentadas en Next.js 16:

- `cacheComponents: true`. Las rutas combinan un shell prerenderizado con contenido dinámico. El contenido cacheable se marca con `use cache`.
- `partialPrefetching: true`. Requiere Cache Components. El prefetch de `<Link>` toma las partes estáticas de la ruta y deja fuera los datos dinámicos.

TypeScript usa el alias `@/*` hacia `./src/*`. El layout tipa sus props con `LayoutProps` de la ruta raíz, un helper generado por Next.js 16.

El lockfile marca ESLint 9.39.5 como versión fuera de soporte. `npm run lint` termina sin errores. No se actualiza en esta fase.

El entorno local de npm avisa de una clave `devdir` no reconocida. Esa clave no está en el repositorio.

## Supabase

No hay configuración operativa de Supabase.

- El repositorio no depende de `@supabase/supabase-js` ni de `@supabase/ssr`.
- No existe `supabase/config.toml`.
- `supabase/migrations/` está vacía y solo existe en el disco local.
- `.env.example` trae nombres de variables y valores de ejemplo. La regla `.env*` ignora el resto, y `!.env.example` versiona solo la plantilla.
- No hay `.env` ni `.env.local` en la raíz.
- El árbol de Git no contiene credenciales ni claves reales.
- No hay tablas, políticas ni clientes que revisar.

Supabase sigue pendiente como sistema de datos (P-001). Esta fase no crea tablas. Los nombres de variables ya están reservados en la plantilla.

## Git

- Rama `main`, alineada con `origin/main`.
- Remoto `https://github.com/FG-DUARTE/candidaton.git`.
- Historial: scaffold de Create Next App y un segundo commit que añadió los cuatro documentos vacíos.
- `.gitignore` ignora `.env*` y vuelve a incluir `.env.example`. También ignora `node_modules`, `.next`, `out`, cobertura, `*.pem`, logs, `.vercel`, `*.tsbuildinfo` y `next-env.d.ts`.
- Los valores reales de entorno siguen fuera del repositorio.
- Git no versiona directorios vacíos, así que `scripts/`, `tests/` y `supabase/migrations/` no forman parte del histórico.

## Comprobaciones del 8 de noviembre de 2026

Repetidas en la tarea 003, después de la consolidación documental. El código de la aplicación no cambió.

| Comando | Resultado |
| --- | --- |
| `npm run build` | Compila con Next.js 16.4.5 y Turbopack. Cache Components y Partial Prefetching activos. `/` y `/_not-found` quedan estáticas. |
| `npx tsc --noEmit` | Sin errores. |
| `npm run lint` | Sin errores. |

## Arquitectura objetivo

El modelo conceptual está aprobado con condiciones. Construir el esquema y la aplicación espera un encargo distinto. P-001, el proyecto Supabase, sigue abierto.

```
Lectura pública (Next.js, App Router)
        │
        ▼
Casos de uso de solo lectura
        │
        ▼
Supabase Postgres  ←  flujo editorial, visto jurídico y trazabilidad
        │
        ▼
Fuentes citadas, con autenticidad y modo de reutilización
```

Principios vigentes para la implementación futura:

1. La lectura pública y la escritura editorial son superficies distintas. El visitante consulta registros publicados. Quien carga o revisa datos usa otro flujo.
2. La unidad mínima publicable es un enunciado, unido a una o más fuentes auténticas. La ficha de una persona se compone de esos enunciados y de datos biográficos con la misma disciplina de cita.
3. El tipo de información, el estado de verificación, la autenticidad de la fuente y la valoración editorial permanecen separados. Las etiquetas públicas salen de esa combinación.
4. Denuncia, investigación, imputación, condena y absolución no se colapsan. Un caso real espera el visto jurídico de su jurisdicción.
5. El idioma es un atributo del contenido y de la interfaz. El primer contenido es el de Argentina; el esquema reserva país e idioma desde el principio.
6. Las páginas públicas pueden usar el shell de Cache Components. Los datos que cambian con la revisión editorial se tratan como contenido dinámico o con una vida de caché explícita.
7. Las claves de servicio, si llegan a hacer falta, viven solo en el servidor. El cliente público usa la clave anónima y permisos de lectura sobre lo ya publicado.

Límites actuales: no hay esquema, no hay políticas de fila, no hay autenticación instalada y no hay despliegue.

## Qué queda fuera del código a propósito

- Tablas y migraciones de Supabase.
- Variables de entorno y credenciales.
- Sustitución de la página de inicio.
- Publicación o despliegue.
- Cambios en GitHub.
