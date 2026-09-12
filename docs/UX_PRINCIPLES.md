# Principios UI/UX y Checklist de Revisión

Base para diseñar y **revisar** cada pantalla. El agente `ui-ux-reviewer` corre el checklist de abajo
contra una pantalla y devuelve un reporte. Fuentes: Nielsen Norman Group (10 heurísticas), WCAG 2.2 AA.

## 10 Heurísticas de Nielsen (condensadas)
1. **Visibilidad del estado** — feedback claro (loading, guardado, progreso).
2. **Correspondencia con el mundo real** — lenguaje del usuario, no jerga técnica.
3. **Control y libertad** — deshacer, cancelar, volver; salidas de emergencia.
4. **Consistencia y estándares** — mismos patrones/componentes en todo el producto.
5. **Prevención de errores** — evitar el error antes de que ocurra (validaciones, defaults).
6. **Reconocer > recordar** — opciones visibles; no obligar a memorizar.
7. **Flexibilidad y eficiencia** — atajos para expertos sin estorbar a novatos.
8. **Estético y minimalista** — sin ruido; jerarquía clara.
9. **Ayuda a reconocer/recuperarse de errores** — mensajes específicos + cómo solucionar.
10. **Ayuda y documentación** — accesible cuando se necesita.

## Checklist de revisión por pantalla (WCAG 2.2 AA + UX)
Marcar cada punto. Reportar incumplimientos con nodo/nombre y corrección.

```
[ ] Contraste: texto normal ≥ 4.5:1; texto grande (≥24px / ≥18.7px bold) y UI/iconos ≥ 3:1  (WCAG 1.4.3 / 1.4.11)
[ ] Touch targets ≥ 24×24 px (WCAG 2.2 SC 2.5.8); acciones primarias en móvil 44×44
[ ] Estado de foco visible en cada elemento interactivo, indicador ≥ 3:1  (SC 2.4.7)
[ ] La información NO depende solo del color (icono/texto de respaldo)  (SC 1.4.1)
[ ] Texto escalable a 200% sin pérdida; body mínimo 16px en móvil  (SC 1.4.4)
[ ] Espaciado en grid 8pt; ritmo consistente entre secciones
[ ] Jerarquía visual clara: UNA CTA primaria por vista; escala tipográfica respetada
[ ] Estados presentes: loading / vacío / error / éxito
[ ] Mensajes de error específicos + ruta de recuperación; acciones destructivas confirmables/undo
[ ] Todos los inputs con label (placeholder ≠ label)
[ ] Consistencia: componentes desde `COMPONENTES`; sin hex/tipografía/espaciado hardcoded
[ ] Orden de lectura/tab lógico; jerarquía de headings sin saltos
[ ] Reflow sin scroll horizontal a 393px / 320px  (SC 1.4.10)
[ ] En móvil: navegación colapsada correctamente (sidebar/navbar → drawer)
```

## Prioridad de hallazgos
- **Bloqueante:** contraste insuficiente, target táctil < 24px, sin foco, scroll horizontal en móvil,
  valores hardcoded en vez de tokens.
- **Mayor:** jerarquía confusa, falta de estados (error/vacío), inconsistencia de componentes.
- **Menor:** ritmo de espaciado, microcopys, refinamientos estéticos.

## Notas
- SC 2.4.13 (Focus Appearance) y 2.5.5 (target 44px genérico) son **AAA**; el mínimo **AA** es
  foco visible (2.4.7) + contraste no-textual 3:1 y target 24px (2.5.8). Para móvil apuntamos a 44px por buena práctica.

> Referencia rápida: `https://www.w3.org/TR/WCAG22/` · NN/g "10 Usability Heuristics".
