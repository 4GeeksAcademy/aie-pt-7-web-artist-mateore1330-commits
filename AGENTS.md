# AGENTS.md — Iron Wolf

## 1. Qué es este proyecto

La landing de **Iron Wolf**, un artista de rock **ficticio** de Madrid: el ejercicio de 4Geeks
"Muestra el talento de tu amigo artista con un website". Una sola página, hecha **solo con HTML y
CSS** (`index.html` y `styles.css`). Sin JavaScript.

## 2. Qué leer antes de actuar

Antes de analizar, modificar o generar nada, revisa siempre:

1. **Reglas:** [`./.agents/rules`](.agents/rules/). Empieza por
   [`using-rules.md`](.agents/rules/using-rules.md): dice qué otros archivos de reglas leer según lo
   que vayas a tocar. Al terminar, cita los ID de las reglas que has aplicado (por ejemplo, "HT-01,
   A11Y-03, GD-02").
2. **Skills:** [`./.agents/skills`](.agents/skills/): `accessibility` y `seo`, para auditar.
3. **Memory bank:** [`./memory-bank`](memory-bank/): qué es el producto, arquitectura, herramientas,
   progreso por fase y estado actual.

## 3. Fuentes de verdad, por prioridad

| Tema | Manda |
|---|---|
| Textos, `alt`, `aria-label`, créditos | [`CONTENT.md`](CONTENT.md): se copian **tal cual** |
| Todo lo visual | [`DESIGN.md`](DESIGN.md) |
| Quién es el artista y qué pide | [`BRIEFING.md`](BRIEFING.md) |
| Valores exactos (`@keyframes`, `clip-path`, sombras) | [`design/`](design/): maqueta, solo referencia; si choca con `DESIGN.md`, vale `DESIGN.md` |

Si algo no está en estos documentos, **se pregunta a Mateo**. No se inventa (regla UR-02).

## 4. El plan y qué fase toca

El plan está en [`PLAN.md`](PLAN.md) y cada fase en [`plans/`](plans/). Para saber qué fase toca:

1. Mira la tabla de fases de `PLAN.md` §4: la primera que no esté **Hecha**. Si está **En
   revisión**, su PR espera a que Mateo lo fusione: no se empieza la siguiente hasta entonces (el
   estado se cambia en la propia rama antes de pedir la revisión, así que lo que manda es la
   fusión, no la tabla).
2. Comprueba que la anterior está fusionada en `main`: `git log origin/main` y
   `gh pr list --state merged`. Si no lo está, no empieces.
3. Contrasta con [`memory-bank/current-state.md`](memory-bank/current-state.md) § "Siguiente fase".
4. Abre `plans/phase-N-*.md`, resume a Mateo lo que vas a hacer y **espera su "sí"** (el silencio no
   es un sí).

## 5. Lo que nunca se hace

- **JavaScript**, de ningún tipo: ni `<script>` (salvo el único `application/ld+json`), ni `on*=`,
  ni frameworks, ni el CDN de Tailwind (HT-01). El `README.md` de la plantilla lo sugiere: no se
  sigue.
- **Inventar** textos o datos (horas, precios, direcciones, nombres) que no estén en los documentos
  (HT-06, SEO-04).
- **Fusionar un PR** o hacer push a `main`: lo hace siempre Mateo (GD-04).
- **`git commit --no-verify`**: el hook de gitleaks no se salta (GD-03).
- Escribir **"hard rock"**: siempre "rock" (HT-06).

## 6. Puesta en marcha tras clonar

```bash
git config core.hooksPath .githooks   # activa el hook de gitleaks (no viaja con el clon)
python3 -m http.server 8000           # vista previa en http://localhost:8000
```

El `server.py` de la plantilla también sirve la web, pero necesita Flask (`pip3 install flask`).
