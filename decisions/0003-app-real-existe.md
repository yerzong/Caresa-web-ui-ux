# ADR 0003 — La app Desktop real ya existe (supera el "PASO 0" del ADR 0002)

- **Fecha:** 2026-09-11
- **Estado:** Aceptado (supersede parcialmente ADR 0002)

## Contexto
El ADR 0002 asumía que el archivo era **solo `PROPUESTAS`** (variantes en competencia) y planteaba un
"PASO 0: elegir la propuesta ganadora" antes de responsivar. Esa premisa era **incorrecta**: se debió a
que `get_metadata` sin `nodeId` solo listaba la página `PROPUESTAS`.

Al inspeccionar con el Plugin API (copia editable `DRcQy7uKgoL5AlMPK0fJU7`) se confirmó que el archivo
contiene la **app Desktop completa** repartida en páginas por módulo (`1.0 Login` … `10 Recompra`),
una página `COMPONENTES` (design system) y `PROPUESTAS` (solo exploraciones).

## Decisión
1. **La fuente de verdad Desktop son las páginas de módulo** (no `PROPUESTAS`). `PROPUESTAS` queda como referencia.
2. **Se retoma la misión original:** homologar + tokenizar + responsivar cada módulo a Tablet/Mobile.
   El "elegir propuesta" del ADR 0002 **ya no aplica** (la app ya tomó su dirección: login real + dashboards por módulo).
3. **Design system:** vive en `COMPONENTES` + variables globales. Está **casi sin tokenizar**
   (0 estilos de color/texto) → tokenizar color (marca `primary-Caressa` verde/lima + neutrales + semánticos)
   y tipografía (Inter) es Fase 0.
4. **Responsive:** se habilita con la colección **`Breakpoints`** (modos Desktop/Tablet/Mobile) ya creada.
5. **Se conservan** de ADR 0002: base de componentes tipo Untitled UI, migrar restos SDS a la base única.

## Consecuencias
- (+) Se ataca la app real; no se pierde tiempo re-eligiendo dirección.
- (+) Checklist claro por módulo en `PROJECT_MAP.md`.
- (−) Homologación mayor: hay que tokenizar de cero color y tipografía.
- (−) Módulos enormes (Inicio, Pedidos, Carrito) → obligan a trabajar pantalla por pantalla.

## Estructura de páginas resultante
- Fuente (solo lectura): `COMPONENTES`, `1.0 Login` … `10 Recompra`, `PROPUESTAS`.
- Trabajo (escritura): `04_Claude_Sandbox` → aprobado a `02_Tablet` / `03_Mobile`.
- Se eliminaron las páginas redundantes `00_Design_System` y `01_Web_Final` creadas por error.

## Siguiente
- Fase 0: tokenizar color + tipografía (`design-system-librarian`).
- Luego responsivar por módulo empezando por **Login** (valida el flujo completo).
