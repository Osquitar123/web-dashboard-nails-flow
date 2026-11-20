# Constitución de NailFlow

## Principios fundamentales

### I. Especificar antes de implementar

Para cambios que introduzcan o modifiquen un flujo de usuario, permisos o reglas de
negocio, el equipo DEBE documentar el problema, el alcance y la aceptación en
`specs/` antes de implementar. El plan y las tareas DEBEN remitir a esos criterios.
Si cambia un requisito acordado, actualizar la especificación y los artefactos afectados.

### II. Mantener los límites del frontend

Organizar el código por funcionalidad y, dentro de cada una, por tipo. Las rutas
DEBEN suministrar datos y coordinar la navegación. Las páginas componen la vista
con componentes que reciben props tipadas. Los contratos y el acceso a datos
pertenecen a la funcionalidad que los usa. Compartir componentes cuando varias
funcionalidades los necesiten. Las rutas y carpetas están descritas en la
[guía del repositorio](../../AGENTS.md).

### III. Priorizar la operación del salón

La interfaz DEBE dar prioridad a las tareas del equipo, como consultar las citas y su estado. Los cambios visuales DEBEN seguir la [guía de interfaz](../../app/AGENTS.md) y [DESIGN.md](../../DESIGN.md). Verificar contraste en ambos temas, foco con teclado, estados expresados en texto y movimiento reducido cuando haya animación.

### IV. Verificar el comportamiento

Antes de abrir un PR con cambios de código, ejecutar `npm test` y `npm run build`. Para cambios visuales, comprobar los escenarios afectados en móvil y escritorio y adjuntar evidencia. Cuando un PR implemente una especificación, enlazarla e indicar qué criterios se verificaron.

### V. Seguridad de acceso y datos

Toda operación con datos protegidos DEBE autenticar la sesión y comprobar
permisos en el servidor. Validar allí las entradas de las operaciones de
escritura. Mantener secretos y credenciales de servicio fuera del repositorio y
del código que se entrega al navegador.

## Base técnica

- Usar Node.js 24 para reproducir CI. El dashboard usa React, React Router con
  renderizado en servidor, TypeScript, Vite y Tailwind CSS. Consultar
  [package.json](../../package.json) para las versiones de las dependencias.
- El código del dashboard vive en `app/`. Aplicar el patrón
  contenedor/presentación y las convenciones de la [guía raíz](../../AGENTS.md).
- El dashboard usa datos de ejemplo. La elección de un servicio de identidad o
  de persistencia se documenta en el plan de la funcionalidad que lo necesite,
  junto con las implicaciones para permisos y datos.

## Flujo de desarrollo y revisión

1. Escribir y revisar la especificación según la
   [guía de especificaciones](../../specs/AGENTS.md).
2. En el plan técnico, comprobar los principios aplicables y justificar las
   decisiones de arquitectura, dependencias o persistencia que introduzca el cambio.
3. Vincular las tareas a los criterios de aceptación y revisar la coherencia de
   los tres documentos antes de implementar. Registrar en el PR la evidencia
   de los criterios verificados.
4. Los mensajes de commit DEBEN seguir el formato `tipo: descripción breve`,
   con el tipo y la descripción en inglés y en minúsculas. Consultar la
   [guía raíz](../../AGENTS.md) para ver ejemplos.
5. Las nuevas ramas de trabajo DEBEN seguir el formato `tipo/descripcion-del-cambio`
   en inglés y en minúsculas, con guiones entre palabras. Los directorios de
   especificaciones conservan el formato `specs/NNN-nombre-breve/`.
6. Los pull requests (PR o MR) de ramas de trabajo DEBEN apuntar a `staging`.
   Para promover los cambios integrados, abrir un PR de `staging` hacia `main`.
7. Al crear un pull request, se DEBE usar la
   [plantilla del repositorio](../../.github/pull_request_template.md) y completar
   sus secciones con los cambios, verificaciones y evidencias reales de la rama.
   Enlazar la especificación cuando aplique e indicar qué quedó pendiente.

## Gobernanza

La constitución fija las reglas comunes del proyecto. Las guías `AGENTS.md` concretan
cómo aplicarlas y los planes registran las decisiones de cada funcionalidad. Si
una propuesta requiere cambiar una regla común, documentar el motivo y los
artefactos afectados en el PR y obtener su aprobación como enmienda.

Actualizar la fecha de enmienda y la versión con SemVer. Usar una versión mayor
si cambia una regla de forma incompatible, menor si se añade o amplía una regla,
y de parche para aclaraciones que conservan su significado.

**Versión** · 1.4.0 | **Adopción** · 2026-11-20 | **Última enmienda** · 2026-11-20
