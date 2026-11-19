---
name: tech-stack
description: Tecnologías de la web, cómo previsualizarla y herramientas de trabajo y validación
last_verified: 2026-11-19 (sobre el commit 748bb32, cierre de la fase 3)
---

# Stack tecnológico

## La web

| Pieza | Detalle |
|---|---|
| HTML5 | Un solo `index.html`, `lang="es"`, semántico |
| CSS | Un solo `styles.css`: variables en `:root`, Grid de 12 columnas, `clamp()`, `clip-path`, `background-clip: text`, `mix-blend-mode`, `@keyframes` y `animation-timeline: view()` (dentro de `@supports`) |
| Fuentes | Google Fonts con `<link>`: Archivo Black, Archivo (400, 500, 700) y Special Elite (`DESIGN.md` §3) |
| Datos estructurados | JSON-LD de Schema.org en `<script type="application/ld+json">` |
| JavaScript | **Ninguno** (regla HT-01) |

**Sin dependencias, sin `package.json` y sin build.** Lo que hay en el repositorio es lo que se
sirve.

## Vista previa en local

```bash
python3 -m http.server 8000     # en la raíz; abrir http://localhost:8000
```

Si el puerto 8000 está ocupado (en el equipo de Mateo lo usa Docker), usa otro:
`python3 -m http.server 8080 --bind 127.0.0.1`.

El `server.py` de la plantilla también vale, pero necesita Flask (`pip3 install flask`).

## Herramientas

| Herramienta | Para qué | Dónde |
|---|---|---|
| `cwebp` 1.6.0 | Pasar las fotos a WebP (fase 2) | `/opt/homebrew/bin/cwebp` |
| `sips` | Recortar `og.jpg` (fase 2) | Incluido en macOS |
| `gitleaks` 8.30 | Hook `pre-commit` contra secretos | `/opt/homebrew/bin/gitleaks`, activado con `git config core.hooksPath .githooks` |
| `gh` | Abrir PR | `/opt/homebrew/bin/gh` |
| Validador Nu de W3C | HTML: 0 errores | https://validator.w3.org/nu/ |
| Lighthouse | Accesibilidad 100, SEO | Chrome DevTools |
| Validador de schema.org | JSON-LD: 0 errores | https://validator.schema.org |
| Prueba de resultados enriquecidos | Que detecte los eventos | https://search.google.com/test/rich-results |
| Playwright | Capturas y pruebas en el navegador (skill `rx-test-web`) | Fases 4–6 |
| VoiceOver | Prueba real con lector de pantalla | macOS |
| Python 3.14 | Servidor de vista previa | Sistema |

## Skills del agente

En [`.agents/skills/`](../.agents/skills/), copiadas del proyecto del dashboard (licencia MIT,
`web-quality-skills`): `accessibility` y `seo`.
