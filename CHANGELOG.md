# Changelog

Todos los cambios relevantes de la página de herramientas se registran aquí.
El formato sigue [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/)
y las versiones usan [Versionado Semántico](https://semver.org/lang/es/).

## [2.1.0] - 2026-10-27

### Añadido
- **Nueva pestaña Mural** para preparar los números que se anotan en la pizarra de la tienda.
  - Lee el **Excel de diarización del mes** directamente en el navegador; el archivo no se sube a ningún servidor.
    Reconoce las hojas de tienda por su formato (B5 = tienda, C5 = "Diarización", E5 = "Forecast",
    E6 = meta mensual, una fila por día con la meta en E y la venta neta en F) e ignora las hojas de totales.
  - Si el Excel trae varias tiendas se elige una, y se recuerda para el mes siguiente.
  - Solo se guardan en el dispositivo las metas diarias de la tienda elegida (`localStorage`: `mural_metas`, `mural_tienda`),
    así la meta mensual se carga **una vez al mes**.
  - Cada día se escriben la venta acumulada, la venta de ayer, el NPS (acumulado, domicilio, retiro) y el OTD.
    Si el Excel ya trae la venta de ayer, las ventas se precargan.
    Los datos se guardan por fecha (`mural_datos`, últimas 2 semanas) y se limpian solos al cambiar el día.
  - Calcula meta diaria, meta de ayer, meta acumulada (día 1 hasta hoy, igual que la planilla `mural_automatica`),
    % de cumplimiento `(venta acum. − meta acum.) / meta acum.` y diferencia de ayer, en verde o rojo según el signo.
  - Avisa cuando las metas guardadas son de otro mes.
- El lector de Excel (SheetJS 0.18.5, cdnjs) se descarga solo al cargar un archivo y corre en un *worker*
  para no congelar la pantalla; lee únicamente las primeras filas de cada hoja.

### Cambiado
- Con 4 pestañas, en pantallas de hasta 420 px se achica el texto de la navegación; bajo 370 px se ocultan los iconos.

## [2.0.0] - 2026-10-27

Rediseño de la interfaz ("UX v2"), pensado sobre todo para el uso en celular.

### Añadido
- **Rótulo:** botones rápidos **Hoy / Ayer** para la fecha de rotulado, junto al selector de otra fecha.
- **Rótulo:** aviso visible ("Rotulando con …, no con hoy") cuando la fecha de rotulado no es la de hoy.
- **Rótulo:** interruptor **"Mostrar fr y FV calculados"** (antes solo se alternaba tocando la tabla o el campo FV).
- **Rótulo:** mensaje "Elige un producto para ver su rótulo" y tabla atenuada mientras no hay producto.
- **Rótulo:** resumen de reglas en pastillas (Caja / Prep / Prod) en vez de una línea de texto.
- **Rótulo:** encabezado en la vista por tipo con el nombre del tipo y la cantidad de productos.
- **Rótulo:** botón flotante **"Tipos"** para volver arriba en listas largas.
- **Rótulo:** se recuerda el último tipo de producto elegido en el dispositivo (`localStorage`, clave `ra_last_type`).
- **Descuentos:** el precio se formatea con puntos de miles mientras se escribe (12.990).
- **Descuentos:** al abrir la pestaña con el campo vacío, el cursor queda listo para escribir.
- **Fechas:** el resultado personalizado indica "en N días", "hace N días" u "hoy".
- **Fechas:** la lista de días se actualiza sola al pasar la medianoche si la página queda abierta.
- Accesibilidad: roles `tablist`/`tab`, `aria-selected`, `aria-pressed`, `role="switch"`, etiquetas `for` y foco visible con teclado.
- `meta theme-color` con el verde de la marca para la barra del navegador en el celular.

### Cambiado
- Verde de la marca unificado a `#006341` (antes `#006D56`) mediante variables CSS (`--pj`, `--pj-700`, etc.).
- Pestañas con icono y texto en una sola fila; en celular la primera dice "Rótulo".
- Cabecera más baja para ganar espacio vertical.
- Pastillas de tipo en cuadrícula de 3 columnas en celular (antes una fila con desplazamiento horizontal).
- Formulario del rótulo en dos columnas (producto / FV) en pantallas medianas.
- Las horas de inicio y vencimiento solo se muestran en procesos medidos en **horas**; en procesos en días aparece "—".
- Descuentos: se muestra "—" en vez de "$0" mientras no hay precio y se quitó la etiqueta repetida "Precio final" de cada tarjeta.
- Fechas: "Hoy es" pasa a una pastilla en el título de la tarjeta; el día de la semana se resalta en verde.
- Los efectos `:hover` solo se aplican en dispositivos con puntero (`@media (hover: hover)`), evitando estados "pegados" al tocar en el celular.
- Impresión: ocultos los nuevos controles; la tabla se imprime sin atenuar aunque no haya producto.

### Corregido
- **Reglas de cárnicos:** "Pollo Asado" se separa de "Alitas / Chicken Poppers" con su propia regla: **8 días** cerrado y 8 días preparado (antes compartía 7 días).

## [1.0.0] - 2026-10

Versión inicial publicada: rótulo automático, calculadora de descuentos y calculadora de fechas/horas.

[2.1.0]: https://github.com/vkieferv/pj/compare/bda256a...main
[2.0.0]: https://github.com/vkieferv/pj/compare/7293431...56d61c3
[1.0.0]: https://github.com/vkieferv/pj/tree/7293431
