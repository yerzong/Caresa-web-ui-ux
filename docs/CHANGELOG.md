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
