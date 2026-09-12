# Design System — CARESA WEB UI 2026

Tokens, estilos y componentes detectados en el archivo Figma.

> ⚠️ **El archivo mezcla dos sistemas.** Decisión pendiente (ver `PROJECT_MAP.md` PASO 0):
> consolidar a UNO solo antes de responsivar.
> - **SDS — Simple Design System** (tokens `--sds-*`) → usado en los login "SDS".
> - **Componentes tipo Untitled UI** → usados en los dashboards.

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

> Fuente: página `PROPUESTAS` del archivo `OL0CHY8eN9zjNeGmHg0el3`. Sincronizar con `RESPONSIVE_TOKENS.md`.
