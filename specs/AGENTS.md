# Convenciones de especificación de NailFlow

Consulta la [constitución](../.specify/memory/constitution.md) para conocer los principios, la base técnica y cuándo corresponde escribir una especificación. Aplica las convenciones de código de la [guía raíz](../AGENTS.md) y, para interfaz, las de [app/AGENTS.md](../app/AGENTS.md).

## Organización

Usa `specs/NNN-nombre-breve/` para cada cambio que se pueda revisar y validar por separado. Mantén el identificador cuando revises el mismo alcance. Escribe los documentos en español y conserva las secciones de las plantillas de Spec Kit.

## Qué va en cada archivo

- **`spec.md`** describe a quién afecta el problema, qué necesita hacer y por qué. Incluye alcance, exclusiones, historias priorizadas, requisitos, escenarios de aceptación y supuestos. Registra las decisiones pendientes que cambien el flujo o el alcance. Si la funcionalidad maneja datos, describe qué información necesita, quién puede usarla y qué reglas debe cumplir.
- **`plan.md`** explica cómo resolver los requisitos acordados dentro de la base técnica del proyecto. Documenta los módulos y contratos afectados, las dependencias y la estrategia de validación. Cuando se incorpore persistencia, registra la elección del servicio o motor, el esquema y las migraciones que hagan falta. Referencia el [sistema de diseño](../DESIGN.md) para cambios visuales.
- **`tasks.md`** especifica acciones verificables en orden de dependencia. Cada tarea enlaza la historia, el requisito o el criterio que implementa o verifica.

## Cómo revisar una propuesta

Usa identificadores estables como `US1` para historias, `FR-001` para requisitos, `SC-001` para criterios de éxito y `T001` para tareas. Mantén los identificadores de documentos existentes cuando sigan describiendo el mismo comportamiento.

Redacta escenarios desde la perspectiva de quien usa el panel. Ejemplo.

> Dado que hay citas para la jornada, cuando una integrante del salón consulta la agenda en el teléfono, entonces puede leer la hora, el cliente y el estado de cada cita juntos, sin desplazamiento horizontal.

Revisa primero el problema, el alcance y los escenarios. Cuando estén acordados, prepara el plan y las tareas y comprueba que cubran los requisitos. Si cambian los escenarios, actualiza los artefactos afectados. Registra en el PR la evidencia de los criterios verificados según [la constitución](../.specify/memory/constitution.md).
