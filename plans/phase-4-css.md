# Fase 4 — Estilos (sin animaciones)

> Rama: `feat/phase-4-css` · PR a `main` · Depende de: fase 3 fusionada

## Objetivo

Escribir `styles.css` para que la página se vea **igual que la maqueta aprobada**, en escritorio y
en móvil, pero **quieta**: sin `@keyframes`, sin `transition` y sin animaciones ligadas al scroll.
Los estados al pasar el ratón y el foco sí se estilan (con el cambio final, sin transición). Así
se valida el diseño estático por separado de los efectos.

## Lee antes

- `.agents/rules/using-rules.md`, `css.md`, `accessibility.md` y `git-and-docs.md`.
- `DESIGN.md` entero (sobre todo §2–6, §8, §9 y §12).
- `design/mockup-propuesta-2.html` y `design/README.md` para copiar valores exactos: recortes de
  `clip-path`, sombras, giros, tamaños y la tabla de equivalencias de las imágenes.

## Entregables

| Archivo | Contenido |
|---|---|
| `styles.css` | Todos los estilos estáticos |
| `index.html` | Solo clases, si faltan. Ningún cambio de texto ni de estructura sin avisar en el PR |

## Organización de `styles.css`

Bloques en este orden, cada uno con su comentario de cabecera:

1. Variables (`:root`): colores, fuentes, medidas y rutas de texturas.
2. Base: `box-sizing`, `body`, tipografía, enlaces, `img`, `:focus-visible`, `.skip-link`,
   `scroll-margin-top`.
3. Utilidades: contenedor (`.wrap`), rejilla de 12 columnas, `.visually-hidden` si hace falta.
4. Texturas: grano (estático en esta fase), tinta gastada (`background-clip: text`) y bordes
   rasgados.
5. Componentes: botones, menú, cinta, sello, foto pegada, portada de disco, entrada de concierto,
   redes y email.
6. Secciones: portada, Sobre mí, Galería, Trayectoria, Próximas presentaciones y pie.
7. Escritorio: `@media (min-width: 861px)`.
8. (Fase 5) Animaciones y movimiento reducido.

**Primero móvil:** los estilos base son para móvil (una columna) y el bloque de escritorio añade
la rejilla de 12 columnas, las columnas de las entradas y los desplazamientos decorativos.

## Pasos

Un commit por paso.

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b feat/phase-4-css
```

### Paso 2 — Variables, base y utilidades

Todas las variables de `DESIGN.md` §2–4. Alto de sección `min-height: 100svh`. Foco visible
(contorno naranja de 3px separado 4px). Enlace para saltar al contenido.

Commit: `feat: add css tokens, base styles and layout utilities`

### Paso 3 — Texturas

Grano (`assets/textures/noise.svg`, capa fija, sin animar todavía), tinta gastada con
`wear-dark.svg` y `wear-light.svg` (la de cada título según `DESIGN.md` §5.2) y bordes rasgados
con el `clip-path` de `DESIGN.md` §5.3, del color de la sección siguiente.

Commit: `feat: add grain, worn ink and torn edge textures`

### Paso 4 — Componentes

Todos los de `DESIGN.md` §6, con sus estados `:hover` y `:focus-visible` (sin transición).

Commit: `feat: add buttons, tape, stamp, ticket and other components`

### Paso 5 — Portada y cabecera

Foto de fondo en blanco y negro con filtro, capa naranja en `multiply`, foco de luz y degradado.
Título girado y crédito vertical.

Commit: `feat: style header and hero`

### Paso 6 — Sobre mí y Galería

La Galería usa `live-1.webp` y `live-2.webp` como fondo de `.shot-img`, con las copias
(`::before` y `::after`) preparadas pero ocultas (`opacity: 0`).

Commit: `feat: style about and gallery sections`

### Paso 7 — Trayectoria, Próximas presentaciones y pie

Commit: `feat: style timeline, tickets and footer`

### Paso 8 — Comprobación visual y técnica

1. **Capturas** con Playwright (skill `rx-test-web`) a 375, 768 y 1440px de ancho, de la página
   entera, comparadas con la maqueta (`design/mockup-propuesta-2.html` en el lienzo). Las
   diferencias se corrigen o se justifican.
2. **Sin scroll horizontal** a 320, 375, 768, 1024 y 1440px (`scrollWidth` igual a
   `clientWidth`).
3. **Alto de sección**: cada `section` mide al menos el alto de la ventana a 1440 × 900 y a
   375 × 812.
4. **Contraste**: calcular con un script (o con DevTools) cada combinación de texto y fondo
   usada. Todas de 4,5:1 o más (de 3:1 o más en texto de 24px o más).
5. **Con `grep`**: ningún color (`#…`, `rgb(`) fuera del bloque `:root`, ningún `!important` y
   ningún `@keyframes`, `transition` ni `animation`.
6. **Zoom al 200 %**: el texto no se corta ni se solapa.
7. **Mateo revisa** las capturas en el PR y aprueba el aspecto.

Si hay que corregir algo: commit `fix: …`.

### Paso 9 — Cierre

`PLAN.md`, `progress.md` (capturas y resultados) y `current-state.md` actualizados. Push y PR a
`main` con las capturas. Pararse aquí.

## Criterios de aceptación

- [ ] A 1440px se ve como la maqueta aprobada (Mateo lo confirma con las capturas).
- [ ] A 375px se ve según `DESIGN.md` §9: una columna, entradas apiladas, sin muescas.
- [ ] Sin scroll horizontal en ninguno de los 5 anchos.
- [ ] Cada sección mide al menos el alto de la pantalla.
- [ ] Todo el texto cumple el contraste mínimo (tabla en el PR).
- [ ] Foco visible en todos los enlaces y botones.
- [ ] Ningún color fuera de `:root`, ningún `!important`, ninguna animación ni transición.
- [ ] `index.html` sigue sin `style=""` y sin cambios de texto.
- [ ] PR a `main` sin fusionar.

## Fuera de alcance

- Animaciones, transiciones y efectos de la galería (fase 5).
- Cambiar el diseño: si algo de `DESIGN.md` no funciona, se pregunta a Mateo antes de cambiarlo.
