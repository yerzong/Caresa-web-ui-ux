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
| `border/default` | `#E3E3DD` | borde base |
| `border/strong` | `#E6E6E6` | borde fuerte |
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

## 4. Brechas de homologación pendientes
- Migrar restos **SDS** (`--sds-*`) a los tokens `Color`/tipografía de arriba.
- **Ligar** los componentes de `COMPONENTES` a estos tokens (hoy usan hex sueltos) — tarea de homologación.
- Consolidar/deprecar la colección legacy `Colección de variables`.
- Nombres de capa mixtos: normalizar a semánticos.
- Auditar contraste de la marca lima donde se use como texto.

---

> Fuente: página `COMPONENTES` del archivo `DRcQy7uKgoL5AlMPK0fJU7`. Sincronizar con `RESPONSIVE_TOKENS.md`.
