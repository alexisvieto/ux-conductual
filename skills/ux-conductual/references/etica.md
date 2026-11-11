# Ética del diseño conductual

Las mismas técnicas que hacen fácil una app pueden usarse para manipular. La
diferencia está en **a favor de quién** operan.

## La regla de oro

> Usa la psicología para que la **acción correcta y honesta** sea la más fácil.
> Nunca para que una acción que **perjudica al usuario** sea la fácil, la
> predeterminada o la difícil de evitar.

**Prueba rápida:** si tuvieras que explicarle en voz alta al usuario por qué la
pantalla está diseñada así, ¿te daría vergüenza? Si la respuesta es sí, es un
dark pattern. Quítalo.

## Dark patterns (siempre severidad 4 en una auditoría)

Taxonomía basada en Brignull (deceptive.design), Gray et al. (2018) y Mathur et
al. (2019).

| Patrón | Qué es | Ejemplo |
|---|---|---|
| **Confirmshaming** | Culpar o avergonzar por elegir la opción sana | "No, prefiero pagar de más" |
| **Defaults tramposos** | Premarcar lo que conviene al negocio y perjudica o sorprende | Seguro de envío o newsletter premarcados |
| **Roach motel (fricción asimétrica)** | Fácil entrar, difícil salir | Suscribirse en un clic, cancelar solo por teléfono |
| **Urgencia falsa** | Contadores o plazos inventados | "La oferta termina en 05:00" que se reinicia |
| **Escasez falsa** | Stock o demanda inventados | "Quedan 2" que nunca cambia |
| **Prueba social falsa** | Actividad o reseñas inventadas | "Juan de Lima acaba de comprar" generado |
| **Badges inflados** | Indicadores que no representan nada real | Punto rojo permanente para atraer clics |
| **Nagging** | Insistir para forzar una conducta | Pedir activar notificaciones en cada visita |
| **Costos ocultos (sneaking)** | Revelar cargos al final | Comisión que aparece en el último paso |
| **Preguntas capciosas** | Copy confuso o doble negación | "Desmarca para no dejar de recibir correos" |
| **Obstrucción** | Esconder o disfrazar lo que el usuario quiere | "Cancelar" en gris claro y texto pequeño |
| **Privacy zuckering** | Empujar a compartir más datos de los que quiere | "Aceptar todo" destacado, "Configurar" escondido |
| **Interferencia visual** | Disfrazar anuncios como contenido o botones falsos | Un anuncio con forma de botón "Descargar" |

## Anti-patrones de UX (errores honestos, igual de dañinos)

- **Acción muda**: sin feedback; el usuario reintenta y duplica.
- **Bloqueo sin explicación**: deshabilitar sin decir qué falta.
- **Validación tardía**: todo al final en vez de prevenir.
- **Sobrecarga de opciones**: un botón más cada vez.
- **Progreso falso o eterno**: rompe la confianza.
- **Estado vacío mudo** o vacío que esconde un error.
- **Romper Jakob**: inventar donde había un patrón conocido.
- **Colores fuera de los tokens**: rompe la consistencia.
- **Solo color para comunicar**: inaccesible para daltónicos.
- **Iconos sin etiqueta** cuyo significado no es universal.
- **Emojis como iconos**: usa una familia de iconos consistente.

## Marco legal (no es asesoría legal)

El diseño engañoso ya no es solo un problema ético; en varias jurisdicciones es
ilegal:

- **Unión Europea, Ley de Servicios Digitales (Reglamento 2022/2065), art. 25**:
  prohíbe a las plataformas en línea diseñar interfaces que engañen o manipulen,
  o que distorsionen la capacidad de decidir libremente.
- **RGPD (GDPR)**: el consentimiento debe ser libre, específico, informado e
  inequívoco; rechazar debe ser tan fácil como aceptar, y las casillas
  premarcadas no valen como consentimiento.
- **Directiva de Prácticas Comerciales Desleales (UE)**: aplica a la urgencia
  falsa, la escasez falsa y los costos ocultos.
- **Estados Unidos**: la FTC persigue el diseño engañoso bajo su facultad contra
  prácticas engañosas, y leyes estatales como la CPRA de California consideran
  inválido el consentimiento obtenido con dark patterns. Verifica el estado
  actual de las reglas federales sobre cancelación de suscripciones antes de
  citarlas.
- **Latinoamérica**: las leyes de protección al consumidor y de datos personales
  de cada país (por ejemplo, la Ley 81 de 2019 en Panamá o la LGPD en Brasil)
  exigen consentimiento informado e información veraz sobre precios.

Si el producto opera en estas jurisdicciones, un dark pattern es también un
riesgo legal. Ante la duda, consulta con un abogado.

## Checklist de ética

- [ ] La opción honesta y sana es la más fácil y la predeterminada.
- [ ] Ningún default sorprende ni perjudica si se acepta sin mirar.
- [ ] Toda urgencia, escasez y prueba social es real y verificable.
- [ ] Todo badge o contador representa una tarea real y accionable.
- [ ] Cancelar, salir o rechazar es tan fácil como entrar o aceptar.
- [ ] El precio total se conoce antes del último paso.
- [ ] El copy es claro: sin dobles negaciones ni culpa.
- [ ] Podrías explicarle el diseño al usuario sin vergüenza.

> La confianza es el activo. Un solo dark pattern y la gente deja de creerle al
> producto. El diseño honesto no es solo lo correcto: es lo que hace que el
> producto funcione a largo plazo.
