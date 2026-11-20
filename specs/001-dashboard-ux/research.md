# Decisiones técnicas de la vista inicial

| Decisión | Motivo | Alternativa considerada |
| --- | --- | --- |
| Preparar la vista con datos de ejemplo en el loader de `/`. Usar parámetros de desarrollo para reproducir perfiles y casos. | Permite compartir una URL de revisión y entregar al navegador los datos correspondientes al perfil. | Selector de rol visible en la interfaz. Introduciría un control que no forma parte de la experiencia acordada. |
| Usar cifras por persona y período, y sumar los valores de cada integrante para el total del salón. | Permite verificar el alcance y la inclusión de la dueña con datos deterministas. | Calcular períodos y cobros a partir de movimientos reales. Requiere reglas de zona horaria, pagos e integración que pertenecen a otra etapa. |
| Abrir un detalle básico junto a la cita destacada. | Verifica la acción y la cita seleccionada dentro de la vista inicial. | Crear una pantalla de gestión de citas. Está prevista para su propia spec. |
| Aplicar variables de tema en el contenedor del dashboard y conservar su preferencia guardada. | Mantiene las dos paletas del dashboard y permite seguir usando los tokens boutique en acceso y registro. | Cambiar los tokens boutique globales. Cambiaría también los formularios de acceso. |
