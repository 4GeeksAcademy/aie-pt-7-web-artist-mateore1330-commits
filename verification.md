# Verificación final — Landing de Iron Wolf

> Informe de la fase 6 de [`PLAN.md`](PLAN.md). Comprueba, uno a uno, los 8 criterios de
> evaluación del ejercicio y las 16 comprobaciones del plan.
>
> - **Fecha:** 19-11-2026
> - **Rama:** `chore/phase-6-verification`
> - **Navegador de las pruebas automáticas:** Chrome 157, con Playwright (`playwright-core` 1.65)
> - **Capturas:** [`design/screenshots/`](design/screenshots/), por fases
>
> Las comprobaciones marcadas como **Pendiente (Mateo)** las hace Mateo a mano. Sus resultados se
> añaden a este informe antes de la entrega.

---

## 1. Los 8 criterios de evaluación

| # | Criterio | Cómo se cumple | Prueba | Resultado |
|---|---|---|---|---|
| 1 | El HTML está correctamente formateado | Sangría de 2 espacios, sin tabuladores; `<!DOCTYPE html>` y `lang="es"`; Prettier no lo reformatea (`.prettierignore`) | Validador Nu de W3C (comprobación 1) | ✅ 0 errores, 0 avisos |
| 2 | Las etiquetas están bien organizadas según su jerarquía | Un solo `h1` ("Iron Wolf"); un `h2` por sección y otro en el pie; `h3` en los 6 hitos, en "Discografía" y en las 4 ciudades; sin saltos de nivel | Esquema de títulos (fase 3) | ✅ |
| 3 | Uso estricto de HTML semántico | `header`, `nav` con `aria-label`, `main`, 5 `section` con `aria-labelledby`, `footer`; `ol`/`ul`, `figure`/`figcaption`, `time datetime`, `dl`, `cite`, `address`, `strong`, `small` | Revisión del HTML y `rx-review` (comprobación 16) | ✅ |
| 4 | Los estilos CSS dan una presentación atractiva y moderna | Diseño aprobado (`DESIGN.md`): cartel de gira gastado sobre una base minimalista, con texturas, tinta gastada, bordes rasgados y 15 animaciones | Capturas por fase; Mateo aprobó el aspecto (PR #5) y los efectos (PR #6) | ✅ |
| 5 | Organización correcta de archivos | `index.html` y `styles.css` en la raíz; `assets/images/` (WebP, `og.jpg`, originales), `assets/textures/`, `assets/favicon.svg`; ningún estilo en el HTML | `find` y `grep` (comprobación 13) | ✅ |
| 6 | Apto para lectores de pantalla | `alt` de `CONTENT.md`; `role="img"` con `aria-label` en las fotos de fondo; lo decorativo con `aria-hidden`; "Saltar al contenido"; foco visible; contraste de 4,5:1 o más; movimiento reducido; con el menú abierto, la página de detrás se oculta al lector | Comprobaciones 3, 4, 6, 7, 8 y 12 | ✅ (falta VoiceOver y Lighthouse de Mateo) |
| 7 | Datos estructurados de Schema.org | JSON-LD en `@graph`: `MusicGroup`, `MusicAlbum`, 3 `MusicRecording` y 4 `MusicEvent` con `MusicVenue` y dirección comprobada en la web oficial de cada sala | Comprobación 9 | ✅ 0 errores; 4 eventos válidos en Google |
| 8 | Cumple los requisitos del artista | Una sola página; menú con Sobre mí, Trayectoria y Próximas presentaciones; portada de bienvenida; cada sección de al menos una pantalla | Comprobación 15 | ✅ |

---

## 2. Las 16 comprobaciones

| # | Comprobación | Herramienta | Resultado |
|---|---|---|---|
| 1 | HTML válido | Validador Nu de W3C (`curl … validator.w3.org/nu/?out=json`) | ✅ 0 errores y 0 avisos |
| 2 | CSS válido | Validador CSS de W3C (jigsaw), perfil CSS3 + SVG | ✅ con salvedades: 27 errores y 42 avisos, todos justificados (§3.1). No hay ningún error real |
| 3 | Lighthouse, móvil y escritorio | Chrome DevTools | ⏳ **Pendiente (Mateo)**. Resultado: _rellenar_ |
| 4 | Auditoría de accesibilidad | Skill `accessibility` + pruebas de Playwright | ✅ Sin hallazgos abiertos. El de la revisión final (página de detrás del menú accesible) se corrigió en `770aeea` |
| 5 | Auditoría de SEO | Skill `seo` | ✅ Sin hallazgos abiertos. `canonical`, `og:url`, `robots.txt` y sitemap no aplican porque la web no se publica (§3.2) |
| 6 | Teclado | Playwright con Tab real | ✅ Los 15 elementos de escritorio en orden lógico, con contorno de 3px. "Saltar al contenido" lleva a `#contenido`. Menú de móvil: Enter abre; Tab recorre Cerrar → Sobre mí → Trayectoria → Próximas presentaciones, y con el menú abierto no cae en enlaces tapados. Ningún elemento con foco queda bajo la cabecera ni detrás del botón ↑ (`scroll-padding`) |
| 7 | Lector de pantalla | VoiceOver en Safari | ⏳ **Pendiente (Mateo)**, con la guía del PR. Resultado: _rellenar_ |
| 8 | Contraste | Script con la fórmula de WCAG (colores planos) + píxeles reales detrás del texto de la portada | ✅ 21 parejas de colores planos de 4,89:1 o más. Sobre la foto (mediana): menú ≥ 8,4:1, logo ≥ 13:1, lema ≥ 16:1, antetítulo 4,94 (375px), 5,40 (1440px) y 5,77:1 (768px) |
| 9 | Schema.org | Validador de schema.org + prueba de resultados enriquecidos de Google | ✅ 0 errores y 0 avisos; Google: "4 elementos válidos" en Eventos (PR #4). El JSON-LD no ha cambiado desde entonces |
| 10 | Responsive | Playwright | ✅ Sin scroll horizontal en 16 anchos (320–1920px); ningún título se sale de su caja; zoom al 200 % sin solapes. Capturas de página completa a 320, 375, 768, 1024 y 1440px en [`design/screenshots/fase-6/`](design/screenshots/fase-6/) |
| 11 | Navegadores | Chrome (automático); Firefox y Safari (Mateo) | ✅ Chrome. Sin animaciones de scroll (simulado: los `@supports` en falso), ningún contenido oculto a 1440 ni a 375px. ⏳ **Pendiente (Mateo):** Firefox, Safari en el Mac y Safari en el iPhone (menú y cabecera fija) |
| 12 | Movimiento reducido | Playwright (`reducedMotion: 'reduce'`) | ✅ Solo quedan `header-fill` y `to-top-in`, la excepción aprobada (§3.3); todo el contenido visible |
| 13 | Restricciones | `grep` y `find` | ✅ Un único `<script>` (`application/ld+json`); 0 `on…=`; 0 `style=""`; 0 archivos `.js`; 0 "hard rock"; ningún color fuera de `:root`; `!important` solo en el bloque 9 |
| 14 | Textos | Script que busca cada texto de `index.html` en `CONTENT.md` | ✅ Los 124 textos y todos los `alt`/`aria-label` coinciden. "EP ·" y "Single ·" son combinaciones de la tabla de la discografía |
| 15 | Requisitos del artista | Revisión | ✅ 1 página; menú con `#sobre-mi`, `#trayectoria` y `#presentaciones`; portada con `h1`; secciones de 900–1317px a 1440 × 900 y de 812–2463px a 375 × 812 |
| 16 | Revisión de código | Skill `rx-review` + gitleaks | ✅ Sin secretos. 2 hallazgos, corregidos: página de detrás del menú accesible (`770aeea`) y clase sin uso (`f22ff9c`). 1 nota que queda abierta: Google Fonts (§3.5) |

**Rendimiento:** 3 s de scroll suave dan 179 fotogramas, con una media de 16,7 ms (60 fps) y
ninguno de más de 50 ms. Las animaciones solo usan `transform`, `rotate`, `scale`, `translate`,
`opacity`, `filter`, `clip-path` y colores.

---

## 3. Salvedades y decisiones

### 3.1 Errores del validador de CSS

- **27 errores, todos iguales.** El validador no conoce las propiedades de las animaciones de
  scroll: `animation-timeline`, `animation-range`, `timeline-scope` y `view-timeline`. Son CSS
  estándar (módulo *Scroll-driven Animations*), funcionan en Chrome y en Safari actuales, y van
  siempre dentro de `@supports`: un navegador que no las conoce las ignora y la página se ve
  completa.
- **42 avisos:**
  - 30 son "las variables CSS no se comprueban".
  - 8 son prefijos `-webkit-` necesarios: `text-stroke`, `background-clip`, `text-size-adjust`
    y `tap-highlight-color`.
  - 1 marca como obsoleto `background-clip: text`, que hoy es estándar.
  - 2 son "colores iguales". Son a propósito: el borde y el fondo de "CERRAR" son naranjas, y el
    primer fotograma del fondo de la cabecera es transparente.

### 3.2 La web no se publica

Mateo decidió no publicarla en GitHub Pages: los criterios del ejercicio no lo piden y la entrega
es la URL del repositorio. Por eso:

- No hay `canonical` ni `og:url`.
- `og:image` y las `image` del JSON-LD son rutas relativas, así que la tarjeta al compartir en
  redes no mostrará la foto hasta que la web tenga una dirección pública.
- `robots.txt` y el sitemap no aplican.

Si se publicara, basta con activar Pages desde `main` y cambiar esas rutas por URL absolutas.

### 3.3 Excepción en movimiento reducido

Con "Reducir movimiento" se apagan todas las animaciones y transiciones, **salvo dos**, aprobadas
por Mateo: el fondo de la cabecera, que se oscurece al bajar, y la aparición del botón ↑. Solo
cambian el color y la opacidad, no mueven nada, y sin ellas el botón taparía el texto en móvil.

### 3.4 Menú de móvil sin JavaScript

El menú usa `:target`, la única técnica sin JavaScript que se cierra al pulsar una sección. Lo
que se pierde, aceptado por Mateo (`DESIGN.md` §6):

- El lector de pantalla oye "enlace" en vez de "botón, expandido o contraído".
- Esc no cierra el menú.
- La dirección muestra `#menu` mientras está abierto.

### 3.5 Google Fonts

Las fuentes se cargan desde Google, como fija `DESIGN.md` §3, y eso envía la IP del visitante a
Google. Para un ejercicio no es un problema. Para una web real en la UE, convendría alojarlas en
`assets/fonts/`.

### 3.6 Lo que mejoró respecto a la maqueta

Fallos de la maqueta que se corrigieron por el camino:

- Títulos que no cabían a 1440px y en móvil.
- Tildes cortadas por la textura.
- Contraste insuficiente del antetítulo sobre la foto.
- Giros borrados por las animaciones.
- El nombre en naranja liso durante la interferencia.
- Animaciones de scroll paradas por `overflow: hidden`.
- El sello saliéndose de la pantalla.

El detalle de cada uno está en [`memory-bank/progress.md`](memory-bank/progress.md).

---

## 4. Pendiente de Mateo

| Comprobación | Qué hacer | Resultado |
|---|---|---|
| 3. Lighthouse | Guía en el PR de la fase 6 | _Móvil: Rendimiento __ · Accesibilidad __ · Buenas prácticas __ · SEO ___ <br> _Escritorio: Rendimiento __ · Accesibilidad __ · Buenas prácticas __ · SEO ___ |
| 7. VoiceOver | Guía en el PR de la fase 6 | _rellenar_ |
| 11. Firefox | Abrir la web, recargar sin hacer scroll y bajar hasta el final: todo visible | _rellenar_ |
| 11. Safari (Mac) | Igual que en Firefox | _rellenar_ |
| 11. Safari (iPhone) | Menú (abrir, ir a una sección, cerrar), cabecera fija y botón ↑ | _rellenar_ |
