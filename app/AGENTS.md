# Guía de diseño de NailFlow

## Dirección visual

Usa [DESIGN.md](../DESIGN.md) como referencia para las paletas, la tipografía y el espaciado. Respeta el orden de las secciones del dashboard definido para cada rol en la spec activa.

## Paleta y temas

- Aplica la paleta neutra al dashboard. Usa el índigo para identificar las acciones principales y los elementos seleccionados. Conserva el interruptor de sol y luna y la preferencia guardada en el navegador.
- Acceso y registro usan la paleta boutique con cualquier preferencia del sistema. Reutiliza las utilidades `boutique-*` definidas en [app.css](./app.css).

## Tipografía y composición

Usa Inter y la escala definida en [DESIGN.md](../DESIGN.md). Mantén alineados los márgenes entre secciones. Usa `rounded-xl` para tarjetas y `rounded-lg` para botones y campos. Escribe etiquetas y acciones breves en español.

## Accesibilidad y revisión

- Mantén el foco visible, usa controles nativos y da un nombre accesible a los botones de solo icono. Identifica los estados con texto además del color y comprueba el contraste en ambos temas.
- Usa animaciones breves como respuesta a una interacción y respeta `prefers-reduced-motion`.
- Revisa el área modificada en móvil y escritorio. Prueba la navegación con teclado y, para cambios de tema, alterna ambos modos y comprueba que la elección se conserva al recargar.
