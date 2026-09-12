# ADR 0001 — Estructura de páginas Figma y método de trabajo

- **Fecha:** 2026-09-11
- **Estado:** Aceptado (provisional, ajustar tras análisis del archivo)

## Contexto
Proyecto 100% Figma (CARESA WEB UI 2026). La versión Web/Desktop ya existe. Hay que pasarlo a
responsive (Tablet, Mobile) y homologar componentes/estilos. En proyectos Figma grandes, Claude
Code satura contexto y degrada/inventa diseños. Necesitamos un método determinista.

## Decisión
1. **Repo "cerebro"** de documentación (sin código) como memoria persistente del proyecto.
2. **Estructura de páginas Figma** con aislamiento de contexto:
   `00_Design_System`, `01_Web_Final` (solo lectura), `02_Tablet`, `03_Mobile`, `04_Claude_Sandbox`.
3. **Ejecución atómica**: una pantalla/componente por tarea; generar en sandbox; humano aprueba y mueve.
4. **Homologar antes de responsivar**: quitar valores sueltos y usar componentes maestros.
5. **Higiene de contexto**: `/clear` entre pantallas; docs como memoria; commits atómicos.
6. **Agentes especializados**: `figma-auditor`, `design-system-librarian`, `responsive-architect`.

## Consecuencias
- (+) Trabajo trazable, reversible (git) y resistente a alucinaciones.
- (+) La versión Web original queda protegida.
- (−) Requiere disciplina del humano (aprobar/mover frames, `/clear`).
- Pendiente: validar que la estructura de páginas propuesta encaje con el archivo real.

## Alternativas consideradas
- Trabajar todo en una página → descartado (satura contexto, mezcla diseños).
- Migrar a código (React/Tailwind) → fuera de alcance por ahora (proyecto es solo Figma).
