# Fase 3 — Estructura HTML, SEO y Schema.org

> Rama: `feat/phase-3-html` · PR a `main` · Depende de: fase 2 fusionada

## Objetivo

Escribir `index.html` completo: estructura semántica, todos los textos de `CONTENT.md`, el
`<head>` con SEO y Open Graph, y los datos estructurados de Schema.org. **Sin estilos**: solo se
enlaza `styles.css` (que se crea vacío). Al terminar, la página tiene que entenderse y usarse
perfectamente sin CSS, con teclado y con lector de pantalla.

## Lee antes

- `.agents/rules/using-rules.md`, `html.md`, `accessibility.md`, `seo-schema.md` y
  `git-and-docs.md`.
- `CONTENT.md` entero, `DESIGN.md` §8 y §11, y la estructura de `design/mockup-propuesta-2.html`
  (solo la estructura: las clases y los estilos de la maqueta **no** se copian tal cual).
- Las skills `accessibility` y `seo`.
- Los `width` y `height` reales de las imágenes en `memory-bank/progress.md` (fase 2).

## Entregables

| Archivo | Contenido |
|---|---|
| `index.html` | La página completa |
| `styles.css` | Vacío, con un comentario de cabecera (se rellena en la fase 4) |

## Estructura que debe tener `index.html`

```text
html lang="es"
├── head  (ver paso 2)
└── body
    ├── a.skip-link → #contenido                       "Saltar al contenido"
    ├── header
    │   ├── a → #inicio                                "Iron Wolf"
    │   └── nav aria-label="Navegación principal"
    │       └── ul > li > a  (#sobre-mi, #trayectoria, #presentaciones)
    ├── main id="contenido"
    │   ├── section#inicio      aria-labelledby → h1   Portada
    │   ├── section#sobre-mi    aria-labelledby → h2   01 Sobre mí
    │   ├── section#galeria     aria-labelledby → h2   02 Galería
    │   ├── section#trayectoria aria-labelledby → h2   03 Trayectoria
    │   └── section#presentaciones aria-labelledby → h2  04 Próximas presentaciones
    ├── footer
    └── div.grain aria-hidden="true"                   (capa de grano, vacía)
```

Etiquetas que se esperan en cada parte:

| Parte | HTML semántico |
|---|---|
| Portada | `h1` con dos `span` (líneas "Iron" y "Wolf"); lema en `p`; botones como `a`; foto como `img` con su `alt` y `fetchpriority="high"`; capas de luz y degradado como `div aria-hidden` |
| Sobre mí | `figure` con `img` y `figcaption` (los dos textos del pie); texto en `p` con el `strong`; fichas en `dl` (`dt` y `dd`) |
| Galería | Dos `figure`; cada foto, un `div role="img" aria-label="…"` (necesita fondo CSS para los efectos, ver `DESIGN.md` §10) con sus capas `span.flash` y `span.curtain` con `aria-hidden`; `figcaption` con la cinta y el crédito; "LIVE" en `p aria-hidden` |
| Trayectoria | Hitos en `ol`; cada hito, un `li` con `time datetime="AAAA"`, `h3` y `p`; títulos de obras en `cite`; sello "SOLD OUT" con `aria-hidden`; Discografía con `h3` y `ul`; portadas como `div aria-hidden` |
| Próximas presentaciones | `ol` de entradas; cada una, un `li` con `time datetime="2027-04-17"` (talón), `h3` con la ciudad, recinto en `p` y enlace con su `aria-label` de `CONTENT.md`; muescas con `aria-hidden` |
| Pie | `h2` con la llamada; email en `address` con `a href="mailto:…"`; redes en `ul` de enlaces con `aria-label` e icono SVG en línea con `aria-hidden="true"` y `focusable="false"`; copyright en `p` con `small`; "IRON WOLF" gigante en `p aria-hidden` |
| Decoración | Números de sección, bordes rasgados (`div.tear`), trozos de cinta: siempre `aria-hidden="true"` |

**Enlaces de ejemplo** (ni entradas ni redes existen): se usan dominios reservados que nunca
apuntan a nadie real. Entradas: `https://example.com/entradas/<ciudad>-<fecha>`. Redes:
`https://example.com/instagram`, `…/youtube` y `…/spotify`. Email: `booking@ironwolf.example`.

## Pasos

Un commit por paso.

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b feat/phase-3-html
```

### Paso 2 — Esqueleto y `<head>`

`index.html` con el `<head>` completo y `styles.css` vacío:

- `<meta charset="utf-8">` y `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- `<title>` y `<meta name="description">` de `CONTENT.md` §0.
- Open Graph: `og:type` (`website`), `og:title`, `og:description`, `og:image`
  (`assets/images/og.jpg`), `og:locale` (`es_ES`). Twitter card: `summary_large_image`.
  `canonical` y `og:url` **solo** si Mateo decide publicar (ver `PLAN.md` §7); si no, se omiten.
- `<meta name="theme-color" content="#0E0E0E">` y `<link rel="icon" href="assets/favicon.svg" type="image/svg+xml">`.
- Google Fonts como en `DESIGN.md` §3 y `<link rel="stylesheet" href="styles.css">`.

Commit: `feat: add html document head with seo metadata`

### Paso 3 — Cabecera, navegación y portada

Commit: `feat: add header, navigation and hero section`

### Paso 4 — Sobre mí y Galería

Commit: `feat: add about and gallery sections`

### Paso 5 — Trayectoria

Commit: `feat: add career timeline and discography`

### Paso 6 — Próximas presentaciones y pie

Commit: `feat: add upcoming shows and footer`

### Paso 7 — Schema.org (JSON-LD)

Un único `<script type="application/ld+json">` al final del `<head>`, con `@graph`:

- **`MusicGroup`** (`@id: "#iron-wolf"`): Iron Wolf, el proyecto del artista con su banda de
  directo. `name`, `description` (la de `CONTENT.md` §0), `genre: "Rock"`, `foundingDate: "2022"`,
  `foundingLocation` (Vallecas, Madrid, ES), `image` (`hero.webp`), `album` y `track`. Se usa
  `MusicGroup` y no `Person` porque es el tipo que Google y schema.org recomiendan para quien
  actúa en un evento musical, y porque no tenemos nombre real (decisión del `BRIEFING.md`).
- **`MusicAlbum`**: *Howl*, `albumReleaseType: "EPRelease"`, `datePublished: "2024"`,
  `byArtist` → `#iron-wolf`.
- **`MusicRecording`** × 3: *Silver Fang* (2022), *Midnight Engine* (2023) y *Rust* (2023),
  `byArtist` → `#iron-wolf`.
- **`MusicEvent`** × 4: `name` (por ejemplo, "Iron Wolf · Gira 2027 · Barcelona"; el del festival,
  "Meseta Rock Festival 2027"), `startDate` (solo la fecha, sin hora: la hora no la sabemos),
  `eventStatus: EventScheduled`, `eventAttendanceMode: OfflineEventAttendanceMode`,
  `location` (`MusicVenue` con `name` y `address` → `PostalAddress` con `addressLocality` y
  `addressCountry: "ES"`), `performer` → `#iron-wolf`, `image` y `offers` (`Offer` con la `url`
  de ejemplo de las entradas).
- **Datos que no se inventan:** sin hora, sin precio y sin organizador. El `streetAddress` de las
  salas reales solo se pone si se ha comprobado en la web oficial de la sala (anotar la fuente en
  `progress.md`). El festival es ficticio: solo `addressLocality: "Valladolid"`.

Commit: `feat: add json-ld structured data`

### Paso 8 — Validación

1. **Validador Nu de W3C** (envía el HTML a un servicio externo; el contenido es público):

   ```bash
   curl -s -H "Content-Type: text/html; charset=utf-8" --data-binary @index.html \
     "https://validator.w3.org/nu/?out=json"
   ```

   Objetivo: 0 errores. Los avisos se revisan uno a uno y se justifican en el PR.
2. **Esquema de títulos**: listar `h1`–`h3` en orden y comprobar que no hay saltos.
3. **Validador de schema.org** (https://validator.schema.org) con el JSON-LD: 0 errores.
4. **Prueba de resultados enriquecidos de Google**
   (https://search.google.com/test/rich-results), pegando el código: que detecte los eventos. Si
   el agente no puede usarla, deja las instrucciones a Mateo en el PR.
5. **Comprobaciones con `grep`**: ningún `style=`, ningún `<script` salvo el JSON-LD, ningún
   `on…=` y ninguna aparición de "hard rock".
6. **Sin CSS**: abrir la página en local y recorrerla con Tab. Todo es alcanzable, en orden lógico,
   y el enlace "Saltar al contenido" funciona.
7. **Textos**: comparar cada texto con `CONTENT.md` (se copian tal cual).
8. Auditoría rápida con las skills `accessibility` y `seo`. Los hallazgos se corrigen o se
   justifican.

Si hay que corregir algo: commit `fix: …`.

### Paso 9 — Cierre

`PLAN.md`, `progress.md` (resultados de las validaciones) y `current-state.md` actualizados. Push
y PR a `main`. Pararse aquí.

## Criterios de aceptación

- [ ] Validador Nu de W3C: 0 errores.
- [ ] Un solo `h1`; un `h2` por sección y en el pie; `h3` en hitos, Discografía y ciudades; sin
      saltos de nivel.
- [ ] Landmarks: `header`, `nav` con `aria-label`, `main`, 5 `section` con `aria-labelledby` y
      `footer`.
- [ ] Todos los textos coinciden con `CONTENT.md`.
- [ ] Toda `<img>` tiene `alt` (de `CONTENT.md`), `width` y `height`; las fotos de la galería
      tienen `role="img"` y `aria-label`.
- [ ] Todo lo decorativo tiene `aria-hidden="true"`.
- [ ] JSON-LD válido en schema.org (0 errores) y eventos detectados en la prueba de Google (o
      instrucciones para Mateo).
- [ ] 0 JavaScript ejecutable, 0 `style=""` y 0 "hard rock" (prueba con `grep` en el PR).
- [ ] Se navega entera con teclado sin CSS.
- [ ] PR a `main` sin fusionar.

## Fuera de alcance

- Cualquier estilo (fase 4) o animación (fase 5).
- Textos nuevos que no estén en `CONTENT.md`.
