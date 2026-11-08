# Ideas

Banco de ideas de CANDIDATON. Todo lo que sigue es propuesta. No son decisiones; las decisiones están en [DECISIONS.md](./DECISIONS.md). Ninguna idea de esta lista autoriza esquema, dependencias nuevas ni despliegue.

## Lectura e investigación

- Ficha de persona con línea de cargos, candidaturas y enunciados, cada bloque con su tipo y su fuente.
- Búsqueda por nombre, con desambiguación cuando haya homónimos, usando años, distrito y organización.
- Comparación lado a lado de dos o más personas, alineada por elección o por tema, manteniendo el tipo de cada enunciado.
- Línea de tiempo por persona y por elección, útil para el ciclo argentino hacia 2027.
- Ficha de elección: qué se elige, en qué jurisdicción y qué candidaturas están registradas.
- Enlaces estables y citables a una ficha o a un enunciado concreto, para que un tercero pueda referenciar la plataforma.

## Fuentes y neutralidad

- Cada enunciado muestra el tipo antes que el texto: hecho acreditado, denuncia, opinión o resolución judicial.
- Una denuncia enlaza la causa o la cobertura que la reporta, y se mantiene distinta de una sentencia o de un archivo.
- Una opinión queda atribuida a quien la emite y no se presenta como hallazgo de la plataforma.
- Una resolución judicial guarda tribunal, fecha, identificador público y enlace a la fuente oficial cuando exista.
- Vista de “fuentes en desacuerdo”: dos registros del mismo episodio, cada uno con su origen, sin fusionarlos en un párrafo único.
- Historial público del enunciado: cuándo se publicó, cuándo se corrigió y qué fuente motivó el cambio.
- Glosario visible de los cuatro tipos, escrito en lenguaje llano, presente en la ficha y no solo en la documentación interna.

## Escala internacional

- País y jurisdicción como datos de primera clase, con Argentina como primer catálogo.
- Contenido traducible sin duplicar la identidad de la persona: un mismo registro, varios textos.
- Interfaz en español de Argentina primero; estructura lista para otro idioma cuando haya fichas reales.
- Calendario electoral por país, empezando por las fechas argentinas que se puedan citar con fuente oficial.

## Confianza del visitante

- Página de método: qué publica CANDIDATON, qué no infiere y cómo se corrige un error.
- Indicador de cobertura de una ficha (pocas fuentes, varias fuentes, fuente oficial presente), separado de cualquier juicio sobre la persona.
- Canal de corrección para señalar una fuente omitida o un enunciado mal clasificado.
- Exportación sobria de una ficha, con las citas incluidas, para investigación y prensa.

## Ingeniería, cuando toque

- Lecturas públicas cacheadas con invalidación al publicar un cambio editorial.
- Semillas de desarrollo con datos ficticios claramente marcados, nunca mezclados con fichas reales.
- Pruebas del clasificador de enunciados: un hecho no puede guardarse ni renderizarse como opinión.
- Bitácora de migraciones pequeña y revisable, una preocupación de dominio por migración.

## Ideas que conviene no hacer pronto

- Un número único que resuma a una persona.
- Ingesta automática de redes sociales o de portales de noticias.
- Cuentas, comentarios o rankings de la audiencia.
- Ampliar a un segundo país antes de cerrar el recorrido de lectura de Argentina.
