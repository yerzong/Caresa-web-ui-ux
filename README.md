# CARESA WEB UI 2026 — Cerebro del Proyecto

Repositorio de **orquestación y documentación** para el proyecto de diseño
**CARESA WEB UI 2026** en Figma. Aquí **no hay código**: el diseño vive en Figma y este
repo es la "memoria" que evita que el trabajo se pierda o se degrade cuando el proyecto crece.

## Objetivo

La versión **Web/Desktop ya existe** en Figma. La misión es:

1. **Analizar y documentar** todo lo que ya está hecho.
2. **Homologar** componentes y estilos (eliminar valores sueltos).
3. Pasar el proyecto a **responsive** (Tablet 834 px y Mobile 393 px).

## Cómo se usa

Este repo se abre con **Claude Code** dentro de esta carpeta. Claude lee `CLAUDE.md`
automáticamente y sigue las reglas y el protocolo definidos aquí.

Flujo de una sesión típica:

1. `git pull` (traer el estado más reciente del cerebro).
2. Abrir el archivo de Figma en la **app de escritorio** (con acceso de edición).
3. Pedir a Claude una tarea **atómica** (una pantalla / un componente).
4. Claude trabaja en la página `04_Claude_Sandbox` de Figma.
5. Revisar y aprobar → mover el frame a la página final.
6. Claude actualiza `PROJECT_MAP.md` y `CHANGELOG.md` → **commit** → `/clear`.

## Estructura

```
CLAUDE.md              # Fuente de verdad (reglas + índice)
docs/
  PROJECT_MAP.md       # Inventario y checklist de pantallas
  RESPONSIVE_TOKENS.md # Matriz de homologación Web→Tablet→Mobile
  DESIGN_SYSTEM.md     # Tokens, colores, tipografía, componentes
  FIGMA_ANALYSIS.md    # Análisis del archivo Figma
  ARCHITECTURE.md      # Páginas de Figma y convenciones
  WORKFLOW.md          # Protocolo de ejecución + prompts plantilla
  CHANGELOG.md         # Bitácora de cambios
.claude/agents/        # Subagentes especializados
decisions/             # Registro de decisiones (ADRs)
```

## Estado

- [ ] Acceso de edición al archivo Figma confirmado
- [ ] Análisis inicial del archivo (`FIGMA_ANALYSIS.md`)
- [ ] Design System documentado (`DESIGN_SYSTEM.md`)
- [ ] Matriz responsive definida (`RESPONSIVE_TOKENS.md`)
- [ ] Estructura de páginas Figma creada
- [ ] Migración responsive por flujo (ver `PROJECT_MAP.md`)

> Repo mantenido con Claude Code. Push manual vía GitKraken (cuenta personal).
