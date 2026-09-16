# Plan de Migración NEW_ — Rehacer de 0% (responsivo, atómico, fiel)

> Decisión 2026-09-15: la base previa en sandbox NO convence → se rehace **de 0%** con esta metodología.
> **Prohibido código.** Único objetivo: UI en Figma. **No se toca NADA de lo existente** (páginas fuente ni sus nodos).

## Convención de nombres
- **Páginas nuevas:** `NEW_00 Design System`, `NEW_01 Login`, `NEW_02 Inicio`, `NEW_03 Carrito`,
  `NEW_04 Catalogos`, `NEW_05 Consultas`, `NEW_06 Corte`, `NEW_07 Pedidos`, `NEW_08 Chat`, `NEW_09 Abonos`, `NEW_10 Recompra`.
- **Componentes:** `Atom/…` · `Molecule/…` · `Organism/…` (variantes con propiedades; nombres semánticos).
- **Pantallas:** `Screen/{Módulo}_{NN}_{Nombre}--{Desktop|Tablet|Mobile}` (ej. `Screen/Login_01_Acceso--Mobile`).

## Fases
| # | Fase | Salida | Estado |
|---|---|---|---|
| 1 | **Análisis profundo** (solo lectura): secciones, frames y **connectors** (a dónde lleva cada flecha) | `docs/FLOWS.md` | [x] 212 connectors mapeados (2026-09-15) |
| 2 | **NEW_00 Design System**: átomos (tokens ya existentes se conservan) + moléculas fieles extraídas de la UI real | página `NEW_00` | [x] catálogo 18 + Login set + Modal/TableRow/Table (faltan: dropdown base, avatar label group) |
| 3 | **Migración por módulo** (una página NEW_XX a la vez): pantallas solo-instancias × 3 breakpoints | páginas `NEW_01..10` | [~] **NEW_01 Login LISTO** (6 screens + prototipo + flows); sigue NEW_02 Inicio |
| 4 | **Flujos/prototipo**: recablear los connectors como interacciones en las pantallas nuevas | prototipo | [ ] |
| 5 | **QA**: checklist UX/WCAG por pantalla + registro + commit/push | docs + GitHub | [ ] |

## Reglas de la migración
1. Analizar SIEMPRE el original antes de construir (`get_screenshot` + estructura). Fidelidad: si se ve distinto, está mal.
2. Pantallas ensambladas **solo con instancias** de `NEW_00`. Nada hardcodeado (tokens Color/Spacing/Radius/Tipografía/Breakpoints).
3. Auto Layout en todo (HUG/FILL); absolutos solo overlays deliberados. Touch ≥44 en móvil.
4. **Una pantalla por tarea**; actualizar `PROJECT_MAP.md` + `CHANGELOG.md` + push antes de pasar a la siguiente.
5. Orden de módulos: 01 Login → 02 Inicio → 03 Carrito → 05 Consultas → 07 Pedidos → resto.

## Qué se conserva de la etapa previa
- **Tokens** (colecciones `Color`, `Spacing`, `Radius`, `Breakpoints` + 9 estilos de texto): extraídos del diseño real → se reutilizan en NEW_00.
- Los screens/experimentos del sandbox previo quedan **obsoletos** (se archivarán/borrarán al final de la migración).
