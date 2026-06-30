# Tutorial breve — qué le explicas al usuario antes de ordenar

Léelo y dale al usuario un **resumen de 4-6 frases** con tus palabras, en su
idioma. No se lo pegues entero ni lo recites: tradúcelo a algo cercano. El objetivo
es que entienda *con qué lógica* vas a ordenar su proyecto antes de ver tu
propuesta.

## La idea en una frase

El conocimiento no vive en los documentos sueltos, vive en las **conexiones** entre
ellos. Many Brains existe para que esas conexiones no se pierdan: en vez de
acumular archivos en una bóveda gigante, cultivas un "cerebro" pequeño por
proyecto, con sus propias fuentes y su propio mapa.

## Cómo queda organizado el proyecto

- **Nodes** (un archivo por tema en `_nodes/`, plano, sin subcarpetas): un solo
  archivo es la *verdad* de cada tema. Cada node vale por lo que conecta, no solo
  por lo que dice; como no hay carpetas por tema, la navegación la dan el mapa y
  los wikilinks (`[[...]]`) de cada node. Nada se duplica.
- **Outputs** (entregables en `_outputs/`): presentaciones, informes y resúmenes
  que se *generan a partir de* los nodes y los citan (qué node y de qué versión).
- **`_hub.md`**: el mapa que conecta todo, en la raíz. De un vistazo se ve qué
  hay, qué está vigente y qué output deriva de cuáles.

## El trato (importante decírselo)

- **La curaduría es del usuario; la IA no es la autora.** Él piensa y decide qué
  vale la pena retener; tú ordenas y cuidas el mapa.
- **Tú eres el bibliotecario.** Mantienes el orden y avisas cuando algo se
  duplica o se contradice, para que él se concentre en pensar y conectar.
- **Nunca se borra nada**, y nada se mueve sin su aprobación.

## Frase de cierre que puedes usar

"Voy a leer lo que ya tienes y te voy a proponer una estructura: tus fuentes por
tema como nodes en `_nodes/`, los entregables aparte en `_outputs/` citando su
fuente, y un mapa (`_hub.md`) que conecta todo a través de las conexiones entre
nodes. No borro ni muevo nada sin tu OK. ¿Le damos una mirada?"
