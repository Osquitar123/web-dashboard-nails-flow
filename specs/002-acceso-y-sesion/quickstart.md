# Validar acceso y sesión

Usar Node.js 24 y ejecutar `npm ci` y `npm run dev` desde la raíz. Antes del PR de código, ejecutar también `npm test` y `npm run build`.

## Primera entrega · Revisar login

Abrir `/login` en móvil y escritorio. Comprobar las etiquetas, el foco y que la opción de recuperación sea visible. Revisar los estados de envío, error genérico y servicio no disponible con respuestas de prueba. Esta revisión cubre la presentación de AC-01 y AC-02. El siguiente bloque conecta la opción con la pantalla de recuperación.

En desarrollo, abrir `/login?estado=pending`, `/login?estado=invalid` y `/login?estado=unavailable` para inspeccionar esos estados. La compilación de producción muestra siempre el estado de acceso pendiente de integración.

Para probar el envío en desarrollo, abrir `/login` e ingresar el correo `prueba@example.test` y la contraseña ficticia `NaraDemo2026!`. Al coincidir, el formulario abre el dashboard de ejemplo y guarda una sesión de prueba hasta la siguiente medianoche de `America/Bogota`. Cambiar la contraseña muestra el error genérico.

Con la sesión activa, recargar `/` y abrir `/login` directamente. Ambos llevan al dashboard. Pulsar **Cerrar sesión** y abrir `/` para comprobar la redirección al login. La revisión con datos reales se hará cuando exista el servicio de identidad.

## Entregas siguientes · Revisar recuperación e invitaciones

- Probar la confirmación de solicitud de recuperación, el formulario de contraseña nueva y el tratamiento de un enlace inválido o vencido. **AC-08, AC-09**.
- Probar **Invitar al equipo** con respuestas de superadmin y trabajadora, y revisar los estados de envío, aceptación, vencimiento y reenvío. **AC-03, AC-04, AC-05, AC-06, AC-07**.

## Tras conectar el servicio · Verificar acceso real

| Caso | Resultado esperado | Criterios |
| --- | --- | --- |
| Cuenta de trabajadora, superadmin y ambos roles, además de credenciales inválidas | El mismo login abre la vista autorizada para cada cuenta. Las credenciales inválidas dan un mensaje genérico. | AC-01, AC-02 |
| Salón habilitado, invitación de cada rol y solicitud hecha por una trabajadora | La superadmin inicial invita. El alta aplica el rol indicado. El servidor rechaza la solicitud de la trabajadora. | AC-03, AC-04, AC-05 |
| Invitación al vencer su tercer día y reenvío | El enlace vencido se rechaza. Solo el enlace más reciente permite aceptar durante su vigencia. | AC-06, AC-07 |
| Correo conocido y desconocido, enlace válido, vencido y reutilizado | Confirmación uniforme, cambio de contraseña con un enlace válido y rechazo del enlace vencido o utilizado. | AC-08, AC-09 |
| Abrir y recargar sin sesión, pasar de medianoche con la página abierta y ejecutar una acción vencida | El panel vuelve al login. La acción vencida se rechaza antes de aplicar cambios. Repetir con el dispositivo en una zona horaria diferente de la del salón. | AC-10, AC-11, AC-12 |
| Cerrar una de dos sesiones de la misma cuenta | El dispositivo actual vuelve al login y el otro conserva su sesión. | AC-13 |

Registrar la evidencia de cada fase. Los resultados con respuestas de prueba sirven para revisar la interfaz. Confirmar la autenticación y los permisos con el servicio integrado.
