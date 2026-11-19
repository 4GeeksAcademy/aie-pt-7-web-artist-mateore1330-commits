# Fase 6 — Verificación final y entrega

> Rama: `chore/phase-6-verification` · PR a `main` · Depende de: fase 5 fusionada

## Objetivo

Comprobar, uno a uno, los 8 criterios de evaluación del enunciado y los criterios globales de
`PLAN.md` §5. Corregir lo que falle. Dejar el informe en `verification.md` y un README de
entrega. Al fusionar esta fase, `main` es el trabajo que Mateo presenta.

## Lee antes

- Todas las reglas de `.agents/rules/` y `PLAN.md` §5.
- Las skills `accessibility` y `seo`, y la skill `rx-review` para la revisión de código.

## Entregables

| Archivo | Contenido |
|---|---|
| `verification.md` | Informe: cada criterio, cómo se comprobó, resultado y pruebas |
| `README.md` | README del proyecto (sustituye al de la plantilla) |
| Correcciones | Las que salgan de la verificación, con commits `fix:` |

## Pasos

### Paso 1 — Rama y dos preguntas a Mateo

```bash
git checkout main && git pull
git checkout -b chore/phase-6-verification
```

Antes de seguir, preguntar a Mateo (`PLAN.md` §7):

1. **¿Publicamos en GitHub Pages?** Si sí: activar Pages desde `main` (lo hace Mateo o el agente
   con su permiso) y añadir `canonical`, `og:url` y URL absolutas en `og:image` y en el JSON-LD.
2. **¿Sustituimos los README de la plantilla?** Propuesta: `README.md` nuevo en español y borrar
   `README.es.md` y `README.cn.md`.

### Paso 2 — Batería de comprobaciones

| # | Comprobación | Herramienta | Objetivo |
|---|---|---|---|
| 1 | HTML válido | Validador Nu de W3C | 0 errores |
| 2 | CSS válido | Validador CSS de W3C (jigsaw) | 0 errores; los avisos por propiedades modernas (`animation-timeline`, `background-clip: text`) se justifican |
| 3 | Lighthouse, móvil y escritorio | Chrome DevTools | Accesibilidad 100 y SEO 100; Rendimiento y Buenas prácticas de 90 o más (o justificados) |
| 4 | Auditoría de accesibilidad | Skill `accessibility` | Sin hallazgos abiertos |
| 5 | Auditoría de SEO | Skill `seo` | Sin hallazgos abiertos |
| 6 | Teclado | Manual | Todo alcanzable con Tab, en orden, con foco visible; "Saltar al contenido" funciona |
| 7 | Lector de pantalla | VoiceOver en Safari (**lo hace Mateo**, con la guía del paso 3) | Se entiende la página entera; nada decorativo se lee |
| 8 | Contraste | Script o DevTools | Todo de 4,5:1 o más |
| 9 | Schema.org | Validador de schema.org y prueba de resultados enriquecidos de Google | 0 errores; 4 eventos detectados |
| 10 | Responsive | Playwright a 320, 375, 768, 1024 y 1440px | Sin scroll horizontal; capturas en el informe |
| 11 | Navegadores | Chrome, Firefox y Safari | Contenido completo en los tres |
| 12 | Movimiento reducido | Playwright | 0 animaciones activas |
| 13 | Restricciones | `grep` | 0 JavaScript (salvo JSON-LD), 0 `style=""`, 0 "hard rock", ningún color fuera de `:root` |
| 14 | Textos | Comparación con `CONTENT.md` | Coinciden todos |
| 15 | Requisitos del artista | Manual | Una página, menú con las 3 secciones, portada y secciones de una pantalla |
| 16 | Revisión de código | Skill `rx-review` | Sin hallazgos abiertos |

Cada fallo se corrige en su propio commit `fix: …` y se vuelve a comprobar.

### Paso 3 — Guía de VoiceOver para Mateo

Dejar en el PR una guía corta: activar VoiceOver (Cmd + F5), abrir la web en Safari, recorrer los
encabezados con el rotor (Ctrl + Opción + U) y los enlaces, y qué se debería oír en cada sección.
Mateo anota el resultado y se incluye en `verification.md`.

### Paso 4 — `verification.md`

Tabla con los 8 criterios del enunciado y las 16 comprobaciones: cómo se hizo, resultado,
fecha y pruebas (salidas, puntuaciones, capturas en `docs/screenshots/`).

Commit: `docs: add verification report`

### Paso 5 — `README.md`

En español: qué es el proyecto (y que Iron Wolf es ficticio), captura de la portada, cómo verlo
en local, estructura de archivos, decisiones de accesibilidad y SEO, créditos de las fotos y
enlace a la web publicada (si se publica).

Commit: `docs: add project readme`

### Paso 6 — Cierre y entrega

- `PLAN.md`: todas las fases en **Hecha** (esta, en **En revisión**).
- `memory-bank/progress.md` y `current-state.md` actualizados.
- Push y PR a `main`. Pararse aquí.
- Cuando Mateo fusione, la entrega en 4Geeks la hace **Mateo**, siguiendo las indicaciones de su
  instructor (normalmente, pegar la URL del repositorio en la plataforma).

## Criterios de aceptación

- [ ] Las 16 comprobaciones están hechas y registradas en `verification.md`, con sus pruebas.
- [ ] Los 8 criterios del enunciado se cumplen.
- [ ] Lighthouse: Accesibilidad 100 y SEO 100 en móvil y escritorio.
- [ ] Mateo ha hecho la prueba con VoiceOver y está anotada.
- [ ] README nuevo y decisión sobre los de la plantilla aplicada.
- [ ] Publicación resuelta (publicada, o explicado por qué no).
- [ ] PR a `main` sin fusionar.
