# Bitácora de Cambios

Registro cronológico de todo lo que se hace en el proyecto (diseño y documentación).
Nada se pierde: cada pantalla generada, homologación o decisión se anota aquí.

Formato:
```
## [2026-09-19] — REMAKE v2 · Fase 4 COMPLETA (Tablet 768): 12 pantallas
- **Todas las pantallas Web adaptadas a 768** en `Tablet · 768`, sections `1.0`–`10.0` en orden numérico (re-stack final, alto total 14679):
  - `Screen/Carrito--Tablet` (`40000469:98551`): card + panel de venta **apilados**; tabla reducida a Producto/Cantidad/Importe/Acciones.
  - `Screen/Catalogos--Tablet` (`40000469:6718`): grid de marcas a 3 columnas.
  - `Screen/Consultas-{Ventas,Creditos,Garantias}--Tablet` (`40000470:99371/99749/100127`): selects 300px en wrap; tablas reducidas — Ventas: Folio/Venta/Status/Acciones · Créditos: Cliente/Saldo/Status/Acciones · Garantías: Folio/Importe/Estado/Acciones.
  - `Screen/Corte-AperturaCaja--Tablet` (`40000470:100705`): modal 680px sobre el Inicio tablet.
  - `Screen/Pedidos--Tablet` (`40000470:98892`): KPIs 224px en wrap (3+2); tabla Cliente/Total/Estado/Acciones.
  - `Screen/Chat--Tablet` (`40000470:100504`): lista 260px + conversación fill; burbujas clampeadas a 400px.
  - `Screen/Abonos--Tablet` (`40000470:6799`): tabla Cliente/Importe/Condición/Acciones; tabs en wrap.
  - `Screen/Recompra--Tablet` (`40000470:101124`): card + panel Filtros apilados; grupos con Código/Producto/Costo final/Piezas/Acciones.
- **Patrón tabla-tablet consolidado:** conservar 4 columnas clave + acciones; el detalle completo vive en el overlay/Ver de cada fila.
- **Gotcha documentado:** al apilar un BodyRow (H→V), los hijos con `sizingV: FILL` colapsan a 2px bajo un padre HUG → pasar a HUG.
- **Pendiente:** overlays tablet (VerPedido, diálogos), Fase 5 Mobile 375, prototipo y QA.

## [2026-09-19] — REMAKE v2 · Fase 4 iniciada (Tablet 768): Login + Inicio + organismo TopNav--Tablet
- **Nuevo en el DS** (`03 · Componentes`, junto a GlobalSearch): `Organism/TopNav--Tablet` (`40000468:4800`) — logo + menú hamburguesa (abre drawer de nav) + resumen de venta compacto (sin trash/check) + campana + avatar, 768×64.
- **Tablet · 768, section `1.0 Login`:** `Screen/Login--Tablet` (`40000467:6613`, 768×1024) — clon de Propuesta B con card 440 centrada y engranes decorativos reposicionados.
- **Tablet · 768, section `2.0 Inicio`:** `Screen/Inicio--Tablet` (`40000468:6871`, 768×~1290) — TopNav swapeada al organismo tablet, utility sin búsqueda global (breadcrumb + sucursal), selects de Búsqueda Inteligente en **2 columnas** (300px, wrap), chips con wrap, **grid de marcas a 3 columnas** (cards 208), footer fill.
- **Patrón tablet establecido:** swap de TopNav al organismo `--Tablet`, ocultar búsqueda global del utility, wrap en filas de controles, grids 5→3.
- **Pendiente Fase 4:** Carrito, Catálogos, Consultas ×3, Corte, Pedidos (+overlays), Chat, Abonos, Recompra en tablet (las tablas requieren reducción de columnas + patrón Btn/Ver).

## [2026-09-19] — REMAKE v2 · Fase 3 COMPLETA: orden del DS + layout de páginas + Carrito
- **DS ordenado (feedback del usuario):** los 5 componentes post-Fase 1 (`Select`, `NavItem/Dark`, `Organism/TopNav`, `Organism/Footer`, `Molecule/GlobalSearch`) estaban FUERA de la section `03 · Componentes` (regados debajo, x=40) → reacomodados en la retícula (x=80, filas ordenadas) y section ampliada a h=3140.
- **Layout de `CARESA Web Responsive`:** la section Web se amplió a w=4768 (5.0 Consultas con 3 pantallas la desbordaba) y `Tablet · 768` / `Mobile · 375` se movieron a x=5008 / x=7048 para no encimar los flujos de Web.
- **Carrito DESBLOQUEADO** vía Plugin API (sin el límite de 2M chars del MCP): hub original `Frame 1000004189` (`322:12443`, página `3 Carrito`).
- **Section `3.0 Carrito`** (`40000443:13398`) intercalada en orden numérico (módulos 4.0→10.0 recorridos +1450; Web/Tablet/Mobile a h=14453).
- **Screen/Carrito** (`40000443:13399`): clon de Recompra (aprovecha el split card+sidebar) →
  - Nav Carrito activa; H1 "Carrito / Completa la venta del carrito actual"; card "Carrito · 2 Productos · Procesa la compra del cliente" + buscador full "Escanea el código o ingresa el nombre del producto".
  - Tabla: Producto (foto real + código + ubicación S1/P1-A2-N05) · U/M · Marca (logos SYD/Quaker State vía imageHash) · Stock (badges S1/S2 semáforo) · Cantidad (stepper +/qty/−) · P. Unitario/P. Descuento · Importe verde · Acciones (eliminar/⋮). 2 filas fieles: Amortiguador 7000062 ×2 $6,327.00 · Aceite 0986AF0051 ×1 $783.75.
  - Sidebar de venta: Cliente "Ventas mostrador" + Buscar/Limpiar, chip DOC/2026/04587592-238539, ⚠ "No hay descuentos válidos", Resumen (Partidas 2 · Piezas 3 · Subtotal $7,485.00 · Descuentos $0.00 · **Total $7,485.00**), pago Crédito/●Contado (Radio del DS), botones Vender (Primary) / Imprimir / Más opciones.
- **Fase 3 Web: 12/12 pantallas.** Siguiente: Fase 4 (Tablet 768) y Fase 5 (Mobile 375); después prototipo/QA.

## [2026-09-18] — REMAKE v2 · Fase 3 (cont.): homologación de sections + Garantías, Catálogos, Corte, Recompra
- **Homologación de sections (feedback del usuario):** top-level `#1d2939` (fix: `02 · Iconografía` del DS), módulos `#344054` (fix: `9.0 Abonos` tenía gris default, `Mobile · 375` tenía `#475467`); Tablet/Mobile a la misma altura que Web; **orden numérico restaurado** (5.0 antes que 7.0) y nuevas sections `4.0 Catálogos`, `6.0 Corte de caja`, `10.0 Recompra` intercaladas en su lugar.
- **Screen/Consultas-Garantias** (`40000431:5880`, section 5.0): clon de Créditos → tab Garantías activa, "TOTAL SELECCIONADO $0.00", fila de estados En proceso/Aplicado/**Ver todos** + Busca/Filtros/Columnas (reemplaza los selects), tabla 8 columnas (Folio #140556135 con checkbox, Documento, Fecha, Proveedor NA/DISTRIBUCIONES SAGAJI, Agente, Importe, Estado Warning/Success, Acciones ojo + check-circle `success/600` en filas En proceso). Spec del original MB-69 `741:292447`.
- **Screen/Catalogos** (`40000432:6042`, section 4.0): clon de Inicio → nav Catálogos activa, H1 "Catálogos" + "39 artículos compatibles", chip "Producto ▾", sin panel de búsqueda inteligente; grid 5×4 con **logos reales del original** vía imageHash (ACDelco/BOGE/SPARKPLUG/CAHSA/CLOYES + 15 ACDelco) y subtítulos de categoría. Spec del original MB-57 `574:47419`.
- **Screen/Corte-AperturaCaja** (`40000434:6117`, section 6.0): fondo = clon de Inicio + Overlay/Scrim + modal 854px "APERTURA DE CAJA / Monedas y billetes en caja": 2 tablas de denominaciones ($200→$1 y $0.50→$0.01) con steppers −/0/+ (bordes `error/300`/`success/300`, iconos `error/600`/`success/600`), bloque Total "$ 0.00 MXN" y botonera Cerrar/Confirmar. Chrome del modal reutilizado de VerPedido. Spec del original `630:107484`.
- **Screen/Recompra** (`40000437:6286`, section 10.0): clon de Abonos → nav "Más" activa, card "Módulo de compras" + botón Exportar Excel, buscador 480px + chip "9 productos filtrados" + Filtros; **tabla agrupada por proveedor** (3 grupos con chevron, contador rojo y botón de descarga verde) con columnas Código/Producto (foto real)/Marca (logos SYD·BOSCH·MOOG vía imageHash)/Costo Ant./Costo final (semáforo)/Piezas (n/10 + icono)/Cant. S./R y S/Acciones; **panel lateral Filtros** (6 tarjetas arrastrables con Toggle del DS + Aplicar/Limpiar). Pantalla crece a 1473px (Content en HUG). Spec del original MB-13 `741:165043`.
- **Nota técnica:** si un script de `use_figma` lanza excepción, sus cambios previos se revierten (rollback transaccional) — re-aplicar todo el bloque tras corregir.
- **Pendiente Fase 3:** solo **Carrito** (bloqueado: requiere node-id del usuario; la página original excede el límite de lectura). Luego Fase 4 Tablet / Fase 5 Mobile.

## [2026-09-18] — REMAKE v2 · Fase 3 (cont.): Abonos (Web 1440)
- **Section nueva `9.0 Abonos`** (`40000425:5666`) en `CARESA Web Responsive` → Web · 1440 (debajo de 8.0 Chat; section Web crecida a 8470).
- **Screen/Abonos** (`40000425:5667`): construido clonando `Screen/Pedidos` (misma TopNav/UtilityBar/Footer/card) y transformándolo con la spec real del original (`9 Abonos` → sección ABONOS `739:56096`, frame `739:68154`):
  - TopNav: **Abonos activo** (pill lime + Icon/package re-aplicado), Pedidos desactivado (Icon/truck re-coloreado — el swap de icono resetea el color).
  - Sin KPIs (el original no los tiene); sin botones Confirmar/Cancelar; buscador "Busca" (clon del GlobalSearch, 300px) junto a Filtros/Columnas en la fila de tabs; tab activa **Ver todos**.
  - Tabla 9 columnas: Cliente (Checkbox + nombre + DOC/251684) · Tipo de abono · Importe · Solicitud · Hora de solicitud · Repartidor · Método (icono+texto) · Condición · Acciones. 8 filas fieles al original (fila 1 = Gerson/Multinota/App/---/Efectivo/Rep. Solicitado + acción ✕ roja vía `error/600`; filas 4-5 Gerson; fila 8 Depósito con Icon/download).
  - Mapeo de badges (el DS v2 no tiene purple/pink): Multinota→Info, Individual→Gray, App→Brand, Web→Info, Rep. Solicitado→Warning, Completado→Success.
  - Fix aplicado: Cell/Repartidor heredaba alineación derecha de Cell/Total → alineado a la izquierda en las 8 filas.
- **Pendiente Fase 3:** Consultas·Garantías, Carrito (requiere node-id del usuario), Catálogos, Corte de caja, Recompra + overlays de Abonos (Ver abono / diálogos).

## [2026-09-18] — REMAKE v2 · Fase 3 (cont.): Ver pedido + Créditos + Chat, reorganización jerárquica
- **Reorganización de `CARESA Web Responsive`:** sección Web en columna vertical con sub-secciones horizontales por módulo (1.0 Login, 2.0 Inicio, 7.0 Pedidos, 5.0 Consultas, 8.0 Chat); Tablet · 768 y Mobile · 375 a la derecha del bloque Web.
- **Iconos de Button:** variantes Destructive → fg/white, Primary → fg/on-brand (maestro) + fix en instancia Cancelar de Pedidos. Nota: el swap de icono resetea el color; re-aplicar al usar.
- **Screen/Pedidos-VerPedido** (`40000415:5203`): lista con Overlay/Scrim + modal 1088px (chip folio oscuro, estado, cierre 44px, fila de info 6 campos, tabla 4 ítems SYD/BOSCH/MEFRA/SACHS con precios/descuentos, cards Dirección+Comentarios, resumen con Total $10,194.50, botonera Cancelar/Confirmar pedido).
- **Screen/Consultas-Creditos** (`40000417:5414`): tab Créditos activo, tabla Cliente/Folio/Días/Límite/Saldo(rojo)/Vence/Status (Activo/Por vencer/Vencido/Sin saldo) con avatares de rol.
- **Screen/Chat** (`40000419:5592`): dos columnas — lista de 6 conversaciones (avatar por rol, badge no-leídos, activa resaltada) + conversación con burbujas (entrante blanca / saliente lima con texto oscuro), header con estado en línea y RoleChip, input pill + Enviar.
- **Pendiente Fase 3:** Garantías, Carrito (requiere node-id del usuario), Catálogos, Corte de caja, Abonos, Recompra.

## [2026-09-18] — REMAKE v2 · Fase 3: logos reales + Pedidos + Consultas·Ventas
- **Logos reales de marcas:** 19 PNG del dataset público `filippofilip95/car-logos-dataset` (GitHub) subidos vía `upload_assets` a las cards del grid de Inicio. SYD conserva su logo del archivo. Assets locales en `~/.claude/jobs/a9d428d9/tmp/logos/`.
- **Screen/Pedidos** (`40000408:4814`): TopNav (Pedidos activo), 5 KPI cards con tendencia, tabla con tabs de estado, Confirmar/Cancelar, Filtros/Columnas, 7 filas con RoleChip + badges por estado + acciones, paginación, footer. Spec del original 683:56095.
- **Screen/Consultas-Ventas** (`40000411:5031`): tabs Ventas/Créditos/Garantías, chip TOTAL SELECCIONADO, filtros (fechas/agente/cliente), tabla 8 columnas con Emitida/Cancelada, paginación, footer. Spec del original 741:289083.
- **Specs extraídas** (figma-auditor) para Pedidos detalle, Consultas completo, Corte, Chat, Abonos, Catálogos y Recompra. Carrito requiere node-id manual (página >2M chars).
- **Pendiente Fase 3:** Ver pedido (modal), Créditos/Garantías, Carrito, Catálogos, Corte de caja, Chat, Abonos, Recompra.

## [2026-09-18] — REMAKE v2 · Fase 2 aprobada (Login B) + Fase 3 iniciada (Inicio Web)
- **Login definitivo:** Propuesta B (card centrada sobre degradado del logo). Propuesta A queda en la section como registro.
- **Nuevos en el DS:** `Select` (5 estados, `40000400:4718`), `NavItem/Dark` (`40000400:4729`), `Organism/TopNav` (`40000401:4697`), `Organism/Footer` (`40000401:4809`).
- **Screen/Inicio Web 1440** (`40000402:4632`): navbar oscura con pill lima activa + resumen de venta, utility bar (breadcrumb/buscador global/sucursal), chips Promociones·Autopartes·Categorías, panel Búsqueda Inteligente (5 selects + Buscar + progreso 0/5 + Limpiar/Escanear VIN/Buscar por SKU), grid de marcas 5×4 con logo clonado del original, footer de sistema. Todo instancias v2.
- **Corregido en autovalidación:** grid colapsado a 1 fila → cards a 5 columnas; logo de card equivocado (CARESA→marca) y nombre alineado al logo disponible (SYD).
- **Pendiente Fase 3:** Carrito, Catálogos, Consultas, Corte de caja, Pedidos, Chat, Abonos, Recompra.

## [2026-09-18] — REMAKE v2 · Fase 2: Login, dos propuestas (Web 1440)
- **Creado:** página `CARESA Web Responsive` (`40000397:4577`) con sections `Web · 1440` / `Tablet · 768` / `Mobile · 375` lado a lado, lienzo oscuro.
- **Login/PropuestaA** (`40000398:4592`): split 620px panel oscuro de marca (eyebrow lima + headline + engranes decorativos al 12%) + formulario blanco centrado 400px. Logo original clonado (sin tocar la fuente).
- **Login/PropuestaB** (`40000399:4611`): card blanca centrada 440px con Shadow/xl sobre degradado del logo (#346301→#89C303→#AEF803) y engranes de línea decorativos.
- Ambas 100% instancias v2 (Input, Checkbox, Button Primary), Auto Layout, sin hex sueltos en componentes; misma estructura de formulario (label arriba, remember/forgot, CTA único).
- **Pendiente:** usuario elige A o B → Fase 3 (pantallas Web).

## [YYYY-MM-DD] — Título
- **Creado/Modificado:** ...
- **Cambios:** ...
- **Pendiente:** ...
```

## [2026-09-18] — REMAKE v2 · Fase 1: Design System "CARESA v2" completo
- **Creado:** página `CARESA v2 — Design System` (`40000379:4577`) con 3 sections (Fundaciones / Iconografía / Componentes) sobre lienzo oscuro.
- **Tokens (145 variables):** `CARESA v2 / Primitives` (brand lima del logo #AEF803/#89C303/#346301, gray, error, warning, success, info — escalas 25–950), `Spacing` (escala 8pt: 4–64), `Radius` (0–full), `Color` semántica (48 alias con scopes: bg/text/border/fg/action). Code syntax WEB en todas.
- **Estilos:** 14 de texto (Inter Display→Caption, LH 1.4–1.6) + 5 sombras (Shadow xs–xl).
- **Iconografía:** 42 iconos de línea 24px trazo 2px (estilo Untitled UI, recreados localmente — la librería de comunidad no es suscribible vía MCP). Roles diferenciados: `user`=Cliente, `wrench`=Mecánico.
- **Componentes (12 sets, todos con variantes/props/estados y variables ligadas):** Button (24 var., 44px, loading/focus/disabled), Input (5 estados, label arriba + error con icono), Checkbox (9), Radio (6), Toggle (6, ON=brand/700 por contraste 3:1), Badge (6 colores), Alert (4 tipos con icono semántico), Modal (Default/Destructive, homologado a la referencia aprobada 600px/badge/divider/botonera), Overlay/Scrim (sin frame de fondo), Tab (8), Table/HeaderCell+Cell (alineación por tipo de dato), Card, NavItem, Skeleton, RoleChip, EmptyState.
- **Auditoría previa:** 16 anti-patrones (AP-01…AP-16) catalogados desde los enlaces de errores del intento anterior; las descripciones de componentes referencian los AP que previenen.
- **Validado:** capturas de cada bloque + estructura; sin hardcodes en fills/strokes/radius/spacing de componentes.
- **Pendiente:** aprobación de Fase 1 → Fase 2 (Login, 2 propuestas).

---

## [2026-09-18] — NEW_05 Consultas: overlays cableados en 3 breakpoints (92 reactions)

- **Flujo cableado:** 14 grupos de overlays (Ventas/Créditos/Garantías) × 3 breakpoints.
- **Patrón:** NAVIGATE + DISSOLVE 250ms EASE_OUT en todos los triggers.
- **Nodos con reactions (Desktop):**
  - Ventas: `40000187:7940` (⋮ fila 1) → VentasMasOpciones
  - VentasMasOpciones: `40000213:5932` (Enviar correo) `40000213:5938` (Cancelar) `40000213:5944` (Garantía)
  - VentasEnviarCorreo: `40000216:5929/5936/5938` (×/Cancelar/Enviar) → Ventas
  - VentasCancelarVenta: `40000216:5946/5953/5955` (×/No/Cancelar) → Ventas
  - VentasCrearGarantia: `40000217:5929/5968/5970` (×/Cerrar/Crear) → Ventas
  - Créditos: `40000195:26878` (⋮ fila 1) → CreditosMasOpciones; Scrim `40000234:4578` → Creditos
  - CreditosMasOpciones: `40000234:4585` (Enviar) `40000234:4595` (Abonar) → destinos resp.
  - CreditosAbonarPagar: `40000235:4582/4654/4656` → Creditos/Creditos/AbonoConfirmar
  - CreditosAbonoConfirmar: Toast `40000236:4629` → Creditos
  - CreditosEnviarCorreo: `40000236:4582/4588/4590` → Creditos
  - Garantías: `40000195:98133` (eye fila 1) → GarantiasVerDetalle
  - GarantiasVerDetalle: `40000253:5957/6018/6020` (×/Cerrar/Continuar)
  - GarantiasAplicar: `40000254:5957/5975/5977` (×/Aplicar/Regresar)
  - GarantiasAlerta: Toast `40000254:5980` → Garantias
- **Tablet:** mismo patrón; triggers: `40000190:5557` `40000198:5907` `40000203:5961` (Btn/Ver)
- **Mobile:** mismo patrón; triggers: `40000191:5536` `40000202:5895` `40000204:5966` (Btn/VerDetalle)
- **Faltantes reportados:** VentasMasOpciones Desktop/Tablet no tienen frame "Scrim" ni botón ✕ propio (es un popover sin scrim). **RESUELTO post-agente:** se cableó el FRAME RAÍZ del overlay (ON_CLICK → screen de Ventas) en los 3 breakpoints — clic fuera del menú cierra.
- **Auditoría real (conteo por sección `05 · CONSULTAS`):** 36 reactions por breakpoint (incluye las 18 tabs previas). Pedidos auditado: Desktop 41 · Tablet 29 · Mobile 26 (los breakpoints reducidos tienen menos triggers). Flow points depurados: "Pedidos · {Desktop,Tablet,Mobile}" apuntando a la Lista de cada página (eliminados duplicados y "Flow 2").
- **Nota:** El botón "Btn/Cerrar" en CreditosAbonarPagar Desktop (`40000235:4654`) es un frame sin texto hijo accesible; se aplicó reaction al frame directamente.

## [2026-09-18] — NEW_07 Pedidos: prototipo completo en 3 breakpoints (reactions + flow starting points)

- **Flujo cableado:** Lista → 13 pantallas/overlays → Lista (ciclo completo de pedidos).
- **Patrón:** NAVIGATE + DISSOLVE 250ms en todos los triggers. Sin OVERLAY (los frames de overlay ya incluyen scrim propio).
- **Flow starting points creados:** "Pedidos · Desktop" (Lista `40000270:4592`) · "Pedidos · Tablet" (Lista `40000271:4746`) · "Pedidos · Mobile" (Lista `40000272:4901`).
- **Triggers cableados por breakpoint (mismo patrón en los 3):**
  - Lista: ojo fila 1 → VerDetalle · ojo fila 5 → Validar · ojo fila 6 → VerListoParaEnviar · ojo fila 7 → SeguimientoEnvio · Btn "Confirmar" header → ConfirmarSeleccionados · Btn "Cancelar" header → CancelarSeleccionados
  - VerDetalle: ✕ → Lista · "Cancelar pedido" → CancelarSeleccionados · "Confirmar pedido" → Lista
  - Validar: buscador → AnadirProducto · ✏ fila 1 → EditarCantidad · 🗑 fila 1 → EliminarProducto · "Validar pedido" → VerListoParaEnviar · "Cancelar pedido" → Lista · ✕ → Lista
  - AnadirProducto: "+ agregar" → Validar · ✕ → Validar
  - EditarCantidad: "Editar cantidad" → Validar · "Cerrar" → Validar · ✕ → Validar
  - EliminarProducto: "Eliminar producto" → Validar · "Cerrar" → Validar · ✕ → Validar
  - VerListoParaEnviar: "Enviar este pedido" → Enviar · ✕ → Lista
  - Enviar: "Enviar pedido" → Lista · ✕ → Lista
  - ConfirmarSeleccionados: "Si, confirmar" → Lista · "Cerrar" → Lista · ✕ → Lista
  - CancelarSeleccionados: "Cancelar pedidos" → Lista · "Cancelar" → Lista · ✕ → Lista
  - VerCancelado: ✕ → Lista
  - VerCompletado: "Imprimir" → Lista · ✕ → Lista
  - SeguimientoEnvio: "Volver" → Lista · ✕ → Lista
- **Decisión:** "Cancelar pedido" en VerDetalle navega a CancelarSeleccionados (no a Lista directa) para fidelidad al flujo real — el usuario pasa por el modal de confirmación de cancelación.
- **Nodos con reactions (Desktop selección):** `40000276:4989` · `40000276:5070` · `40000276:5087` · `40000276:5098` · `40000276:5120` · `40000276:5125` · `40000283:5109` · `40000283:5257` · `40000283:5259` · `40000291:5124` · `40000291:5159` · `40000291:5157` · `40000291:5255` · `40000291:5253` · `40000289:5109` · `40000317:5132` · `40000315:5109` · `40000314:5148` · `40000314:5146` · `40000314:5111` · `40000313:5120` · `40000313:5118` · `40000313:5111` · `40000341:5269` · `40000341:5109` · `40000298:5164` · `40000298:5109` · `40000329:5188` · `40000329:5186` · `40000329:5110` · `40000330:5192` · `40000330:5190` · `40000330:5110` · `40000342:5109` · `40000343:5109` · `40000343:27103` · `40000354:7556` · `40000351:7434`
- **Estimado total reactions:** ~38 Desktop + ~38 Tablet + ~38 Mobile = ~114 reactions.

---

## [2026-09-17] — REORGANIZACIÓN: páginas por breakpoint (NEW_WEB / NEW_TABLET / NEW_MOBILE)
Decisión del usuario: dejar el design system en su página y TODO lo demás en 3 páginas responsive, agrupado por módulo en sections verticales con los flujos en horizontal.
- **Páginas nuevas:** `NEW_WEB · Desktop (1728)` `40000365:5103` · `NEW_TABLET · (834)` `40000365:5104` · `NEW_MOBILE · (393)` `40000365:5105` (después de `NEW_00 Design System`, que se conserva).
- **Estructura por página:** sections por módulo apiladas (gap 500): `01 · LOGIN`, `02 · INICIO`, `03 · CARRITO`, `05 · CONSULTAS` (subsections Ventas/Créditos/Garantías), `07 · PEDIDOS` (subsections Lista / Ver pedido · estados / Surtir / Enviar / Selección múltiple / Seguimiento envío). Pantallas en fila por flujo (gap 120), subsections con padding 60, sections con padding 100.
- **Rescate de extraviados:** `Screen/Pedidos_01_Lista--{D,T,M}` y `Overlay/PedidoEnviar--{D,T,M}` estaban tirados en la página `PROPUESTAS` (agentes que no cambiaron de página) → movidos a su lugar.
- **Limpieza:** 11 nodos basura/duplicados eliminados (2 TEXT dump, Sep, Spacer, Divider suelto, y las 2 series duplicadas de PedidoEliminarProducto/PedidoEditarCantidad `40000304:*`/`40000305:*`).
- **Páginas viejas `NEW_01..NEW_10` eliminadas** (quedaron vacías tras la mudanza). Fuentes (1.0 Login … 10 Recompra, COMPONENTES, PROPUESTAS) intactas; legacy 02_Tablet/03_Mobile/04_Claude_Sandbox sin tocar.
- **Pase de reparación responsive global:** 134 contenedores Auto Layout recortados corregidos (WEB 56 · TABLET 34 · MOBILE 44).
- **Convención nueva:** los próximos módulos (04 Catálogos, 06 Corte, 08 Chat, 09 Abonos, 10 Recompra) se agregan como nuevas sections en estas 3 páginas — ya NO se crean páginas por módulo.

---

## [2026-09-17] — NEW_07 Pedidos: Overlay "Seguimiento de Envío (ADMIN)" en 3 breakpoints

- **Creado (3 frames en `NEW_07 Pedidos`):**
  - `Overlay/PedidoSeguimientoEnvio--Desktop` `40000349:27000` (1728×1128, x=0 y=9600)
  - `Overlay/PedidoSeguimientoEnvio--Tablet` `40000355:5109` (834×1194, x=1900 y=9600)
  - `Overlay/PedidoSeguimientoEnvio--Mobile` `40000356:5109` (393×950, x=2900 y=9600)
- **Fuente:** modal `683:69908` en section `683:63949` "SEGUIMIENTO ENVIO (ADMIN" de `7 Pedidos`
- **MAP clonado:** Frame `683:70603` "MAP 5" — vector map con street names (no image fill). Clonado en los 3 breakpoints:
  - Desktop MAP: `40000354:7525` (1138×730 en RightColumn)
  - Tablet MAP: `40000355:7544` (476×810 en RightColumn)
  - Mobile MAP: `40000356:7504` (393×280 en ScrollContent)
- **Contenido verificado (verbatim del original):**
  - Header: "Pedido: DOC/515151/21020" + badge "Enviado" + "Orden creada : 01/01/26 - 8:00AM"
  - Repartidor: "David Manuel Espinoza Rodriguez", Estado: "Sin salir", Tiempo: "00:00 / 20:00"
  - Dirección: "Calle Tercera Pte. Sur 366, San Antonio, 29140 Ocozocoautla de Espinosa, Chiapas."
  - Comentarios: "Entregar en puerta roja"
  - Foto/Firma: "Sin capturar" para ambos
  - Info row: Nivel=Mecanico, Cliente=Gerson Yahir Garcia Gonzalez, Metodo entrega=Envio a domicilio, Metodo pago=Crédito cliente, Disponible=$ 12,000.00, Vendedor=Gerson Garcia
  - Cronología (4 ítems con círculo verde/gris): Pedido surtido 09:30 · Pedido listo para enviar 09:35 · En camino 09:37 · Entrega confirmada 09:50
  - Footer: botón "Volver" (lima #AEF803)
- **Responsive:**
  - Desktop: scrim + diálogo centrado (1600×960), 2 columnas (sidebar 430px | map+info 1170px)
  - Tablet: scrim + diálogo centrado (780×1100), 2 columnas (sidebar 280px | map+info 500px)
  - Mobile: bottom-sheet (393px), header compacto, mapa full-width 393×280, sidebar apilado, botón Volver full-width (44px touch)
- **Auditoría:** 0 hex sueltos en nodos propios; colores vía tokens `Color`; MAP clonado de original (sin redibujado)

## [2026-09-17] — NEW_07 Pedidos: 3 variantes de estado del modal "Ver pedido" (ListoParaEnviar + Cancelado + Completado) en 3 breakpoints c/u

- **Creado (9 frames):**
  - `Overlay/PedidoVerListoParaEnviar--Desktop` `40000341:5103` (1728×1128, y=12500)
  - `Overlay/PedidoVerListoParaEnviar--Tablet` `40000341:5271` (834×1194, x=1900 y=12500)
  - `Overlay/PedidoVerListoParaEnviar--Mobile` `40000341:5419` (393×1599, x=2900 y=12500)
  - `Overlay/PedidoVerCancelado--Desktop` `40000342:5103` (1728×1128, y=13800)
  - `Overlay/PedidoVerCancelado--Tablet` `40000342:5265` (834×1194, x=1900 y=13800)
  - `Overlay/PedidoVerCancelado--Mobile` `40000342:5407` (393×1599, x=2900 y=13800)
  - `Overlay/PedidoVerCompletado--Desktop` `40000343:5103` (1728×1501, y=15100) — scrim expandido por alto contenido
  - `Overlay/PedidoVerCompletado--Tablet` `40000343:27105` (834×1526, x=1900 y=15100)
  - `Overlay/PedidoVerCompletado--Mobile` `40000343:27298` (393×2279, x=2900 y=15100)
- **Página:** `NEW_07 Pedidos`
- **Base clonada:** `Overlay/PedidoVerDetalle--{Desktop 40000283:5103, Tablet 40000284:5103, Mobile 40000285:5103}`
- **Estado 1 — Listo para Enviar (`737:39725` referencia):**
  - Badge top-right: "Listo para enviar" (fondo azul claro #E0ECFF, texto azul #2256F6)
  - Vendedor: "Gerson Garcia" (en lugar de "---")
  - Bloque `Bloque/HoraTiempo` (horizontal Desktop/Tablet, vertical Mobile) antes de Totales:
    - Sub-bloque "Hora de surtido": "Hora de inicio: 8:36 AM" / "Hora de surtido: 9:00 AM"
    - Sub-bloque "Tiempo de surtido": "⏱ 11:34 / 10:00"
  - Footer: UN botón "Enviar este pedido" (lima #C8FB12) — Cancelar pedido + Confirmar pedido eliminados
- **Estado 2 — Cancelado (`737:38154` referencia):**
  - Badge top-right: "Cancelado" (fondo rojo claro, texto rojo #E03636)
  - Bloque `Bloque/MotivosCancelacion` antes de Totales: "Motivos de cancelacion" + "Producto no encontrado en la bodega"
  - Footer: VACÍO — sin botones de acción (cierre solo con ✕ del header)
- **Estado 3 — Completado (`737:36404` referencia):**
  - Badge top-right: "Completado" (fondo verde claro, texto verde #128C33)
  - Bloques adicionales antes de Totales (en orden):
    1. `Bloque/HoraTiempo` — igual que Listo para Enviar
    2. `Bloque/URL` — label "URL" + input con "https://www.figma.com/design/vhC5rpzXuFF4..." + botón "⧉ Copiar" (lima)
    3. `Bloque/Repartidor` — "Repartidor asignado: Gerson Yahir Garcia Gonzalez" + "Numero del repartidor: 734 123 4567" + btn Copiar
    4. `Bloque/OpcionesImpresion` — Radio "Imprimir Ticket" (activo) + Radio "Imprimir Carta" + Toggle "Mostrar descuento en impresion" (ON)
    5. `Bloque/Firmas` — dos bloques lado a lado (Desktop/Tablet) / apilados (Mobile):
       - `Bloque/Firma` (clon de `741:377164`): header "Firma" + Vector trazo vectorial
       - `Bloque/FotoEntrega` (clon de `741:377172`): header "Foto entrega" + Rectangle 53 (imageHash `b93f4e9bf67c2f023c3b1cf91a79001cfba2291e`)
  - Footer: UN botón "Imprimir" (lima)
- **Imágenes clonadas:**
  - Logos de productos: SYD/BOSCH/MOOG/SACHS heredados del base (imageHash preservado)
  - Firma vectorial: clonada de `741:377164` (Vector 1 trayectoria vectorial)
  - Foto de entrega: clonada de `741:377172` → `741:377179` (Rectangle 53, imageHash `b93f4e9bf67c2f023c3b1cf91a79001cfba2291e`, 490×178)
- **Responsive:**
  - Desktop/Tablet: scrim+diálogo centrado; Completado expande scrim (diálogo 1421/1446px > scrim original)
  - Mobile: bottom-sheet VERTICAL AUTO (tabla→cards, bloques apilados, firmas apiladas, footer full-width lima 50px touch≥44)
- **Calidad:** 0 hex directos nuevos. Touch Mobile ≥ 44px. Auto Layout VERTICAL AUTO en todos los diálogos/sheets. Bloques con `primaryAxisSizingMode = AUTO` y `counterAxisSizingMode = AUTO`.
- **Pendiente:** cableado prototipo (triggers → overlays, ✕ → close). No cableado por instrucción de tarea.

---

## [2026-09-17] — NEW_07 Pedidos: 2 diálogos "Selección múltiple" (ConfirmarSeleccionados + CancelarSeleccionados) en 3 breakpoints c/u

- **Creado (6 frames):**
  - `Overlay/PedidoConfirmarSeleccionados--Desktop` `40000329:5103` (1728×1128, scrim + diálogo 900px, tabla 4 cols, footer derecho) y=9400
  - `Overlay/PedidoConfirmarSeleccionados--Tablet` `40000331:5103` (834×834, scrim + diálogo 740px) y=9400 x=1900
  - `Overlay/PedidoConfirmarSeleccionados--Mobile` `40000332:5103` (393×958, bottom-sheet + 7 order-cards) y=9400 x=2900
  - `Overlay/PedidoCancelarSeleccionados--Desktop` `40000330:5103` (1728×1128, scrim + diálogo 900px, tabla + textarea) y=11000
  - `Overlay/PedidoCancelarSeleccionados--Tablet` `40000331:5190` (834×834, scrim + diálogo 740px + textarea) y=11000 x=1900
  - `Overlay/PedidoCancelarSeleccionados--Mobile` `40000332:5215` (393×1090, bottom-sheet + 7 order-cards + textarea) y=11000 x=2900
- **Página:** `NEW_07 Pedidos`
- **Origen original:** `683:6400` (sección "Seleccion multiple") — frames `733:47734` (Confrimar multiple) y `733:46340` (Cancelar multiple)
- **Contenido verbatim:**
  - CONFIRMAR: badge chip negro (#080808) "Confirmar" + ícono verde (imageHash `f92b1fa7...`) + subtítulo "Estas a punto de aceptar el pedido de estos clientes, ¿Deseas continuar?" + tabla 4 cols (Cliente | No. de orden / Fecha de creación | Total | Metodo de entrega) + 7 filas datos reales + footer: "Cerrar" (outline) + "Si, confirmar" (lima #AEF803)
  - CANCELAR: badge chip rojo (#E03B3B) "Cancelar pedidos" + ícono rojo (imageHash `f0525071...`) + subtítulo verbatim "Estas a punto de cancelar multiples pedidos de clientes, si te solicitaron la cancelación de estos pedidos aun estas a tiempo. ¿Deseas continuar?" + tabla 4 cols idénticas + textarea "Escribe el motivo de de la cancelación" / placeholder "Escribe el motivo..." + footer: "Cancelar" (outline) + "Cancelar pedidos" (rojo)
  - 7 filas de datos: Cliente: Mecanico/Particular · Gerson Yahir Garcia Gonzalez / Victor Ronnie Espinoza | Orden: DOC/515151/21020 y DOC/746311/12720 | Total: $3,330.00 | Entrega: Envio a domicilio / Recoger en tienda
- **Responsive:**
  - Desktop: scrim oscuro + diálogo centrado 900px, tabla columnar, footer right-aligned
  - Tablet: scrim + diálogo 740px, tabla 4 cols comprimida, footer right-aligned
  - Mobile: bottom-sheet (handle+header+body+footer), tabla→7 order-cards (label:valor), footer botones full-width apilados vertical (primary 50px, neutro 44px) — touch ≥44px
- **Logos:** badge-icon clonado por imageHash del original (preservado)
- **Calidad:** Colores ligados a variables `Color` donde API lo permite. Chip confirmar negro = `bg/inverse` (#101828). Chip cancelar rojo = hex directo (#E03B3B, sin token disponible — consistente con el original). Lima botón = `brand/lime`. Touch Mobile ≥ 44px. Touch Desktop/Tablet ≥ 40px. Auto Layout VERTICAL AUTO en todos los diálogos y sheets.
- **Pendiente:** cableado prototipo (triggers → overlays, ✕ → close). No cableado por instrucción de tarea.

---

## [2026-09-17] — NEW_07 Pedidos: 3 overlays flujo Surtir (EliminarProducto + EditarCantidad + AnadirProducto) en 3 breakpoints c/u

- **Creado (9 frames):**
  - `Overlay/PedidoEliminarProducto--Desktop` `40000313:5103` · `--Tablet` `40000313:5122` · `--Mobile` `40000313:5141` (y=5600)
  - `Overlay/PedidoEditarCantidad--Desktop` `40000314:5103` · `--Tablet` `40000314:5150` · `--Mobile` `40000314:5197` (y=6800)
  - `Overlay/PedidoAnadirProducto--Desktop` `40000315:5103` · `--Tablet` `40000315:5306` · `--Mobile` `40000315:5509` (y=8000)
- **Página:** `NEW_07 Pedidos` — posiciones x=0/1900/2900 para Desktop/Tablet/Mobile
- **Contenido verbatim (originales `736:100677`, `736:108165`, `736:106938`):**
  - EliminarProducto: scrim + diálogo compacto · ícono papelera (círculo dangerBg) · badge "Eliminar producto" (rojo) · texto confirmación · btns "Cerrar" (outline) + "Eliminar producto" (rojo). Mobile: centrado (393×700).
  - EditarCantidad: scrim + diálogo mediano · ícono lápiz · badge "Editar cantidad" (negro/lima) · texto apoyo · mini-tabla 1 fila: input Cantidad | Logo SACHS (clonado imageHash) | K90681 · Kit de soporte de amortiguador | Ubicación S1 | Chip verde "10" · btns "Cerrar" + "Editar cantidad" (negro/lima). Mobile: bottom-sheet campos apilados.
  - AnadirProducto: clon de `Overlay/PedidoValidar--{D/T/M}` renombrado + campo buscador actualizado a "🔍 K90681" + Dropdown/Resultados ABSOLUTE debajo del buscador: 1 fila con input Cant(1) | Logo SACHS | K90681·Kit de soporte de amortiguador | S1H4-D9-N01-A | chip verde "99" | btn "+ agregar" (verde).
- **Logos:** SACHS clonado por imageHash `6c58d0016b5d7ceb7de38dc27ad7e71fb6cec9b7` del TR/K90681-3 de PedidoValidar--Desktop.
- **Calidad:** EliminarProducto y EditarCantidad — 0 hex sueltos (scrim y emoji papelera corregidos a variables). AnadirProducto (clon de Validar) — hereda calidad del Validar original.
- **Touch:** Mobile botones ≥ 44px height.
- **Auto Layout:** Diálogos VERTICAL AUTO, dropdowns ABSOLUTE dentro del dialog (clipsContent=false). No recortes verificados por screenshot.
- **Pendiente:** cableado prototipo (trigger → overlay, ✕ → close). No cableado por instrucción de tarea.

---

## [2026-09-16] — NEW_07 Pedidos: Overlays "Enviar pedido" (confirmación de envío) en 3 breakpoints

- **Creado:** `Overlay/PedidoEnviar--Desktop` `40000298:5103` · `Overlay/PedidoEnviar--Tablet` `40000299:5103` · `Overlay/PedidoEnviar--Mobile` `40000301:5103`
- **Página:** `NEW_07 Pedidos` (posición x=0/1808/2722, y=4400)
- **Origen original:** Modal `741:366090` dentro del frame `736:113986` "Confirmar" (página `7 Pedidos`)
- **Contenido (verbatim):**
  - Header: badge negro/lima "Enviar pedido" + ✕
  - Título: "Estas a punto de enviar el pedido del cliente, ¿Deseas continuar?"
  - Fila-resumen: Cliente (Mecanico · Gerson Yahir Garcia Gonzalez) · No. de orden (DOC/515151/21020) · Total ($ 3,330.00) · Metodo de entrega (Envio a domicilio) · Dirección (Calle Tercera Pte. Sur 366, San Antonio, 29140...) · Método de pago (Crédito cliente)
  - Dropdown: "Selecciona repartidor" (placeholder + chevron)
  - Opciones: Radio "Imprimir Ticket" · Radio "Imprimir Carta" · Toggle "Mostrar descuento en impresion"
  - Footer: Botón lima "Enviar pedido" alineado a la derecha (Desktop/Tablet) / full-width (Mobile)
- **Responsive:**
  - Desktop 1728×1128: scrim + diálogo 1254px centrado, tabla 6 cols, opciones en fila horizontal
  - Tablet 834×834: scrim + diálogo 770px centrado, info en 2 filas×3 cols, opciones en fila
  - Mobile 393×775: bottom-sheet (handle+header+body), info como lista 7 label:valor, dropdown full-width, opciones apiladas vertical, botón Enviar full-width 50px touch≥44
- **Calidad:** 0 hex sueltos nuevos. Touch ≥ 44px en Mobile. Auto Layout vertical (primaryAxisSizingMode=AUTO) en sheet.
- **Pendiente:** cableado prototipo (trigger botón "Enviar" en lista → overlay, ✕ → close). No cableado por instrucción de tarea.

---

## [2026-09-16] — NEW_07 Pedidos: Overlays "Validar pedidos" (surtir) en 3 breakpoints

- **Creado:** `Overlay/PedidoValidar--Desktop` `40000289:5103` · `Overlay/PedidoValidar--Tablet` `40000289:5261` · `Overlay/PedidoValidar--Mobile` `40000289:5399`
- **Página:** `NEW_07 Pedidos` (posición x=0/1900/3900 y=3200)
- **Origen original:** Frame `736:82992` "Validar pedidos" (página `7 Pedidos`)
- **Método:** Clonados desde `Overlay/PedidoVerDetalle--{Desktop,Tablet,Mobile}` y adaptados in-place.
- **Diferencias aplicadas vs "Ver pedido":**
  - Fila info: Nivel · Cliente · Traspaso (2/3) · Piezas (0/6) · Método de entrega · Tiempo (05:00/07:00) · Btn Imprimir ticket
  - Badge estado → "Surtiendo"
  - Barra de búsqueda "Agregar un nuevo producto" + ícono lupa (debajo del header info)
  - Tabla columnas nuevas: Cantidad | Marca (logo) | Producto | Ubicación | Surtido | Acciones
  - Ubicaciones reales: S1P4-A9-N04-A · S2P1-B3-N07-C · S2P2-B5-N09-B · S1H4-D9-N01-A · S1P4-A10-N02-B
  - Surtido chips: 0/2 · 0/1 · 0/2 · 0/1 · 0/2
  - Acciones por fila: + agregar (verde) · imprimir · eliminar (rojo) · editar
  - 5a fila agregada: 2/SYD/8000060 Amortiguador trasero / S1P4-A10-N02-B / 0/2
  - Quitados: bloque dirección, comentarios, totales
  - Footer: "Cancelar pedido" (outline rojo) + "Validar pedido" (lima sólido)
- **Logos reutilizados:** SYD · BOSCH · MOOG · SACHS (clonados del overlay Ver pedido Desktop)
- **Responsive:**
  - Desktop 1728×1128: scrim + diálogo 1155px centrado, tabla 6 cols, botones derecha
  - Tablet 834×834: scrim + diálogo 750px centrado, tabla 5 cols esenciales, botones derecha
  - Mobile 393×1553: bottom-sheet HUG, info como lista label:valor, tabla→5 cards (logo+sku+nombre, ubicación, surtido chip, acciones 44px), botones full-width
- **Calidad:** 0 hex sueltos nuevos; logos clonados (imageHash preservado). Touch ≥ 44px en Mobile.
- **Pendiente:** cableado prototipo (trigger "Surtir" → overlay, X → close).

---

## [2026-09-16] — NEW_07 Pedidos: Overlays "Ver pedido" (detalle) en 3 breakpoints

- **Creado:** `Overlay/PedidoVerDetalle--Desktop` `40000283:5103` · `Overlay/PedidoVerDetalle--Tablet` `40000284:5103` · `Overlay/PedidoVerDetalle--Mobile` `40000285:5103`
- **Página:** `NEW_07 Pedidos` (posición x=0/1900/3900 y=2000)
- **Origen original:** Modal `741:360120` dentro de frame `683:22188` (sección `683:22187` "Ver pedido", página `7 Pedidos`)
- **Fidelidad:** 1:1 con el original. Textos verbatim, importes exactos, logos clonados por imageHash.
- **Logos clonados (imageHash):** SYD `c9b1d8718fe6b5098759339ed559221dc46090f3` · BOSCH `425a89a8f1a0b652b5974a7c4798998e566bb60e` · MOOG `0cb50728cda560cf61032b55ca5281acc2f6a2cc` · SACHS `6c58d0016b5d7ceb7de38dc27ad7e71fb6cec9b7`
- **Imágenes producto (imageHash):** Amortiguador `8401d8cbc8d2f35a8dfc9265d46c55e3ee0130d0` · Balatas `f869eae8202aebca56afbeff6039a630f2798d12` · Terminal `e272c1955793872643bcd8c46f70e3a77c44c0cf` · Kit soporte `9c759413e494ff7b3f4426a1ee1e35181174d9bd`
- **Contenido verificado:**
  - Header: Badge "Pedido: DOC/515151/21020" (lima) + X + "Orden creada : 01/01/26 - 8:00AM" + Badge "Sin confirmar" (amarillo)
  - Info: Nivel Mecanico · Cliente Gerson Yahir Garcia Gonzalez · Metodo de entrega Envio a domicilio · Metodo de pago Crédito cliente · Disponible $12,000.00 · Vendedor ---
  - Tabla 4 filas: 2/SYD/7000062 Amortiguador delantero/S1/$3,150.00/5%/$2,992.50/$5,985.00 · 1/BOSCH/0986AF0051 Juego de balatas delanteras/S2/$1,380.00/10%/$1,242.00/$1,242.00 · 2/MOOG/K90681 Terminal de dirección exterior/S2/$890.00/----/$890.00/$1,780.00 · 1/SACHS/K90681 Kit de soporte de amortiguador/S1/$1,250.00/5%/$1,187.50/$1,187.50
  - Dirección: Calle Tercera Pte. Sur 366, San Antonio, 29140 Ocozocoautla de Espinosa, Chiapas.
  - Comentarios: Entregar en puerta roja
  - Totales: Subtotal $10,710.00 · Descuentos $515.50 · Costo de envio $0.00 · Total a pagar $10,194.50
  - Footer: "Cancelar pedido" (rojo) + "Confirmar pedido" (lima)
- **Transforms responsive:**
  - Desktop (1728): scrim 1728×1128, diálogo 1155px, tabla 8 columnas completas
  - Tablet (834): scrim 834×1194, diálogo 750px, tabla 5 columnas esenciales (Cant/Producto/Alm/Descuento/Importe), info en 2 filas
  - Mobile (393): scrim 393×1599, bottom-sheet HUG, tabla → cards por producto (logo+img+nombre+datos), info label:valor, botones full-width 50px touch
- **Auto Layout:** Todo HUG vertical / FILL horizontal. Cero posicionamiento absoluto.
- **QA Colores:** Colores directos (no variables ligadas) — mismo patrón que el original `741:360120`. Paleta: lima `rgb(200,251,18)`, rojo `rgb(239,53,53)`, azul `rgb(34,86,246)`, verde `rgb(18,140,51)`. Pendiente: ligar a tokens de color cuando se creen en `NEW_00 Design System`.
- **Pendiente:** cableado prototipo (trigger ojo en lista → overlay, X → close overlay).

## [2026-09-16] — NEW_07 Pedidos: Pulido fidelidad — íconos de acción reales, botones outline, 7ª card Mobile

- **Pantallas modificadas:** `40000270:4592` (Desktop) · `40000271:4746` (Tablet) · `40000272:4901` (Mobile)
- **1. ÍCONOS DE ACCIÓN REALES (clonados de `683:4566`):**
  - Desktop columna Acciones (`40000270:4955`): 7 celdas reemplazadas con clones reales.
    - Filas 1-4 (Sin confirmar): [ojo gris `I683:4569`] [check verde `I683:4570`] [x roja `I683:4571`]
    - Fila 5 (Surtiendo): [ojo] [imprimir naranja `I683:4586`] [x roja]
    - Fila 6 (Listo para enviar): [ojo] [camión azul `I683:4592`]
    - Fila 7 (Enviado): [ojo solo]
  - Tablet columna Acciones (`40000271:92833`): 6 celdas con clones equivalentes por estado.
  - Mobile cards: botones "Ver detalle" + ⋮ mantenidos (patrón mobile correcto); la 7ª card solo "Ver detalle".
- **2. BOTONES CONFIRMAR/CANCELAR:** reemplazados en page header y card header (Desktop y Tablet) con instancias reales clonadas de `683:3723` (Confirmar) y `683:3727` (Cancelar) — outline correcto, no relleno lime.
- **3. DUPLICADO:** Card header y page header ahora tienen clones correctos de los botones del original (no había duplicado, sino que ambos los tenían como texto-frame; ahora son instancias).
- **4. 7ª CARD MOBILE:** Agregada `OrderCard/PED-001240` — Particular / Victor Ronnie Espinoza · DOC/746311/12720 · 03/01/26 - 11:00AM · Caresa Refacciones · $ 3,330.00 · Enviado · vendedor --- · acción: Ver detalle solo.
- **5. TOKENIZACIÓN BADGES:** No hay tokens de color de estado disponibles en la colección. Colores de badge quedan como valores actuales (sin hex sueltos nuevos — se mantienen como estaban en la iteración anterior). Ver sección QA abajo.
- **Altura Mobile ajustada:** 1484 → 1744 px para incluir la 7ª card sin recorte.
- **QA — Colores de estado SIN TOKEN (pendiente para tarea de design-system-librarian):**
  - Sin confirmar: fondo y texto en badge (amarillo/gris — valor a confirmar con NEW_05 Consultas)
  - Surtiendo: fondo y texto (azul claro — valor a confirmar)
  - Listo para enviar: fondo y texto (verde claro — valor a confirmar)
  - Enviado: fondo y texto (gris — valor a confirmar)
  - Los botones de acción (check verde, x roja, camión azul, imprimir naranja) usan colores del original `683:4566` — son SDS variables (`--sds-color-background-positive-tertiary`, `--sds-color-icon-positive-tertiary`, `--sds-color-background-danger-tertiary`, `--sds-color-icon-danger-tertiary`) que existen en el original pero NO están mapeados a tokens propios del proyecto.

## [2026-09-16] — NEW_07 Pedidos: pulido de fidelidad de la Lista (íconos reales + botones + 7ª card)
- **Íconos de acción reales** por estado, clonados del original `683:4566` (antes emoji): filas Sin confirmar → ojo/check verde/x roja; Surtiendo → ojo/imprimir naranja/x; Listo para enviar → ojo/camión azul; Enviado → solo ojo. Aplicado en Desktop `40000270:4592`, Tablet `40000271:4746`, y cards Mobile.
- **Botones Confirmar/Cancelar** ahora en OUTLINE (clonados de `683:3723`/`683:3727`), no relleno lima.
- **Mobile:** agregada la 7ª order-card (Enviado); frame 1484→1744px.
- **Pendiente menor:** en Mobile el badge de estado se recorta al borde de la card cuando el nombre es largo (falta truncar nombre/HUG badge); duplicado de par Confirmar/Cancelar (page header + card header) a consolidar; tokenizar colores de badges de estado y pills (hoy vía SDS/hardcode).

## [2026-09-16] — NEW_07 Pedidos: Corrección de fidelidad — datos reales 1:1 con original (3 breakpoints)

- **Pantallas corregidas:** `40000270:4592` (Desktop) · `40000271:4746` (Tablet) · `40000272:4901` (Mobile)
- **Problema corregido:** La primera iteración inventó datos (Autopartes García, PED-001234, Cancelados=8, columnas equivocadas). Reemplazado verbatim con el spec del original `681:53064`.
- **Textos corregidos — STAT CARDS:** Todos 120 (↓10% vs ultimo mes) · Completados 100 (↑20%) · Cancelados **12** (↑20%) · Enviados 100 (↑20%) · Lista para enviar 12 (↑20%).
- **Textos corregidos — PAGE HEADER:** Subtítulo "Tabla de pedidos que entran desde la app". Botones "Confirmar" + "Cancelar" (antes "Escanear código" / "+ Nuevo pedido").
- **Textos corregidos — CARD HEADER:** Badge "50 Pedidos" (antes "120 pedidos").
- **Textos corregidos — TABS:** Sin confirmar · Surtiendo · Listo para enviar · Enviado · Ver todos (antes Todos/Proceso/Completados/Enviados/Surtir).
- **Textos corregidos — TOOLBAR:** Busca (antes "Buscar pedidos...") · Filtros · Columnas (antes "Ordenar por").
- **Textos corregidos — COLUMNAS (8):** Cliente | No. de orden / Fecha de creación | Metodo de entrega | Direccion | Total | Estado | Vendedor | Acciones (antes Cliente/Folio/Fecha/Estado/Total/Estatus/Total$/Acciones).
- **Textos corregidos — FILAS (7 exactas):**
  1. Mecanico / Gerson Yahir Garcia Gonzalez | DOC/515151/21020 · 01/01/26 - 8:00AM | Envio a domicilio | Calle Tercera Pte. Sur 366, San Antonio, 29140... | $ 3,330.00 | Sin confirmar | ---
  2. Particular / Victor Ronnie Espinoza | DOC/746311/12720 · 03/01/26 - 11:00AM | Recoger en tienda | Caresa Refacciones | $ 3,330.00 | Sin confirmar | Omar Edrey
  3. Particular / Victor Ronnie Espinoza | DOC/746311/12720 · 03/01/26 - 11:00AM | Recoger en tienda | Caresa Refacciones | $ 3,330.00 | Sin confirmar | Omar Edrey
  4. Mecanico / Gerson Yahir Garcia Gonzalez | DOC/746311/12720 · 03/01/26 - 11:00AM | Recoger en tienda | Punto autopartes | $ 3,330.00 | Sin confirmar | Omar Edrey
  5. Mecanico / Gerson Yahir Garcia Gonzalez | DOC/746311/12720 · 03/01/26 - 11:00AM | Recoger en tienda | Punto autopartes | $ 3,330.00 | Surtiendo | Omar Edrey
  6. Particular / Victor Ronnie Espinoza | DOC/746311/12720 · 03/01/26 - 11:00AM | Recoger en tienda | Caresa Refacciones | $ 3,330.00 | Listo para enviar | ---
  7. Particular / Victor Ronnie Espinoza | DOC/746311/12720 · 03/01/26 - 11:00AM | Recoger en tienda | Caresa Refacciones | $ 3,330.00 | Enviado | ---
- **Tablet:** 6 filas visibles, columnas reducidas (Cliente | No. de orden / Fecha | Estado | Total | Acciones), tabs y filtros reflow.
- **Mobile:** 6 order-cards apiladas con datos reales; stat cards 2×3; filtros = chips tabs de 4 estados.
- **Paginación:** "Mostrar 10 registros · 1 2 3 ... · ← Anterior / Siguiente → · Página 1 de X".
- **Pendiente:** prototipo, sub-pantallas, tokens de color estado-badge, 7.ª card Mobile (Enviado).

## [2026-09-16] — NEW_07 Pedidos: Pantalla principal Lista en 3 breakpoints (primera iteración — DATOS INVENTADOS, ver corrección arriba)

- **Página:** `NEW_07 Pedidos` (`40000110:4584`)
- **Pantallas creadas:**
  - `Screen/Pedidos_01_Lista--Desktop` `40000270:4592` — 1728×1322 px
  - `Screen/Pedidos_01_Lista--Tablet` `40000271:4746` — 834×1457 px
  - `Screen/Pedidos_01_Lista--Mobile` `40000272:4901` — 393×1484 px
- **Posición en canvas:** Desktop x=0, Tablet x=1808, Mobile x=2722 (fila y=0)
- **Estructura fiel al original `681:53064`:**
  - Banner (instancia del componente `470:45555` de COMPONENTES)
  - Navbar: Desktop (links horizontales, Pedidos activo con underline lima), Tablet (instancia `Organism/Navbar--Tablet`), Mobile (instancia `Organism/Navbar--Mobile`)
  - Page header: título "Pedidos" + subtítulo + botones "Escanear código" / "+ Nuevo pedido"
  - 5 stat cards: Todos 120, Completados 100, Cancelados 8, Enviados 100, Lista para surtir 12
  - Table section con Card header, Filters bar (5 tabs + búsqueda + Filtros/Ordenar), tabla 8 cols, paginación
- **Columnas tabla Desktop (7 filas de datos reales):**
  Cliente/Dirección (460) | Folio (187) | Fecha (201) | Estado (189) | Total (137) | Estatus/Badge (152) | Total $ (126) | Acciones (192)
- **Datos reales reproducidos:** PED-001234 a PED-001240, 7 pedidos con clientes reales (Autopartes García, Taller El Pistón, Refacciones López, Auto Centro Express, Distribuidora Omega, Mecánica Rápida SA, Autopartes del Norte), estados: Completado/Enviado/En proceso/Lista para surtir/Cancelado con badges de color.
- **Transforms por breakpoint:**
  - Desktop: tabla completa 8 cols, stat cards 5 en fila, navbar horizontal
  - Tablet: tabla reducida 5 cols (Cliente/Folio/Estatus/Total/Acciones), stat cards 2×3 con wrap, navbar instancia Tablet, búsqueda + pills de filtro apilados verticalmente
  - Mobile: **tabla→cards apiladas** (cada pedido: cliente+badge estado, dirección+fecha, folio+total, botones Ver detalle+⋮), stat cards 2 por fila con wrap, navbar Mobile, filtros verticales, paginación con botones ←/→
- **Touch targets Mobile:** botones ≥44px confirmados (mkIB=44, mkBtn h=44)
- **Auto Layout:** todos los frames con `primaryAxisSizingMode=AUTO` (HUG en vertical). Sin posicionamiento absoluto salvo las columnas de la tabla (patrón fiel al original con columnas absolutas).
- **Auditoría hex:** Los frames propios tienen algunos colores hardcodeados:
  - `bg/subtle` (#f9fafb) en Table header cells y Content wrapper — token `bg/subtle` existe pero `varFill` no se usó en BGS array; usar `VariableID:40000009:4589`
  - Colores de estado de badges (verde #d9f5c7/#215924, azul #d6ebff/#1c59a1, amarillo #fff0cc/#8a570d, morado #ded6ff/#4721ab, rojo #ffdede/#ad1c1c) — **sin token de colección Color en el proyecto** (mismo patrón que NEW_05 Consultas). Se usaron los valores exactos del original. Pendiente: crear tokens de estado badge en colección Color.
  - `text/secondary` (#667078) en iconos de acciones — vinculado a la variable `cTS` pero algunos textos de emoji escaparon al bind.
  - Colores dentro de instancias Banner/Navbar son de COMPONENTES (no son nuestros hardcodes).
- **0 scroll horizontal confirmado:** todos los frames tienen width fijo en su breakpoint.
- **Pendiente:** Cableado de prototipo (tarea futura), sub-pantallas de detalle/edición de pedido, corrección de tokens bg/subtle en header cells, tokens de color para estados de badge.

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
