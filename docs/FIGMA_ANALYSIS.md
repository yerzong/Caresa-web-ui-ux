# Análisis del Archivo Figma

Análisis de la estructura del archivo de trabajo **CW-Responsive-prueba** (`fileKey: DRcQy7uKgoL5AlMPK0fJU7`),
copia del original **CARESA WEB UI 2026** (`fileKey: OL0CHY8eN9zjNeGmHg0el3`, ahora solo lectura/deprecado).

## Estado
🟢 **Lectura habilitada** · 🟢 **Escritura HABILITADA** (verificada 2026-09-11 en la copia).

Cuenta conectada: **Gerson Garcia** (gersongarcia@zurco.com.mx), asiento **Full** en *Zurco Designio*.

## Hallazgo principal ✅ (corrige análisis previo)
El archivo **NO** es "una sola página de propuestas". Al inspeccionar con el Plugin API se ve la
**estructura real**: la **app Desktop completa ya existe**, organizada en **páginas por módulo**,
más una página `COMPONENTES` (design system) y una página `PROPUESTAS` (solo exploraciones).

> El análisis anterior solo veía `PROPUESTAS` porque `get_metadata` sin `nodeId` no listaba todas
> las páginas. Esto restaura la **misión original**: responsivar la app Desktop existente (no "elegir
> una propuesta"). Ver ADR 0003.

## Páginas reales (15 en total)

### Fuente de verdad Desktop — módulos (SOLO LECTURA)
Cada página es un **board de flujos** (con connectors) que contiene **varias pantallas Desktop** por módulo.

| Página | ID | Contenido (secciones top-level) |
|---|---|---|
| `1.0 Login` | `0:1` | `LOGIN` (5944×1343) + assets |
| `2.0 Inicio (MAIN)` | `4:2` | FILTRO MANUAL, BARRA DE VENTA, AUTOPARTES, PROMOCIONES, FILTRO INTELIGENTE, CATEGORÍAS, filtros por categoría, INICIO, INICIO - PERFIL |
| `3 Carrito` | `13:96` | MIGRACIÓN MÓDULO CARRITO (x2), CARRITO - MÁS OPCIONES, CARRITO DE VENTA RÁPIDA |
| `4 Catálogos` | `13:100` | CATÁLOGOS - CREAR/ABRIR BURBUJAS, Modal |
| `5 Consultas` | `13:104` | VENTAS, CRÉDITOS, GARANTÍAS |
| `6 Corte de caja` | `595:70899` | FILTRO MANUAL (10187×8443) |
| `7 Pedidos` | `681:51807` | PEDIDOS, Pantalla por defecto, SEGUIMIENTO ENVÍO (ADMIN), PEDIDOS - INTERFAZ/ACCIONES, VER PEDIDO (estados) |
| `8 Chat` | `681:53445` | MÓDULO CHAT WEB (12896×7451) |
| `9 Abonos` | `681:61345` | ABONOS (14388×2577) |
| `10 Recompra` | `681:61346` | MÓDULO DE COMPRAS (21506×3137) |

### Design system (SOLO LECTURA salvo tarea de librarian)
| Página | ID | Contenido |
|---|---|---|
| `COMPONENTES` | `747:28881` | `COMPONENTES - NO BORRAR` (3280×7409) + `Autopartes - Section` |

### Exploraciones (referencia, NO es la app)
| Página | ID | Contenido |
|---|---|---|
| `PROPUESTAS` | `184:3079` | PROPUESTA SIDEBAR, PROPUESTA BANNER/NAVBAR (x2), PROPUESTA LOGIN, INICIO |

### Páginas de trabajo responsive (creadas 2026-09-11 — ESCRITURA)
| Página | ID | Rol |
|---|---|---|
| `02_Tablet` | `40000003:4579` | Pantallas Tablet (834) aprobadas |
| `03_Mobile` | `40000003:4580` | Pantallas Mobile (393) aprobadas |
| `04_Claude_Sandbox` | `40000003:4581` | Zona de generación/pruebas |

## Estado de tokenización (⚠️ casi nulo)
- **Variables:** 1 colección previa (`Colección de variables`) con solo 2 colores (`False-Default`, `primary-Caressa`).
- **+ NUEVO:** colección **`Breakpoints`** (`VariableCollectionId:40000007:4577`) con modos **Desktop/Tablet/Mobile**
  y 11 variables numéricas (container, márgenes, gutter, padding, escala tipográfica, touch target). Ver `RESPONSIVE_TOKENS.md`.
- **Estilos de color:** 0 · **Estilos de texto:** 0.
- **Implicación:** homologar = **tokenizar de cero** color + tipografía sobre los componentes existentes.
  Tarea del `design-system-librarian`.

## Sistemas de diseño observados
- Componentes tipo **Untitled UI** en dashboards (tablas, métricas, nav items, paginación).
- Login/algunas pantallas con restos **SDS** (`--sds-*`) → migrar a la base única.
- Tipografía base: **Inter**. Marca: verde/lima (var `primary-Caressa`).

## Método de trabajo (recordatorio)
Archivo **enorme** y denso → trabajar **una pantalla/módulo a la vez**, en `04_Claude_Sandbox`,
usando `get_metadata` para ubicar nodos y `get_design_context`/`get_screenshot` solo sobre el nodo objetivo.
