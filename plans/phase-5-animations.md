# Fase 5 — Animaciones y efectos

> Rama: `feat/phase-5-animations` · PR a `main` · Depende de: fase 4 fusionada

## Objetivo

Añadir todas las animaciones y efectos de `DESIGN.md` §7, **solo con CSS**: transiciones,
animaciones al cargar, animaciones continuas, efectos al pasar el ratón y animaciones ligadas al
scroll. Con una regla de oro: si la persona pide reducir el movimiento, **nada se mueve**, y si el
navegador no admite las animaciones de scroll, **todo se ve quieto y completo**.

## Lee antes

- `.agents/rules/using-rules.md`, `css.md`, `accessibility.md` y `git-and-docs.md`.
- `DESIGN.md` §6 y §7.
- Los `@keyframes` de `design/mockup-propuesta-2.html`: se copian los fotogramas tal cual (con
  los nombres de clase adaptados a los de `styles.css`).

## Entregables

| Archivo | Contenido |
|---|---|
| `styles.css` | Bloque "Animaciones" y bloque "Movimiento reducido", al final |

## Pasos

Un commit por paso.

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b feat/phase-5-animations
```

### Paso 2 — Transiciones de los componentes

Barra del menú, botones (hundirse y flecha), entradas (enderezarse y subir), redes (giro), email
(relleno) y años de la línea del tiempo (relleno al pasar el ratón).

Commit: `feat: add hover transitions`

### Paso 3 — Animaciones al cargar

Zoom de la foto de portada, subida del nombre por líneas y aparición del lema y los botones, con
los retrasos de `DESIGN.md` §7.

Commit: `feat: add hero load animations`

### Paso 4 — Animaciones continuas

Grano, foco parpadeante, temblor e interferencia del `h1`, e interferencia automática de las fotos
de la galería (la segunda desfasada 3 s).

Commit: `feat: add continuous grain, light and glitch animations`

### Paso 5 — Efectos de la galería al pasar el ratón

Flash, contraste, zoom con giro y franjas cortadas continuas en las dos copias.

Commit: `feat: add gallery hover glitch effect`

### Paso 6 — Animaciones ligadas al scroll

Todas dentro de `@supports (animation-timeline: view())`: deslizamiento de los `h2`, aparición
de bloques, hitos y entradas, relleno de los años, caída del sello, cortina y profundidad de las
fotos, y deriva de "LIVE".

Commit: `feat: add scroll-driven animations`

### Paso 7 — Movimiento reducido y desplazamiento suave

- `@media (prefers-reduced-motion: reduce)`: `animation: none !important` y
  `transition: none !important` en todo (es el único sitio con `!important`). Los elementos que
  empiezan ocultos para una animación se muestran en su estado final.
- `scroll-behavior: smooth` en `html`, solo dentro de
  `@media (prefers-reduced-motion: no-preference)`.

Commit: `feat: respect reduced motion preference`

### Paso 8 — Comprobación

Con Playwright (skill `rx-test-web`):

1. **Chrome**: grabar o capturar la portada al cargar, un scroll completo y el ratón sobre una foto
   de la galería y una entrada. Los efectos coinciden con `DESIGN.md` §7.
2. **Firefox y WebKit** (no admiten todas las animaciones de scroll): captura de la página entera
   **sin hacer scroll**. Todo el contenido es visible: nada se queda oculto u opaco esperando una
   animación.
3. **Movimiento reducido** (`reducedMotion: 'reduce'`): `document.getAnimations().length` es 0
   después de cargar y de hacer scroll, y todo el contenido es visible.
4. **Rendimiento**: grabación de rendimiento en DevTools con scroll. Sin tirones evidentes; las
   animaciones solo usan `transform`, `opacity`, `filter`, `clip-path` y colores.
5. **Sin JavaScript nuevo**: `grep` igual que en la fase 3.
6. **Mateo lo prueba** en su navegador y aprueba.

Si hay que corregir algo: commit `fix: …`.

### Paso 9 — Cierre

`PLAN.md`, `progress.md` y `current-state.md` actualizados. Push y PR a `main` (con un vídeo o
GIF de los efectos si es posible). Pararse aquí.

## Criterios de aceptación

- [ ] Las 15 animaciones de `DESIGN.md` §7 funcionan en Chrome.
- [ ] En Firefox y WebKit, sin animaciones de scroll, todo el contenido se ve completo.
- [ ] Con movimiento reducido no hay ninguna animación activa y todo es visible.
- [ ] Las animaciones de scroll están todas dentro de `@supports`.
- [ ] `!important` solo aparece en el bloque de movimiento reducido.
- [ ] 0 JavaScript.
- [ ] Mateo aprueba los efectos.
- [ ] PR a `main` sin fusionar.

## Fuera de alcance

- Efectos que no estén en `DESIGN.md` §7.
- JavaScript para cualquier efecto: si algo no se puede hacer solo con CSS, se habla con Mateo.
