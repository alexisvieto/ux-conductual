# Playbook por tipo de pantalla

Para cada arquetipo: los principios de mayor palanca, los patrones concretos y
lo que hay que evitar. Adáptalos a los componentes y tokens del proyecto.

**Índice:** [Formulario](#formulario) · [Lista, bandeja o tabla](#lista-bandeja-o-tabla) ·
[Dashboard](#dashboard) · [Detalle de un objeto](#detalle-de-un-objeto) ·
[Búsqueda](#búsqueda) · [Checkout y precios](#checkout-y-precios) ·
[Pedir permisos](#pedir-permisos) · [Acciones destructivas](#acciones-destructivas) ·
[Notificaciones](#notificaciones) · [Onboarding](#onboarding) ·
[Estados vacíos](#estados-vacíos) · [Login](#login) ·
[Interfaces de IA](#interfaces-de-ia) · [Microcopy](#microcopy)

---

## Formulario

**Principios.** Fitts, Hick, reconocer, defaults, prevención de error, feedback,
memoria de trabajo, Tesler.

**Patrones.**
- Una acción de envío, en zona cómoda (fija abajo en móvil); si hay total o
  resumen, junto al botón.
- Etiqueta visible arriba de cada campo; el placeholder es un ejemplo real
  (`ej. 6000-0000`), nunca la etiqueta.
- Campos en secciones temáticas con título. Marca los opcionales ("opcional") en
  vez de llenar de asteriscos los obligatorios, si la mayoría son obligatorios.
- Selección en vez de texto libre para valores conocidos; defaults pre-llenados;
  cálculos automáticos.
- `type`, `inputmode` y `autocomplete` correctos para el teclado y el autollenado.
- Acepta formatos flexibles (Tesler): espacios, guiones y prefijos en teléfonos y
  tarjetas.
- Validación al salir del campo; avisos de consecuencia antes de enviar.
- Si bloqueas el envío, di qué falta; mejor aún, deja enviar y lleva el foco al
  primer error con un resumen arriba.
- Estado "Enviando…" y confirmación clara al terminar (peak-end).

**Evita.** Total tecleable; texto libre para catálogos; placeholder como
etiqueta; validar mientras se escribe el primer carácter; borrar lo escrito
cuando hay un error.

## Lista, bandeja o tabla

**Principios.** Hick (filtros), tareas abiertas, Jakob, Gestalt, posición serial.

**Patrones.**
- Lo accionable o urgente primero; orden por prioridad real.
- Pocos filtros rápidos (Todas, Mías, Pendientes) y búsqueda para el resto.
- Fila escaneable: dato clave destacado, secundarios en color atenuado.
- Responsable y estado visibles en cada fila.
- Móvil: tarjetas; desktop: tabla con encabezado fijo y columnas alineadas
  (números a la derecha, con cifras tabulares).
- Acciones por fila mínimas; el resto en un menú. Acciones masivas al
  seleccionar varias.
- Badges que bajan al resolver, no al mirar.

**Evita.** Muros de columnas iguales sin jerarquía; contadores que mienten;
paginar cuando el usuario necesita comparar.

## Dashboard

**Principios.** Tareas abiertas, jerarquía de atención, progreso, framing.

**Patrones.**
- "Necesita tu atención" arriba, con lo urgente en color de estado y clic directo
  a la acción.
- Métricas como progreso cuando hay un objetivo o límite, no solo números.
- Comparación con un referente (periodo anterior, meta) para que el número
  signifique algo.
- Contenido por rol: no el mismo panel para todos.
- Un ancla de contexto visible (periodo, alcance).

**Evita.** Un dashboard bonito sin "¿qué hago ahora?"; gráficos que no responden
ninguna pregunta.

## Detalle de un objeto

**Principios.** Progressive disclosure, prevención, reversibilidad, progreso,
feedback.

**Patrones.**
- Acciones según el estado del objeto, no todas siempre.
- El ciclo de vida como progreso visible (borrador → enviado → pagado).
- Historial o trazabilidad a la vista si importa (quién cambió qué y cuándo).
- Edición en el lugar para cambios pequeños.

**Evita.** Mostrar todas las acciones siempre; confirmaciones sin contexto.

## Búsqueda

**Principios.** Reconocer, Tesler, feedback, estados vacíos.

**Patrones.**
- Campo visible arriba (Jakob), con atajo de teclado en desktop (`/` o `Ctrl+K`).
- Sugerencias y recientes al enfocar; autocompletar mientras se escribe.
- Tolerancia a errores: acentos, mayúsculas, plurales y dedazos.
- Resultados con el término resaltado; filtros después de buscar, no antes.
- Sin resultados: di qué se buscó, sugiere una corrección y ofrece limpiar
  filtros.

**Evita.** Búsqueda exacta que falla por una tilde; "0 resultados" sin salida.

## Checkout y precios

**Principios.** Fricción mínima, prevención, framing honesto, peak-end, ética.

**Patrones.**
- Compra como invitado; crear cuenta después, si quiere.
- Pasos visibles con progreso; resumen del pedido siempre a la vista.
- **Precio total desde el principio**: impuestos, envío y cargos incluidos o
  anunciados antes del último paso.
- Autollenado de dirección y tarjeta; detección del tipo de tarjeta.
- En planes: comparación clara, un plan recomendado destacado (Von Restorff) y
  precio anual frente a mensual sin trucos.
- Confirmación final con número de pedido, qué pasa ahora y cuándo llega.

**Evita.** Cargos que aparecen al final (es un dark pattern); seguros o
add-ons premarcados; registro obligatorio antes de pagar.

## Pedir permisos

**Principios.** Fogg (momento justo), confianza, Jakob.

**Patrones.**
- Pide el permiso **en contexto**, cuando el usuario intenta usar la función que
  lo necesita (cámara al tocar "escanear"), no todos al abrir la app.
- Antes del aviso del sistema, una pantalla propia que explique qué gana el
  usuario. Si dice que no, no muestres el aviso del sistema (se puede pedir una
  sola vez).
- Si lo niega, la función degrada con elegancia y explica cómo activarlo después.

**Evita.** Bombardear con permisos al inicio; bloquear toda la app por un
permiso que solo usa una función.

## Acciones destructivas

**Principios.** Reversibilidad, prevención, Fitts (distancia), feedback.

**Patrones.**
- Preferir archivar o papelera con deshacer.
- Si es irreversible, confirmación con contexto: qué se borra, cuánto y qué
  efecto tiene ("Se eliminarán 3 facturas y sus pagos. No se puede deshacer.").
- El botón de confirmar nombra la acción ("Eliminar 3 facturas") y usa el color
  de peligro; cancelar es la opción por defecto del foco.
- Para lo muy grave, escribir el nombre del recurso para confirmar.
- Botones destructivos separados de los frecuentes.

**Evita.** "¿Seguro?" con "Aceptar/Cancelar"; destructivo junto a "Guardar".

## Notificaciones

**Principios.** Fogg (prompt), tareas abiertas, respeto por la atención.

**Patrones.**
- Dispara cuando la acción tiene sentido y lleva directo al destino exacto.
- Agrupa lo no urgente en un resumen; da control (preferencias por tipo).
- Badges que reflejan pendientes reales y bajan al resolver.
- El texto dice qué pasó y qué hacer, sin necesidad de abrir para entender.

**Evita.** Insistir para forzar conducta; badges inflados; notificaciones que
llevan a la home.

## Onboarding

**Principios.** Fogg (bajar la barrera), progreso dotado, progressive disclosure,
peak-end.

**Patrones.**
- Valor en el primer minuto: que el usuario logre algo útil antes de configurar.
- Pide lo mínimo al inicio; lo demás cuando haga falta.
- Checklist de configuración con progreso real; celebra el primer logro.
- Datos de ejemplo o plantillas para no empezar en blanco.
- Ayuda en contexto en lugar de tours largos obligatorios.

**Evita.** Tours de diez pasos; pedir todo antes de mostrar valor.

## Estados vacíos

Un estado vacío enseña, no muestra un cajón en blanco.

- **Primer uso:** explica qué va aquí y da el primer paso ("Crea tu primera
  factura"), con el botón en el propio estado vacío.
- **Todo resuelto:** enmárcalo como logro ("Todo al día"), no como error.
- **Sin resultados de un filtro o búsqueda:** distínguelo de "no hay datos" y
  ofrece limpiar filtros.
- **Error al cargar:** dilo y ofrece reintentar. Nunca un vacío que en realidad
  es un fallo.

**Evita.** El vacío mudo; un vacío que esconde un error de carga.

## Login

**Principios.** Jakob, reconocer (WCAG 3.3.8), feedback, prevención.

**Patrones.**
- Sobrio y rápido; foco automático en el primer campo.
- `autocomplete="username"` y `"current-password"`; permite pegar; mostrar u
  ocultar la contraseña.
- Passkeys, enlace mágico o inicio con proveedor cuando existan.
- "Verificando…" al enviar; errores útiles sin revelar si la cuenta existe.
- Recuperación de contraseña visible.

**Evita.** Bloquear el pegado; captchas en el primer intento; errores
genéricos.

## Interfaces de IA

Las interfaces con modelos de lenguaje y agentes traen problemas nuevos:
respuestas lentas, resultados variables y acciones con consecuencias.

**Principios.** Tiempos de respuesta, feedback, reversibilidad, prevención,
confianza.

**Patrones.**
- **Streaming**: muestra la respuesta mientras se genera; el primer token llega
  en menos de 1 s, aunque la respuesta completa tarde.
- **Estado del trabajo**: si el agente usa herramientas, muestra qué está
  haciendo ("Buscando en tus facturas…") y permite detenerlo.
- **Incertidumbre visible**: cita fuentes, marca lo que no está verificado y
  facilita comprobarlo. Nunca presentes una suposición con el mismo tono que un
  dato.
- **Resultados editables**: el usuario corrige o regenera sin empezar de cero.
- **Confirmar antes de actuar**: si el agente va a enviar, pagar, borrar o
  publicar, muestra exactamente qué hará y pide confirmación. Lo reversible puede
  ir directo con deshacer.
- **Sugerencias de inicio**: ejemplos de lo que puede hacer, para vencer la hoja
  en blanco (reconocer, no recordar).
- **Límites honestos**: di lo que no puede hacer en vez de inventarlo.

**Evita.** Spinners de 20 s sin nada; respuestas seguras que son inventadas;
agentes que actúan sin mostrar qué harán; perder el texto del usuario si falla
la generación.

## Microcopy

**Patrones.**
- **Botones**: verbo + objeto ("Enviar factura", "Crear cuenta"), no "Aceptar" ni
  "Enviar" a secas cuando hay ambigüedad.
- **Errores**: qué pasó + cómo seguir, en lenguaje del usuario, sin culpar
  ("No encontramos ese correo. Revisa si está bien escrito o crea una cuenta.").
- **Estados**: verbos en gerundio para el proceso ("Guardando…") y en participio
  para el resultado ("Guardado").
- **Confirmaciones**: qué se hizo y qué sigue.
- **Consistencia**: un concepto, una palabra. Si es "cliente", no alternes con
  "usuario" o "contacto".
- **Tono**: el del proyecto (tú o usted), claro antes que ingenioso.

**Evita.** Jerga técnica ("Error 500"); humor en los errores graves; mayúsculas
para gritar.
