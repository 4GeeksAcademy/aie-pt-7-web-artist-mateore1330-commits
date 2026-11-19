# Fase 2 — Imágenes

> Rama: `feat/phase-2-images` · PR a `main` · Depende de: fase 1 fusionada

## Objetivo

Generar a partir de los originales las imágenes finales que usará la web: ligeras, en WebP y con
los tamaños que pide el diseño. También la imagen para compartir en redes y el favicon. Va antes
del HTML para que la fase 3 ya pueda poner los `width` y `height` reales.

## Lee antes

- `.agents/rules/using-rules.md`, `git-and-docs.md` y `accessibility.md`.
- `DESIGN.md` §10 (Imágenes) y `assets/images/CREDITS.md`.

## Entregables

| Archivo | Origen | Tamaño final | Objetivo de peso |
|---|---|---|---|
| `assets/images/hero.webp` | `originals/hero.jpg` (1600 × 2400) | 1600px de ancho (bajar a 1280 si no entra en el peso) | < 250 KB |
| `assets/images/about.webp` | `originals/about.jpg` (1600 × 1067) | 1200px de ancho | < 150 KB |
| `assets/images/live-1.webp` | `originals/live-1.jpg` (1600 × 2401) | 1200px de ancho | < 200 KB |
| `assets/images/live-2.webp` | `originals/live-2.jpg` (1600 × 1069) | 1200px de ancho | < 150 KB |
| `assets/images/og.jpg` | Recorte de `hero` | 1200 × 630 | < 200 KB |
| `assets/favicon.svg` | Nuevo | 32 × 32 (vectorial) | < 1 KB |
| `memory-bank/progress.md` | — | Tabla con medidas y pesos reales | — |

Los originales **se quedan** en `assets/images/originals/`, para poder regenerar.

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b feat/phase-2-images
```

### Paso 2 — Fotos a WebP

Con `cwebp` (instalado en `/opt/homebrew/bin/cwebp`), por ejemplo:

```bash
cwebp -q 75 -resize 1200 0 assets/images/originals/about.jpg -o assets/images/about.webp
```

- Empezar con calidad 75 y bajarla de 5 en 5 (sin pasar de 60) hasta cumplir el peso. Si con 60
  no se cumple, reducir el ancho.
- **No pasarlas a blanco y negro**: eso lo hace el CSS. Los archivos quedan en color.
- Anotar en `progress.md` el ancho, el alto, la calidad y el peso final de cada una (son los
  `width` y `height` de la fase 3).

Commit: `feat: add optimized webp photos`

### Paso 3 — Imagen para redes (`og.jpg`)

Recorte de 1200 × 630 de `hero` en el que se vea el guitarrista (zona alta-central, equivalente a
`object-position: center 28%`). Con `sips` (incluido en macOS): primero escalar al ancho de 1200 y
después recortar a 630 de alto con el desplazamiento adecuado. Comprobar el recorte abriendo la
imagen.

Commit: `feat: add open graph image`

### Paso 4 — Favicon (pide aprobación)

El diseño no define favicon. **Antes de crearlo, propón a Mateo** este diseño y espera su sí:
un rombo naranja (`#E0692F`) sobre un cuadrado tinta (`#0E0E0E`), el mismo rombo que marca los
hitos de la línea del tiempo. SVG escrito a mano, sin texto (las fuentes no cargan en un favicon).

Commit: `feat: add svg favicon`

### Paso 5 — Cierre

- Revisar que `CREDITS.md` sigue siendo correcto (los nombres de archivo no cambian).
- `PLAN.md`, `progress.md` y `current-state.md` actualizados.
- Push y PR a `main` con la tabla de medidas y pesos. Pararse aquí.

## Criterios de aceptación

- [ ] Las 4 fotos WebP existen, se ven bien (sin artefactos visibles) y cumplen su peso.
- [ ] Las fotos siguen en color.
- [ ] `og.jpg` mide 1200 × 630, pesa menos de 200 KB y se ve el guitarrista.
- [ ] El favicon está aprobado por Mateo y pesa menos de 1 KB.
- [ ] `progress.md` tiene la tabla con ancho, alto y peso reales de cada imagen.
- [ ] Los originales siguen en `originals/`.
- [ ] PR a `main` sin fusionar.

## Fuera de alcance

- Usar las imágenes en el HTML (fase 3) o aplicar filtros (fase 4).
- Buscar fotos nuevas.
