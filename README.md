# Frontend Alojamientos — Sprint 2 (SPA Vanilla)

Incremento acumulado del frontend de `api-alojamientos`. HTML5, CSS3, Bootstrap 5, JavaScript ES Modules, Vite, `fetch`, History API. Sin React, Vue ni Angular.

## Requisitos

- Node compatible con Vite 8 (preferiblemente 22.12 o posterior), npm y Git.
- API Flask real operativa en `http://localhost:5000`; MySQL disponible y migración `003` aplicada.
- En el `.env` **del backend**: `CORS_ALLOWED_ORIGINS=http://localhost:5173,http://localhost:3000`.

## Preparación

Desde este directorio:

```bash
npm ci
```

En Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

En Linux/macOS:

```bash
cp .env.example .env
```

La única variable necesaria para Vite es `VITE_API_URL=http://localhost:5000`. No copie las claves MySQL ni `SECRET_KEY` del backend al frontend. Vite expone las variables con prefijo `VITE_` al navegador.

```bash
npm test
npm run dev
```

Abra `http://localhost:5173`, manteniendo Flask disponible en otra terminal. Para comprobar la compilación:

```bash
npm run build
npm run preview
```

## Vistas

La sesión se guarda solo en `sessionStorage` y desaparece al cerrar la pestaña. No existe logout remoto ni renovación del JWT en la API real. Para obtener un admin, registre un usuario y ejecute `python -m scripts.promover_admin admin@ejemplo.com` **en la carpeta backend** con su `.venv`; cierre sesión e inicie nuevamente para refrescar el menú si cambió el rol.

## Contratos backend

`POST /api/v1/usuarios/registro` (201/400/409), `POST /api/v1/usuarios/login` (200/401), `GET /api/v1/usuarios/perfil` (200/401), `GET /api/v1/admin/usuarios` (200/401/403). No se implementa edición de perfiles ni de roles: esas rutas no existen en el backend entregado.

## Pruebas

`npm test` debe informar **23 pruebas superadas**, incluidos los 9 casos del Sprint 1. Las pruebas automatizadas simulan llamadas a `fetch` y no sustituyen el recorrido manual completo contra Flask/MySQL. Consulte `SPRINT-02.md` y `TUTORIAL-02.md` del paquete del docente.


## Sprint 3 — Gestión de alojamientos y comodidades

Se añaden páginas `/mis-alojamientos`, `/alojamientos/nuevo`, `/alojamientos/:id/editar` y `/admin/comodidades/nueva`. El frontend utiliza exclusivamente los endpoints previstos en el Tutorial 3, sin reservas, imágenes ni edición/eliminación del catálogo de comodidades.

**Requisitos de backend:** Flask con MySQL y migraciones 001, 002 y 003. El backend del Sprint 2 por sí solo no incluye alojamientos ni comodidades. Configure `VITE_API_URL=http://localhost:5000` localmente mediante `.env` (no publicarlo).

**Comprobaciones:** `npm ci`, `npm test` (37 pruebas esperadas), `npm run dev`, `npm run build`, `npm run preview`. Las operaciones CRUD requieren backend y permisos reales, no se validan solo con tests Node.
