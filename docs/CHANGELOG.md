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
