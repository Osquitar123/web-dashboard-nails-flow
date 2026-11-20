# Especificación de la vista inicial del dashboard por rol

**Rama de la funcionalidad** · Sin rama dedicada  
**Revisión** · 2026-11-20  
**Estado** · Aprobada para planificación  
**Solicitud** · Dar prioridad a la atención de citas para las trabajadoras y al resumen del salón para las superadmins.

## Escenarios de usuario y pruebas

El personal que atiende necesita saber a quién atender y cómo va su propia jornada. Las dueñas necesitan una vista de todo el salón y pueden atender citas con la misma cuenta si tienen ambos roles.

### US1 · Consultar mi jornada como trabajadora (P1)

**Valor y prueba independiente** · Con una cuenta de trabajadora y datos de dos personas, abrir el dashboard y comprobar qué citas y métricas aparecen y en qué orden.

1. **AC-01** · Dado que una trabajadora tiene citas para hoy, cuando abre el panel, entonces encuentra su cita destacada, su agenda con la fecha de hoy y sus métricas personales, en ese orden. Solo ve sus propias citas y cifras.
2. **AC-02** · Dado que hay citas visibles, cuando consulta la agenda, entonces puede leer la hora, la clienta, el servicio y el estado en texto. En móvil, el servicio va debajo de la hora, la clienta y el estado, y el contenido se ajusta al ancho disponible. En escritorio, los encabezados identifican los cuatro datos.
3. **AC-06** · Dado que hay varias citas pendientes de hoy, cuando abre el panel sin una cita en curso, entonces la más próxima ocupa el bloque «Próxima cita». Las demás se muestran en orden cronológico.
4. **AC-07** · Dado que la jornada no tiene citas en curso ni próximas, cuando abre el panel, entonces la agenda muestra la fecha y el mensaje «No hay próximas citas para hoy».
5. **AC-08** · Dado que la trabajadora tiene una cita en curso y otra por atender, cuando abre el panel, entonces la primera ocupa el bloque «Cita en curso». Desde cualquiera de las dos variantes del bloque, **Ver detalle** abre la cita que aparece destacada.

### US2 · Revisar el salón como superadmin (P1)

**Valor y prueba independiente** · Con una cuenta que solo tiene el rol de superadmin, abrir el panel y consultar el resumen y el detalle de dos trabajadoras.

1. **AC-09** · Dado que la cuenta tiene el rol de superadmin, cuando abre el dashboard, entonces primero ve las métricas de todo el salón y luego la jornada de todo el equipo.
2. **AC-10** · Dado que el resumen muestra el total del salón, cuando la superadmin consulta el detalle de una trabajadora, entonces ve las métricas de esa persona para el período seleccionado y puede volver al total del salón.

### US3 · Revisar el salón y atender mis citas desde una cuenta (P1)

**Valor y prueba independiente** · Con una cuenta que tiene ambos roles, abrir el panel y verificar el orden de las secciones y el acceso a las métricas propias.

1. **AC-11** · Dado que una superadmin también tiene el rol de trabajadora, cuando abre el panel, entonces primero ve las métricas de todo el salón, después sus propias citas con la regla de cita destacada y por último la jornada de las demás trabajadoras.
2. **AC-12** · Dado que la superadmin ha atendido citas, cuando consulta las métricas, entonces su actividad forma parte del total del salón y puede consultar sus propias cifras por separado, además de las de las demás trabajadoras.

### US4 · Consultar métricas por período (P2)

**Valor y prueba independiente** · Con cifras de ejemplo distintas por período, cambiar el selector y comprobar qué cifras se actualizan.

1. **AC-13** · Dado cualquiera de los perfiles, cuando abre el dashboard, entonces el resumen inicia en «Hoy» y muestra **Citas por atender**, **Citas completadas** y **Total cobrado por servicios** para su ámbito de consulta.
2. **AC-14** · Dado que el resumen está en «Hoy», cuando la persona selecciona «Esta semana» o «Este mes», entonces se actualizan las tres métricas del ámbito que está consultando. La agenda sigue mostrando la jornada de hoy.

### Casos límite

- Con una sola cita próxima se muestran los cuatro datos en el bloque destacado.
- Una cita en curso sigue destacada aunque sea la única de la jornada.

## Requisitos

### Requisitos funcionales

| ID | Requisito | Aceptación |
| --- | --- | --- |
| FR-001 | Para una trabajadora, mostrar la cita destacada y la agenda personal de hoy antes de sus métricas. | AC-01 |
| FR-002 | Mostrar hora, clienta, servicio y estado en texto por cita. Adaptar la disposición a móvil y escritorio. | AC-02 |
| FR-003 | En la agenda personal, ordenar por hora las citas pendientes de hoy. Destacar la más próxima cuando no hay una cita en curso. | AC-06 |
| FR-004 | Mostrar la fecha y un mensaje explícito cuando no hay una cita en curso ni quedan próximas citas. | AC-07 |
| FR-005 | Dar prioridad a la cita en curso en el bloque personal y permitir abrir el detalle de la cita destacada. | AC-08 |
| FR-006 | La trabajadora solo puede consultar sus datos. La superadmin puede consultar los datos del salón y las métricas de cada trabajadora, y el panel abre en la vista general del salón. | AC-01, AC-09, AC-10 |
| FR-007 | Una cuenta puede tener uno o ambos roles. Con ambos, mostrar métricas del salón, citas personales y jornada del resto del equipo, en ese orden. Incluir la actividad propia en el total y permitir consultarla por separado. | AC-11, AC-12 |
| FR-008 | Mostrar citas por atender, citas completadas y total cobrado por servicios. Usar «Hoy» al abrir el panel y ofrecer «Hoy», «Esta semana» y «Este mes». Aplicar el período solo a las métricas. | AC-13, AC-14 |

### Entidades clave

- **Cuenta** · Puede tener el rol de trabajadora, el de superadmin o ambos.
- **Cita** · Pertenece a una trabajadora y tiene hora, clienta, servicio y estado.
- **Resumen de métricas** · Cifras de una persona o del salón para el período seleccionado. El total cobrado representa pagos de clientas por servicios.

## Criterios de éxito

- **SC-001** · En móvil y escritorio, en modo claro y oscuro, el perfil de trabajadora muestra exclusivamente sus datos. Se verifican una cita en curso, varias próximas, una sola próxima y la jornada vacía. **AC-01, AC-02, AC-06, AC-07, AC-08**.
- **SC-002** · Con tres perfiles de prueba se verifica el orden de los bloques, el acceso de superadmin al detalle individual y la inclusión de la dueña que atiende en el total del salón. **AC-01, AC-09, AC-10, AC-11, AC-12**.
- **SC-003** · En los tres perfiles se verifican las tres métricas al abrir en «Hoy», al cambiar a «Esta semana» y al cambiar a «Este mes». La fecha y el contenido de la agenda permanecen iguales al cambiar el período. **AC-13, AC-14**.

## Supuestos y alcance

- Usar datos de ejemplo para los tres perfiles. «Hoy» corresponde a la fecha de la jornada de ejemplo. El uso con datos reales depende de la [spec de acceso y sesión](../002-acceso-y-sesion/spec.md). El servicio debe entregar solo los datos autorizados para la cuenta.
- Esta spec cubre la vista inicial del panel y el acceso al detalle desde la cita destacada. El contenido del detalle, las reservas y las acciones sobre citas se documentarán en la spec de gestión de citas.
- La ganancia personal se especificará cuando se defina su cálculo. La web de clientas se especificará en su propio repositorio.
- El [plan técnico](./plan.md) y las [tareas](./tasks.md) siguen el alcance de esta spec. Los criterios AC-03 a AC-05 del piloto se retiran.
