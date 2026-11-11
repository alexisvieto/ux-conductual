# Auditoría real de la demo

Le pedimos a Claude, con la skill instalada, que auditara [`antes.html`](antes.html) en **modo AUDITAR**. Esta es su respuesta, sin cambios de contenido. La pantalla corregida está en [`despues.html`](despues.html).

> Prompt: *"Audita esta pantalla de Nueva factura. Usuario: dueño de una pequeña empresa en Panamá, en el celular, entre otras tareas; quiere facturar rápido y teme enviar una factura equivocada."*

---

**Paso 0:** HTML/CSS plano, sin design system, tokens ni componentes. Los arreglos usan HTML nativo (`<label>`, `type`, `inputmode`, `<input type="date">`) y no proponen colores crudos nuevos: primero hay que definir tokens de estado (éxito, peligro, primario), porque hoy hay 4 colores sin significado. El copy mezcla tú y usted. No hay iconos.

**Usuario:** dueño de una pequeña empresa en Panamá. Usa el celular con una mano, entre otras tareas, y lo interrumpen. Quiere facturar rápido a un cliente que muchas veces ya conoce. Teme enviar una factura con datos o montos equivocados, o enviarla dos veces.

| # | Hallazgo | Principio | Severidad | Dónde | Arreglo |
|---|---|---|---|---|---|
| 1 | La casilla "Enviar copia a nuestros socios comerciales" viene marcada: comparte los datos del cliente con terceros si el usuario no la mira, y una casilla premarcada no vale como consentimiento | Ética: default tramposo / defaults | 4 | `antes.html:42` | Quitarla. Si de verdad hace falta, desmarcada, explicando qué se comparte y con quién, con etiqueta clicable |
| 2 | Para rechazar Pro hay que leer "No gracias, prefiero seguir perdiendo clientes", que culpa al usuario. Además es un `<small>` de 9 px en #bbb que ni siquiera es un botón: rechazar cuesta mucho más que aceptar | Ética: confirmshaming / salir tan fácil como entrar | 4 | `antes.html:51` | Botón neutro "Ahora no" del mismo tamaño que "Quiero Pro", con copy informativo y sin culpa |
| 3 | "Enviar" manda la factura en el acto, sin vista previa ni resumen (a quién, cuánto, cuándo vence) y sin avisar consecuencias, aunque eso es justo lo que teme el usuario | Prevención de error / avisar consecuencias antes | 3 | `antes.html:45` | Mostrar antes de enviar un resumen con contexto y un botón que diga la acción: "Enviar factura de $X a cliente@correo" |
| 4 | "Borrar" está pegado a "Guardar" y "Enviar", con el mismo tamaño y sin confirmación ni deshacer. Con objetivos pequeños y una mano, tocarlo por error es fácil y se pierde el trabajo | Reversibilidad / Fitts (lo destructivo lejos de lo frecuente) | 3 | `antes.html:46` | Sacarlo de la fila principal (menú o enlace terciario) y ofrecer "Deshacer" o confirmación con contexto |
| 5 | 4 botones del mismo peso y 4 colores distintos, ninguno primario. El color no significa nada (el naranja de PDF es el mismo del anuncio) y no se sabe cuál es la acción principal | Hick / Von Restorff / un solo primario | 3 | `antes.html:43` | Un solo primario ("Revisar y enviar"); "Guardar borrador" secundario; "PDF" terciario o dentro de la vista previa |
| 6 | El usuario escribe a mano "ITBMS" y "Total" aunque el sistema puede calcularlos con cantidad × precio. Es una fuente directa de facturas con montos equivocados | Tesler / lo que el sistema sabe no se pide / prevención | 3 | `antes.html:39` | Calcular subtotal, ITBMS (7 % por defecto, editable) y total, en solo lectura y en vivo |
| 7 | Cliente, RUC, correo y teléfono se teclean de memoria cada vez, aunque el cliente casi siempre ya existe | Reconocer, no recordar / WCAG 3.3.7 | 3 | `antes.html:31` | Selector de cliente con búsqueda que rellena RUC, correo y teléfono, más "Nuevo cliente" |
| 8 | Los placeholders hacen de etiqueta: desaparecen al escribir y, tras una interrupción, el usuario no sabe qué campo es. Tampoco dan un nombre accesible a los lectores de pantalla | Etiqueta visible / memoria de trabajo | 3 | `antes.html:31` | `<label>` visible en cada campo; el placeholder solo como ejemplo ("8-123-456") |
| 9 | "Error: entrada inválida" aparece arriba antes de que el usuario haga nada. No dice qué campo falla ni cómo corregirlo, no está junto al campo y no tiene `role="alert"` | Feedback útil / prevención > mensaje de error | 3 | `antes.html:30` | Validar al salir de cada campo, con el mensaje junto al campo ("Falta el RUC del cliente") y `role="alert"` / `aria-describedby` |
| 10 | No hay estado "Enviando…", confirmación de éxito ni protección contra el doble toque en Guardar o Enviar: riesgo de factura duplicada o de no saber si salió. Es un mock estático, pero el diseño no define esos estados | Feedback inmediato / doble envío | 3 | `antes.html:44` | Deshabilitar y mostrar "Enviando…"; al terminar, confirmar ("Factura #123 enviada a …") con el siguiente paso |
| 11 | Botones de ~28 px de alto, inputs de ~30 px y una casilla nativa sin etiqueta clicable, todo por debajo de 44–48 px para uso con una mano | Fitts / objetivos táctiles | 2 | `antes.html:17` | 44–48 px de alto como mínimo en botones e inputs; casilla dentro de un `<label>` |
| 12 | Fechas en texto libre; la fecha de emisión no trae hoy por defecto y el vencimiento no ofrece plazos habituales | Defaults / reconocer > recordar | 2 | `antes.html:35` | `type="date"` con hoy por defecto; vencimiento con opciones (contado, 15, 30 días) |
| 13 | Moneda sin valor por defecto ("Moneda" como opción) y colocada después del Total, en un orden ilógico | Defaults / orden natural de la tarea | 2 | `antes.html:41` | USD por defecto, junto al precio o el total, o en ajustes |
| 14 | 11 campos en una sola columna sin grupos ni títulos (cliente, fechas, detalle y montos mezclados) | Gestalt / memoria de trabajo (~4 bloques) | 2 | `antes.html:31` | Agrupar en "Cliente", "Detalle" y "Totales", con títulos y más espacio entre grupos que dentro de ellos |
| 15 | Correo, teléfono, cantidad y precio sin `type` ni `inputmode`: en el celular sale el teclado de texto | Jakob / menos fricción | 2 | `antes.html:33` | `type="email"`, `type="tel"`, `inputmode="decimal"` en cantidad y precio |
| 16 | El anuncio de Pro compite con la tarea dentro del formulario de facturar | Hick / atención en la tarea principal | 2 | `antes.html:50` | Sacarlo del flujo; si acaso, mostrarlo tras un envío exitoso y sin presión |
| 17 | El estado vacío "No hay datos" no dice de qué es la lista ni qué hacer | Estados vacíos enseñan el siguiente paso | 2 | `antes.html:49` | "Aún no has emitido facturas. La primera aparecerá aquí", o quitarlo de esta pantalla |
| 18 | Contraste bajo AA: "ayuda" en #999 a 11 px, la lista en #aaa, el rechazo en #bbb a 9 px y el texto de la casilla en #777 (~4.48:1, apenas bajo 4.5:1) | Contraste AA / estética-usabilidad | 2 | `antes.html:13` | Subir los textos secundarios a ≥4.5:1 y a 13 px como mínimo |
| 19 | Ancho fijo de 390 px: en teléfonos de 360 px habrá scroll horizontal | Mecánica / responsive | 2 | `antes.html:10` | `max-width: 390px; width: 100%` |

**Los 3 arreglos de mayor impacto**
1. Quitar los dos dark patterns: la casilla premarcada de "socios comerciales" (desmarcada o eliminada) y el confirmshaming de Pro (botón neutro "Ahora no").
2. Antes de enviar, mostrar un resumen (cliente, total, vencimiento) y un solo botón primario "Enviar factura de $X a …", con estado "Enviando…" y confirmación de éxito; "Borrar" sale de la fila.
3. Que el sistema haga el trabajo: selector de cliente que rellena RUC y correo, ITBMS y total calculados, fecha de hoy y USD por defecto, con etiquetas visibles y errores junto a cada campo.
