# Clasificación — cómo decidir qué es cada archivo (modo Adoptar)

Esta es tu guía para proponer un destino por archivo. Son **señales, no reglas
rígidas**: usa criterio y, en la duda, propón tu mejor hipótesis y márcala "(confianza baja)" en el plan (el usuario
corrige el plan antes de que se ejecute). El principio rector: **un archivo es
*node* si es una fuente de verdad sobre un tema; es *output* si se generó a
partir de uno o más nodes para presentarlos, entregarlos o resumirlos.**

## La pregunta clave: ¿fuente o representación?

Antes de mirar la extensión, pregúntate: *¿este archivo es donde vive el
conocimiento original, o es una versión hecha para mostrar/entregar algo que ya
existe en otro lado?*

- Donde vive el conocimiento → **node** (un archivo `.md` en `_nodes/`).
- Una versión para mostrar/entregar → **output** (en `_outputs/`).

La extensión ayuda pero no manda: un `.html` suele ser output, pero un `.md`
largo de notas crudas es node aunque esté desordenado.

## Tabla de señales

| Lo que ves en el archivo | Rol | Destino propuesto |
| --- | --- | --- |
| Visión, propósito, conceptos clave, brief, antecedentes, research previo transversal | Contexto | `_context/` |
| `.md` con sustancia sobre **un tema** (investigación, segmentos, propuesta, notas de trabajo, análisis) | Node | `_nodes/` (un node kebab-case por tema) |
| Bibliografía, papers de terceros, PDFs externos, enlaces fuente, capturas de referencia | Node de referencia externa | `_nodes/` (márcalo como material de terceros dentro del node; ya NO hay `_referencias/`) |
| `.pptx` / `.html` / `.docx` / PDF generado / resumen / one-pager / pitch | Output | `_outputs/` |
| Tokens, paleta, tipografía, guías o componentes visuales **aportados por el usuario** | Design system | `_design-system/` (solo si el usuario lo provee/pide) |
| Bitácora/log de decisiones de rumbo | Decisiones | `_decisiones.md` (archivo único en la raíz) |
| Archivo de sistema o config (`.DS_Store`, `.gitignore`, `.obsidian/`, `node_modules/`) | Ruido | **no se toca, se ignora** |
| Genuinamente sin encaje tras agotar lo anterior | — | `_por-clasificar/` (último recurso) |

`_outputs/_historico/` no aparece en esta tabla a propósito: **nunca se asigna
automáticamente**, solo por orden explícita del usuario (ver reglas duras).

## Cómo nombrar nodes

`_nodes/` es **plano**: nada de subcarpetas por tema. **Un node = un archivo
`.md` por tema**, con nombre en **kebab-case** descriptivo
(`investigacion-usuarios.md`, `segmentos.md`, `modelo-negocio.md`,
`arquitectura-de-pagos.md`). Reglas prácticas:

- Si hay varios `.md` sobre el mismo tema, propón **fusionarlos en un solo node**
  (una fuente de verdad por tema); no dejes el mismo contenido repartido.
- Si un tema tiene un único archivo, ya es su node: nómbralo en kebab-case y
  ubícalo en `_nodes/`.
- Si un `.md` mezcla dos temas, **no lo partas tú**: proponlo como un node del
  tema dominante y anota que quizá convenga separarlo en dos nodes más adelante
  (eso es decisión del usuario).

Como `_nodes/` es plano, la navegación no la dan las carpetas: la dan el
`_hub.md` y la capa `## Conexiones` (`[[...]]`, con backlinks recíprocos) de cada
node. Eso se añade en un paso aparte (ver "Adoptar reubica, no modifica").

## Distinciones que suelen confundirse

- **Contexto vs. node temático.** `_context/` es para lo *transversal* a todo
  el proyecto (visión, propósito, conceptos, brief, antecedentes). Un tema
  específico (un segmento, un hallazgo) es un node en `_nodes/`, no contexto.
- **Referencia vs. node propio.** Ambos viven en `_nodes/`: la diferencia es de
  *naturaleza*, no de carpeta. Una referencia es material *de terceros* que
  consultas (un informe de mercado ajeno, un paper) y entra como node marcado
  como material externo. Un node propio es conocimiento *del proyecto*, aunque
  cite fuentes externas. Cuando una afirmación de un node propio se apoya en una
  referencia, se cita con footnote (`[^1]`).
- **Output vs. node.** Si el archivo dice "basado en…", o claramente resume/
  presenta algo, es output. Si dudas, mira si su contenido existe ya en otro
  archivo más completo: si sí, este es el output y aquel es el node-fuente.

## Reglas duras (no las rompas)

- **`_outputs/_historico/` nunca se asigna automáticamente.** Solo se congela ahí
  un snapshot cuando el usuario lo ordena explícitamente, porque depende de un
  evento externo (se presentó a un comité, a dirección) que solo él conoce.
- **`_por-clasificar/` es el último recurso (la ambigüedad de categoría NO cuenta: para eso, ubícalo en tu mejor hipótesis y márcalo "confianza baja").** Agota todas las opciones antes de
  mandar algo ahí. Cada archivo que caiga ahí lleva una nota de por qué y **se le
  reporta al usuario**. La meta es que la carpeta quede vacía.
- **Ruido se ignora, no se borra.** No elimines `.DS_Store` ni nada: el sistema
  nunca borra.
- **Nada se mueve sin OK.** Todo esto es una *propuesta* hasta que el usuario
  aprueba el plan. Y recuerda: adoptar **reubica, no modifica** — añadir
  `## Conexiones`, backlinks o citas a los archivos es un paso aparte, propuesto y
  opcional.
