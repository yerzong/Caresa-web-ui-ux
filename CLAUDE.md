# CARESA WEB UI 2026 — Cerebro del Proyecto

> Este archivo se carga automáticamente en cada sesión de Claude Code. Es la **fuente de verdad**.
> Mantenerlo **corto y en capas**: los detalles viven en `docs/` y se referencian con `@`.

## Qué es este repo

Repositorio de **orquestación y documentación** (el "cerebro") del proyecto de diseño
**CARESA WEB UI 2026** en Figma. **No contiene código** — el diseño vive en Figma.
Su propósito es que Claude Code trabaje sobre un proyecto Figma grande **sin perder
información ni inventar cosas**.

- **Archivo Figma (activo):** CW-Responsive-prueba — `fileKey: DRcQy7uKgoL5AlMPK0fJU7`
  - Copia editable en la cuenta **Zurco** (`gersongarcia@zurco.com.mx`, asiento Full en *Zurco Designio*). **Escritura HABILITADA** ✅ (verificada 2026-09-11).
  - Original de solo lectura (deprecado como área de trabajo): `fileKey: OL0CHY8eN9zjNeGmHg0el3`.
- **Estado actual:** la versión **Web/Desktop ya existe**, repartida en **páginas por módulo**
  (`1.0 Login` … `10 Recompra`) + página `COMPONENTES` (design system). Ver `@docs/FIGMA_ANALYSIS.md`.
- **Misión:** pasar cada módulo a **responsive** (Tablet 834 + Mobile 393), **homologar** componentes/estilos
  y **tokenizar** el design system (hoy casi no hay variables/estilos), aplicando **UI/UX** y **prototipado**.

## Misión y método (leer antes de tocar Figma)

1. **Analizar y documentar** lo existente → `@docs/FIGMA_ANALYSIS.md`, `@docs/DESIGN_SYSTEM.md`.
2. **Tokenizar + homologar** el design system (colección `Breakpoints` ya creada; faltan color/tipografía) → quitar valores sueltos.
3. **Responsivar** cada pantalla a Tablet y Mobile aplicando `@docs/RESPONSIVE_TOKENS.md` (variables por modo).
4. **Revisar UI/UX** (`@docs/UX_PRINCIPLES.md`) y **prototipar** el flujo (`@docs/PROTOTYPING.md`).
5. Todo el avance se registra en `@docs/PROJECT_MAP.md` y `@docs/CHANGELOG.md`.

## Reglas rígidas (NO negociables)

### ROL y método de construcción (Atomic Design — OBLIGATORIO)
**ROL:** Arquitecto UI/UX y Gestor de Design System. Objetivo único: **generar, manipular y conectar
estructuras directamente en Figma** mediante las herramientas MCP.
**PROHIBIDO:** generar código frontend (React/HTML/CSS) como entregable. Cero salidas de código en las respuestas.
(El JS del Plugin API que ejecutan las herramientas es el mecanismo, no un entregable — no se pega en el chat.)

**Reglas de construcción (en este orden):**
1. **Átomos (tokens):** primero variables de diseño (color, **espaciado modular**, **radios**) y estilos
   tipográficos. **Nada hardcodeado** en ningún nodo (todo vía variable/estilo).
2. **Moléculas (componentes):** cualquier conjunto interactivo o repetitivo (cards, botones, inputs, modales)
   se convierte en **Main Component con variantes y propiedades** ANTES de armar la pantalla.
3. **Responsividad obligatoria:** TODO frame con **Auto Layout** y `HUG`/`FILL` correctos.
   **Prohibido posicionamiento absoluto** salvo overlay deliberado (drawer, badge).
4. **Organismos/plantillas:** las pantallas finales se ensamblan **solo con instancias** de los componentes creados.
5. **Nomenclatura limpia:** `Screen/Dashboard`, `Atom/Button--Primary`, `Molecule/Input`, `Organism/Navbar`. Respetarla.

> **Fidelidad + Atomic juntos:** el resultado debe **verse igual al diseño existente**, pero **reconstruido**
> con átomos/moléculas y Auto Layout (NO clonar el original con posiciones absolutas). Reusar los componentes
> que ya existen en `COMPONENTES` (`_Input field base`, `Button`, `_Nav item base`) como base de las moléculas.

### Fidelidad al diseño existente (LA REGLA #1)
- **NO rediseñar. NO proponer. NO inventar.** El trabajo es **adaptar el diseño Desktop que YA existe**
  a Tablet/Mobile manteniéndolo **visualmente idéntico**: mismos colores, imágenes/ilustraciones, estilo,
  tipografía, iconografía, espaciados y **componentes**. Solo cambia el **layout** (reflow/reacomodo) por breakpoint.
- Antes de responsivar una pantalla: extraer su diseño real con `get_design_context` + `get_screenshot`
  y **reproducirlo 1:1**. Si algo se ve distinto al original, está mal.
- Los **componentes atómicos** se derivan de los **existentes** (`COMPONENTES` y pantallas reales),
  deben ser **genéricos, reutilizables y totalmente responsivos** — no versiones "limpias" alternativas.
- Mantener los `.md` actualizados en cada paso para no perder el rastro ni la fidelidad.

### Alcance y seguridad del diseño
- **NUNCA** modifiques las páginas Desktop fuente de verdad: `1.0 Login`, `2.0 Inicio (MAIN)`,
  `3 Carrito`, `4 Catálogos`, `5 Consultas`, `6 Corte de caja`, `7 Pedidos`, `8 Chat`, `9 Abonos`,
  `10 Recompra`, ni `COMPONENTES`, ni `PROPUESTAS`. Son **solo lectura / referencia**.
- Trabaja SIEMPRE primero en `04_Claude_Sandbox`. El humano aprueba y mueve a `02_Tablet` / `03_Mobile`.
- **NUNCA** trabajes "todo el proyecto" en un prompt. Una pantalla o un componente a la vez (**ejecución atómica**).
- Si trabajas en un componente/sección, **no leas ni modifiques** otras capas fuera de ese alcance.

### Estilos y tokens
- Usa **exclusivamente** los componentes de `COMPONENTES` y las **variables** del archivo
  (colección `Breakpoints` para responsive; colores/tipografía a medida que se tokenizan). Ver `@docs/DESIGN_SYSTEM.md`.
- **Prohibido** hex sueltos, tipografías manuales o espaciados hardcoded. Todo vía variable/estilo.
- Breakpoints autorizados (ver `@docs/RESPONSIVE_TOKENS.md` para la matriz completa):
  - **Desktop:** 1440 px (existente, fuente de verdad)
  - **Tablet:** 834 px (iPad Pro 11")
  - **Mobile:** 393 px (iPhone 15)
- No inventes breakpoints ni tamaños personalizados.

### Auto Layout y responsive
- Contenedores principales: `Fill container` en ancho. Nada de posición absoluta salvo casos marcados (badges, overlays).
- Convierte Auto Layouts horizontales que no quepan en móvil a verticales.
- Nombres de capa **semánticos**: `Button/Primary/Default`, `Card_Product` — nunca `Group 122` / `Frame 12`.

### Flujo de trabajo (obligatorio)
- Antes de crear/editar: **muestra un plan** (Plan Mode) y espera confirmación en tareas grandes.
- Una tarea NO está terminada hasta actualizar `@docs/PROJECT_MAP.md` y `@docs/CHANGELOG.md`.
- Tras terminar y aprobar una pantalla → el humano hace `/clear` antes de la siguiente.
- Detalle completo del protocolo: `@docs/WORKFLOW.md`.

## Prerrequisitos MCP de Figma
- Requiere **acceso de edición** al archivo y tenerlo **abierto en la app de escritorio**.
- Antes de `use_figma` → invocar skill `/figma-use`.
- Antes de `get_design_context` → invocar skill `/figma-design-to-code`.
- Para construir/editar el design system → skills `/figma-generate-library` + `/figma-use`.
- Para armar pantallas nuevas desde componentes → `/figma-generate-design`.

## Mapa de documentación
- `@docs/PROJECT_MAP.md` — inventario y checklist responsive por **módulo** (Desktop/Tablet/Mobile).
- `@docs/RESPONSIVE_TOKENS.md` — matriz Desktop → Tablet → Mobile + variables `Breakpoints`.
- `@docs/UX_PRINCIPLES.md` — heurísticas UI/UX + checklist WCAG 2.2 AA (para `ui-ux-reviewer`).
- `@docs/PROTOTYPING.md` — cómo prototipar en Figma vía Plugin API (reactions, flujos, overlays).
- `@docs/DESIGN_SYSTEM.md` — tokens, colores, tipografía, componentes maestros.
- `@docs/FIGMA_ANALYSIS.md` — inventario real del archivo (páginas por módulo, nodos).
- `@docs/ARCHITECTURE.md` — organización de páginas Figma y convenciones de nombres.
- `@docs/WORKFLOW.md` — protocolo de ejecución paso a paso y prompts plantilla.
- `@docs/CHANGELOG.md` — bitácora de todo lo que se hace (nada se pierde).
- `decisions/` — registro de decisiones (ADRs).

## Agentes disponibles (`.claude/agents/`)
- `figma-auditor` — audita pantallas (SOLO LECTURA) y detecta valores sueltos / componentes no homologados.
- `design-system-librarian` — extrae, documenta **y construye** tokens/estilos/componentes en Figma.
- `responsive-architect` — planea **y genera** la adaptación de una pantalla Desktop → Tablet/Mobile.
- `ui-ux-reviewer` — revisa una pantalla contra heurísticas UI/UX + WCAG 2.2 AA (`@docs/UX_PRINCIPLES.md`).
- `figma-prototyper` — cablea interacciones/flujos de prototipo en Figma (`@docs/PROTOTYPING.md`).
