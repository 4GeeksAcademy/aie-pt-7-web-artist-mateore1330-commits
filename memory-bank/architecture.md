---
name: architecture
description: Estructura de archivos, las 6 partes de la página con su ID y fondo, los bloques de styles.css y cómo se usan texturas y fotos
last_verified: 2026-11-19 (sobre el commit 748bb32, cierre de la fase 3)
---

# Arquitectura

> Describe la estructura **prevista** por `PLAN.md` y `DESIGN.md`. A 19-11-2026 ya existen las
> imágenes, el favicon e `index.html`; `styles.css` está vacío (ver [`current-state.md`](current-state.md)).

## Estructura de archivos

```text
/
├── index.html                  ← la página (fase 3)
├── styles.css                  ← todos los estilos (fases 4 y 5)
├── assets/
│   ├── favicon.svg             ← rombo naranja sobre tinta (fase 2)
│   ├── images/
│   │   ├── hero.webp, about.webp, live-1.webp, live-2.webp, og.jpg   ← fase 2
│   │   ├── originals/          ← JPEG originales (se conservan para regenerar)
│   │   └── CREDITS.md
│   └── textures/               ← noise.svg, wear-dark.svg, wear-light.svg
├── design/                     ← maqueta aprobada (solo referencia, no se publica)
├── BRIEFING.md, CONTENT.md, DESIGN.md, PLAN.md, plans/
├── AGENTS.md, CLAUDE.md, .agents/ (rules, skills), memory-bank/
├── .githooks/pre-commit        ← gitleaks
└── server.py, learn.json, README*.md, .vscode/   ← plantilla de 4Geeks (no se tocan hasta la fase 6)
```

## La página, de arriba abajo

| Orden | Parte | ID | Fondo | Borde rasgado hacia |
|---|---|---|---|---|
| — | Enlace "Saltar al contenido" → `#contenido` | — | — | — |
| — | Cabecera (logo + `nav` con 3 enlaces), encima de la portada | — | Transparente | — |
| — | `main` | `contenido` | — | — |
| 1 | Portada | `inicio` | Foto `hero` B/N + capa naranja `multiply` 45 % + foco + degradado | Papel |
| 2 | 01 Sobre mí | `sobre-mi` | Papel (`--color-paper`) | Naranja |
| 3 | 02 Galería (no está en el menú) | `galeria` | Naranja (`--color-accent`) | Tinta |
| 4 | 03 Trayectoria (+ Discografía) | `trayectoria` | Tinta (`--color-ink`) | Papel |
| 5 | 04 Próximas presentaciones | `presentaciones` | Papel | Tinta |
| — | Pie | — | Tinta | — |
| — | Capa de grano `div.grain` | — | Fija sobre todo | — |

Las 5 secciones tienen `min-height: 100svh`. Fuentes: `DESIGN.md` §4, §5.3 y §8;
[`plans/phase-3-html.md`](../plans/phase-3-html.md).

## `styles.css` por bloques

1. Variables (`:root`) · 2. Base · 3. Utilidades · 4. Texturas · 5. Componentes · 6. Secciones ·
7. Escritorio (`@media (min-width: 861px)`) · 8. Animaciones · 9. Movimiento reducido.

Primero móvil; corte en 860/861px. Reglas [CS-03 y CS-05](../.agents/rules/css.md).

## Texturas

| Archivo | Uso |
|---|---|
| `noise.svg` | Grano: capa fija, el doble de la pantalla, `opacity: .16`, `mix-blend-mode: overlay`, `pointer-events: none`. Animada en la fase 5 |
| `wear-dark.svg` | Tinta gastada dentro de los títulos claros sobre oscuro (`h1`, Trayectoria, Discografía, `h2` del pie), con `background-clip: text` |
| `wear-light.svg` | Igual para títulos oscuros sobre claro (Sobre mí, Próximas presentaciones) y Galería |

Los bordes rasgados no son archivo: son una tira de 44px con `clip-path` (`DESIGN.md` §5.3).

## Fotos

| Foto | Cómo entra | Motivo |
|---|---|---|
| `hero.webp` | `<img>` con `fetchpriority="high"`, `object-position: center 28%` | Contenido y LCP |
| `about.webp` | `<img>` en `figure`, `loading="lazy"` | Contenido |
| `live-1.webp`, `live-2.webp` | **Fondo CSS** de un `div role="img" aria-label="…"` | Los efectos de interferencia necesitan copias (`::before`, `::after`) |
| `og.jpg` | Solo en `og:image` | Imagen al compartir: recorte 1200 × 630 de `hero`, con el guitarrista y la guitarra (≈ `center 46%`) |

Todas se pasan a blanco y negro **con CSS** (`grayscale(1)`); los archivos quedan en color.
Fuente: `DESIGN.md` §10. Ojo: en la maqueta, `.p-live1` y `.p-live2` están cruzadas
([`design/README.md`](../design/README.md)).
