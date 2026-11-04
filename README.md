# Aloja — Frontend de Alojamientos | Entrega final (Trabajos 1–4)

SPA académica de consulta y gestión de alojamientos, desarrollada con **HTML5, CSS3, JavaScript Vanilla (ES Modules), Vite, Bootstrap 5.3 y Bootstrap Icons**. Consume una API REST real construida en Flask y respaldada por MySQL. No utiliza React, Vue ni Angular.

## Objetivo

Permitir la consulta pública de alojamientos y comodidades; el registro, inicio y cierre de sesión; y la gestión de alojamientos y comodidades según los permisos validados por Flask. El frontend no implementa reservas, pagos, carga de imágenes ni administración de roles o perfiles.

## Tecnologías y arquitectura

- **Presentación:** `index.html`, `src/css/main.css`, componentes reutilizables y páginas en `src/js/pages/`.
- **Enrutamiento SPA:** History API y `src/js/router/`; navegación sin recargar en enlaces internos, manejo de rutas inexistentes y guards de autenticación/rol.
- **Comunicación con API:** `fetch` mediante `src/js/api/http.js` y clientes específicos en `src/js/api/`.
- **Sesión:** token JWT y datos mínimos del usuario en `sessionStorage` (`src/js/state/sesion.js`). Los controles visuales no sustituyen los permisos del backend.
- **Herramientas:** npm, Vite 8, pruebas con `node --test`.

## Estructura

```text
frontend-alojamientos/
├── .env.example                 # Configuración pública de ejemplo
├── .gitignore                   # Exclusión de dependencias, builds y secretos
├── README.md                    # Esta documentación
├── docs/
│   ├── SPRINT-01.md             # SPA y catálogo público
│   ├── SPRINT-02.md             # Autenticación y roles
│   ├── SPRINT-03.md             # CRUD y comodidades
│   ├── VERIFICACION-FINAL.md    # Procedimiento de aceptación
│   └── evidencias/              # Instrucciones para capturas de evidencia
├── index.html
├── package.json
├── package-lock.json
├── vite.config.js
├── src/
│   ├── css/main.css
│   └── js/
│       ├── main.js
│       ├── config.js
│       ├── api/                   # http, pública, autenticación, gestión
│       ├── components/            # Barra, pie, tarjetas, formularios, estados
│       ├── pages/                 # Vistas públicas y privadas
│       ├── router/                # Definición/resolución de rutas
│       ├── state/                 # Sesión por pestaña
│       └── utils/                 # Validaciones, gestión y formato
└── tests/                        # Pruebas automatizadas Node
```

## Requisitos

- **Node.js 22.12 o posterior**, compatible con Vite 8; npm y Git.
- Para las pruebas integrales: **API Flask** accesible en `http://localhost:5000`, con MySQL activa y migraciones **001, 002 y 003** aplicadas.
- Navegador moderno. En local se utiliza `http://localhost:5173` para desarrollo y habitualmente `http://localhost:4173` para la vista previa.

## Instalación desde cero

```bash
# 1. Clonar el frontend
git clone https://github.com/santiagomed44/frontend-alojamientos.git
cd frontend-alojamientos

# 2. Instalar las dependencias conforme al lockfile
npm ci

# 3. Crear .env local a partir de .env.example
# Windows PowerShell: Copy-Item .env.example .env
# Windows Git Bash / Linux / macOS:
cp .env.example .env

# 4. Iniciar el servidor de desarrollo
npm run dev
```

Abrir la URL indicada por Vite (normalmente `http://localhost:5173`). Mantener Flask activo **en otra terminal y en el proyecto backend**, no en la carpeta frontend. Para una instalación inicial también puede usarse `npm install`, como exige el enunciado; `npm ci` es la opción reproducible recomendada cuando existe `package-lock.json`.

## Variables de entorno

El archivo versionado `.env.example` contiene:

```dotenv
VITE_API_URL=http://localhost:5000
```

`VITE_API_URL` indica la **raíz del servidor** Flask: no agregar `/api/v1`, porque `/health` se encuentra en la raíz. El frontend puede usar el origen `http://localhost:5000` como valor predeterminado, pero se recomienda configurar `.env` explícitamente. **Nunca incluir en el frontend** `SECRET_KEY`, claves JWT, contraseñas de MySQL ni tokens. Las variables `VITE_` quedan expuestas al navegador durante el build. `.env` se excluye de Git.

### Conexión con Flask/MySQL

1. En el proyecto **backend**, configurar de forma privada sus variables de conexión a MySQL, arrancar MySQL y aplicar las migraciones 001–003 según su documentación.
2. Iniciar Flask desde su directorio y entorno Python: `python -m flask --app app run --debug`. Verificar `http://localhost:5000/health` (esperado: `status: ok`).
3. En el `.env` **del backend**, configurar `CORS_ALLOWED_ORIGINS=http://localhost:5173,http://localhost:4173` (y otros orígenes locales usados), sin duplicar el nombre de la variable.
4. Ejecutar el frontend y comprobar los listados en `/alojamientos` y `/comodidades`; los formularios requieren la API y una sesión válida.
5. Ante errores de conexión, revisar el puerto, el origen CORS y las respuestas en la pestaña **Red/Network** de las herramientas de desarrollo.

El frontend **no se conecta directamente a MySQL**: se comunica mediante HTTP con Flask.

## Comandos

| Comando | Propósito |
|---|---|
| `npm install` | Instala dependencias y puede actualizar el lockfile |
| `npm ci` | Instalación limpia y reproducible según `package-lock.json` |
| `npm test` | Ejecuta las pruebas automatizadas con Node |
| `npm run dev` | Ejecuta Vite en desarrollo |
| `npm run build` | Genera la compilación de producción en `dist/` |
| `npm run preview` | Sirve localmente el contenido compilado |

`dist/`, `node_modules/`, `.env`, archivos de cobertura y configuración local del editor no se publican en Git ni se incluyen en el ZIP definitivo.

## Módulos funcionales por Sprint

- **Sprint 1:** página inicial, catálogo público, detalle del alojamiento, catálogo de comodidades, estado de la API, tarjetas y navegación SPA.
- **Sprint 2:** registro, login, JWT, sesión por pestaña, perfil de usuario, cierre de sesión, guardas de rutas, acceso administrativo al listado de usuarios y pantalla de no autorizado.
- **Sprint 3:** creación, consulta, edición y eliminación de alojamientos; listado local «Mis alojamientos» filtrando por `usuario_id`; creación administrativa de comodidades; asociación/desasociación mediante reemplazo de la lista completa de identificadores; validaciones y tratamiento de errores.

Véanse los registros técnicos de cada etapa en [`docs/SPRINT-01.md`](docs/SPRINT-01.md), [`docs/SPRINT-02.md`](docs/SPRINT-02.md) y [`docs/SPRINT-03.md`](docs/SPRINT-03.md).

## Rutas SPA

| Ruta | Acceso | Funcionalidad |
|---|---|---|
| `/` | Público | Inicio |
| `/alojamientos` | Público | Catálogo de alojamientos |
| `/alojamientos/:id` | Público | Detalle y comodidades asociadas |
| `/comodidades` | Público | Catálogo de comodidades |
| `/estado` | Público | Estado de la API |
| `/registro` | Público | Registro |
| `/login` | Público | Inicio de sesión |
| `/perfil` | Autenticado | Consulta del perfil |
| `/mis-alojamientos` | Autenticado | Filtrado local de alojamientos propios |
| `/alojamientos/nuevo` | Autenticado | Creación de alojamiento |
| `/alojamientos/:id/editar` | Propietario o admin* | Edición, eliminación, asignación de comodidades |
| `/admin/usuarios` | Administrador | Listado de usuarios |
| `/admin/comodidades/nueva` | Administrador | Creación de una comodidad |

*El frontend ofrece una restricción visual de propietario o administrador; la **autorización definitiva la realiza Flask** en las operaciones protegidas. Una ruta no reconocida muestra página 404.

## Endpoints del backend consumidos

| Método | Endpoint | Uso / autenticación |
|---|---|---|
| `GET` | `/health` | Diagnóstico público |
| `GET` | `/api/v1/alojamientos` | Listado público |
| `GET` | `/api/v1/alojamientos/:id` | Detalle público |
| `GET` | `/api/v1/comodidades` | Catálogo público |
| `POST` | `/api/v1/usuarios/registro` | Registro público |
| `POST` | `/api/v1/usuarios/login` | Obtención de JWT |
| `GET` | `/api/v1/usuarios/perfil` | Perfil con JWT |
| `GET` | `/api/v1/admin/usuarios` | Listado, administrador |
| `POST` | `/api/v1/alojamientos` | Crear, JWT |
| `PATCH` | `/api/v1/alojamientos/:id` | Editar, propietario/admin |
| `DELETE` | `/api/v1/alojamientos/:id` | Eliminar, propietario/admin; responde `204` sin JSON |
| `PATCH` | `/api/v1/alojamientos/:id/comodidades` | Reemplazar asociaciones, propietario/admin; cuerpo `{ "comodidades_ids": [1, 2] }` |
| `POST` | `/api/v1/comodidades` | Crear, administrador |

El cliente procesa respuestas JSON con `success` y `data`, y mensajes de error bajo `error.message`. Para `DELETE` con HTTP `204`, no intenta interpretar JSON. La API es la autoridad sobre permisos, integridad de relaciones y persistencia.

## Roles y permisos

| Operación | Invitado | Usuario autenticado | Administrador |
|---|---|---|---|
| Consultar catálogos y detalles | Sí | Sí | Sí |
| Registrarse / iniciar sesión | Sí | Sí | Sí |
| Consultar su perfil | No | Sí | Sí |
| Crear alojamiento | No | Sí | Sí |
| Modificar/eliminar alojamiento propio | No | Sí | Sí |
| Modificar/eliminar alojamiento ajeno | No | No | Sí |
| Gestionar asociaciones de un alojamiento | No | Solo propio | Cualquiera |
| Listar todos los usuarios | No | No | Sí |
| Crear comodidad | No | No | Sí |

El rol debe existir en el backend; no se obtiene privilegio administrador modificando `sessionStorage`. Si el backend tiene una operación de promoción administrativa, debe realizarse allí con las medidas correspondientes.

## Verificación y evidencia

La verificación manual efectuada en los Trabajos 1–3 cubrió autenticación, CRUD, gestión de comodidades y denegación de edición ajena. El historial de trabajo mostró **37 pruebas frontend aprobadas** y **16 pruebas backend aprobadas**; el build frontend también se verificó en el entorno del estudiante. Una nueva ejecución de `npm test` sobre el ZIP del Sprint 3 produjo **37 aprobadas, 0 fallidas**. Estas pruebas automatizadas no reemplazan las pruebas con Flask/MySQL real.

El procedimiento de comprobación final —incluida una instalación independiente, pruebas de viewport y evidencias— está en [`docs/VERIFICACION-FINAL.md`](docs/VERIFICACION-FINAL.md). Consulte también [`docs/evidencias/README.md`](docs/evidencias/README.md) para adjuntar capturas auténticas (no generadas).

## Repositorio e historial

Repositorio: https://github.com/santiagomed44/frontend-alojamientos

Historial de los tres sprints conservado en commits y Pull Requests. Sprint 3: [PR #4](https://github.com/santiagomed44/frontend-alojamientos/pull/4), relacionado con [Issue #3](https://github.com/santiagomed44/frontend-alojamientos/issues/3). La publicación definitiva del Trabajo 4 debe integrarse a `main` después de verificar los cambios documentales.

## Alcance y limitaciones

No se implementan reservas, pagos, fotos de alojamientos, actualización de perfiles, edición de roles ni modificación/eliminación del catálogo maestro de comodidades. «Mis alojamientos» aplica un filtro local sobre el listado público porque este backend no ofrece `GET /mis-alojamientos`. El acceso al backend es necesario para las funciones dinámicas: la compilación estática no proporciona una API simulada.
