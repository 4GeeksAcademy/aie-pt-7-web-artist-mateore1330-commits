# design/ — Maqueta aprobada (solo referencia)

`mockup-propuesta-2.html` es el código de la maqueta "propuesta 2 (más rock)", aprobada por Mateo
el 19-11-2026. Se hizo en el lienzo de diseño de Claude (https://claude.ai/artifact/K6wbiVyecCu598LWjFbagA,
privado).

## Cómo usarla

- **Manda `DESIGN.md`.** Esta maqueta es una referencia para copiar valores exactos: fotogramas
  de las animaciones (`@keyframes`), recortes con `clip-path`, efectos de las fotos, sombras,
  giros y tamaños. Si algo no coincide con `DESIGN.md`, vale `DESIGN.md`.
- **Los textos salen de `CONTENT.md`**, no de la maqueta.
- **No se publica ni se abre como web**: no funciona fuera del lienzo. Usa un formato propio
  (`<x-dc>`, `<helmet>`, `{{accent}}`, `data-props`, `support.js`) que no forma parte de la web
  final. `DESIGN.md` §12 explica qué cambia al pasarla a `index.html` + `styles.css`.

## Equivalencia de las imágenes

Dentro de la maqueta, las imágenes apuntan a direcciones internas del lienzo (`/_blob/…`). Estos
son los archivos reales del repositorio:

| En la maqueta | Archivo real | Contenido |
|---|---|---|
| `/_blob/2799d71eef9b6ce33ff874e0fd9f622f` | `assets/images/originals/hero.jpg` | Portada: guitarrista a contraluz entre humo |
| `/_blob/fd51dfa4f73154a40b96ac62de4f285a` | `assets/images/originals/about.jpg` | Sobre mí: guitarrista melenudo |
| `/_blob/e08956287b6730773691c32920e1209e` (clase `.p-live2`) | `assets/images/originals/live-1.jpg` | Galería, foto 1: silueta con foco |
| `/_blob/458c65055f131fa6d16b072de120c486` (clase `.p-live1`) | `assets/images/originals/live-2.jpg` | Galería, foto 2: guitarrista de rodillas |
| `/_blob/84615cefa8fe71da6d700578b978c1f3` | `assets/textures/noise.svg` | Grano de película |
| `/_blob/b429c88515770ab88ff2110c527ed906` | `assets/textures/wear-dark.svg` | Tinta gastada, arañazos oscuros |
| `/_blob/5deeddd2f0fe5b18e17a4e9cb92a609f` | `assets/textures/wear-light.svg` | Tinta gastada, arañazos claros |

**Atención:** en la maqueta, las clases `.p-live1` y `.p-live2` están **cruzadas** respecto a los
nombres finales. En la web final, la foto 1 de la galería es `live-1` (la silueta) y la foto 2 es
`live-2` (de rodillas), como dicen `CONTENT.md` y `DESIGN.md`.
