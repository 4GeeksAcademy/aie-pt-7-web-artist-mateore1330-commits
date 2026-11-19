---
name: progress
description: Registro por fase — qué se hizo, decisiones, problemas y cómo se verificó
last_verified: 2026-11-19 (sobre el commit 748bb32, cierre de la fase 3)
---

# Progreso

> Una sección por fase, en orden. Mantén este archivo al día al cerrar cada fase (regla UR-04).
> El plan de cada fase está en [`plans/`](../plans/).

## Sesión de diseño (19-11-2026)

**Qué se hizo:** en una sesión previa a la implementación, Mateo y el agente fijaron, en este
orden: `BRIEFING.md` → `CONTENT.md` → maqueta iterada → `DESIGN.md` → `PLAN.md` y `plans/`.

**Decisiones:**

- Artista ficticio, Iron Wolf, rock de Madrid. Salas reales; fechas, festival y telonero
  inventados.
- Diseño aprobado: "propuesta 2 (más rock)" (cartel de gira gastado sobre base minimalista).
- Mateo no quiere la expresión "hard rock" en ningún texto: siempre "rock".
- La Galería no va en el menú (el encargo pide solo tres secciones).
- Fotos de Unsplash con crédito, en WebP, pasadas a blanco y negro con CSS.
- Git simplificado: `main` + una rama por fase, sin `develop`, sin GitHub Project ni issues.
- La implementación se hace en sesiones nuevas que solo dependen de lo que hay en el repositorio.

**Verificación:** Mateo aprobó `BRIEFING.md`, `CONTENT.md`, `DESIGN.md` y `PLAN.md` el 19-11-2026.

## Fase 0 — Preparación del repositorio (PR #1, fusionado el 19-11-2026)

**Qué se hizo:** `.gitignore` (primer commit de la rama), hook `.githooks/pre-commit` con gitleaks,
y versionados los documentos, la maqueta, las fotos originales, las texturas y el plan. 5 commits
(`bd8a0d6` a `49239f1`).

**Verificación:**

- El hook bloqueó un token falso `ghp_…` preparado en un archivo temporal (`leaks found: 1`,
  salida 1); el archivo no se commiteó y se borró.
- Los 4 commits posteriores al hook pasaron gitleaks (`no leaks found`); ninguno con
  `--no-verify`.
- `git status --short --ignored` tras el último commit: solo `!! .learn/`.

**A tener en cuenta:** `core.hooksPath` es local; en un clon nuevo hay que ejecutar
`git config core.hooksPath .githooks` (regla GD-03).

## Fase 1 — Archivos para el agente (PR #2, fusionado el 19-11-2026)

**Qué se hizo:**

- 6 archivos de reglas en `.agents/rules/` (UR, HT, CS, A11Y, SEO, GD), con frontmatter y reglas con
  Regla, Por qué, Haz, Evita y Cómo comprobarlo.
- 5 archivos de memory bank en `memory-bank/`.
- Skills `accessibility` y `seo` copiadas sin cambios del proyecto del dashboard.
- `AGENTS.md` (punto de entrada) y `CLAUDE.md` (`@AGENTS.md`).

**Decisiones:**

- `DESIGN.md` usa dos colores que no están en su tabla de §2: `#1C1C1C` (portadas de los singles,
  §6) y `#2A2A2A` (contorno de "IRON WOLF" del pie, §8). La regla CS-02 manda declararlos también
  como variables de `:root` y avisar en el PR de la fase 4.
- No se copia `skills-lock.json` del dashboard (el plan no lo pide).
- Se aclaró `PLAN.md` §4: una fase pasa a **En revisión** en su rama y a **Hecha** en el PR de la
  fase siguiente; lo que manda es la fusión en `main`.

**Prueba en frío (paso 6):** un subagente sin el contexto de la sesión, con la única instrucción
"Lee `AGENTS.md` de este repositorio y lo que te indique, y responde citando archivos e ID de
reglas". Se hizo dos veces.

| # | Pregunta | Respuesta esperada (y obtenida en la 2.ª prueba) |
|---|---|---|
| 1 | ¿Qué fase toca ahora y qué archivo la describe? | La fase 1 está en curso y sin fusionar; la siguiente es la 2 (`plans/phase-2-images.md`), que no se empieza hasta que la 1 esté en `main`. Cita `AGENTS.md` §4, `PLAN.md` §2 y §4, `current-state.md`, GD-01 |
| 2 | ¿Puedo añadir un `<script>` para un menú desplegable? | No: HT-01 (es su ejemplo de "Evita"), `AGENTS.md` §5, `PLAN.md` §3. El menú se hace con CSS (`flex-wrap`, `DESIGN.md` §6); si algo parece necesitar JS, se pregunta a Mateo |
| 3 | ¿De dónde saco el texto de Trayectoria? | `CONTENT.md` §5, tal cual, nunca de la maqueta (UR-02, HT-06); leer antes `git-and-docs.md`, `html.md` y `accessibility.md` (UR-01) |
| 4 | Cambiar el color de los botones: ¿qué reglas y dónde? | `git-and-docs.md`, `css.md`, `accessibility.md` (UR-01); CS-02 y A11Y-06. Un valor nuevo de color: primero `DESIGN.md` §2 con aprobación de Mateo y después `:root`; cambiar qué variable usa el botón: solo `styles.css` |
| 5 | He terminado una fase: ¿rama y quién fusiona? | Actualizar `PLAN.md`, `progress.md` y `current-state.md` (UR-04), push y PR a `main` con criterios marcados, avisar y parar; **fusiona Mateo** (GD-04), nunca `--no-verify` (GD-03) |

**1.ª prueba:** las 5 respuestas fueron correctas. Señaló dos dudas, que se corrigieron en
`2dfeb1f`:

- La 4 no dejaba claro si cambiar un color exige cambiar antes `DESIGN.md`. Se añadió a CS-02.
- No quedaba claro qué significa una fase "En revisión". Se aclaró en `AGENTS.md` §4.

También se unificó en UR-01 "antes de analizar o modificar".

**2.ª prueba:** las 5 respuestas fueron correctas y la 4 ya era inequívoca. Señaló la redacción de
`PLAN.md` §4 sobre cuándo se marca "Hecha", y se aclaró en el commit de cierre. El resto de lo que
señaló ya estaba documentado o se resuelve al abrir el PR:

- La contradicción de colores de `DESIGN.md`.
- El README de la plantilla con Tailwind.
- La excepción de Git frente a las reglas globales de Mateo.

## Fase 2 — Imágenes (PR #3, fusionado el 19-11-2026)

**Qué se hizo:** las 4 fotos en WebP con `cwebp`, en color (el blanco y negro lo pone el CSS), la
imagen para redes `og.jpg` y el favicon. Los originales siguen en `assets/images/originals/`.

**Medidas y pesos reales** (son los `width` y `height` que usa la fase 3):

| Archivo | Ancho × alto | Calidad | Peso | Objetivo |
|---|---|---|---|---|
| `assets/images/hero.webp` | 1600 × 2400 | 75 | 178 758 B (175 KB) | < 250 KB ✅ |
| `assets/images/about.webp` | 1200 × 801 | 75 | 40 534 B (40 KB) | < 150 KB ✅ |
| `assets/images/live-1.webp` | 1200 × 1801 | 75 | 20 342 B (20 KB) | < 200 KB ✅ |
| `assets/images/live-2.webp` | 1200 × 802 | 75 | 11 854 B (12 KB) | < 150 KB ✅ |
| `assets/images/og.jpg` | 1200 × 630 | JPEG 80 (`sips`) | 150 224 B (147 KB) | < 200 KB ✅ |
| `assets/favicon.svg` | 32 × 32 (vectorial) | — | 185 B | < 1 KB ✅ |

Comandos:

```bash
cwebp -q 75 -resize 1600 0 assets/images/originals/hero.jpg -o assets/images/hero.webp
cwebp -q 75 -resize 1200 0 assets/images/originals/<foto>.jpg -o assets/images/<foto>.webp
sips -s format jpeg -s formatOptions 80 --resampleWidth 1200 assets/images/originals/hero.jpg --out hero-1200.jpg   # 1200 × 1800
sips -c 630 1200 --cropOffset 540 0 hero-1200.jpg --out assets/images/og.jpg
```

**Decisiones:**

- Las 4 fotos entraron en el peso con la calidad inicial (75), así que no hizo falta bajarla.
- **Recorte de `og.jpg`:** el plan proponía el equivalente a `center 28%` (desplazamiento de 328 px
  sobre 1800). Con él se veía la cabeza y los hombros, pero la guitarra quedaba fuera. Mateo eligió
  un recorte más bajo (desplazamiento de 540 px, ≈ `center 46%`), con el guitarrista y la guitarra.
- **Favicon:** propuesta del plan, aprobada por Mateo: rombo `#E0692F` sobre cuadrado `#0E0E0E`,
  el mismo rombo que marca los hitos. Sin texto.
- `live-2` ya es en blanco y negro en el original: se deja tal cual.

**Verificación:**

- Las 4 fotos se revisaron a ojo (convertidas a PNG), también con recortes a tamaño real de
  `live-1` y `live-2`, que son las que menos pesan. No hay artefactos visibles.
- `og.jpg` se abrió para comprobar el encuadre.
- El favicon se renderizó a 256 px.
- `CREDITS.md` sigue siendo correcto: los nombres de archivo no cambian.

## Fase 3 — Estructura HTML, SEO y Schema.org (rama `feat/phase-3-html`)

**Qué se hizo:**

- `index.html` completo, con la estructura de `plans/phase-3-html.md`: enlace de salto, `header`,
  `nav`, `main` con 5 `section` y `aria-labelledby`, `footer` y la capa de grano.
- Todos los textos copiados de `CONTENT.md`.
- `<head>` con la lista de SEO-01.
- JSON-LD en `@graph` (SEO-03).
- `styles.css` vacío, con un comentario de cabecera.

Clases BEM preparadas para la fase 4:

| Parte | Clases |
|---|---|
| Cabecera y menú | `site-header`, `nav` |
| Portada | `hero` |
| Secciones (comunes) | `section__num`, `section__title`, `section__lead` |
| Sobre mí | `polaroid`, `facts` |
| Galería | `shot`, `shot__img--live-1`/`--live-2` |
| Trayectoria | `timeline`, `milestone`, `stamp` |
| Discografía | `discography`, `release` |
| Próximas presentaciones | `tickets`, `ticket`, `ticket--festival` |
| Pie | `site-footer`, `social`, `mail` |
| Comunes | `tape`, `tear--paper`/`--accent`/`--ink`, `btn--primary`/`--ghost`/`--ticket`/`--ticket-dark` |

**Decisiones:**

- **Direcciones de las salas** (Mateo eligió buscarlas en la web oficial, SEO-04):

  | Sala | `streetAddress` | `postalCode` | Fuente oficial |
  |---|---|---|---|
  | Razzmatazz | C/ Almogàvers 122 | — (la web no lo da junto a esa dirección) | https://www.salarazzmatazz.com/info/ ("C/ Almogàvers 122", acceso principal) |
  | Moon | Calle San Vicente 200 | — (la web no lo da) | https://www.moonvalencia.es/web/contacto/ ("Calle San Vicente 200, València") |
  | Kafe Antzokia | San Vicente 2 | 48001 | https://www.kafeantzokia.eus/es/contacto/ ("Done Bikendi / San Vicente 2, 48001 Bilbao") |

  Comprobadas el 19-11-2026 descargando cada página. El Meseta Rock Festival es ficticio: solo
  `addressLocality: "Valladolid"`.
- **Fecha del talón:** el texto de `CONTENT.md` "17 · Sáb · Abr 2027" va en tres `span` (`ticket__day`,
  `ticket__sep` con " · " y `ticket__date`), para que la fase 4 pueda separar el día grande sin
  perder el texto.
- **Discografía:** el tipo y el año de la tabla de `CONTENT.md` se muestran como "EP · 2024".
- **Sin `canonical`, `og:url` ni URL absolutas** hasta la decisión de publicar (fase 6). Por eso
  `og:image` y las `image` del JSON-LD son relativas.
- El `h1` lleva un espacio entre sus dos `span`, para que el lector de pantalla lea "Iron Wolf" y no
  "IronWolf".

**Verificación (19-11-2026):**

| Comprobación | Resultado |
|---|---|
| Validador Nu de W3C (`curl … validator.w3.org/nu/?out=json`) | ✅ 0 errores y 0 avisos |
| Esquema de títulos | ✅ 1 `h1`; `h2` en Sobre mí, Galería, Trayectoria, Próximas presentaciones y el pie; `h3` en los 6 hitos, Discografía y las 4 ciudades; sin saltos |
| Validador de schema.org (servicio `validator.schema.org/validate`) | ✅ 0 errores y 0 avisos. Detecta `MusicGroup`, `MusicAlbum`, `MusicRecording`, `MusicEvent` ×4, `MusicVenue`, `PostalAddress`, `Place` y `Offer` |
| Prueba de resultados enriquecidos de Google | ✅ La pasó Mateo el 19-11-2026, pegando el bloque JSON-LD (el agente lo intentó con Claude in Chrome y Google respondió "vuelve a intentarlo dentro de unas horas"). Resultado: "Se han detectado 4 elementos válidos", **Eventos** con 4 elementos válidos y "Detectados problemas no críticos": avisos de campos recomendados que no se rellenan porque no hay datos (SEO-04). 0 errores |
| `grep`: `<script` | ✅ Solo el `application/ld+json` |
| `grep`: `on…=`, `style=`, `<style`, `javascript:`, "hard rock", tabuladores, archivos `.js` | ✅ Ninguno |
| Anclas | ✅ Cada `href="#…"` tiene su `id` |
| Imágenes | ✅ Las 2 `<img>` con `alt` de `CONTENT.md`, `width` y `height` reales; la portada con `fetchpriority="high"`, la otra con `loading="lazy"` |
| Textos frente a `CONTENT.md` (script) | ✅ Los 119 textos y todos los `alt`/`aria-label` están en `CONTENT.md`; solo "EP ·" y "Single ·" son combinaciones de la tabla |
| Teclado sin CSS (Chrome, Tab real) | ✅ 15 elementos en orden lógico; "Saltar al contenido" lleva a `#contenido` |
| Skills `accessibility` y `seo` | ✅ Nada que corregir en el HTML. Quedan para otras fases: contraste, foco y objetivos táctiles (4), movimiento (5), `robots.txt`, sitemap, `canonical`, HTTPS y VoiceOver (6) |

**Problemas:**

- El puerto 8000 estaba ocupado por Docker en este equipo. La vista previa se hizo con
  `python3 -m http.server 8080 --bind 127.0.0.1`.
- Claude in Chrome no tiene permiso para leer `validator.schema.org` ni las webs de las salas.
  Se usó `curl` en su lugar.
