# Sprint 2 — Autenticación, sesión y permisos

## Objetivo

Integrar registro e inicio de sesión JWT con Flask y controles de acceso en la SPA sin incorporar un framework frontend.

## Funcionalidades

- `/registro`: validación de correo y contraseña; envía `POST /api/v1/usuarios/registro`.
- `/login`: envía `POST /api/v1/usuarios/login`; almacena `access_token` y usuario en `sessionStorage`.
- `/perfil`: consulta con JWT a `GET /api/v1/usuarios/perfil`.
- `/admin/usuarios`: listado únicamente para rol `admin`, usando `GET /api/v1/admin/usuarios`.
- Cierre de sesión local, actualización del menú y redirección a login cuando una vista requiere autenticación.
- Respuestas `401` con JWT se manejan invalidando la sesión; `403` representa falta de permiso y no requiere cierre de sesión.

## Archivos principales

`src/js/api/auth.api.js`, `src/js/api/http.js`, `src/js/state/sesion.js`, `src/js/router/router.js`, `src/js/router/routes.js`, páginas `RegistroPage.js`, `LoginPage.js`, `PerfilPage.js`, `AdminUsuariosPage.js`, `NoAutorizadoPage.js`.

## Prueba manual

1. Registrar usuario y acceder.
2. Consultar perfil y cerrar sesión.
3. Intentar acceder a `/perfil` sin sesión y comprobar redirección.
4. Con usuario estándar, intentar `/admin/usuarios`; comprobar vista de no autorizado y `403` de Flask ante petición protegida.
5. Con rol administrativo real establecido desde backend, iniciar nueva sesión y consultar usuarios.

## Seguridad y alcance

Los elementos ocultos o guards del frontend no sustituyen verificaciones de permisos en Flask. No se implementa cambio de roles, edición de perfil ni refresh token.
