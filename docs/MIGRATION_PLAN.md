# Plan de Migración NEW_ — Rehacer de 0% (responsivo, atómico, fiel)

> Decisión 2026-09-15: la base previa en sandbox NO convence → se rehace **de 0%** con esta metodología.
> **Prohibido código.** Único objetivo: UI en Figma. **No se toca NADA de lo existente** (páginas fuente ni sus nodos).

## Convención de nombres (ACTUALIZADA 2026-09-17)
- **Páginas de trabajo:** `NEW_00 Design System` + 3 páginas responsive: `NEW_WEB · Desktop (1728)` (`40000365:5103`),
  `NEW_TABLET · (834)` (`40000365:5104`), `NEW_MOBILE · (393)` (`40000365:5105`).
  Las páginas por módulo `NEW_01..NEW_10` fueron eliminadas — cada módulo vive como **SECTION** dentro de las 3 páginas
  (`01 · LOGIN`, `02 · INICIO`, `03 · CARRITO`, `05 · CONSULTAS`, `07 · PEDIDOS`, …), con **subsections por flujo**
  y las pantallas en fila horizontal (gaps: 120 pantalla, 200 subsección, 500 módulo).
  ⚠️ Toda pantalla nueva se AGREGA a la section de su módulo en la página de su breakpoint — NO crear páginas nuevas.
- **Componentes:** `Atom/…` · `Molecule/…` · `Organism/…` (variantes con propiedades; nombres semánticos).
- **Pantallas:** `Screen/{Módulo}_{NN}_{Nombre}--{Desktop|Tablet|Mobile}` (ej. `Screen/Login_01_Acceso--Mobile`).

## Fases
| # | Fase | Salida | Estado |
|---|---|---|---|
| 1 | **Análisis profundo** (solo lectura): secciones, frames y **connectors** (a dónde lleva cada flecha) | `docs/FLOWS.md` | [x] 212 connectors mapeados (2026-09-15) |
| 2 | **NEW_00 Design System**: átomos (tokens ya existentes se conservan) + moléculas fieles extraídas de la UI real | página `NEW_00` | [x] catálogo 18 + Login set + Modal/TableRow/Table (faltan: dropdown base, avatar label group) |
| 3 | **Migración por módulo** (una página NEW_XX a la vez): pantallas solo-instancias × 3 breakpoints | páginas `NEW_01..10` | [~] **NEW_01 Login LISTO**; **NEW_02 Inicio: Home ×3 lista** (faltan sub-pantallas del módulo) |
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
