---
name: css
description: Cómo se escribe styles.css — variables en :root, primero móvil, clases BEM, bloques en orden y animaciones que se apagan
scope: styles.css
---

# Reglas de CSS

Aplican a cualquier cambio en `styles.css`. Los valores (colores, tamaños, giros, sombras) salen de
[`DESIGN.md`](../../DESIGN.md); los exactos que no estén allí, de
[`design/mockup-propuesta-2.html`](../../design/mockup-propuesta-2.html) (ver UR-02).

## CS-01 · Todo el estilo en `styles.css`, con rutas relativas

**Regla:** Hay **un solo** archivo de estilos, `styles.css`, en la raíz. Las imágenes y texturas se
referencian con rutas relativas a él: `url("assets/textures/noise.svg")`,
`url("assets/images/live-1.webp")`. Nada de estilos en el HTML (ver HT-02).

**Por qué:** criterio 5 de `PLAN.md` §5 ("`index.html` y `styles.css` en la raíz… Nada de estilos
en el HTML"). `DESIGN.md` §12: las rutas `/_blob/…` de la maqueta "se cambian por las rutas
relativas de `assets/`" (tabla de equivalencias en [`design/README.md`](../../design/README.md)).

**✅ Haz:** `background-image: url("assets/images/live-1.webp");` para la foto 1 de la galería.

**❌ Evita:** copiar `url(/_blob/e089…)` de la maqueta, o crear un segundo archivo `.css`.

**Cómo comprobarlo:** `grep -n "_blob" styles.css` no devuelve nada y
`find . -name "*.css" -not -path "./.git/*"` solo lista `./styles.css`.

## CS-02 · Colores, fuentes y medidas solo como variables de `:root`

**Regla:** Declara en `:root` todas las variables de `DESIGN.md` §2 (colores, con sus nombres
exactos: `--color-ink`, `--color-accent`…), §3 (familias de fuentes) y §4 (ancho máximo,
márgenes, relleno de sección). Fuera de `:root`, los colores se usan **solo** con `var(…)`:
ningún `#…`, `rgb(…)` ni nombre de color. Las transparencias se derivan de una variable, por
ejemplo `color-mix(in srgb, var(--color-paper) 90%, transparent)`.

Si `DESIGN.md` usa un color que no está en la tabla de §2 (hoy, `#1C1C1C` de las portadas de los
singles en §6 y `#2A2A2A` del contorno de "IRON WOLF" en §8), también se declara como variable en
`:root` y se avisa en el PR.

**Por qué:** `DESIGN.md` §2: "Se definen como variables en `:root` y no se usa ningún color fuera de
esta lista". §1: "Un solo acento: el naranja óxido. Nada de otros colores". §12: "Los colores,
fuentes y medidas se toman de las variables de `:root`, no a mano".
[`plans/phase-4-css.md`](../../plans/phase-4-css.md) paso 8 lo comprueba con `grep`.

**✅ Haz:** `.btn--primary { background: var(--color-accent); color: var(--color-ink); }`

**❌ Evita:** `color: #E0692F;` en un componente, o un naranja nuevo "parecido".
**El naranja `--color-accent` nunca es texto sobre fondo claro**: ahí va `--color-accent-ink`
(`DESIGN.md` §2).

**Cómo comprobarlo:** fuera del bloque `:root`, `grep -nE "#[0-9a-fA-F]{3,8}\b|rgba?\(|hsla?\(" styles.css`
no devuelve nada.

## CS-03 · Primero móvil, con el corte en 861px

**Regla:** Los estilos base son los de **móvil** (una columna, márgenes de 20px). El escritorio se
añade en un único bloque `@media (min-width: 861px)`: rejilla de 12 columnas, columnas de las
entradas, desplazamientos decorativos y márgenes de 64px. Los tamaños de títulos se adaptan con
`clamp()` (`DESIGN.md` §3). Ninguna parte de la página se sale en horizontal.

**Por qué:** `DESIGN.md` §4 ("Punto de corte a móvil: 860px") y §9 (cambios en móvil).
`plans/phase-4-css.md` § "Organización de `styles.css`": "Primero móvil".

**✅ Haz:** `.shot--2 { margin-top: 0; }` en la base y `margin-top: 220px` dentro del bloque de
escritorio (`DESIGN.md` §8 y §9).

**❌ Evita:** `@media (max-width: 860px)` para deshacer estilos de escritorio, o varios bloques de
escritorio repartidos por el archivo.

**Cómo comprobarlo:** `grep -n "@media" styles.css` solo muestra `(min-width: 861px)` y
`prefers-reduced-motion` (`reduce`, o `no-preference` para el desplazamiento suave), y a 320, 375, 768, 1024 y 1440px `scrollWidth` es igual a
`clientWidth`.

## CS-04 · Nombres de clase tipo BEM

**Regla:** `bloque`, `bloque__elemento` y `bloque--variante`, en inglés y en kebab-case. Se
estiliza por clase, no por ID ni por anidamiento profundo de etiquetas.

**Por qué:** `PLAN.md` y [`plans/phase-1-agent-harness.md`](../../plans/phase-1-agent-harness.md)
fijan los ejemplos `.ticket`, `.ticket__stub` y `.ticket--festival`. `DESIGN.md` §6 nombra los
componentes (`.tape`, foto de la galería).

**✅ Haz:** `.ticket`, `.ticket__stub`, `.ticket__body`, `.ticket--festival`.

**❌ Evita:** `#presentaciones li div span { … }` o clases como `.naranja-grande`.

**Cómo comprobarlo:** `grep -nE "^\s*#[a-z][a-z-]*\s*[,{]" styles.css` no muestra selectores por
ID y las clases siguen el patrón `bloque(__elemento)?(--variante)?`.

## CS-05 · El archivo va por bloques comentados, en este orden

**Regla:** `styles.css` se organiza en bloques, cada uno con su comentario de cabecera:

1. Variables (`:root`)
2. Base (`box-sizing`, `body`, tipografía, enlaces, `img`, `:focus-visible`, `.skip-link`,
   `scroll-margin-top`)
3. Utilidades (`.wrap`, rejilla, `.visually-hidden`)
4. Texturas (grano, tinta gastada, bordes rasgados)
5. Componentes
6. Secciones (portada, Sobre mí, Galería, Trayectoria, Próximas presentaciones, pie)
7. Escritorio (`@media (min-width: 861px)`)
8. Animaciones (fase 5)
9. Movimiento reducido (fase 5)

**Por qué:** `plans/phase-4-css.md` § "Organización de `styles.css`" y
[`plans/phase-5-animations.md`](../../plans/phase-5-animations.md) (bloques "Animaciones" y
"Movimiento reducido", al final).

**✅ Haz:** añadir los estilos de un componente nuevo dentro del bloque 5.

**❌ Evita:** poner `@keyframes` entre los componentes o variables sueltas fuera de `:root`.

**Cómo comprobarlo:** `grep -n "^/\* " styles.css` lista las cabeceras en el orden de arriba.

## CS-06 · Sin `!important` (salvo en "Movimiento reducido")

**Regla:** No uses `!important`. La única excepción es el bloque
`@media (prefers-reduced-motion: reduce)`, que tiene que ganar a cualquier animación.

**Por qué:** `plans/phase-1-agent-harness.md` (regla de `css.md`) y `plans/phase-4-css.md` paso 8
("ningún `!important`").

**✅ Haz:** subir la especificidad con una clase de variante (`.btn--ticket`) cuando haga falta.

**❌ Evita:** `color: var(--color-paper) !important;` en un componente.

**Cómo comprobarlo:** `grep -n "!important" styles.css` solo devuelve líneas dentro del bloque de
movimiento reducido.

## CS-07 · Las animaciones nunca son imprescindibles

**Regla:**

- Las animaciones ligadas al scroll van dentro de `@supports (animation-timeline: view())`: sin
  soporte, el contenido se ve **quieto y completo**.
- Con `@media (prefers-reduced-motion: reduce)` se apagan **todas** las animaciones y transiciones,
  y `scroll-behavior: smooth` solo se aplica cuando no se ha pedido reducir el movimiento.
- La fase 4 no lleva ningún `@keyframes`, `transition` ni `animation`: llegan en la fase 5.
- Los fotogramas se copian de la maqueta, adaptando los nombres de clase.

**Por qué:** `DESIGN.md` §1 (regla 3), §7 y §12; `plans/phase-4-css.md` (objetivo: "quieta") y
`plans/phase-5-animations.md` ("si la persona pide reducir el movimiento, nada se mueve").

**✅ Haz:** el estado inicial "oculto" de una aparición al bajar se declara **dentro** del
`@supports`, para que sin soporte se vea el contenido.

**❌ Evita:** `opacity: 0` fuera del `@supports` en un bloque que solo aparece con el scroll.

**Cómo comprobarlo:** con "Reducir movimiento" activado en el sistema, nada se mueve; y en un
navegador sin `animation-timeline` todo el contenido es visible.
