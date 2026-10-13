# NailFlow — Dashboard

### La operación del salón, organizada en un solo lugar.

Este repositorio contiene el **frontend del dashboard interno de NailFlow**, la plataforma de gestión para un negocio de belleza y manicura. Está dirigido al equipo del salón: administradores y empleadas.

## Objetivo del dashboard

El dashboard busca centralizar la operación cotidiana del salón mediante una interfaz privada, con acceso y herramientas adaptadas al rol de cada persona:

| Perfil                  | Enfoque                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------- |
| **Admin / Super Admin** | Administración del negocio, configuración y consulta de la operación y sus resultados. |
| **Empleada**            | Consulta y gestión de las tareas y citas de su jornada, según los permisos asignados.  |

El alcance previsto para la interfaz incluye:

- **Agendas de trabajo:** visualizar y coordinar citas en paralelo para el equipo.
- **Servicios:** administrar el catálogo de servicios predefinidos (crear, consultar, editar y eliminar).
- **Métricas mensuales:** consultar indicadores financieros del mes.
- **Cierre de mes:** descargar reportes en Excel y aplicar la política definida para la purga de datos antiguos.
- **Permisos por rol:** mostrar las secciones y acciones permitidas para cada perfil.

La autenticación, los permisos efectivos, la persistencia y las reglas de negocio deben validarse también en el backend que consume el dashboard; ocultar una acción en la interfaz no sustituye la autorización del servidor.

## Tecnologías

Las dependencias configuradas actualmente en este repositorio son:

- **React 19** y **TypeScript** para construir la interfaz.
- **React Router 8** para rutas y renderizado de la aplicación.
- **Tailwind CSS 4** para estilos.
- **Vite 8** como herramienta de desarrollo y build.

FullCalendar, ExcelJS y JWT forman parte de las tecnologías que podrían incorporarse al producto para calendarios, exportación de reportes y autenticación, respectivamente; **no son dependencias instaladas actualmente** en este frontend.

## Requisitos

- Node.js compatible con las versiones instaladas en el proyecto.
- npm.

No se requiere una base de datos para ejecutar la pantalla inicial actual. Cuando se integre con la API de NailFlow, el acceso a los datos dependerá de que ese servicio esté disponible y de la configuración que se defina para el entorno.

## Instalación y desarrollo local

```bash
npm install
npm run dev
```

El servidor de desarrollo mostrará en la terminal la URL local, normalmente `http://localhost:5173`.

### Scripts disponibles

| Comando             | Descripción                                       |
| ------------------- | ------------------------------------------------- |
| `npm run dev`       | Inicia el servidor de desarrollo de React Router. |
| `npm run typecheck` | Genera los tipos de rutas y ejecuta TypeScript.   |
| `npm run build`     | Genera el build de producción.                    |
| `npm run start`     | Sirve el build de producción generado.            |

Para probar una compilación de producción:

```bash
npm run typecheck
npm run build
npm run start
```
