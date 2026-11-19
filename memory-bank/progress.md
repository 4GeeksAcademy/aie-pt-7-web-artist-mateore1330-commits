---
name: progress
description: Registro por fase — qué se hizo, decisiones, problemas y cómo se verificó
last_verified: 2026-11-19 (sobre el commit 1defd93, fase 1)
---

# Progreso

> Una sección por fase, en orden. Mantén este archivo al día al cerrar cada fase (regla UR-04).
> El plan de cada fase está en [`plans/`](../plans/).

## Sesión de diseño (19-11-2026)

**Qué se hizo:** en una sesión previa a la implementación, Mateo y el agente fijaron, en este
orden: `BRIEFING.md` → `CONTENT.md` → maqueta iterada → `DESIGN.md` → `PLAN.md` y `plans/`.

**Decisiones:**

- Artista ficticio, Iron Wolf, rock de Madrid. Salas reales; fechas, festival y telonero
  inventados.
- Diseño aprobado: "propuesta 2 (más rock)" (cartel de gira gastado sobre base minimalista).
- Mateo no quiere la expresión "hard rock" en ningún texto: siempre "rock".
- La Galería no va en el menú (el encargo pide solo tres secciones).
- Fotos de Unsplash con crédito, en WebP, pasadas a blanco y negro con CSS.
- Git simplificado: `main` + una rama por fase, sin `develop`, sin GitHub Project ni issues.
- La implementación se hace en sesiones nuevas que solo dependen de lo que hay en el repositorio.

**Verificación:** Mateo aprobó `BRIEFING.md`, `CONTENT.md`, `DESIGN.md` y `PLAN.md` el 19-11-2026.

## Fase 0 — Preparación del repositorio (PR #1, fusionado el 19-11-2026)

**Qué se hizo:** `.gitignore` (primer commit de la rama), hook `.githooks/pre-commit` con gitleaks,
y versionados los documentos, la maqueta, las fotos originales, las texturas y el plan. 5 commits
(`bd8a0d6` a `49239f1`).

**Verificación:**

- El hook bloqueó un token falso `ghp_…` preparado en un archivo temporal (`leaks found: 1`,
  salida 1); el archivo no se commiteó y se borró.
- Los 4 commits posteriores al hook pasaron gitleaks (`no leaks found`); ninguno con
  `--no-verify`.
- `git status --short --ignored` tras el último commit: solo `!! .learn/`.

**A tener en cuenta:** `core.hooksPath` es local; en un clon nuevo hay que ejecutar
`git config core.hooksPath .githooks` (regla GD-03).

## Fase 1 — Archivos para el agente (rama `docs/phase-1-agent-harness`)

**Qué se hizo:**

- 6 archivos de reglas en `.agents/rules/` (UR, HT, CS, A11Y, SEO, GD), con frontmatter y reglas con
  Regla, Por qué, Haz, Evita y Cómo comprobarlo.
- 5 archivos de memory bank en `memory-bank/`.
- Skills `accessibility` y `seo` copiadas sin cambios del proyecto del dashboard.
- `AGENTS.md` (punto de entrada) y `CLAUDE.md` (`@AGENTS.md`).

**Decisiones:**

- `DESIGN.md` usa dos colores que no están en su tabla de §2: `#1C1C1C` (portadas de los singles,
  §6) y `#2A2A2A` (contorno de "IRON WOLF" del pie, §8). La regla CS-02 manda declararlos también
  como variables de `:root` y avisar en el PR de la fase 4.
- No se copia `skills-lock.json` del dashboard (el plan no lo pide).
