# Plan técnico de acceso y sesión del panel

**Feature** · `002-acceso-y-sesion` · Rama Git actual `main`  
**Fecha** · 2026-11-20  
**Estado** · Aprobado  
**Entrada** · [Spec aprobada](./spec.md)

## Resumen

Preparar el login único del dashboard con correo y contraseña. La primera entrega será la pantalla de acceso con sus estados y el enlace de recuperación, para revisarla contigo en móvil y escritorio. Las pantallas de recuperación e invitación se revisarán en entregas posteriores. La conexión con un servicio de identidad será una fase separada.

## Contexto técnico

- **Stack** · Node.js 24, TypeScript, React Router en modo Framework y Tailwind CSS. Usar la paleta de acceso definida en [DESIGN.md](../../DESIGN.md).
- **Punto de partida** · `/login` y `/registro` comparten una pantalla con controles deshabilitados. El dashboard usa datos ficticios.
- **Integración** · El repositorio empezó por el frontend. El [contrato del servicio](./contracts/auth-service.md) define operaciones y respuestas esperadas con independencia del proveedor. El servicio deberá disponer de identidad, roles por salón, zona horaria y envío de correos.
- **Validación** · Usar `npm test`, `npm run build` y la [guía de validación](./quickstart.md). Registrar por separado la revisión visual y los resultados de la integración real.

## Comprobación de la constitución

Aplicar la [constitución](../../.specify/memory/constitution.md). Las rutas coordinan formularios y redirecciones. Los componentes reciben estados tipados y presentan la interfaz. El servicio verifica sesión, salón y permisos en cada operación protegida. Las rutas privadas sirven datos reales únicamente tras esa comprobación. Los datos de ejemplo se limitan al dashboard de demostración y a la revisión aislada de estados de interfaz.

Revisión posterior al diseño · El plan conserva el alcance del frontend, identifica las capacidades pendientes del servicio y vincula las comprobaciones con la spec.

## Estructura y entregas

| Bloque | Trabajo | Criterios relacionados |
| --- | --- | --- |
| 1. Login único | Adaptar la ruta `/login` y el formulario en `app/features/auth/`. Mostrar correo, contraseña, la acción de iniciar sesión y el enlace de recuperación. Preparar estados de envío, error genérico y servicio no disponible. Revisar la pantalla contigo antes de continuar. | AC-01, AC-02 |
| 2. Recuperación | Preparar la solicitud por correo y la pantalla para establecer una contraseña nueva. Representar confirmación uniforme, enlace inválido o vencido y retorno al login tras éxito. | AC-08, AC-09 |
| 3. Invitaciones | Preparar **Invitar al equipo** para superadmin y las pantallas de aceptación y reenvío. Reutilizar `/registro` como entrada de aceptación de una invitación. | AC-03, AC-04, AC-05, AC-06, AC-07 |
| 4. Integración y protección | Conectar las rutas con el servicio cuando esté disponible. Aplicar sesión y roles a las rutas y acciones protegidas, redirigir al login según el contrato y verificar vencimiento y cierre de sesión. | AC-01 a AC-13 |

En desarrollo, usar una cuenta ficticia y una sesión local para verificar persistencia, redirecciones y cierre a medianoche con el dashboard de ejemplo. La sesión de prueba usa `America/Bogota` y un identificador opaco en una cookie persistente. El acceso real requiere el servicio de identidad. La prueba integrada se hará en local o en un entorno de pruebas con cuentas y correos de prueba.

## Decisiones para la integración

- Mantener las llamadas al servicio y la gestión de sesión en módulos de servidor de `app/features/auth/`. Validar la sesión y los permisos para cada lectura y acción del panel. La sesión determina los roles que consume el dashboard.
- Aplicar la fecha de vencimiento absoluta calculada en el servidor para la próxima medianoche del salón. Con la pestaña abierta, programar su salida al login. Al recuperar foco después de una suspensión, volver a comprobar el vencimiento. El servidor sigue rechazando solicitudes vencidas. [OWASP, gestión de sesión](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
- Resolver el cierre manual sobre la sesión actual. En una integración del mismo origen, usar una cookie de sesión protegida y solicitudes POST protegidas frente a CSRF para los cambios de sesión. [OWASP, gestión de sesión](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
- Confirmar la vigencia del enlace de recuperación con el servicio elegido. Mantener uniforme la confirmación de solicitud y consumir el enlace una sola vez. [OWASP, recuperación de contraseña](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html)

Ver [decisiones técnicas](./research.md), [modelo de datos](./data-model.md) y [guía de validación](./quickstart.md).
