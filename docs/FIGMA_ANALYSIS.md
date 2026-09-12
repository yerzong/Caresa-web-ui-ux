# Análisis del Archivo Figma

Análisis de la estructura del archivo **CARESA WEB UI 2026** (`fileKey: OL0CHY8eN9zjNeGmHg0el3`).

## Estado
🟢 **Lectura habilitada** · 🔴 **Escritura BLOQUEADA** (archivo en modo solo lectura para la cuenta Gerson).

Cuenta conectada: **Gerson Garcia** (gersongarcia@zurco.com.mx).
Prueba de escritura (2026-09-11): `createPage` → `Can't call "createPage" in read-only mode`.

### Para habilitar escritura (elegir una)
- **A (recomendada):** mover el archivo al team **Zurco Designio** (Gerson tiene asiento Full).
- **B:** el dueño comparte a `gersongarcia@zurco.com.mx` como **"can edit"**.
- **C (evitar):** usar cuenta de Dilan (afecta también la otra terminal de Zurco).

## Hallazgo principal ⚠️
El archivo tiene **una sola página: `PROPUESTAS`** y contiene **propuestas de diseño
(variantes en exploración)**, NO una aplicación web terminada con un set fijo de pantallas.
Todo está en **Desktop**; **no existe todavía ninguna versión Tablet/Mobile**.

Esto cambia la estrategia: **antes de responsivar hay que ELEGIR la propuesta ganadora**
(layout con sidebar vs. navbar, y variante de login), consolidar el design system, y
recién entonces adaptar a Tablet/Mobile. No se responsivizan propuestas que competirán entre sí.

## Estructura real (página `PROPUESTAS`, id `184:3079`)

Canvas ~21908×21262 px. Secciones de nivel superior:

### 1. `PROPUESTA SIDEBAR` (id `184:4559`) — Dashboards con sidebar izquierdo
Layout de panel administrativo con navegación lateral. Contiene 3 sub-propuestas:
- `PROPUESTA 1` (id `189:5961`) — 1 pantalla Desktop (1856×1131)
- `PROPUESTA 2` (id `189:5962`) — varias pantallas Desktop (1856×1077)
- `PROPIESTA 3` (id `189:5963`) *(nombre con typo en el archivo)* — varias pantallas Desktop

### 2. `PROPUESTA BANNER / NAVBAR` v1 (id `184:8903`) — Dashboards con navbar superior
Alternativa al sidebar: navegación en barra superior. (6358×1520)

### 3. `PROPUESTA BANNER / NAVBAR` v2 (id `211:6276`) — Más variantes de navbar
Conjunto ampliado de dashboards con navbar superior. (10103×4153, varias pantallas Desktop)

### 4. `PROPUESTA LOGIN` (id `184:14677`) — Flujos de acceso
- `Propuesta A — CARESA WEB UI 2026` (id `184:14301`): branded (Brand Panel verde + Form Panel).
  - `Login 2026 — Propuesta A` (1440×900) — usuario/email + contraseña.
  - `Login 2026 — Propuesta A (Paso 2)` (1440×900) — paso 2 (selección de caja/sucursal).
- `CARESA WEB UI 2026 — Login Flow (SDS)` (id `184:14369`): usa Simple Design System.
  - `CARESA — Login Paso 1 (SDS)` (1440×900)
  - `CARESA — Login Paso 2 · Sucursal (SDS)` (1440×900)
  - + variantes adicionales de Login Paso 1 (ids `193:5451`, `193:5462`)

## Sistemas de diseño detectados (⚠️ mezcla)
- **Simple Design System (SDS):** los login "SDS" usan tokens `--sds-*` (ver `DESIGN_SYSTEM.md`).
- **Componentes tipo Untitled UI:** los dashboards usan `_Nav item base`, `Featured icon`,
  `Metric item`, `_Button group base`, `_Pagination button group base`, `Table cell`, etc.
- Tipografía base: **Inter**.
- **Implicación:** homologar a UN solo sistema antes de responsivar.

## Volumen (densidad del archivo)
~1005 "Table cell", 704 "Text", 266 "Avatar", 257 "Button", 133 "_Nav item base",
55 "Metric item"/"Credit card"/"Heading". Archivo denso → trabajar por sección/pantalla.

## Inventario de pantallas Desktop
15 frames "Desktop" en total (dashboards) + 4-6 frames de Login (1440×900). Detalle y
naming en `PROJECT_MAP.md`.

## Pendiente de análisis
- [ ] Capturas individuales por propuesta para nombrar cada dashboard por su función.
- [ ] Confirmar cuál propuesta (sidebar vs navbar) es la dirección elegida.
- [ ] Extraer set completo de variables/estilos del design system.
