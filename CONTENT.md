# CONTENT — Textos de la web de Iron Wolf

> Textos definitivos de la landing, sacados de `BRIEFING.md`. Al construir la web, se copian tal
> cual. Si un texto no está aquí, se pregunta.
>
> Estado: **APROBADO** (19-11-2026), incluidos los añadidos tras aprobar el diseño (propuesta 2).
>
> El aspecto visual de cada texto (tipografía, color, animación) está en `DESIGN.md`.

---

## 0. Datos de la página (no se ven, los leen Google y las redes)

| Campo | Texto |
|---|---|
| Título de la pestaña (`<title>`) | Iron Wolf · Rock desde Madrid · Gira 2027 |
| Descripción (`meta description`) | Iron Wolf, rock desde Vallecas. Conoce su historia, su EP *Howl* y las fechas de la gira 2027: Barcelona, Valencia, Bilbao y Meseta Rock Festival. |
| Título al compartir (Open Graph) | Iron Wolf · Gira 2027 |
| Descripción al compartir | El rock no ha muerto. Aquí sigue aullando. Barcelona, Valencia, Bilbao y Meseta Rock Festival. |
| Imagen al compartir (Open Graph) | La foto de la portada (`hero`), recortada a 1200 × 630. |

---

## 1. Cabecera y navegación

- **Enlace para saltar el menú** (solo lo ven quienes navegan con teclado o lector de pantalla):
  "Saltar al contenido"
- **Logo / nombre** (enlaza a la portada): **Iron Wolf**
- **Nombre accesible del menú:** "Navegación principal"
- **Botón del menú en móvil** (junto al icono de tres rayas, que va oculto al lector de pantalla): Menú
- **Enlaces del menú:**
  1. Sobre mí → `#sobre-mi`
  2. Trayectoria → `#trayectoria`
  3. Próximas presentaciones → `#presentaciones`

La Galería **no** va en el menú: el encargo pide solo estas tres secciones.

---

## 2. Portada (bienvenida)

- **Antetítulo:** Rock · Madrid
- **Título principal (`h1`):** Iron Wolf
- **Lema:** El rock no ha muerto. Aquí sigue aullando.
- **Botón principal:** Ver próximos conciertos → `#presentaciones`
- **Botón secundario:** Conóceme → `#sobre-mi`
- **Foto de fondo, texto alternativo (`alt`):**
  "Iron Wolf a contraluz tocando la guitarra entre el humo del escenario"
- **Crédito (texto vertical, a la derecha):**
  Foto: Daniel Sturgess / Unsplash

---

## 3. Sobre mí — sección 01

- **Número de sección (decorativo, oculto al lector de pantalla):** 01 /
- **Título (`h2`):** Sobre mí
- **Texto** (en primera persona, como si hablara él):

  > Me crié en Vallecas. Con 14 años cogí la guitarra de mi padre en un garaje del barrio y ya no
  > la solté. Aprendí a base de poner discos una y otra vez y de tocar hasta que se quejaban los
  > vecinos.
  >
  > En 2022 nació Iron Wolf. Empecé tocando en los garitos de Malasaña, noche tras noche, para quien
  > quisiera escuchar. Lo mío es el rock de siempre: los riffs directos de AC/DC, la épica de
  > Led Zeppelin y la actitud de Guns N' Roses. Canto en inglés, toco con las guitarras al frente y
  > hago estribillos para cantarlos a gritos.
  >
  > Hoy salgo al escenario con mi banda: guitarra solista, bajo y batería. Y una sola regla: que
  > nadie se quede quieto.

  "que nadie se quede quieto." va destacado (`<strong>`).

- **Datos rápidos** (fichas destacadas):
  - **Desde** 2022
  - **De** Vallecas, Madrid
  - **Suena a** AC/DC · Led Zeppelin · Guns N' Roses

- **Foto pegada con cinta:**
  - `alt`: "Iron Wolf con la melena al aire tocando la guitarra eléctrica"
  - Pie de foto, a la izquierda: Vallecas, Madrid
  - Pie de foto, a la derecha: Foto: Hector Bermudez / Unsplash

---

## 4. Galería — sección 02

- **Número de sección (decorativo):** 02 /
- **Título (`h2`):** Galería
- **Palabra decorativa de fondo (oculta al lector de pantalla):** LIVE

| # | Pie de foto (cinta) | `alt` | Crédito |
|---|---|---|---|
| 1 | 01 · En directo | Iron Wolf en silueta tocando la guitarra bajo un foco | Foto: Diane Picchiottino / Unsplash |
| 2 | 02 · Sobre las tablas | Iron Wolf de rodillas con la guitarra bajo los focos del escenario | Foto: Greyson Joralemon / Unsplash |

---

## 5. Trayectoria — sección 03

- **Número de sección (decorativo):** 03 /
- **Título (`h2`):** Trayectoria
- **Entradilla:** Del garaje a cabeza de cartel. Así ha sido el camino.

### Hitos (línea del tiempo)

| Año | Título del hito | Texto |
|---|---|---|
| 2015 | El garaje | Con 14 años empieza a tocar la guitarra de su padre en un garaje de Vallecas. |
| 2022 | Nace Iron Wolf | Primeros conciertos en los garitos de Malasaña y primer single: *Silver Fang*. |
| 2023 | Se da a conocer | Salen *Midnight Engine* y *Rust*, y forma su banda de directo. |
| 2024 | *Howl* y el primer sold out | Presenta su EP *Howl* en La Riviera (Madrid) y cuelga el cartel de entradas agotadas. |
| 2025 | Telonero de The Black Highway | Abre en Madrid el concierto de la leyenda estadounidense del rock. Esa noche le abre las puertas de los grandes escenarios. |
| 2026 | Cabeza de cartel | Se anuncia como cabeza de cartel del Meseta Rock Festival 2027. |

- **Sello sobre el hito de 2024 (decorativo, oculto al lector de pantalla, porque el texto ya lo
  dice):** SOLD OUT

### Discografía (subsección dentro de Trayectoria)

- **Subtítulo (`h3`):** Discografía

| Año | Tipo | Título |
|---|---|---|
| 2024 | EP | *Howl* |
| 2023 | Single | *Rust* |
| 2023 | Single | *Midnight Engine* |
| 2022 | Single | *Silver Fang* |

Las portadas son cuadrados de color con el título escrito; son decorativas (ocultas al lector de
pantalla), porque el título ya aparece al lado.

---

## 6. Próximas presentaciones — sección 04

- **Número de sección (decorativo):** 04 /
- **Título (`h2`):** Próximas presentaciones
- **Entradilla:** Gira 2027. Cuatro noches para subir el volumen. La última, en lo más alto del
  cartel.

### Conciertos (entradas de concierto)

| Fecha visible (talón) | Ciudad | Recinto | Etiqueta | Botón |
|---|---|---|---|---|
| 17 · Sáb · Abr 2027 | Barcelona | Razzmatazz | — | Entradas |
| 15 · Sáb · May 2027 | Valencia | Moon | — | Entradas |
| 12 · Sáb · Jun 2027 | Bilbao | Kafe Antzokia | — | Entradas |
| 10 · Sáb · Jul 2027 | Valladolid | Meseta Rock Festival | **Cabeza de cartel** | Entradas |

- **Línea pequeña de las tres entradas de sala:**
  Iron Wolf · Gira 2027 · Admite uno
- **Lo que oye un lector de pantalla en cada botón** (para que no oiga "Entradas" cuatro veces sin
  más):
  - "Entradas para Barcelona, Razzmatazz, 17 de abril de 2027"
  - "Entradas para Valencia, Moon, 15 de mayo de 2027"
  - "Entradas para Bilbao, Kafe Antzokia, 12 de junio de 2027"
  - "Entradas para Valladolid, Meseta Rock Festival, 10 de julio de 2027"
- Los botones apuntan a una URL de ejemplo, porque las entradas no existen.

---

## 7. Pie de página

- **Llamada (`h2`):** ¿Sala, festival o prensa? Hablemos.
- **Email:** booking@ironwolf.example
- **Redes** (iconos; el lector de pantalla oye el nombre):
  - "Iron Wolf en Instagram"
  - "Iron Wolf en YouTube"
  - "Iron Wolf en Spotify"
- **Copyright:** © 2026 Iron Wolf. Hecho con ruido en Madrid.
- **Palabra decorativa gigante al final (oculta al lector de pantalla):** IRON WOLF

---

## 8. Créditos de las fotos

Todas las fotos son de Unsplash, con la licencia de Unsplash (uso gratuito, también comercial; el
crédito no es obligatorio, pero lo damos). Se guardan también en `assets/images/CREDITS.md`.

| Uso | Archivo | Autor | Foto en Unsplash |
|---|---|---|---|
| Portada | `hero` | Daniel Sturgess | https://unsplash.com/photos/eFR3GdoSSzw |
| Sobre mí | `about` | Hector Bermudez | https://unsplash.com/photos/iIWDt0fXa84 |
| Galería 1 | `live-1` | Diane Picchiottino | https://unsplash.com/photos/kFX82FuIiXg |
| Galería 2 | `live-2` | Greyson Joralemon | https://unsplash.com/photos/nEX8iFBPPko |
