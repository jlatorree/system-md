# Mantenimiento del hub (obligatorio)

> Esta es la **regla permanente** del proyecto. La instala el skill Many Brains en
> el handoff: en Claude Code es el `CLAUDE.md` del proyecto; en Cowork se pega en
> Settings del proyecto → Instructions. El onboarding (leer el proyecto, proponer
> estructura, sembrar) lo hace el skill; este archivo es solo lo que mantiene el
> sistema vivo después.

Este proyecto usa un `_hub.md` en la raíz como índice vivo de todos los
documentos. Es tu mapa: léelo al inicio de cada sesión para orientarte sobre qué
node es la fuente de verdad de cada tema, cuándo se actualizó y qué output
deriva de cuáles.

No crees carpetas vacías por adelantado: créalas solo cuando llegue el primer
archivo que va en ellas. Las decisiones de rumbo se registran en `_decisiones.md`
(archivo único en la raíz; créalo al registrar la primera).

El flujo del proyecto es generativo: las conversaciones cristalizan en **nodes**
temáticos (archivos `.md` planos en `_nodes/`, uno por tema, en kebab-case), y
esos nodes son las fuentes con las que generas **outputs** (presentaciones,
informes, one-pagers) que viven en `_outputs/`. Como `_nodes/` es PLANO (sin
carpetas por tema), la navegación NO la dan las carpetas: la dan el `_hub.md` y
la capa de `## Conexiones` (`[[...]]`) de cada node. Mantén el sistema vivo SIN
que el usuario te lo pida, aplicando estas cinco consignas:

1. **Una fuente de verdad por tema.** Cada tema es un solo node en `_nodes/`.
   No dupliques contenido entre nodes. Si necesitas una representación
   (presentación, resumen, informe), créala como output que deriva del node, no
   como copia.

2. **Versionado solo por cambio estructural.** Sube versión (v0.2 → v0.3) solo
   ante un cambio de fundamento (premisa, modelo, arquitectura, alcance). Cambios
   incrementales (agregar sección, refinar, reordenar) NO suben versión: solo
   actualizan la fecha de cabecera. En la duda, no bumpees.

3. **Hub como mapa.** `_hub.md` es el único lugar donde se ve qué nodes están
   vigentes, cuándo se actualizaron y qué output deriva de cuáles. Cuando crees,
   muevas, renombres o modifiques un node o un output, actualiza de inmediato la
   fila correspondiente en `_hub.md` (ruta, fecha, versión, estado) y la fecha de
   su cabecera.

4. **Los outputs citan sus nodes-fuente.** Todo output que generes (HTML, .docx,
   .pptx, resumen) debe llevar en cabecera o pie: "Basado en `node.md`
   (versión del YYYY-MM-DD)". Además, usa **citas por afirmación**: cuando una
   afirmación concreta de un node u output viene de un node específico (o de una
   referencia externa), cítala con footnote (`[^1]`). Al generar un output, lee
   primero su(s) node(s) como fuente — nunca inventes contenido que debería venir
   del node.

5. **Conexiones explícitas y recíprocas en wikilinks.** Cada node cierra con una
   sección `## Conexiones` que declara con enlaces `[[...]]` de qué depende, qué
   alimenta y con qué se relaciona, usando alias para legibilidad
   (`[[arquitectura-de-pagos|Arquitectura de pagos]]`). Mantén **backlinks
   recíprocos**: si A enlaza a B, B enlaza a A. Es tu mapa de navegación
   (reemplaza a las carpetas) y la base del lint: al abrir un archivo, lee sus
   Conexiones para saber qué otros nodes leer antes de responder o generar un
   output.

## Operaciones que debes ejecutar

- **Cristalizar.** Cuando una conversación produzca conocimiento que vale la
  pena retener (un hallazgo, una decisión, un análisis), PROPÓN proactivamente
  guardarlo — no esperes solo a que el usuario lo pida. La decisión final de
  guardar es suya. Si acepta, guárdalo como node temático en `_nodes/` (un
  archivo plano en kebab-case, p. ej. `arquitectura-de-pagos.md`), nunca dejes
  morir lo valioso en el chat. No guardes la conversación entera, solo lo que
  vale. Al crearlo, agrégalo al `_hub.md`, dale su sección `## Conexiones`
  (recíprocas) y pon citas por afirmación en sus afirmaciones sustantivas.

- **Registrar decisión.** Cuando se tome una decisión que cambia el rumbo del
  proyecto (un pivote, un cambio de premisa, descartar un enfoque), añade una
  entrada al INICIO (lo más reciente arriba) de `_decisiones.md` (archivo único
  en la raíz; créalo si no existe) con el formato `## [YYYY-MM-DD] Título` y un
  párrafo breve con el QUÉ y el PORQUÉ. Es append-only: no edites entradas
  pasadas. Registra solo decisiones de rumbo, no operaciones mecánicas (crear un
  output o actualizar una fecha NO van aquí). Si el archivo crece mucho, pártelo
  por año (`_decisiones-2026.md`).

- **Derivar (output).** Cuando el usuario pida un output a partir de nodes
  ("con X.md y Y.md genera una presentación"), lee primero esos nodes como
  fuente, genera el output en `_outputs/`, ponle la cita "Basado en…" más citas
  por afirmación (`[^1]`) en las afirmaciones que vengan de un node, y registra
  su fila en `_hub.md`.

- **Congelar (histórico).** Solo por orden explícita del usuario. Crea
  `_outputs/_historico/AAAA-MM-DD_nombre/` con el output congelado, una carpeta
  `nodos-fuente/` (copia inmutable de los nodes usados) y un `_meta.md` (qué,
  cuándo y por qué se congeló). El snapshot es autocontenido e inmutable; los
  nodes copiados nunca vuelven a `_nodes/`. Nunca se asigna automáticamente.

- **Design system.** Solo si el usuario lo pide y lo provee, guarda su `design.md`
  en `_design-system/`. El skill no lo crea ni lo clasifica por su cuenta.

- **Lint (cuando el usuario lo pida).** Haz un health-check del proyecto POR
  RAZONAMIENTO (no script; compatible con Cowork) y reporta: nodes sin sección
  `## Conexiones`; wikilinks `[[...]]` que apuntan a archivos que no existen;
  **backlinks no recíprocos** (A enlaza a B pero B no enlaza a A); afirmaciones
  sustantivas sin cita; outputs marcados `requiere refresh` desde hace tiempo;
  contradicciones entre nodes; conceptos mencionados varias veces que merecerían
  su propio node. Propón correcciones, no las apliques sin confirmar.

## Reglas operativas adicionales

- Al modificar un node, marca como `requiere refresh` en el hub todo output que
  dependa de él.
- No pre-crees carpetas vacías. Crea cada carpeta solo cuando llegue el primer
  archivo que va en ella.
- `_nodes/` es PLANO: nada de subcarpetas por tema. Un node = un archivo
  kebab-case, fuente de verdad de un tema.
- Las referencias externas (bibliografía, papers de terceros, PDFs externos,
  enlaces fuente, capturas) entran a `_nodes/` como nodes de referencia, marcados
  como material de terceros dentro del node. No hay carpeta de referencias.
- Carpetas con prefijo `_` del piso mínimo (no renombrar): `_context/`,
  `_nodes/`, `_outputs/` (con `_outputs/_historico/` dentro), `_design-system/`.
  Más los archivos de raíz `_hub.md` y `_decisiones.md`.
- Histórico solo por orden explícita del usuario; snapshots autocontenidos e
  inmutables. No es para borradores.
- Nunca borres archivos sin consentimiento explícito del usuario.
- Si detectas que el hub quedó desactualizado respecto al estado real de las
  carpetas, corrígelo y avisa al usuario qué reconciliaste.
