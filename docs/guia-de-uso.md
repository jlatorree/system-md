# Guía de uso — Sistema de organización de proyectos

Sistema estándar para organizar el contenido que generas en proyectos de Claude Cowork y Claude Code. Resuelve el problema de "voy generando documentos y es difícil mapear la información".

> **Nota:** esta guía y el `README.md` son documentación del *skill* para entender el método; no se copian a tus proyectos. Dentro de un proyecto, el sistema funciona con tres cosas: el `_hub.md`, la regla de mantenimiento (en el `CLAUDE.md` del proyecto si usas Code, o en las instrucciones del proyecto si usas Cowork) y el `_decisiones.md` en la raíz.

## Las piezas

El sistema son **tres elementos que trabajan juntos**:

1. **`_hub.md`** — el mapa (el *presente*). Índice vivo de qué node es la fuente de verdad de cada tema, qué output deriva de cuáles, cuándo se actualizó cada cosa y en qué estado está todo. Lo lees tú para orientarte; lo lee el agente para no duplicar ni perderse. Vive en la raíz, con prefijo `_`.
2. **La regla de mantenimiento** — el motor. Un bloque de instrucciones en el `CLAUDE.md` (Code) o en las instrucciones del proyecto (Cowork) que ordena al agente mantener todo vivo en cada sesión, sin que se lo pidas. Vive FUERA del árbol del proyecto.
3. **`_decisiones.md`** — la bitácora (el *cómo llegamos aquí*). Registro append-only de las decisiones que cambiaron el rumbo, fechado y con lo más reciente arriba, con su QUÉ y su PORQUÉ. Es un archivo único en la raíz (con prefijo `_`). El hub dice qué hay ahora; la bitácora cuenta la secuencia que llevó hasta ahí.

Sin la pieza 2, el sistema se desactualiza apenas dejas de hacerlo a mano. Con ella, el mantenimiento es automático.

> **Buena práctica de longitud.** El `CLAUDE.md` rinde mejor por debajo de ~200 líneas (es contexto que el agente carga cada sesión); mantén ahí solo la regla de mantenimiento. El `_hub.md` el agente lo lee bajo demanda, así que puede ser más largo — pero si pasa de ~150 líneas, suele ser señal de congelar outputs viejos en `_outputs/_historico/` o dividir el proyecto.

## La idea central: el flujo de conocimiento

El sistema tiene una sola dirección de flujo:

**conversación → node (`_nodes/`) → output (`_outputs/`)**

1. Conversas con el agente y algo cristaliza (un segmento, una propuesta de valor, un hallazgo).
2. Eso se guarda como **node** en `_nodes/`, en **kebab-case** (`propuesta-de-valor.md`). Tus nodes *son* tus fuentes de conocimiento, y nacen de las conversaciones. `_nodes/` es **plano**: un node = un archivo, sin subcarpetas por tema.
3. Cuando pides un **output** (entregable), combinas nodes: *"con `segmentos.md` y `propuesta-de-valor.md` genera una presentación para stakeholders"*. Esa operación se llama **derivar**; el resultado es un *output*. Se guarda en **`_outputs/`** y cita sus nodes-fuente.

Las carpetas (todas con prefijo `_`, nacen cuando llega su primer archivo; nada se pre-crea vacío):

- **`_context/`** — inputs y brief del proyecto (visión, propósito, conceptos clave, antecedentes). El skill lo pide al iniciar.
- **`_nodes/`** — TODO el conocimiento, **plano**, un `.md` por node en kebab-case. Aquí viven tus **fuentes**. Las referencias externas (papers, PDFs de terceros, enlaces) entran aquí como nodes, marcados como material de terceros (ya no hay carpeta de referencias aparte).
- **`_outputs/`** — los **entregables** generados desde nodes (la última versión viva). Su histórico vive dentro, en `_outputs/_historico/`, como snapshots congelados y autocontenidos.
- **`_design-system/`** — solo si el usuario lo provee/pide: guarda el `design.md` que él aporta.

Además, en la raíz: `_hub.md` (el mapa) y `_decisiones.md` (la bitácora).

Cada node cierra con una sección `## Conexiones` en wikilinks (`[[...]]`, con alias para legibilidad: `[[arquitectura-de-pagos|Arquitectura de pagos]]`) que declara de qué depende, qué alimenta y con qué se relaciona. No es para un grafo bonito: como `_nodes/` es plano, **las carpetas ya no dan la navegación — la dan el `_hub.md` y las conexiones**. Al abrir un archivo, el agente ve qué más leer, y esa capa es la base del *lint*. Los backlinks son **recíprocos**: si A enlaza a B, B enlaza a A. Como ya usas Obsidian, el grafo aparece gratis; pero los `[[...]]` son texto plano, así que el sistema no queda atado a ningún plugin.

## Aplicarlo en un proyecto

Ya no traes una carpeta: **invocas el skill**. Una vez instalado (ver `README.md`), *Many Brains* detecta en qué estado está tu proyecto y actúa en consecuencia, sin pre-crear carpetas (cada una nace cuando llega su primer archivo):

- **Proyecto vacío → Sembrar.** Crea el `_hub.md` y te pregunta qué cargar como contexto.
- **Proyecto con contenido, sin Many Brains → Adoptar.** Lee todo lo que existe, te explica el método, propone una estructura en árbol y reordena **solo con tu aprobación, sin borrar nada**. Adoptar reubica, no modifica contenido: añadir Conexiones y citas a archivos existentes es un paso aparte, propuesto y opcional.
- **Proyecto que ya usa Many Brains → Reconciliar.** Ajusta los desfases del `_hub.md` y, si lo pides, corre el *lint*. Es idempotente: si te corren de nuevo, detecta el `_hub.md` y reconcilia; no re-siembra ni duplica.

Al cerrar, el skill instala la **regla de mantenimiento** a nivel de proyecto para que el `_hub.md` se mantenga vivo solo en cada sesión futura:

- **En Claude Code:** crea o actualiza el `CLAUDE.md` del proyecto (en Code el archivo es el mecanismo permanente, se queda).
- **En Claude Cowork:** te entrega el texto para pegarlo en las instrucciones del proyecto (panel → Instructions), porque la app no lo escribe por ti.

> **Diferencia clave:** en Code la regla vive en el archivo `CLAUDE.md`; en Cowork vive en el panel de la app. En ambos casos el skill **nunca borra nada sin tu consentimiento**.

## El flujo diario

1. **Empiezas una sesión** → el agente lee el `_hub.md` y se orienta. (La primera vez en un proyecto, te pregunta qué cargar como contexto.)
2. **Conversas y algo cristaliza** → el agente te *propone* guardarlo como node en `_nodes/` (operación *cristalizar*), en kebab-case, con su sección `## Conexiones` recíprocas y sus citas por afirmación. Tú decides; no se queda en el chat.
3. **Tomas una decisión de rumbo** → el agente la registra al inicio de `_decisiones.md` (lo más reciente arriba), con fecha, QUÉ y PORQUÉ. Append-only: no se editan entradas pasadas.
4. **El agente actualiza el hub** → fecha, versión, estado de outputs. Sin que lo pidas. Si modificas un node, marca `requiere refresh` en el hub a todo output que dependa de él.
5. **Pides un output** → "usa `node.md` como fuente". El agente lee primero el node (y sus Conexiones), no inventa lo que debe venir del node, y lo guarda en `_outputs/` con la cita "Basado en…" y citas por afirmación.
6. **De vez en cuando pides un *lint*** → el agente revisa la salud del proyecto por razonamiento: nodes sin Conexiones, wikilinks rotos, backlinks no recíprocos, afirmaciones sin cita, outputs marcados `requiere refresh` hace tiempo, contradicciones entre nodes. Propone correcciones; no las aplica sin confirmar.

## Las cinco consignas (lo que nunca cambia)

1. **Una fuente de verdad por tema.** Cada tema = un solo node en `_nodes/`; no se duplica contenido entre nodes.
2. **Versionado solo por cambio estructural** (premisa, modelo, arquitectura, alcance); lo incremental solo actualiza la fecha. En la duda, no bumpear.
3. **Hub como mapa** — único lugar donde se ve qué nodes están vigentes, cuándo se actualizaron y qué output deriva de cuáles.
4. **Los outputs citan sus nodes-fuente** ("Basado en `node.md`, versión del YYYY-MM-DD") y usan **citas por afirmación** con footnotes (`[^1]`) cuando una afirmación viene de un node específico.
5. **Conexiones explícitas y recíprocas en wikilinks** — navegación del sistema (reemplaza a las carpetas) y base del lint.

## Relación con `CLAUDE.md` / `AGENTS.md`

No confundas dos capas:

- **`CLAUDE.md`** = contexto e instrucciones para el *agente* (cómo comportarse, qué reglas seguir). Aquí vive la regla de mantenimiento.
- **`_hub.md`** = mapa del *contenido* para humanos y agente (qué node es qué, qué output deriva de cuáles).

Son complementarios. Si en algún proyecto usas también `AGENTS.md` (estándar multi-herramienta), la regla de mantenimiento puede ir ahí en lugar de `CLAUDE.md` — el agente la lee igual.

---

*Inspirado en el MANIFEST.md de David Paluy y en el patrón LLM Wiki de Andrej Karpathy, adaptados a un flujo generativo. De Paluy: la idea de un archivo-mapa. De Karpathy: las tres capas (fuentes / contenido que el agente mantiene / schema en CLAUDE.md), la operación de archivar buenos hallazgos (aquí, "cristalizar"), el lint periódico, y los wikilinks como navegación. De kfchou/wiki-skills se adoptan dos convenciones: las **citas por afirmación** (footnotes que atan cada afirmación sustantiva a su node o referencia) y la **reciprocidad de backlinks** (las conexiones `[[...]]` son bidireccionales). Lo que NO se tomó: el grafo de Karpathy es convergente (muchas fuentes externas → síntesis) y a gran escala (cientos de páginas, motor de búsqueda, log cronológico); este sistema es generativo (pocos nodes propios → muchos outputs) y a escala humana, donde el hub y la memoria del proyecto bastan sin log aparte.*
