# Contrato esperado del servicio de acceso

Estas son capacidades y resultados que el frontend necesita. La integración acordará la API efectiva, el transporte y el proveedor. Los roles y el salón se obtienen de la cuenta autenticada.

| Operación | Entrada | Resultado esperado |
| --- | --- | --- |
| Iniciar sesión | Correo y contraseña | Sesión activa y cuenta autorizada, error genérico de credenciales o servicio no disponible. |
| Consultar sesión | Sesión actual | Cuenta, roles, salón, hora del servidor y vencimiento. Una sesión ausente o vencida lleva al login. |
| Cerrar sesión | Sesión actual | Revocación de esa sesión. La navegación posterior abre el login. |
| Solicitar recuperación | Correo | Confirmación uniforme. El servicio envía un enlace temporal si corresponde a una cuenta habilitada. |
| Restablecer contraseña | Enlace de recuperación y nueva contraseña | Cambio confirmado o enlace inválido, vencido o usado. Tras éxito se vuelve al login. |
| Enviar invitación | Sesión de superadmin, correo de destino y rol ofrecido | Invitación emitida para ese salón y válida por 3 días, o rechazo por falta de permiso o error del servicio. |
| Reenviar invitación | Sesión de superadmin e identificador de invitación pendiente o vencida | Nuevo enlace de 3 días para el mismo correo. El enlace anterior pierde vigencia. |
| Aceptar invitación | Enlace de invitación y nueva contraseña | Cuenta vinculada al salón con el rol ofrecido y acceso al login, o un resultado de enlace inválido o vencido. |

Una operación protegida verifica sesión y permisos antes de leer o cambiar datos. El frontend redirige a `/login` cuando la sesión falta o vence. Ante una sesión válida con permisos insuficientes, la operación se rechaza y el panel muestra un estado de acceso restringido.
