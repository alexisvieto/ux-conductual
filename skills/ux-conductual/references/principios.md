# Principios de diseño conductual

Cada principio trae: **qué es**, **por qué funciona** (la psicología), **cómo
aplicarlo** (patrones agnósticos de stack), **la trampa** y **la regla**. Los
números marcados como *heurística* son puntos de partida razonables, no leyes:
valídalos con datos (ver [Cómo validar](#cómo-validar)). Las fuentes están en
[fuentes.md](fuentes.md).

**Índice**
- [A. Percepción y mecánica](#a-percepción-y-mecánica): Hick, Fitts, memoria de
  trabajo, Jakob, Gestalt, Von Restorff, posición serial
- [B. Carga cognitiva](#b-carga-cognitiva): reconocer, defaults, progressive
  disclosure, Tesler
- [C. Motivación](#c-motivación): Fogg, tareas abiertas, progreso
- [D. Confianza y error](#d-confianza-y-error): tiempos de respuesta, feedback,
  prevención, reversibilidad, framing, peak-end, estética
- [Cuando dos principios chocan](#cuando-dos-principios-chocan)
- [Cómo validar](#cómo-validar)

---

## A. Percepción y mecánica

### 1. Ley de Hick — cada opción cuesta tiempo

**Qué es.** El tiempo para decidir crece con el número de opciones igual de
probables que se presentan a la vez (crece de forma logarítmica, no lineal).

**Por qué funciona.** Cada alternativa compite por la misma atención limitada.
Ojo con el matiz: el efecto es fuerte cuando las opciones son desconocidas y se
comparan entre sí; se debilita cuando el usuario ya sabe lo que busca y puede
escanear o buscar. La "sobrecarga de opciones" de los estudios de mermeladas
tampoco es universal: los metaanálisis encuentran efectos muy variables.

**Cómo aplicarlo.**
- Una sola acción primaria por contexto; lo demás es secundario o navegación.
- Muestra las acciones según el estado del objeto, no todas siempre.
- Divide decisiones complejas en pasos (un wizard bien hecho reduce opciones por
  pantalla).
- Si la lista es larga pero el usuario sabe qué quiere (países, clientes), no la
  recortes: dale búsqueda o autocompletar.

**La trampa.** "Ya que estamos, agrego este botón." Cada opción nueva ralentiza
las demás. Y la trampa contraria: esconder opciones que el usuario necesita para
"limpiar" la pantalla.

**Regla.** Un botón primario visible por contexto. Si necesitas dos, la pantalla
hace dos cosas: sepárala.

### 2. Ley de Fitts — grande y cerca se alcanza más rápido

**Qué es.** El tiempo para alcanzar un objetivo depende de su distancia y su
tamaño: más grande y más cerca, más rápido y con menos errores.

**Por qué funciona.** Es motriz. En móvil, la mayoría sostiene el teléfono con
una mano o lo acuna y usa el pulgar; el centro y la parte baja de la pantalla son
los más cómodos y las esquinas superiores las más difíciles. En desktop, los
bordes y esquinas son "infinitos": el cursor se detiene ahí solo.

**Cómo aplicarlo.**
- Acción principal grande y en la zona cómoda: barra inferior o botón fijo en
  móvil; visible sin scroll en desktop.
- Tamaños táctiles: WCAG 2.2 pide 24×24 px CSS como mínimo (2.5.8, AA) y 44×44
  para AAA; Apple recomienda 44 pt y Material 48 dp. En móvil apunta a 44–48.
- Separa lo destructivo de lo frecuente para evitar toques accidentales.
- Agranda el área clickeable más allá del dibujo (padding, toda la fila
  clickeable).

**La trampa.** Reusar tamaños de desktop en móvil. Un icono cómodo con mouse es
frustrante con el pulgar.

**Regla.** La acción más frecuente es el objetivo más grande y más alcanzable de
la pantalla.

### 3. Memoria de trabajo — de a bocados

**Qué es.** La memoria de trabajo retiene pocos elementos a la vez. El famoso
"7 ± 2" de Miller (1956) hablaba de cuánto podemos repetir de memoria; la
estimación actual es de **unos 4 bloques** (Cowan, 2001). Agrupar convierte
muchos elementos en pocos bloques.

**Aclaración importante.** Esto **no** significa "máximo 7 elementos en
pantalla". Lo que se ve no hay que recordarlo. Aplica cuando el usuario debe
**retener** algo mientras hace otra cosa: un código entre pantallas, opciones de
un menú de voz, datos de un paso anterior.

**Cómo aplicarlo.**
- Parte formularios largos en secciones temáticas con un título que explique el
  bloque.
- Agrupa números largos y códigos (`4512 8890 1123`, no `451288901123`).
- No obligues a recordar entre pantallas: muestra el dato de nuevo donde se
  necesita.

**La trampa.** Usar "7" como límite mágico para menús o tarjetas. El criterio
real es si el usuario tiene que recordar, y si los elementos forman grupos con
sentido.

**Regla.** Agrupa por tema; nunca hagas que el usuario memorice algo que la
interfaz puede mostrarle.

### 4. Ley de Jakob — usa lo que ya conocen

**Qué es.** Los usuarios pasan la mayor parte del tiempo en otras apps y esperan
que la tuya funcione igual.

**Por qué funciona.** El conocimiento previo se transfiere. Un patrón familiar se
usa sin aprender; uno nuevo obliga a construir un modelo mental desde cero.

**Cómo aplicarlo.**
- Patrones estándar de la plataforma: pestañas inferiores en móvil, buscador
  arriba, carrito arriba a la derecha, swipe para acciones en listas.
- Convenciones del dominio: si el usuario vive en un ERP, su banca o una
  herramienta concreta, respeta esa semántica y vocabulario.
- Iconos con significado establecido (lupa = buscar, engranaje = ajustes) y con
  etiqueta cuando el significado no es universal.

**La trampa.** Inventar una interacción "más elegante" que rompe el hábito.
Novedad no es mejora si cuesta reaprender.

**Regla.** Antes de inventar, pregunta dónde vive ya este usuario y cómo lo
resuelve allá.

### 5. Gestalt — la vista agrupa sola

**Qué es.** El cerebro organiza lo que ve con reglas automáticas: proximidad,
similitud, región común, continuidad y figura-fondo.

**Por qué funciona.** Ocurre antes de pensar. Bien usado, la estructura se
entiende sin leer.

**Cómo aplicarlo.**
- **Proximidad**: lo que va junto, junto; la etiqueta pegada a su campo.
- **Región común**: encierra grupos en tarjetas; pon el mensaje dentro del
  bloque que lo causa.
- **Similitud**: mismo significado, mismo tratamiento visual.
- **Contraste de espaciado**: poco espacio dentro del grupo, mucho entre grupos.

**La trampa.** Espaciado uniforme en todo: si todo está igual de separado, nada
se agrupa.

**Regla.** El espacio entre grupos siempre es mayor que dentro del grupo.

### 6. Efecto Von Restorff — lo distinto se recuerda

**Qué es.** Entre elementos parecidos, el que difiere se nota y se recuerda más.

**Por qué funciona.** La atención se dispara con el contraste.

**Cómo aplicarlo.**
- La acción primaria es la **única** con el tratamiento más fuerte (relleno,
  color de acción).
- Destaca el plan recomendado o el dato crítico, uno solo.
- No dependas solo del color: suma forma, peso, icono o texto (daltonismo,
  pantallas al sol).

**La trampa.** Destacar todo. Si cinco cosas compiten por ser distintas, ninguna
lo es.

**Regla.** Un solo elemento destacado por contexto, y que sea el que importa.

### 7. Posición serial — lo primero y lo último pesan más

**Qué es.** En una secuencia recordamos mejor los primeros elementos (primacía)
y los últimos (recencia).

**Cómo aplicarlo.**
- En navegación, pon los destinos clave al inicio y al final.
- En listas de beneficios u opciones, lo más importante primero.
- En onboarding, el primer y el último paso son los que se recuerdan.

**La trampa.** Enterrar lo importante en el medio de una lista larga.

**Regla.** Lo crítico, al principio o al final; nunca escondido en el medio.

---

## B. Carga cognitiva

### 8. Reconocer en vez de recordar

**Qué es.** Reconocer una opción es mucho más fácil que recuperarla de memoria y
teclearla.

**Por qué funciona.** Reconocer usa pistas externas; recordar es esfuerzo puro y
fuente de errores (dedazos, formatos inconsistentes).

**Cómo aplicarlo.**
- Select, combobox o autocompletar para valores de un conjunto conocido.
- Información útil dentro de la opción (saldo, estado) para no ir a otra
  pantalla.
- Recientes, favoritos y sugerencias basadas en el historial.
- Login sin pruebas de memoria: permite pegar contraseñas y usar el gestor
  (WCAG 3.3.8).

**La trampa.** Texto libre para algo con valores conocidos: trae inconsistencia
que después rompe reportes y búsquedas.

**Regla.** Si el valor pertenece a un conjunto conocido, se elige, no se teclea.

### 9. Defaults inteligentes y menos fricción

**Qué es.** Cada campo, tap y decisión extra pierde usuarios. Un buen default
hace que "no hacer nada" ya sea lo correcto en el caso común.

**Por qué funciona.** Tendemos a quedarnos con lo que viene puesto (sesgo de
statu quo). El efecto es tan fuerte que cambia tasas de donación de órganos
entre países: un default es una decisión que tomas por el usuario, para bien o
para mal.

**Cómo aplicarlo.**
- Pre-llena lo que el sistema sabe: fecha de hoy, usuario actual, última
  elección, país por la dirección.
- Calcula en vez de pedir (totales, impuestos).
- No vuelvas a pedir lo ya ingresado en el mismo proceso (WCAG 3.3.7).
- Teclado e input correctos (`type="email"`, `inputmode="numeric"`,
  `autocomplete`).

**La trampa.** Defaults peligrosos. El default debe ser el caso común **y
seguro**: nunca uno que, aceptado sin mirar, cause daño o cobre de más (ver
[etica.md](etica.md)).

**Regla.** Para cada campo: ¿el sistema ya lo sabe o puede adivinarlo con
seguridad? Si sí, ponlo de default y deja editarlo.

### 10. Progressive disclosure — lo esencial primero

**Qué es.** Mostrar de entrada lo que la mayoría necesita y revelar lo avanzado
bajo demanda.

**Por qué funciona.** La complejidad visible asusta y ralentiza aunque no se use.

**Cómo aplicarlo.**
- Formulario mínimo con "opciones avanzadas" colapsadas.
- Acciones que aparecen según el estado del objeto.
- Ayuda contextual detrás de un icono, disponible pero fuera del camino.

**La trampa.** Esconder algo frecuente detrás de "Ver más". Esto es para lo
infrecuente.

**Regla (heurística).** Lo que se usa en una de cada cinco visitas o más, va a
la vista. Confírmalo con analítica si la tienes.

### 11. Ley de Tesler — la complejidad se conserva

**Qué es.** Toda tarea tiene una complejidad que no se puede eliminar, solo
mover: la asume el sistema o la asume el usuario.

**Cómo aplicarlo.**
- Que el sistema absorba formatos (acepta `+507 6000-0000`, `60000000` y
  `6000 0000`), zonas horarias, cálculos y validaciones.
- Detecta en vez de preguntar (tipo de tarjeta por sus dígitos, ciudad por
  código postal).

**La trampa.** "Simplificar" quitando opciones que el usuario necesita: la
complejidad no desaparece, se va a un correo a soporte.

**Regla.** Ante cada dificultad, pregunta quién la debería cargar. Casi siempre,
el sistema.

---

## C. Motivación

### 12. Modelo de Fogg — B = MAP

**Qué es.** Una conducta ocurre cuando coinciden **M**otivación, **A**bilidad
(facilidad) y un **P**rompt (disparador) en el mismo instante. Fogg llamaba
"trigger" al prompt en versiones anteriores del modelo.

**Por qué funciona.** No basta querer ni poder: hace falta un empujón en el
momento correcto. Subir la facilidad suele rendir más que subir la motivación,
porque la motivación sube y baja.

**Cómo aplicarlo.**
- **Habilidad**: todo lo de la parte B (defaults, reconocer, menos pasos).
- **Prompt**: notificaciones o estados "necesita tu atención" **cuando la acción
  tiene sentido**, que llevan **directo** a hacerla (el push abre la pantalla
  exacta, no la home).
- **Motivación**: progreso visible, sentido de logro, beneficio claro.

**La trampa.** Disparar sin facilitar: una notificación que lleva a un flujo de
seis pasos muere.

**Regla.** Para cada acción que quieras provocar: ¿es fácil? ¿Hay un prompt en
el momento justo que lleve directo a hacerla?

### 13. Tareas abiertas (efecto Ovsiankina)

**Qué es.** Tendemos a **retomar** las tareas interrumpidas o inconclusas.

**Nota sobre la evidencia.** Durante décadas se citó el efecto Zeigarnik
("recordamos mejor lo inconcluso"). Las revisiones recientes encuentran que esa
ventaja de memoria no se replica de forma consistente; lo que sí se sostiene es
la tendencia a retomar lo que quedó a medias, descrita por Ovsiankina. Para
diseño, la consecuencia práctica es la misma: un pendiente visible invita a
cerrarlo.

**Cómo aplicarlo.**
- Sección "pendientes" o "necesita tu atención" arriba, por urgencia real.
- Contadores que **bajan al cerrar la tarea, no al mirarla**.
- "Continuar donde lo dejaste" con el borrador guardado.

**La trampa (ética).** Fabricar pendientes o badges inflados para crear
ansiedad. Si el pendiente no es real y accionable, se vuelve ruido.

**Regla.** Muestra pendientes reales, ordenados por urgencia real, que bajen
solo al resolverlos.

### 14. Progreso dotado y gradiente de meta

**Qué es.** Completamos más una meta cuando percibimos que ya avanzamos
(progreso dotado), y aceleramos a medida que nos acercamos al final (gradiente
de meta).

**Cómo aplicarlo.**
- Barras de progreso fieles: pasos completados frente a totales.
- Checklists de configuración con lo ya hecho marcado (crear la cuenta cuenta
  como paso, si de verdad lo es).
- Hacer visible lo poco que falta ("te falta 1 paso").

**La trampa.** Progreso falso, que retrocede o que nunca llega al 100 %: mata la
confianza.

**Regla.** Toda meta con pasos se muestra como progreso visible y verídico.

---

## D. Confianza y error

### 15. Tiempos de respuesta

**Qué es.** La percepción de la espera tiene umbrales estables desde los años 60:

| Tiempo | Percepción | Qué mostrar |
|---|---|---|
| ≤ 0.1 s | Instantáneo, causa-efecto directo | Nada extra; el resultado |
| ~0.1–1 s | Se nota, pero no se pierde el hilo | Cambio de estado del control |
| ~1–10 s | Se pierde la sensación de fluidez | Indicador de carga o skeleton |
| > 10 s | Se pierde la atención | Progreso con estimación y opción de cancelar o seguir en segundo plano |

El umbral de Doherty (~400 ms) marca cuándo el sistema deja de "seguir el ritmo"
de quien trabaja con él.

**Cómo aplicarlo.**
- Responde al toque de inmediato (estado presionado, `:active`) aunque el
  trabajo tarde.
- Optimistic UI en acciones reversibles y casi siempre exitosas (marcar como
  leído, me gusta), con reversión si falla.
- Skeletons con la forma del contenido para cargas de 1 a 10 s.
- Procesos largos: progreso real, estimación y la opción de avisar al terminar.

**La trampa.** Un spinner sin fin para todo; o esperas artificiales (debounces,
animaciones largas) en el camino del input.

**Regla.** Bajo 0.1 s, no mostrar nada; sobre 1 s, mostrar que trabaja; sobre
10 s, mostrar cuánto falta.

### 16. Feedback inmediato — nada pasa en silencio

**Qué es.** Toda acción produce una respuesta perceptible.

**Por qué funciona.** Sin feedback, el cerebro asume que falló y **repite**
(doble envío) o se angustia ("¿se guardó?").

**Cómo aplicarlo.**
- Estado "en proceso" con verbo ("Guardando…") y el control deshabilitado
  mientras.
- Confirmación de éxito visible (toast, cambio de estado, check).
- Error visible y accesible (`role="alert"`, `aria-live`), junto al campo que lo
  causa.

**La trampa.** Acciones mudas, o feedback que tapa el contenido o desaparece
antes de poder leerlo.

**Regla.** Todo lo que dispara trabajo: (1) muestra que está en proceso, (2) se
deshabilita, (3) confirma el resultado. Siempre los 4 estados: cargando, vacío,
con datos y error.

### 17. Prevención de error > mensaje de error

**Qué es.** Mejor hacer el error imposible o improbable que reportarlo después
(poka-yoke).

**Cómo aplicarlo.**
- Restringe en vez de permitir y regañar: rangos, máscaras, opciones válidas.
- Valida en vivo, pero **después** de que el usuario deja el campo, no mientras
  escribe el primer carácter.
- Avisa la consecuencia antes de actuar ("esto enviará la factura al cliente").
- Si bloqueas el envío, di qué falta.
- Mensaje de error, último recurso, con tres partes: **qué pasó**, **por qué**
  (si ayuda) y **qué hacer**. "El correo necesita una @" en vez de "Entrada
  inválida".

**La trampa.** Validar solo al final con un error genérico; regañar en rojo
mientras el usuario todavía escribe; bloquear sin explicar.

**Regla.** Primero, imposible; si no, aviso en vivo con su consecuencia; el
mensaje de error siempre dice qué pasó y cómo seguir.

### 18. Reversibilidad — deshacer da valentía

**Qué es.** Poder deshacer reduce el miedo a actuar y la necesidad de
confirmaciones pesadas.

**Cómo aplicarlo.**
- "Deshacer" en un toast tras acciones comunes, en vez de "¿Seguro?" antes.
- Borradores autoguardados; papelera o archivar en vez de borrar definitivo.
- Estados intermedios (borrador, pendiente) con marcha atrás.

**La trampa.** Confirmar todo: el usuario aprende a decir que sí sin leer, y la
confirmación deja de proteger cuando importa.

**Regla.** Si es reversible, hazlo fluido y ofrece deshacer. Si es irreversible y
costoso, confirmación con contexto y botón que nombra la acción.

### 19. Framing y aversión a la pérdida

**Qué es.** Cómo encuadras un dato cambia la decisión aunque el número sea el
mismo. Las pérdidas suelen pesar más que las ganancias equivalentes, aunque la
magnitud de ese efecto (el clásico "dos veces más") está en discusión y depende
del contexto.

**Cómo aplicarlo.**
- Para cupos y saldos, encuadra en lo disponible: "te quedan 3" se entiende
  mejor que "usaste 7 de 10".
- Avisa al acercarse a un límite, antes de chocar con él.

**La trampa (ética).** Usarlo para presionar ("¡pierdes tu descuento en 5
minutos!" falso). Es para informar y cuidar.

**Regla.** Encuadra límites en lo disponible y avisa a tiempo; nunca inventes una
pérdida.

### 20. Peak-end — el final es lo que se recuerda

**Qué es.** El recuerdo de una experiencia se forma sobre todo por su momento
más intenso y por cómo terminó, no por el promedio.

**Cómo aplicarlo.**
- Diseña el último paso con cuidado: confirma el resultado, muestra el estado
  final y ofrece el siguiente paso obvio.
- Cuida los picos negativos (un error en el pago pesa más que diez pasos
  fluidos).

**La trampa.** Flujos que terminan en seco: un redirect sin confirmación o un
"OK" sin contexto.

**Regla.** Cada flujo termina con una confirmación clara y un siguiente paso.

### 21. Estética-usabilidad

**Qué es.** Las interfaces percibidas como estéticas se juzgan más fáciles de
usar y se les perdonan más los fallos menores.

**Cómo aplicarlo.** Respeta tokens, escala de espaciado y tipografía del
proyecto; consistencia y contraste antes que adornos.

**La trampa.** Confundir bonito con recargado, o usar la estética para tapar
problemas reales: el halo se rompe al primer error serio.

**Regla.** Orden, contraste y consistencia antes que decoración.

---

## Cuando dos principios chocan

| Conflicto | Cómo decidir |
|---|---|
| **Hick** (menos opciones) vs. **descubrir funciones** | Recorta lo infrecuente a un menú, pero deja una ruta visible ("Más acciones"). Lo que se usa seguido no se esconde. |
| **Progressive disclosure** vs. **reconocer, no recordar** | Si el usuario necesita saber que la opción existe para buscarla, déjala visible aunque sea secundaria. Esconde configuración, no capacidades. |
| **Defaults** vs. **ética** | El default es lo que elegiría el usuario informado, no lo que más le conviene al negocio. Si dudas, sin marcar. |
| **Feedback** vs. **ruido** | Confirma lo que el usuario no puede ver por sí mismo. Si el cambio ya es visible en pantalla, no hace falta toast. |
| **Prevención** (confirmar) vs. **fluidez** | Reversible: actúa y ofrece deshacer. Irreversible y costoso: confirma con contexto. |
| **Jakob** (lo conocido) vs. **innovar** | Innova en el valor, no en los controles. Si un patrón nuevo es claramente mejor, pruébalo con usuarios antes de imponerlo. |
| **Fitts** (botón grande y fijo) vs. **contenido** | En pantallas de lectura, la acción puede ir al final; en pantallas de tarea, fija. |
| **Densidad** (expertos) vs. **simplicidad** (novatos) | Optimiza para quien más usa la pantalla. Si conviven, atajos de teclado y vistas densas opcionales para expertos. |

## Cómo validar

Los principios son hipótesis bien fundadas, no garantías. Para saber si un cambio
funcionó, mide antes y después:

- **Tasa de éxito**: ¿cuántos completan la tarea?
- **Tiempo en la tarea** y **errores** por tarea.
- **Abandono por paso** en el embudo (dónde se van).
- **Tickets de soporte** sobre esa pantalla.
- **Pruebas con 5 usuarios** pensando en voz alta: encuentran la mayoría de los
  problemas graves con muy poco costo.
- **A/B test** cuando hay tráfico suficiente y una métrica clara.

Si no hay datos, dilo en la auditoría y propone qué medir.
