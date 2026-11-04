# Sprint 3 — CRUD de alojamientos y comodidades

## Objetivo

Incorporar la creación, consulta, actualización y eliminación de alojamientos, la creación administrativa del catálogo de comodidades y la asignación de comodidades a alojamientos existentes.

## Funcionalidades y rutas

- `/mis-alojamientos`: lista con filtro local por `usuario_id` del usuario conectado.
- `/alojamientos/nuevo`: formulario con título, descripción, ciudad y precio nocturno; el servidor toma el propietario del JWT.
- `/alojamientos/:id/editar`: formulario prellenado para el propietario o administrador; permite editar, eliminar y gestionar asociaciones.
- `/admin/comodidades/nueva`: creación del catálogo para rol `admin`.
- `/alojamientos/:id`: muestra comodidades devueltas por el backend.

## Contratos de API

| Método | Endpoint | Comportamiento |
|---|---|---|
| `POST` | `/api/v1/alojamientos` | Crear alojamiento con JWT |
| `PATCH` | `/api/v1/alojamientos/:id` | Actualizar campos autorizados |
| `DELETE` | `/api/v1/alojamientos/:id` | Eliminar con `204` sin cuerpo |
| `PATCH` | `/api/v1/alojamientos/:id/comodidades` | Reemplazar relación con `{ "comodidades_ids": [...] }`; `[]` elimina asociaciones |
| `POST` | `/api/v1/comodidades` | Crear comodidad con JWT administrativo |

Las consultas de alojamiento y comodidades siguen usando los GET públicos del Sprint 1. Las opciones de asignación proceden del catálogo real de la API; no son datos simulados.

## Validaciones y permisos

El formulario verifica campos requeridos y precio positivo. Flask verifica propiedad/rol al modificar o eliminar; la restricción visual no es una barrera de seguridad. La asignación rechaza identificadores inexistentes, duplicados o con tipo incorrecto desde el backend. El frontend maneja errores HTTP y `204` correctamente.

## Componentes y archivos

`src/js/api/alojamientos.api.js`, `comodidades.api.js`, `src/js/components/AlojamientoForm.js`, `ComodidadesSelector.js`, `src/js/pages/CrearAlojamientoPage.js`, `EditarAlojamientoPage.js`, `MisAlojamientosPage.js`, `AdminCrearComodidadPage.js`, `src/js/utils/gestion.js`.

## Evidencias funcionales ya observadas en el desarrollo

Se realizó la creación de un apartamento, cambio de precio de 180000 a 195000 COP, asociación y posterior retiro de Wi-Fi, y eliminación de un alojamiento de prueba. También se observó el bloqueo de modificación de un registro ajeno con usuario normal. La documentación del Trabajo 4 debe acompañarse con capturas propias en `docs/evidencias/`.

## Verificación automatizada

Las pruebas frontend de gestión están en `tests/crud-api.test.js`, `gestion-componentes.test.js`, `gestion-routes.test.js` y `gestion.test.js`; las pruebas existentes de sprints anteriores se mantienen. Verificación más reciente: **37/37 aprobadas**.

Sprint 3 integrado mediante https://github.com/santiagomed44/frontend-alojamientos/pull/4; Issue https://github.com/santiagomed44/frontend-alojamientos/issues/3.
