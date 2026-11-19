---
name: current-state
description: Qué hay hoy en el repositorio, qué falta y cuál es la siguiente fase
last_verified: 2026-11-19 (sobre el commit b72a21e, cierre de la fase 6)
---

# Estado actual

> **Actualízalo** al cerrar cada fase o cuando cambie el resultado de una comprobación (regla
> UR-04). La fecha y el commit de la cabecera indican cuándo se comprobó por última vez.

## Fases

| Fase | Estado |
|---|---|
| 0 a 5 | Hechas (PR #1 a #6 fusionados) |
| 6 — Verificación final y entrega | En revisión (rama `chore/phase-6-verification`, PR a `main` sin fusionar) |

La tabla que manda es la de [`PLAN.md`](../PLAN.md) §4; lo que decide si una fase está terminada
es la fusión en `main`.

## Qué hay (comprobado el 19-11-2026)

La web está completa. El detalle de cada comprobación está en [`verification.md`](../verification.md).

| Comprobación | Resultado |
|---|---|
| HTML (W3C) | ✅ 0 errores y 0 avisos |
| CSS (W3C) | ✅ Solo errores de propiedades de scroll que el validador no conoce (justificados) |
| Schema.org | ✅ 0 errores; Google: 4 eventos válidos |
| Accesibilidad | ✅ Teclado, foco, contraste ≥ 4,5:1, `aria-hidden` en lo decorativo, menú de móvil que oculta la página de detrás, movimiento reducido |
| Responsive | ✅ Sin scroll horizontal en 16 anchos (320–1920px) |
| Restricciones | ✅ 0 JavaScript (salvo JSON-LD), 0 `style=""`, 0 "hard rock", colores solo en `:root` |
| Lighthouse | ⏳ Pendiente: lo pasa Mateo |
| VoiceOver | ⏳ Pendiente: lo prueba Mateo |
| Firefox, Safari (Mac e iPhone) | ⏳ Pendiente: los prueba Mateo |

## Carencias conocidas

- La web no está publicada (decisión de Mateo). Sin `canonical` ni `og:url`; `og:image` es
  relativa.
- Google Fonts envía la IP del visitante a Google (nota en `verification.md` §3.5).
- Menú de móvil sin JavaScript: el lector de pantalla oye "enlace" y no "botón"; Esc no lo cierra.

## Siguiente paso

Cuando Mateo añada sus resultados a `verification.md` §4 y fusione la fase 6, `main` es la entrega.
La entrega en 4Geeks la hace **Mateo**, normalmente pegando la URL del repositorio en la
plataforma.
