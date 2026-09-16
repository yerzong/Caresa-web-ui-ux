# Design System — CARESA WEB UI 2026

Tokens, estilos y componentes del archivo Figma (`DRcQy7uKgoL5AlMPK0fJU7`). Componentes en la página `COMPONENTES`.
Valores extraídos del uso real (scan de `COMPONENTES`, 2026-09-11) y creados como variables/estilos.

## Colecciones de variables
| Colección | Modos | Contenido |
|---|---|---|
| `Breakpoints` | Desktop/Tablet/Mobile | layout + tamaños de fuente responsive (ver `RESPONSIVE_TOKENS.md`) |
| `Color` | Default | 23 tokens de color (marca/neutral/semántico) |
| `Colección de variables` (legacy) | Mode 1 | `primary-Caressa`, `False-Default` — consolidar/deprecar |

## 1. Color (colección `Color` · `VariableCollectionId:40000009:4577`)
Marca CARESA = **lima `#AEF803`** + **verde `#006C00`**.

| Token | Hex | Uso |
|---|---|---|
| `brand/lime` | `#AEF803` | primario (acentos, CTA) |
| `brand/green` | `#006C00` | marca oscura / éxito |
| `brand/green-subtle` | `#E0FFE5` | fondo éxito |
| `brand/olive` | `#272C11` | acento oscuro |
| `text/primary` | `#101828` | texto principal |
| `text/secondary` | `#6B6D73` | texto secundario |
| `text/tertiary` | `#7A7C81` | texto terciario |
| `text/slate` | `#364153` | texto slate |
| `text/on-brand` | `#101828` | texto sobre lima (oscuro) |
| `text/inverse` | `#FFFFFF` | texto sobre oscuro |
| `bg/default` | `#FFFFFF` | fondo base |
| `bg/subtle` | `#FAFAF7` | fondo sutil |
| `bg/muted` | `#F0F0EC` | fondo apagado |
| `bg/inverse` | `#101828` | fondo oscuro |
| `border/default` | `#E3E3DD` | borde base (decorativo, no cumple 3:1) |
| `border/strong` | `#E6E6E6` | borde fuerte |
| `border/input` | `#8C8F96` | borde de campos (3.24:1 sobre blanco, WCAG 1.4.11 ✓) |
| `semantic/info` | `#155DFC` | info / link |
| `semantic/warning` | `#D08700` | advertencia |
| `semantic/danger` | `#F54900` | error / destructivo |
| `semantic/success` | `#006C00` | éxito |
| `semantic/danger-bg` | `#FEE4E2` | fondo error |
| `base/black` | `#000000` | — |
| `base/white` | `#FFFFFF` | — |

> ⚠️ Contraste: `brand/lime` sobre blanco NO cumple para texto (usar `brand/lime` solo como fondo/acento
> con `text/on-brand` oscuro encima). Verificar con `ui-ux-reviewer`.

## 2. Tipografía (estilos de texto · Inter)
| Estilo | Fuente | Tamaño/LH |
|---|---|---|
| `Heading/Display` | Inter Bold | 36 / 44 |
| `Heading/H1` | Inter Bold | 26 / 34 |
| `Heading/H2` | Inter Bold | 22 / 30 |
| `Heading/H3` | Inter Medium | 20 / 28 |
| `Body/Strong` | Inter Bold | 16 / 24 |
| `Body/Semibold` | Inter Semi Bold | 16 / 24 |
| `Body/Regular` | Inter Regular | 16 / 24 |
| `Label/Medium` | Inter Semi Bold | 14 / 20 |
| `Label/Small` | Inter Semi Bold | 10 / 14 |

> Para responsive, ligar `fontSize` a las variables `type/*` de `Breakpoints` (o intercambiar estilo por modo).

## 2b. Espaciado y radios (átomos)
Colección `Spacing` (`40000074:4577`), scopes GAP+WIDTH/HEIGHT:
`space/2xs`=4 · `xs`=8 · `sm`=12 · `md`=16 · `lg`=24 · `xl`=32 · `2xl`=48 · `3xl`=64.

Colección `Radius` (`40000074:4586`), scope CORNER_RADIUS:
`radius/sm`=4 · `md`=8 · `lg`=12 · `xl`=16 · `full`=999.

> Capa de átomos completa: **Color**, **Tipografía**, **Spacing**, **Radius**, **Breakpoints**.
> Regla: ningún nodo con valores hardcodeados — todo vía estas variables/estilos.

## 2c. NEW_00 Design System (página `40000110:4577`) — catálogo de componentes REALES
Sección `01 Catálogo` (`40000113:4657`): **instancias indexadas para REUSAR (no duplicar)**:

| Componente | Main ID | | Componente | Main ID |
|---|---|---|---|---|
| Banner (navbar) | `470:45555` | | Input/Text (estados) | `40000034:4890` |
| Button CARESA (6 var) | `390:21859` | | Button/Primary (estados) | `40000035:4886` |
| Card marca (4 var) | `390:23706` | | Select (estados) | `40000036:4894` |
| Card filtros (4 var) | `392:24284` | | NavItem (estados) | `40000060:4886` |
| Card AUTOS (2 var) | `392:26247` | | Avatar UUI | `130:11113` |
| Alerts (7 var) | `464:68983` | | _Nav item base UUI | `130:12188` |
| Badge (2 var) | `430:14181` | | Dropdown menu UUI | `146:9363` |
| Barra progreso (6 var) | `392:25169` | | Table cell UUI | `130:8064` |
| Container filtros (7 var) | `433:15676` | | more-vertical UUI | `146:9430` |

Otros ya existentes: `BOTÓN BUSCAR` `393:27283`, `Autopartes - Section` `390:23171`, Input UUI `327:59646`, Select avatar `143:3244`.
Secciones `02 Molecules` / `03 Organisms` de NEW_00 contienen los componentes del Login (Stepper×2, LoginForm, EstacionForm, BrandPanel×3).

**Brechas (crear como Main Components propios):** `Molecule/Modal` (+header/actions — hoy son frames anónimos),
`Molecule/TableRow`/`Organism/Table` (hoy frames sueltos con celdas UUI), dropdown base homologado, `Avatar label group` propio.

## 3. Componentes (inventario por frecuencia — página `COMPONENTES`)
| Componente | Aprox. instancias | Sistema |
|---|---|---|
| Table cell | ~1005 | Untitled-style |
| Avatar | ~266 | Untitled-style |
| Button | ~257 | mixto |
| _Nav item base | ~133 | Untitled-style |
| _Pagination / _Button group base | ~99 c/u | Untitled-style |
| Featured icon | ~88 | Untitled-style |
| Metric item / Number and chart / Credit card | ~55 c/u | Untitled-style |
| Badge | ~36 | mixto |

## 3b. Componentes homologados 2026 · Forms (con estados)
Sección `HOMOLOGADO 2026 · Forms` (`40000034:4891`) en la página `COMPONENTES`. Cero hex sueltos;
todo ligado a tokens `Color` + estilos de texto. Propiedad de variante `State`.

| Component set | ID | Variantes (State) |
|---|---|---|
| `Input/Text` | `40000034:4890` | Default · Focus (anillo `semantic/info`) · Error (`semantic/danger` + helper) · Disabled |
| `Button/Primary` | `40000035:4886` | Default (lima) · Hover (`brand/green`) · Loading (spinner + "Cargando…") · Disabled |
| `Select` | `40000036:4894` | Default · Focus · Error · Disabled (con chevron) |
| `NavItem` | `40000060:4886` | Default · Active (indicador 3px `brand/lime`) · Hover — para drawer/nav oscuro |

Estados de grid (referencia, en `04_Claude_Sandbox`): `ProductGrid/Empty` `40000061:4581` · `ProductGrid/Loading` `40000061:4889`.

> Estos son los componentes canónicos para formularios. Al homologar/rehacer pantallas, **instanciar
> estos** en lugar de dibujar inputs/botones sueltos. Pendiente: sustituir los controles inline del
> Login del sandbox por instancias de estos componentes.

## 4. Brechas de homologación pendientes
- Migrar restos **SDS** (`--sds-*`) a los tokens `Color`/tipografía de arriba.
- **Ligar** los componentes de `COMPONENTES` a estos tokens (hoy usan hex sueltos) — tarea de homologación.
- Consolidar/deprecar la colección legacy `Colección de variables`.
- Nombres de capa mixtos: normalizar a semánticos.
- Auditar contraste de la marca lima donde se use como texto.

---

> Fuente: página `COMPONENTES` del archivo `DRcQy7uKgoL5AlMPK0fJU7`. Sincronizar con `RESPONSIVE_TOKENS.md`.
