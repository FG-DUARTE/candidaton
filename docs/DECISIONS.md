# Decisiones

Registro de arquitectura de CANDIDATON. Una decisión confirmada ya rige. Una decisión aprobada con condiciones rige dentro de esas condiciones. Una propuesta pendiente espera autorización y no autoriza implementación.

Fecha de este registro: 8 de noviembre de 2026. La tarea 003 aprobó con condiciones P-002, P-006, P-008 y P-012 a P-019, e incorporó esas condiciones a la documentación. Cerró además la plantilla de entorno (C-012).

## Confirmadas

### C-001. Producto y primer mercado

CANDIDATON es una plataforma internacional para buscar, investigar y comparar candidatos políticos y otras figuras públicas. El primer mercado es Argentina, con vistas a las elecciones de 2027. El producto debe ser escalable, multilingüe y neutral.

Origen: encargo de producto de la tarea 001. Todavía no está reflejado en la interfaz.

### C-002. Separación editorial en tres dimensiones

Cada enunciado mantiene separadas tres dimensiones:

1. Tipo de información.
2. Estado de verificación.
3. Valoración editorial positiva, neutral o negativa.

La plataforma tiene que poder expresar hecho acreditado, denuncia o acusación, opinión atribuida, resolución judicial e información no verificada. La información no verificada no se publica como hecho. Una valoración positiva o negativa no equivale a verdadero o falso, ni al revés. La verificación de fuentes es un requisito de producto.

Cómo se guardan esas etiquetas y cómo se publica cada pieza quedó aprobado con condiciones en P-002, P-008 y P-012 a P-019. Las condiciones —autenticidad distinta de veracidad, posturas procesales separadas, rectificación, respuesta, retirada, trazabilidad, visto jurídico por jurisdicción y límites de licencia y datos— están escritas en `docs/DOMAIN_MODEL.md`, `docs/EDITORIAL_POLICY.md` y `docs/VERIFICATION_WORKFLOW.md`.

Origen: encargos de las tareas 001, 002 y 003.

### C-003. Aplicación web con Next.js y React

La aplicación es Next.js 16.4.5 con App Router en `src/app`, React 19.3.0 y React DOM 19.3.0. El paquete npm es privado y se llama `candidaton`, versión 0.1.0.

Origen: scaffold instalado y lockfile.

### C-004. TypeScript estricto

TypeScript 5.9.3 con `strict`, `noEmit` y resolución `bundler`. El alias `@/*` apunta a `./src/*`. Next.js typecheck forma parte de `next build`.

Origen: `tsconfig.json` y comprobación de compilación.

### C-005. Tailwind CSS 4

Los estilos usan Tailwind CSS 4.3.5 mediante `@import "tailwindcss"` y `@tailwindcss/turbopack` como loader en la configuración de Turbopack. No hay fichero `tailwind.config` ni `postcss.config`.

Origen: scaffold. `npm run build` confirma que esta combinación compila.

### C-006. ESLint en configuración plana

La calidad estática usa ESLint 9 con `eslint-config-next` 16.4.5 (`core-web-vitals` y TypeScript) y los ignores de `.next`, `out`, `build` y `next-env.d.ts`.

Origen: `eslint.config.mjs`. `npm run lint` pasa. La metadata del lockfile marca ESLint 9.39.5 como versión fuera de soporte; actualizarlo es una propuesta distinta y no está autorizado ahora.

### C-007. Cache Components y Partial Prefetching activos

`next.config.ts` activa `cacheComponents` y `partialPrefetching`. Next.js 16.4.5 acepta ambas opciones y el build las anuncia al arrancar. Partial Prefetching depende de Cache Components.

Origen: scaffold, conservado porque el build de producción ya depende de él. Revisar su uso cuando existan datos dinámicos, sin desactivarlo en esta fase.

### C-008. Repositorio en `main`

El código vive en la rama `main`, que sigue a `origin/main` en `https://github.com/FG-DUARTE/candidaton.git`. Esta fase no crea ramas, commits ni cambios remotos por su cuenta.

Origen: estado de Git en la tarea 001.

### C-009. Secretos fuera del repositorio

`.gitignore` excluye `.env*` y vuelve a incluir solo `.env.example`. También excluye `*.pem` y `.vercel`. `.env.example` tiene nombres de variables y valores de ejemplo, sin credenciales. El repositorio no contiene cliente de Supabase, URLs reales de proyecto ni claves.

Origen: `.gitignore`, `.env.example` y la tarea 003. La plantilla versionable es C-012.

### C-010. Límites de la fase de preparación

En esta fase no se borran archivos existentes, no se crean ni modifican tablas de Supabase, no se publica ni despliega, no se instalan dependencias de más, no se modifican credenciales ni archivos de entorno, y no se hacen cambios automáticos en GitHub.

Origen: restricciones de la tarea 001.

### C-011. Límites de la tarea 002

El modelo editorial y de dominio se diseña en documentos. Esta tarea no crea ni modifica tablas de Supabase, no cambia la interfaz, no instala paquetes, no publica, no despliega y no hace commits. Implementar el modelo espera una autorización distinta.

Origen: restricciones de la tarea 002.

### C-012. Plantilla de entorno versionable

`.gitignore` ignora `.env*` y exceptúa `.env.example`. La plantilla declara `NEXT_PUBLIC_SITE_URL`, `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` y `SUPABASE_SERVICE_ROLE_KEY`, con valores de ejemplo. La clave de servicio no lleva prefijo público. Los archivos con valores reales siguen fuera de Git.

Origen: tarea 003, que ejecuta la antigua propuesta P-010. No elige proyecto, región ni claves de Supabase: eso sigue en P-001.

### C-013. Límites de la tarea 003

Esta tarea consolida documentación y la plantilla de entorno. No crea ni modifica tablas, no cambia la interfaz, no instala dependencias, no publica en Vercel, no modifica credenciales y no hace commits ni push.

Origen: restricciones de la tarea 003.

## Aprobadas con condiciones

La tarea 003 aceptó estas propuestas. La aceptación obliga a cumplir las condiciones de abajo. No autoriza, por sí sola, crear tablas ni publicar casos reales.

Condiciones comunes, ya escritas en el modelo, la política y el flujo:

1. La autenticidad de la fuente y la veracidad del contenido se registran por separado.
2. Denuncia, investigación, imputación, condena y absolución son posturas distintas. El término oficial de la jurisdicción se conserva.
3. Hay cauce de rectificación, derecho de respuesta y retirada. Cada decisión guarda actor, instante y motivo.
4. El historial de decisiones editoriales es append-only e incluye visto jurídico, autenticidad, respuesta y retiro.
5. Un caso real no se publica sin revisión jurídica específica de esa jurisdicción sobre esa versión.
6. La reutilización respeta licencia, derechos de autor y protección de datos. El modo inicial es citar y enlazar.

### P-002. Modelo conceptual

Aprobado con las condiciones comunes. Rige `docs/DOMAIN_MODEL.md`: personas, jurisdicciones, organizaciones, cargos y períodos, elecciones y candidaturas, fuentes, enunciados, promesas y grados de cumplimiento, procedimientos y resoluciones, vínculos, respuesta, visto jurídico y trazabilidad.

Efecto: el modelo puede guiar un esquema futuro. Esta aprobación no abre la migración.

### P-006. Lectura pública y papeles editoriales

Aprobado con las condiciones comunes. La lectura pública es anónima. Los papeles son redactor, revisor y editor responsable. El agente de investigación no autoriza. En un equipo mínimo, la misma persona puede redactar y autorizar, y ese acto queda a su nombre. El visto jurídico de un caso real lo firma una persona identificada, interna o externa.

El proveedor técnico de las cuentas editoriales no queda elegido. Implementar la autenticación pertenece a una fase posterior.

### P-008. Política editorial y de fuentes

Aprobada con las condiciones comunes. Rige `docs/EDITORIAL_POLICY.md`, con el circuito de `docs/VERIFICATION_WORKFLOW.md`. El modo inicial de una fuente es citar y enlazar. La cita breve, el texto oficial y la reproducción con licencia son modos registrados. El cuerpo de una obra en modo `forbidden` no se almacena.

### P-012. Etiquetas públicas derivadas

Aprobado con las condiciones comunes. Se guardan cuatro tipos (`factual`, `allegation`, `attributed_opinion`, `judicial_resolution`). «Hecho acreditado» exige tipo fáctico, verificación corroborada y fuente auténtica. «Información no verificada» es el estado `unverified` y no se publica.

### P-013. Polaridad editorial

Aprobado con las condiciones comunes. La valoración positiva, neutral o negativa es la polaridad de la pieza respecto del sujeto. El valor inicial es neutral. No se calcula desde la autenticidad ni desde la verificación, no se agrega por persona y no ordena un ranking.

### P-014. Escala de cumplimiento de promesas

Aprobado con las condiciones comunes. Siete grados ordinales, sin porcentaje: horizonte abierto, evidencia insuficiente, parcial, cumplida, incumplida, retirada o reemplazada, y no evaluable. Cada grado es un juicio con fuentes, verificación y autorización propias.

### P-015. La IA propone y una persona publica

Aprobado con las condiciones comunes. Una corrida guarda agente, modelo, encargo, hallazgos y fuentes consultadas, usadas o descartadas. La autorización nombra a la persona y la versión. El agente no escribe el estado de verificación ni autoriza la publicación. El prompt completo no se archiva.

### P-016. Historial que no reescribe

Aprobado con las condiciones comunes. Las versiones publicadas son inmutables. El historial de eventos es append-only. Contradicciones, rectificaciones externas, respuestas y resoluciones posteriores son relaciones. La pieza anterior permanece identificable. La retirada deja de mostrarla y conserva el registro interno.

### P-017. Vocabulario territorial abierto

Aprobado con las condiciones comunes. Jurisdicción, identificadores externos opcionales y vocabularios abiertos para partidos, rondas electorales, tribunales y términos procesales. El nombre oficial del país se conserva junto a la postura procesal. Ningún documento nacional es la clave de la persona.

### P-018. La ficha estructurada espera al enunciado

Aprobado con las condiciones comunes. Una candidatura, un período de cargo, un vínculo, una promesa o una resolución solo se muestran en público si los sostiene un enunciado que pasó el flujo, incluido el visto jurídico cuando se trata de un caso real.

### P-019. Alcance de una resolución judicial

Aprobado con las condiciones comunes. Corroborar una resolución acredita que esa decisión existe y que el resumen concuerda con la fuente auténtica. Los hechos de fondo que el órgano declaró siguen atribuidos a esa declaración. Pasarlos a hecho acreditado de la plataforma exige otro enunciado fáctico. Condena y absolución no reescriben la denuncia, la investigación ni la imputación anteriores.

## Pendientes

Estas propuestas no están aceptadas. Desarrollarlas exige un encargo explícito.

### P-001. Supabase como sistema de datos

Usar Supabase Postgres para los datos estructurados, con lectura pública de lo publicado y escritura reservada al flujo editorial. Existe la carpeta local vacía `supabase/migrations/`. La plantilla de entorno ya reserva los nombres de variables, con valores de ejemplo. No hay SDK, CLI, `config.toml` ni claves reales.

Hace falta confirmar el proyecto, la región, el modelo de claves y el momento en que se escribe la primera migración. El modelo conceptual ya puede guiar ese esquema. Esta propuesta sigue siendo la puerta de la fase 3.

### P-003. Internacionalización

Elegir el mecanismo de idiomas de la interfaz y del contenido. El HTML actual declara `lang="en"` porque es el scaffold. El primer mercado sugiere contenido y UI en español de Argentina, con margen para más idiomas. La biblioteca, la ruta de locale y el idioma por defecto siguen abiertos. Ver también P-009.

### P-004. Sustituir el scaffold visible

Reemplazar la página, la metadata, el README y los enlaces de despliegue de Create Next App por una cáscara neutra de CANDIDATON. La identidad visual, la tipografía definitiva y el tono de la interfaz están sin definir. Geist y la paleta del scaffold son herencia técnica, no una decisión de marca.

### P-005. Alojamiento

Elegir dónde se ejecuta la aplicación. El README y los SVG públicos mencionan Vercel porque vienen de la plantilla. No hay proyecto de Vercel ni `output` de despliegue configurado.

### P-007. Pruebas y integración continua

Elegir el corredor de pruebas y el pipeline. `tests/` está vacío y no hay script `test` ni configuración de CI. El único control automático vigente es TypeScript dentro del build y ESLint.

### P-009. Idioma por defecto de la interfaz

Confirmar el idioma inicial de la UI. Propuesta de trabajo, todavía no aceptada: español (`es-AR`) como idioma por defecto del primer mercado, con inglés preparado en la estructura y sin traducir toda la interfaz en la primera entrega.

### P-011. Actualización de ESLint

Valorar el aviso de deprecación de ESLint 9.39.5 en el lockfile y subir de línea mayor solo con una comprobación de `eslint-config-next`. El lint actual pasa; no es un bloqueo.
