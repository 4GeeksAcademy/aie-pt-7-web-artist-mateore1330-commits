---
name: seo-schema
description: El <head> obligatorio, el h1 único y los datos estructurados JSON-LD de Schema.org, sin inventar datos
scope: "<head> y <script type=\"application/ld+json\"> de index.html"
---

# Reglas de SEO y Schema.org

El artista quiere "que le encuentren en los buscadores cuando alguien busque rock en Madrid o sus
conciertos" ([`BRIEFING.md`](../../BRIEFING.md)); los datos estructurados son el criterio 7 de
`PLAN.md` §5. Para auditar, usa la skill [`seo`](../skills/seo/SKILL.md).

## SEO-01 · El `<head>` lleva estas etiquetas, ni más ni menos

**Regla:** El `<head>` de `index.html` contiene, con los textos de `CONTENT.md` §0:

- `<meta charset="utf-8">` y `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- `<title>` y `<meta name="description">`.
- Open Graph: `og:type` (`website`), `og:title`, `og:description`, `og:image`
  (`assets/images/og.jpg`) y `og:locale` (`es_ES`). Twitter: `twitter:card` =
  `summary_large_image`.
- `<meta name="theme-color" content="#0E0E0E">` y
  `<link rel="icon" href="assets/favicon.svg" type="image/svg+xml">`.
- Google Fonts con los `preconnect` y el `<link>` de `DESIGN.md` §3, y
  `<link rel="stylesheet" href="styles.css">`.
- El bloque JSON-LD (SEO-03), al final.

`canonical` y `og:url` (y las URL absolutas) **solo** si Mateo decide publicar en GitHub Pages
(`PLAN.md` §7); si no, se omiten y se explica en `verification.md`.

**Por qué:** lista del paso 2 de [`plans/phase-3-html.md`](../../plans/phase-3-html.md); textos en
`CONTENT.md` §0; decisión abierta en `PLAN.md` §7.

**✅ Haz:** `<title>Iron Wolf · Rock desde Madrid · Gira 2027</title>`.

**❌ Evita:** un `canonical` con una URL inventada, o `<meta name="keywords">` (no está en la lista).

**Cómo comprobarlo:** `sed -n '/<head>/,/<\/head>/p' index.html` contiene cada etiqueta de la lista
y la skill `seo` no señala ausencias.

## SEO-02 · Un solo `h1`

**Regla:** La página tiene un único `h1`, "Iron Wolf" (ver HT-04).

**Por qué:** `CONTENT.md` §2 ("Título principal (`h1`): Iron Wolf") y criterio 2 de `PLAN.md` §5.

**✅ Haz:** el nombre del artista como `h1` en la portada.

**❌ Evita:** convertir en `h1` el lema o la palabra decorativa del pie.

**Cómo comprobarlo:** `grep -c "<h1" index.html` devuelve `1`.

## SEO-03 · JSON-LD en un `@graph` con artista, música y conciertos

**Regla:** Un único `<script type="application/ld+json">` con `@context: "https://schema.org"` y un
`@graph` que contiene:

- **`MusicGroup`** (`@id: "#iron-wolf"`): `name`, `description` (la de `CONTENT.md` §0),
  `genre: "Rock"`, `foundingDate: "2022"`, `foundingLocation` (Vallecas, Madrid, ES), `image`,
  `album` y `track`.
- **`MusicAlbum`**: *Howl*, `albumReleaseType: "EPRelease"`, `datePublished: "2024"`, `byArtist` →
  `#iron-wolf`.
- **`MusicRecording`** × 3: *Silver Fang* (2022), *Midnight Engine* (2023) y *Rust* (2023).
- **`MusicEvent`** × 4: `name`, `startDate` (solo fecha), `eventStatus`, `eventAttendanceMode`,
  `location` (`MusicVenue` con `PostalAddress`), `performer` → `#iron-wolf`, `image` y `offers`
  (`Offer` con la URL de ejemplo).

**Por qué:** paso 7 de `plans/phase-3-html.md`, que justifica `MusicGroup` en vez de `Person` (es el
tipo recomendado para quien actúa en un evento musical y no hay nombre real). Los datos salen de
`BRIEFING.md` (discografía y gira).

**✅ Haz:** `"startDate": "2027-04-17"` para Razzmatazz.

**❌ Evita:** varios bloques JSON-LD sueltos, o un `Person` con un nombre inventado.

**Cómo comprobarlo:** validador de schema.org (https://validator.schema.org): 0 errores; prueba de
resultados enriquecidos de Google: detecta los eventos.

## SEO-04 · No se inventan datos

**Regla:** En el JSON-LD y en las `meta` solo va lo que dicen `BRIEFING.md` y `CONTENT.md`:

- Sin hora de los conciertos, sin precio y sin organizador.
- El `streetAddress` de una sala real (Razzmatazz, Moon, Kafe Antzokia) **solo** si se ha
  comprobado en la web oficial de la sala, anotando la fuente en `memory-bank/progress.md`.
- El Meseta Rock Festival es ficticio: solo `addressLocality: "Valladolid"` y
  `addressCountry: "ES"`.
- Las URL de entradas y redes son de ejemplo (`https://example.com/…`), porque no existen.

**Por qué:** `PLAN.md` §1 ("No se inventa") y §6 (salas reales; fechas, festival y telonero
inventados); paso 7 de `plans/phase-3-html.md` ("Datos que no se inventan").

**✅ Haz:** omitir `doorTime` porque la hora no se sabe.

**❌ Evita:** `"price": "25"` o una dirección "aproximada" de una sala.

**Cómo comprobarlo:** cada valor del JSON-LD se encuentra en `BRIEFING.md`, `CONTENT.md` o en una
fuente anotada en `progress.md`.
