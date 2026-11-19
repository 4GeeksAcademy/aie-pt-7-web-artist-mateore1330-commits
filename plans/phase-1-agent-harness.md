# Fase 1 — Archivos para el agente

> Rama: `docs/phase-1-agent-harness` · PR a `main` · Depende de: fase 0 fusionada

## Objetivo

Que **cualquier agente, en cualquier sesión**, pueda continuar el proyecto solo con lo que hay en
el repositorio: qué se construye, con qué reglas, en qué punto está y qué está prohibido. Se sigue
la misma estructura que el proyecto del dashboard financiero
(`../aie-pt-7-dashboard-financiero-mateore1330-commits/`), adaptada a una web de HTML y CSS.

**No se escribe nada de la web.**

## Lee antes

- `PLAN.md`, `BRIEFING.md`, `CONTENT.md`, `DESIGN.md` y `design/README.md`.
- Como modelo de formato (no de contenido): en el dashboard, `AGENTS.md`,
  `.agents/rules/using-rules.md`, `.agents/rules/git-and-docs.md` y `memory-bank/*.md`.

## Entregables

| Archivo | Contenido |
|---|---|
| `AGENTS.md` | Punto de entrada para cualquier agente |
| `CLAUDE.md` | Importa `AGENTS.md` (para Claude Code) |
| `.agents/rules/*.md` | 6 archivos de reglas con ID |
| `memory-bank/*.md` | 5 archivos de contexto vivo |
| `.agents/skills/accessibility/`, `.agents/skills/seo/` | Copiadas del dashboard |

## Pasos

### Paso 1 — Rama

```bash
git checkout main && git pull
git checkout -b docs/phase-1-agent-harness
```

### Paso 2 — Reglas en `.agents/rules/`

Cada archivo lleva frontmatter (`name`, `description`, `scope`) y reglas con ID. Cada regla tiene:
**Regla**, **Por qué** (con referencia a un documento del repo), **✅ Haz**, **❌ Evita** y
**Cómo comprobarlo**, como en el dashboard.

| Archivo | Prefijo | Qué debe cubrir como mínimo |
|---|---|---|
| `using-rules.md` | UR | Qué reglas leer según el archivo que se toque (tabla). Citar los ID aplicados al terminar. Las reglas nuevas se apoyan en un documento del repo. Actualizar el memory bank al cerrar cada fase. Prioridad de las fuentes: `CONTENT.md` (textos), `DESIGN.md` (visual), `BRIEFING.md` (artista), `design/` (referencia) |
| `html.md` | HT | Solo HTML en `index.html`. **Prohibido JavaScript**: ni `<script>` (salvo el JSON-LD), ni `on*=`, ni frameworks, ni el CDN de Tailwind. Prohibido `style=""`. HTML semántico y jerarquía de títulos (un `h1`, `h2` por sección, sin saltos). IDs de ancla fijos: `contenido`, `inicio`, `sobre-mi`, `galeria`, `trayectoria`, `presentaciones`. Textos copiados tal cual de `CONTENT.md`; nunca "hard rock". Sangría de 2 espacios. Toda `<img>` con `alt`, `width` y `height` |
| `css.md` | CS | Todo el estilo en `styles.css`. Colores, fuentes y medidas solo como variables de `:root` (`DESIGN.md` §2–4); ningún color fuera de `:root`. Primero móvil: estilos base para móvil y `@media (min-width: 861px)` para escritorio. Nombres de clase tipo BEM (`.ticket`, `.ticket__stub`, `.ticket--festival`). Orden del archivo por bloques comentados (variables, base, utilidades, componentes, secciones, animaciones, movimiento reducido). Sin `!important`, salvo en el bloque de `prefers-reduced-motion`. Rutas relativas a `assets/` |
| `accessibility.md` | A11Y | `alt` según `CONTENT.md`; lo decorativo con `aria-hidden="true"` (lista en `DESIGN.md` §11); `aria-label` en los enlaces de solo icono y en los botones de entradas; cada `section` con `aria-labelledby`; enlace "Saltar al contenido"; foco visible siempre; contraste de 4,5:1 o más; objetivos táctiles de 44px o más; todo se apaga con `prefers-reduced-motion`. Usar la skill `accessibility` para auditar |
| `seo-schema.md` | SEO | Etiquetas obligatorias del `<head>` (lista de la fase 3). Un solo `h1`. JSON-LD en `@graph` con `MusicGroup`, `MusicAlbum`, `MusicRecording` y `MusicEvent`. **No inventar datos**: solo lo que dice `BRIEFING.md`/`CONTENT.md`; una dirección postal solo si se ha comprobado en la web oficial de la sala. Validar con el validador de schema.org y la prueba de resultados enriquecidos. Usar la skill `seo` para auditar |
| `git-and-docs.md` | GD | `main` y una rama por fase (`tipo/phase-N-descripcion`). Conventional Commits en inglés, un commit por paso, sin coautor. `git add` con rutas explícitas. Nunca `--no-verify`. PR a `main` con criterios marcados. **El agente no fusiona.** Activar el hook tras clonar: `git config core.hooksPath .githooks`. La documentación se escribe en español |

### Paso 3 — Memory bank en `memory-bank/`

Cada archivo lleva frontmatter (`name`, `description`, `last_verified`).

| Archivo | Contenido |
|---|---|
| `product-overview.md` | El ejercicio (enunciado resumido, entregables, restricción de solo HTML y CSS y los 8 criterios de evaluación); Iron Wolf es **ficticio**; para quién es la web; qué decide cada documento |
| `architecture.md` | Estructura de archivos; las 6 secciones con su ID, fondo y orden; estructura de `styles.css` por bloques; cómo se usan las texturas y las fotos |
| `tech-stack.md` | HTML5, CSS (variables, Grid, `clamp()`, `animation-timeline`), Google Fonts, JSON-LD; sin dependencias ni build; vista previa con `python3 -m http.server`; herramientas: `cwebp`, `gitleaks`, validador Nu de W3C, Lighthouse, validador de schema.org |
| `progress.md` | Registro por fase: qué se hizo, decisiones, problemas y cómo se verificó. Empieza con la sesión de diseño (19-11-2026) y las fases 0 y 1 |
| `current-state.md` | Qué hay hoy (tabla de comprobaciones), carencias conocidas y siguiente fase |

### Paso 4 — Skills

```bash
cp -R ../aie-pt-7-dashboard-financiero-mateore1330-commits/.agents/skills/accessibility .agents/skills/
cp -R ../aie-pt-7-dashboard-financiero-mateore1330-commits/.agents/skills/seo .agents/skills/
```

Revisa que se copian `SKILL.md` y `references/` de cada una y que conservan su licencia (MIT,
`web-quality-skills`). No se modifican.

### Paso 5 — `AGENTS.md` y `CLAUDE.md`

`AGENTS.md` (en español) debe decir, en este orden:

1. Qué es el proyecto, en dos líneas, y que **solo se usa HTML y CSS**.
2. Qué leer antes de actuar: `./.agents/rules` (empezando por `using-rules.md`),
   `./.agents/skills` y `./memory-bank`.
3. Las fuentes de verdad y su prioridad (`CONTENT.md`, `DESIGN.md`, `BRIEFING.md`, `design/`).
4. Dónde está el plan (`PLAN.md`) y cómo saber qué fase toca.
5. Lo que nunca se hace: JavaScript, inventar datos o textos, fusionar PR, `--no-verify`, escribir
   "hard rock".
6. Puesta en marcha tras clonar: `git config core.hooksPath .githooks` y la vista previa.

`CLAUDE.md`:

```markdown
@AGENTS.md
```

Commits (uno por paso): `docs: add agent rules`, `docs: add memory bank`,
`chore: add accessibility and seo agent skills`, `docs: add AGENTS.md and CLAUDE.md`.

### Paso 6 — Prueba en frío

Lanzar un subagente **sin el contexto de esta sesión**, con esta única instrucción: "Lee
`AGENTS.md` de este repositorio y lo que te indique, y responde citando archivos e ID de reglas".
Preguntas:

1. ¿Qué fase del plan toca ahora y qué archivo la describe?
2. ¿Puedo añadir un `<script>` para un menú desplegable?
3. ¿De dónde saco el texto de la sección Trayectoria?
4. Voy a cambiar el color de los botones: ¿qué reglas leo y dónde cambio el color?
5. He terminado una fase: ¿qué hago con la rama y quién fusiona?

Si alguna respuesta es incorrecta o duda, se corrige la documentación y se repite la prueba. Las
preguntas y respuestas se copian en `memory-bank/progress.md`.

### Paso 7 — Cierre

- `PLAN.md`: fase 0 en **Hecha** (si aún no lo está) y fase 1 en **En revisión**.
- `memory-bank/progress.md` y `current-state.md` actualizados.
- Push y PR a `main`. Pararse aquí.

## Criterios de aceptación

- [ ] Existen los 6 archivos de reglas, todos con frontmatter y reglas con ID, Por qué, Haz, Evita
      y Cómo comprobarlo.
- [ ] `html.md` prohíbe JavaScript de forma explícita, con la única excepción del JSON-LD.
- [ ] Existen los 5 archivos del memory bank, con `last_verified`.
- [ ] Las dos skills están copiadas completas.
- [ ] `CLAUDE.md` importa `AGENTS.md` y `AGENTS.md` cubre los 6 puntos del paso 5.
- [ ] La prueba en frío responde bien a las 5 preguntas (registrada en `progress.md`).
- [ ] Ninguna regla contradice `DESIGN.md`, `CONTENT.md` ni `PLAN.md`.
- [ ] PR a `main` sin fusionar.

## Fuera de alcance

- Escribir `index.html` o `styles.css`.
- Modificar el contenido de las skills copiadas.
