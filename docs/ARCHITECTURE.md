# Arquitectura del Archivo Figma

Cómo se organiza el archivo de trabajo (`DRcQy7uKgoL5AlMPK0fJU7`) para trabajar con Claude Code
de forma contenida y segura. El objetivo es limitar el "campo de visión" de Claude por página.

## Estructura de páginas (real)

| Página | Rol | Permiso para Claude |
|---|---|---|
| `COMPONENTES` | Design system (componentes maestros) | **Solo lectura** (salvo tarea explícita de librarian) |
| `1.0 Login` … `10 Recompra` | Pantallas Desktop existentes (fuente de verdad) | **Solo lectura — NUNCA modificar** |
| `PROPUESTAS` | Exploraciones antiguas (referencia) | **Solo lectura** |
| `02_Tablet` | Pantallas responsive Tablet aprobadas | Escritura (mover desde sandbox) |
| `03_Mobile` | Pantallas responsive Mobile aprobadas | Escritura (mover desde sandbox) |
| `04_Claude_Sandbox` | Zona de generación y pruebas | **Escritura libre** |

> No existe una página `00_Design_System` separada: el design system vive en `COMPONENTES`
> (componentes) + las **variables globales** del archivo (colección `Breakpoints` y tokens de color/tipografía a crear).
> Las variables de Figma son **globales al archivo**, no dependen de una página.

## Variables (colecciones)
- **`Breakpoints`** — modos `Desktop` / `Tablet` / `Mobile`; números de layout y tipografía (ver `RESPONSIVE_TOKENS.md`).
- **`Colección de variables`** (previa) — 2 colores (`primary-Caressa`, `False-Default`). A consolidar en el set de color.
- **(pendiente)** colección de **color** y de **tipografía** semánticas.

## Convención de nombres

### Frames de pantalla responsive (en sandbox / Tablet / Mobile)
`{Device} - {Módulo}_{NN}_{Nombre}`
Ej.: `Mobile - Login_01_Acceso`, `Tablet - Inicio_01_Home`, `Mobile - Carrito_02_Resumen`

### Capas / componentes
Semántico y jerárquico, estilo design system:
- `Button/Primary/Default`, `Button/Primary/Hover`
- `Input/Text/Default`, `Card_Product`, `Navbar/Desktop`, `Sidebar/Mobile`
- **Prohibido**: `Group 122`, `Frame 12`, `Rectangle 4`.

## Reglas de contención
- Claude trabaja en **una página / un módulo / una pantalla a la vez**.
- Genera en `04_Claude_Sandbox`; el humano aprueba y mueve a `02_Tablet` / `03_Mobile`.
- El design system (`COMPONENTES` + variables) se toca solo con `design-system-librarian` y tarea explícita.
- Para módulos grandes (Inicio, Pedidos, Carrito): dividir por **pantalla/sección**, nunca el board completo.
