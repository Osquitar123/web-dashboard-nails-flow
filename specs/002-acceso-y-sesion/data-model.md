# Datos esperados por el frontend de acceso

| Entidad | Datos y reglas |
| --- | --- |
| Cuenta | Identificador de cuenta, correo, salón y roles asignados. Puede tener uno o ambos roles. Las credenciales se entregan al servidor solo para la operación correspondiente. |
| Salón | Identificador y zona horaria de referencia. Empieza con una cuenta de superadmin habilitada. |
| Sesión | Identidad y roles autorizados, hora de referencia del servidor y hora absoluta de fin. Cada sesión puede cerrarse de forma independiente. |
| Invitación | Identificador, correo de destino, salón, rol ofrecido y fecha de vencimiento. El servicio controla el enlace vigente y lo reemplaza en cada reenvío. La vigencia es de 3 días desde cada envío. |
| Recuperación | Resultado uniforme de solicitud y estado de validación del enlace. El servicio verifica la vigencia y el uso único antes de cambiar la contraseña. |

La interfaz recibe la información mínima para presentar cada pantalla. Los mecanismos de sesión, validación de enlaces y persistencia pertenecen a la integración.
