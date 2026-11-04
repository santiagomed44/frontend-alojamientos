# Verificación de entrega final — Trabajo 4

Documento de aceptación reproducible. Marcar los resultados solo después de ejecutarlos; las comprobaciones de la API y la responsividad requieren interacción manual.

## A. Instalación independiente

1. Desde **una carpeta diferente** al directorio de desarrollo, clonar el repositorio publicado en `main`.
2. Comprobar Node.js compatible con Vite 8 (`node -v`) y npm (`npm -v`).
3. Ejecutar `npm ci` (o `npm install` como solicita el enunciado).
4. Copiar `.env.example` a `.env` y configurar `VITE_API_URL=http://localhost:5000`.
5. Iniciar el backend Flask y MySQL, con migraciones 001, 002 y 003 y CORS incluyendo `http://localhost:5173` y `http://localhost:4173`.
6. Ejecutar `npm test`, `npm run dev`, `npm run build`, `npm run preview`.
7. Abrir el sitio de Vite y de preview, comprobar `GET /health`, catálogo y detalles.
8. Comprobar que `git status` no presenta cambios no deseados en archivos versionados y que los directorios generados están ignorados.

## B. Matriz de aceptación funcional

| ID | Escenario | Criterio de aceptación | Evidencia |
|---|---|---|---|
| F01 | Inicio y navegación | SPA abre y permite volver/avanzar | Captura de Inicio |
| F02 | Catálogo público | Lista un alojamiento desde Flask y filtra por texto | Catálogo |
| F03 | Detalle y comodidades | Presenta datos y asociaciones vigentes | Detalle |
| F04 | Catálogo de comodidades | Muestra lista obtenida por API | Catálogo comodidades |
| F05 | Salud API | Indica estado de Flask | Estado API |
| F06 | Registro/login | Permite registro e inicio con JWT | Formulario y pantalla autenticada (sin token visible) |
| F07 | Perfil/logout | Muestra datos y finaliza sesión | Perfil / cierre |
| F08 | Roles | Usuario normal no accede a administración; admin sí | Vista no autorizado / admin |
| F09 | Crear alojamiento | Registro aparece en catálogo | Formulario / detalle |
| F10 | Editar alojamiento | Cambios persisten al recargar | Antes/después |
| F11 | Comodidades | Asociar y retirar se reflejan en detalle | Antes/después |
| F12 | Eliminar | Alojamiento de prueba deja de aparecer | Mis alojamientos |
| F13 | Permisos de propiedad | Usuario ajeno no puede editar ni eliminar (`403`) | Aviso / DevTools sin token |
| F14 | Responsive | Sin desbordamiento crítico en desktop, tablet y móvil | 3 capturas |
| F15 | Pruebas | `npm test` termina sin fallos | Terminal |
| F16 | Build | `npm run build` termina con éxito | Terminal |
| F17 | Instalación limpia | Clon nuevo ejecuta tests y compila | Terminal desde carpeta independiente |

## C. Verificaciones ya disponibles antes de publicar Trabajo 4

- En la carpeta de trabajo de los Sprints 1–3: **37/37 tests frontend**, **16/16 tests backend**, `npm run build` exitoso según capturas compartidas.
- Se observó en GitHub la fusión del Sprint 3 a `main` mediante PR #4.
- El archivo del Sprint 3 se preparó con `git archive`, sin `node_modules` ni `dist`.
- Durante la preparación documental se ejecutó `npm test` en una copia extraída del ZIP: **37/37 aprobados**.

**Pendiente de confirmar en Trabajo 4:** instalación independiente de dependencias, nuevo build desde clon limpio, recorrido manual de todos los casos y capturas documentales; no se declaran completados por el mero hecho de existir este archivo.

## D. Publicación final

Usar rama específica del Trabajo 4, revisar `git diff`, registrar un commit documental con el texto `docs: finalizar documentacion y entrega frontend`, subir la rama, abrir PR hacia `main`, fusionar y ejecutar `git pull --ff-only origin main`. Generar el ZIP **a partir del commit final de `main`** con `git archive --format=zip --output=../Aloja_Frontend_Trabajo4_Final.zip main`.
