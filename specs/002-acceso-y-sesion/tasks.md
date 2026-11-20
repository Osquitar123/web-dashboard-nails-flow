# Tareas de acceso y sesión

**Entradas** · [Spec](./spec.md), [plan](./plan.md), [modelo](./data-model.md), [contrato](./contracts/auth-service.md) y [validación](./quickstart.md).

Las rutas de código son relativas a la raíz. Cada bloque de interfaz se revisa con el usuario antes de empezar el siguiente. Las tareas de integración empiezan cuando haya un servicio de identidad y un entorno de pruebas.

## Fase 1 · Preparación

- [X] T001 Confirmar la configuración y comprobar el estado inicial con los scripts de `package.json` y las rutas de `app/routes.ts`. **FR-001**.

## Fase 2 · Base de la primera entrega

- [X] T002 Definir en `app/features/auth/components/LoginForm.tsx` los estados tipados del formulario y seleccionarlos para revisión aislada desde `app/routes/login.tsx`, solo en desarrollo. Mantener deshabilitado el envío real. **AC-01, AC-02**.

## Fase 3 · US1 · Login único (P1)

**Prueba independiente** · Abrir `/login` en móvil y escritorio, revisar los campos, la opción de recuperación y los estados visuales.

- [X] T003 [US1] Reutilizar el diseño boutique de `app/features/auth/pages/AuthPage.tsx` para mostrar correo, contraseña y recuperación, con etiquetas persistentes y mensajes accesibles en `app/features/auth/components/LoginForm.tsx`. **AC-01, AC-02**.
- [X] T004 [US1] Verificar la entrega visual con `specs/002-acceso-y-sesion/quickstart.md` y mostrar el resultado al usuario antes de avanzar. **AC-01, AC-02**.

## Fase 4 · US3 · Recuperación (P1)

**Prueba independiente** · Abrir la solicitud desde el login y comprobar las pantallas de confirmación, contraseña nueva y enlace vencido.

- [ ] T005 [US3] Conectar la opción de recuperación de `app/features/auth/components/LoginForm.tsx` con las pantallas de recuperación. Añadir sus rutas en `app/routes.ts`, usando los resultados definidos para Recuperación en [data-model.md](./data-model.md). **AC-08, AC-09**.
- [ ] T006 [US3] Revisar con estados de prueba la confirmación uniforme, el enlace inválido y el retorno al login, siguiendo `specs/002-acceso-y-sesion/quickstart.md`. Mostrar esta entrega al usuario. **AC-08, AC-09**.

## Fase 5 · US2 · Invitaciones (P1)

**Prueba independiente** · Revisar la opción de superadmin, el formulario por correo y la aceptación con estados de prueba.

- [ ] T007 [US2] Preparar **Invitar al equipo** en `app/features/dashboard/pages/DashboardPage.tsx` y `app/features/auth/components/InviteForm.tsx`. Usar el correo, el rol y la vigencia de Invitación descritos en [data-model.md](./data-model.md). **AC-03, AC-04, AC-05, AC-06, AC-07**.
- [ ] T008 [US2] Adaptar `app/routes/register.tsx` y los componentes de `app/features/auth/` para aceptar una invitación y presentar estados de enlace vigente, vencido o inválido. Revisar el flujo con `specs/002-acceso-y-sesion/quickstart.md` y mostrarlo al usuario. **AC-04, AC-06, AC-07**.

## Fase 6 · Integración con identidad y sesión

**Prueba independiente de US4** · Abrir el panel con dos sesiones, probar el límite de medianoche y comprobar la redirección de accesos o acciones vencidos. Requiere el servicio de identidad.

- [ ] T009 [US1] Conectar el login en `app/routes/login.tsx` con el servicio desde `app/features/auth/data/authService.server.ts`. Usar Cuenta.roles y Cuenta.salón de [data-model.md](./data-model.md) para entrar a la vista autorizada. **AC-01, AC-02**.
- [ ] T010 [US2] Conectar el envío, reenvío y aceptación en `app/features/auth/data/authService.server.ts` y `app/routes/register.tsx`. Validar permisos y vigencia conforme a Invitación.rol e Invitación.vencimiento en [data-model.md](./data-model.md). **AC-03, AC-04, AC-05, AC-06, AC-07**.
- [ ] T011 [US3] Conectar recuperación en `app/features/auth/data/authService.server.ts` y sus rutas de formulario. Validar los resultados de Recuperación en [data-model.md](./data-model.md) y comprobar el enlace de un solo uso. **AC-08, AC-09**.
- [ ] T012 [US4] Aplicar el control de sesión en `app/routes/home.tsx` y las demás rutas protegidas desde `app/features/auth/data/session.server.ts`. Usar Sesión.hora de fin y Salón.zona horaria de [data-model.md](./data-model.md). En `app/features/dashboard/pages/DashboardPage.tsx`, redirigir al vencer y ofrecer cierre de la sesión actual. **AC-10, AC-11, AC-12, AC-13**.

## Fase 7 · Verificación final

- [ ] T013 Ejecutar los scripts de `package.json` y los escenarios integrados de `specs/002-acceso-y-sesion/quickstart.md`. Registrar resultados por criterio y adjuntar evidencia de móvil y escritorio. **SC-001, SC-002, SC-003, SC-004**.

## Dependencias y entrega

T001 precede a T002–T004. El primer bloque termina al revisar el login visual. Recuperación e invitaciones reutilizan su base y tienen revisiones separadas. Las tareas de integración requieren el contrato efectivo del servicio y sus cuentas de prueba. T013 sigue a la integración. El orden de revisión acordado determina la entrega de los bloques.
