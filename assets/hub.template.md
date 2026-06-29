# 00 — Hub del proyecto [NOMBRE]

*Mapa maestro de los documentos del proyecto. Última actualización: YYYY-MM-DD.*

Este archivo es el **índice vivo** del proyecto: la vista **global** de qué está vigente y qué deriva de qué. Como `_nodes/` es plano (sin carpetas por tema), la navegación no la dan las carpetas: la dan este `_hub.md` y la vista **local** de cada node, que vive dentro del propio archivo en su sección `## Conexiones` (de qué depende, qué alimenta, con qué se relaciona).

> Al clonar este template, reemplaza `[NOMBRE]` y empieza a llenar las tablas. Las carpetas se crean solas a medida que generas contenido; ninguna se pre-crea vacía (ver el schema en `CLAUDE.md`).

---

## Reglas de gestión (las cinco consignas)

**1. Una fuente de verdad por tema.** Cada tema es un solo node en `_nodes/`. No se duplica contenido entre nodes.

**2. Versionado solo por cambio estructural.** La versión sube solo ante un cambio de fundamento (premisa, modelo, arquitectura, alcance). Lo incremental solo actualiza la fecha. En la duda, no bumpear.

**3. Hub como mapa.** Este archivo es el único lugar donde se ve qué nodes están vigentes, cuándo se actualizaron y qué output deriva de cuáles. Se actualiza al crear, mover, renombrar o modificar.

**4. Los outputs citan sus nodes-fuente.** Cada output lleva *"Basado en `node.md` (versión del YYYY-MM-DD)"*. Además, **citas por afirmación**: cuando una afirmación concreta viene de un node específico, se cita con footnote (`[^1]`). Al generar un output, primero se leen sus nodes; nunca se inventa lo que debe venir del node.

**5. Conexiones explícitas y recíprocas en wikilinks.** Cada node cierra con una sección `## Conexiones` (`[[...]]`, con alias para legibilidad: `[[arquitectura-de-pagos|Arquitectura de pagos]]`) que declara de qué depende, qué alimenta y con qué se relaciona. **Backlinks recíprocos**: si A enlaza a B, B enlaza a A. Es la navegación del sistema (reemplaza a las carpetas) y la base del lint.

---

## Estructura de carpetas

Todo lo del proyecto vive bajo carpetas con prefijo `_`. En la raíz, además, dos archivos sueltos: este `_hub.md` y `_decisiones.md`.

| Ruta              | Contenido                                                                                  |
| ----------------- | ------------------------------------------------------------------------------------------ |
| `_hub.md`         | Este índice vivo / mapa del proyecto (raíz)                                                 |
| `_decisiones.md`  | Bitácora append-only de decisiones de rumbo, fechada, lo más reciente arriba (raíz)         |
| `_context/`       | Inputs/brief del proyecto: visión, propósito, conceptos clave, antecedentes, research transversal |
| `_nodes/`         | TODO el conocimiento, plano, un `.md` por node (kebab-case). Las referencias externas entran aquí como nodes |
| `_outputs/`       | Entregables generados desde nodes (la última versión viva)                                  |
| `_outputs/_historico/` | Snapshots congelados y autocontenidos (output + `nodos-fuente/` + `_meta.md`); solo por orden explícita |
| `_design-system/` | On-demand: guarda un `design.md` que el usuario provee, solo si lo pide                      |

`_nodes/` es plano: nada de subcarpetas por tema. La navegación la dan este hub y las `## Conexiones` de cada node. El schema (la regla de mantenimiento) vive fuera del árbol: en `CLAUDE.md` (Code) o en las Instructions del proyecto (Cowork).

---

## Nodes vigentes

| Documento | Tema | Última actualización | Versión |
| --------- | ---- | -------------------- | ------- |
| _(vacío)_ | | | |

---

## Outputs activos

| Output | Construido sobre (nodes) | Última actualización | Estado |
| ------ | ------------------------ | -------------------- | ------ |
| _(vacío)_ | | | |

> **Estado**: `al día` o `requiere refresh`.

---

## Documentos pendientes de crear

- _(vacío)_

---

## Cómo se mantiene este hub

El agente lo mantiene en cada sesión gracias al schema en `CLAUDE.md` (Code) o en las Instructions del proyecto (Cowork): actualiza fechas/versiones al tocar nodes, marca como `requiere refresh` los outputs que dependen de un node modificado, agrega filas nuevas al crear/mover/renombrar, y actualiza la fecha de cabecera con cada cambio. Ver `docs/guia-de-uso.md` para el detalle.
