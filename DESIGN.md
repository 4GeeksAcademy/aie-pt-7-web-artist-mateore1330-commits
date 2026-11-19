# DESIGN — Sistema visual de la web de Iron Wolf

> Diseño **aprobado** por Mateo el 19-11-2026: "propuesta 2 (más rock)".
> Maqueta de referencia (privada): https://claude.ai/artifact/K6wbiVyecCu598LWjFbagA → mesa
> "Landing — propuesta 2 (más rock)".
>
> Este documento manda sobre la maqueta: si algo no coincide, vale lo que diga aquí. Los textos
> están en `CONTENT.md`, el artista en `BRIEFING.md`.
>
> Restricción: **solo HTML y CSS**. Todo lo que se describe aquí (texturas, animaciones, efectos)
> se hace con CSS y archivos SVG estáticos, sin JavaScript.

---

## 1. Concepto

**Un cartel de gira gastado sobre una base minimalista.** La estructura es limpia y editorial:
mucho espacio, una rejilla de 12 columnas, títulos enormes y un solo color de acento. Encima va la
suciedad del rock: grano de película, tinta gastada, bordes de papel rasgado, cinta adhesiva,
sellos y entradas de concierto. Las fotos van en blanco y negro con mucho contraste.

Tres reglas para no perder el equilibrio:

1. **Un solo acento**: el naranja óxido. Nada de otros colores.
2. **La suciedad decora, no tapa**: los textos se leen siempre.
3. **Las animaciones son llamativas**, pero se apagan del todo si la persona pide menos movimiento
   en su sistema.

---

## 2. Colores

Se definen como variables en `:root` y no se usa ningún color fuera de esta lista.

| Variable | Valor | Uso |
|---|---|---|
| `--color-ink` | `#0E0E0E` | Fondo oscuro (portada, Trayectoria, pie), texto sobre naranja |
| `--color-ink-2` | `#161616` | Entradas de concierto oscuras |
| `--color-paper` | `#F2F0EC` | Fondo claro (Sobre mí, Próximas presentaciones), texto sobre oscuro |
| `--color-white` | `#FFFFFF` | Solo el marco de la foto pegada de Sobre mí |
| `--color-accent` | `#E0692F` | Naranja óxido: acento, fondo de la Galería, entrada del festival |
| `--color-accent-ink` | `#A04A20` | Naranja oscurecido para texto pequeño sobre fondo claro |
| `--color-text-dark` | `#111111` | Texto principal sobre fondo claro |
| `--color-muted-dark` | `#3D3B38` | Texto secundario sobre fondo claro |
| `--color-label-dark` | `#55534F` | Etiquetas pequeñas sobre fondo claro |
| `--color-muted-light` | `#BDBAB4` | Texto secundario sobre fondo oscuro |
| `--color-label-light` | `#8C8983` | Etiquetas pequeñas y copyright sobre fondo oscuro |
| `--color-line-dark` | `#2E2E2E` | Líneas y bordes sobre fondo oscuro |
| `--color-line-mid` | `#3A3A3A` | Bordes de botones de redes, portadas de singles |
| `--color-cover` | `#1C1C1C` | Fondo de las portadas de los singles (§6) |
| `--color-outline` | `#2A2A2A` | Contorno de "IRON WOLF" gigante del pie (§8) |
| `--color-line-stub` | `#4A4A4A` | Línea discontinua del talón de las entradas oscuras (§6) |
| `--color-light` | `#FFE2BE` | Foco de luz cálida de la portada, al 42 % de opacidad (§7, §8) |

**Contraste (aproximado; se verifica con herramienta en la fase de pruebas):**
todas las combinaciones de texto superan 4,5:1. Las más justas son `--color-accent` sobre
`--color-ink` (≈ 5,7:1) y `--color-accent-ink` sobre `--color-paper` (≈ 5:1). **El naranja
`#E0692F` nunca se usa como texto sobre fondo claro**: ahí se usa `--color-accent-ink`.

---

## 3. Tipografía

Tres familias de Google Fonts, cargadas con `<link>` en el `<head>` (es CSS, no JavaScript):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Archivo+Black&family=Archivo:wght@400;500;700&family=Special+Elite&display=swap" rel="stylesheet">
```

| Familia | Papel | Dónde |
|---|---|---|
| **Archivo Black** | Títulos: ancha y pesada | `h1`, `h2`, ciudades, años, fechas, logo |
| **Archivo** (400, 500, 700) | Texto | Párrafos, botones, menú |
| **Special Elite** | Máquina de escribir, tono fanzine | Antetítulo, números de sección, etiquetas, cintas, créditos, copyright |

| Elemento | Tamaño | Detalles |
|---|---|---|
| `h1` "IRON WOLF" | `clamp(4.5rem, 15vw, 15rem)` | Mayúsculas, interlineado 0,82, `letter-spacing: -.03em`, girado −2° |
| `h2` de sección | `clamp(3.25rem, 8vw, 7.5rem)` | Mayúsculas, interlineado 0,88. Ajustes aprobados por Mateo en la fase 4 para que la palabra más larga quepa: en móvil, `clamp(2rem, 11vw, 3.25rem)` ("Próximas presentaciones": `clamp(1.75rem, 8.5vw, 3rem)`); en escritorio, "Trayectoria" `clamp(3.25rem, calc(8.6vw - 16px), 6.7rem)` y "Próximas presentaciones" `clamp(2.5rem, calc(6.7vw - 12px), 5.25rem)` |
| `h2` del pie | `clamp(2.5rem, 6vw, 5.75rem)` | Mayúsculas |
| Ciudad en la entrada (`h3`) | 44px | Archivo Black, mayúsculas. Escala por debajo de ~1100px para que "VALLADOLID" quepa (fase 4): `clamp(1.75rem, calc(14vw - 14px), 2.75rem)` en móvil y `clamp(1.75rem, calc(14vw - 92px), 2.75rem)` en escritorio |
| Año de la línea del tiempo | 56px | Solo contorno (ver §6) |
| Día en el talón de la entrada | 68px | Archivo Black |
| Lema de la portada | `clamp(1.4rem, 2.4vw, 2.1rem)` | Archivo 700 |
| Párrafos de Sobre mí | 20px | Interlineado 1,6 |
| Texto de los hitos | 15px | Interlineado 1,55 |
| Menú y botones | 14–15px | Archivo 700, mayúsculas, `letter-spacing: .12–.18em` |
| Etiquetas Special Elite | 13–18px | Mayúsculas en antetítulos y etiquetas |

---

## 4. Rejilla y medidas

- **Ancho máximo del contenido:** 1440px, centrado.
- **Márgenes laterales:** 64px en escritorio; 20px en móvil.
- **Rejilla:** 12 columnas (`repeat(12, minmax(0, 1fr))`), con huecos de 24–48px.
- **Alto de las secciones:** `min-height: 100svh` en las 5 secciones (portada, Sobre mí, Galería,
  Trayectoria, Próximas presentaciones), como pide el encargo. El contenido puede hacer la sección
  más alta, pero nunca más baja.
- **Relleno vertical de las secciones:** 112px arriba y 140px abajo (el extra de abajo deja sitio
  al borde rasgado).
- **Punto de corte a móvil:** 860px. Por debajo, todas las rejillas pasan a **una columna** y se
  quitan los desplazamientos decorativos (ver §9).
- Los enlaces del menú llevan a anclas; cada sección tiene `scroll-margin-top` para que el título
  no quede pegado arriba.

---

## 5. Texturas

Tres SVG estáticos en `assets/textures/`. Se generan con filtros SVG (`feTurbulence`): no son
fotos ni pesan casi nada (< 0,5 KB cada uno).

### 5.1 Grano de película — `noise.svg`

Capa fija sobre toda la página: `position: fixed`, el doble del tamaño de la pantalla,
`opacity: .16`, `mix-blend-mode: overlay` y `pointer-events: none`. Se anima (ver §7).

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="300" height="300" viewBox="0 0 300 300"><filter id="n" x="0" y="0" width="100%" height="100%"><feTurbulence type="fractalNoise" baseFrequency="0.85" numOctaves="3" stitchTiles="stitch"/><feColorMatrix type="saturate" values="0"/></filter><rect width="300" height="300" filter="url(#n)"/></svg>
```

### 5.2 Tinta gastada — `wear-dark.svg` y `wear-light.svg`

Arañazos sueltos del color del fondo. Se ponen **dentro de las letras** de los títulos con
`background-clip: text`: dos capas de fondo (la textura encima y el color del texto debajo) y
`color: transparent`. El texto sigue siendo texto real: se puede seleccionar y lo lee el lector de
pantalla.

- `wear-dark.svg` (arañazos `#0E0E0E`): títulos claros sobre fondo oscuro (`h1`, "Trayectoria",
  "Discografía", el `h2` del pie).
- `wear-light.svg` (arañazos `#F2F0EC`): títulos oscuros sobre fondo claro ("Sobre mí",
  "Próximas presentaciones") y "Galería" (tinta `#0E0E0E` sobre naranja).

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="500" height="500" viewBox="0 0 500 500"><filter id="g" x="0" y="0" width="100%" height="100%"><feTurbulence type="fractalNoise" baseFrequency="0.09 0.3" numOctaves="4" seed="7" stitchTiles="stitch"/><feColorMatrix type="matrix" values="0 0 0 0 0.055  0 0 0 0 0.055  0 0 0 0 0.055  0 0 0 14 -9.6"/></filter><rect width="500" height="500" filter="url(#g)"/></svg>
```

`wear-light.svg` es igual, con `seed="11"` y los tres primeros valores de color cambiados a
`0.949`, `0.941` y `0.925`.

Si el navegador no carga la textura, el título se ve en su color liso: no se rompe nada.

### 5.3 Bordes rasgados

Al final de cada sección hay una tira de 44px, del color de la **sección siguiente**, recortada con
`clip-path` en dientes irregulares. Así parece que el papel de la sección de abajo se rasga hacia
arriba. Es decorativa (`aria-hidden="true"`).

```css
clip-path: polygon(0 100%,0 55%,4% 72%,8% 34%,13% 62%,17% 40%,22% 76%,27% 30%,31% 58%,36% 44%,41% 80%,45% 38%,50% 66%,55% 26%,59% 60%,64% 42%,69% 78%,73% 36%,78% 64%,83% 32%,87% 70%,92% 44%,96% 68%,100% 40%,100% 100%);
```

Orden de los bordes: portada → papel, Sobre mí → naranja, Galería → tinta, Trayectoria → papel,
Próximas presentaciones → tinta.

---

## 6. Componentes

| Componente | Cómo es |
|---|---|
| **Cabecera** | **Fija arriba** (`position: fixed`): el logo y el menú bajan contigo al hacer scroll (pedido por Mateo en la fase 4). Logo "IRON WOLF" a la izquierda; menú a la derecha. Sobre la portada es transparente; al bajar, en los primeros 120px de scroll, aparece el fondo de tinta (§7). Si el navegador no admite las animaciones de scroll, el fondo es de tinta desde el principio. La página lleva `scroll-padding-top` con el alto de la cabecera (102px): al saltar a una sección o al moverse con el teclado, la cabecera no tapa el título ni el elemento con foco. Sin JavaScript no se puede esconder al bajar y mostrar al subir. |
| **Menú en móvil (hamburguesa)** | Por debajo de 861px, los enlaces se recogen tras un botón "MENÚ" con el icono de tres rayas (Archivo 700, mayúsculas, borde de 2px en papel, alto de 44px o más). Al abrirlo, un fondo de tinta con grano cubre **toda la pantalla**: arriba quedan el logo y, en el sitio de "MENÚ", el botón "✕ CERRAR" (mismo marco). "CERRAR" apunta a la propia cabecera (`#cabecera`), que es fija: el menú se cierra sin mover la página. Debajo, los tres enlaces con el estilo del menú (Archivo 700, 14px, mayúsculas, papel), uno por línea, de 44px o más y separados por líneas `--color-line-dark`. **Toques de naranja** (pedidos por Mateo): delante de cada enlace, su número de sección ("01 /", "03 /", "04 /") en Special Elite naranja; a la derecha, una flecha → naranja; el botón "✕ CERRAR" relleno de naranja con el texto en tinta, y abajo del todo un borde rasgado naranja (§5.3). Los números y las flechas son decorativos (`aria-hidden="true"`) y no se ven en escritorio. Mientras está abierto, la página no hace scroll. **Se cierra** con "CERRAR", que te deja donde estabas, o al pulsar una sección, que lleva a ella. En escritorio el menú se ve siempre en línea, sin botón. Decidido por Mateo en la fase 4. |
| **Por qué `:target`** | Sin JavaScript, es la única técnica en la que el menú se cierra solo al pulsar una sección: "MENÚ" es un enlace a `#menu` y el panel se muestra con `#menu:target`; al ir a `#trayectoria`, deja de estar apuntado y desaparece. Con `<details>`, *popover* o una casilla oculta, el panel se quedaría abierto. **Lo que se pierde:** el lector de pantalla oye "enlace" en vez de "botón, expandido o contraído"; la tecla Esc no cierra el menú; la dirección muestra `#menu` mientras está abierto, y el botón "Atrás" lo cierra. |
| **Enlace del menú** | Archivo 700, mayúsculas. Al pasar el ratón, aparece debajo una barra naranja inclinada (−20°) que crece de izquierda a derecha. |
| **Enlace "Saltar al contenido"** | Oculto fuera de la pantalla; al recibir el foco del teclado, aparece arriba a la izquierda con fondo naranja. |
| **Botón principal** | Fondo naranja, texto tinta, sombra dura de 6px en papel (sin difuminar). Al pasar el ratón, el botón "se hunde" 3px y la sombra baja a 3px. Flecha que avanza 6px. |
| **Botón fantasma** | Borde de 2px en papel, transparente; al pasar el ratón se rellena de papel. |
| **Botón de entrada** | Papel sobre las entradas oscuras (al pasar el ratón, naranja); tinta sobre la entrada naranja del festival (al pasar el ratón, papel). |
| **Todos los botones** | Alto mínimo de 52px (objetivo táctil). |
| **Foco del teclado** | Contorno naranja de 3px separado 4px en todos los enlaces y botones. Nunca se quita. |
| **Cinta** (`.tape`) | Etiqueta de cinta adhesiva: fondo papel al 90 %, texto Special Elite, bordes irregulares con `clip-path`, girada ±2°. Se usa en los pies de la Galería y en "Cabeza de cartel" (ahí en tinta con texto papel). |
| **Trozos de cinta** | Dos tiras de papel semitransparente que sujetan la foto de Sobre mí por las esquinas superiores, giradas ±37°. |
| **Foto pegada** | Marco blanco de 14px (56px abajo, donde va el pie), girada −2,5°, con sombra suave debajo. |
| **Sello "SOLD OUT"** | Borde doble naranja de 4px, texto naranja Archivo Black, girado −12°, sobre el hito de 2024, arriba a la derecha. |
| **Línea del tiempo** | 6 columnas en escritorio. Cada hito tiene una raya superior de 3px y un rombo naranja de 14px. El año va **solo con contorno** (`-webkit-text-stroke: 1.5px` en papel) y se rellena de naranja al pasar el ratón o al hacer scroll. |
| **Portada de disco** | Cuadrado de 108px con el título escrito abajo. *Howl* en naranja con sombra dura en papel; los singles en `#1C1C1C` con borde. Cada una girada entre −3° y 3°. |
| **Foto de la galería** | Marco con `overflow: hidden`; la foto va en blanco y negro (`grayscale(1) contrast(1.25)`). Lleva además dos copias de la foto para la interferencia, una capa de flash blanco y una cortina negra (ver §7). |
| **Entrada de concierto** | Tres columnas: talón con la fecha (200px), cuerpo (ciudad y recinto) y botón. El talón se separa con una línea discontinua de 2px y dos muescas circulares de 28px (arriba y abajo) del color del fondo. Las entradas están giradas ±0,5° de forma alterna. Al pasar el ratón, se enderezan, suben 6px y aparece debajo una sombra naranja. Las tres de sala son oscuras (`--color-ink-2`); la del festival es naranja con la cinta "Cabeza de cartel". |
| **Redes** | Cuadrados de 52px con borde de 2px e icono de línea de 22px. Al pasar el ratón, borde e icono naranjas, giro de −8° y escala de 1,08. |
| **Email** | Subrayado naranja de 4px que, al pasar el ratón, sube hasta rellenar todo el fondo del enlace (el texto pasa a tinta). |
| **Botón "Volver al inicio"** | Cuadrado naranja de 52px con una flecha ↑ en tinta, borde de tinta de 2px y sombra dura de papel de 4px, fijo abajo a la derecha. Lleva a la portada (`#inicio`). Para que **no tape el contenido**: en escritorio va dentro del margen lateral de 64px (a 6px del borde), y no pisa nada; en móvil no hay margen, así que solo aparece al llegar a Próximas presentaciones, la recta final de la página (a 20px del borde). En escritorio aparece al dejar atrás la portada (§7). Mientras está oculto no se puede pulsar ni alcanzar con el teclado. La página lleva `scroll-padding-bottom` de 84px para que un elemento con foco no quede detrás del botón (WCAG 2.2, 2.4.11). Si el navegador no admite las animaciones de scroll, se ve siempre. Foco: doble anillo de tinta y papel. Al pasar el ratón, fondo papel. Pedido por Mateo en la fase 4. |

---

## 7. Animaciones

Todas en CSS. Las ligadas al scroll usan `animation-timeline: view()` dentro de
`@supports (animation-timeline: view())`: si el navegador no lo admite, el contenido aparece
quieto y completo. **Con `prefers-reduced-motion: reduce` se apagan todas las animaciones y
transiciones.**

| Animación | Dónde | Disparo | Detalle |
|---|---|---|---|
| Grano | Toda la página | Siempre | La capa de grano salta de posición en 5 pasos cada 0,7 s |
| Zoom de entrada | Foto de la portada | Al cargar | Escala de 1,12 a 1 en 2,4 s |
| Foco parpadeante | Portada | Siempre | Un foco de luz cálida (degradado radial, `mix-blend-mode: screen`) parpadea de forma irregular cada 4,5 s |
| Subida del nombre | `h1` | Al cargar | Cada línea sube desde abajo, oculta por una máscara, con una ligera inclinación (1 s; "WOLF" con 0,12 s de retraso) |
| Temblor + interferencia | `h1` | Cada 5 s, desde 1,8 s | Una sacudida breve y un desdoble del texto en naranja y gris (`text-shadow`) |
| Aparición | Lema y botones | Al cargar | Suben 24px y aparecen (0,6 s, 0,8 s y 1 s de retraso) |
| Deslizamiento de títulos | Todos los `h2` | Scroll | Entran desde la izquierda, girados −3° y casi transparentes |
| Aparición al bajar | Bloques, hitos, entradas | Scroll | Suben 60px y aparecen |
| Relleno de años | Años de la línea del tiempo | Scroll | El contorno se rellena de naranja al cruzar el centro de la pantalla |
| Sello | "SOLD OUT" | Scroll | Cae desde una escala de 2,4 a 1, con un pequeño rebote |
| Cortina | Fotos de la galería | Scroll | Una cortina negra se retira hacia la derecha |
| Profundidad | Fotos de la galería | Scroll | La foto se mueve más despacio que la página (escala de 1,25 a 1 y desplazamiento vertical del 6 %) |
| Deriva | "LIVE" de fondo | Scroll | Se desplaza en horizontal |
| Interferencia automática | Fotos de la galería | Cada 6 s (la segunda, desfasada 3 s) | La copia teñida de naranja aparece cortada en franjas desplazadas durante un instante |
| Interferencia al pasar el ratón | Fotos de la galería | Ratón encima | Flash blanco, contraste al máximo, zoom de 1,06 con giro de −0,6° y franjas cortadas continuas en naranja y en negativo |
| Fondo de la cabecera | Cabecera fija | Scroll (0–120px) | El fondo pasa de transparente a tinta. Se adelantó a la fase 4 |
| Aparición del botón "Volver al inicio" | Botón ↑ | Scroll: en escritorio, al final de la portada; en móvil, al llegar a Próximas presentaciones | Pasa de oculto a visible. Se adelantó a la fase 4 |
| Desplazamiento suave | Toda la página | Al pulsar un enlace interno | `scroll-behavior: smooth`, solo si no se ha pedido reducir el movimiento. Se adelantó a la fase 4 |

---

## 8. Sección por sección

| # | Sección | Fondo | Contenido y composición |
|---|---|---|---|
| — | **Portada** | Foto `hero` a pantalla completa, en blanco y negro, con una capa naranja en `multiply` al 45 %, el foco parpadeante y un degradado oscuro hacia abajo | Abajo a la izquierda: antetítulo, "IRON / WOLF" gigante en dos líneas con tinta gastada, lema a la izquierda y botones a la derecha. Crédito de la foto en vertical en el borde derecho. |
| 01 | **Sobre mí** | Papel | Título arriba. Debajo: foto pegada (5 columnas) a la izquierda y texto (6 columnas) a la derecha, con las tres fichas separadas por una raya de 4px. "que nadie se quede quieto." en caja negra con texto papel. |
| 02 | **Galería** | Naranja | "LIVE" gigante en contorno de fondo. Dos fotos de 6 columnas: la primera vertical (4:5) y la segunda horizontal (4:3), bajada 220px. Pies en cinta y crédito al lado. |
| 03 | **Trayectoria** | Tinta | Título (8 columnas) y entradilla (4 columnas). Línea del tiempo de 6 hitos y, debajo, la discografía en 4 columnas. |
| 04 | **Próximas presentaciones** | Papel | Título (8 columnas) y entradilla (4 columnas). Cuatro entradas apiladas con 28px de separación. |
| — | **Pie** | Tinta | `h2` "¿Sala, festival o prensa? Hablemos." ("Hablemos." en naranja), email a la izquierda y redes a la derecha, copyright y, al final, "IRON WOLF" gigante en contorno `#2A2A2A` (decorativo). |

---

## 9. Móvil (por debajo de 860px)

- Todas las rejillas a una columna; márgenes laterales de 20px.
- El menú se recoge en un botón hamburguesa "MENÚ" (ver §6, "Menú en móvil").
- La segunda foto de la galería no se baja (`margin-top: 0`).
- Entradas de concierto: talón, cuerpo y botón apilados; el talón se separa con la línea
  discontinua abajo y desaparecen las muescas.
- La línea del tiempo pasa a vertical (un hito debajo de otro).
- Los títulos se adaptan solos con `clamp()`.
- Ninguna parte de la página se sale de la pantalla en horizontal.

---

## 10. Imágenes

| Archivo final | Origen | Uso | Encuadre |
|---|---|---|---|
| `assets/images/hero.webp` | Daniel Sturgess (Unsplash `eFR3GdoSSzw`) | Fondo de la portada | `object-position: center 28%` |
| `assets/images/about.webp` | Hector Bermudez (`iIWDt0fXa84`) | Foto pegada de Sobre mí (4:5) | `object-position: 40% center` |
| `assets/images/live-1.webp` | Diane Picchiottino (`kFX82FuIiXg`) | Galería, foto 1 (4:5) | Centrada |
| `assets/images/live-2.webp` | Greyson Joralemon (`nEX8iFBPPko`) | Galería, foto 2 (4:3) | Centrada |
| `assets/images/og.jpg` | Recorte de `hero` | Imagen al compartir, 1200 × 630 | — |

- **Formato WebP**, con un ancho máximo de 1600px (la portada, 1920px como mucho) y un objetivo de
  menos de 250 KB por foto.
- Las fotos se pasan a blanco y negro **con CSS** (`filter: grayscale(1)`): los archivos se quedan
  en color.
- Toda `<img>` lleva `width` y `height` reales (para que la página no salte al cargar) y su `alt`
  de `CONTENT.md`. La de la portada lleva `fetchpriority="high"`; las demás, `loading="lazy"`.
- Las fotos de la galería van como fondo CSS (los efectos necesitan copias de la imagen), así que
  su contenedor lleva `role="img"` y `aria-label` con el texto alternativo.
- **Créditos** en `assets/images/CREDITS.md` y en la propia página (ver `CONTENT.md`).

---

## 11. Accesibilidad que impone el diseño

- Todo lo decorativo lleva `aria-hidden="true"`: números de sección, "LIVE", "IRON WOLF" gigante,
  bordes rasgados, grano, trozos de cinta, sello, portadas de disco, iconos, foco y capas de las
  fotos.
- Los textos con tinta gastada (`background-clip: text`) siguen siendo texto real.
- El contraste del texto es de 4,5:1 como mínimo (§2).
- El foco del teclado siempre es visible (§6).
- Sin movimiento si la persona lo pide (§7).
- Ningún efecto depende solo del ratón para mostrar información: el ratón solo añade espectáculo.

---

## 12. De la maqueta a la web final

La maqueta usa el formato del lienzo de diseño. Al pasarla a `index.html` + `styles.css`:

- Los estilos que en la maqueta van dentro de cada etiqueta (`style="…"`) se pasan a **clases en
  `styles.css`**. En el HTML no queda ningún `style`.
- Los colores, fuentes y medidas se toman de las **variables de `:root`** (§2), no a mano.
- Las alturas de 56–58rem de la maqueta pasan a `min-height: 100svh`.
- Desaparecen los ajustes del panel de la maqueta (selector de color y el interruptor de
  animaciones). El acento queda fijo en `#E0692F` y las animaciones solo dependen de
  `prefers-reduced-motion`.
- Las rutas `/_blob/…` se cambian por las rutas relativas de `assets/`.
- `scroll-behavior: smooth` en `html`, solo cuando la persona no ha pedido reducir el movimiento.

---

## 13. Pendiente

- [ ] Las 4 fotos son de personas distintas. Para la entrega del ejercicio se usan tal cual. Si se
  quiere más coherencia, se buscan fotos de un mismo artista.
- [x] Textos nuevos de `CONTENT.md` aprobados por Mateo (19-11-2026).
