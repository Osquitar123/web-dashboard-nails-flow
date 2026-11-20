# Contrato de interfaz del dashboard

## Entrada de la vista de ejemplo

En desarrollo, la ruta `/` acepta estos parámetros con valores explícitos:

| Parámetro | Valores |
| --- | --- |
| `demo` | `trabajadora`, `superadmin` o `ambos`. El valor predeterminado es `trabajadora`. |
| `caso` | `proximas`, `en-curso`, `una` o `vacia`. El valor predeterminado es `proximas`. Aplica a la agenda personal. |

Un valor omitido o desconocido usa su predeterminado. Fuera de desarrollo, usar el perfil y el caso predeterminados con datos sintéticos. Los parámetros solo seleccionan ejemplos de validación. La identidad y los permisos reales se resolverán en el servidor cuando exista esa integración.

## Datos entregados a la página

| Perfil | Datos |
| --- | --- |
| Trabajadora | Fecha, cita destacada y agenda propias, métricas propias por período. |
| Superadmin | Fecha, agenda del equipo, métricas del salón y detalle por integrante y período. |
| Ambos | Fecha, cita destacada y agenda propias, agenda del resto del equipo y métricas del salón y de cada integrante, incluida la cuenta que atiende. |

Al abrir, el resumen usa «Hoy» y muestra el ámbito correspondiente al perfil. Una cuenta de superadmin puede pasar del total del salón al detalle individual y volver al total. Al cambiar período se conserva el ámbito elegido. Al cambiar el ámbito se conserva el período. La cita que se abre con **Ver detalle** es la que aparece en el bloque en ese momento.
