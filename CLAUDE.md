# CARESA WEB UI 2026 — Cerebro del Proyecto

> Este archivo se carga automáticamente en cada sesión de Claude Code. Es la **fuente de verdad**.
> Mantenerlo **corto y en capas**: los detalles viven en `docs/` y se referencian con `@`.

## Qué es este repo

Repositorio de **orquestación y documentación** (el "cerebro") del proyecto de diseño
**CARESA WEB UI 2026** en Figma. **No contiene código** — el diseño vive en Figma.
Su propósito es que Claude Code trabaje sobre un proyecto Figma grande **sin perder
información ni inventar cosas**.

- **Archivo Figma:** CARESA WEB UI 2026 — `fileKey: OL0CHY8eN9zjNeGmHg0el3`
- **Estado actual:** la versión **Web/Desktop ya existe**.
- **Misión:** pasar todo a **responsive** (Tablet + Mobile) y **homologar componentes y estilos**.

## Misión y método (leer antes de tocar Figma)

1. **Analizar y documentar** lo existente → `@docs/FIGMA_ANALYSIS.md`, `@docs/DESIGN_SYSTEM.md`.
2. **Homologar** estilos y componentes de la versión Web (quitar valores sueltos/hardcoded).
3. **Responsivar** cada pantalla a Tablet y Mobile aplicando `@docs/RESPONSIVE_TOKENS.md`.
4. Todo el avance se registra en `@docs/PROJECT_MAP.md` y `@docs/CHANGELOG.md`.

## Reglas rígidas (NO negociables)

### Alcance y seguridad del diseño
- **NUNCA** modifiques las pantallas de la página `01_Web_Final`. Es **solo lectura**.
- Trabaja SIEMPRE primero en `04_Claude_Sandbox`. El humano aprueba y mueve a la página final.
- **NUNCA** trabajes "todo el proyecto" en un prompt. Una pantalla o un componente a la vez (**ejecución atómica**).
- Si trabajas en un componente/sección, **no leas ni modifiques** otras capas fuera de ese alcance.

### Estilos y tokens
- Usa **exclusivamente** los estilos globales y variables de la página `00_Design_System`.
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
- `@docs/PROJECT_MAP.md` — inventario y checklist de pantallas/flujos (Web/Tablet/Mobile).
- `@docs/RESPONSIVE_TOKENS.md` — matriz de homologación Web → Tablet → Mobile.
- `@docs/DESIGN_SYSTEM.md` — tokens, colores, tipografía, componentes maestros.
- `@docs/FIGMA_ANALYSIS.md` — análisis crudo del archivo (estructura de páginas y nodos).
- `@docs/ARCHITECTURE.md` — organización de páginas Figma y convenciones de nombres.
- `@docs/WORKFLOW.md` — protocolo de ejecución paso a paso y prompts plantilla.
- `@docs/CHANGELOG.md` — bitácora de todo lo que se hace (nada se pierde).
- `decisions/` — registro de decisiones (ADRs).

## Agentes disponibles (`.claude/agents/`)
- `figma-auditor` — audita pantallas y detecta valores sueltos / componentes no homologados.
- `design-system-librarian` — extrae y documenta tokens, estilos y componentes maestros.
- `responsive-architect` — planea la adaptación de una pantalla Web → Tablet/Mobile.
