# Fase 0 — Preparación del repositorio

> Rama: `chore/phase-0-setup` · PR a `main` · Depende de: nada

## Objetivo

Dejar el repositorio listo para trabajar con seguridad: `.gitignore` antes de cualquier commit
nuevo, el hook de gitleaks que impide subir secretos, y todo lo aprobado en la sesión de diseño
(documentos, maqueta, fotos, texturas y plan) versionado en Git. **No se escribe nada de la web.**

## Punto de partida

- `main` tiene solo el commit inicial de la plantilla `html-hello` (`server.py`, `learn.json`,
  los README de la plantilla y `.vscode/`).
- Hay archivos sin versionar, creados en la sesión de diseño: `BRIEFING.md`, `CONTENT.md`,
  `DESIGN.md`, `PLAN.md`, `plans/`, `design/` y `assets/`. También `.learn/`, que es la
  configuración local de LearnPack.
- `gitleaks` 8.30 está instalado (`/opt/homebrew/bin/gitleaks`).

## Entregables

| Archivo | Contenido |
|---|---|
| `.gitignore` | Archivos del sistema y del editor, secretos, `.learn/` y cachés de Python |
| `.githooks/pre-commit` | Hook que ejecuta gitleaks sobre lo preparado para el commit |
| Documentos | `BRIEFING.md`, `CONTENT.md`, `DESIGN.md`, `PLAN.md`, `plans/` |
| Recursos | `design/`, `assets/images/originals/`, `assets/images/CREDITS.md`, `assets/textures/` |

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b chore/phase-0-setup
```

### Paso 2 — `.gitignore`

Crear `.gitignore` con, al menos:

```gitignore
# Sistema y editor
.DS_Store
Thumbs.db
*.swp

# Secretos
.env
.env.*
!.env.example

# LearnPack (configuración local de 4Geeks)
.learn/

# Python (server.py de la plantilla)
__pycache__/
```

Git no admite comentarios al final de una línea de patrón: van siempre en su propia línea.
`.vscode/` **no** se ignora, porque ya viene versionado de la plantilla.

Commit: `chore: add gitignore`

### Paso 3 — Hook de gitleaks

1. Crear `.githooks/pre-commit`:

   ```sh
   #!/bin/sh
   # Bloquea el commit si gitleaks encuentra un posible secreto en lo preparado.
   gitleaks git --pre-commit --staged --redact --no-banner
   status=$?
   if [ $status -ne 0 ]; then
     echo "gitleaks: posible secreto detectado. Commit cancelado."
     exit $status
   fi
   ```

2. Darle permisos y activarlo:

   ```bash
   chmod +x .githooks/pre-commit
   git config core.hooksPath .githooks
   ```

3. **Probarlo**: crear un archivo temporal con un token falso con formato de GitHub (`ghp_`
   seguido de 36 caracteres alfanuméricos inventados), prepararlo con `git add` e intentar el
   commit. **Tiene que fallar.** Después: `git restore --staged <archivo>` y borrar el archivo.
   Esta prueba no se commitea.

`core.hooksPath` es configuración local: no viaja con el repositorio. Por eso, la fase 1 lo
documenta en `AGENTS.md` y la fase 6, en el README.

Commit: `chore: add gitleaks pre-commit hook`

### Paso 4 — Documentos del proyecto

```bash
git add BRIEFING.md CONTENT.md DESIGN.md
```

Commit: `docs: add artist briefing, content and design specs`

### Paso 5 — Maqueta y recursos

```bash
git add design/ assets/
```

Comprueba antes, con `git status`, que solo entran los archivos esperados (§ Entregables).

Commit: `docs: add approved mockup, original photos and textures`

### Paso 6 — Plan

```bash
git add PLAN.md plans/
```

Commit: `docs: add implementation plan`

### Paso 7 — Push y PR

```bash
git push -u origin chore/phase-0-setup
gh pr create --base main --title "chore: phase 0 – repository setup" --body "<resumen y criterios>"
```

Pararse aquí: Mateo revisa y fusiona.

## Criterios de aceptación

- [ ] El `.gitignore` existe y está en el primer commit de la rama; sus comentarios van en líneas
      propias.
- [ ] `git status` queda limpio después del paso 6, salvo `.learn/` (ignorado) y nada más.
- [ ] El hook bloquea el token falso de la prueba (pega en el PR la salida, con el token
      redactado).
- [ ] `git log --oneline main..HEAD` muestra los 5 commits de la fase, en inglés y con tipo.
- [ ] Ningún commit contiene secretos (lo garantiza el hook: ningún commit se ha saltado el hook
      con `--no-verify`).
- [ ] El PR va contra `main` y no está fusionado.

## Fuera de alcance

- Crear otro repositorio o cambiar el remoto: el actual (`4GeeksAcademy/…`) es el bueno.
- Tocar `server.py`, `learn.json`, `.vscode/` o los README de la plantilla.
