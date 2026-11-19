---
name: product-overview
description: Qué es el ejercicio, qué se entrega, con qué restricciones, cómo se evalúa y qué decide cada documento
last_verified: 2026-11-19 (sobre el commit 2dfeb1f, cierre de la fase 1)
---

# Descripción del producto

## El ejercicio

Ejercicio del bootcamp 4Geeks (AI Engineering PT 7): **"Muestra el talento de tu amigo artista con
un website"**. Se construye la landing de un artista con **solo HTML y CSS**, cuidando la
semántica, la accesibilidad y el SEO (datos estructurados de Schema.org). El repositorio parte de
la plantilla `html-hello` de 4Geeks (`server.py`, `learn.json`, README de la plantilla y
`.vscode/`). Fuente: [`PLAN.md`](../PLAN.md) §1 y §5.

### Entregables

- `index.html` y `styles.css` en la raíz, e imágenes en `assets/`.
- `verification.md` con la comprobación de cada criterio, y un README de entrega (fase 6).

### Restricción bloqueante

**Solo HTML y CSS.** Ni JavaScript, ni frameworks, ni Tailwind (su CDN es JavaScript). Única
excepción: un `<script type="application/ld+json">` con datos de Schema.org. Regla
[HT-01](../.agents/rules/html.md).

### Los 8 criterios de evaluación (`PLAN.md` §5)

| # | Criterio | Se construye en |
|---|---|---|
| 1 | El HTML está correctamente formateado | Fase 3 |
| 2 | Las etiquetas están bien organizadas según su jerarquía | Fase 3 |
| 3 | Uso estricto de HTML semántico | Fase 3 |
| 4 | Los estilos CSS dan una presentación atractiva y moderna | Fases 4 y 5 |
| 5 | Organización correcta de archivos | Fases 0–4 |
| 6 | Apto para lectores de pantalla | Fases 3–6 |
| 7 | Datos estructurados de Schema.org | Fase 3 |
| 8 | Cumple los requisitos del artista | Fases 3–5 |

Además, en todas las fases: 0 JavaScript (salvo JSON-LD), 0 `style=""`, ningún texto que no venga
de `CONTENT.md` y ninguna aparición de "hard rock" (siempre "rock").

## El artista: Iron Wolf (ficticio)

**Iron Wolf es un artista inventado** para el ejercicio: cantante y guitarrista de rock de
Vallecas (Madrid), 25 años, en activo desde 2022. Las **salas** de la gira son **reales**
(Razzmatazz, Moon, Kafe Antzokia, La Riviera); las **fechas**, el **Meseta Rock Festival** y la
banda **The Black Highway** son **inventados**. Las personas de las fotos no son él
([`assets/images/CREDITS.md`](../assets/images/CREDITS.md)). Fuente: [`BRIEFING.md`](../BRIEFING.md)
y `PLAN.md` §6.

## Para quién es la web

- **Público de Iron Wolf:** gente que busca rock en Madrid o sus conciertos, y quiere conocerle y
  ver las fechas de la gira 2027.
- **Salas, festivales y prensa:** la llamada del pie ("¿Sala, festival o prensa? Hablemos.").
- **Cualquier persona**, también con lector de pantalla o teclado (`BRIEFING.md`).
- **Quien evalúa el ejercicio** (4Geeks), con los 8 criterios de arriba.

Lo que pide el artista: una sola página; menú con **Sobre mí**, **Trayectoria** y **Próximas
presentaciones**; una buena portada; cada sección de al menos el alto de la pantalla; atractiva,
accesible y fácil de encontrar en buscadores. La Galería existe pero **no** va en el menú.

## Qué decide cada documento

| Documento | Decide | Manda sobre |
|---|---|---|
| [`CONTENT.md`](../CONTENT.md) | Todos los textos, `alt`, `aria-label` y créditos | Todo lo textual |
| [`DESIGN.md`](../DESIGN.md) | Todo lo visual | La maqueta |
| [`BRIEFING.md`](../BRIEFING.md) | Quién es el artista y qué pide | — |
| [`design/`](../design/) | Maqueta aprobada: solo referencia para valores exactos | — |
| [`PLAN.md`](../PLAN.md) y [`plans/`](../plans/) | Fases, ramas, pasos y criterios de aceptación | — |
| [`.agents/rules/`](../.agents/rules/) | Cómo se trabaja (reglas con ID) | — |

Si algo no está en ningún documento, **se pregunta a Mateo** (regla UR-02).
