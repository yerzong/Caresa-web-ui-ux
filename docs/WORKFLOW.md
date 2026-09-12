# Protocolo de Ejecución

Método para trabajar el proyecto Figma con Claude Code sin perder información ni degradar
diseños existentes. Basado en las mejores prácticas de Claude Code (contexto en capas,
plan mode, commits atómicos, verificación) adaptadas a un flujo 100% Figma.

## Principio central: contención de contexto

Un archivo Figma grande satura el contexto y provoca alucinaciones. Lo evitamos con:

1. **Aislamiento por página** — Claude solo mira la página en la que trabaja.
2. **Sandbox** — se genera en `04_Claude_Sandbox`, no en las páginas finales.
3. **Ejecución atómica** — una pantalla o componente por tarea, nunca "todo".
4. **`/clear` entre pantallas** — resetea la memoria de conversación (los docs locales persisten).

## Las 4 fases por pantalla

### Fase 1 — Planificación (Plan Mode, sin escribir)
Claude inspecciona y propone. No modifica nada.
> "Analiza la pantalla `Web - [Nombre]` en Figma. Dame el plan para su versión Mobile (393 px)
> siguiendo `@docs/RESPONSIVE_TOKENS.md`. No modifiques nada todavía."

### Fase 2 — Homologación (antes de responsivar)
Corregir valores sueltos en la fuente Web para que use estilos/variables globales.
> "Revisa `Web - [Nombre]`. Si hay colores/tipografías/espaciados aplicados manualmente,
> reemplázalos por el estilo o variable homologado según `@docs/DESIGN_SYSTEM.md`."

### Fase 3 — Generación en Sandbox
Crear la variante responsive en `04_Claude_Sandbox`.
> "Basado en `Web - [Nombre]` homologada, crea la variante Mobile (393 px) en `04_Claude_Sandbox`,
> aplicando `@docs/RESPONSIVE_TOKENS.md`. Usa componentes maestros de `00_Design_System`,
> Auto Layout con `Fill container`, y nombres de capa semánticos."

### Fase 4 — Verificación, registro y cierre
1. Humano revisa el resultado en el sandbox.
2. Si está correcto → mover el frame a la página final (`02_Tablet` / `03_Mobile`).
3. Claude actualiza `PROJECT_MAP.md` (marca `[x]`) y `CHANGELOG.md`.
4. **Commit atómico** (ver abajo).
5. Humano ejecuta **`/clear`** antes de la siguiente pantalla.

## Reglas de oro
- Nunca "haz todo responsive". Siempre una pantalla/flujo a la vez.
- Nunca tocar `01_Web_Final`. Es solo lectura.
- Referir capas por **nombre semántico exacto**, no por "Group 122".
- Restringir el alcance: si es el Header, prohibir mirar el Footer.
- Si Claude propone algo fuera de `PROJECT_MAP.md`, detenerse y confirmar con el humano.

## Commits atómicos (bitácora en git)
Un commit por unidad de trabajo terminada. Ejemplos:
```
docs(analysis): inventario inicial del archivo Figma
feat(mobile): variante responsive de Home (393px)
chore(homolog): homologa colores sueltos en flujo Auth
```
El commit acompaña la actualización de `PROJECT_MAP.md` y `CHANGELOG.md`.

## Higiene de contexto
- `/clear` — al terminar y aprobar una pantalla (memoria en blanco para la siguiente).
- `/compact` — si una sola tarea larga acumula demasiado contexto a mitad de camino.
- Los docs de este repo son la memoria persistente: si algo importa, va a un doc, no solo al chat.

## Plantillas de prompt

**Auditar un flujo:**
> "Usa el agente `figma-auditor`. Audita el flujo [X] en `01_Web_Final` (solo lectura) y
> reporta valores sueltos y componentes no homologados. No modifiques nada."

**Documentar design system:**
> "Usa el agente `design-system-librarian`. Extrae tokens, estilos y componentes maestros
> de `00_Design_System` y actualiza `@docs/DESIGN_SYSTEM.md`."

**Planear responsive de una pantalla:**
> "Usa el agente `responsive-architect`. Planea la adaptación de `Web - [Nombre]` a Mobile y
> Tablet según `@docs/RESPONSIVE_TOKENS.md`. Devuelve plan, sin tocar Figma."
