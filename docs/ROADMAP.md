# Roadmap

Hoja de ruta de CANDIDATON a partir de la auditoría del 8 de noviembre de 2026. El horizonte de producto es Argentina hacia las elecciones de 2027. Las fechas de cada fase se fijan cuando se autorice el trabajo, no en este documento.

Cada fase posterior a la 0 espera autorización. Ninguna fase autoriza, por sí sola, crear tablas, desplegar o publicar en GitHub.

## Fase 0. Auditoría y preparación

Estado: realizada en la tarea 001. La tarea 002 se encargó a continuación.

- Inventario del scaffold Next.js 16, React 19, TypeScript y Tailwind 4.
- Revisión de Supabase, Git y `.gitignore`, sin exponer credenciales.
- Comprobación de `npm run build`, `tsc --noEmit` y `npm run lint`.
- Redacción de `docs/ROADMAP.md`, `docs/IDEAS.md`, `docs/ARCHITECTURE.md` y `docs/DECISIONS.md`.

Resultado: el proyecto compila. La aplicación visible sigue siendo el scaffold. Supabase no está configurado.

## Fase 1. Modelo editorial y de dominio

Estado: aprobada con condiciones en la tarea 003. Las condiciones quedaron escritas en el modelo, la política y el flujo. No hay esquema ni cambios de interfaz.

Documentos vigentes:

- `docs/DOMAIN_MODEL.md`
- `docs/EDITORIAL_POLICY.md`
- `docs/VERIFICATION_WORKFLOW.md`

La fase cubre personas, elecciones, cargos, organizaciones, fuentes, enunciados, promesas, procedimientos judiciales y vínculos; las tres dimensiones de C-002; autenticidad de la fuente distinta de la veracidad del contenido; denuncia, investigación, imputación, condena y absolución; rectificación, derecho de respuesta y retirada; el visto jurídico por jurisdicción; y la trazabilidad de lo que encontró una IA, las fuentes que usó y quién autorizó cada decisión.

P-002, P-006, P-008 y P-012 a P-019 rigen con esas condiciones. La fase 3 puede apoyarse en este modelo cuando se autorice la primera migración.

## Fase 2. Fundaciones del repositorio

Estado: la plantilla de entorno quedó hecha en la tarea 003 (C-012). El resto espera encargo.

Hecho:

- `.gitignore` versiona `.env.example` y sigue ignorando los archivos con valores reales.
- `.env.example` trae nombres de variables y valores de ejemplo, sin credenciales.

Pendiente:

- Cáscara de la aplicación: nombre, metadata, idioma y retirada de los textos de Create Next App (P-004, P-009).
- Estructura de carpetas de la aplicación, todavía sin lógica de negocio innecesaria.
- Decisión explícita sobre el proyecto Supabase: región, claves y forma de acceso (P-001).

## Fase 3. Esquema inicial

El modelo de la fase 1 ya está aprobado con condiciones. Esta fase sigue esperando un encargo explícito y el cierre de P-001: proyecto, región y momento de la primera migración. Esta tarea no crea tablas.

- Primera migración: tablas, claves, relaciones y restricciones del modelo aprobado, incluidas autenticidad, postura procesal, visto jurídico, respuesta y modo de reutilización.
- Políticas de lectura del contenido publicado.
- Cliente de servidor mínimo para leer un registro de prueba controlado.
- Sin carga de casos reales. Publicarlos exigirá, además, el visto jurídico de cada jurisdicción.

## Fase 4. Lectura pública de Argentina

- Búsqueda de personas.
- Ficha con las etiquetas públicas separadas, la fuente visible y la polaridad sin tratarla como verdad.
- Comparación inicial entre dos fichas.
- Páginas que respetan Cache Components: shell estático y datos editoriales con vida de caché explícita.

## Fase 5. Flujo editorial

Implementa el circuito ya vigente en `docs/VERIFICATION_WORKFLOW.md`. P-006, P-015 y P-016 están aprobadas con condiciones. Falta el encargo de construirlas.

- Roles de propuesta, revisión, autorización y visto jurídico.
- Historial de cambios y de decisiones editoriales.
- Estados de verificación y autenticidad de la fuente visibles para quien lee.
- Rectificación, derecho de respuesta, retirada y resolución posterior.

## Fase 6. Idiomas y segundo paso internacional

- Interfaz y contenido desacoplados del texto fijo en español (P-003).
- Un segundo idioma de interfaz cuando el primero ya tenga fichas reales.
- El modelo de país permanece listo para otro mercado, sin abrirlo hasta que Argentina tenga un recorrido de lectura completo.

## Fase 7. Endurecimiento y salida

- Pruebas, integración continua y observabilidad (P-007).
- Decisión de alojamiento (P-005).
- Revisión de accesibilidad, rendimiento y neutralidad del lenguaje.
- Despliegue solo con una autorización distinta de este roadmap.

## Fuera de alcance hasta nuevo encargo

- Scraping o ingestión automática de medios, registros oficiales o redes.
- Puntuaciones únicas de “verdad” o de “confiabilidad” de una persona.
- Aplicaciones nativas.
- Cuentas públicas de la ciudadanía, comentarios o foros.
- Cambios de marca más allá de una cáscara neutra.
