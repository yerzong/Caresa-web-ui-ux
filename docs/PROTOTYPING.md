# Prototipado en Figma (vía Plugin API)

Cómo cablear interacciones de prototipo con `use_figma`. Lo hace el agente `figma-prototyper`.
Siempre cargar la skill `/figma-use` antes de `use_figma`.

## Modelo
El prototipo se edita poniendo **reactions** en nodos: `await node.setReactionsAsync(reactions)`.
Una **Reaction** = `{ trigger, actions[] }`. Usar SIEMPRE `actions[]` (el campo singular `action` está **deprecado**).
Patrón obligatorio: **read-modify-write** (clonar `reactions` actuales, mutar, `setReactionsAsync`).

## Enums clave
- **Triggers:** `ON_CLICK`, `ON_HOVER`, `ON_PRESS`, `ON_DRAG`, `AFTER_TIMEOUT`, `MOUSE_ENTER/LEAVE/UP/DOWN`, `ON_KEY_DOWN`.
- **Action.type:** `NODE`, `BACK`, `CLOSE`, `URL`, `SET_VARIABLE`, `SET_VARIABLE_MODE`, `UPDATE_MEDIA_RUNTIME`, `CONDITIONAL`.
- **NODE.navigation:** `NAVIGATE`, `OVERLAY`, `SWAP`, `SCROLL_TO`, `CHANGE_TO`.
- **transition.type:** `SMART_ANIMATE`, `SCROLL_ANIMATE`, `DISSOLVE`, `MOVE_IN/OUT`, `PUSH`, `SLIDE_IN/OUT` (+ `easing`, `duration`).
- **Flow start:** `page.flowStartingPoints = [{ nodeId, name }]`.

## Patrón — Login Paso 1 → Paso 2
```js
const btn = /* nodo botón "Continuar" en Paso 1 */;
const paso2 = /* frame Paso 2 */;
await btn.setReactionsAsync([{
  trigger: { type: "ON_CLICK" },
  actions: [{
    type: "NODE", destinationId: paso2.id, navigation: "NAVIGATE",
    transition: { type: "SMART_ANIMATE", easing: { type: "EASE_OUT" }, duration: 0.3 }
  }]
}]);
```

## Patrón — Sidebar/Navbar → Drawer (móvil)
```js
// Hamburguesa abre drawer como overlay que entra desde la izquierda
await hamburger.setReactionsAsync([{
  trigger: { type: "ON_CLICK" },
  actions: [{ type: "NODE", destinationId: drawer.id, navigation: "OVERLAY",
              transition: { type: "SLIDE_IN", easing:{type:"EASE_OUT"}, duration: 0.25 } }]
}]);
// Scrim / botón cerrar
await closeBtn.setReactionsAsync([{ trigger:{type:"ON_CLICK"}, actions:[{ type:"CLOSE" }] }]);
```

## Patrón — Cambiar breakpoint en vivo (demo responsive)
```js
// Botón que cambia el modo de la colección Breakpoints (Desktop/Tablet/Mobile)
await btn.setReactionsAsync([{
  trigger: { type: "ON_CLICK" },
  actions: [{ type: "SET_VARIABLE_MODE", variableCollectionId: BREAKPOINTS_COLLECTION_ID, modeId: MOBILE_MODE_ID }]
}]);
```

## Limitaciones / gotchas
- `setReactionsAsync` es **async** → siempre `await`.
- Reactions por API pueden renderizarse ligeramente distinto a las dibujadas a mano (quirk conocido).
- `overlayPositionType` por API es limitado/históricamente con bugs → fijar posición del overlay y verificar.
- No se puede iniciar el modo Present desde la API; el humano abre la vista de prototipo.
- Devolver SIEMPRE los IDs de nodos a los que se les puso reactions.

> Referencia: developers.figma.com → Reaction / Action / `setReactionsAsync`.
