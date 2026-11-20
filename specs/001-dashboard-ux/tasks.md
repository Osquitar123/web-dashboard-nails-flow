# Tareas de la vista inicial del dashboard por rol

**Entradas** · [Spec aprobada](./spec.md), [plan técnico](./plan.md), [modelo](./data-model.md), [contrato](./contracts/dashboard.md) y [guía de validación](./quickstart.md).

Las rutas de código son relativas a la raíz del repositorio. `[P]` identifica tareas que se pueden ejecutar en paralelo dentro de la misma fase. Los criterios `AC` corresponden a la spec. La implementación se revisará una vista a la vez.

## Fase 1 · Preparación

- [ ] T001 Comprobar el punto de partida con Node.js 24 y los comandos de `package.json`. Registrar cualquier fallo previo siguiendo `specs/001-dashboard-ux/quickstart.md`. **FR-001 a FR-008**.

## Fase 2 · Base compartida

- [ ] T002 [P] Definir en `app/features/dashboard/model/dashboard.ts` los tipos de vista de los tres perfiles según [data-model.md](./data-model.md). Aplicar las reglas de Perfil.roles, Perfil.integrante, Integrante.identificador, Jornada.fecha, Cita.identificador, Cita.integrante, Cita.hora, Cita.estado y Métricas.período e importe. **FR-001 a FR-008**.
- [ ] T003 [P] Definir en `app/app.css` las variables semánticas de fondo, superficie, texto, bordes y acción bajo `data-dashboard-theme`, aplicando `DESIGN.md`. Mantener disponibles los tokens boutique para acceso y registro. **AC-02**.
- [ ] T004 Preparar en `app/features/dashboard/data/dashboardData.server.ts` los datos ficticios y las cifras por integrante y período, según [data-model.md](./data-model.md). Incluir una fecha fija, citas desordenadas, una cita en curso, un nombre largo y variantes con una o ninguna cita. **AC-01, AC-06, AC-07, AC-08, AC-12, AC-13, AC-14**.

## Fase 3 · US1 · Jornada de la trabajadora (P1, primera entrega)

**Prueba independiente** · Abrir `/?demo=trabajadora` con las variantes de jornada y verificar los datos personales, el orden, el detalle y las tres métricas.

- [ ] T005 [US1] Preparar la vista de trabajadora en `app/features/dashboard/data/dashboardData.server.ts` y entregarla desde el loader de `app/routes/home.tsx`. Resolver los casos de agenda solo en desarrollo y usar la vista sintética predeterminada fuera de desarrollo. Proyectar solo citas y métricas propias antes de serializar. **AC-01, AC-06, AC-07, AC-08**.
- [ ] T006 [P] [US1] Adaptar `app/features/dashboard/components/UpcomingAppointmentsTable.tsx` con fecha y estado vacío, tabla desde `md`, lista móvil y 14 px arriba y abajo por cita. Mantener el destino de navegación `#appointments`. **AC-02, AC-06, AC-07**.
- [ ] T007 [P] [US1] Crear `app/features/dashboard/components/HighlightedAppointment.tsx` para mostrar «Cita en curso» o «Próxima cita» según la selección del loader. Implementar **Ver detalle** con los cuatro datos básicos y un desplegable accesible. **AC-06, AC-08**.
- [ ] T008 [P] [US1] Adaptar `app/features/dashboard/components/MetricsOverview.tsx` y `app/features/dashboard/components/MetricCard.tsx` para presentar las tres cifras y el selector de período. La página controla la selección. **AC-13, AC-14**.
- [ ] T009 [US1] Componer cita destacada, agenda y métricas personales en `app/features/dashboard/pages/DashboardPage.tsx`. Inicializar el selector en «Hoy» y aplicar tipografía y paleta a los bloques y a `app/features/dashboard/components/DashboardHeader.tsx` y `app/features/dashboard/components/DashboardSidebar.tsx`. Conservar el interruptor y su persistencia. **AC-01, AC-02, AC-13, AC-14**.
- [ ] T010 [US1] Verificar la vista de trabajadora siguiendo `specs/001-dashboard-ux/quickstart.md`. Mostrar el resultado al usuario y acordar la aprobación antes de implementar la superadmin. **AC-01, AC-02, AC-06, AC-07, AC-08, AC-13, AC-14**.

## Fase 4 · US2 · Resumen del salón (P1)

**Prueba independiente** · Abrir `/?demo=superadmin`, comprobar métricas antes de la jornada del equipo y consultar las cifras de dos personas.

- [ ] T011 [US2] Ampliar `app/features/dashboard/data/dashboardData.server.ts` y `app/routes/home.tsx` para servir el escenario superadmin en desarrollo. Entregar la agenda con la trabajadora asignada, el total por período y el detalle de cada integrante. **AC-09, AC-10, AC-13**.
- [ ] T012 [US2] Componer la vista y regular el ámbito de métricas en `app/features/dashboard/pages/DashboardPage.tsx`. Añadir el selector de integrante en `app/features/dashboard/components/MetricsOverview.tsx` y mostrar quién atiende cada cita del equipo en `app/features/dashboard/components/UpcomingAppointmentsTable.tsx`. El total inicial, el detalle y el regreso al total conservan el período elegido. **AC-09, AC-10, AC-13, AC-14**.
- [ ] T013 [US2] Verificar la vista superadmin siguiendo `specs/001-dashboard-ux/quickstart.md`. Mostrar el resultado al usuario y acordar la aprobación antes de implementar ambos roles. **AC-09, AC-10, AC-13, AC-14**.

## Fase 5 · US3 · Salón y citas propias en una cuenta (P1)

**Prueba independiente** · Abrir `/?demo=ambos&caso=en-curso`, verificar el orden y reconciliar el total con la suma individual.

- [ ] T014 [US3] Incorporar el escenario con ambos roles en `app/routes/home.tsx` y `app/features/dashboard/data/dashboardData.server.ts`. Proyectar citas propias y del resto sin duplicar la asignación. Incluir una vez las métricas personales de la dueña en cada total. **AC-11, AC-12, AC-13**.
- [ ] T015 [US3] Componer el resumen del salón, las citas propias y la jornada del resto en `app/features/dashboard/pages/DashboardPage.tsx`. Habilitar el detalle individual propio desde las métricas y usar identificadores distintos para ambas agendas. **AC-11, AC-12, AC-14**.
- [ ] T016 [US3] Verificar la vista con ambos roles siguiendo `specs/001-dashboard-ux/quickstart.md` y mostrarla al usuario para cerrar el tercer bloque. **AC-11, AC-12, AC-13, AC-14**.

## Fase 6 · US4 · Períodos del resumen (P2)

**Prueba independiente** · Alternar los tres períodos en los tres perfiles, con más de una persona seleccionable en administración.

- [ ] T017 [US4] Completar la verificación de los selectores de `app/features/dashboard/pages/DashboardPage.tsx` siguiendo `specs/001-dashboard-ux/quickstart.md`. Confirmar tres cifras correctas por período, ámbito conservado y la misma fecha y citas en la agenda. Corregir cualquier discrepancia antes de cerrar la historia. **AC-13, AC-14**.

## Fase 7 · Verificación final

- [ ] T018 Ejecutar los comandos de verificación de `package.json` y recorrer la matriz de `specs/001-dashboard-ux/quickstart.md`. Registrar criterios verificados y evidencia de móvil, escritorio, ambos temas y teclado. **SC-001, SC-002, SC-003**.

## Dependencias y estrategia

La base compartida precede a cada historia. El orden de entrega es **US1 → US2 → US3 → US4**. US2 reutiliza los componentes de US1. US3 combina los bloques de ambas historias. US4 empieza con el selector que se entrega en US1 y se cierra al comprobar los tres perfiles. La verificación final sigue al cierre de US4.

T002 y T003 se pueden ejecutar en paralelo. En US1, T006, T007 y T008 usan tipos compartidos y modifican archivos distintos, por lo que se pueden hacer en paralelo una vez definida la base. Cada vista pasa por su revisión antes de avanzar.
