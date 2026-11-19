---
name: current-state
description: Qué hay hoy en el repositorio, qué falta y cuál es la siguiente fase
last_verified: 2026-11-19 (sobre el commit 211bfb6, cierre de la fase 5)
---

# Estado actual

> **Actualízalo** al cerrar cada fase o cuando cambie el resultado de una comprobación (regla
> UR-04). La fecha y el commit de la cabecera indican cuándo se comprobó por última vez.

## Fases

| Fase | Estado |
|---|---|
| 0 — Preparación del repositorio | Hecha (PR #1 fusionado) |
| 1 — Archivos para el agente | Hecha (PR #2 fusionado) |
| 2 — Imágenes | Hecha (PR #3 fusionado) |
| 3 — HTML, SEO y Schema.org | Hecha (PR #4 fusionado) |
| 4 — Estilos | Hecha (PR #5 fusionado) |
| 5 — Animaciones | En revisión (rama `feat/phase-5-animations`, PR a `main` sin fusionar) |
| 6 | Pendiente |

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
| `index.html` | ✅ Completo: W3C 0 errores, schema.org 0 errores, teclado correcto (ver `progress.md`, fase 3) |
| Prueba de resultados enriquecidos de Google | ✅ 4 eventos válidos, solo avisos no críticos (la pasó Mateo) |
| `styles.css` | ✅ Estilos estáticos, móvil y escritorio: sin scroll horizontal en 16 anchos, contraste ≥ 4,5:1, foco visible (ver `progress.md`, fase 4) |
| Animaciones | ✅ Las 15 de `DESIGN.md` §7, con movimiento reducido y sin JavaScript (ver `progress.md`, fase 5). Firefox y Safari: pendientes de que los pruebe Mateo |

## Carencias conocidas

- Pendiente probar en Safari (iPhone) y Firefox: menú de móvil, cabecera fija y animaciones.
- `og:image` y las `image` del JSON-LD son rutas relativas: pasan a absolutas solo si se publica (fase 6).
- El `README.md` es todavía el de la plantilla y sugiere el CDN de Tailwind, que está **prohibido**
  (HT-01). Se sustituye en la fase 6 si Mateo lo aprueba (`PLAN.md` §7).
- Pendiente de decidir (fase 6): publicar o no en GitHub Pages (`canonical`, `og:url`).

## Siguiente fase

Fase 6 — Verificación final y entrega ([`plans/phase-6-verification.md`](../plans/phase-6-verification.md)),
cuando la fase 5 esté fusionada en `main`. Empieza con dos preguntas a Mateo: publicar en GitHub
Pages y sustituir los README de la plantilla.
