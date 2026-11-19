# PLAN — Landing de Iron Wolf

> Plan de implementación de la web de Iron Wolf (ejercicio 4Geeks "Muestra el talento de tu amigo
> artista con un website").
>
> Estado del plan: **APROBADO** por Mateo el 19-11-2026.

---

## 1. Qué hay que construir

Una landing de una sola página para Iron Wolf, un artista de rock ficticio, **solo con HTML y
CSS**. Las fuentes de verdad, por orden de prioridad:

| Documento | Qué decide |
|---|---|
| `BRIEFING.md` | Quién es el artista y qué pide para su web |
| `CONTENT.md` | Todos los textos, los `alt` y los créditos, tal cual |
| `DESIGN.md` | Todo lo visual: colores, tipografía, componentes, animaciones, móvil |
| `design/` | Maqueta aprobada: referencia para copiar valores exactos (manda `DESIGN.md`) |
| `assets/` | Fotos originales, créditos y texturas SVG |

Si algo no está en estos documentos, **se pregunta a Mateo**. No se inventa.

---

## 2. Cómo arrancar una sesión nueva

1. Lee este `PLAN.md` entero y mira la tabla de fases (§4) para saber cuál toca.
2. Si la fase 1 ya está fusionada, lee `AGENTS.md` y sigue lo que indica (reglas, skills y memory
   bank). Si no, lee `BRIEFING.md`, `CONTENT.md` y `DESIGN.md`.
3. Abre el archivo de la fase que toca (`plans/phase-N-*.md`) y sigue sus pasos.
4. **No empieces una fase hasta que la anterior esté fusionada en `main`.** Compruébalo con
   `git log origin/main` y `gh pr list --state merged`.

---

## 3. Forma de trabajo

- **Repositorio:** `4GeeksAcademy/aie-pt-7-web-artist-mateore1330-commits` (público). El remoto
  ya está bien configurado: no se crea otro repo.
- **Ramas:** `main` y una rama de trabajo por fase, que sale de `main` actualizada. No hay
  `develop`.
- **Commits:** un commit por paso del plan, en inglés, con Conventional Commits (`feat:`, `fix:`,
  `docs:`, `chore:`, `refactor:`, `test:`). Sin coautor. `git add` con rutas explícitas.
- **PR:** al terminar la fase, un PR de la rama de trabajo a `main` con el resumen, los criterios
  de aceptación marcados y cómo se comprobó cada uno.
- **Fusión:** **la hace siempre Mateo.** El agente nunca fusiona ni hace push a `main`.
- **Aprobaciones:** antes de empezar una fase, el agente resume lo que va a hacer y espera el "sí"
  de Mateo. El silencio no es un sí.
- **Restricción bloqueante:** solo HTML y CSS. Ni JavaScript, ni frameworks, ni Tailwind (su CDN es
  JavaScript). Única excepción: un bloque `<script type="application/ld+json">` con datos de
  Schema.org, que son datos y no código.
- **Vista previa en local:** `python3 -m http.server 8000` en la raíz y abrir
  `http://localhost:8000`. El `server.py` de la plantilla también vale, pero necesita Flask.

---

## 4. Fases

| Fase | Archivo | Rama | Resultado | Estado |
|---|---|---|---|---|
| 0 | [`plans/phase-0-setup.md`](plans/phase-0-setup.md) | `chore/phase-0-setup` | `.gitignore`, hook de gitleaks, documentos y recursos versionados | **Hecha** |
| 1 | [`plans/phase-1-agent-harness.md`](plans/phase-1-agent-harness.md) | `docs/phase-1-agent-harness` | `AGENTS.md`, `CLAUDE.md`, reglas, memory bank y skills | **En revisión** |
| 2 | [`plans/phase-2-images.md`](plans/phase-2-images.md) | `feat/phase-2-images` | Fotos en WebP, imagen para redes y favicon | Pendiente |
| 3 | [`plans/phase-3-html.md`](plans/phase-3-html.md) | `feat/phase-3-html` | `index.html` semántico completo, SEO y Schema.org | Pendiente |
| 4 | [`plans/phase-4-css.md`](plans/phase-4-css.md) | `feat/phase-4-css` | `styles.css` sin animaciones, móvil y escritorio | Pendiente |
| 5 | [`plans/phase-5-animations.md`](plans/phase-5-animations.md) | `feat/phase-5-animations` | Animaciones y efectos, con versión sin movimiento | Pendiente |
| 6 | [`plans/phase-6-verification.md`](plans/phase-6-verification.md) | `chore/phase-6-verification` | Verificación completa, `verification.md` y README de entrega | Pendiente |

Cada fase pasa a **En revisión** en su propia rama, antes de pedir la revisión. Pasa a **Hecha**
en el PR de la fase siguiente, una vez fusionada. Lo que decide si una fase está terminada es la
fusión en `main`, no esta tabla.

---

## 5. Criterios globales de aceptación

Son los 8 criterios de evaluación del enunciado. Cada uno indica dónde se construye y cómo se
comprueba al final (fase 6).

| # | Criterio de evaluación | Fase | Cómo se comprueba |
|---|---|---|---|
| 1 | El HTML está correctamente formateado | 3 | Validador oficial Nu de W3C: 0 errores. Sangría de 2 espacios, uniforme |
| 2 | Las etiquetas están bien organizadas según su jerarquía | 3 | Un solo `h1`, un `h2` por sección, `h3` por debajo, sin saltos de nivel. Esquema de títulos revisado |
| 3 | Uso estricto de HTML semántico | 3 | `header`, `nav`, `main`, `section` con `aria-labelledby`, `footer`, `article`/`ol`/`ul`, `figure`/`figcaption`, `time datetime`, `dl`, `cite`, `address`. Sin `div` donde hay una etiqueta con significado |
| 4 | Los estilos CSS dan una presentación atractiva y moderna | 4 y 5 | Coincide con la maqueta aprobada en 1440px y en 375px. Mateo lo valida |
| 5 | Organización correcta de archivos | 0–4 | `index.html` y `styles.css` en la raíz, `assets/images/`, `assets/textures/`. Nada de estilos en el HTML |
| 6 | Apto para lectores de pantalla | 3–6 | `alt` correctos, `aria-label` donde hacen falta, lo decorativo con `aria-hidden`, enlace para saltar el menú, foco visible. Lighthouse Accesibilidad 100 y prueba real con VoiceOver |
| 7 | Datos estructurados de Schema.org | 3 | JSON-LD con el artista, su música y los 4 conciertos. Validador de schema.org: 0 errores. Prueba de resultados enriquecidos de Google: eventos detectados |
| 8 | Cumple los requisitos del artista | 3–5 | Una página, menú con Sobre mí, Trayectoria y Próximas presentaciones, portada de bienvenida y cada sección de al menos el alto de la pantalla |

Además, en todas las fases:

- **0 JavaScript** en el proyecto (aparte del JSON-LD).
- **0 atributos `style=""`** en el HTML.
- **Ningún texto que no venga de `CONTENT.md`.**
- **Ninguna aparición de "hard rock"**: Mateo pide decir siempre "rock".

---

## 6. Decisiones ya tomadas

- Artista ficticio. Las salas son reales y las fechas, el festival y la banda telonera, inventados
  (ver `BRIEFING.md`).
- La Galería **no** va en el menú: el encargo pide solo tres secciones.
- Git simplificado: `main` y una rama por fase, sin `develop` ni GitHub Project.
- Fotos de Unsplash con crédito, en WebP, y pasadas a blanco y negro con CSS.
- Skills `accessibility` y `seo` copiadas del proyecto del dashboard (fase 1).

## 7. Decisiones abiertas (se preguntan a Mateo cuando toque)

- **Publicación (fase 6):** si se publica en GitHub Pages, se podrán poner las URL absolutas de
  `canonical` y `og:url`/`og:image`. Si no, se dejan fuera y se explica en `verification.md`.
- **README de la plantilla (fase 6):** se propone sustituir `README.md` por uno del proyecto en
  español y quitar `README.es.md` y `README.cn.md` de la plantilla.
