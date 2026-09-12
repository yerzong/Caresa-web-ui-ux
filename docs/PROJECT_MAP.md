# Mapa del Proyecto — CARESA WEB UI 2026

Inventario real y checklist de avance. La app **Desktop ya existe** por módulos (ver `FIGMA_ANALYSIS.md`).
Objetivo por pantalla: existir en **Desktop (fuente) → Tablet (834) → Mobile (393)**, homologada y con UI/UX + prototipo.

## Leyenda
- `[ ]` pendiente · `[~]` en progreso/sandbox · `[x]` aprobado y movido a página final
- Columnas por módulo: `Homologada | Tablet | Mobile | UX ✔ | Prototipo`

> ⚠️ Cada módulo es un **board con varias pantallas**. El desglose pantalla-por-pantalla se
> completa con una pasada de `figma-auditor`/`responsive-architect` por módulo (tarea atómica).

---

## Fase 0 — Fundaciones (transversal)
| Tarea | Estado |
|---|---|
| Colección `Breakpoints` (Desktop/Tablet/Mobile) | [x] creada 2026-09-11 |
| Tokens de **color** (marca verde/lima + neutrales + semánticos) | [ ] |
| Estilos/variables de **tipografía** (Inter, escala display→small) | [ ] |
| Inventario de **componentes maestros** (`COMPONENTES`) | [ ] |
| Homologar restos **SDS** → base única | [ ] |

---

## Módulos (Desktop → responsive)

| # | Módulo | Página (ID) | Homolog. | Tablet | Mobile | UX ✔ | Prototipo |
|---|---|---|---|---|---|---|---|
| 1 | Login | `1.0 Login` (`0:1`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 2 | Inicio (MAIN) | `2.0 Inicio (MAIN)` (`4:2`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 3 | Carrito | `3 Carrito` (`13:96`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 4 | Catálogos | `4 Catálogos` (`13:100`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 5 | Consultas | `5 Consultas` (`13:104`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 6 | Corte de caja | `6 Corte de caja` (`595:70899`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 7 | Pedidos | `7 Pedidos` (`681:51807`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 8 | Chat | `8 Chat` (`681:53445`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 9 | Abonos | `9 Abonos` (`681:61345`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 10 | Recompra / Compras | `10 Recompra` (`681:61346`) | [ ] | [ ] | [ ] | [ ] | [ ] |

---

## Orden sugerido
1. **Fase 0 — fundaciones** (tokens color + tipografía) antes de responsivar en serie.
2. **Login** (más chico, valida el flujo end-to-end: homologar → responsivar → UX → prototipar).
3. **Inicio (MAIN)** (patrón sidebar + tabla → cards; define la mayoría de transforms).
4. Resto de módulos, uno por uno.

## Progreso global
- Módulos: **10** · Fundaciones: `Breakpoints` ✅, tokens color/tipografía pendientes.
- Homologados: 0 · Tablet: 0 · Mobile: 0 · UX: 0 · Prototipo: 0

> El desglose pantalla-por-pantalla dentro de cada módulo se documenta al empezar ese módulo.
