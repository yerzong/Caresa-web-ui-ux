# Mapa del Proyecto — CARESA WEB UI 2026

Inventario real y checklist de avance. La app **Desktop ya existe** por módulos (ver `FIGMA_ANALYSIS.md`).
Objetivo por pantalla: existir en **Desktop (fuente) → Tablet (834) → Mobile (393)**, homologada y con UI/UX + prototipo.

## Leyenda
- `[ ]` pendiente · `[~]` en progreso/sandbox · `[x]` aprobado y movido a página final
- Columnas por módulo: `Homologada | Tablet | Mobile | UX ✔ | Prototipo`

> ⚠️ Cada módulo es un **board con varias pantallas**. El desglose pantalla-por-pantalla se
> completa con una pasada de `figma-auditor`/`responsive-architect` por módulo (tarea atómica).

---

## REMAKE v2 (2026-09-18) — misión vigente
Remake desde cero en páginas nuevas (`CARESA v2 — Design System` + `CARESA Web Responsive`), base Untitled UI recreada localmente. Breakpoints v2: **1440 / 768 / 375**.

| Fase | Contenido | Estado |
|---|---|---|
| 1 | Design System (tokens, tipografía, iconos, 12 sets de componentes) | [x] construido 2026-09-18 |
| 2 | Login (2 propuestas) | [x] aprobada Propuesta B (2026-09-18) |
| 3 | Pantallas Web | [x] **COMPLETA 2026-09-19** — Login B · Inicio · Carrito · Catálogos · Consultas (Ventas/Créditos/Garantías) · Corte (Apertura caja) · Pedidos (+Ver pedido) · Chat · Abonos · Recompra |
| 4 | Tablet | [x] **COMPLETA 2026-09-19** — 12 pantallas (faltan solo overlays secundarios) |
| 5 | Mobile | [ ] |

IDs clave: página DS `40000379:4577` · Button `40000386:4768` · Input `40000388:4673` · Modal `40000391:4704` · Overlay `40000391:4705` · Ledger: `~/.claude/jobs/a9d428d9/tmp/ds-state.json`

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
| 5 | Consultas | `5 Consultas` (`13:104`) | [~] | [x] | [x] | [ ] | [x] |
| 6 | Corte de caja | `6 Corte de caja` (`595:70899`) | [ ] | [ ] | [ ] | [ ] | [ ] |
| 7 | Pedidos | `7 Pedidos` (`681:51807`) | [~] | [~] | [~] | [ ] | [x] |
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
- Calidad: 0 hex sueltos. Reactions cableadas (2026-09-18): NAVIGATE DISSOLVE 250ms EASE_OUT en los 3 breakpoints.
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
- Calidad: 0 hex sueltos. Reactions cableadas (2026-09-18): NAVIGATE DISSOLVE 250ms EASE_OUT en los 3 breakpoints.
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

### NEW_07 Pedidos — Pantalla Lista (en `NEW_07 Pedidos`)
Fuente Desktop: `681:53064` (1728×1330). 3 breakpoints. Corregidos con datos reales 2026-09-16:
- `Screen/Pedidos_01_Lista--Desktop` `40000270:4592` — 1728×1322, fila y=0
- `Screen/Pedidos_01_Lista--Tablet` `40000271:4746` — 834×1457, x=1808 y=0
- `Screen/Pedidos_01_Lista--Mobile` `40000272:4901` — 393×1484, x=2722 y=0
Datos reales: 5 stat cards fiel · 7 filas tabla exactas · 8 columnas reales · badges Sin confirmar/Surtiendo/Listo para enviar/Enviado · Vendedores --- / Omar Edrey · Total $ 3,330.00 todas · Paginación "50 Pedidos / Página 1 de X".
Transforms: Desktop→tabla 8 cols; Tablet→tabla 5 cols (Cliente|No. orden|Estado|Total|Acciones)+wrap stat cards 2×3; Mobile→7 order-cards apiladas+stat 2×3.
Pulido 2026-09-16: iconos de accion reales (clones de `683:4566`), botones Confirmar/Cancelar outline reales, 7a card Mobile agregada (Enviado, 1744px). Mobile height ajustada a 1744px.
Pendiente: prototipo, tokens color estado-badge (sin token disponible), reactions.

### NEW_07 Pedidos — Overlays "Ver pedido" (detalle) — 3 breakpoints base + 3 variantes de estado
Fuente original: modal `741:360120` (dentro de `683:22188` → sección `683:22187`). Todos en `NEW_07 Pedidos`, fila y=2000:
- Desktop: `Overlay/PedidoVerDetalle--Desktop` `40000283:5103` (1728×1128, scrim + diálogo 1155px, 8 cols tabla)
- Tablet: `Overlay/PedidoVerDetalle--Tablet` `40000284:5103` (834×1194, scrim + diálogo 750px, 5 cols tabla, info 2 filas)
- Mobile: `Overlay/PedidoVerDetalle--Mobile` `40000285:5103` (393×1599, bottom-sheet HUG, tabla→cards, botones full-width)
Logos clonados por imageHash: SYD · BOSCH · MOOG · SACHS. Importe total: $10,194.50. 0 hex nuevos.
**Variante Listo para Enviar** (y=12500): Desktop `40000341:5103` · Tablet `40000341:5271` · Mobile `40000341:5419` — badge azul, vendedor Gerson Garcia, bloque Hora/Tiempo, btn Enviar este pedido.
**Variante Cancelado** (y=13800): Desktop `40000342:5103` · Tablet `40000342:5265` · Mobile `40000342:5407` — badge rojo, bloque Motivos cancelacion, footer vacío.
**Variante Completado** (y=15100): Desktop `40000343:5103` (1728×1501) · Tablet `40000343:27105` (834×1526) · Mobile `40000343:27298` (393×2279) — badge verde, Hora/Tiempo+URL+Repartidor+Opciones impresión+Firmas clonadas, btn Imprimir.
Imágenes firma/foto: clonadas de `741:377164` (firma vector) y `741:377172`→`741:377179` (foto imageHash `b93f4e9bf67c2f023c3b1cf91a79001cfba2291e`).
Pendiente: prototipo (trigger ojo → overlay por estado, X → close).

### NEW_07 Pedidos — Overlays "Enviar pedido" (confirmación de envío) — 3 breakpoints
Fuente original: modal `741:366090` (dentro de `736:113986` "Confirmar", página `7 Pedidos`). Todos en `NEW_07 Pedidos`, fila y=4400:
- Desktop: `Overlay/PedidoEnviar--Desktop` `40000298:5103` (1728×1128, scrim + diálogo 1254px, tabla 6 cols, opciones en fila)
- Tablet: `Overlay/PedidoEnviar--Tablet` `40000299:5103` (834×834, scrim + diálogo 770px, info 2 filas×3 cols)
- Mobile: `Overlay/PedidoEnviar--Mobile` `40000301:5103` (393×775, bottom-sheet HUG, info lista 7 rows, dropdown full-width, opciones apiladas, botón full-width)
Contenido verbatim: badge "Enviar pedido" (negro/lima) · título "Estas a punto..." · fila-resumen 6 cols · dropdown repartidor · radio×2 + toggle · botón Enviar pedido lima.
0 hex sueltos. Touch ≥ 44px Mobile. Pendiente: prototipo (trigger "Enviar" → overlay, ✕ → close).

### NEW_07 Pedidos — Overlays "Selección múltiple": ConfirmarSeleccionados + CancelarSeleccionados — 3 breakpoints c/u
Fuente original: sección `683:6400` ("Seleccion multiple", página `7 Pedidos`). Frames: `733:47734` (VERDE "Confrimar multiple") y `733:46340` (ROJO "Cancelar multiple"). Todos en `NEW_07 Pedidos`, posición y=9400 (Confirmar) / y=11000 (Cancelar):
- CONFIRMAR: Desktop `40000329:5103` · Tablet `40000331:5103` · Mobile `40000332:5103` (bottom-sheet 393×958)
- CANCELAR: Desktop `40000330:5103` · Tablet `40000331:5190` · Mobile `40000332:5215` (bottom-sheet 393×1090)
Contenido verbatim: badge chip + ícono clonado + subtitle + tabla 4 cols (Cliente|No. de orden/Fecha|Total|Metodo de entrega) + 7 filas reales. Cancelar agrega textarea "Escribe el motivo de de la cancelación". Footer: Cerrar/Si,confirmar (lima) para confirmar; Cancelar/Cancelar pedidos (rojo) para cancelar. Mobile tabla→7 order-cards.
Pendiente: prototipo (triggers → overlays, ✕ → close).

### NEW_07 Pedidos — Overlays flujo Surtir: EliminarProducto + EditarCantidad + AnadirProducto — 3 breakpoints c/u
Todos en `NEW_07 Pedidos`. Posiciones: Desktop x=0 · Tablet x=1900 · Mobile x=2900.
- EliminarProducto (y=5600): `40000313:5103` (D) · `40000313:5122` (T) · `40000313:5141` (M 393×700)
- EditarCantidad (y=6800): `40000314:5103` (D) · `40000314:5150` (T) · `40000314:5197` (M bottom-sheet)
- AnadirProducto (y=8000): `40000315:5103` (D) · `40000315:5306` (T) · `40000315:5509` (M 393×1553)
Contenido: ver CHANGELOG 2026-09-17. Logo SACHS imageHash preservado. 0 hex nuevos en Eliminar+Editar. AnadirProducto = clon Validar + dropdown ABSOLUTE.
Pendiente: prototipo (triggers → overlays, ✕ → close).

### NEW_07 Pedidos — Overlay "Seguimiento de envío (ADMIN)" — 3 breakpoints
Fuente original: modal `683:69908` (dentro de frame `683:68953` → section `683:63949` "SEGUIMIENTO ENVIO (ADMIN", página `7 Pedidos`). Todos en `NEW_07 Pedidos`, fila y=9600:
- Desktop: `Overlay/PedidoSeguimientoEnvio--Desktop` `40000349:27000` (1728×1128, x=0) — scrim + diálogo centrado 1600×960, 2 columnas (sidebar 430px | map+info 1170px)
- Tablet: `Overlay/PedidoSeguimientoEnvio--Tablet` `40000355:5109` (834×1194, x=1900) — scrim + diálogo centrado 780×1100, 2 columnas (sidebar 280px | map+info 500px)
- Mobile: `Overlay/PedidoSeguimientoEnvio--Mobile` `40000356:5109` (393×950, x=2900) — bottom-sheet 750px, info repartidor compacto, mapa 393×280 full-width, sidebar apilado, Volver full-width 44px touch
MAP clonado (3 instancias de `683:70603`): Desktop `40000354:7525` · Tablet `40000355:7544` · Mobile `40000356:7504`
Contenido verbatim: Pedido DOC/515151/21020 · Enviado · Orden creada 01/01/26 · Repartidor David Manuel Espinoza Rodriguez · Sin salir · 00:00/20:00 · Dirección Calle Tercera Pte. Sur 366 · Comentarios puerta roja · Foto/Firma Sin capturar · Cronología 4 ítems · Info 6 cols.
0 hex nuevos en nodos propios (colores del MAP clonado son del original). Pendiente: prototipo (trigger → overlay, ✕ → close).

### NEW_07 Pedidos — Overlays "Validar pedidos" (surtir) — 3 breakpoints
Fuente original: frame `736:82992` (página `7 Pedidos`). Todos en `NEW_07 Pedidos`, fila y=3200:
- Desktop: `Overlay/PedidoValidar--Desktop` `40000289:5103` (1728×1128, scrim + diálogo 1155px, 6 cols tabla)
- Tablet: `Overlay/PedidoValidar--Tablet` `40000289:5261` (834×834, scrim + diálogo 750px, 5 cols tabla)
- Mobile: `Overlay/PedidoValidar--Mobile` `40000289:5399` (393×1553, bottom-sheet HUG, tabla→cards)
Logos clonados del Ver pedido Desktop: SYD · BOSCH · MOOG · SACHS (imageHash preservado).
Datos: 5 productos (incluyendo 8000060 Amortiguador trasero), ubicaciones reales, surtido 0/X.
Footer: "Cancelar pedido" (rojo outline) + "Validar pedido" (lima). 0 hex nuevos.
Pendiente: prototipo (trigger "Surtir" → overlay, X → close).

## Orden sugerido
1. **Fase 0 — fundaciones** (tokens color + tipografía) antes de responsivar en serie.
2. **Login** (más chico, valida el flujo end-to-end: homologar → responsivar → UX → prototipar).
3. **Inicio (MAIN)** (patrón sidebar + tabla → cards; define la mayoría de transforms).
4. Resto de módulos, uno por uno.

## Progreso global
- Módulos: **10** · Fundaciones: `Breakpoints` ✅, tokens color/tipografía pendientes.
- Homologados: 0 · Tablet: 0 · Mobile: 0 · UX: 0 · Prototipo: 0

> El desglose pantalla-por-pantalla dentro de cada módulo se documenta al empezar ese módulo.
