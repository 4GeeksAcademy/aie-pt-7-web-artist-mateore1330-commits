---
name: accessibility
description: Lo que hace la web apta para lector de pantalla y teclado — alt, aria, foco, contraste, objetivos táctiles y movimiento
scope: index.html, styles.css, assets/images/**
---

# Reglas de accesibilidad

El artista pide una web "que todo el mundo pueda usar, también las personas que navegan con lector
de pantalla" ([`BRIEFING.md`](../../BRIEFING.md)), y es el criterio 6 de `PLAN.md` §5. Para
auditar, usa la skill [`accessibility`](../skills/accessibility/SKILL.md).

## A11Y-01 · `alt` según `CONTENT.md`

**Regla:** Cada imagen con contenido lleva el `alt` literal de [`CONTENT.md`](../../CONTENT.md).
Las fotos de la galería van como fondo CSS, así que su contenedor lleva `role="img"` y
`aria-label` con ese mismo texto. Una imagen decorativa lleva `alt=""` (o `aria-hidden="true"` si
no es `<img>`).

**Por qué:** `CONTENT.md` §2–4 da el `alt` de cada foto; `DESIGN.md` §10 explica el `role="img"` de
la galería.

**✅ Haz:** `<div class="shot__img" role="img" aria-label="Iron Wolf en silueta tocando la guitarra bajo un foco">`.

**❌ Evita:** `alt="foto"`, `alt="hero.webp"` o un `alt` escrito por ti.

**Cómo comprobarlo:** cada `alt=` y cada `aria-label` de imagen se encuentra literal en
`CONTENT.md`.

## A11Y-02 · Lo decorativo, oculto con `aria-hidden="true"`

**Regla:** Llevan `aria-hidden="true"` todos los elementos de la lista de `DESIGN.md` §11: números
de sección ("01 /"…), "LIVE", "IRON WOLF" gigante del pie, bordes rasgados, grano, trozos de
cinta, sello "SOLD OUT", portadas de disco, iconos, foco de luz y capas de las fotos (flash,
cortina, degradados). Los iconos SVG en línea llevan además `focusable="false"`.

**Por qué:** `DESIGN.md` §11 y `CONTENT.md` (cada decorativo está marcado como "oculto al lector de
pantalla"; el sello porque "el texto ya lo dice").

**✅ Haz:** `<span class="section-num" aria-hidden="true">01 /</span>`.

**❌ Evita:** que el lector de pantalla lea "cero uno barra" antes de "Sobre mí", o "SOLD OUT" dos
veces.

**Cómo comprobarlo:** revisión con VoiceOver: no se oye ningún elemento de la lista.

## A11Y-03 · `aria-label` en los enlaces que no se entienden solos

**Regla:**

- Los cuatro botones "Entradas" llevan el `aria-label` exacto de `CONTENT.md` §6 ("Entradas para
  Barcelona, Razzmatazz, 17 de abril de 2027"…).
- Los enlaces de redes (solo icono) llevan "Iron Wolf en Instagram", "Iron Wolf en YouTube" e
  "Iron Wolf en Spotify" (`CONTENT.md` §7).
- El `nav` lleva `aria-label="Navegación principal"` (`CONTENT.md` §1).

**Por qué:** `CONTENT.md` §6: "para que no oiga 'Entradas' cuatro veces sin más".

**✅ Haz:** `<a class="btn btn--ticket" href="https://example.com/entradas/barcelona-2027-04-17" aria-label="Entradas para Barcelona, Razzmatazz, 17 de abril de 2027">Entradas</a>`.

**❌ Evita:** un enlace de icono sin nombre, o un `aria-label` distinto del de `CONTENT.md`.

**Cómo comprobarlo:** en el rotor de enlaces de VoiceOver, cada enlace tiene un nombre distinto y
comprensible.

## A11Y-04 · Cada sección tiene nombre y hay un enlace para saltar el menú

**Regla:** Cada `section` lleva `aria-labelledby` apuntando al `id` de su título. El primer
elemento del `body` es el enlace "Saltar al contenido" a `#contenido` (el `main`): oculto fuera de
la pantalla y visible al recibir el foco.

**Por qué:** `CONTENT.md` §1 (texto del enlace), `DESIGN.md` §6 (cómo se ve) y la estructura de
[`plans/phase-3-html.md`](../../plans/phase-3-html.md).

**✅ Haz:** `<section id="sobre-mi" aria-labelledby="sobre-mi-titulo">` con
`<h2 id="sobre-mi-titulo">Sobre mí</h2>`.

**❌ Evita:** ocultar el enlace de salto con `display: none` (deja de recibir el foco).

**Cómo comprobarlo:** al cargar, el primer Tab muestra "Saltar al contenido" y Enter lleva el foco
al `main`.

## A11Y-05 · El foco del teclado siempre se ve

**Regla:** Todo enlace y botón muestra con `:focus-visible` un contorno naranja de 3px separado 4px
(`outline: 3px solid var(--color-accent); outline-offset: 4px`). Nunca se quita (`outline: none`)
sin un sustituto igual de visible. El orden del Tab sigue el orden visual; no se usa `tabindex`
positivo.

**Por qué:** `DESIGN.md` §6 ("Foco del teclado… Nunca se quita") y §11.

**✅ Haz:** el estilo de foco en el bloque Base de `styles.css`, para todos los elementos.

**❌ Evita:** `a:focus { outline: none; }`.

**Cómo comprobarlo:** recorrer la página entera con Tab: el foco se ve siempre, en orden lógico.

## A11Y-06 · Contraste de 4,5:1 o más

**Regla:** Todo texto tiene un contraste de 4,5:1 o más con su fondo (3:1 en texto de 24px o más).
Se usan las combinaciones de `DESIGN.md` §2. El naranja `--color-accent` **nunca** es texto sobre
fondo claro: ahí va `--color-accent-ink`. Las texturas no pueden bajar la legibilidad.

**Por qué:** `DESIGN.md` §2 (contraste) y §1 ("La suciedad decora, no tapa: los textos se leen
siempre").

**✅ Haz:** etiquetas pequeñas naranjas sobre papel con `var(--color-accent-ink)`.

**❌ Evita:** texto `--color-accent` sobre `--color-paper`, o texto encima de una foto sin capa
oscura.

**Cómo comprobarlo:** calcular el contraste de cada pareja texto/fondo usada (script o DevTools) y
Lighthouse Accesibilidad 100.

## A11Y-07 · Objetivos táctiles de 44px o más

**Regla:** Todo enlace o botón interactivo mide al menos 44 × 44px. Los botones del diseño miden
52px de alto y los de redes 52 × 52px.

**Por qué:** `DESIGN.md` §6 ("Todos los botones: Alto mínimo de 52px (objetivo táctil)" y "Redes:
Cuadrados de 52px").

**✅ Haz:** `min-height: 52px` en `.btn`.

**❌ Evita:** enlaces del menú en móvil de 20px de alto pegados unos a otros.

**Cómo comprobarlo:** a 375px, medir en DevTools los enlaces del menú, los botones y las redes.

## A11Y-08 · Sin movimiento si se pide, y nada depende solo del ratón

**Regla:** Con `prefers-reduced-motion: reduce` no se mueve nada (ver CS-07). Ningún contenido ni
información aparece solo al pasar el ratón: el ratón solo añade espectáculo.

**Por qué:** `DESIGN.md` §7 y §11 ("Ningún efecto depende solo del ratón para mostrar
información").

**✅ Haz:** el año de la línea del tiempo se lee siempre (con contorno); el relleno naranja es un
extra.

**❌ Evita:** un texto que solo se ve en `:hover`.

**Cómo comprobarlo:** con "Reducir movimiento" activado, la página está quieta; con teclado y sin
ratón, se accede a toda la información.
