---
name: html
description: Cómo se escribe index.html — sin JavaScript, sin estilos en línea, semántico y con los textos de CONTENT.md
scope: index.html
---

# Reglas de HTML

Aplican a cualquier cambio en `index.html`. Para el `<head>` y el JSON-LD, lee también
[`seo-schema.md`](seo-schema.md); para `alt`, `aria-*` y foco, [`accessibility.md`](accessibility.md).

## HT-01 · Prohibido JavaScript (única excepción: el JSON-LD)

**Regla:** El proyecto es **solo HTML y CSS**. En `index.html` no puede haber:

- Ningún `<script>`, salvo **un único** `<script type="application/ld+json">` con los datos de
  Schema.org (son datos, no código).
- Ningún atributo de evento (`onclick=`, `onload=`, `onsubmit=`… cualquier `on*=`).
- Ninguna URL `javascript:`.
- Ningún framework ni librería, **ni el CDN de Tailwind** (`@tailwindcss/browser` es JavaScript).

Los efectos (menú, animaciones, interferencias de las fotos) se hacen con CSS. Si algo del diseño
parece necesitar JavaScript, **se pregunta a Mateo** antes de buscar una alternativa.

**Por qué:** `PLAN.md` §3 lo marca como "Restricción bloqueante" y §5 exige "0 JavaScript en el
proyecto (aparte del JSON-LD)". `DESIGN.md` (cabecera y §7) dice que todo se hace "con CSS y
archivos SVG estáticos, sin JavaScript". El `README.md` de la plantilla sugiere el CDN de Tailwind:
**no se sigue**.

**✅ Haz:** un menú que se reparte en varias líneas en móvil con CSS (`flex-wrap`), como pide
`DESIGN.md` §6.

**❌ Evita:** un `<script>` para un menú desplegable, un `onclick` en un botón o el
`<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4">` de la plantilla.

**Cómo comprobarlo:**

```bash
grep -n "<script" index.html          # solo una línea, con type="application/ld+json"
grep -nE " on[a-z]+=" index.html      # sin resultados
grep -rn "javascript:" index.html     # sin resultados
find . -name "*.js" -not -path "./.git/*"   # sin resultados
```

## HT-02 · Prohibido `style=""`: todo el estilo va en `styles.css`

**Regla:** Ningún atributo `style` ni bloque `<style>` en `index.html`. El HTML solo lleva clases;
los estilos van en `styles.css`, enlazado con `<link rel="stylesheet" href="styles.css">`.

**Por qué:** `PLAN.md` §5 exige "0 atributos `style=""` en el HTML" y el criterio 5 ("Nada de
estilos en el HTML"). `DESIGN.md` §12 dice que los `style="…"` de la maqueta se pasan a clases.

**✅ Haz:** `<p class="hero__tagline">`, con su estilo en `styles.css`.

**❌ Evita:** copiar de la maqueta un `<div style="transform: rotate(-2deg)">`.

**Cómo comprobarlo:** `grep -nE "style=|<style" index.html` no devuelve nada.

## HT-03 · Usa la etiqueta con significado, no un `div`

**Regla:** Usa la etiqueta semántica que corresponde: `header`, `nav`, `main`, `section` (con
`aria-labelledby` hacia su título), `footer`, `ol`/`ul`/`li`, `figure`/`figcaption`,
`time datetime`, `dl`/`dt`/`dd`, `cite`, `address`, `strong`, `small`. El `div` y el `span` solo
para capas decorativas o agrupaciones sin significado. Sigue la estructura de
[`plans/phase-3-html.md`](../../plans/phase-3-html.md) § "Estructura que debe tener `index.html`".

**Por qué:** es el criterio 3 de `PLAN.md` §5 ("Uso estricto de HTML semántico… Sin `div` donde
hay una etiqueta con significado"). La tabla de etiquetas por sección está en
`plans/phase-3-html.md`.

**✅ Haz:** cada hito de la Trayectoria como `<li>` de un `<ol>`, con `<time datetime="2024">`,
`<h3>` y `<p>`, y los títulos de canciones en `<cite>`.

**❌ Evita:** `<div class="timeline-item">` para un hito, o una fecha de concierto sin `<time>`.

**Cómo comprobarlo:** el validador Nu de W3C da 0 errores y la revisión contra la tabla de
`plans/phase-3-html.md` no encuentra un `div` donde corresponde otra etiqueta.

## HT-04 · Jerarquía de títulos: un `h1`, un `h2` por sección, sin saltos

**Regla:**

- Un solo `h1`: "Iron Wolf", en la portada.
- Un `h2` por sección (Sobre mí, Galería, Trayectoria, Próximas presentaciones) y otro en el pie.
- `h3` por debajo: hitos de la Trayectoria, "Discografía" y la ciudad de cada entrada.
- Nunca se salta un nivel (de `h2` a `h4`) ni se elige un título por su tamaño: el tamaño lo da el
  CSS.

**Por qué:** criterio 2 de `PLAN.md` §5. `CONTENT.md` marca qué texto es `h1`, `h2` y `h3`.

**✅ Haz:** `<h3>Discografía</h3>` dentro de la sección Trayectoria, como dice `CONTENT.md` §5.

**❌ Evita:** un segundo `h1` para "IRON WOLF" gigante del pie (es decorativo, va en
`<p aria-hidden="true">`), o un `h4` directamente bajo un `h2`.

**Cómo comprobarlo:** `grep -noE "<h[1-6]" index.html` lista los títulos en orden; hay un `h1`, y
ningún nivel aumenta en más de uno respecto al anterior.

## HT-05 · Los IDs de ancla son fijos

**Regla:** Usa exactamente estos IDs, sin cambiarlos ni traducirlos:

| ID | Elemento |
|---|---|
| `contenido` | `<main>` (destino de "Saltar al contenido") |
| `inicio` | Sección de portada |
| `sobre-mi` | Sección Sobre mí |
| `galeria` | Sección Galería |
| `trayectoria` | Sección Trayectoria |
| `presentaciones` | Sección Próximas presentaciones |

**Por qué:** `CONTENT.md` §1 y §2 fija los destinos de los enlaces (`#sobre-mi`, `#trayectoria`,
`#presentaciones`) y `plans/phase-3-html.md` la estructura con `#contenido`, `#inicio` y
`#galeria`.

**✅ Haz:** `<section id="presentaciones" aria-labelledby="presentaciones-titulo">`.

**❌ Evita:** `id="shows"` o `id="proximas-presentaciones"`: rompen los enlaces del menú.

**Cómo comprobarlo:** cada `href="#…"` de `index.html` apunta a un `id` que existe
(`grep -o 'href="#[^"]*"' index.html` frente a `grep -o 'id="[^"]*"' index.html`).

## HT-06 · Los textos se copian tal cual de `CONTENT.md`; nunca "hard rock"

**Regla:** Todo texto visible, `alt`, `aria-label`, `<title>` y `meta` sale **literal** de
[`CONTENT.md`](../../CONTENT.md). No se reescribe, no se resume y no se añade ninguno. El género
se escribe siempre **"rock"**: la expresión "hard rock" no aparece en ningún archivo de la web.

**Por qué:** `CONTENT.md` dice "se copian tal cual. Si un texto no está aquí, se pregunta".
`PLAN.md` §5: "Ningún texto que no venga de `CONTENT.md`" y "Ninguna aparición de 'hard rock':
Mateo pide decir siempre 'rock'".

**✅ Haz:** el lema exacto: "El rock no ha muerto. Aquí sigue aullando."

**❌ Evita:** "Rock duro desde Madrid", "hard rock" o un texto de relleno tipo "Bienvenido a mi
web".

**Cómo comprobarlo:** `grep -rni "hard rock" index.html styles.css` no devuelve nada, y cada texto
se encuentra con `grep -F` en `CONTENT.md`.

## HT-07 · Formato: sangría de 2 espacios y toda `<img>` con `alt`, `width` y `height`

**Regla:**

- Sangría de **2 espacios**, uniforme, sin tabuladores. Un elemento de bloque por línea.
- `<!DOCTYPE html>` y `<html lang="es">`.
- Toda `<img>` lleva `alt` (de `CONTENT.md`), `width` y `height` con las medidas reales del archivo
  (anotadas en `memory-bank/progress.md`, fase 2). La de la portada lleva `fetchpriority="high"`;
  el resto, `loading="lazy"`.
- Rutas relativas (`assets/images/hero.webp`), nunca absolutas al disco.

**Por qué:** criterio 1 de `PLAN.md` §5 ("Sangría de 2 espacios, uniforme"). `DESIGN.md` §10:
"Toda `<img>` lleva `width` y `height` reales (para que la página no salte al cargar) y su `alt`
de `CONTENT.md`".

**✅ Haz:** `<img src="assets/images/about.webp" alt="Iron Wolf con la melena al aire tocando la guitarra eléctrica" width="…" height="…" loading="lazy">`, con las medidas reales.

**❌ Evita:** una `<img>` sin `width`/`height`, o con medidas inventadas.

**Cómo comprobarlo:** `grep -nP "\t" index.html` no devuelve nada, y cada `<img>` contiene `alt=`,
`width=` y `height=` (`grep -n "<img" index.html`).
