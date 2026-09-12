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
