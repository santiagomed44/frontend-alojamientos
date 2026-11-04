# Sprint 1 — SPA y consulta pública

## Objetivo

Crear la base de Aloja como una SPA modular con HTML, CSS, JavaScript ES Modules, Vite y Bootstrap 5.3 conectada a consultas públicas de la API Flask.

## Funcionalidades verificables

- Inicio `/` y navegación mediante History API y enlaces internos.
- Catálogo `/alojamientos` con búsqueda por título o ciudad aplicada a los alojamientos cargados.
- Detalle `/alojamientos/:id` y presentación de los datos devueltos por Flask.
- Consulta pública de comodidades `/comodidades`.
- Diagnóstico de conectividad `/estado` contra `GET /health`.
- Estados de carga, error y lista vacía; página para rutas inexistentes.
- Componentes reutilizables de navegación, pie y tarjetas; CSS responsive.

## API consumida

`GET /health`, `GET /api/v1/alojamientos`, `GET /api/v1/alojamientos/:id`, `GET /api/v1/comodidades`.

## Archivos principales

`src/js/main.js`, `src/js/router/`, `src/js/pages/InicioPage.js`, `AlojamientosPage.js`, `DetallePage.js`, `ComodidadesPage.js`, `EstadoPage.js`, `src/js/components/`, `src/js/api/publica.api.js`, `src/css/main.css`.

## Verificación

Abrir rutas públicas sin token; comprobar búsqueda, un detalle existente, un ID inexistente, estados de API disponible/no disponible y navegación Atrás/Adelante. Las pruebas de las rutas y API públicas están en `tests/`. Las verificaciones reales requieren Flask/MySQL encendidos.

## Alcance

Las operaciones de reserva y pago no forman parte del proyecto.
