# Design System — CARESA WEB UI 2026

Tokens, estilos y componentes del archivo Figma. Componentes en la página `COMPONENTES`.

> ⚠️ **Estado de tokenización: casi nulo.** El archivo tiene **0 estilos de color, 0 estilos de texto**
> y solo 2 variables de color previas (`primary-Caressa`, `False-Default`) + la nueva colección
> **`Breakpoints`**. Homologar = **tokenizar de cero** (color + tipografía) sobre los componentes existentes.
> Tarea del `design-system-librarian`.
>
> Además hay restos de **SDS** (`--sds-*`) en algunas pantallas que se migran a la base única
> (componentes tipo **Untitled UI** + tokens de marca). Tipografía base: **Inter**.

## 0. Colección `Breakpoints` (creada 2026-09-11) ✅
`VariableCollectionId:40000007:4577` · modos `Desktop`/`Tablet`/`Mobile`. 11 variables numéricas de
layout y tipografía. Tabla de valores en `RESPONSIVE_TOKENS.md`.

## 1. Tokens SDS detectados (de `get_variable_defs`)

### Color
| Token | Valor |
|---|---|
| `--sds-color-text-default-default` | `#1e1e1e` |
| `--sds-color-text-default-tertiary` | `#b3b3b3` |
| `--sds-color-background-default-default` | `#ffffff` |
| `--sds-color-border-default-default` | `#d9d9d9` |
| `--sds-color-border-brand-default` | `#2c2c2c` |

### Tipografía
| Token | Valor |
|---|---|
| `--sds-typography-body-font-family` | **Inter** |
| `--sds-typography-body-size-medium` | `16` |
| `--sds-typography-body-font-weight-regular` | `400` |
| Estilo `Body Base` | Inter Regular 16 / line-height 1.4 |

### Espaciado / tamaño
| Token | Valor |
|---|---|
| `--sds-size-space-200` | `8` |
| `--sds-size-space-300` | `12` |
| `--sds-size-space-400` | `16` |
| `--sds-size-radius-200` | `8` |
| `--sds-size-stroke-border` | `1` |

> ⏳ Falta extraer el set completo (escala tipográfica de headings, paleta de marca verde/lima,
> todos los espaciados). Ejecutar `design-system-librarian` sobre los nodos del design system.

## 2. Marca CARESA (observado visualmente)
- Login branded: panel oscuro **verde** con acento **lima/amarillo-verde** y logo CARESA.
- Confirmar hex exactos de la paleta de marca (pendiente extracción).

## 3. Componentes detectados (inventario por frecuencia)
| Componente | Aprox. instancias | Sistema |
|---|---|---|
| Table cell | 1005 | Untitled-style |
| Avatar | 266 | Untitled-style |
| Button | 257 | mixto |
| _Nav item base | 133 | Untitled-style |
| _Pagination button group base | 99 | Untitled-style |
| _Button group base | 99 | Untitled-style |
| Featured icon | 88 | Untitled-style |
| Metric item / Number and chart / Credit card | 55 c/u | Untitled-style |
| Badge | 36 | mixto |
| Input (Email/Pass/Caja) | login | SDS + custom |

## 4. Brechas de homologación detectadas
- **Dos design systems mezclados** (SDS vs Untitled-style) → unificar.
- Nombres de capa mixtos: hay semánticos (`Btn Continuar`, `Login Card`) y genéricos
  (`Frame 1000004102`, `Group 33779`, `Rectangle`).
- Pendiente auditoría formal con `figma-auditor` sobre la propuesta elegida.

---

> Fuente: página `PROPUESTAS` del archivo de trabajo `DRcQy7uKgoL5AlMPK0fJU7` (copia editable). Sincronizar con `RESPONSIVE_TOKENS.md`.
