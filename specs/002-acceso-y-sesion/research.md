# Decisiones técnicas de acceso y sesión

| Decisión | Motivo | Alternativa considerada |
| --- | --- | --- |
| Definir un contrato funcional y preparar primero el formulario. | El proyecto arrancó por el frontend. La pantalla y sus estados pueden revisarse con respuestas de prueba. | Elegir ahora un proveedor de identidad y correo. Esa decisión corresponde a la integración. |
| Reutilizar el diseño boutique de acceso y su punto de entrada `/login`. | Mantiene la identidad visual y el login común para ambos roles. | Crear un login por perfil. La cuenta ya dispone de roles asignados. |
| Tratar el vencimiento del servidor como la fuente del estado de sesión. | La medianoche debe seguir la zona horaria del salón, incluso si el dispositivo usa otra. | Calcular el vencimiento desde la hora local del navegador. Puede producir una hora distinta. |
| Revisar los estados de la interfaz y probar persistencia con una sesión ficticia exclusivamente en desarrollo. | Permite comprobar las redirecciones y el vencimiento con el dashboard de ejemplo. La verificación de permisos reales corresponde al entorno integrado. | Probar la sesión únicamente con vistas estáticas, sin poder verificar recargas ni redirecciones. |
