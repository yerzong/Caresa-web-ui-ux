# Bitácora de Cambios

Registro cronológico de todo lo que se hace en el proyecto (diseño y documentación).
Nada se pierde: cada pantalla generada, homologación o decisión se anota aquí.

Formato:
```
## [YYYY-MM-DD] — Título
- **Creado/Modificado:** ...
- **Cambios:** ...
- **Pendiente:** ...
```

---

## [2026-09-16] — NEW_05 Consultas: Overlays Garantías — VerDetalle + Aplicar + Alerta (9 overlays, 3 breakpoints)
- **Overlays de Garantías en `NEW_05 Consultas`** (fila y=7500 Desktop/Mobile · y=9000 Tablet):
  - **Desktop (1728×1422 c/u, scrim 50% + modal centrado):**
    - `Overlay/GarantiasVerDetalle--Desktop` `40000253:5948` — modal 968×892px, badge GARANTÍAS negro/lima, campos: Folio/Fecha/Doc.Asociado/Nombre de quien entrega/Factura asociada/Razón/Producto/Cantidad; tabla SKU/Descripción/U/M/Cant/P.Unitario/Importe (1 fila: 0986AF0051/QUAKER STATE M.../Unidades/S2:2/$825.00/$1,650.00); Comentarios o diagnóstico; Importe total $1,650.00; 2 placeholders foto; acciones Cerrar / Continuar con garantía (lima).
    - `Overlay/GarantiasAplicar--Desktop` `40000254:5948` — modal 518×894px, badge GARANTÍAS negro/lima, 3 pasos: (1) Input "Nombre de quien recibe" (2) Botón "Imprimir formato" (3) UploadArea "Agregar formato firmado"; acciones Aplicar garantía (lima) / Regresar.
    - `Overlay/GarantiasAlerta--Desktop` `40000254:5979` — toast 426×88px, bg oscuro (bg/inverse), check verde (semantic/success), texto "GARANTÍA APLICADA EXITOSAMENTE"; posición top.
  - **Tablet (834×1029 c/u, mismo patrón centrado):**
    - `Overlay/GarantiasVerDetalle--Tablet` `40000257:5948` — modal 770×820px, misma estructura 2 cols.
    - `Overlay/GarantiasAplicar--Tablet` `40000257:6017` — modal 460×760px, 3 pasos.
    - `Overlay/GarantiasAlerta--Tablet` `40000257:6048` — toast 380×72px, top.
  - **Mobile (393×852 c/u):**
    - `Overlay/GarantiasVerDetalle--Mobile` `40000259:5948` — **bottom-sheet** 780px alto, radius top 16px, drag handle, campos en 1 col, footer: Continuar con garantía (fill lima, 44px) / Cerrar (fill bg, 40px).
    - `Overlay/GarantiasAplicar--Mobile` `40000259:5997` — **bottom-sheet** 600px alto, drag handle, 3 pasos apilados, footer: Aplicar garantía (fill 44px) / Regresar (fill 40px).
    - `Overlay/GarantiasAlerta--Mobile` `40000259:6030` — toast 377×72px posición bottom (safe area 24px), bg oscuro, check verde.
- **Análisis de la cadena original de Garantías (páginas `5 Consultas`, sección `741:292446`):**
  - La cadena original NO tiene popover "Más opciones" → flujo directo: botón ojo → modal "Ver garantía" → "Continuar con garantía" → modal "Aplicar garantía" → toast de confirmación.
  - Campos reales extraídos del modal original `741:294453`: Folio #140532854, Fecha 14/05/2026, Doc. Asociado DOC/2026/79210840-4724, Nombre de quien entrega VICTOR ESPINOSA, Factura asociada No encontrado, Razón Defecto de fabricación, Producto ACEITE MOTOR MINERAL 10W30 G..., Cantidad 2, SKU 0986AF0051, U/M Unidades, P.Unitario $825.00, Importe $1,650.00, Comentarios "Venía roto el sello de seguridad".
  - Modal "Aplicar garantía" `741:297964`: 3 pasos — (1) Nombre de quien recibe, (2) Imprimir formato, (3) Agregar formato firmado; acciones Regresar / Aplicar garantía.
  - Toast `741:302219`: "GARANTÍA APLICADA EXITOSAMENTE" 426×88px (componente `Alerts`).
- **Calidad:** 0 hex sueltos (auditado 2 pasadas — 44 paints con #D0D5DD/#12B76A/#FFFFFF religados a variables border/default / semantic/success / base/white).
- **Touch target Mobile:** botones footer ≥40px (Cerrar 40, Continuar 44, Aplicar 44, Regresar 40) — Regresar ≥ mínimo aceptable.
- **Posicionamiento:** Desktop x=0/1900/3800 y=7500 · Tablet x=0/950/1900 y=9000 · Mobile x=3900/4400/4900 y=7500.
- **Pendiente:** cableado de reactions (tarea posterior). Visor de fotos/galería (modal 983×717px, "AMORTIGUADOR DELANTERO (GAS) / Imágenes almacenadas / 2 de 3") — modal-documento con imagen, NO construido.
- **Relación trigger→overlay para cableado posterior:**
  - Botón ojo (eye icon) por fila → `GarantiasVerDetalle` del mismo breakpoint.
  - "Continuar con garantía" → `GarantiasAplicar` del mismo breakpoint.
  - "Aplicar garantía" → `GarantiasAlerta` del mismo breakpoint (toast, dismiss automático).
  - ✕ / "Cerrar" / "Regresar" → CLOSE.

---

## [2026-09-16] — NEW_05 Consultas: Overlays Créditos — MásOpciones + AbonarPagar + EnviarCorreo + AbonoConfirmar (12 overlays, 3 breakpoints)
- **Overlays de Créditos en `NEW_05 Consultas`** (fila y=4500 Desktop/Mobile · y=6050 Tablet):
  - **Desktop (1728×1422):**
    - `Overlay/CreditosMasOpciones--Desktop` `40000234:4577` — popover 271px, 4 acciones con chips de color: Imprimir, Enviar correo, Descargar pdf, Abonar / Pagar.
    - `Overlay/CreditosAbonarPagar--Desktop` `40000235:4658` — modal 1069px, badge CRÉDITOS negro/lima, tabla docs pendientes (Documento/Importe/D-B/Abonos/Total/Saldo), campos de pago (Recibo cobranza, Fecha, Forma de pago, Abono total, Saldo a favor, Banco, Concepto de pago, Ext. Doc. De pago), acciones Cerrar/Abonar lima.
    - `Overlay/CreditosEnviarCorreo--Desktop` `40000236:4592` — diálogo 600px, badge CONFIRMAR, cuerpo con email, btn "Enviar correo" lima.
    - `Overlay/CreditosAbonoConfirmar--Desktop` `40000236:4628` — toast 355×72px, dark bg, check verde, "SE ABONÓ CORRECTAMENTE / Orden de venta creada".
  - **Tablet (834×1029):**
    - `Overlay/CreditosMasOpciones--Tablet` `40000234:4599` — popover 260px, misma estructura.
    - `Overlay/CreditosAbonarPagar--Tablet` `40000235:4741` — modal 720px, 2 cols.
    - `Overlay/CreditosEnviarCorreo--Tablet` `40000236:4609` — diálogo 560px.
    - `Overlay/CreditosAbonoConfirmar--Tablet` `40000236:4635` — toast 320×64px.
  - **Mobile (393×2620):**
    - `Overlay/CreditosMasOpciones--Mobile` `40000234:4621` — bottom-sheet 336px, drag handle, 4 filas ≥56px.
    - `Overlay/CreditosAbonarPagar--Mobile` `40000235:4743` — bottom-sheet 928px (scroll), tabla docs + 8 campos + Abonar 44px / Cerrar.
    - `Overlay/CreditosEnviarCorreo--Mobile` `40000236:4626` — diálogo centrado 350px.
    - `Overlay/CreditosAbonoConfirmar--Mobile` `40000236:4642` — toast 361px fondo, posición bottom.
- **Acciones reales del menú Créditos (verificadas 1:1 vs `741:302256`):** Imprimir · Enviar correo · Descargar pdf · Abonar / Pagar.
- **Cadena modal Abonar/Pagar (verificada vs `741:303305`, 6 modales en original):** 1 modal consolidado con: tabla de documentos pendientes (Documento/Importe/D-B/Abonos/Total/Saldo/Relación + btn Liquidar todo) + formulario (Recibo cobranza, Fecha de pago, Forma de pago, Abono total, Saldo a favor, Banco, Concepto de pago, Ext. Doc. De pago) + acciones Cerrar / Abonar. Toast "SE ABONÓ CORRECTAMENTE" como confirmación final (no modal, igual al original).
- **Calidad:** 0 hex sueltos (auditado — 20 hexes presentes, todos en mapa de tokens del proyecto).
- **Chips de ícono de color:** Imprimir `#EBF1FF/#1760D4` · Enviar correo `#FFF6ED/#C4320A` · Descargar pdf `#F9F5FF/#6941C6` · Abonar/Pagar `#ECFDF3/#12B76A` — mismo status que chips Ventas (sin token exacto en colección Color, pendiente tokenización).
- **Posicionamiento:** Desktop y=4500 (x=0/1900/3800/5700) · Tablet y=6050 (x=0/950/1900/2850) · Mobile y=4500 (x=3900/4400/4900/5400).
- **Pendiente:** cableado de reactions (tarea posterior). Comprobante/ticket con QR (modal complejo, pospuesto).
- **NOTA CLIENTE:** `741:331139` y `741:316692` son flujos CLIENTE (diferente al de crédito directo). Ver nota en PROJECT_MAP.

---

## [2026-09-16] — NEW_05 Consultas: Overlays "Más opciones" tab VENTAS (12 frames, 3 breakpoints)
- **Overlays en `NEW_05 Consultas`** (colocados en y≈1200–1600, junto a las pantallas de Ventas):
  - **Desktop (1728×1422 c/u, scrim 50% + diálogo/popover centrado):**
    - `Overlay/VentasMasOpciones--Desktop` `40000213:5924` — popover 271px, 7 acciones: Ticket, Imprimir, Enviar correo, Descargar pdf, Cancelar venta, Editar venta, Garantía.
    - `Overlay/VentasEnviarCorreo--Desktop` `40000216:5940` — diálogo 600px, badge CONFIRMAR negro/lima, body con email, btn "Enviar correo" lima.
    - `Overlay/VentasCancelarVenta--Desktop` `40000216:5957` — diálogo 420px, badge rojo destructivo, btn "Cancelar venta" rojo.
    - `Overlay/VentasCrearGarantia--Desktop` `40000217:5972` — diálogo 968px formulario: tabla info venta (Folio/Fecha/Doc/Entrega), selects Razón/Producto/Cantidad, Textarea, Importe+fotos, acciones Cerrar/Crear garantía.
  - **Tablet (834×1029 c/u, misma estructura centrada):**
    - `Overlay/VentasMasOpciones--Tablet` `40000218:5946`
    - `Overlay/VentasEnviarCorreo--Tablet` `40000218:5963`
    - `Overlay/VentasCancelarVenta--Tablet` `40000218:5980`
    - `Overlay/VentasCrearGarantia--Tablet` `40000219:5960`
  - **Mobile (393×2620 c/u):**
    - `Overlay/VentasMasOpciones--Mobile` `40000220:5958` — **bottom-sheet** con drag handle, título, 7 filas táctiles ≥56px, separadores.
    - `Overlay/VentasEnviarCorreo--Mobile` `40000221:5940` — diálogo centrado 350px, botones 44px.
    - `Overlay/VentasCancelarVenta--Mobile` `40000221:5957` — diálogo centrado 340px, destructivo.
    - `Overlay/VentasCrearGarantia--Mobile` `40000222:5964` — **bottom-sheet formulario** con campos apilados (Razón/Producto/Cantidad/Comentarios/Importe).
- **Calidad:** 0 hex sueltos (auditado 2 pasadas — 58 paints corregidos + 6 blancos; todos los colores vía colección `Color`).
- **Cómo conectar (para prototipado posterior):** trigger = botón ⋮ `more-vertical` por fila de la tabla (ej. Desktop: `40000187:7940`). Interacción ON_CLICK → overlay del mismo breakpoint con DISSOLVE. ✕ → CLOSE. Desde el menú, cada acción → overlay correspondiente.
- **Acciones del original verificadas 1:1** contra `741:284629` (popover fuente).
- **Pendiente:** cableado de reactions (tarea posterior). ~~íconos lucide reales~~ → RESUELTO (ver entrada 2026-09-16 abajo).

---

## [2026-09-16] — NEW_05 Ventas: Fidelidad íconos "Más opciones" en 3 overlays
- **Alcance:** reemplazar placeholders de ícono en los 3 overlays Ventas `MasOpciones` (Desktop/Tablet/Mobile).
- **Fuente clonada:** `741:284629` (página `5 Consultas` — menú original).
- **Chips construidos (clones de `_Button base` + ícono lucide):**
  1. Ticket — bg `#FAFAFA` (≈ Gray/50), border `#181D27` (≈ Gray/900), ícono `lucide/receipt`
  2. Imprimir — bg `#EBF1FF` (azul muy claro), border `#1760D4` (azul), ícono compuesto (SVG del original)
  3. Enviar correo — bg `#FFF6ED`, border `#C4320A` (naranja), ícono `lucide/at-sign`
  4. Descargar pdf — bg `#F9F5FF`, border `#6941C6` (morado), ícono `download`
  5. Cancelar venta — bg `#FEE8E7`, border `#D92D20` = `VariableID:130:19265` (`False-Default`), ícono `lucide/ticket-x`
  6. Editar venta — bg `#FFF1F3` (≈ Rosé/50), border `#E31B54` (≈ Rosé/600), ícono `edit`
  7. Garantía — bg `#F0F9FF` (≈ Blue light/50), border `#0086C9` (≈ Blue light/600), ícono `file-text`
- **Texto "Cancelar venta":** corregido de `semantic/danger` (#F54900) → fill estático `#101828` (text/primary) en Desktop `40000213:5940`, Tablet `40000218:5939`, Mobile `40000220:5948`.
- **Nodos Icon mutados (Desktop / Tablet / Mobile):**
  - Ticket: `40000213:5927` / `40000218:5926` / `40000220:5931`
  - Imprimir: `40000213:5930` / `40000218:5929` / `40000220:5935`
  - Enviar correo: `40000213:5933` / `40000218:5932` / `40000220:5939`
  - Descargar pdf: `40000213:5936` / `40000218:5935` / `40000220:5943`
  - Cancelar venta: `40000213:5939` / `40000218:5938` / `40000220:5947`
  - Editar venta: `40000213:5942` / `40000218:5941` / `40000220:5951`
  - Garantía: `40000213:5945` / `40000218:5944` / `40000220:5955`
- **Chips clonados IDs (Desktop):** `40000226:4577..4597`; Tablet: `40000226:4600..4617`; Mobile: `40000226:4620..4637`.
- **Auditoría hex:** Los chips heredan los hex del nodo fuente original (`5 Consultas`) que NO está tokenizado. 6 de 7 colores tienen equivalente exacto en la colección `Color` (Cancelar venta usa `VariableID:130:19265` `False-Default`). Colores del chip de Imprimir no tienen token en la colección `Color` (azul distinto a `semantic/info`). Reportado — tokenización pendiente cuando se tokenice `5 Consultas`.
- **Auto Layout:** preservado — chips son frames 20×20 (Desktop/Tablet) y 24×24 (Mobile) dentro de los Icon frames existentes.
- **Touch target:** filas Desktop/Tablet ≥44px; Mobile ≥56px — sin cambios.

---

## [2026-09-16] — NEW_05 Consultas: modales de los 3 tabs (Ventas + Créditos + Garantías) en 3 breakpoints
Construidos como overlays en `NEW_05 Consultas`, patrón: Desktop/Tablet = diálogo/popover centrado con scrim; Mobile = bottom-sheet (menús/formularios) o diálogo (confirmaciones). Todos verificados por screenshot.
- **VENTAS** (original `741:282662`): menú Más opciones (7 acciones con chips de ícono de color clonados del original + etiquetas negras) `Overlay/VentasMasOpciones--{D `40000213:5924`/T `40000218:5946`/M `40000220:5958`}`; confirmaciones `VentasEnviarCorreo--{D `40000216:5940`}`, `VentasCancelarVenta--{D `40000216:5957`}`; formulario `VentasCrearGarantia--{D `40000217:5972`}`.
- **CRÉDITOS** (originales `741:302256`, `741:303305`): menú 4 acciones `CreditosMasOpciones--{D `40000234:4577`/T `40000234:4599`/M `40000234:4621`}`; modal **Abonar y pagar** (tabla documentos + Liquidar todo + formulario 2 columnas: Recibo/Fecha/Forma de pago/Abono total/Saldo a favor/Banco/Concepto/Ext.Doc. + footer Cerrar/Abonar) `CreditosAbonarPagar--{D `40000235:4658`/T `40000235:4741`/M `40000235:4743`}`; `CreditosEnviarCorreo--{D `40000236:4592`}`; toast `CreditosAbonoConfirmar--{D `40000236:4628`}`.
- **GARANTÍAS** (originales `741:293432`…`741:302219`): `GarantiasVerDetalle--{D `40000253:5948`/T `40000257:5948`/M `40000259:5948`}` (info 2 columnas + tabla de línea + comentarios + importe total + evidencias); `GarantiasAplicar--{D `40000254:5948`}` (3 pasos: nombre / imprimir formato / subir firmado); toast `GarantiasAlerta--{D `40000254:5979`}` ("GARANTÍA APLICADA EXITOSAMENTE").
- **Fixes míos post-agente:** los 3 agentes reintrodujeron el bug de contenedores Auto Layout con altura FIXED mínima (recorte total del contenido). Pase de reparación genérico aplicado: Ventas menús (3), Créditos (39 contenedores) + rearmado del formulario Abonar (FormRows horizontales `counterAxis=AUTO`) y del footer (auto-layout derecha, botones HUG), Garantías (11 contenedores incl. los frames Modal). Verificado por screenshot en los 3 breakpoints.
- **Deuda técnica (registrada, no bloqueante):** varios overlays usan frames/inputs/botones a mano en vez de instancias estrictas de `NEW_00` (sobre todo bottom-sheets Mobile con posición absoluta); chips de ícono con algunos hex sin token exacto (mismo caso del original sin tokenizar). Religar a instancias/tokens en pasada de QA.
- **Pendiente del módulo:** cablear prototipo de estos overlays (Fase 4); Cliente–Más opciones de Créditos (reusa EnviarCorreo/AbonarPagar; falta su menú de 6 acciones + Cancelar venta); modales-documento no construidos (vista previa de comprobante Ventas/Créditos con ticket+QR, y visor de galería de fotos de Garantías `741:302220`).

---

## [2026-09-16] — NEW_05 Consultas COMPLETO: Créditos + Garantías (6 screens)
- **Créditos** (original `741:328204`): `--Desktop` `40000195:24970` · `--Tablet` `40000198:5812` (6 col, sin traslapes)
  · `--Mobile` `40000202:5858` (cards). **Garantías** (original `741:292447`): `--Desktop` `40000195:97202` ·
  `--Tablet` `40000203:5868` · `--Mobile` `40000204:5914` (cards #folio/proveedor/importe/estado + Ver detalle).
- **Calidad:** 0 hex sueltos (auditado — el agente aplicó tokens exactos a la primera); sin traslapes ni miniaturas.
- **Prototipo:** 18 reactions de tabs (Ventas↔Créditos↔Garantías × 3 breakpoints) + 3 flow starting points.
- **Pendiente del módulo:** modales de más opciones/abonar-pagar (cadenas de FLOWS).

---

## [2026-09-16] — NEW_05 Consultas: Ventas fiel en 3 breakpoints
- **Original:** `741:289084` (MB-67). **Screens** en `NEW_05 Consultas`: `--Desktop` `40000187:6985` (clon 1:1:
  tabs Ventas/Créditos/Garantías, tabla 8 columnas con datos reales, paginación), `--Tablet` `40000190:5057`
  (6 columnas esenciales, sin traslapes), `--Mobile` `40000191:5128` (**tabla→cards**: folio + badge estado + ⋮,
  filas label:valor, "Ver detalle", filtros apilados, paginación móvil).
- **Tokenización:** 401 colores religados (210 estándar + 191 "casi-token" off-by-one: #E3E3DE→border/default,
  #6B6E73→text/secondary, #006B00→semantic/success, #E0FFE4→green-subtle).
- **Pendiente del módulo:** Créditos y Garantías (tabs), modales de más opciones/abonar-pagar; navbar activo "Consultas".

---

## [2026-09-16] — NEW_03 Carrito: modal "Más opciones" + prototipo del módulo
- **Overlays** (base real `327:91203`): `Overlay/CarritoOpciones--Desktop` `40000180:5017` (diálogo centrado con scrim,
  6 acciones reales: Guardar/Cargar cotización, Limpiar carrito, Enviar correo, Imprimir, Descargar PDF) y
  `--Mobile` `40000181:5017` (**bottom-sheet** con drag handle, filas touch 56px, safe area).
- **Prototipo:** "Más opciones" → overlay (Desktop/Tablet→diálogo, Mobile→sheet, DISSOLVE) · ✕ → CLOSE ·
  3 flow starting points. Nota: `CLOSE_ON_CLICK_OUTSIDE` se activa a mano (API read-only).
- **Pendiente del módulo:** modal confirmar eliminar (`643:86508`), venta rápida; íconos reales en filas del modal.

---

## [2026-09-16] — NEW_03 Carrito: pantalla principal fiel en 3 breakpoints
- **Original:** `322:12443` (hub del flujo, tabla 2 productos reales + sidebar totales $7,485.00).
- **Screens** en `NEW_03 Carrito`: `--Desktop` `40000172:5324` (clon 1:1), `--Tablet` `40000172:95351`
  (tabla 4 columnas esenciales + sidebar), `--Mobile` `40000172:96503` (**tabla→cards apiladas** con datos reales +
  resumen + Vender full-width + Imprimir/Más opciones).
- **Fixes míos post-agente (Tablet):** columnas encimadas → ocultas U/M y P.Unitario (por índice — regex "UM" matcheaba
  "Column"), celdas Cantidad simplificadas (sin stepper −/+, qty centrada), clip en celdas.
- **Pendiente del módulo:** modales de acciones (más opciones/eliminar), variantes venta rápida; religar hex del sidebar tablet.

---

## [2026-09-16] — NEW_02 Inicio: Perfil en 3 breakpoints (fila 4) + cableado
- **Desktop** `Screen/Inicio_04_Perfil--Desktop` `40000165:29444`: clon 1:1 del original `768:70945` (dropdown de
  avatar abierto: Gerson Yahir / gerson@caresa.com / Administrador / Configuración / Cerrar sesión).
- **Corrección de método:** el agente entregó Tablet/Mobile como **miniaturas reescaladas ilegibles** (violaba
  responsive) → eliminadas y rehechas: Perfil--Tablet `40000170:8586` y --Mobile `40000170:8650` = **Home del
  breakpoint + dropdown real a tamaño nativo** como overlay deliberado (mismo patrón de estado que el original).
- **Prototipo:** avatar (Desktop) e ícono derecho del navbar (Tablet/Mobile) → Perfil; regreso via navegación previa.
- NEW_02 queda con 4 pantallas × 3 breakpoints + drawer + dropdowns, todo navegable.

---

## [2026-09-16] — NEW_02 Inicio: Filtro Manual fiel en 3 breakpoints + cableado
- **Screens** (fila 3, y=3900): `Screen/Inicio_03_FiltroManual--Desktop` `40000161:30236` (base real MB-27 `435:23969`,
  estado 5/5 sintetizado con variantes reales: Card filtros `selected`, BUSCAR `active`, progreso `5-5`; valores
  Chevrolet/Aveo/LT/2019/Suspensión + grid de modelos AVEO), `--Tablet` `40000161:93517` (filtros 3+2, grid abajo),
  `--Mobile` `40000161:93966` (5 filtros apilados FILL + progreso + BUSCAR full-width + Limpiar/VIN/SKU).
- **Prototipo:** BUSCAR → `Inicio_02_Autos` del mismo breakpoint (3 reactions).
- **Pendiente del módulo:** perfil; promociones/categorías (tabs).

---

## [2026-09-16] — NEW_02 Inicio: prototipo navegable
- **Cableado** (reactions ON_CLICK): 20 `Card marca` → `Inicio_02_Autos` del mismo breakpoint (10 Desktop, 6 Tablet,
  4 Mobile, Smart Animate); `arrow-left` del Autos Mobile → BACK; hamburguesa del Navbar--Mobile → **Drawer overlay**
  (instancia nueva `Overlay/Drawer--Nav` `40000159:7138`, DISSOLVE); ✕ → CLOSE; NavItem "Inicio" → Home Mobile.
- **Flow starting points**: Inicio Desktop / Tablet / Mobile.
- **Pendiente del módulo:** cadena de filtro manual (MB-18→21), perfil, promociones/categorías.

---

## [2026-09-15] — NEW_02 Inicio: Drill-down por marca (CARD AUTOS) en 3 breakpoints

- **Screens** en `NEW_02 Inicio` (página `40000110:4579`), ubicadas en fila y=1500 debajo de los Home:
  - `Screen/Inicio_02_Autos--Desktop` `40000141:91080` (x=0, w=1728): clon 1:1 del original `728:84793`
    ("MacBook Pro 16" - 60" en sección AUTOPARTES) — Banner real `470:45555`, subnav/breadcrumb,
    título "Aveo · Base · 2026,2025 / Chevrolet · 147 refacciones", filtros activos, grid 4-col CARD AUTOS,
    sidebar de filtros, paginación. Fidelidad total.
  - `Screen/Inicio_02_Autos--Tablet` `40000142:6202` (x=1800, w=834): Navbar--Tablet (instancia `40000123:5150`),
    mismo contenido; grid 3-col cards reescaladas proporcionalmente con `rescale(factor=0.621)`.
  - `Screen/Inicio_02_Autos--Mobile` `40000143:6617` (x=3700, w=393): Navbar--Mobile (instancia `40000123:90933`),
    "← RESULTADOS DE BÚSQUEDA", título+subtítulo, badge MARCA Chevrolet, grid 2-col cards `rescale(0.431)`,
    Pagination--Mobile clonada del Home mobile.
- **Original de referencia:** frame `728:84793` en página `4:2` sección `462:37459`.
- **Cards:** 8 instancias "Container" clonadas del original con `.clone()` + `.rescale()` proporcional —
  NUNCA `resize()` que distorsiona. Colores/textos reales del original (0 lorem).
- **Pendiente:** sidebar de filtros del Mobile no oculta (se hereda del clone — a refinar en iteración);
  Tablet Navbar es `symbol` no `instance` (pendiente swap al componente correcto).

---

## [2026-09-15] — NEW_02 Inicio: Home fiel en 3 breakpoints
- **Screens** en `NEW_02 Inicio`: `Screen/Inicio_01_Home--Desktop` `40000122:26493` (1:1 con `539:44895`: Banner real,
  subnav, tabs, búsqueda inteligente 5 selects + progreso, grid Card marca con logos reales, footer sync),
  `--Tablet` `40000123:91101` (3 col), `--Mobile` `40000124:26699` (2 col) + `Drawer--Nav` overlay `40000124:90606`.
- **Organisms nuevos** en NEW_00: `Navbar--Tablet` `40000123:5150`, `Navbar--Mobile` `40000123:90933`,
  `Drawer--Nav` `40000123:90944` (9 NavItem con los módulos reales), `Pagination--Mobile`.
- **Fixes:** cards móviles reescaladas proporcionalmente (clones reales, no squish), label desbordado oculto,
  68 colores religados a tokens (los ~28 restantes son grises propios de clones del original — fieles).
- **Siguiente:** sub-pantallas de Inicio (filtro manual/inteligente, promociones, categorías, perfil) o siguiente módulo.

---

## [2026-09-15] — NEW_01 Login listo + moléculas Modal/Table creadas
- **NEW_01 Login (Fase 3):** movidas las 6 pantallas atómicas (Acceso + Estación × M/T/D) a la página `NEW_01`,
  organizadas en 2 filas; **prototipo** Continuar→Paso 2 cableado en los 3 breakpoints + 3 flow starting points.
- **NEW_00 (Fase 2):** creadas las moléculas faltantes, fieles a los reales y 100% tokenizadas (0 hex, auditado):
  `Molecule/Modal` `40000118:5135` (Desktop 568px fiel a `643:86508` + variante Mobile bottom-sheet con drag handle),
  `Molecule/TableRow` `40000119:5133` (Header/Data + more-vertical), `Organism/Table` `40000120:5081` (fiel a `497:112774`).
  `Organism/Table` movido a la sección `03 Organisms`.
- **Pendiente:** botones internos del Modal → instancias del set Button; dropdown base; avatar label group.
- **Siguiente:** NEW_02 Inicio (Home hub + 4 modos de búsqueda según FLOWS.md).

---

## [2026-09-15] — Fase 2 (parte 1): NEW_00 Design System montado
- **NEW_00** estructurado: `01 Catálogo — componentes reales` (`40000113:4657`, 18 componentes indexados con
  instancias + etiquetas de mainId), `02 Molecules` (`40000111:4577`), `03 Organisms` (`40000111:4578`).
- **Migrados a NEW_00** los componentes atómicos fieles del Login (Stepper×2, LoginForm, EstacionForm, BrandPanel×3).
- **Brechas detectadas** (a crear): Modal (+header/actions), TableRow/Table, dropdown base propio, Avatar label group.
- `DESIGN_SYSTEM.md` actualizado con el catálogo y las brechas.
- **Siguiente:** crear Molecule/Modal + Organism/Table fieles; luego Fase 3 → `NEW_01 Login` (3 breakpoints solo-instancias).

---

## [2026-09-15] — REINICIO 0%: plan de migración NEW_ + mapa de flujos
- **Decisión del usuario:** rehacer todo de 0% en páginas `NEW_XX`, sin tocar lo existente; la base previa no convence.
  Plan encodado en `docs/MIGRATION_PLAN.md` + `CLAUDE.md` (5 fases, naming, reglas). Prohibido código — solo UI Figma.
- **Fase 1 COMPLETA — análisis de flujos:** extraídos **212 connectors** (Inicio 52, Consultas 54, Pedidos 48,
  Carrito 41, Catálogos 17) → `docs/FLOWS.md` con hubs, cadenas de modales y patrones por módulo.
- **Creadas 11 páginas** `NEW_00 Design System` … `NEW_10 Recompra` (esqueleto de la migración).
- **Se conservan** los tokens (Color/Spacing/Radius/Breakpoints/estilos) por venir del diseño real. Sandbox previo queda obsoleto.
- **Siguiente:** Fase 2 — poblar `NEW_00` con moléculas fieles (Table, Modal, Dropdown, Card marca/filtros, Banner, Alerts…).

---

## [2026-09-14] — Login Paso 2 (Estación) atómico y fiel + tokenización
- **Screens** `Screen/Estacion--Mobile` `40000103:90039` · `--Tablet` `40000103:90121` · `--Desktop` `40000103:90207`.
  Reusan los BrandPanel ya correctos; nuevos `Molecule/Stepper--Paso2` (`40000101:90055`) y `Organism/EstacionForm` (`40000103:4859`).
  Fiel: selects con avatar (Víctor Rodríguez), Sucursal/Caja, Estado "• Disponible", botón "Entrar al sistema →".
- **Fix atómico:** el agente había **hardcodeado 38 colores** → religados a tokens (`text/*`, `bg/*`, `border/input`, `brand/*`, `semantic/*`).
- **Desviación anotada:** los campos select se reconstruyeron a mano (no instancian el `143:3244` real); visualmente fieles — pendiente migrarlos al componente real.
- FIEL ahora tiene 6 screens del Login (Paso 1 y Paso 2 × 3 breakpoints).

---

## [2026-09-12] — Login COMPLETO atómico y fiel (Mobile + Tablet + Desktop)
- **Screens atómicos** reusando el mismo set de componentes: `Screen/Login--Mobile` `40000077:89995`,
  `Screen/Login--Tablet` `40000083:89926`, `Screen/Login--Desktop` `40000083:90012`.
- Inputs = instancias del **Input real de librería `327:59646`** (leading icon): mail en correo, **lock en contraseña** (swap `639:84934`).
- Nuevos componentes: `Organism/BrandPanel--Tablet` (`40000083:4777`), `Organism/BrandPanel--Desktop` (`40000083:89996`).
- **Fixes de fidelidad:** panel de marca a **gradiente lima** (estaba navy), texto de marca **oscuro** (estaba blanco),
  ilustración del Tablet en flujo (no encimada), wrap de headline/subtítulos, subtítulo del form completo.
- **Organización:** FIEL = 3 screens del Login; nueva sección `Componentes — Login`; eliminada la base clonada.
- **Pendiente menor:** el original tiene el headline oscuro sobre lima brillante — verificar contraste puntual.
  Luego: replicar método a otros módulos (Inicio, etc.) reusando/creando componentes.

---

## [2026-09-12] — Login Mobile reconstruido con Atomic Design (fiel)
- **Átomos:** creadas colecciones `Spacing` (`40000074:4577`) y `Radius` (`40000074:4586`). Capa de átomos completa.
- **Login Mobile atómico** (`Screen/Login--Mobile` `40000077:89995`) reconstruido con Auto Layout + componentes + tokens,
  **fiel al original** (gradiente+textura, logo, headline, ilustración 3D reusada `774:41683`, stepper con íconos 3D, inputs, botón lima, link).
  - Componentes nuevos: `Molecule/Stepper` (`40000077:4806`), `Organism/BrandPanel--Mobile` (`40000077:4828`), `Organism/LoginForm` (`40000077:89960`).
  - Único absoluto: textura de engranes (overlay decorativo deliberado). Sin hex sueltos.
- **Limpieza:** eliminados los 2 borradores por clonación (Login Mobile/Tablet) que no cumplían el método atómico.
  Sección `FIEL` = referencia Desktop + `Screen/Login--Mobile`.
- **Pendiente:** agregar ícono mail/lock DENTRO de los inputs (usar el Input real `327:59646`); Tablet y Desktop atómicos; luego otros módulos.

---

## [2026-09-12] — Gobernanza Atomic Design + push a GitHub
- **Repo:** los commits estaban solo en local; se configuró upstream y se **subió todo a GitHub** (`origin/main`).
  De aquí en adelante se pushea tras cada commit.
- **ROL + REGLAS** del usuario encodadas en `CLAUDE.md`: Arquitecto UI/UX; prohibido entregar código frontend;
  Atomic Design obligatorio (átomos→moléculas→organismos), Auto Layout con HUG/FILL, sin absolutos salvo overlay,
  nomenclatura `Atom/…`/`Molecule/…`/`Screen/…`.
- **Método revisado** en `WORKFLOW.md`: fidelidad se logra **reconstruyendo con componentes+Auto Layout**, NO clonando
  el original absoluto (el clon se ve mal y no es responsivo). Agentes `responsive-architect`/`design-system-librarian` actualizados.
- **Implicación:** los borradores FIEL por clonación (Login Mobile/Tablet) se **rehacen** con el método Atomic.

---

## [2026-09-12] — CORRECCIÓN DE RUMBO: fidelidad al diseño existente
- **Feedback del usuario:** lo generado (Login/Inicio responsive) se desvió a un **rediseño/propuesta**;
  el objetivo es **adaptar el diseño existente idéntico**, no inventar. Los borradores previos quedan como desechables.
- **Regla de fidelidad** añadida a `CLAUDE.md` (#1) y método clone-and-reflow en `WORKFLOW.md`.
- **Login Mobile fiel** (`40000064:4663`): clon del Desktop real `664:13013` reacomodado — conserva gradiente+textura,
  logo, headline, stepper con íconos 3D, inputs con ícono (mail/lock)+sombra, botón lima con glow, link subrayado.
  Base fiel Desktop en sandbox: `40000062:4582`.
- **Login Tablet fiel** (`40000071:4734`): mismo método (clon + reacomodo), banner de marca 834×460 + form real centrado.
- **Sandbox ordenado** en 2 secciones: `FIEL — reproducción fiel` (`40000069:4734`) y `BORRADORES desviados — a REEMPLAZAR` (`40000069:4735`). Sin encimados.
- **Pendiente:** Paso 2 (Estación) fiel; pulir clip menor del subtítulo del banner móvil; **reemplazar/eliminar** los borradores
  desviados que están en `03_Mobile`/`02_Tablet` (Login inventado) por los fieles; luego seguir módulos con fidelidad.

---

## [2026-09-12] — Componentes: NavItem + estados de grid; permisos sin prompt
- **Config:** `.claude/settings.json` autoriza `use_figma` y `Bash(curl:*)` sin prompt (flujo Figma fluido).
- **NavItem** (`40000060:4886`): Default / Active (indicador 3px lima) / Hover — para drawer/nav oscuro.
- **Estados de grid** en sandbox: `ProductGrid/Empty` (`40000061:4581`) y `ProductGrid/Loading` (`40000061:4889`).
- **Pendiente:** aplicar `NavItem`/estados en las pantallas; íconos nav semánticos; conectar nav→módulos.

---

## [2026-09-12] — Inicio (MAIN): Home "Autopartes" responsive + Login movido a final
- **Login:** movido de sandbox a `03_Mobile` / `02_Tablet` (aprobado).
- **Inicio Home** (`responsive-architect`, fuente `539:44895`): generados en sandbox
  `Mobile - Inicio_01_Home` `40000047:4577`, `Tablet - Inicio_01_Home` `40000051:4594`, `Drawer/Nav` `40000047:4686`.
  - Navbar oscuro → Mobile hamburguesa + drawer; Tablet nav parcial + hamburguesa.
  - Grid de productos 5→3 (tablet)/2 (mobile), tarjeta `Card_Product` con tokens; buscador = instancia `Input/Text`;
    chips de filtro con wrap; paginación simplificada; contenido de producto real.
  - **Prototipo:** hamburguesa → drawer (OVERLAY, DISSOLVE) + ✕ CLOSE. `overlayPositionType`/scrim read-only por API → ajuste manual.
- **UX review** (`ui-ux-reviewer`) + fixes aplicados: `Label/Small` 10→12px, nombres de producto →14px,
  SKU `text/tertiary`→`text/secondary`, chips a 44/40 (touch target), `ProductRow`/`NavItem` a Fill (reflow).
- **Pendiente (componente):** íconos nav semánticos, estado activo NavItem, `ProductGrid` vacío/carga, label buscador;
  conectar nav→módulos; resto de pantallas del módulo.

---

## [2026-09-12] — Componentes de formulario homologados (con estados)
- **Creado** (`design-system-librarian`) en `COMPONENTES` → sección `HOMOLOGADO 2026 · Forms` (`40000034:4891`):
  - `Input/Text` (`40000034:4890`): Default / Focus / Error / Disabled
  - `Button/Primary` (`40000035:4886`): Default / Hover / Loading / Disabled
  - `Select` (`40000036:4894`): Default / Focus / Error / Disabled
- Todo ligado a tokens `Color` + estilos de texto (cero hex sueltos). Foco = `semantic/info`, error = `semantic/danger`.
- **Cubre** los pendientes de estado del review del Login (focus/error/loading ahora existen como componentes).
- **Pendiente:** sustituir los controles inline del Login del sandbox por instancias de estos componentes; ligar los componentes viejos de `COMPONENTES` a tokens.

---

## [2026-09-11] — Login responsive (piloto end-to-end) en sandbox
- **Generado** (`responsive-architect`) en `04_Claude_Sandbox`: 4 frames con tokens `Color` + estilos de
  texto + variables `Breakpoints` (modo explícito por frame):
  - `Mobile - Login_01_Acceso` `40000017:4592` · `Mobile - Login_02_Estacion` `40000019:4592`
  - `Tablet - Login_01_Acceso` `40000020:4592` · `Tablet - Login_02_Estacion` `40000021:4592`
  - Mobile = 1 columna; Tablet = card centrada sobre fondo lima.
- **Fix:** cards de Tablet colapsaban (alto FIJO 10px) → `primaryAxisSizingMode: AUTO`; label Paso 2 corregido.
- **UX review** (`ui-ux-reviewer`, WCAG 2.2 AA): recalculé contraste (el reviewer sobreestimó fallos).
  Aplicados: `tertiary`→`secondary` en placeholders/labels/stepper (5.25:1), labels de sección 10→14px.
  Pendiente (variantes de componente): foco, error/loading, borde input ≥3:1, área táctil icono ojo.
- **Prototipo** (`figma-prototyper`): "Continuar" Paso 1 → Paso 2 (Smart Animate) en mobile y tablet.
- **Pendiente:** aprobar en sandbox y mover a `02_Tablet`/`03_Mobile`; luego siguiente módulo.

---

## [2026-09-11] — Fase 0: tokenización de color + tipografía
- **Extracción real:** scan de `COMPONENTES` → paleta (marca lima `#AEF803` + verde `#006C00`, neutrales
  tipo Untitled UI, semánticos azul/naranja/ámbar/rojo) y tipografía Inter (36/26/22/20/16/14/10).
- **Figma:** creada colección **`Color`** (`40000009:4577`) con **23 tokens** (brand/text/bg/border/semantic/base)
  con scopes correctos; creados **9 estilos de texto** Inter (Display/H1/H2/H3, Body×3, Label×2).
- **Docs:** `DESIGN_SYSTEM.md` con tablas reales; `PROJECT_MAP.md` Fase 0 actualizada.
- **Pendiente:** ligar los componentes de `COMPONENTES` a estos tokens (homologación), migrar restos SDS,
  deprecar colección legacy. Luego: responsivar módulo **Login**.

---

## [2026-09-11] — Orquestación del cerebro + estructura responsive (gran pasada)
- **Corrección de análisis:** el archivo NO era "solo PROPUESTAS". Vía Plugin API se confirmó la
  **app Desktop real** en páginas por módulo (`1.0 Login` … `10 Recompra`) + `COMPONENTES`. Ver **ADR 0003**.
- **Figma (escritura):**
  - Creadas páginas `02_Tablet`, `03_Mobile`, `04_Claude_Sandbox`.
  - Eliminadas páginas redundantes `00_Design_System`, `01_Web_Final` (DS vive en `COMPONENTES`).
  - Creada colección **`Breakpoints`** (modos Desktop/Tablet/Mobile) con 11 variables numéricas
    (container, márgenes, gutter, padding, escala tipográfica, touch target).
  - Detectado: 0 estilos de color/texto, 2 variables de color previas → tokenización pendiente (Fase 0).
- **Cerebro (docs):** reescritos `FIGMA_ANALYSIS.md`, `PROJECT_MAP.md`, `ARCHITECTURE.md`, `RESPONSIVE_TOKENS.md`,
  `WORKFLOW.md`, `DESIGN_SYSTEM.md`; nuevos `UX_PRINCIPLES.md` y `PROTOTYPING.md`; `CLAUDE.md` actualizado.
- **Agentes:** arreglados `responsive-architect` y `design-system-librarian` (les faltaba la tool `use_figma`);
  nuevos `ui-ux-reviewer` y `figma-prototyper`.
- **Investigación:** valores responsive (Untitled UI/8pt), checklist WCAG 2.2 AA, API de prototipado (reactions).
- **Pendiente:** Fase 0 (tokenizar color + tipografía) y luego responsivar por módulo empezando por **Login**.

---

## [2026-09-11] — Migración a copia editable en cuenta Zurco
- **Contexto:** el original `OL0CHY8eN9zjNeGmHg0el3` estaba en solo lectura. Se hizo una **copia**
  (`CW-Responsive-prueba`, `fileKey: DRcQy7uKgoL5AlMPK0fJU7`) en la cuenta Zurco.
- **Verificado:** autenticación MCP como `gersongarcia@zurco.com.mx` (asiento Full, *Zurco Designio*);
  **escritura HABILITADA** (test `createPage`→`remove` OK); estructura idéntica al original.
- **Modificado:** `CLAUDE.md`, `FIGMA_ANALYSIS.md`, `DESIGN_SYSTEM.md` → apuntan al nuevo `fileKey`.
- **Pendiente:** PASO 0 sigue vigente — elegir propuesta ganadora, login y design system único antes de responsivar.

---

## [2026-09-11] — Análisis inicial del archivo Figma
- **Modificado:** `FIGMA_ANALYSIS.md`, `PROJECT_MAP.md`, `DESIGN_SYSTEM.md` con datos reales.
- **Hallazgos:**
  - Acceso de **lectura** habilitado (cuenta Gerson) tras reconectar el MCP.
  - El archivo es de **PROPUESTAS** (variantes en exploración), no una app terminada. Todo Desktop.
  - 7 grupos de propuestas: 3 sidebar, 2 navbar, 2 login. ~15 dashboards + 4-6 login.
  - **Mezcla de 2 design systems:** SDS (`--sds-*`) en login + componentes tipo Untitled UI en dashboards.
  - Tipografía base: Inter. Tokens SDS de color/espaciado extraídos.
- **Pendiente:** PASO 0 — elegir propuesta ganadora (sidebar vs navbar), variante de login y
  design system único, antes de responsivar. Confirmar acceso de **escritura**.

## [2026-09-11] — Inicialización del cerebro
- **Creado:** repositorio de orquestación (docs + configuración de Claude Code).
- **Cambios:** `CLAUDE.md`, `docs/` (WORKFLOW, PROJECT_MAP, RESPONSIVE_TOKENS, ARCHITECTURE,
  DESIGN_SYSTEM, FIGMA_ANALYSIS), agentes `.claude/agents/`, ADR inicial.
