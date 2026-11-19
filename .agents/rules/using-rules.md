---
name: using-rules
description: Qué archivo de reglas leer antes de editar, qué fuente manda y cómo añadir o cambiar reglas
scope: "**"
---

# Uso de las reglas

Reglas para cualquier agente (o persona) que edite este repositorio. Todas se apoyan en un
documento del propio repositorio: `PLAN.md`, `BRIEFING.md`, `CONTENT.md`, `DESIGN.md`,
`design/README.md` o los planes de `plans/`.

## UR-01 · Lee las reglas que correspondan antes de editar

**Regla:** Antes de modificar un archivo, lee siempre [`git-and-docs.md`](git-and-docs.md) y,
además, los archivos de reglas que correspondan a lo que vas a tocar:

| Si vas a tocar… | Lee también |
|---|---|
| `index.html` (estructura, textos, atributos) | [`html.md`](html.md) y [`accessibility.md`](accessibility.md) |
| El `<head>` de `index.html` o el bloque JSON-LD | [`seo-schema.md`](seo-schema.md) y [`html.md`](html.md) |
| `styles.css` | [`css.md`](css.md) y [`accessibility.md`](accessibility.md) |
| `assets/images/**` o `assets/favicon.svg` | [`accessibility.md`](accessibility.md) (`alt`, `width`, `height`) |
| `PLAN.md`, `plans/**`, `memory-bank/**`, `AGENTS.md`, `.agents/**` | Solo `git-and-docs.md` y esta regla |

**Por qué:** [`AGENTS.md`](../../AGENTS.md) obliga a revisar `./.agents/rules` antes de actuar,
pero no dice qué archivo aplica a cada tarea. Cada plan de fase lista las reglas que hay que leer
(por ejemplo, [`plans/phase-3-html.md`](../../plans/phase-3-html.md) § "Lee antes").

**✅ Haz:** para añadir la sección de Trayectoria en `index.html`, lee `git-and-docs.md`,
`html.md` y `accessibility.md`.

**❌ Evita:** cambiar un color en `styles.css` sin haber leído `css.md`, o tocar el JSON-LD sin
haber leído `seo-schema.md`.

**Cómo comprobarlo:** al terminar, cita el ID de cada regla aplicada en tu respuesta y en el PR
(por ejemplo, "HT-01, HT-05, A11Y-02, GD-03").

## UR-02 · Respeta qué documento manda en cada tema

**Regla:** Cuando dos fuentes no coincidan, manda la de esta tabla. Si algo no está en ninguna,
**se pregunta a Mateo**: no se inventa.

| Tema | Fuente que manda |
|---|---|
| Textos, `alt`, `aria-label` y créditos | [`CONTENT.md`](../../CONTENT.md) |
| Todo lo visual: colores, tipografía, componentes, animaciones, móvil | [`DESIGN.md`](../../DESIGN.md) |
| Quién es el artista y qué pide para su web | [`BRIEFING.md`](../../BRIEFING.md) |
| Valores exactos (`@keyframes`, `clip-path`, sombras, giros) | [`design/mockup-propuesta-2.html`](../../design/mockup-propuesta-2.html), solo como referencia: si contradice a `DESIGN.md`, vale `DESIGN.md` |
| Fases, ramas, criterios de aceptación | [`PLAN.md`](../../PLAN.md) y [`plans/`](../../plans/) |

**Por qué:** `PLAN.md` §1 fija este orden y dice "Si algo no está en estos documentos, se
pregunta a Mateo. No se inventa." [`design/README.md`](../../design/README.md) dice que la maqueta
es solo referencia y que sus textos no valen ("Los textos salen de `CONTENT.md`, no de la
maqueta").

**✅ Haz:** copiar el `alt` de la foto de portada de `CONTENT.md` §2, aunque la maqueta tenga otro.

**❌ Evita:** copiar un texto de la maqueta, o rellenar con un dato "razonable" (una hora de
concierto, un precio, un nombre de músico) que no está en ningún documento.

**Cómo comprobarlo:** cada texto visible de `index.html` se encuentra literalmente en `CONTENT.md`
(`grep -F "<texto>" CONTENT.md`).

## UR-03 · Toda regla nueva se apoya en un documento del repositorio

**Regla:** Al añadir o cambiar una regla, usa la plantilla de abajo y apóyala en un documento del
repositorio, citando su ruta y su sección. No se aceptan "buenas prácticas" genéricas sin esa
referencia.

**Por qué:** las reglas de este proyecto existen para que cualquier agente continúe solo con lo
que hay en el repositorio (objetivo de [`plans/phase-1-agent-harness.md`](../../plans/phase-1-agent-harness.md)).
Una regla sin fuente no se puede comprobar ni discutir.

**✅ Haz:** "Toda `<img>` lleva `width` y `height`. Por qué: `DESIGN.md` §10".

**❌ Evita:** "Escribe CSS limpio", que no cita nada.

**Cómo comprobarlo:** cada regla de esta carpeta tiene un **Por qué** con una ruta del
repositorio.

## UR-04 · Mantén el `memory-bank` al día al cerrar cada fase

**Regla:** Lee [`memory-bank/`](../../memory-bank/) al empezar. Al cerrar una fase (y siempre que
tu cambio haga falso algo de lo que dice), actualízalo en la misma rama:

| Si cambias… | Actualiza |
|---|---|
| Cualquier fase (al cerrarla) | [`progress.md`](../../memory-bank/progress.md) y [`current-state.md`](../../memory-bank/current-state.md) |
| Archivos, secciones, IDs o bloques de `styles.css` | [`architecture.md`](../../memory-bank/architecture.md) |
| Herramientas, fuentes o forma de previsualizar | [`tech-stack.md`](../../memory-bank/tech-stack.md) |
| El alcance del ejercicio o qué decide cada documento | [`product-overview.md`](../../memory-bank/product-overview.md) |

Actualiza también el campo `last_verified` con la fecha y el commit sobre el que lo comprobaste,
y el estado de la fase en la tabla de `PLAN.md` §4.

**Por qué:** cada plan de fase termina con un paso de cierre que pide actualizar `PLAN.md`,
`progress.md` y `current-state.md` (por ejemplo, [`plans/phase-3-html.md`](../../plans/phase-3-html.md)
paso 9). Un agente nuevo decide qué fase toca leyendo esos archivos.

**✅ Haz:** al cerrar la fase 2, anotar en `progress.md` las medidas y pesos reales de cada WebP.

**❌ Evita:** dejar `current-state.md` diciendo que algo falta cuando ya está hecho.

**Cómo comprobarlo:** el PR de cada fase incluye cambios en `PLAN.md`, `progress.md` y
`current-state.md`.

### Plantilla de una regla

```markdown
## <ID> · <Título corto>

**Regla:** qué hacer, en modo imperativo.

**Por qué:** el documento del repositorio que la justifica, con su ruta y sección.

**✅ Haz:** ejemplo correcto.

**❌ Evita:** el error concreto que la regla previene.

**Cómo comprobarlo:** comando o revisión que demuestra que se ha cumplido.
```

Cada archivo de reglas lleva frontmatter con `name`, `description` y `scope`.

## Índice de reglas

| Archivo | Alcance | Reglas |
|---|---|---|
| [`using-rules.md`](using-rules.md) | Todo el repositorio | UR-01 a UR-04 |
| [`html.md`](html.md) | `index.html` | HT-01 a HT-07 |
| [`css.md`](css.md) | `styles.css` | CS-01 a CS-07 |
| [`accessibility.md`](accessibility.md) | `index.html`, `styles.css`, imágenes | A11Y-01 a A11Y-08 |
| [`seo-schema.md`](seo-schema.md) | `<head>` y JSON-LD de `index.html` | SEO-01 a SEO-04 |
| [`git-and-docs.md`](git-and-docs.md) | Ramas, commits, PR y documentación | GD-01 a GD-05 |
