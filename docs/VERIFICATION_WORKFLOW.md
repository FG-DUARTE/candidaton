# Flujo de verificación y trazabilidad

Flujo de verificación y trazabilidad de CANDIDATON. La tarea 003, del 8 de noviembre de 2026, lo aprobó con condiciones, junto con el [modelo de dominio](./DOMAIN_MODEL.md) y la [política editorial](./EDITORIAL_POLICY.md). Los papeles de abajo quedan aceptados como política. Instalar la autenticación pertenece a una fase posterior.

## Papeles

| Papel | Qué hace | Qué no hace |
| --- | --- | --- |
| Agente de investigación | Busca, propone texto y lista fuentes dentro de una corrida | No verifica, no autoriza, no publica |
| Redactor | Arma y edita el borrador. Puede ser quien parte de un hallazgo del agente | No autoriza su propia publicación mientras exista otro editor disponible |
| Revisor | Contrasta fuentes, tipo, verificación, polaridad, fechas y enlaces | No publica |
| Editor responsable | Autoriza una versión concreta o la retira, y deja motivo | No delega ese acto en el agente |
| Revisión jurídica | Da el visto de una jurisdicción sobre una versión de un caso real | No sustituye al editor responsable ni verifica en su lugar |

En un equipo mínimo, la misma persona puede redactar y autorizar. El acto de autorización se registra igual, con su nombre. El agente nunca ocupa el papel de editor responsable. Esa excepción quedó aceptada con P-006 y P-015. El visto jurídico lo firma una persona identificada, interna o externa. Puede coincidir con el editor solo si el registro lo dice y la jurisdicción no exige otra cosa.

La lectura pública no exige cuenta. Quien no edita no recorre este flujo. El proveedor técnico de las cuentas editoriales sigue abierto, junto con P-001.

## Dos estados que avanzan por separado

### Revisión editorial

Describe el lugar de la pieza en el trabajo humano.

| Estado | Sentido |
| --- | --- |
| `draft` | Borrador interno, humano o nacido de un hallazgo |
| `in_review` | Un revisor la está contrastando |
| `changes_requested` | Vuelve al redactor con una nota |
| `authorized` | Un editor responsable autorizó esa versión. Todavía puede no estar visible |
| `published` | Visible en la lectura pública |
| `withdrawn` | Dejó de estar visible. La versión y el historial se conservan |

### Verificación

La asigna una persona. Describe el respaldo de las fuentes, no el paso administrativo.

| Estado | Sentido |
| --- | --- |
| `unverified` | Nadie completó el contraste. No se publica |
| `attribution_checked` | Consta quién dijo o denunció eso, y dónde |
| `corroborated` | El contenido fáctico, o el texto de la resolución, concuerda con las fuentes exigidas |
| `disputed` | Hay piezas o fuentes incompatibles, enlazadas |
| `rectified` | Una versión o una pieza posterior corrige esta |
| `not_ascertainable` | Se buscó y no hay base para sostenerla. No se publica como hecho |

La polaridad positiva, neutral o negativa se edita en otro campo y puede cambiar sin cambiar la verificación.

## Recorrido de un enunciado

1. **Abrir contexto.** La pieza nace de una corrida de investigación o de un alta humana. El origen queda grabado.
2. **Redactar.** El redactor fija sujetos, tipo, texto, idioma, fecha del acontecimiento y precisión. La verificación inicial es `unverified`. La polaridad inicial es `neutral` hasta que alguien la cambie a propósito.
3. **Citar.** Cada fuente entra con rol, localizador y momento de consulta. Las fuentes que el agente solo mencionó y el redactor descarta quedan en la corrida, no como sostén del enunciado.
4. **Enlazar.** El revisor busca contradicciones, rectificaciones y resoluciones posteriores. Si encuentra alguna, crea la relación. Si no encuentra, la autorización lo dice de forma explícita.
5. **Revisar.** El revisor completa la lista de abajo y propone el estado de verificación. Puede devolver la pieza con `changes_requested`.
6. **Autorizar.** El editor responsable acepta una versión inmutable. Ese acto crea `PublicationAuthorization`.
7. **Publicar.** La versión autorizada pasa a `published` y recibe la fecha de publicación de la plataforma. La etiqueta pública se calcula con la tabla de puertas.
8. **Corregir después.** Cualquier cambio de texto, tipo, verificación, polaridad, fuentes o relaciones crea otra versión. Si la pieza ya era pública, esa versión nueva espera otra autorización. La anterior sigue en el historial.

Un borrador puede permanecer en `unverified` todo el tiempo que haga falta. No tiene fecha de publicación.

## Puertas de publicación

La autorización solo puede caer sobre una versión que cumpla una fila.

| Destino público | Tipo | Verificación mínima | Otras condiciones |
| --- | --- | --- | --- |
| Hecho acreditado | `factual` | `corroborated` | Al menos una fuente `supports` u `official_text` con autenticidad `authentic` |
| Denuncia | `allegation` y postura `complaint` | `attribution_checked` | Fuente auténtica. Se identifica quién denuncia. El fondo no se redacta como hecho acreditado |
| Investigación o imputación | `factual` sobre el acto, o `allegation` si solo consta la acusación | `corroborated` para el acto oficial; `attribution_checked` si todavía es una acusación | La postura es `investigation` o `charge`. La conducta de fondo no hereda la corroboración del acto |
| Opinión atribuida | `attributed_opinion` | `attribution_checked` | Autor identificable y fuente `attributes_quote` auténtica |
| Condena o absolución | `judicial_resolution` | `corroborated` | Postura `conviction` o `acquittal`, término oficial, fuente auténtica `official_text` o la mejor primaria disponible |
| En disputa | El tipo que corresponda | `disputed` | La relación `contradicts` existe. No usa la etiqueta de hecho acreditado |
| No se publica | Cualquiera | `unverified` o `not_ascertainable` | Permanece en borrador o retirada |

Si la pieza trata un caso real, la fila correspondiente no basta: hace falta un `LegalClearance` de esa jurisdicción sobre esa versión, con resultado `cleared` o `cleared_with_limits`. El resultado `blocked` deja la pieza fuera de la lectura pública.

`authorized` sin el paso a `published` permite una espera breve, por ejemplo para publicar varias piezas juntas. Las dos fechas quedan registradas si no coinciden.

## Lista del revisor

Antes de pedir autorización, el revisor deja constancia de cada punto:

- El tipo y la postura procesal describen la pieza. Una denuncia no se sube a hecho, una imputación no se llama condena y un archivo no se llama absolución.
- La autenticidad de cada fuente de apoyo está en `authentic`. La verificación del contenido se fijó aparte, por una persona.
- La polaridad está elegida a propósito y no se dedujo del tipo, de la autenticidad ni de la verificación.
- La fecha del acontecimiento tiene precisión, aunque la precisión sea `unknown`.
- Las fechas de la fuente y de la consulta están guardadas.
- El modo de reutilización permite la cita que se va a mostrar.
- Los sujetos son las personas u organizaciones correctas, homónimos incluidos.
- Hay al menos una fuente con rol y localizador, según la puerta buscada.
- Se buscaron contradicciones, rectificaciones, respuestas pendientes y resoluciones posteriores.
- Si la pieza es un caso real, el visto jurídico de su jurisdicción cubre esta versión.
- Si intervino un agente, la corrida, los hallazgos y las fuentes usadas están enlazados.
- El texto sigue la política de verbos: atribuir la denuncia, nombrar el acto de investigación o imputación, y atribuir al órgano la condena, la absolución o el archivo.

## Qué encontró la IA, qué fuentes usó y quién publicó

### Corrida (`ResearchRun`)

Se abre cada vez que un agente trabaja sobre un ámbito: una persona, una elección, un proceso o una pregunta acotada.

- Identidad del agente, modelo y versión del modelo.
- Inicio y fin.
- Encargo en lenguaje claro: qué debía buscar.
- Ámbito: jurisdicción y sujetos.
- Estado de la corrida.

El prompt completo no se archiva. Puede contener datos de más. Guardar el encargo, el modelo, los hallazgos y las fuentes cubre la pregunta de qué se le pidió.

### Hallazgo (`Finding`)

- Corrida a la que pertenece.
- Texto que produjo el agente, inmutable.
- Enunciado borrador que se creó a partir de él, si el redactor lo tomó.
- Confianza informada por el agente, si vino en la respuesta. Queda al lado del hallazgo y fuera de `verification_status`.

### Uso de fuente (`FindingSource`)

- Fuente ya registrada, o cita en bruto si todavía no lo está: título y URL.
- Uso: `consulted`, `relied_upon` o `discarded`.
- Localizador.
- Momento de la consulta.

`relied_upon` no convierte esa fuente en sostén del enunciado. Eso ocurre cuando el redactor crea un `StatementSource`. La diferencia importa: una cosa es lo que el agente miró y otra lo que la versión autorizada cita.

### Autorización (`PublicationAuthorization`)

Una por versión publicada o republicada.

- Versión exacta.
- Editor responsable.
- Instante.
- Lista de corridas y hallazgos tenidos en cuenta. Vacía si el origen es solo humano.
- Resultado de la búsqueda de contradicciones: enlaces creados, o constancia de que no aparecieron.
- Nota breve del editor.
- Identificador del visto jurídico, si la versión trata un caso real.

Con esas piezas se puede reconstruir qué propuso el agente, qué fuentes pasaron por la corrida, qué autenticidad se les reconoció, qué texto quedó en la versión, qué visto jurídico lo permitió y qué persona autorizó esa versión.

## Después de publicar

### Cambio de la plataforma

Una fe de erratas interna es una versión nueva: evento en el historial, revisión desde `in_review` y autorización nueva. La ficha muestra la versión vigente y permite ver que hubo una anterior.

### Rectificación externa

Se crea otro enunciado con su fuente y se enlaza con `rectifies`. El original puede pasar a verificación `rectified` sin desaparecer.

### Contradicción nueva

Se publica o se actualiza el otro enunciado y se crea `contradicts`. Los dos pueden permanecer visibles. La verificación de cada uno pasa a `disputed` cuando el revisor así lo decide. El flujo no elige un ganador automático.

### Derecho de respuesta

El pedido entra como `ReplyRequest`, unido a la versión publicada. Mientras la decisión sea `pending`, la ficha interna lo muestra al editor. Publicar la respuesta crea un enunciado, la relación `replies_to` y una autorización propia. Rechazarla guarda actor, instante y motivo. Las dos decisiones son eventos. El enunciado original no se reescribe.

### Resolución posterior

Se registra la resolución si todavía no existe, con su enunciado de tipo judicial. La pieza anterior gana un enlace `followed_by_resolution`. El texto viejo no se sustituye por el fallo. La ficha actual muestra el enlace junto a la pieza.

### Retiro

`withdrawn` saca la pieza de la lectura pública cuando no debía publicarse, cuando un visto jurídico lo exige o cuando dejarla visible causa un daño que la corrección no resuelve. La autorización de retiro guarda actor, instante y motivo: error, exigencia jurídica, pedido de derechos, duplicado, pieza superada u otro. Hallazgos, versiones y fuentes permanecen en el registro interno. Si el retiro nace de un visto, el evento enlaza ese visto.

### Promesas

El alta de la promesa recorre este mismo flujo: lo que se publica es que alguien formuló ese compromiso. Cada grado de cumplimiento es otro paso completo, con fuentes y autorización propias. El grado anterior permanece en el historial del compromiso.

### Fichas estructuradas

Candidatura, período, vínculo, elección y procedimiento se hacen visibles junto con el enunciado que los sostiene, no antes. Si ese enunciado se retira, la ficha estructurada deja de mostrarse hasta que otra versión autorizada la respalde.

## Registro que no se borra

El historial de eventos es append-only. Una corrección añade un evento. No se reescribe el evento anterior para dejarlo «limpio».

Cada evento guarda actor, clase de actor, instante, versión afectada y motivo. Los eventos mínimos son: creación, edición, cambio de tipo, de verificación, de polaridad o de postura procesal, alta o baja de fuente, resultado de autenticidad, modo de reutilización, alta de relación, paso de revisión, autorización, visto jurídico, respuesta recibida, respuesta publicada, respuesta rechazada, publicación y retiro.

Ese registro responde, para cada decisión editorial:

- Qué información encontró el agente: el texto del hallazgo.
- Qué fuentes utilizó y si se reconocieron como auténticas.
- Quién fijó el tipo, la postura, la verificación y la polaridad.
- Quién dio el visto jurídico, en qué jurisdicción y con qué resultado.
- Quién autorizó la publicación de esa versión.
- Quién publicó o rechazó una respuesta, y quién retiró la pieza, con el motivo.

## Condiciones ya incorporadas

P-006, P-012, P-015 y P-016 quedaron aprobadas con condiciones en la tarea 003. Este flujo incorpora los papeles, las puertas que separan autenticidad y veracidad, el visto jurídico previo a un caso real, el derecho de respuesta, la retirada con motivo y el historial que no se reescribe. El prompt completo sigue fuera del archivo. El proveedor de autenticación de los editores queda para la fase que implemente las cuentas.
