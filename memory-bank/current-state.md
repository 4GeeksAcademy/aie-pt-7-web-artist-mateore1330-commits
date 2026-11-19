---
name: current-state
description: Qué hay hoy en el repositorio, qué falta y cuál es la siguiente fase
last_verified: 2026-11-19 (sobre el commit 5dd02fd, cierre de la fase 2)
---

# Estado actual

> **Actualízalo** al cerrar cada fase o cuando cambie el resultado de una comprobación (regla
> UR-04). La fecha y el commit de la cabecera indican cuándo se comprobó por última vez.

## Fases

| Fase | Estado |
|---|---|
| 0 — Preparación del repositorio | Hecha (PR #1 fusionado) |
| 1 — Archivos para el agente | Hecha (PR #2 fusionado) |
| 2 — Imágenes | En revisión (rama `feat/phase-2-images`, PR a `main` sin fusionar) |
| 3 a 6 | Pendientes |

La tabla que manda es la de [`PLAN.md`](../PLAN.md) §4; lo que decide si una fase está terminada
es la fusión en `main`.

## Qué hay (comprobado el 19-11-2026)

| Comprobación | Resultado |
|---|---|
| `.gitignore` | ✅ Ignora sistema, editor, `.env*` (salvo `.env.example`), `.learn/` y `__pycache__/` |
| Hook de gitleaks | ✅ `.githooks/pre-commit`; bloquea un token falso. Requiere `git config core.hooksPath .githooks` en cada clon |
| Documentos aprobados | ✅ `BRIEFING.md`, `CONTENT.md`, `DESIGN.md`, `PLAN.md`, `plans/` |
| Maqueta | ✅ `design/mockup-propuesta-2.html` (solo referencia) |
| Reglas, memory bank, skills, `AGENTS.md`, `CLAUDE.md` | ✅ Prueba en frío superada (ver `progress.md`, fase 1) |
| Fotos originales | ✅ 4 JPEG en `assets/images/originals/`, con `CREDITS.md` |
| Fotos WebP | ✅ `hero`, `about`, `live-1`, `live-2`, en color y dentro de su peso (medidas en `progress.md`, fase 2) |
| `og.jpg` | ✅ 1200 × 630, 147 KB |
| `favicon.svg` | ✅ 185 B, aprobado por Mateo |
| Texturas | ✅ `noise.svg`, `wear-dark.svg`, `wear-light.svg` |
| `index.html`, `styles.css` | ❌ No existen (fases 3 y 4) |

## Carencias conocidas

- No hay web todavía: ni HTML ni CSS.
- `DESIGN.md` usa `#1C1C1C` y `#2A2A2A` fuera de su tabla de colores (ver `progress.md`, fase 1).
- El `README.md` es todavía el de la plantilla y sugiere el CDN de Tailwind, que está **prohibido**
  (HT-01). Se sustituye en la fase 6 si Mateo lo aprueba (`PLAN.md` §7).
- Pendiente de decidir (fase 6): publicar o no en GitHub Pages (`canonical`, `og:url`).

## Siguiente fase

Fase 3 — Estructura HTML, SEO y Schema.org ([`plans/phase-3-html.md`](../plans/phase-3-html.md)),
cuando la fase 2 esté fusionada en `main`.
