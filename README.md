# Flotti — prototipo navegacional mobile-first (throwaway)

Prototipo de validación de concepto para el rediseño mobile-first del portal admin.
**No es código de producción. No está conectado a datos ni rutas. Mock data inline.**

## Cómo verlo
Abrir `index.html` (o `dashboard.html`) en un navegador. Probar en responsive a **375px** (móvil), **768px** (tablet) y **1280px** (escritorio).

## Arquitectura
- `app.css` — tokens de diseño (portados de `src/admin/views/layout.ejs`) + chrome móvil (bottom-nav, sheets, cards, totals).
- `shell.js` — inyecta el chrome compartido (sidebar en `lg`, bottom-nav + sheet "Más" en móvil). Cada página declara `<body data-page="..." data-title="...">`.
- Cada pantalla es un `.html` autocontenido: Tailwind CDN + `app.css` + `shell.js`, con `<main class="lg:ml-60 ... pb-24 lg:pb-8">`.

## Patrón (referencia: `dashboard.html` y `cuotas.html`)
- **Listas = card-list** (patrón base móvil), no tablas. Cada fila → `.list-card` con identificador, secundario, chip de estado y monto ancla (`.money`, alineado a la derecha, tabular).
- **Drill-down**: la lista muestra 3-4 campos; el resto va al detalle.
- **Summary-first**: franja de totales (`.totals-strip`) arriba de listas financieras.
- **Filtros**: segmented control (`.segmented`/`.seg`) + bottom-sheet (`.sheet`).
- **Tabla densa** solo en `cuotas`/`pagos` como `hidden lg:block` (mejora de escritorio).

## Estado
Pantallas: index, login, dashboard, cuotas (referencia) + el resto generado por workers.
