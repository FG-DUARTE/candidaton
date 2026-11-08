# Política editorial

Política editorial de CANDIDATON. La tarea 003, del 8 de noviembre de 2026, la aprobó con condiciones, junto con el [modelo de dominio](./DOMAIN_MODEL.md) y el [flujo de verificación](./VERIFICATION_WORKFLOW.md). La aprobación obliga a cumplir las reglas de este documento. No crea tablas ni cambia la interfaz.

## Para qué existe

CANDIDATON informa sobre personas públicas y candidatos. El primer catálogo previsto es Argentina y el modelo vale para otros países. La plataforma muestra piezas con fuente, tipo y estado. No emite un veredicto global sobre una persona.

La neutralidad, en esta política, es separar cuatro cosas: lo que la fuente es, lo que la fuente dice, lo que un humano pudo contrastar de ese dicho y la polaridad con la que la pieza afecta al sujeto.

## Tres dimensiones

Cada enunciado lleva, a la vez:

1. **Tipo de información.** La clase de la pieza: enunciado fáctico, denuncia o acusación, opinión atribuida o resolución judicial.
2. **Estado de verificación.** El resultado de la revisión humana de las fuentes.
3. **Valoración editorial.** Polaridad respecto del sujeto: positiva, neutral o negativa.

Las tres se eligen por separado. La valoración describe si la pieza, redactada como va a publicarse, resulta favorable, desfavorable o ninguna de las dos para el sujeto principal. Ejemplos de lectura, todavía hipotéticos:

- Una condena corroborada en fuente oficial puede tener polaridad negativa y ser un resumen de resolución, no una opinión de la plataforma.
- Un premio o una ley sancionada a iniciativa de la persona puede tener polaridad positiva y ser un hecho corroborado.
- La fecha de una elección puede ser un hecho corroborado de polaridad neutral.
- Una columna elogiosa puede tener polaridad positiva, tipo opinión y verificación limitada a la atribución.

Una polaridad positiva no afirma que el contenido sea verdadero. Una polaridad negativa no afirma que sea falso. La verdad o el respaldo documental viven solo en el estado de verificación y en las fuentes.

La polaridad por defecto es neutral cuando la dirección no está clara. No se promedia por persona, no ordena un ranking y no sustituye al tipo ni a la verificación.

## Etiquetas que puede ver el público

| Etiqueta | Qué significa para quien lee |
| --- | --- |
| Hecho acreditado | La plataforma contrasta un enunciado fáctico con las fuentes exigidas y una persona autorizó esa versión |
| Denuncia o acusación | Alguien formuló una imputación. La plataforma muestra quién la formula y dónde consta. La conducta imputada no queda publicada como hecho acreditado |
| Opinión atribuida | Alguien valoró o interpretó un asunto. La plataforma identifica a quien habla. No adopta la opinión |
| Resolución judicial | Un órgano resolvió algo. La plataforma resume la decisión y conserva el término oficial |
| Información no verificada | La pieza está en preparación o no tiene respaldo revisado. No se publica y no se rotula como hecho |

«Hecho acreditado» e «información no verificada» salen de cruzar el tipo con la verificación. Se guardan así desde la aprobación condicionada de P-012. Una denuncia no cambia de tipo para convertirse en hecho.

## Autenticidad de la fuente y veracidad del contenido

La autenticidad responde si el documento citado es ese documento y si el pasaje coincide con el localizador. La veracidad responde qué puede afirmarse del contenido una vez contrastadas las fuentes auténticas. Son decisiones editoriales distintas y las dos quedan en el historial.

| Situación | Autenticidad | Veracidad del contenido |
| --- | --- | --- |
| El boletín oficial contiene la fecha de la elección y el pasaje coincide | `authentic` | El enunciado fáctico puede corroborarse |
| El diario es genuino y atribuye una frase a una persona | `authentic` | Puede comprobarse la atribución. La opinión sigue siendo opinión |
| El diario es genuino y escribe que alguien cometió un delito | `authentic` | La existencia de la nota puede constar. El delito no queda acreditado por esa nota |
| El fallo es el documento del tribunal y el resumen lo sigue | `authentic` | Queda acreditado que el órgano resolvió eso. El fondo alegado por las partes exige otro enunciado |
| La cita no aparece en la página indicada | `does_not_match` | No hay puerta de publicación sobre esa cita |

Una fuente auténtica no vuelve verdadero su contenido. Una verificación `corroborated` no se concede si la fuente de apoyo sigue en `unchecked` o en `does_not_match`.

## Reglas por tipo

### Enunciado fáctico

Se publica como hecho acreditado solo con verificación `corroborated`. El texto dice lo que las fuentes permiten sostener, con fecha del acontecimiento o con la precisión marcada como desconocida.

Si las fuentes discrepan, el estado es `disputed` y las piezas contradictorias permanecen enlazadas. La plataforma no elige una de oficio.

Si no hubo forma de constatarlo (`not_ascertainable`) o nadie completó la revisión (`unverified`), no hay ficha pública de ese enunciado.

### Denuncia, investigación, imputación, condena y absolución

Estas cinco situaciones no se redactan como si fueran la misma. El término oficial de la jurisdicción se muestra junto a la postura del modelo.

| Postura | Cómo se publica |
| --- | --- |
| Denuncia | Alguien formuló una acusación. El texto nombra a quien denuncia, a quién alcanza y el cauce. La verificación mínima es `attribution_checked` sobre una fuente auténtica. La conducta denunciada no se publica como hecho acreditado |
| Investigación | Una autoridad tiene el caso abierto. Puede acreditarse la apertura si el acto oficial es auténtico. La conducta investigada permanece en otro enunciado |
| Imputación | Una autoridad formuló un cargo formal. No se llama denuncia ni condena. Puede acreditarse la existencia del cargo. El hecho imputado no hereda esa corroboración |
| Condena | Resolución de fondo que declara responsabilidad, con el término oficial. Acredita la condena. No reescribe sola la denuncia o la imputación anteriores |
| Absolución | Resolución de fondo que descarta esa responsabilidad, con el término oficial. No se presenta como si la denuncia no hubiera existido: se enlaza |

Sobreseimiento, archivo, prescripción y figuras locales equivalentes usan la postura `other` y el nombre del país. No se traducen a absolución por semejanza.

Cada cambio de postura es un enunciado o una resolución nueva, enlazada con la anterior. El momento previo sigue siendo identificable.

### Opinión atribuida

Hace falta una persona o una organización identificable y una fuente de la formulación: cita, transcripción o pieza firmada. Una opinión sin autor identificable no se publica bajo esta etiqueta.

Se comprueba que esa persona dijo eso. No se comprueba si la opinión «tiene razón». La polaridad puede ser positiva o negativa según el contenido hacia el sujeto, y esa polaridad no es un acuerdo de CANDIDATON.

### Resolución judicial

El resumen dice lo que el órgano resolvió, en el sentido de «el tribunal dispuso…» o «el tribunal dio por probado…», y cita la resolución. El nombre oficial de la decisión viaja junto a cualquier clase internacional gruesa.

La verificación `corroborated` de este tipo significa que la resolución existe y que el resumen concuerda con la fuente auténtica. P-019, aprobada con condiciones, mantiene aparte los hechos de fondo: una condena permite acreditar la condena; los hechos que el órgano declaró quedan atribuidos a esa declaración salvo que un enunciado fáctico propio los contraste.

### Información no verificada

Puede vivir en un hallazgo de investigación o en un borrador. No tiene fecha de publicación. No aparece en búsqueda ni en comparación. No se exporta como hecho. Si más adelante se contrasta, cambia la verificación y recorre el flujo; la etiqueta pública sale de ese estado nuevo.

## Fuentes

Una pieza pública tiene al menos una fuente con rol y un localizador: página, párrafo, minuto, artículo o identificador de archivo.

- La fuente primaria se prefiere cuando el país la ofrece: boletín, resolución, padrón, versión taquigráfica, comunicado oficial.
- La fuente secundaria se admite para denuncias publicadas en prensa, opiniones y contexto. Se muestra como secundaria.
- Varias fuentes pueden sostener la misma pieza. También pueden contradecirla o rectificarla, con el rol correspondiente.
- Consultar una fuente no alcanza: el enlace guarda el momento de la consulta y el resultado de autenticidad, porque las páginas cambian.
- Una fuente no recibe un puntaje numérico de confiabilidad en esta política.

## Licencias, derechos de autor y datos personales

La ficha cita y enlaza. El modo de reutilización de cada fuente queda registrado.

- `cite_and_link` es el modo inicial.
- Una cita breve usa `short_quotation` y se limita al pasaje necesario para sostener el enunciado.
- El texto oficial que la jurisdicción publica como documento público usa `official_text`.
- Una reproducción más amplia usa `licensed_reproduction` y guarda la licencia que la permite.
- `forbidden` impide almacenar el cuerpo de la obra. La referencia bibliográfica puede quedar.

No se copia el artículo, el libro ni la resolución íntegros por el hecho de haberlos consultado. No hay ingesta automática de medios.

Los nombres públicos, los identificadores, las causas y los hallazgos de una investigación asistida son datos personales. El registro interno puede guardarlos para trazabilidad. La ficha pública muestra solo lo que la versión autorizada incluye y lo que el visto jurídico de esa jurisdicción permite. El prompt completo del agente no se archiva.

## Contradicción, rectificación, respuesta y retirada

Estas situaciones se muestran o se registran. No se aplastan en un párrafo único.

- **Contradicción.** Dos enunciados publicados pueden decir cosas incompatibles. Cada uno conserva sus fuentes y su verificación. La relación `contradicts` los une. El estado `disputed` avisa de esa tensión.
- **Rectificación de la plataforma.** Si CANDIDATON corrige su propio texto, la versión anterior queda en el historial y la nueva versión necesita otra autorización. El evento guarda quién corrigió, cuándo y por qué.
- **Rectificación externa.** Si un medio, un organismo o el propio sujeto corrige lo ocurrido, esa corrección es un enunciado nuevo enlazado con `rectifies`. El relato anterior sigue identificable.
- **Derecho de respuesta.** La persona u organización afectada, o quien actúe en su nombre, puede pedir que se publique su versión. El pedido guarda el texto ofrecido y la versión sobre la que versa. Publicarlo crea un enunciado enlazado con `replies_to` y exige autorización humana. Rechazarlo exige actor, instante y motivo. En los dos casos el enunciado original permanece.
- **Resolución posterior.** Una denuncia, una investigación o una imputación pueden apuntar a un archivo, una absolución, una condena o un recurso mediante `followed_by_resolution`. El enlace es parte de la lectura actual y no borra la pieza previa.
- **Retirada.** El estado `withdrawn` saca la pieza de la lectura pública. El motivo es uno de estos: error, exigencia jurídica, pedido de derechos, duplicado, pieza superada u otro. El evento de retiro guarda actor, instante y motivo. Versiones, fuentes y hallazgos siguen en el registro interno.

Quien lee tiene que poder distinguir la fecha del acontecimiento, la fecha de la fuente y la fecha en que CANDIDATON publicó.

## Promesas y cumplimiento

Una promesa publicada identifica quién la formuló, con qué palabras, ante qué fuente y con qué horizonte. Publicarla significa que la atribución está comprobada.

El grado de cumplimiento es un juicio aparte, con sus fuentes. Usa la escala ordinal del modelo de dominio: horizonte abierto, evidencia insuficiente, parcial, cumplida, incumplida, retirada o reemplazada, no evaluable. No hay porcentaje ni semáforo de la persona.

Un grado «incumplida» con polaridad negativa sigue siendo un juicio documental sobre ese compromiso. No convierte el resto de la ficha en una valoración global.

## Personas, cargos y vínculos

Candidaturas, períodos de cargo y vínculos con organizaciones se publican como datos estructurados solo si un enunciado ya pasó la misma política. Un resultado electoral es el dato de la autoridad competente, con su fuente. No se traduce a polaridad por el hecho de haber ganado o perdido: esa polaridad, si se asigna, es un campo aparte y puede quedar neutral.

Los homónimos se separan con la nota de desambiguación y con los identificadores externos que existan. La ausencia de un documento nacional no impide crear la ficha.

## Procedimientos de cualquier país

El procedimiento guarda el tribunal, el identificador local y el papel de cada parte con los nombres de esa jurisdicción. La clase gruesa internacional sirve para filtrar y comparar. La ficha muestra primero el término oficial.

Una investigación abierta se presenta con la postura `investigation`, no como hecho acreditado de la conducta investigada. La imputación, la condena y la absolución usan sus posturas y sus términos oficiales.

## Revisión jurídica antes de un caso real

Publicar un caso real en una jurisdicción exige un visto jurídico de esa jurisdicción sobre la versión que va a verse. El caso real incluye una denuncia, una investigación, una imputación, una condena, una absolución u otro procedimiento sobre personas identificables.

El visto nombra a quien revisa, la jurisdicción, el momento y el resultado: autorizado, autorizado con límites o bloqueado. Un visto de otra jurisdicción no cubre esta. Un visto de una versión anterior no cubre la versión nueva. Si el resultado trae límites, el texto público se queda dentro de ellos. Si el resultado es bloqueado, la pieza no se publica.

La revisión cubre, para ese país, la licitud de publicar, la protección de datos y los límites de la cita. Este documento no sustituye ese dictamen.

## Investigación asistida por IA

Un agente puede localizar fuentes, proponer textos y señalar contradicciones posibles. El rastro debe decir qué se le pidió, qué modelo intervino, qué propuso y qué fuentes consultó, usó o descartó.

El agente no publica, no autoriza y no deja fijado el estado de verificación. La confianza que el propio modelo declare se archiva con el hallazgo y no entra en la etiqueta pública.

Si una persona redacta sin agente, el origen queda como humano y la autorización sigue siendo humana.

## Lenguaje de la ficha

- El tipo y el estado de verificación se leen antes del relato, o en un lugar de igual jerarquía.
- Los verbos de una denuncia son de atribución: «denunció», con quien denuncia.
- Los verbos de una investigación o de una imputación nombran el acto oficial: «se abrió una investigación», «la autoridad imputó». No dicen que la conducta haya quedado probada.
- Los verbos de una resolución son del órgano: «condenó», «absolvió», «archivó», «sobreseyó», con el término oficial.
- Las opiniones y las respuestas llevan el autor en la misma frase.
- La polaridad, si se muestra, se nombra como polaridad de la pieza. Se mantiene aparte de la veracidad y de la autenticidad de la fuente.
- No se usan adjetivos de carácter que las fuentes no sostengan.

## Qué queda fuera de la publicación

- Enunciados sin revisión humana autorizada.
- Información no verificada presentada como hecho, como denuncia comprobada o como opinión atribuida.
- Un caso real sin visto jurídico de su jurisdicción.
- Una cita cuya autenticidad no fue contrastada, usada como sostén de una pieza pública.
- Copia de una obra por encima del modo de reutilización registrado.
- Un número único que resuma a la persona.
- La polaridad usada como orden de «mejores» y «peores».
- Copiar el fondo de una acusación o de una sentencia al tipo fáctico sin un enunciado propio.
- Llamar condena a una imputación, o absolución a un archivo, cuando el término oficial dice otra cosa.
- Inferir delitos, filiación partidaria o ciudadanías que las fuentes no traen.
- Tratar la legislación, los partidos o el calendario de un solo país como valores fijos del sistema.

## Condiciones ya incorporadas

P-008 y las reglas conexas P-012 a P-019 quedaron aprobadas con condiciones en la tarea 003. Este documento incorpora la separación entre autenticidad y veracidad, las cinco posturas procesales, la rectificación, el derecho de respuesta, la retirada, la trazabilidad de cada decisión, el visto jurídico por jurisdicción y el respeto a licencias, derechos de autor y datos personales.
