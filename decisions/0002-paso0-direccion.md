# ADR 0002 — PASO 0: Dirección elegida

- **Fecha:** 2026-09-11
- **Estado:** ⚠️ **SUPERADO por ADR 0003** — su premisa ("el archivo es solo PROPUESTAS, hay que elegir
  una propuesta") era incorrecta: la app Desktop real ya existe por módulos. Se conserva por historial.
  Sigue válido: base de componentes Untitled-style + migrar restos SDS.

## Contexto
El archivo `PROPUESTAS` tenía variantes en competencia (3 sidebar, 2 navbar, 2 login) mezclando
dos design systems. Antes de responsivar hay que consolidar una sola dirección.

## Decisiones
1. **Login:** layout de **Propuesta A** (branded: panel verde + logo CARESA + form pulido con
   toggle de contraseña y flujo Paso 1 → Paso 2 Caja/Sucursal), pero **reconstruido con el design
   system único** (Untitled UI + tokens de marca). "Lo mejor de ambas".
2. **Dashboard:** **Sidebar (navegación lateral)**. Justificación: el sistema es un ERP/POS con
   muchos módulos (~65 ítems de nav apretados en la variante navbar). El sidebar escala mejor,
   es el estándar de paneles admin y colapsa limpio a drawer en móvil.
3. **Design System:** base en **componentes tipo Untitled UI** (los dashboards ya los usan:
   tablas, métricas, nav items, paginación). Se formalizan **tokens** encima: tipografía **Inter**,
   paleta de marca **verde/lima**, escala de espaciado y radios. Los login SDS se migran a esta base.

## Consecuencias
- (+) Una sola fuente de verdad de componentes → homologación real.
- (+) Sidebar da un patrón responsive claro (drawer en móvil).
- (−) Hay que reconstruir el login A con componentes Untitled-style (no solo copiar).
- (−) Migrar los tokens `--sds-*` del login a la nomenclatura del DS elegido.

## Siguiente
- Crear páginas nuevas (`00_Design_System`, `01_Web_Final`, `02_Tablet`, `03_Mobile`,
  `04_Claude_Sandbox`) sin tocar `PROPUESTAS`.
- Poblar `00_Design_System` con tokens + componentes maestros.
- Requiere **acceso de escritura** (por confirmar).
