# Plan técnico de la vista inicial del dashboard por rol

**Feature** · `001-dashboard-ux` · Rama Git actual `main`  
**Fecha** · 2026-11-20  
**Estado** · Aprobado  
**Entrada** · [Spec aprobada](./spec.md)

## Resumen

Adaptar la página inicial para trabajadora, superadmin y cuenta con ambos roles. La ruta prepara los datos de ejemplo del perfil y la página compone agenda y métricas en el orden aprobado. El trabajo empieza por la vista de trabajadora. Revisar cada perfil con el usuario antes de avanzar al siguiente.

## Contexto técnico

- **Stack** · Node.js 24, TypeScript, React, React Router, Vite y Tailwind CSS del repositorio.
- **Datos** · Perfiles, citas y métricas sintéticos con fecha fija. El resumen se prepara para tres períodos. La integración con identidad, reservas, pagos y persistencia pertenece a las funcionalidades correspondientes.
- **Validación** · `npm test`, `npm run build` y pruebas de navegador en móvil y escritorio. Usar la [guía de validación](./quickstart.md).

## Comprobación de la constitución

Aplicar la [constitución](../../.specify/memory/constitution.md) y las reglas de [interfaz](../../app/AGENTS.md). Separar el acceso a datos, la composición y los componentes. Entregar al navegador solo los datos sintéticos que correspondan a su perfil de prueba. Para la integración real, el servidor resolverá la identidad y autorizará los datos antes de entregarlos. Verificar orden de lectura, foco, contraste, texto de estado y movimiento reducido en ambos temas. Vincular la evidencia con los criterios de la spec.

Revisión posterior al diseño · El alcance se verifica con los tres perfiles de prueba, el contrato acota el acceso a datos y los escenarios de la guía cubren los criterios aprobados.

## Estructura y flujo

- **Entrada.** Mantener `/` y usar un loader en `app/routes/home.tsx` para resolver el perfil sintético. En desarrollo, una URL permite probar los tres perfiles y las variantes de la agenda. Fuera de desarrollo se usa el perfil sintético predeterminado.
- **Datos.** En `app/features/dashboard/`, mantener los tipos en `model/` y preparar los datos por perfil en un módulo de servidor de `data/`. La página recibe solo la parte correspondiente al perfil. Consultar el [modelo](./data-model.md) y el [contrato de interfaz](./contracts/dashboard.md).
- **Pantalla.** Componer los tres órdenes en la página existente y reutilizar los componentes de agenda y métricas. Reemplazar los indicadores y gráficos del prototipo por los bloques de la spec. Conservar `#appointments` para la agenda visible y un identificador distinto si la vista contiene una segunda agenda.
- **Agenda.** Usar tabla con encabezados desde `md` y lista adaptable por debajo. Alimentar ambas presentaciones con la misma selección de citas y mostrar una sola para cada ancho. Implementar **Ver detalle** como un desplegable accesible junto a la cita destacada, con los cuatro datos básicos. La spec de gestión de citas definirá el contenido ampliado y las acciones.
- **Métricas.** Mantener en la página el período y, cuando el perfil lo permita, la persona elegida. Inicializar en «Hoy» y en el ámbito aprobado. Actualizar el resumen al cambiar cualquiera de los dos selectores. Mantener la agenda de hoy independiente de estos controles.
- **Diseño.** Aplicar los colores acordados en [DESIGN.md](../../DESIGN.md) mediante variables de color semánticas limitadas al dashboard. Usar Inter y 14 px arriba y abajo de cada cita. Conservar el selector sol/luna con la preferencia persistida.

## Orden de entrega y revisión

| Bloque | Criterios |
| --- | --- |
| Trabajadora. Comprobar cita destacada, detalle básico, agenda y resumen personal con selector de período. | AC-01, AC-02, AC-06, AC-07, AC-08, AC-13, AC-14 |
| Superadmin. Añadir la jornada del equipo, el total del salón y el detalle individual. | AC-09, AC-10, AC-13, AC-14 |
| Ambos roles. Integrar las citas propias y comprobar el total y el detalle personal de la dueña. | AC-11, AC-12, AC-13, AC-14 |

El [plan de validación](./quickstart.md) describe las comprobaciones para cada bloque. Las [tareas de implementación](./tasks.md) siguen el orden de entrega aprobado.
