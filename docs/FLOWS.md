# Mapa de Flujos (connectors del archivo original)

Extraído vía Plugin API 2026-09-15. Total: **212 connectors** en 5 páginas (las otras 5 no tienen).
Este mapa guía el **re-cableado del prototipo** en las páginas `NEW_XX` (Fase 4) y evita inventar navegación.

> Nota: los endpoints se listan por su contexto (sección › frame). Los nombres `MacBook Pro 16" - NN`
> son las pantallas Desktop del original. Ningún connector tiene texto/etiqueta.

## 1.0 Login (0 connectors)
Flujo implícito por diseño: `Acceso (Paso 1)` → `Caja/Estación (Paso 2)` → entra al sistema (Inicio).

## 2.0 Inicio (MAIN) — 52 connectors
Patrones detectados:
- **Hub central:** la pantalla `MB-57` (Inicio con banner) recibe flechas desde las secciones `FILTRO INTELIGENTE`, `FILTRO MANUAL`, `PROMOCIONES` y `CATEGORÍAS` → es la **Home** desde donde salen los 4 modos de búsqueda.
- **Cadena de filtro manual:** `MB-18 → 19 → 20 → 21` (Card filtros paso a paso; botón BUSCAR dispara resultados) + tablas de resultados → vuelven a Card filtros.
- **Cadena de marcas/catálogo:** `MB-22 ↔ 23 ↔ 25 ↔ 27 ↔ 43` (Card marca → CARD AUTOS → botones) — drill-down por marca/auto.
- **Barra de venta:** grupos de `BARRA DE VENTA` → Banner de `MB-49` (modales de venta: selects, botones, checkbox de alerta).
- **Resultados con dropdown:** tablas/scrollbars → `Dropdown` de `MB-44`/`MB-58` (ordenar/format), `Dropdown menu → _Dropdown list item`.
- **Filtros por categoría:** secciones `FILTROS - FOCOS/ANTICONGELANTES/CABLES/FUSIBLES/QUÍMICOS` → Cards marca de `MB-55` (variantes de card por categoría).
- **INICIO - PERFIL:** grupos → `Dropdown menu` del perfil; búsqueda → `Input field` del header; tabla → botón `more-vertical`; y `MB-61 → Banner de MB-57` (perfil regresa a Home).

## 3 Carrito — 41 connectors
- **MIGRACIÓN MODULO CARRITO** (flujo principal): `Frame 1000004189` (carrito base) es el **hub** — recibe de tablas, botones y variantes; `Table (1000004260)` ↔ modales (`1000004281/1000004282`) = acciones sobre líneas del carrito; cadena de modales `1000004543 → 1000004272`, `1000004522 → 1000004503 → 1000004510 (Table)`.
- **CARRITO - MÁS OPCIONES:** `Modal 1000004548` es el hub de opciones — recibe de 5+ tablas/botones; `Table 1000004300` y `Table 1000004286` concentran acciones; `1000004286 → carrito base (1000004189)` conecta ambos flujos.
- **Venta rápida:** sección `CARRITO DE VENTA RÁPIDA` sin connectors (pantallas sueltas).

## 4 Catálogos — 17 connectors
- **CREAR BURBUJAS:** cadena lineal `MB-57 ← 58 ← 59 ← 60 ← 61 ← 63 ← 64 ← 65 ← 66 ← 67` (wizard paso a paso de creación) + `MB-70 → MB-69`.
- **ABRIR BURBUJAS:** `MB-73 → Modal`, `MB-74 → MB-73`, `Rectangle → MB-74`, y `ABRIR → CREAR (MB-70)` (cross-link entre secciones).

## 5 Consultas — 54 connectors
- **VENTAS:** `Table 1000004572` = hub de "más opciones" (recibe de 4+ orígenes; modales encadenados `1000004134 → 1000004133`); `MB-67` = pantalla principal de Ventas (recibe de MB-68, frames y la tabla de opciones).
- **CRÉDITOS:** `Table 1000004577` = hub; sub-flujo **ABONAR/PAGAR** con cadena de modales (`Group 143 → 144 → 145/146 → 147/148` + dropdowns); `MB-73` = pantalla principal de Créditos; **CLIENTE - MÁS OPCIONES** replica el patrón con `Table 1000004583` y cadena ABONAR/PAGAR propia.
- **Cross:** `CRÉDITOS (Banner 1000004580) → VENTAS (MB-67)` (tabs entre consultas).
- **GARANTÍAS:** `MB-69` = principal; grupos → modales encadenados (`138 → 139 → 140`), `Alerts → Modal 142`.

## 7 Pedidos — 48 connectors
- **Hub:** `PEDIDOS › MB-9` = pantalla principal — de ella salen: Surtir, Ver pedido, Confirmar, Cancelar; y recibe de `Pantalla por defecto (MB-16)`, `Filtros y búsqueda (MB-19)`, `Columnas tablas (MB-21)`.
- **CONFIRMAR/CANCELAR:** botones → `Ver pedido › Modal`.
- **Surtir pedidos:** `Validar pedidos › Modal` = hub (valida ↔ confirmar ↔ añadir producto con buscador ↔ editar/eliminar producto ↔ variantes MB-13/23).
- **Enviar pedido:** `Confirmar › Modal` hub (tabla, acciones de modal, confirmaciones encadenadas) → regresa a `PEDIDOS MB-9`.
- **VER PEDIDO (ESTADOS):** `MB-22` → variantes de `Pedidos` por estado (6 flechas = 6 estados); modal → Seguimiento envío (ADMIN), → Enviar, → Surtir.
- **Selección múltiple:** `MB-17` → Alerts (2) + Confirmar/Cancelar múltiple.

## 6 Corte de caja · 8 Chat · 9 Abonos · 10 Recompra — 0 connectors
Boards de pantallas sin flechas; el flujo se infiere por orden visual (documentar al migrar cada módulo).

---

## Implicaciones para la migración NEW_
1. **Patrón dominante:** pantalla principal por módulo (hub) + **modales/dropdowns** como sub-flujos → en responsive,
   los modales se vuelven **sheets/full-screen** en móvil (ver `RESPONSIVE_TOKENS.md`).
2. Componentes de flujo recurrentes a tener en NEW_00: `Table` + acciones fila (`more-vertical`), `Modal` (+header/actions),
   `Dropdown menu`/`_Dropdown list item`, `Alerts`, `Card marca`/`Card filtros`, `Banner`/header con búsqueda.
3. El prototipo de cada `NEW_XX` replica estas flechas como reactions (NAVIGATE para pantallas, OVERLAY para modales/dropdowns).
