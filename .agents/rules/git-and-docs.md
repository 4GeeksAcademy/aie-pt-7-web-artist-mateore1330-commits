---
name: git-and-docs
description: Ramas, commits, hook de gitleaks, PR (que fusiona Mateo) e idioma de la documentación
scope: ramas, mensajes de commit, PR y archivos .md
---

# Reglas de Git y documentación

Aplican a cualquier tarea que termine en un commit, un PR o un cambio en la documentación.

## GD-01 · `main` y una rama por fase

**Regla:** Solo hay una rama permanente, `main`. Cada fase se trabaja en su rama, que sale de
`main` actualizada, con el nombre de la tabla de `PLAN.md` §4 (`tipo/phase-N-descripcion`). No se
empieza una fase hasta que la anterior está fusionada en `main`.

**Por qué:** `PLAN.md` §3 ("No hay `develop`") y §2 paso 4 ("No empieces una fase hasta que la
anterior esté fusionada en `main`"). Es una excepción acordada a la regla general de Mateo
(`main` + `develop`), para no sobredimensionar un ejercicio de una página.

**✅ Haz:** `git checkout main && git pull && git checkout -b feat/phase-3-html`.

**❌ Evita:** crear `develop`, trabajar dos fases en la misma rama o empezar la fase 3 con la 2 sin
fusionar.

**Cómo comprobarlo:** `git log --oneline origin/main` y `gh pr list --state merged` muestran
fusionada la fase anterior.

## GD-02 · Conventional Commits en inglés, un commit por paso, sin coautor

**Regla:** Mensajes en inglés, en imperativo y con tipo (`feat:`, `fix:`, `docs:`, `chore:`,
`refactor:`, `test:`), en minúsculas y sin punto final. **Un commit por paso** del plan de la fase,
con el mensaje que indica el plan. Sin líneas de coautor. `git add` con **rutas explícitas**, nunca
`git add .` ni `git add -A`.

**Por qué:** `PLAN.md` §3 ("un commit por paso del plan, en inglés… Sin coautor. `git add` con
rutas explícitas"). Cada `plans/phase-N-*.md` da el mensaje de cada paso.

**✅ Haz:** `git add index.html && git commit -m "feat: add header, navigation and hero section"`.

**❌ Evita:** `git add . && git commit -m "cambios"`, o un `Co-Authored-By:` al final.

**Cómo comprobarlo:** `git log --oneline main..HEAD` muestra un commit por paso, en inglés y con
tipo.

## GD-03 · Nunca `--no-verify`: el hook de gitleaks se respeta

**Regla:** Tras clonar el repositorio, activa el hook una vez:

```bash
git config core.hooksPath .githooks
```

Nunca uses `git commit --no-verify` (ni `-n`). Si gitleaks bloquea un commit, se revisa el
archivo; no se salta el hook. No se versionan secretos: van en `.env`, que está ignorado.

**Por qué:** la fase 0 añadió `.githooks/pre-commit`, que ejecuta gitleaks sobre lo preparado
([`plans/phase-0-setup.md`](../../plans/phase-0-setup.md) paso 3). `core.hooksPath` es
configuración local: no viaja con el clon.

**✅ Haz:** comprobar `git config core.hooksPath` (debe devolver `.githooks`) antes del primer
commit en un clon nuevo.

**❌ Evita:** `git commit --no-verify` para "desbloquear" un commit.

**Cómo comprobarlo:** cada commit muestra en su salida la línea de gitleaks `no leaks found`.

## GD-04 · PR a `main` con criterios marcados; **el agente no fusiona**

**Regla:** Al terminar la fase: push de la rama y PR a `main` con el resumen, los criterios de
aceptación del plan marcados y cómo se comprobó cada uno. **Ahí el agente se para.** La revisión y
la fusión las hace **siempre Mateo**. El agente nunca fusiona, nunca hace push a `main` y no empieza
una fase sin el "sí" de Mateo al resumen del plan (el silencio no es un sí).

**Por qué:** `PLAN.md` §3 ("Fusión: la hace siempre Mateo. El agente nunca fusiona ni hace push a
`main`" y "Aprobaciones").

**✅ Haz:** `gh pr create --base main --title "feat: phase 3 – html structure" --body-file …` y avisar
a Mateo con el enlace.

**❌ Evita:** `gh pr merge`, `git push origin main` o encadenar la fase siguiente sin aprobación.

**Cómo comprobarlo:** `gh pr view` muestra el PR abierto contra `main` y sin fusionar.

## GD-05 · La documentación se escribe en español

**Regla:** Todos los `.md` del proyecto (planes, reglas, memory bank, `verification.md`, README) y
los cuerpos de los PR van en **español**. En inglés solo los mensajes de commit y los nombres de
clase CSS. Al cerrar cada fase se actualizan `PLAN.md` §4 (estado), `memory-bank/progress.md` y
`memory-bank/current-state.md` (ver UR-04).

**Por qué:** Mateo trabaja en español (`BRIEFING.md`: "Su web es en español"); `PLAN.md` y todos
los documentos del repositorio están en español. `PLAN.md` §4 pide cambiar el estado de cada fase.

**✅ Haz:** la sección de una fase nueva de `progress.md` en español.

**❌ Evita:** escribir `verification.md` en inglés porque "es técnico".

**Cómo comprobarlo:** revisión del diff de los `.md` del PR.
