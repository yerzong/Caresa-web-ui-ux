# Matriz de Homologación Responsive

Reglas para traducir la versión **Web/Desktop** (fuente de verdad) a **Tablet** y **Mobile**.
Valores base verificados contra Untitled UI, WCAG 2.2 y prácticas de grid 8pt (2025-2026).
Ajustar a lo que exista en Figma cuando se afinen los tokens de marca.

## Método correcto (una sola pantalla que responde, sin duplicar)
1. Auto Layout en todo: contenedores raíz `Fill` en ancho, `Hug` en alto.
2. **Variables por modo** (colección `Breakpoints`) ligadas a padding/gap/min-max/tamaño de fuente.
3. Cambiar el **modo** del frame (Desktop/Tablet/Mobile) reflowa todo el subárbol.
4. Los cambios de **dirección** (fila→columna) y **hug/fill** NO se pueden ligar a variable →
   requieren variante o **script `use_figma`** (lo hace `responsive-architect`).

## Breakpoints / Frames
| Dispositivo | Ancho frame | Referencia | Modo variable |
|---|---|---|---|
| Desktop | 1440 px | MacBook / Web | `Desktop` (fuente de verdad) |
| Tablet | 834 px | iPad Pro 11" | `Tablet` |
| Mobile | 393 px | iPhone 15 | `Mobile` |

## Variables `Breakpoints` (ya creadas en Figma)
Colección `VariableCollectionId:40000007:4577`. Valores por modo `[Desktop, Tablet, Mobile]`:

| Variable | Scope | Desktop | Tablet | Mobile |
|---|---|---|---|---|
| `container/max-width` | width/height | 1216 | 768 | 361 |
| `page/margin` | width/gap | 112 | 32 | 16 |
| `section/padding` | gap/width | 32 | 24 | 16 |
| `grid/gutter` | gap | 32 | 24 | 16 |
| `touch/min-target` | width/height | 40 | 40 | 44 |
| `type/display` | font-size | 60 | 44 | 36 |
| `type/h1` | font-size | 36 | 32 | 28 |
| `type/h2` | font-size | 30 | 26 | 24 |
| `type/h3` | font-size | 24 | 22 | 20 |
| `type/body` | font-size | 16 | 16 | 16 |
| `type/small` | font-size | 12 | 12 | 12 |

> Line-height objetivo ≈ 1.5 en body (16/24), ~1.25 en headings. Grid columnas 12/8/4 (documental,
> no bindable: se aplica con el número de columnas del Layout Grid por breakpoint).

## Comportamiento de componentes (Desktop → Mobile)
| Componente | Desktop | Mobile |
|---|---|---|
| Navbar superior | Links horizontales visibles | Hamburguesa → **drawer** (overlay) |
| Sidebar | Fija a la izquierda | Off-canvas **drawer** / tab bar inferior |
| Tabla de datos | Tabla completa | **Cards apiladas** (label:valor) |
| Grid N columnas (3–4) | N columnas | 1 columna (Tablet suele 2) |
| Card horizontal | Auto Layout → (fila) | Auto Layout ↓ (columna), imagen `Fill` |
| Botón primario | `Hug contents` | `Fill container` (ancho completo) |
| Fila de filtros | Horizontal | Stack vertical o sheet colapsable |
| Modal centrado | Centrado | Full-screen sheet |

## Reglas de Auto Layout responsive
- Contenedores raíz: `Fill container` en ancho; padding/gap vía **variable** `Breakpoints`.
- Horizontal que no cabe → vertical (aplicar por script si depende del modo).
- Posición absoluta solo para badges/overlays.
- Móvil: respetar `touch/min-target` (44) en toda acción táctil.

## Accesibilidad al responsivar (mínimos, ver `UX_PRINCIPLES.md`)
- Sin scroll horizontal a 393/320 px (WCAG 1.4.10 Reflow).
- Texto body ≥ 16 px en móvil; contraste ≥ 4.5:1 (texto) / 3:1 (UI).

---

> Mantener sincronizada con `DESIGN_SYSTEM.md`. Si un valor cambia aquí, registrarlo en `CHANGELOG.md`
> y, si aplica, actualizar la variable en la colección `Breakpoints`.
