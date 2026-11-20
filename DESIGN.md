# Diseño de NailFlow

El dashboard usa una identidad neutra y cálida para adaptarse a salones de uñas, peluquerías y otros negocios de belleza. La jerarquía de la pantalla depende del rol. El orden de la agenda y las métricas está definido en la [spec de la vista inicial](specs/001-dashboard-ux/spec.md).

## Nombre visible

**Nara Nails Studio** es la marca del salón. Usa el nombre completo en el login, el registro, la navegación y los títulos de pestaña. **NailFlow** es el nombre interno del proyecto.

## Paleta del dashboard

| Uso | Claro | Oscuro |
| --- | --- | --- |
| Fondo | Marfil suave `#FAF9F6` | Zinc profundo `#09090B` |
| Tarjetas y formularios | Blanco `#FFFFFF` | Zinc oscuro `#18181B` |
| Acción principal y elementos seleccionados | Índigo apagado `#46577A` | Índigo suave `#A5B4FC` |
| Texto principal | Gris tinta `#24313B` | Blanco suave `#FAFAFA` |
| Texto secundario | Gris medio `#55636E` | Zinc claro `#A1A1AA` |
| Bordes | Gris cálido `#E5E2DC` | Zinc medio `#27272A` |

Usa texto zinc oscuro `#18181B` sobre el botón índigo del modo oscuro. Reserva el índigo para acciones principales y elementos seleccionados. Los estados de cita llevan texto, como «Confirmada» o «En curso», con el color como apoyo.

El dashboard empieza en modo claro y recuerda la elección del interruptor de sol y luna. La tabla recoge los valores acordados para la próxima implementación del dashboard.

## Tipografía del dashboard

Usa **Inter** en toda la interfaz. Aplica el peso más ligero al título principal y aumenta el peso en los datos que el equipo busca al recorrer la pantalla.

| Elemento | Tamaño | Peso |
| --- | --- | --- |
| Título principal, como «Mi jornada» | 32 px | 300 |
| Títulos de sección, como «Próximas citas» | 18 px | 600 |
| Hora y nombre en la agenda | 14–16 px | 600 |
| Servicio | 14–16 px | 400 |
| Estado | 14–16 px | 500 |
| Cifras de métricas | 28–32 px | 600, con cifras tabulares |

## Espaciado de la agenda

- **Escritorio.** Usa 14 px de espacio arriba y abajo en cada fila y una línea fina entre citas. Alinea hora, clienta, servicio y estado en columnas con encabezados.
- **Móvil.** Usa el mismo espacio vertical. Coloca hora, clienta y estado en la primera línea y el servicio debajo. Permite que los nombres largos pasen a otra línea dentro del ancho disponible.

## Acceso y registro

Usa la paleta boutique definida en [app/app.css](app/app.css). El fondo es marfil `#F6F2EA`, las superficies son arena `#EBE3D5` y los bordes usan `#DFD5C5`. Usa marrón `#3A281E` para texto principal y tierra `#6E5A4F` para texto secundario. Reserva el cobre `#C89B7B` para acentos y acciones secundarias al pasar el cursor.

El botón principal usa bronce `#A67554` con texto marfil `#F6F2EA` de 20 px en negrita. Al pasar el cursor, el fondo cambia a `#8C5E40`. Usa Inter y espaciado amplio entre letras en los títulos de acceso y registro.

## Revisión visual

Comprueba la interfaz en móvil y escritorio con ambos temas del dashboard. Verifica foco visible, nombres accesibles para controles de solo icono y movimiento reducido. Comprueba un contraste de al menos 4,5:1 para texto normal y 3:1 para texto grande. [WCAG 2.2, contraste mínimo](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)

Consulta las instrucciones de implementación en [app/AGENTS.md](app/AGENTS.md).
