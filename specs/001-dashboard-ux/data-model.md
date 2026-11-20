# Modelo de datos de ejemplo

| Entidad | Campos y relaciones |
| --- | --- |
| Perfil | Identificador estable y roles asignados. Una cuenta con rol de trabajadora tiene un identificador de integrante del salón. |
| Integrante | Identificador y nombre visible. Una dueña con ambos roles aparece como una integrante en las métricas y en la asignación de citas. |
| Jornada | Fecha de referencia fija y citas de ese día. Es la misma al cambiar el período de métricas. |
| Cita | Identificador estable, integrante asignada, hora de inicio ordenable, nombre ficticio de clienta, servicio y estado con etiqueta en texto. |
| Métricas | Por integrante y período, número de citas por atender, número de citas completadas e importe cobrado por servicios en unidades monetarias menores. Formatear al mostrar. |

## Selección y totales

- La cita destacada es la cita en curso o, si no hay una, la primera próxima cita por hora. Los casos de ejemplo tienen como máximo una cita en curso por integrante.
- La agenda personal muestra las citas próximas restantes en orden cronológico. La agenda del equipo identifica a la trabajadora de cada cita. Con ambos roles, la agenda del equipo excluye las citas de la dueña ya cubiertas en su sección personal.
- El total del salón suma una vez los valores de cada integrante para el mismo período. Incluir los cobros de la dueña que trabaja en el total y en su detalle individual.
- Preparar cifras distintas para «Hoy», «Esta semana» y «Este mes». Los valores de ejemplo tienen una moneda común y quedan fijados para las pruebas. Las reglas de cálculo con datos reales se acordarán en la integración correspondiente.
