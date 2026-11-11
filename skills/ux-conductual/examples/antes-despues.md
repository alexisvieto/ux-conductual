# Antes y después

Patrones en HTML y React genéricos. Tradúcelos a los componentes y tokens del
proyecto: aquí `btn`, `field` y los colores son ilustrativos.

## 1. Botón que dispara trabajo (feedback + doble envío)

**Antes.** Sin estado de carga: el usuario toca dos veces y crea dos pedidos.

```tsx
<button onClick={guardar}>Guardar</button>
```

**Después.** Muestra que trabaja, se deshabilita y confirma.

```tsx
const [estado, setEstado] = useState<"idle" | "guardando" | "ok" | "error">("idle");

async function onGuardar() {
  setEstado("guardando");
  try { await guardar(); setEstado("ok"); toast("Factura guardada"); }
  catch { setEstado("error"); }
}

<button onClick={onGuardar} disabled={estado === "guardando"} aria-busy={estado === "guardando"}>
  {estado === "guardando" ? "Guardando…" : "Guardar factura"}
</button>
{estado === "error" && <p role="alert">No pudimos guardar. Revisa tu conexión y vuelve a intentarlo.</p>}
```

Principios: feedback inmediato, prevención de error, microcopy (verbo + objeto).

## 2. Campo de formulario (etiqueta, ejemplo, teclado, error útil)

**Antes.**

```html
<input placeholder="Teléfono">
<span class="error">Entrada inválida</span>
```

**Después.**

```html
<label for="tel">Teléfono</label>
<input id="tel" type="tel" inputmode="tel" autocomplete="tel"
       placeholder="ej. 6000-0000" aria-describedby="tel-error" aria-invalid="true">
<p id="tel-error" role="alert">Faltan dígitos: el teléfono tiene 8 números.</p>
```

Principios: etiqueta visible (el placeholder es ejemplo), teclado correcto,
autollenado, error que dice qué pasó y cómo seguir. Acepta `6000 0000` y
`60000000` en el servidor (Tesler).

## 3. Confirmación destructiva (contexto + botón que nombra la acción)

**Antes.**

```text
¿Seguro?            [Cancelar] [Aceptar]
```

**Después.**

```text
Eliminar 3 facturas
Se eliminarán las facturas 104, 105 y 106 y sus pagos registrados.
Esta acción no se puede deshacer.
                    [Cancelar]  [Eliminar 3 facturas]  ← color de peligro; foco inicial en Cancelar
```

Mejor todavía, si se puede: mover a la papelera y mostrar un toast
"3 facturas movidas a la papelera · Deshacer".

Principios: reversibilidad, prevención, microcopy.

## 4. Estado vacío (enseña el siguiente paso)

**Antes.**

```text
No hay datos.
```

**Después (primer uso).**

```text
Aquí verás tus facturas
Crea la primera y te avisamos cuando el cliente la abra.
[Crear factura]
```

**Después (filtro sin resultados).**

```text
Ninguna factura coincide con "vencidas · marzo"
[Limpiar filtros]
```

Principios: estados vacíos, Fogg (prompt + habilidad), reconocer.

## 5. Cupo o límite (framing honesto)

**Antes.** `Usaste 47 de 50 envíos`

**Después.** `Te quedan 3 envíos este mes · Se renuevan el 1 de diciembre`

Principios: framing, aviso antes del límite, sin presión falsa.

## 6. Agente de IA que va a actuar (confirmar antes de enviar)

**Antes.** El agente envía el correo directamente después de redactarlo.

**Después.**

```text
Voy a enviar este correo a ana@cliente.com:
  Asunto: Recordatorio de factura 104
  [vista previa del texto, editable]
[Editar]  [Enviar correo]
```

Principios: prevención, confianza, resultados editables.

## 7. Consentimiento de cookies (ética)

**Antes.** `[Aceptar todo]` destacado; "Configurar" en un enlace gris.

**Después.** `[Rechazar]` y `[Aceptar]` con el mismo peso visual, y
"Elegir qué permitir" como tercera opción clara.

Principios: ética, RGPD (rechazar tan fácil como aceptar).
