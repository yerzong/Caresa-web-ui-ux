# Mapa del Proyecto — CARESA WEB UI 2026

Inventario real y checklist de avance. La app **Desktop ya existe** por módulos (ver `FIGMA_ANALYSIS.md`).
Objetivo por pantalla: existir en **Desktop (fuente) → Tablet (834) → Mobile (393)**, homologada y con UI/UX + prototipo.

## Leyenda
- `[ ]` pendiente · `[~]` en progreso/sandbox · `[x]` aprobado y movido a página final
- Columnas por módulo: `Homologada | Tablet | Mobile | UX ✔ | Prototipo`

> ⚠️ Cada módulo es un **board con varias pantallas**. El desglose pantalla-por-pantalla se
> completa con una pasada de `figma-auditor`/`responsive-architect` por módulo (tarea atómica).

---

## Fase 0 — Fundaciones (transversal)
| Tarea | Estado |
|---|---|
| Colección `Breakpoints` (Desktop/Tablet/Mobile) | [x] creada 2026-09-11 |
| Tokens de **color** (marca lima/verde + neutrales + semánticos) | [x] 23 tokens, colección `Color` (2026-09-11) |
| Estilos de **tipografía** (Inter, Display→Label) | [x] 9 estilos de texto (2026-09-11) |
| Inventario de **componentes maestros** (`COMPONENTES`) | [~] frecuencias documentadas; falta detalle por variante |
| **Componentes de formulario con estados** (Input/Button/Select) | [x] `HOMOLOGADO 2026 · Forms` (2026-09-12) |
| **Ligar** componentes existentes de `COMPONENTES` a los tokens | [ ] |
| Homologar restos **SDS** → base única | [ ] |
| Consolidar/deprecar colección legacy `Colección de variables` | [ ] |

---

## Módulos (Desktop → responsive)

| # | Módulo | Página (ID) | Homolog. | Tablet | Mobile | UX ✔ | Prototipo |
|---|---|---|---|---|---|---|---|
| 1 | Login | `1.0 Login` (`0:1`) | [~] | [x] | [x] | [~] | [x] |
| 2 | Inicio (MAIN) | `2.0 Inicio (MAIN)` (`4:2`) | [~] | [~] | [~] | [~] | [~] |
| 3 | Carrito | `3 Carrito` (`13:96`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 4 | Catálogos | `4 Catálogos` (`13:100`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 5 | Consultas | `5 Consultas` (`13:104`) | [~] | [x] | [x] | [ ] | [~] |
| 6 | Corte de caja | `6 Corte de caja` (`595:70899`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 7 | Pedidos | `7 Pedidos` (`681:51807`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 8 | Chat | `8 Chat` (`681:53445`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 9 | Abonos | `9 Abonos` (`681:61345`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 10 | Recompra / Compras | `10 Recompra` (`681:61346`) | [ ] | [ ] | [ ] | [ ] | [ ] |

---

### Login — detalle (RECONSTRUIDO atómico + fiel, en `04_Claude_Sandbox` › sección FIEL)
Paso 1 (Acceso) en 3 breakpoints, reusando componentes: `Screen/Login--Mobile` `40000077:89995` ·
`Screen/Login--Tablet` `40000083:89926` · `Screen/Login--Desktop` `40000083:90012`.
Componentes en sección `Componentes — Login`: `Molecule/Stepper`, `Organism/LoginForm`, `Organism/BrandPanel--{Mobile,Tablet,Desktop}`.
Inputs = Input real de librería `327:59646` (mail/lock). Los borradores antiguos en `03_Mobile`/`02_Tablet` quedan obsoletos (a reemplazar).
**Pendiente:** Paso 2 (Estación) atómico; mover a páginas finales tras aprobar.
Prototipo: Continuar (Paso 1) → Paso 2 (Smart Animate), mobile y tablet.
UX aplicado: placeholders/labels/stepper `tertiary`→`secondary` (pasa 4.5:1), labels de sección 10→14px.
Borde de input accesible aplicado (token `border/input` #8C8F96, 3.24:1).
**Pendiente (variantes de componente — `design-system-librarian`):** estados `focus`/`error`/`loading`,
área táctil del icono ojo/chevron, indicador de paso completado.

### NEW_05 Consultas — Overlays tab GARANTÍAS: VerDetalle + Aplicar + Alerta (9 overlays)
Todos en `NEW_05 Consultas`. Posición: Desktop x=0/1900/3800 y=7500 · Tablet x=0/950/1900 y=9000 · Mobile x=3900/4400/4900 y=7500.
- Desktop: `GarantiasVerDetalle` `40000253:5948` · `GarantiasAplicar` `40000254:5948` · `GarantiasAlerta` `40000254:5979`
- Tablet: `GarantiasVerDetalle` `40000257:5948` · `GarantiasAplicar` `40000257:6017` · `GarantiasAlerta` `40000257:6048`
- Mobile: `GarantiasVerDetalle` `40000259:5948` (bottom-sheet) · `GarantiasAplicar` `40000259:5997` (bottom-sheet) · `GarantiasAlerta` `40000259:6030` (toast bottom)
- Calidad: 0 hex sueltos. Pendiente: cableado reactions (tarea futura).
- **NO construido (pendiente):** Visor de fotos/galería `741:302220` — modal 983×717, "AMORTIGUADOR DELANTERO (GAS) / Imágenes almacenadas / 2 de 3" — modal-documento con imagen de producto.
- **Relación trigger→overlay:**
  - Botón ojo (eye) por fila → `GarantiasVerDetalle`
  - "Continuar con garantía" → `GarantiasAplicar`
  - "Aplicar garantía" → `GarantiasAlerta` (toast auto-dismiss)
  - ✕ / Cerrar / Regresar → CLOSE overlay

### NEW_05 Consultas — Overlays tab CRÉDITOS: MásOpciones + AbonarPagar + EnviarCorreo + AbonoConfirmar (12 overlays)
Todos en `NEW_05 Consultas`, fila y=4500 (Desktop/Mobile) y y=6050 (Tablet):
- Desktop: `CreditosMasOpciones` `40000234:4577` · `CreditosAbonarPagar` `40000235:4658` · `CreditosEnviarCorreo` `40000236:4592` · `CreditosAbonoConfirmar` `40000236:4628`
- Tablet: `CreditosMasOpciones` `40000234:4599` · `CreditosAbonarPagar` `40000235:4741` · `CreditosEnviarCorreo` `40000236:4609` · `CreditosAbonoConfirmar` `40000236:4635`
- Mobile: `CreditosMasOpciones` `40000234:4621` (BS-336) · `CreditosAbonarPagar` `40000235:4743` (BS-928) · `CreditosEnviarCorreo` `40000236:4626` · `CreditosAbonoConfirmar` `40000236:4642`
- Calidad: 0 hex sueltos. Pendiente: cableado reactions + íconos lucide reales en chips.
- **Pendiente:** Modal de comprobante/ticket con QR — NO construido en esta tarea.
- **Análisis CLIENTE (para tarea futura):**
  - `741:331139` (CLIENTE MÁS OPCIONES): 6 acciones — Ticket, Imprimir, Enviar correo, Descargar pdf, Cancelar venta, Editar venta. DIFIERE del menú de Crédito (no tiene "Abonar/Pagar"; tiene "Ticket" y "Cancelar venta" que crédito no tiene). NO reutiliza los overlays de crédito — requiere overlays propios.
  - `741:316692` (CLIENTE ABONAR/PAGAR): misma cadena de modales que crédito regular. Los overlays de crédito `CreditosAbonarPagar` SERÍA reutilizable para el flujo de cliente, aunque el trigger es diferente.
  - Modal "Enviar correo" del cliente = idéntico al de crédito (mismo texto). PUEDE reusar `CreditosEnviarCorreo`.
  - Modal "Cancelar venta" del cliente: 374px, badge CONFIRMAR, texto "¿Estás seguro de que deseas cancelar la venta?", btns "No" / "Cancelar venta" (destructivo). Es diferente del de Ventas.

### NEW_05 Consultas — Overlays "Más opciones" tab VENTAS (12 overlays)
Todos en `NEW_05 Consultas`, fila y≈1200–1600 junto a las pantallas de Ventas:
- Desktop: `VentasMasOpciones` `40000213:5924` · `VentasEnviarCorreo` `40000216:5940` · `VentasCancelarVenta` `40000216:5957` · `VentasCrearGarantia` `40000217:5972`
- Tablet: `VentasMasOpciones` `40000218:5946` · `VentasEnviarCorreo` `40000218:5963` · `VentasCancelarVenta` `40000218:5980` · `VentasCrearGarantia` `40000219:5960`
- Mobile: `VentasMasOpciones` `40000220:5958` (bottom-sheet) · `VentasEnviarCorreo` `40000221:5940` · `VentasCancelarVenta` `40000221:5957` · `VentasCrearGarantia` `40000222:5964` (bottom-sheet formulario)
- Calidad: 0 hex sueltos. Pendiente: cableado reactions + íconos lucide reales en menú.

### Inicio (MAIN) — Drill-down por Marca / CARD AUTOS (en `NEW_02 Inicio`)
Sub-pantalla que aparece tras clic en una "Card marca". 3 breakpoints en `NEW_02 Inicio` (`40000110:4579`), fila y=1500:
- `Screen/Inicio_02_Autos--Desktop` `40000141:91080` — clon 1:1 de `728:84793` (Banner+4-col grid+sidebar)
- `Screen/Inicio_02_Autos--Tablet` `40000142:6202` — 3-col grid, rescale proporcional
- `Screen/Inicio_02_Autos--Mobile` `40000143:6617` — 2-col grid, Pagination--Mobile
**Pendiente:** sidebar filtros Mobile (ocultar en Mobile, mostrar como sheet); Tablet Navbar→instancia correcta.

### Inicio (MAIN) — Home catálogo "Autopartes" (en `04_Claude_Sandbox`)
Fuente Desktop: `539:44895`. Generados: `Mobile - Inicio_01_Home` `40000047:4577` · `Tablet - Inicio_01_Home`
`40000051:4594` · `Drawer/Nav` `40000047:4686`. Transforms: navbar→hamburguesa+drawer, grid 5→3(tablet)/2(mobile),
buscador Input, chips wrap, paginación simplificada. Prototipo: hamburguesa→drawer (overlay) + ✕ cierra
(posición/animación del overlay se ajustan a mano — API read-only).
UX review aplicado (fixes): nombres 14px, SKU legible (`text/secondary` + `Label/Small` a 12px),
chips 44/40 (touch), filas/nav-items a Fill. Componentes agregados: `NavItem` (Default/Active/Hover),
`ProductGrid/Empty`, `ProductGrid/Loading`. **Pendiente:** íconos nav como botones semánticos + label del buscador;
aplicar `NavItem`/estados en las pantallas; conectar nav items del drawer a módulos; resto de pantallas del módulo Inicio.

## Orden sugerido
1. **Fase 0 — fundaciones** (tokens color + tipografía) antes de responsivar en serie.
2. **Login** (más chico, valida el flujo end-to-end: homologar → responsivar → UX → prototipar).
3. **Inicio (MAIN)** (patrón sidebar + tabla → cards; define la mayoría de transforms).
4. Resto de módulos, uno por uno.

## Progreso global
- Módulos: **10** · Fundaciones: `Breakpoints` ✅, tokens color/tipografía pendientes.
- Homologados: 0 · Tablet: 0 · Mobile: 0 · UX: 0 · Prototipo: 0

> El desglose pantalla-por-pantalla dentro de cada módulo se documenta al empezar ese módulo.
