# Especificación de acceso y sesión del panel del salón

**Rama de la funcionalidad** · Sin rama dedicada  
**Fecha** · 2026-11-20  
**Estado** · Aprobada para planificación  
**Solicitud** · Proteger el panel con un login único y controlar el acceso mediante sesiones, roles e invitaciones.

## Escenarios de usuario y pruebas

El equipo del salón necesita una entrada común al panel. Las superadmins controlan quién se incorpora y cada persona accede al dashboard con los roles asignados a su cuenta.

### US1 · Entrar al panel con mi cuenta (P1)

**Prueba independiente** · Abrir el login en móvil y escritorio. Iniciar sesión con cuentas de trabajadora, superadmin y ambos roles.

1. **AC-01** · Dadas cuentas con roles distintos, cuando abren el login, entonces todas ven el mismo formulario de correo y contraseña y la opción «¿Olvidaste tu contraseña?». Al entrar con credenciales válidas, cada cuenta abre el dashboard correspondiente a sus roles ya asignados. [Vista inicial por rol](../001-dashboard-ux/spec.md).
2. **AC-02** · Dadas credenciales incorrectas, cuando se intenta iniciar sesión, entonces el panel muestra un error genérico y mantiene el acceso protegido.

### US2 · Incorporar personas por invitación (P1)

**Prueba independiente** · Usar la cuenta de superadmin habilitada para invitar a dos personas con roles distintos. Aceptar un enlace, probar un enlace vencido y comprobar el reenvío.

1. **AC-03** · Dado un salón habilitado, cuando empieza a usar el panel, entonces ya tiene una cuenta de superadmin que puede iniciar sesión e invitar al equipo.
2. **AC-04** · Dada una superadmin, incluso si también es trabajadora, cuando abre el panel, entonces ve **Invitar al equipo** y puede enviar una invitación al correo indicado como trabajadora o como superadmin. Quien recibe un enlace vigente puede aceptarlo, crear su contraseña y entrar con el rol asignado.
3. **AC-05** · Dada una cuenta que solo es trabajadora, cuando abre el panel, entonces **Invitar al equipo** está ausente. Si solicita el envío de todas formas, el servidor lo rechaza.
4. **AC-06** · Dada una invitación, cuando pasan 3 días desde su envío, entonces el enlace vence y deja de permitir el alta.
5. **AC-07** · Dada una invitación pendiente o vencida, cuando una superadmin la reenvía, entonces se emite un enlace para el mismo correo con otros 3 días de vigencia y el enlace anterior queda invalidado.

### US3 · Recuperar mi contraseña (P1)

**Prueba independiente** · Solicitar recuperación para una cuenta conocida y un correo desconocido. Usar el enlace recibido y probarlo una segunda vez.

1. **AC-08** · Dado el login, cuando una persona solicita recuperar su contraseña, entonces ve la misma confirmación para cualquier correo. Si corresponde a una cuenta habilitada, el sistema envía un enlace temporal de un solo uso.
2. **AC-09** · Dado un enlace de recuperación vigente, cuando la persona crea una nueva contraseña, entonces vuelve al login y puede entrar con la nueva contraseña. Si usa un enlace vencido o ya utilizado, el sistema rechaza el cambio.

### US4 · Proteger el panel cuando termina la sesión (P1)

**Prueba independiente** · Probar con dos sesiones de la misma cuenta y con el reloj de prueba antes y después de medianoche en la zona horaria del salón.

1. **AC-10** · Dada una persona sin sesión activa, cuando abre o recarga el dashboard, entonces el sistema la redirige al login antes de mostrar datos.
2. **AC-11** · Dado el dashboard abierto con una sesión activa, cuando llega la medianoche local del salón, entonces la sesión vence y la pantalla vuelve al login de inmediato.
3. **AC-12** · Dada una sesión vencida, cuando una persona solicita una acción del dashboard, entonces el servidor rechaza la operación antes de aplicar cambios y el panel vuelve al login.
4. **AC-13** · Dadas dos sesiones activas de la misma cuenta, cuando la persona cierra sesión en una, entonces ese dispositivo vuelve al login y la otra sesión sigue activa.

### Casos límite

- Los enlaces de invitación vencidos o reemplazados dejan el alta pendiente. La superadmin puede emitir un nuevo enlace.
- La medianoche se evalúa según la zona horaria del salón, incluso cuando el dispositivo está configurado en otra zona horaria.

## Requisitos

### Requisitos funcionales

| ID | Requisito | Aceptación |
| --- | --- | --- |
| FR-001 | Usar un único formulario de correo y contraseña para todos los roles. Tras el acceso, aplicar los roles asignados y abrir la vista que corresponde. | AC-01, AC-02 |
| FR-002 | Iniciar la operación de cada salón con una superadmin habilitada. Incorporar al resto del equipo únicamente por invitación. | AC-03, AC-04 |
| FR-003 | Mostrar y autorizar **Invitar al equipo** únicamente para cuentas con rol de superadmin. El envío debe registrar el correo y el rol elegido. La aceptación permite crear la contraseña y entrar con el rol invitado. | AC-04, AC-05 |
| FR-004 | Dar a cada invitación una vigencia de 3 días. Permitir reenvío por superadmin con un enlace nuevo que reinicia la vigencia e invalida el anterior. | AC-06, AC-07 |
| FR-005 | Ofrecer recuperación desde el login con confirmación uniforme y enlace temporal de un solo uso. Tras cambiar la contraseña, volver al login. | AC-08, AC-09 |
| FR-006 | Exigir que el servidor compruebe sesión y permisos al acceder a datos o ejecutar acciones protegidas. Redirigir al login si falta una sesión activa. | AC-01, AC-05, AC-10, AC-12 |
| FR-007 | Vencer la sesión a medianoche local del salón, volver al login si la pantalla sigue abierta y pedir un nuevo inicio de sesión. | AC-10, AC-11, AC-12 |
| FR-008 | Cerrar solo la sesión desde la que se pulsa **Cerrar sesión** y mostrar el login. | AC-13 |

### Entidades clave

- **Cuenta** · Correo, salón y roles asignados. Una cuenta puede tener uno o ambos roles según la spec del dashboard.
- **Invitación** · Salón, correo de destino, rol ofrecido, vigencia y enlace vigente.
- **Sesión** · Acceso activo desde el inicio de sesión hasta el cierre manual o la medianoche local del salón.
- **Enlace de recuperación** · Permiso temporal de un solo uso para cambiar la contraseña de la cuenta asociada.

## Criterios de éxito

- **SC-001** · Los tres perfiles de prueba usan un mismo login en móvil y escritorio y ven la vista que corresponde. Un acceso con credenciales incorrectas queda bloqueado. **AC-01, AC-02**.
- **SC-002** · Verificar una invitación de cada rol, un enlace vencido, un reenvío, la ausencia de la opción en la vista de trabajadora y el rechazo de su solicitud por el servidor. **AC-03, AC-04, AC-05, AC-06, AC-07**.
- **SC-003** · Verificar recuperación con correo conocido y desconocido, y el rechazo de un enlace utilizado o vencido. **AC-08, AC-09**.
- **SC-004** · Verificar redirección al login en apertura, recarga, vencimiento con la pantalla abierta y acción posterior al vencimiento. Verificar también cierre manual con otra sesión activa. **AC-10, AC-11, AC-12, AC-13**.

## Supuestos y alcance

- Esta spec cubre el acceso al panel interno del salón. La [vista inicial por rol](../001-dashboard-ux/spec.md) define el contenido que recibe cada perfil.
- La cuenta inicial de superadmin y la zona horaria del salón están disponibles antes del primer inicio de sesión. La forma de habilitar el primer salón pertenece a su propio flujo.
- El plan técnico definirá la integración de identidad y correo, la duración del enlace de recuperación y los mecanismos para terminar la sesión.
