# Arquitectura del Archivo Figma

Cómo se organiza el archivo **CARESA WEB UI 2026** para trabajar con Claude Code de forma
contenida y segura. El objetivo es limitar el "campo de visión" de Claude por página.

## Estructura de páginas propuesta

> ⏳ Ajustar a la estructura real tras el análisis. Estructura objetivo:

| Página | Rol | Permiso para Claude |
|---|---|---|
| `00_Design_System` | Tokens, estilos, componentes maestros | **Solo lectura** (salvo tarea explícita de librarian) |
| `01_Web_Final` | Pantallas Desktop existentes (fuente de verdad) | **Solo lectura — NUNCA modificar** |
| `02_Tablet` | Pantallas responsive Tablet aprobadas | Escritura (mover desde sandbox) |
| `03_Mobile` | Pantallas responsive Mobile aprobadas | Escritura (mover desde sandbox) |
| `04_Claude_Sandbox` | Zona de generación y pruebas | **Escritura libre** |

## Convención de nombres

### Frames de pantalla
`{Device} - {Flujo}_{NN}_{Nombre}`
Ej.: `Mobile - Auth_01_Login`, `Tablet - Core_01_Home`

### Capas / componentes
Semántico y jerárquico, estilo design system:
- `Button/Primary/Default`, `Button/Primary/Hover`
- `Input/Text/Default`, `Card_Product`, `Navbar/Desktop`, `Navbar/Mobile`
- **Prohibido**: `Group 122`, `Frame 12`, `Rectangle 4`.

## Reglas de contención
- Claude trabaja en **una página a la vez**.
- Genera en `04_Claude_Sandbox`; el humano aprueba y mueve a la página final.
- El design system (`00_`) se toca solo con el agente `design-system-librarian` y tarea explícita.

## Estado actual del archivo
> ⏳ Pendiente de análisis (bloqueado por acceso de edición al archivo Figma).
> Documentar aquí: páginas reales, número de pantallas, y brechas contra esta estructura objetivo.
