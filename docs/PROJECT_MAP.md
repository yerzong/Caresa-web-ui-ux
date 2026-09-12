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
| Tokens de **color** (marca lima/verde + neutrales + semánticos) | [x] 23 tokens, colección `Color` (2026-09-11) |
| Estilos de **tipografía** (Inter, Display→Label) | [x] 9 estilos de texto (2026-09-11) |
| Inventario de **componentes maestros** (`COMPONENTES`) | [~] frecuencias documentadas; falta detalle por variante |
| **Componentes de formulario con estados** (Input/Button/Select) | [x] `HOMOLOGADO 2026 · Forms` (2026-09-12) |
| **Ligar** componentes existentes de `COMPONENTES` a los tokens | [ ] |
| Homologar restos **SDS** → base única | [ ] |
| Consolidar/deprecar colección legacy `Colección de variables` | [ ] |

---

## Módulos (Desktop → responsive)

| # | Módulo | Página (ID) | Homolog. | Tablet | Mobile | UX ✔ | Prototipo |
|---|---|---|---|---|---|---|---|
| 1 | Login | `1.0 Login` (`0:1`) | [~] | [x] | [x] | [~] | [x] |
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

### Login — detalle (MOVIDO a páginas finales ✅)
`03_Mobile`: `Mobile - Login_01_Acceso` `40000017:4592` · `Mobile - Login_02_Estacion` `40000019:4592`.
`02_Tablet`: `Tablet - Login_01_Acceso` `40000020:4592` · `Tablet - Login_02_Estacion` `40000021:4592`.
Prototipo: Continuar (Paso 1) → Paso 2 (Smart Animate), mobile y tablet.
UX aplicado: placeholders/labels/stepper `tertiary`→`secondary` (pasa 4.5:1), labels de sección 10→14px.
Borde de input accesible aplicado (token `border/input` #8C8F96, 3.24:1).
**Pendiente (variantes de componente — `design-system-librarian`):** estados `focus`/`error`/`loading`,
área táctil del icono ojo/chevron, indicador de paso completado.

## Orden sugerido
1. **Fase 0 — fundaciones** (tokens color + tipografía) antes de responsivar en serie.
2. **Login** (más chico, valida el flujo end-to-end: homologar → responsivar → UX → prototipar).
3. **Inicio (MAIN)** (patrón sidebar + tabla → cards; define la mayoría de transforms).
4. Resto de módulos, uno por uno.

## Progreso global
- Módulos: **10** · Fundaciones: `Breakpoints` ✅, tokens color/tipografía pendientes.
- Homologados: 0 · Tablet: 0 · Mobile: 0 · UX: 0 · Prototipo: 0

> El desglose pantalla-por-pantalla dentro de cada módulo se documenta al empezar ese módulo.
