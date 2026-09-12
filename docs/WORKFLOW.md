# Protocolo de Ejecución

Método para trabajar el proyecto Figma con Claude Code sin perder información ni degradar
diseños existentes. Basado en mejores prácticas de Claude Code (contexto en capas, plan mode,
commits atómicos, verificación) adaptadas a un flujo 100% Figma.

## Principio central: contención de contexto

Un archivo Figma grande satura el contexto y provoca alucinaciones. Lo evitamos con:

1. **Aislamiento por página/módulo** — Claude solo mira la pantalla en la que trabaja.
2. **Sandbox** — se genera en `04_Claude_Sandbox`, no en las páginas fuente.
3. **Ejecución atómica** — una pantalla o componente por tarea, nunca "todo".
4. **`/clear` entre pantallas** — resetea la conversación (los docs locales persisten como memoria).

## Tabla de decisión de tools (ahorra contexto)
| Necesito | Tool | Skill previa |
|---|---|---|
| Ubicar un nodo / estructura shallow | `get_metadata` | — |
| Leer el diseño completo de UN nodo (a código) | `get_design_context` | `/figma-design-to-code` |
| Verificación visual | `get_screenshot` | — |
| Inventario de tokens/estilos | `get_variable_defs`, `get_libraries` | — |
| Escribir/editar/crear nodos | `use_figma` | `/figma-use` |
| Construir pantalla desde componentes | `generate_figma_design` / `use_figma` | `/figma-generate-design` |
| Construir design system / componentes | `use_figma` | `/figma-generate-library` + `/figma-use` |

> Regla de oro de contexto: **`get_metadata` primero** para ubicar el nodo; `get_design_context` SOLO
> sobre ese nodo (es caro en tokens). Nunca `get_design_context` sobre una página entera.

## Las fases por pantalla

### Fase 1 — Planificación (Plan Mode, sin escribir)
Claude inspecciona y propone. No modifica nada.
> "Analiza la pantalla `[Módulo] - [Nombre]` en Figma. Dame el plan para Tablet (834) y Mobile (393)
> según `@docs/RESPONSIVE_TOKENS.md`. No modifiques nada todavía."

### Fase 2 — Homologación (antes de responsivar)
Corregir valores sueltos en la fuente para que use tokens/variables/componentes globales.
> "Revisa `[Módulo] - [Nombre]`. Reemplaza colores/tipografías/espaciados manuales por la variable
> o componente homologado según `@docs/DESIGN_SYSTEM.md`." (usa `figma-auditor` para detectar primero).

### Fase 3 — Generación responsive en Sandbox (MÉTODO DE FIDELIDAD)
**Regla:** NO redibujar/reinventar. Se **clona la pantalla Desktop real** y se **reacomoda** por breakpoint,
conservando texturas, ilustraciones, íconos y componentes exactos. Pasos:
1. `node.clone()` de la pantalla real → `04_Claude_Sandbox` (base fiel).
2. Reacomodar: root a `VERTICAL` (móvil), `rescale()` de paneles decorativos (marca) para caber en el ancho,
   `layoutSizingHorizontal='FILL'` en el formulario, `clipsContent=true` en el panel de marca, y
   constreñir los frames de texto a `FILL` + `textAutoResize='HEIGHT'` para que envuelvan (no se recorten).
3. Verificar con `get_screenshot` **contra el original** — si se ve distinto, está mal.
Los átomos salen de los componentes **existentes** (`_Input field base`, `Button`, `_Nav item base`), no de nuevos.

Crear las variantes Tablet/Mobile en `04_Claude_Sandbox`.
> "Basado en `[Módulo] - [Nombre]` homologada, crea Tablet (834) y Mobile (393) en `04_Claude_Sandbox`
> aplicando `@docs/RESPONSIVE_TOKENS.md`: variables de `Breakpoints`, Auto Layout `Fill`, transforms
> (sidebar→drawer, tabla→cards), nombres semánticos." (usa `responsive-architect`).

### Fase 4 — Revisión UI/UX
Correr el checklist de `@docs/UX_PRINCIPLES.md`.
> "Usa `ui-ux-reviewer` sobre la variante Mobile en el sandbox. Reporta incumplimientos WCAG/UX y corrige los bloqueantes."

### Fase 5 — Prototipado
Cablear el flujo con `@docs/PROTOTYPING.md`.
> "Usa `figma-prototyper` para conectar Login Paso 1 → Paso 2 y la hamburguesa → drawer en la variante Mobile."

### Fase 6 — Verificación, registro y cierre
1. Humano revisa el resultado en el sandbox.
2. Si está correcto → mover el/los frame(s) a `02_Tablet` / `03_Mobile`.
3. Claude actualiza `PROJECT_MAP.md` (marca `[x]`) y `CHANGELOG.md`.
4. **Commit atómico** (ver abajo).
5. Humano ejecuta **`/clear`** antes de la siguiente pantalla.

## Organización del sandbox (evitar encimados)
- Colocar cada frame nuevo en su **zona/sección** con márgenes (no en (0,0) por defecto).
- ⚠️ **Dentro de una `SECTION`, `node.x/.y` son RELATIVAS a la sección**, no a la página. Al meter frames a una
  sección, fijar sus coords relativas (dejar ~96px arriba para la etiqueta) y luego `resizeWithoutConstraints`
  al bounding box de los hijos + padding. Verificar con screenshot que ningún frame se salga del borde.
- Zonas actuales: `FIEL — reproducción fiel` (trabajo bueno) y `BORRADORES desviados — a REEMPLAZAR`.

## Reglas de oro
- Nunca "haz todo responsive". Siempre una pantalla/flujo a la vez.
- Nunca tocar las páginas fuente Desktop (`1.0 Login` … `10 Recompra`), `COMPONENTES` ni `PROPUESTAS`.
- Referir capas por **nombre semántico exacto**, no por "Group 122".
- Restringir el alcance: si es el Header, prohibir mirar el Footer.
- Si Claude propone algo fuera de `PROJECT_MAP.md`, detenerse y confirmar con el humano.

## Commits atómicos (bitácora en git)
Un commit por unidad de trabajo terminada. Ejemplos:
```
docs(analysis): inventario real del archivo por módulos
feat(mobile): variante responsive de Login (393px)
chore(homolog): homologa colores sueltos en flujo Carrito
feat(proto): conecta Login Paso 1 → Paso 2
```
El commit acompaña la actualización de `PROJECT_MAP.md` y `CHANGELOG.md`.

## Higiene de contexto
- `/clear` — al terminar y aprobar una pantalla (memoria en blanco para la siguiente).
- `/compact` — si una sola tarea larga acumula demasiado contexto a mitad de camino.
- Los docs de este repo son la memoria persistente: si algo importa, va a un doc, no solo al chat.

## Plantillas de prompt (agentes)
**Auditar:** "Usa `figma-auditor`. Audita `[Módulo]/[pantalla]` (solo lectura) y reporta valores sueltos y componentes no homologados."
**Design system:** "Usa `design-system-librarian`. Extrae/tokeniza color y tipografía de `COMPONENTES` y actualiza `@docs/DESIGN_SYSTEM.md`."
**Responsive:** "Usa `responsive-architect`. Planea y genera Tablet+Mobile de `[pantalla]` según `@docs/RESPONSIVE_TOKENS.md` en el sandbox."
**UX:** "Usa `ui-ux-reviewer`. Corre el checklist de `@docs/UX_PRINCIPLES.md` sobre `[pantalla]`."
**Prototipo:** "Usa `figma-prototyper`. Conecta el flujo de `[módulo]` según `@docs/PROTOTYPING.md`."
