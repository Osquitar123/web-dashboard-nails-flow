# Validar la vista inicial del dashboard

Esta guía se ejecuta a medida que se completa cada bloque de implementación. Usar Node.js 24.

```bash
npm ci
npm run dev
```

Abre la URL que indica Vite y añade estas rutas. Compara las cifras con los datos sintéticos del período y el perfil elegidos.

| Ruta | Comprobación | Criterios |
| --- | --- | --- |
| `/?demo=trabajadora&caso=proximas` | La cita más próxima se destaca, las demás están ordenadas, y las métricas propias quedan al final. Verifica que los datos entregados al navegador tampoco contengan citas ni métricas de otras trabajadoras. | AC-01, AC-02, AC-06, AC-08 |
| `/?demo=trabajadora&caso=en-curso` | Se destaca la cita en curso aunque exista otra próxima. **Ver detalle** abre esa misma cita. | AC-08 |
| `/?demo=trabajadora&caso=una` y `/?demo=trabajadora&caso=vacia` | Una cita muestra sus cuatro datos. La jornada vacía muestra fecha y «No hay próximas citas para hoy». | AC-02, AC-07 |
| `/?demo=superadmin` | El total del salón aparece antes de la agenda del equipo. Consulta las cifras de dos trabajadoras y vuelve al total. | AC-09, AC-10 |
| `/?demo=ambos&caso=en-curso` | Aparecen el resumen del salón, las citas propias y la jornada de las demás trabajadoras, en ese orden. Las cifras de la dueña se pueden ver por separado y se incluyen una vez en el total. | AC-11, AC-12 |
| Los tres perfiles anteriores | El resumen inicia en «Hoy». Cambia a «Esta semana» y «Este mes». Las tres cifras deben corresponder al ámbito y período elegidos. Verifica que la agenda conserve su fecha y contenido. | AC-13, AC-14 |

Verifica móvil y escritorio en los dos temas, con un nombre largo de clienta. Comprueba la lectura sin desplazamiento horizontal y el acceso por teclado a **Ver detalle**, los selectores y el interruptor de tema. Alterna el tema, recarga y vuelve a probar con movimiento reducido. Adjunta al PR evidencia de móvil y escritorio e indica qué escenarios verificaste.

Antes del PR con código, ejecuta `npm test` y `npm run build`.
