---
name: ux-conductual
description: >-
  Diseño conductual para cualquier interfaz: psicología del usuario aplicada a
  pantallas, formularios, flujos, estados (vacío, carga, error), notificaciones,
  microcopy, jerarquía visual e interfaces de IA, en cualquier stack y design
  system. Dos modos: DISEÑAR (construir aplicando los principios) y AUDITAR
  (tabla de hallazgos con principio, severidad, ubicación y arreglo). Traduce
  Hick, Fitts, carga cognitiva, Jakob, Gestalt, reconocer-vs-recordar, defaults,
  progressive disclosure, Fogg (B=MAP), tiempos de respuesta, prevención de
  error, reversibilidad, framing, peak-end y ética anti dark patterns a patrones
  concretos con fuentes. Úsala al diseñar, revisar o mejorar una UI: "revisa este
  formulario", "esto se siente difícil", "hazlo más intuitivo", "reducir
  fricción", "estado vacío", "onboarding", "microcopy", "UX review", "make it
  more intuitive", "review this form/screen/flow", "reduce friction", "empty
  state", "dark patterns", "usability". No la uses para estética pura (paleta,
  tipografía, animación de marca) ni para código sin interfaz.
license: CC-BY-4.0
metadata:
  author: "Alexis Vieto · Senior Software Engineer · Nexera (nexerai.io)"
  version: "2.0.0"
---

# UX Conductual

Diseñar una interfaz no es poner controles en la pantalla: es **hacer que la
acción correcta sea la más fácil, la más visible y la más difícil de
equivocar**, usando cómo funciona de verdad la atención, la memoria y la
motivación humanas. Siempre a favor del usuario, nunca en su contra.

## Principio rector

> La pantalla responde tres preguntas, en este orden y sin que el usuario tenga
> que pensar: **(1) ¿qué necesita mi atención ahora? (2) ¿cuál es la única
> acción principal? (3) ¿cómo sé que salió bien?**

Regla de oro: si el usuario tiene que *pensar* dónde tocar, qué escribir o si
algo se guardó, la pantalla todavía no está lista.

## Paso 0 — Adáptate al proyecto (siempre, antes de proponer nada)

Los principios son universales; las piezas son del proyecto.

1. **Stack y plataforma**: web (React, Vue, Svelte, Angular…), móvil nativo
   (SwiftUI, Compose), Flutter. Usa sus convenciones idiomáticas.
2. **Design system y tokens**: busca `globals.css`, `theme`, `tailwind.config`,
   tokens, librería de componentes. Usa sus colores de estado, espaciado y
   radios. **Nunca inventes una paleta ni metas colores crudos.**
3. **Componentes existentes**: reusa botones, inputs, modales y toasts antes de
   crear otros.
4. **Convenciones**: idioma y tono del copy (tú/usted), una sola familia de
   iconos (nunca emojis como icono), patrones de accesibilidad ya usados.
5. **Documento de diseño**: si hay `DESIGN.md` o guía de marca, es la fuente de
   verdad. Esta skill dice **qué** principios aplicar y **por qué**; el proyecto
   dice **con qué piezas**.

## Perfila al usuario

Antes de diseñar o auditar, responde en una línea cada una:

- **¿Quién?** Rol, experiencia, frecuencia de uso.
- **¿Dónde y cómo?** Dispositivo, una mano o dos, con prisa o con calma.
- **¿Qué quiere lograr?** La tarea real, no "usar la app".
- **¿Qué teme?** Equivocarse, perder trabajo, no saber si se guardó.

Optimiza cada pantalla para **el rol que más la usa, en el momento en que la
usa**, no para el caso raro.

## Elige el modo

### Modo DISEÑAR (pantalla, flujo o componente nuevo)

1. Paso 0 y perfil del usuario.
2. Responde las 3 preguntas del principio rector para esta pantalla.
3. Abre el arquetipo en [references/playbook.md](references/playbook.md)
   (formulario, lista, dashboard, detalle, búsqueda, checkout, permisos,
   onboarding, estados vacíos, login, acciones destructivas, interfaces de IA).
4. Elige los **3–4 principios de mayor palanca** para este contexto. Si dos
   chocan, usa la sección de conflictos de
   [references/principios.md](references/principios.md#cuando-dos-principios-chocan).
5. Construye con los tokens y componentes reales. Para patrones de código, mira
   [examples/antes-despues.md](examples/antes-despues.md).
6. Diseña los **4 estados**: cargando, vacío, con datos y error.
7. Pasa el checklist maestro y el de ética antes de entregar.

### Modo AUDITAR (revisar algo existente)

1. Paso 0 y perfil del usuario.
2. Recorre la pantalla con el checklist maestro y el de ética.
3. Entrega **siempre** esta tabla, ordenada de mayor a menor severidad:

| # | Hallazgo | Principio | Severidad | Dónde | Arreglo |
|---|---|---|---|---|---|
| 1 | El botón "Guardar" no muestra carga y permite doble envío | Feedback inmediato | 3 | `CheckoutForm.tsx:84` | Deshabilitar durante el envío y mostrar "Guardando…" |

**Severidad** (escala de Nielsen): **0** no es problema · **1** cosmético ·
**2** menor, arreglar si hay tiempo · **3** mayor, prioridad alta ·
**4** catástrofe, arreglar antes de lanzar. Un dark pattern es siempre 4.

4. Cierra con **los 3 arreglos de mayor impacto** en una línea cada uno.
5. Si puedes editar el código, ofrece aplicar los arreglos; no los apliques sin
   que te lo pidan.

Evidencia, no opinión: cada hallazgo nombra el principio y la ubicación. Si algo
depende de datos que no tienes (cuántos usuarios abandonan, qué buscan), dilo y
propón cómo medirlo (ver
[references/principios.md](references/principios.md#cómo-validar)).

## Los principios, en un vistazo

Desarrollo completo, psicología, trampas y fuentes en
[references/principios.md](references/principios.md).

**Percepción y mecánica**
- **Hick**: más opciones a la vez, decisión más lenta. Una acción primaria por
  contexto.
- **Fitts**: lo grande y cercano se alcanza más rápido. La acción frecuente es
  el objetivo más grande y alcanzable.
- **Memoria de trabajo (Miller, Cowan)**: retenemos ~4 bloques. Agrupa por tema.
- **Jakob**: el usuario espera que funcione como las apps que ya usa.
- **Gestalt**: lo que va junto se ve junto. Más espacio entre grupos que dentro.
- **Von Restorff**: lo distinto se nota. La acción primaria es la única con ese
  tratamiento.
- **Posición serial**: lo primero y lo último se recuerdan más.

**Carga cognitiva**
- **Reconocer, no recordar**: elegir de una lista, no teclear de memoria.
- **Defaults y menos fricción**: lo que el sistema sabe, no se pide.
- **Progressive disclosure**: lo esencial a la vista, lo avanzado bajo demanda.
- **Tesler**: la complejidad no desaparece; que la absorba el sistema, no el
  usuario.

**Motivación**
- **Fogg (B = MAP)**: conducta = Motivación × Habilidad × Prompt en el mismo
  instante. Facilitar rinde más que motivar.
- **Tareas abiertas (Ovsiankina)**: tendemos a retomar lo que quedó a medias.
  Haz visibles los pendientes reales.
- **Progreso dotado y gradiente de meta**: el avance visible se termina, y se
  acelera cerca del final.

**Confianza y error**
- **Tiempos de respuesta**: 0.1 s se siente instantáneo, 1 s mantiene el hilo,
  10 s es el límite de la atención.
- **Feedback inmediato**: nada pasa en silencio.
- **Prevención > mensaje de error**: haz el error imposible antes que reportarlo.
- **Reversibilidad**: deshacer da valentía; confirma solo lo irreversible.
- **Framing y aversión a la pérdida**: cómo encuadras cambia la conducta. Úsalo
  para informar, nunca para presionar.
- **Peak-end**: el final del flujo es lo que se recuerda.
- **Estética-usabilidad**: lo ordenado se percibe más usable.

## Checklist maestro

**Atención y jerarquía**
- [ ] En 2 segundos se entiende qué necesita atención y cuál es la acción
      principal.
- [ ] Un solo botón primario por contexto; el resto secundario o terciario.
- [ ] El color de estado comunica urgencia real, con los tokens del proyecto, y
      nunca es la única señal (va con texto o icono).

**Carga cognitiva**
- [ ] No se pide nada que el sistema ya sabe ni se vuelve a pedir lo ya
      ingresado (WCAG 3.3.7).
- [ ] Valores conocidos se eligen de una lista, no se teclean.
- [ ] Campos agrupados por tema; cada grupo con un título que explica el bloque.
- [ ] Cada campo tiene etiqueta visible; el placeholder es un ejemplo, nunca la
      etiqueta.

**Mecánica**
- [ ] La acción principal está en la zona cómoda (pulgar en móvil, sin scroll en
      desktop).
- [ ] Objetivos táctiles de 24×24 px como mínimo (WCAG 2.5.8) y 44–48 px en
      móvil (Apple 44 pt, Material 48 dp). Lo destructivo, lejos de lo frecuente.
- [ ] El mismo dato usa el patrón adecuado por tamaño (tabla en desktop,
      tarjetas en móvil).

**Feedback y estados**
- [ ] Toda respuesta tarda menos de 0.1 s o muestra algo: estado de carga a
      partir de ~1 s, progreso con estimación a partir de ~10 s.
- [ ] Todo botón que dispara trabajo muestra "en proceso" y se deshabilita para
      evitar el doble envío.
- [ ] El éxito se confirma; el error es visible y accesible (`role="alert"` o su
      equivalente), dice qué pasó y cómo seguir.
- [ ] Existen los 4 estados: cargando, vacío, con datos y error. El vacío enseña
      el siguiente paso.

**Prevención de error**
- [ ] El envío se bloquea si falta lo mínimo, diciendo **qué** falta.
- [ ] Las consecuencias se avisan **antes** ("esto será público").
- [ ] Lo irreversible pide confirmación con contexto (qué, cuánto, a quién) y el
      botón dice la acción ("Eliminar 3 facturas"), no "Aceptar".

**Accesibilidad y consistencia**
- [ ] Foco visible y orden de tabulación lógico; todo es operable con teclado.
- [ ] Contraste AA (4.5:1 texto, 3:1 componentes); respeta
      `prefers-reduced-motion`.
- [ ] Solo tokens y componentes del proyecto; una familia de iconos; tono de copy
      consistente.

**Cierre**
- [ ] El flujo termina con confirmación clara y un siguiente paso obvio.

## Checklist de ética

Detalle, dark patterns y marco legal en [references/etica.md](references/etica.md).

- [ ] La opción honesta y sana es la más fácil y la predeterminada.
- [ ] Ningún default sorprende ni perjudica si se acepta sin mirar.
- [ ] Toda urgencia, escasez o prueba social mostrada es **real**.
- [ ] Todo badge o contador representa una tarea real y accionable.
- [ ] Salir, cancelar o rechazar es tan fácil como entrar o aceptar.
- [ ] Podrías explicarle el diseño al usuario en voz alta **sin vergüenza**.

## Referencias

- [references/principios.md](references/principios.md): cada principio a fondo,
  conflictos entre principios y cómo validar.
- [references/playbook.md](references/playbook.md): patrones por tipo de
  pantalla.
- [references/etica.md](references/etica.md): dark patterns, anti-patrones y
  marco legal.
- [references/fuentes.md](references/fuentes.md): estudios y fuentes citados.
- [examples/antes-despues.md](examples/antes-despues.md): ejemplos de código
  antes y después.
