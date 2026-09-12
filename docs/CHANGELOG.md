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

## [2026-09-12] — CORRECCIÓN DE RUMBO: fidelidad al diseño existente
- **Feedback del usuario:** lo generado (Login/Inicio responsive) se desvió a un **rediseño/propuesta**;
  el objetivo es **adaptar el diseño existente idéntico**, no inventar. Los borradores previos quedan como desechables.
- **Regla de fidelidad** añadida a `CLAUDE.md` (#1) y método clone-and-reflow en `WORKFLOW.md`.
- **Login Mobile fiel** (`40000064:4663`): clon del Desktop real `664:13013` reacomodado — conserva gradiente+textura,
  logo, headline, stepper con íconos 3D, inputs con ícono (mail/lock)+sombra, botón lima con glow, link subrayado.
  Base fiel Desktop en sandbox: `40000062:4582`.
- **Pendiente:** afinar wrap de subtítulo y ancho del stepper; decidir tratamiento de la ilustración 3D en móvil;
  Tablet fiel; usar componentes EXISTENTES como átomos; **reemplazar** los borradores desviados (Login/Inicio previos).

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
