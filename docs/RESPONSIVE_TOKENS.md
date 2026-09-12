# Matriz de Homologación Responsive

Reglas para traducir la versión **Web/Desktop** (fuente de verdad) a **Tablet** y **Mobile**.
Los valores concretos de tipografía, grid y componentes se **rellenan tras el análisis** del
design system real (`@docs/DESIGN_SYSTEM.md`). Lo de abajo es la estructura + valores base
recomendados; se ajustan a lo que exista en Figma.

## Breakpoints / Frames
| Dispositivo | Ancho frame | Referencia | Uso |
|---|---|---|---|
| Desktop | 1440 px | MacBook / Web | Fuente de verdad (existente) |
| Tablet | 834 px | iPad Pro 11" | Adaptación intermedia |
| Mobile | 393 px | iPhone 15 | Adaptación principal |

## 1. Tipografía (Desktop → Mobile)
> ⏳ Rellenar con la escala real del archivo. Base sugerida:

| Rol | Desktop | Tablet | Mobile |
|---|---|---|---|
| Display | 48 | 40 | 32 |
| H1 | 32 | 28 | 24 |
| H2 | 24 | 22 | 20 |
| H3 | 20 | 18 | 18 |
| Body | 16 | 16 | 16 |
| Small | 14 | 14 | 14 |

## 2. Grid y contenedores
| Propiedad | Desktop | Tablet | Mobile |
|---|---|---|---|
| Columnas | 12 | 8 | 4 |
| Max-width | 1440 | 834 | 393 |
| Margen lateral | 80 | 32 | 16 |
| Gutter | 24 | 16 | 16 |
| Padding contenedor | 64 | 32 | 16 |

## 3. Comportamiento de componentes reutilizables
> ⏳ Rellenar con los componentes reales. Reglas base:

| Componente | Desktop | Mobile |
|---|---|---|
| Navbar | Links horizontales visibles | Hamburguesa → drawer |
| Sidebar | Fija a la izquierda | Colapsa a drawer / oculta |
| Card horizontal | Auto Layout → (horizontal) | Auto Layout ↓ (vertical), imagen `Fill` |
| Button primario | `Hug contents` | `Fill container` (ancho completo) |
| Grid de N columnas | N columnas | 1 columna vertical |
| Tabla de datos | Tabla completa | Cards apiladas o scroll horizontal |

## 4. Reglas de Auto Layout responsive
- Contenedores raíz: `Fill container` en ancho.
- Elementos internos: `Fill` o `Fixed` según breakpoint (documentar por componente).
- Espaciados y paddings vía **variable**, nunca hardcoded.
- Horizontal que no cabe → vertical.

## 5. Variables de Figma (recomendado)
Cuando el archivo lo permita, usar **modos/variables** para anchos y espaciados en lugar de
valores fijos, para que un mismo componente responda por breakpoint sin duplicar lógica.

---

> Mantener esta matriz sincronizada con `DESIGN_SYSTEM.md`. Si un valor cambia aquí,
> registrarlo en `CHANGELOG.md`.
