---
name: progress
description: Registro por fase — qué se hizo, decisiones, problemas y cómo se verificó
last_verified: 2026-11-19 (sobre el commit b72a21e, cierre de la fase 6)
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

## Fase 3 — Estructura HTML, SEO y Schema.org (PR #4, fusionado el 19-11-2026)

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

## Fase 4 — Estilos sin animaciones (PR #5, fusionado el 19-11-2026)

**Qué se hizo:** `styles.css` completo y quieto. No lleva `@keyframes`, `transition` ni
`animation`.

- **Bloques:** 1 Variables, 2 Base, 3 Utilidades, 4 Texturas, 5 Componentes, 6 Secciones y
  7 Escritorio (CS-05).
- **Primero móvil:** la base es de una columna y hay un único `@media (min-width: 861px)` (CS-03).
- **Pendiente para la fase 5:** los bloques 8 (Animaciones) y 9 (Movimiento reducido).
- `index.html` no ha cambiado.

**Decisiones de Mateo durante la fase:**

- **4 colores más en `DESIGN.md` §2**, como variables de `:root`:
  - `--color-cover` `#1C1C1C`: portadas de los singles.
  - `--color-outline` `#2A2A2A`: contorno de "IRON WOLF".
  - `--color-line-stub` `#4A4A4A`: línea discontinua del talón.
  - `--color-light` `#FFE2BE`: foco de luz de la portada.

  Los 2 primeros ya los usaba `DESIGN.md` fuera de la tabla. Los 2 últimos salían de la maqueta
  (commit `b0d72f7`).
- **Tamaños ajustados para que quepa la palabra más larga.** Con los valores de `DESIGN.md`,
  "TRAYECTORIA" y "PRESENTACIONES" se cortaban a 1440px (lo que sobresale de la caja no recibe
  la textura) y se salían de la pantalla en móvil. "BARCELONA" y "VALLADOLID" se salían de la
  entrada. Mateo eligió reducir lo justo; los valores están anotados en `DESIGN.md` §3 (`837e589`):

  | Elemento | Móvil | Escritorio |
  |---|---|---|
  | `h2` de sección | `clamp(2rem, 11vw, 3.25rem)` | `clamp(3.25rem, 8vw, 7.5rem)`, el de `DESIGN.md` |
  | "Próximas presentaciones" | `clamp(1.75rem, 8.5vw, 3rem)` | `clamp(2.5rem, calc(6.7vw - 12px), 5.25rem)`, unos 86px a 1440 |
  | "Trayectoria" | Igual que el resto de `h2` | Unos 111px a 1440 y con tope a partir de ahí |
  | Ciudad de la entrada | Hasta 44px | Escala entre 861 y ~1100px; a partir de ahí, 44px |
- **Halo oscuro** (`text-shadow` en tinta) detrás del logo, el menú, el antetítulo y el lema de
  la portada. Sin él, "ROCK · MADRID" (naranja sobre el humo) se quedaba en ≈ 2,8:1 y el menú en
  móvil en 4,35:1. La foto y los colores no cambian (`49f544a`).

- **Menú hamburguesa en móvil a pantalla completa** (pedido por Mateo al revisar el PR #5; lo
  hablamos antes de implementarlo).

  - **Primer intento** (`d3c5e80`): `<details>` y `<summary>`. Se descartó porque el panel no se
    cerraba al pulsar una sección.
  - **Versión final:** técnica `:target`, sin JavaScript.
    - "MENÚ" es un enlace a `#menu`, y el panel (`id="menu"`) se muestra a pantalla completa con
      `#menu:target`.
    - Al pulsar una sección, la dirección cambia, el panel desaparece y la página baja a esa
      sección.
    - "✕ CERRAR" lleva a `#inicio`, que es la portada, y se anuncia como "Cerrar menú".
    - Con `html:has(#menu:target)`, la página no hace scroll mientras el menú está abierto.
  - **Lo que se pierde**, aceptado por Mateo y anotado en `DESIGN.md` §6:
    - El lector de pantalla oye "enlace" en vez de "botón, expandido o contraído".
    - Esc no cierra el menú.
    - La dirección muestra `#menu` mientras está abierto.
  - **Textos nuevos en `CONTENT.md` §1:** "Menú", "Cerrar" y "Cerrar menú".
  - **Toques de naranja** (pedido por Mateo):
    - Número de sección ("01 /", "03 /", "04 /") en Special Elite naranja delante de cada enlace, y
      flecha → naranja a la derecha. Los dos son decorativos (`aria-hidden`): el lector de pantalla
      sigue oyendo solo "Sobre mí", "Trayectoria" y "Próximas presentaciones".
    - "CERRAR" relleno de naranja con el texto en tinta (5,73:1).
    - Borde rasgado naranja abajo del todo. La forma de los dientes vive ahora en `--tear-shape`,
      para no repetir el polígono.
    - Nada de esto se ve en escritorio.
  - **Ajustes para móviles estrechos:**
    - Hueco entre el logo y el menú: 16px en móvil y 40px en escritorio. Antes, a 320px, el botón
      bajaba a una segunda línea.
    - Botones del menú con 12px de relleno y un espaciado de letra de 0,14em, para que "CERRAR" no
      toque el logo.
    - Enlaces del panel con un espaciado de 0,14em, para que "PRÓXIMAS PRESENTACIONES" quepa en una
      línea desde 375px (a 320px se parte en dos).
  - **Prettier:** al guardar en VS Code, reformateaba `index.html` (`/>` en las etiquetas vacías,
    líneas partidas). Mateo eligió descartar ese formato, y el `.prettierignore` lo evita.

- **Cabecera fija y botón "Volver al inicio"** (pedidos por Mateo; lo hablamos antes de
  implementarlo).

  - **Cabecera fija** (`position: fixed`, alto de 102px):
    - Transparente sobre la portada; el fondo de tinta aparece en los primeros 120px de scroll,
      con `animation-timeline: scroll(root)`. Sin soporte, es de tinta desde el principio.
    - Al saltar a una sección, su borde queda a 102px y el título no se tapa (`scroll-padding-top`,
      ver abajo).
    - "✕ CERRAR" apunta ahora a `#cabecera`, la propia cabecera fija: el menú se cierra sin mover
      la página. Comprobado en Chrome a 4000px; queda pendiente probarlo en Safari en un iPhone.
  - **Botón "Volver al inicio"** (aviso del lector de pantalla, añadido a `CONTENT.md`):
    - Un cuadrado naranja de 52px con una flecha ↑, fijo abajo a la derecha.
    - Lleva borde de tinta y sombra dura de papel para destacar también sobre la Galería naranja.
    - En escritorio aparece entre el 60 % y el 80 % de la altura de la portada (`scroll(root)`,
      `60svh 80svh`); en móvil, ver abajo. Oculto, tiene `visibility: hidden`: no se puede
      pulsar ni enfocar.
    - Foco: doble anillo de papel y tinta.
  - **Para que el botón no tape el contenido** (Mateo eligió las tres medidas):
    - **Escritorio:** el botón va dentro del margen lateral de 64px (a 6px del borde). Comprobado
      a 861, 1440 y 1920px: no pisa ningún elemento de contenido.
    - **Móvil y tableta:** no hay margen, así que solo aparece al llegar a Próximas
      presentaciones (`view-timeline` de `.shows`, `entry 40%` a `entry 60%`). Ahí puede pisar el
      lado derecho de una entrada; es lo aceptado.
    - **Foco:** `scroll-padding-top: 102px` y `scroll-padding-bottom: 84px` en `html`. Con el
      teclado, ningún elemento con foco queda bajo la cabecera ni detrás del botón (WCAG 2.2,
      2.4.11). Sustituye al `scroll-margin-top` de las secciones, y los saltos siguen cayendo a
      102px.
  - **Desplazamiento suave:** `scroll-behavior: smooth`, solo con
    `prefers-reduced-motion: no-preference`.
  - **Se adelantan a la fase 4** dos piezas de la fase 5: el bloque 8 (Animaciones) de
    `styles.css` empieza con el fondo de la cabecera y la aparición del botón, y el desplazamiento
    suave va en el bloque Base.
  - **No se puede sin JavaScript:** esconder la cabecera al bajar y mostrarla al subir.

**Otros ajustes sin cambio de diseño** (`a8870ec`, `49f544a`):

- **Tildes:** la caja de los títulos con tinta gastada se amplía arriba y abajo
  (`padding-block` y `margin-block` negativo). Sin eso, la textura no pintaba las tildes de "MÍ",
  "RÍ" y "Ó".
- **Foto de Sobre mí en móvil y tableta:** centrada y con un ancho máximo de 520px. Así ni la
  foto girada ni la cinta se salen de la pantalla.
- **Crédito vertical de la portada en móvil:** el contenido le deja 28px a la derecha para no
  montarse sobre el botón.
- **Enlaces del menú:** relleno vertical de 15px en vez de los 12px de la maqueta, para llegar a
  44px de alto (A11Y-07).
- **Foco en la entrada del festival:** pasa a tinta, porque el naranja sobre naranja no se veía.
- **Sombra de la foto pegada:** usa la tinta al 45 % en vez del negro de la maqueta, para no
  meter un color fuera de la paleta.
- **"IRON WOLF" del pie:** es más ancho que la pantalla y queda recortado por los lados (igual que
  en la maqueta).

**Verificación (19-11-2026, Playwright 1.65 con el Chrome del equipo, fuera del repo):**

| Comprobación | Resultado |
|---|---|
| Sin scroll horizontal (`scrollWidth` = `clientWidth`) en 320, 360, 375, 414, 480, 600, 720, 768, 860, 861, 900, 1024, 1100, 1280, 1440 y 1920px | ✅ En todos |
| Ningún título más ancho que su caja (mismos 16 anchos) | ✅ En todos |
| Cada `section` mide al menos el alto de la ventana a 1440 × 900 y a 375 × 812 | ✅ Las 5 |
| Contraste de los colores planos (21 parejas de texto y fondo) | ✅ Todas ≥ 4,5:1; la más baja, 4,89:1 |
| Contraste sobre la foto de portada (píxeles reales detrás del texto, mediana) | ✅ Menú ≥ 8,4:1; logo ≥ 13:1; antetítulo 5,45 (1440), 4,96 (375) y 5,77:1 (768); lema ≥ 16:1 |
| `grep`: colores fuera de `:root`, `!important`, `@keyframes`, `transition`, `animation`, `_blob` | ✅ Ninguno |
| Zoom al 200 % (720 × 450 CSS): solapes de texto | ✅ Ninguno |
| Foco visible con Tab en los 15 elementos (escritorio) | ✅ Contorno de 3px: naranja, y tinta en la entrada del festival |
| Menú en móvil (375px, táctil) | ✅ Cerrado, los enlaces están ocultos. Al tocar "MENÚ", la dirección pasa a `#menu` y el panel ocupa 375 × 812; el logo queda encima y "CERRAR" ocupa el sitio de "MENÚ" (mismo borde derecho y la misma altura). Con el menú abierto, la rueda no mueve la página. "Trayectoria" cierra el menú y lleva a la sección. "CERRAR" cierra y deja en la portada. "Atrás" vuelve a abrirlo y otro "Atrás" lo cierra. Con teclado: Enter en "MENÚ" lo abre y Tab recorre "Cerrar menú" → Sobre mí → Trayectoria → Próximas presentaciones. En escritorio, incluso con `#menu`, no hay botones y la página hace scroll. W3C: 0 errores. El botón tiene un contraste de 11,1:1 sobre la foto |
| `index.html` sin cambios y sin `style=""` | ✅ |
| Capturas a 1440, 768 y 375px, por sección | ✅ En `design/screenshots/fase-4/`. Las compara Mateo con la maqueta |

**A tener en cuenta en la fase 5:**

- Fase 6: comprobar con VoiceOver el menú de móvil: "Menú, enlace", "Cerrar menú, enlace" y que el panel cerrado no se lee.

- La subida del nombre por líneas (`iw-rise`) necesita una máscara: en la maqueta, cada línea
  lleva un `span` dentro de otro con `overflow: hidden`. En `index.html`, cada línea es un solo
  `span`. Habrá que añadir el `span` interior (con aviso en el PR) o hacer la máscara con
  `clip-path`.
- El flash blanco de la galería usa `--color-white`, que `DESIGN.md` §2 reserva para el marco de
  la foto. §6 describe el flash blanco, así que se mantiene.
- En el bloque de movimiento reducido harán falta `!important`; CS-06 lo permite solo ahí.
- El bloque 8 ya tiene `header-fill` y `to-top-in`. Al apagar las animaciones con movimiento
  reducido, la cabecera queda de tinta y el botón visible, que es su estado seguro. Comprobarlo.

## Fase 5 — Animaciones y efectos (PR #6, fusionado el 19-11-2026)

**Qué se hizo:** las 15 animaciones de `DESIGN.md` §7, solo con CSS, en el bloque 8 de
`styles.css`, y el bloque 9 (Movimiento reducido). Las tres de la fase 4 (fondo de la cabecera,
aparición del botón ↑ y desplazamiento suave) se mantienen.

| Grupo | Animaciones |
|---|---|
| Transiciones (ratón) | Barra del menú, botones, flecha, entradas, redes, email, años, botón ↑ |
| Al cargar | Zoom de la foto (`iw-zoom`), subida del nombre por líneas (`iw-rise`), aparición del antetítulo, el lema y los botones (`iw-fade`) |
| Continuas | Grano (`iw-grain`), foco (`iw-flicker`), temblor e interferencia del nombre (`iw-shake`, `iw-glitch`), interferencia automática de las fotos (`iw-autoglitch`) |
| Galería con el ratón | Contraste, zoom con giro, franjas (`iw-slice`) y flash (`iw-flash`) |
| Scroll (`@supports (animation-timeline: view())`) | Títulos (`iw-slide`), aparición de bloques (`iw-reveal`), relleno de años (`iw-fill`), sello (`iw-stamp`), cortina (`iw-curtain`), profundidad (`iw-parallax`), deriva de "LIVE" (`iw-drift`) |

**Decisiones de Mateo:**

- **`span` interior en cada línea del `h1`** (`hero__line-inner`): la línea hace de máscara y el
  span sube desde debajo. La tinta gastada pasa al span interior; el texto no cambia.
- **Excepción en movimiento reducido:** se apaga todo
  (`*:not(.site-header, .to-top), *::before, *::after { animation: none !important; transition:
  none !important }`) salvo el fondo de la cabecera y la aparición del botón ↑, que solo cambian el
  color y la opacidad. Sin ellas, el botón taparía el texto en móvil.
- **Firefox y Safari los prueba Mateo a mano** (lista en el PR). No se descargaron los navegadores
  de Playwright.

**Fallos de la maqueta encontrados y corregidos:**

- **Giros fijos borrados:** el temblor y la aparición animan `transform`, y en la maqueta borraban
  el −2° del título y el ±0,5° de las entradas. Los giros pasan a la propiedad `rotate`, la
  aparición al bajar usa `translate` y la profundidad usa `scale` y `translate`, así que no se pisan
  (`54d7de7`).
- **Nombre naranja liso:** con la tinta gastada (`background-clip: text`), Chrome pinta el
  `text-shadow` encima de las letras. El desdoble se hace con `filter: drop-shadow` (`d83c40f`).
  El gris `#6E6E6E` de la maqueta, que no está en la paleta, pasa a `--color-label-light`.
- **Animaciones de scroll paradas:** `overflow: hidden` crea un contenedor de scroll. La cortina,
  la profundidad, "LIVE" y el título del pie seguían el scroll de su contenedor (que no se mueve) y
  se quedaban fijas. La Galería, `.shot__frame` y el pie pasan a `overflow: clip` (`b2d1d85`).
- **Scroll horizontal en móvil:** el sello empieza a escala 2,4 y sobresalía por la derecha.
  Trayectoria lleva `overflow-x: clip`.

**Verificación (19-11-2026, Chrome con Playwright):**

| Comprobación | Resultado |
|---|---|
| Animaciones activas en Chrome | ✅ Las 15 de §7, más `header-fill` y `to-top-in`. Al recorrer la página entera no queda ningún contenido oculto |
| El título no pierde el giro | ✅ `rotate: -2deg`, también en pleno temblor |
| Sin animaciones de scroll (CSS con los `@supports` falsos, como Firefox o WebKit) | ✅ Sin hacer scroll, ningún contenido oculto, a 1440 y a 375px |
| Movimiento reducido (`reducedMotion: 'reduce'`) | ✅ `getAnimations()` solo devuelve `header-fill` y `to-top-in` (la excepción), al cargar y tras el scroll. Todo visible y el título con su giro |
| Rendimiento (3 s de scroll suave) | ✅ 179 fotogramas, 16,7 ms de media y ninguno de más de 50 ms. Las animaciones solo usan `transform`, `rotate`, `scale`, `translate`, `opacity`, `filter`, `clip-path` y colores |
| Regresión de fases anteriores | ✅ W3C 0 errores; sin scroll horizontal en 16 anchos; títulos dentro de su caja; foco visible; zoom al 200 % sin solapes; antetítulo 4,94–5,77:1; botón ↑ y menú igual que en la fase 4 |
| `grep` | ✅ Un solo `<script>` (JSON-LD), sin `on*=`, sin `style=`, sin archivos `.js`; `!important` solo en el bloque 9; sin colores fuera de `:root` |
| Fotogramas clave | ✅ `design/screenshots/fase-5/` (no se grabó vídeo: Playwright pedía descargar su `ffmpeg`) |

## Fase 6 — Verificación final y entrega (rama `chore/phase-6-verification`)

**Qué se hizo:**

- Las 16 comprobaciones del plan, registradas en [`verification.md`](../verification.md) junto
  con los 8 criterios del enunciado.
- Capturas de página completa a 320, 375, 768, 1024 y 1440px en `design/screenshots/fase-6/`,
  hechas con movimiento reducido para que nada salga a medio animar.
- `README.md` nuevo en español. Se borraron `README.es.md` y `README.cn.md` de la plantilla.

**Decisiones de Mateo:**

- **No publicar en GitHub Pages:** los criterios del ejercicio no lo piden. Por eso no hay
  `canonical` ni `og:url`, y `og:image` sigue siendo relativa (`verification.md` §3.2).
- **Sustituir los README de la plantilla.**
- **Lighthouse, VoiceOver, Firefox y Safari (Mac e iPhone) los hace Mateo a mano**, con las guías
  del PR. Sus resultados se añaden a `verification.md` §4.
- Se envió `styles.css` al validador de CSS de W3C, con permiso de Mateo.

**Resultados:**

- **Validador de CSS:** 27 errores, todos de propiedades de animaciones de scroll que el validador
  aún no conoce (`animation-timeline`, `animation-range`, `timeline-scope` y `view-timeline`).
  Además, 42 avisos justificados (variables, prefijos `-webkit-` y colores iguales a propósito).
- **Revisión `rx-review`:** 2 hallazgos, corregidos:
  - Con el menú de móvil abierto, el foco y el lector de pantalla llegaban a la página tapada.
    Ahora se oculta con `visibility: hidden` (`770aeea`).
  - Clase `.visually-hidden` sin uso (`f22ff9c`). La regla CS-05 se actualizó.
- **Nota que queda abierta:** Google Fonts envía la IP del visitante a Google. No se cambia, porque
  `DESIGN.md` §3 lo fija.
- **Documentación:** se actualizaron `AGENTS.md` y la regla HT-01, que citaban el README de la
  plantilla y el antiguo menú en varias líneas.
- **Todo lo demás:** sin cambios respecto a la fase 5 (W3C HTML, schema.org, teclado, contraste,
  16 anchos, movimiento reducido, `grep` y textos).
- **Pruebas de Mateo:**
  - Lighthouse (Navigation): Accesibilidad 100 y SEO 100. Rendimiento y Buenas prácticas no se
    midieron.
  - Firefox y Safari (Mac): todo visible, con el scroll algo lento. Decidió no optimizarlo (causa
    probable en `verification.md` §3.6).
  - iPhone: menú, cabecera fija y botón ↑ bien.
  - VoiceOver: no se hizo, por decisión suya.
