# AXIA RH — MÓDULOS 6 Y 8: VALIDACIÓN DE PAGO DE PTU Y AGUINALDO · FONACOT

Especificación para programación · Versión 1.0 · 15/11/2026
Fuente: registro de decisiones (4.7, 4.8, 4.10, 4.11, 5.0, 5.5 y 6), mapa del PMV (módulos 6 y 8 y encargos), «Corte - Kit de PTU» (13/11/2026) y kit maestro de PTU rev. 74 (regla R-3, D-11 y D-14), especificación del módulo 4 v1.4 (4.8, 5.1, 5.3 y 9), especificación de vacaciones y aguinaldo v1.0 (10 y 15), texto vigente de la LFT (última reforma DOF 14-05-2026) y convenio de afiliación de centro de trabajo del Instituto FONACOT, formulario FO411.07 (persona moral), publicado en fonacot.gob.mx.

Decisiones del usuario del 15/11/2026 (provisionales hasta la revisión final). Cada regla que deriva de una de ellas lleva la marca **[Dn]**.

| # | Decisión | Resolución |
| --- | --- | --- |
| D1 | ¿La casilla «pagado» basta para dar un pago por cumplido? | No. La casilla deja el pago en «Pago declarado», con alertas; solo la evidencia (CFDI o dispersión por persona) lo lleva a «Pagada» |
| D2 | Orden entre «Pagada» y D-14 | «Pagada» se alcanza con la evidencia; D-14 se genera después con el UUID y su firma se controla aparte (D14_FIRMADO). Cambia la definición de «Pagada» de la regla R-3 del kit (encargo al kit, vía Cerebro) |
| D3 | Evidencia del pago del finiquito | El módulo 6 la guarda, sin alertas propias. Se captura una sola vez, en el cierre de la baja del módulo 4, que ya la pide; el módulo 6 no tiene una captura aparte para el finiquito |
| D4 | Lectura del CFDI | Carga del XML, que el sistema lee y coteja; el PDF y la captura manual del UUID se admiten con alerta |
| D5 | Crédito Fonacot en el finiquito | Solo se retiene la amortización que corresponde al último periodo pagado; nunca el saldo del crédito; sin descuento de Fonacot en fallecimiento. Se descarta FON-2 |
| D6 | ¿Se importa la cédula de Fonacot? | El archivo es evidencia obligatoria; la importación por persona es opcional y solo sirve para cotejar |
| D7 | Aviso FON-1 a la persona con crédito que causa baja | Sí, como opción de la empresa (FONACOT_AVISO_PERSONA), activado por omisión |

---

## 0. Convenciones

- Rigen las convenciones de la especificación de permisos v1.4 (sección 0) y de vacaciones v1.0: variables `{{MAYÚSCULAS}}`, condiciones `[SI …] … [FIN SI]` (sus marcas nunca se imprimen), términos fijos «la Empresa» y «la Persona Trabajadora», Arial, PDF generado en el servidor, fechas largas y montos en MXN con dos decimales.
- Niveles de captura: **E** empresa · **O** organigrama · **A** alta · **V** evento (pantallas de estos módulos) · **S** calculada · **B** bitácora · **X** tabla global que administra AEXIS.
- **Días hábiles:** calendario de días inhábiles del módulo 4.
- Reglas de pantalla del registro 5.0: guardar nunca se bloquea; sin candados por fecha; los campos que dependen de una opción aparecen después de ella y sin valor por omisión si la Ley no lo fija.
- **Ningún texto ni código fija cifras que cambian.** Plazos legales y del convenio de Fonacot, calendario de cédulas, claves del catálogo de percepciones del SAT y tolerancias viven en tablas con vigencia.
- **Estos módulos no calculan.** El aguinaldo lo calcula el módulo 11, la PTU el kit (R-4 y R-5), el finiquito el módulo 4 y las retenciones de Fonacot el Instituto, con su cédula. Los módulos 6 y 8 registran, cotejan cifras ya capturadas, alertan y guardan la evidencia.

---

# PARTE I. MÓDULO 6 — VALIDACIÓN DE PAGO DE PTU Y AGUINALDO

## 1. Arquitectura

| Entidad | Qué es | Se crea |
| --- | --- | --- |
| Obligación de pago (`PAGO_OBLIGACION`) | Lo que la Empresa debe pagar a una persona por un concepto y un periodo | Automáticamente, desde el módulo de origen (sección 2) |
| Registro de pago (`PAGO_REGISTRO`) | Cada pago aplicado a una obligación (puede haber varios: pagos parciales, complementarios o sustitutos) | Al registrar un pago, por persona o por lote |
| Evidencia (`PAGO_EVIDENCIA`) | Archivo que acredita el pago: XML o PDF del CFDI, layout o comprobante de dispersión, recibo firmado | Al cargarla; un archivo puede respaldar varios registros (un lote) |
| Lote (`PAGO_LOTE`) | Agrupación de registros con una fecha y un medio de pago comunes | Al registrar pagos en grupo |

Conceptos (`PAGO_CONCEPTO`):

| Concepto | Origen del monto | Fecha límite |
| --- | --- | --- |
| Aguinaldo {año} | Módulo 11: `AGUINALDO_MONTO` con `AGUINALDO_VALIDADO` | `AGUINALDO_FECHA_PAGO` (empresa); límite legal: 19 de diciembre (art. 87 LFT, «antes del día veinte de diciembre») |
| PTU {ejercicio} | Kit de PTU: monto individual del dictamen B firme y neto de R-5 con `PTU_CALCULO_VALIDADO` | `FECHA_LIMITE_PAGO` del kit (art. 122 LFT) |
| PTU adicional {ejercicio} | Kit de PTU: reparto adicional (D-08 B modificado) | `FECHA_LIMITE_PAGO_ADICIONAL` del kit |
| Finiquito **[D3]** | Módulo 4: `TOTAL_NETO` con `CALCULO_VALIDADO` | Sin alerta en este módulo. La evidencia se captura en el cierre de la baja del módulo 4 y se guarda aquí |

Regla de unicidad: una sola obligación por persona, concepto y periodo. Si el módulo de origen recalcula (por ejemplo, el contador revierte `AGUINALDO_VALIDADO`), la obligación se actualiza y guarda su versión anterior en la bitácora; si ya tenía pagos registrados, pasa a «Observada» (sección 4.4).

---

## 2. Nacimiento de las obligaciones

1. **Aguinaldo.** Al validar el contador el cálculo de una persona (`AGUINALDO_VALIDADO`, módulo 11, 10.4), se crea su obligación con `PAGO_MONTO_BRUTO` = `AGUINALDO_MONTO`. El aguinaldo no tiene neto en el sistema (lo calcula nómina; módulo 11, 10.6).
2. **PTU.** Al quedar firme el dictamen con RESULTADO = B y validarse el precálculo de la persona (`PTU_CALCULO_VALIDADO`), se crea su obligación con `PAGO_MONTO_BRUTO` = monto individual del dictamen y `PAGO_MONTO_NETO` = `MONTO_NETO` de R-5. Incluye a las personas con `EX_TRABAJADOR` = Sí.
3. **PTU adicional.** Igual que la PTU, con el monto adicional y su fecha límite.
4. **Finiquito [D3].** Al validarse el cálculo de la baja (`CALCULO_VALIDADO`), con `PAGO_MONTO_NETO` = `TOTAL_NETO`. Si el convenio prevé pago diferido, se crea una obligación por parcialidad (`CONV_PARCIALIDADES`). El registro del pago y su evidencia (comprobante de transferencia, Anexo 2 del convenio, y CFDI) los captura RH en la pantalla de cierre de la baja del módulo 4; el módulo 6 los recibe, aplica el cotejo de 4.3 y los guarda. Lo que el módulo 4 exige para cerrar la baja no cambia desde este módulo.
5. **Personas excluidas de la obligación anual.** Si la persona causa baja antes del pago del aguinaldo, no se crea su obligación anual: el aguinaldo proporcional se paga en el finiquito (módulo 11, 10.5). Si la obligación ya existía y no tenía pago, pasa a «Pagada en finiquito» cuando el finiquito tenga evidencia de pago (sección 6).

---

## 3. Estados (`PAGO_ESTADO`)

| Estado | Condición | Efectos |
| --- | --- | --- |
| Pendiente | Obligación creada, sin registro de pago | Alertas del calendario (sección 5) |
| Pago declarado **[D1]** | RH marcó «pagado» sin evidencia | No cierra la obligación. Alerta a RH a los `PAGO_EVIDENCIA_DIAS` días hábiles y después cada semana. No habilita D-11 Parte 2 ni la exportación probatoria como «Pagada» |
| Pago parcial | La suma de pagos con evidencia es menor que el monto | Alerta a RH y al contador. Si vence la fecha límite, alerta crítica |
| Observada | La evidencia no coincide con la obligación (4.4) o el CFDI fue cancelado | Alerta al contador; se resuelve con «Aceptar con motivo» o con nueva evidencia |
| Pagada | Evidencia cotejada que cubre el monto (4.3) | Cierra la obligación. Para PTU, habilita D-14 con el UUID **[D2]** |
| Pagada en finiquito | El concepto se pagó dentro del finiquito (sección 6) | Bloquea un segundo pago del mismo concepto y periodo |
| Pendiente con aviso | Solo PTU: ex trabajador que no ha cobrado y ya recibió el aviso D-11 Parte 1 | Recordatorio y alerta de traspaso del kit (R-3) |
| No reclamada | Solo PTU: venció `FECHA_TRASPASO_PTU` sin cobro | El monto pasa a `MONTO_NO_RECLAMADO_ANTERIOR` del reparto siguiente (R-3) |
| Cancelada | La obligación dejó de existir (por ejemplo, el dictamen se sustituyó) | Solo con motivo y usuario; nunca se borra |

**Equivalencia con los cinco estados de la regla R-3 del kit de PTU** (`PTU_ESTADO_PAGO`, derivada): Pendiente de pago = Pendiente, Pago declarado, Pago parcial u Observada · Pagada = Pagada · Pagada en finiquito, Pendiente con aviso y No reclamada, iguales. El kit no necesita estados nuevos; solo ve el estado derivado.

**[D2] Cambio que afecta al kit (no se modifica desde aquí):** la regla R-3 define «Pagada» como «con CFDI o dispersión validados **y recibo D-14**», y el encargo pide que D-14 tome el UUID del estado «Pagada». Las dos cosas no pueden ser ciertas a la vez. Decisión del usuario (15/11/2026): «Pagada» = evidencia cotejada; D-14 se genera después y su firma se controla con `D14_FIRMADO`, que no revierte el estado y, si falta, solo genera alerta (regla 5.0: la casilla «documento firmado» basta y el archivo es opcional).

---

## 4. Qué significa «validar un pago»

### 4.1 Registro por persona

En la fila de la persona: botón «Registrar pago» → fecha de pago, medio (Transferencia · Cheque · Efectivo), importe y evidencia. Si se marca «Pagado» sin evidencia, el registro queda como «Pago declarado» **[D1]**.

### 4.2 Registro por lote

1. RH elige el concepto y el periodo, y el sistema propone el lote con todas las obligaciones Pendientes del concepto (puede quitar personas).
2. Carga la evidencia del lote, de una de estas formas:
   - **ZIP con los XML de los CFDI de nómina [D4].** El sistema asigna cada XML a su persona por la CURP del receptor del complemento de nómina y, en segundo lugar, por el RFC.
   - **Layout de dispersión bancaria** (CSV o XLSX con CURP o número de empleado, importe, fecha y referencia), con el comprobante global del banco como archivo adjunto.
3. El sistema muestra el resultado del cotejo: asignados, sin persona (archivo que no corresponde a nadie del lote), personas sin evidencia y discrepancias. RH confirma.
4. **Cuadre del lote:** la suma de los importes individuales debe ser igual al total del comprobante global de dispersión. Si no cuadra, el lote completo queda «Observado» y no se cierra ninguna obligación.
5. Un comprobante bancario global sin detalle por persona no basta para dar por pagada a ninguna persona: se acepta como archivo del lote, pero las obligaciones quedan en «Pago declarado» hasta que se cargue el detalle por persona.

### 4.3 Evidencia y cotejo

| Evidencia | Cotejo automático | Si cumple |
| --- | --- | --- |
| XML del CFDI de nómina **[D4]** | RFC del emisor = RFC de la Empresa · CURP del receptor = CURP de la persona · percepción con la clave del catálogo del SAT que corresponde al concepto (tabla `PAGO_CLAVES_SAT`, X) · importe gravado + exento de esa percepción = `PAGO_MONTO_BRUTO`, dentro de `PAGO_TOLERANCIA` · UUID con formato válido y no usado para otra persona | Pagada; se guarda `UUID_CFDI` y la fecha de pago del XML |
| PDF del CFDI o UUID capturado a mano | Formato del UUID y que no esté usado para otra persona; el importe lo captura RH | Pagada, con alerta permanente «CFDI sin XML: cotejo manual» |
| Dispersión bancaria (layout por persona) | Importe por persona = `PAGO_MONTO_NETO` (PTU y finiquito) dentro de la tolerancia. En aguinaldo, que no hay neto en el sistema, solo se valida que el importe sea mayor que cero y no mayor que `PAGO_MONTO_BRUTO` | Pagada; se guarda `REFERENCIA_DISPERSION`. Alerta «CFDI pendiente» hasta que se cargue el XML o el UUID |
| Recibo firmado (pago en efectivo o cheque) | Ninguno automático; para PTU, el recibo es el D-14 firmado | Pagada, con alerta «Pago sin medio bancario» y alerta «CFDI pendiente» |

Reglas:

- El CFDI es la evidencia principal. La dispersión prueba el pago, pero no sustituye al comprobante fiscal: mientras falte el UUID, la alerta «CFDI pendiente» se repite cada `PAGO_EVIDENCIA_DIAS` días hábiles.
- Un mismo UUID puede respaldar varios conceptos de la misma persona (aguinaldo pagado en la nómina ordinaria), nunca a dos personas.
- Las claves de percepción del SAT (por ejemplo, gratificación anual y participación de utilidades) viven en la tabla `PAGO_CLAVES_SAT`, porque el catálogo del complemento de nómina puede cambiar. Valores por cargar al instalar: verificarlos contra el catálogo vigente del SAT.
- La verificación del estado del CFDI ante el SAT (vigente o cancelado) queda para una fase posterior; en el PMV, RH marca «CFDI cancelado» y carga el sustituto.

### 4.4 Discrepancias («Observada»)

| Caso | Efecto |
| --- | --- |
| Importe distinto del monto, fuera de la tolerancia | Observada; el contador ve la diferencia. «Aceptar con motivo» (motivo obligatorio, usuario y fecha) la pasa a Pagada; si la diferencia es a la baja, a Pago parcial |
| CURP o RFC del XML que no coincide | El archivo no se asigna; queda en «sin persona» |
| Clave de percepción distinta | Observada |
| CFDI cancelado | La obligación vuelve a Observada hasta cargar el sustituto; D-14 genera nueva versión con el UUID nuevo |
| El módulo de origen recalcula después del pago | Observada; si el nuevo monto es mayor, la diferencia se convierte en Pago parcial; si es menor, el contador decide (aceptar con motivo) |
| Pago después de la fecha límite | Pagada, con marca «Pago extemporáneo» y la fecha real; nunca se bloquea |

### 4.5 Quién hace qué

- RH registra pagos y evidencia.
- El contador resuelve las Observadas y los pagos parciales.
- Consultoría recibe las alertas escaladas (sección 5) y no captura pagos.
- Nadie puede borrar un registro de pago o una evidencia: solo sustituirla, con la anterior en la bitácora.

---

## 5. Calendario de alertas

Destinatarios: **RH**, **Ct** contador, **C** consultoría, **P** Persona Trabajadora.

### 5.1 Aguinaldo

Los días de aviso viven en `PAGO_ALERTAS_AGUINALDO` (E), con estos valores por omisión:

| Momento | Condición | Destinatarios | Nivel |
| --- | --- | --- | --- |
| 30 días antes de `AGUINALDO_FECHA_PAGO` | Cálculo provisional | RH, Ct | Ya existe en el módulo 11 (10.4); no se duplica |
| 10 días antes | Personas activas sin `AGUINALDO_VALIDADO` | RH, Ct | Preventiva |
| 3 días hábiles antes | Obligaciones en Pendiente | RH | Preventiva |
| `AGUINALDO_FECHA_PAGO` | Obligaciones en Pendiente, Pago declarado o Pago parcial | RH, Ct | Crítica |
| 19 de diciembre (límite legal) | Ídem | RH, Ct, C | Crítica, escalada: «El aguinaldo debe pagarse antes del 20 de diciembre (art. 87 LFT)» |
| 20 de diciembre en adelante, cada `ALERTA_BAJA_INTERVALO` días hábiles | Ídem | RH, C | Crítica, hasta que se resuelva |
| 31 de enero siguiente | Pagadas sin XML o sin UUID | RH | Preventiva («CFDI pendiente») |

Si el 19 de diciembre es inhábil en el calendario de la empresa, la alerta del límite legal se adelanta al día hábil anterior. `AGUINALDO_FECHA_PAGO` ya se ajusta así en el módulo 11.

### 5.2 PTU

Las fechas las calcula el kit; este módulo solo las lee.

| Momento | Condición | Destinatarios | Nivel |
| --- | --- | --- | --- |
| 15 y 5 días hábiles antes de `FECHA_LIMITE_PAGO` (`PAGO_ALERTAS_PTU`, E) | Obligaciones en Pendiente | RH, Ct | Preventiva |
| `FECHA_LIMITE_PAGO` | Obligaciones de personas activas sin pagar | RH, Ct, C | Crítica |
| `FECHA_LIMITE_PAGO` | Ex trabajadores sin aviso D-11 Parte 1 enviado | RH | Crítica (R-3: el aviso se envía a más tardar ese día) |
| `PTU_AVISO_RECORDATORIO_DIAS` después del aviso (60 por omisión, kit) | Pendiente con aviso | RH | Recordatorio a la persona |
| 30 días antes de `FECHA_TRASPASO_PTU` | Pendiente con aviso | C | Informativa (R-3) |
| `FECHA_TRASPASO_PTU` | Pendiente con aviso | RH, C | Paso automático a No reclamada (R-3) |
| Después de `FECHA_TRASPASO_PTU` | La persona reclama | RH, C | El sistema no paga; registra la reclamación y alerta para hacer valer la prescripción (R-3) |
| `FECHA_LIMITE_PAGO_ADICIONAL` | Reparto adicional sin pagar | RH, Ct, C | Crítica |

La presentación de objeciones ante el SAT no suspende el pago (art. 122 LFT; D-08): el sistema no ofrece una pausa de las alertas por objeción.

---

## 6. Personas que ya salieron

| Situación | Regla |
| --- | --- |
| Baja antes del pago del aguinaldo del año | No se crea la obligación anual; si ya existía sin pago, pasa a «Pagada en finiquito» cuando el finiquito tenga evidencia. El aguinaldo proporcional consta en el recibo de finiquito (módulo 4) |
| Baja después del pago del aguinaldo | La obligación anual queda Pagada; el finiquito no incluye aguinaldo ni descuenta el pago (módulo 11, 10.5) |
| Baja entre `AGUINALDO_VALIDADO` y el pago | Al registrarse la baja, la persona sale del lote pendiente y su obligación anual se cancela con motivo «Pago en finiquito»; el contador ve el aviso para no incluirla en la nómina anual |
| PTU determinada y no pagada a la baja | Si el finiquito incluye «PTU determinada no pagada», la obligación de PTU pasa a «Pagada en finiquito» con la evidencia del finiquito y bloquea el segundo pago (kit) |
| PTU no determinada a la baja | La obligación nace después, con `EX_TRABAJADOR` = Sí; se avisa con D-11 Parte 1 y sigue la regla R-3 |
| Fallecimiento | Lo pendiente se paga a beneficiarios con el convenio 7.8 del módulo 4; la evidencia es el pago a cada beneficiaria. Estado: Pagada, con marca «Pagada a beneficiarios» |
| Ex trabajador que cobra en ventanilla | Recibo D-14 con firma autógrafa y copia de identificación; pago por transferencia, D-14 por firma electrónica al correo personal si la persona conserva ese medio (firma electrónica v1.2) o autógrafa |

**Evidencia del finiquito [D3].** El módulo 6 la guarda con el mismo motor (concepto «Finiquito»), sin alertas propias. Se captura una sola vez, en el cierre de la baja del módulo 4, y sirve para el finiquito, para «Pagada en finiquito» (aguinaldo y PTU) y para el paquete probatorio.

---

## 7. Interfaz con D-11 y D-14 del kit de PTU

- **D-14** toma de este módulo `UUID_CFDI`, `FECHA_PAGO`, `FORMA_PAGO` y `REFERENCIA_DISPERSION` cuando la obligación está en «Pagada» **[D2]**. Antes de ese estado solo se genera como borrador. Si cambia el UUID (CFDI cancelado y sustituido), se genera una nueva versión de D-14.
- Con pago por dispersión sin UUID todavía, D-14 se genera sin el renglón del folio fiscal y con la referencia de la dispersión; al cargarse el UUID, se genera la nueva versión.
- **D-11 Parte 2** (constancia de cumplimiento) se habilita cuando todas las personas del Anexo 1 del dictamen están en Pagada, Pagada en finiquito o Pendiente con aviso (kit). Su Anexo 1 sale de este módulo: persona, monto, fecha, UUID o referencia de dispersión y estado.
- `D14_FIRMADO` (V): casilla «recibo firmado» y archivo opcional; sin casilla, alerta a RH a los `PAGO_EVIDENCIA_DIAS` días hábiles. No revierte «Pagada».

---

## 8. Conservación y paquete probatorio

- **Plazo:** cada evidencia se conserva por `PAGO_CONSERVACION_ANIOS` años desde la fecha del pago (5 por omisión), y nunca menos de un año después de terminada la relación de trabajo. Fundamento: art. 804, fr. IV y último párrafo LFT (comprobantes de PTU, vacaciones, aguinaldos y primas: durante el último año y un año después de extinguida la relación). El plazo de 5 años responde a la conservación fiscal y de seguridad social (CFF, art. 30; LSS, art. 15, fr. II): **pendiente de verificar en el texto vigente**.
- La omisión de estos documentos en juicio genera la presunción de ser ciertos los hechos de la demanda (art. 805 LFT). Por eso el sistema nunca borra una evidencia por sí solo: al vencer el plazo, alerta a consultoría para que decida la supresión o el bloqueo de los datos conforme al aviso de privacidad.
- Cada archivo guarda hash SHA-256, usuario, fecha y hora de carga, y queda en la bitácora (mismo mecanismo de la especificación de firma electrónica).
- **Paquete probatorio exportable**, por concepto y periodo (y por persona): relación de obligaciones con monto, fecha límite, fecha de pago, medio, UUID o referencia, estado y marcas (extemporáneo, aceptado con motivo); los XML y archivos de evidencia; D-14 (PTU) y, en su caso, D-11. Es un reporte del sistema (Arial, PDF del servidor), sin firma. No se crea una «constancia de pago de aguinaldo» propia: ante una inspección prueban el CFDI y la dispersión, no un documento que la Empresa firme para sí.

---

## 9. Pantallas del módulo 6

1. **Tablero de obligaciones:** filtros por concepto, periodo, centro, estado y activo o ex trabajador; semáforo por fecha límite; totales por estado (personas y montos).
2. **Registrar pago:** por persona (4.1) o por lote (4.2), con el resultado del cotejo antes de confirmar.
3. **Observadas:** bandeja del contador con la diferencia, la evidencia y los botones «Aceptar con motivo» y «Solicitar nueva evidencia».
4. **Ex trabajadores (PTU):** avisos D-11 Parte 1 enviados, recordatorios, fechas de traspaso y reclamaciones tardías.
5. **Expediente de pagos:** búsqueda por persona y exportación del paquete probatorio (8).
6. **Configuración:** tolerancia, días de alerta y conservación (sección 10).

---

## 10. Variables del módulo 6

### 10.1 Reutilizadas

Del módulo 11: `AGUINALDO_MONTO`, `AGUINALDO_VALIDADO`, `AGUINALDO_FECHA_PAGO`. Del kit de PTU: `FECHA_LIMITE_PAGO`, `FECHA_LIMITE_PAGO_ADICIONAL`, `FECHA_TRASPASO_PTU`, `PTU_AVISO_RECORDATORIO_DIAS`, `EX_TRABAJADOR`, `EX_TRABAJADORES`, `MONTO_NETO`, `PTU_CALCULO_VALIDADO`, `UUID_CFDI`, `REFERENCIA_DISPERSION`, `PTU_ESTADO_PAGO`, `FECHA_PAGO`, `FORMA_PAGO`, `MONTO_NO_RECLAMADO_ANTERIOR`. Del módulo 4: `TOTAL_NETO`, `CALCULO_VALIDADO`, `CONV_PARCIALIDADES`, `BAJA_FECHA`, `ALERTA_BAJA_INTERVALO` y el calendario de días inhábiles. Del alta: `TRAB_CURP`, `TRAB_RFC`. De la empresa: `PATRON_RFC`.

### 10.2 Nuevas

| Variable | Nivel | Tipo | Validación u omisión | Activa |
| --- | --- | --- | --- | --- |
| PAGO_OBLIGACION | S | Registro: persona, concepto, periodo, monto bruto, monto neto, fecha límite, versión | Una por persona, concepto y periodo | Todo el módulo |
| PAGO_CONCEPTO | S | Aguinaldo · PTU · PTU adicional · Finiquito [D3] | — | Origen y alertas |
| PAGO_MONTO_BRUTO / PAGO_MONTO_NETO | S | Moneda | Del módulo de origen | Cotejo 4.3 |
| PAGO_ESTADO | S | Sección 3 | Transiciones de la sección 3 | Alertas, D-11, D-14, paquete |
| PAGO_REGISTRO | V | Registro: fecha, medio, importe, evidencia, usuario | Varios por obligación | Estado |
| PAGO_MEDIO | V | Transferencia · Cheque · Efectivo | Sin valor por omisión | Cotejo 4.3 |
| PAGO_EVIDENCIA | V | Archivo + tipo (XML CFDI · PDF CFDI · Layout de dispersión · Comprobante bancario · Recibo firmado) + hash | Un archivo puede respaldar un lote | Estado; paquete |
| PAGO_LOTE | V | Identificador, fecha, medio, total, comprobante global | Cuadre 4.2, paso 4 | Registro en grupo |
| PAGO_TOLERANCIA | E | Moneda | 1.00 por omisión | Cotejo 4.3 y 4.4 |
| PAGO_CLAVES_SAT | X | Tabla con vigencia: concepto, clave de percepción del catálogo del SAT | Valores por verificar contra el catálogo vigente | Cotejo del XML |
| PAGO_EVIDENCIA_DIAS | E | Entero (días hábiles) | 5 por omisión | Alertas de Pago declarado, CFDI pendiente y D-14 sin firma |
| PAGO_ALERTAS_AGUINALDO | E | Lista de días antes de AGUINALDO_FECHA_PAGO | 10 y 3 hábiles por omisión | 5.1 |
| PAGO_ALERTAS_PTU | E | Lista de días hábiles antes de FECHA_LIMITE_PAGO | 15 y 5 por omisión | 5.2 |
| PAGO_EXTEMPORANEO | S | Sí/No | Fecha de pago > fecha límite | Marca en tablero y paquete |
| PAGO_ACEPTADO_MOTIVO | V | Texto + usuario + fecha | Obligatorio para «Aceptar con motivo» | Observada → Pagada o Pago parcial |
| PAGO_CFDI_CANCELADO | V | Sí/No + UUID sustituto | — | Observada; nueva versión de D-14 |
| PAGO_A_BENEFICIARIOS | S | Sí/No | Baja por fallecimiento | Marca de la sección 6 |
| PAGO_CONSERVACION_ANIOS | E | Entero | 5 por omisión; nunca menos que el plazo del art. 804 | Sección 8 |
| D14_FIRMADO | V | Casilla + archivo opcional | Regla 5.0 | Alerta; no revierte Pagada |

---

# PARTE II. MÓDULO 8 — FONACOT

## 11. Alcance

Decidido (26/10/2026): solo alertas y evidencia. **El sistema no calcula retenciones**: el crédito se retiene con la cuota que el Instituto notifica en su Cédula de Notificación de Altas y Pagos y lo aplica la nómina del cliente.

Marco verificado:

| Fuente | Qué establece | Uso en el módulo |
| --- | --- | --- |
| Art. 132, fr. XXVI Bis LFT | Afiliar el centro de trabajo al Instituto; la afiliación es gratuita | Sección 12 |
| Art. 132, fr. XXVI LFT | Hacer las deducciones de los arts. 97, fr. IV y 110, fr. VII, y enterarlas primero al Instituto; la obligación no convierte a la Empresa en deudora solidaria del crédito | Secciones 14 y 16 |
| Art. 110, fr. VII LFT | Descuentos aceptados libremente por la persona, sin exceder el 20 % del salario | Sección 16 (finiquito) |
| Art. 994, fr. III LFT (reforma DOF 04-04-2024) | Multa de 50 a 1500 UMA por no cumplir la fr. XXVI Bis del art. 132 | Mensaje de la alerta de afiliación |
| Art. 992 LFT | Si una omisión afecta a varias personas trabajadoras, se impone sanción por cada una | Mensaje de la alerta de afiliación |
| Convenio de afiliación FO411.07 (persona moral), cláusulas Cuarta a Décima Octava y Anexo A | Plazos de avisos e incidencias, entero mensual conforme al calendario del Instituto, intereses moratorios y gastos de cobranza por entero extemporáneo (no trasladables a las personas trabajadoras), responsabilidad directa de la Empresa por lo no descontado ni enterado | Secciones 13 a 17 |

**Los plazos de las secciones 13 a 17 salen del convenio, no de la Ley.** Por eso viven en la tabla `FONACOT_PLAZOS` (X) con la versión del convenio. El cliente puede tener firmada otra versión (la persona física usa otro apartado del formulario): al cargar su convenio, consultoría confirma los plazos de su versión.

**Fecha límite de entero: no confirmada.** Los procedimientos internos publicados por el Instituto (2019) remiten al «Calendario de Emisión, Cobro y Aplicación de Cédulas» con límite el quinto día hábil de cada mes; una publicación especializada de diciembre de 2025 lo sitúa al cierre del mes, con cinco días hábiles de gracia. El convenio solo remite al calendario anual que el Instituto publica en su portal. Por eso la fecha no se fija: vive en `FONACOT_CALENDARIO` (X), que AEXIS carga cada año desde el calendario oficial, con la misma mecánica de aprobación y monitor de los parámetros del módulo 4 (5.3). Mientras no se cargue, el sistema usa «quinto día hábil del mes» y muestra «Calendario Fonacot pendiente de confirmar».

---

## 12. Afiliación del centro de trabajo

### 12.1 Estados (`FONACOT_AFILIACION_ESTADO`, E; sin valor por omisión)

| Estado | Captura | Efecto |
| --- | --- | --- |
| Afiliada | `FONACOT_NUM_CLIENTE`, `FONACOT_AFILIACION_FECHA`, convenio firmado (`FONACOT_CONVENIO_ARCHIVO`) y su versión | Habilita las secciones 13 a 17. Sin archivo del convenio: alerta permanente, sin bloqueo (regla 5.0) |
| En trámite | Fecha de solicitud y acuse del portal | Alerta cada 15 días naturales hasta que cambie el estado |
| No procedente | Fecha y motivo que comunicó el Instituto (por ejemplo, antigüedad de operaciones menor a la que pide) + archivo | Nueva alerta en `FONACOT_REINTENTO_MESES` meses (12 por omisión) o en la fecha que capture RH |
| No afiliada | — | Alerta crítica a RH y consultoría con el mensaje de 12.2 |

### 12.2 Alertas

- **Empresa nueva en el sistema:** si el estado no es Afiliada, alerta a consultoría al dar de alta la empresa, y a RH y consultoría cada `FONACOT_AFILIACION_ALERTA_DIAS` días naturales (30 por omisión).
- **Mensaje fijo de No afiliada:** «La Empresa está obligada a afiliar su centro de trabajo al Instituto Fonacot; la afiliación es gratuita. La omisión puede sancionarse con multa (art. 994, fr. III LFT), que se impone por cada persona trabajadora afectada (art. 992 LFT).»
- La Ley no fija un plazo para afiliar a una empresa nueva (el plazo de doce meses del transitorio de 2012 ya venció). La alerta es una política del sistema, no un plazo legal, y así lo dice su texto en pantalla.
- **Centros de trabajo y sucursales:** el convenio considera las sucursales parte del centro afiliado y pide registrarlas (cláusula Décima Sexta). Al agregar un centro al catálogo de centros (registro 4.4, catálogo único), el sistema pregunta «¿Registrado en Fonacot como sucursal?» (`CENTRO_FONACOT`, Sí · No · No aplica) y alerta mientras sea No.
- **Afiliación anual:** sin alerta periódica; la afiliación es indefinida (cláusula Vigésima). Si el Instituto da por terminado el convenio, RH registra la fecha y el estado vuelve a No afiliada.

### 12.3 Documento

No se genera una «constancia de afiliación» propia. La evidencia de la afiliación es el convenio que firma el Instituto y su número de cliente; un documento emitido por la Empresa no acredita nada frente a una inspección. El sistema muestra una **ficha de afiliación** (reporte sin firma): estado, número de cliente, fecha, versión del convenio, responsable designado, centros registrados y archivos.

---

## 13. Créditos por persona

1. **Alta:** `FONACOT_CREDITO` (A; Sí · No; la persona lo declara; ya está pedida en el registro 5.5). Con Sí, alerta a RH: «Avise al Instituto del ingreso de una persona con crédito vigente», con el plazo de `FONACOT_PLAZOS` (Anexo A, art. 10: 7 días hábiles).
2. **Cédula [D6]:** cada mes, RH carga el archivo de la cédula descargado del portal del Instituto (obligatorio como evidencia). Opcionalmente importa el detalle por persona (CSV exportado del portal: número de trabajador o NSS, número de crédito, retención mensual). Con la importación:
   - Persona en la cédula con `FONACOT_CREDITO` = No: el dato pasa a Sí y se avisa a RH.
   - Persona con `FONACOT_CREDITO` = Sí que ya no aparece: aviso a RH para confirmar si liquidó el crédito («carta de no retención», Anexo A, art. 8).
   - Persona de la cédula que no está en el alta o tiene baja: alerta «Reporte la baja en la cédula».
3. Los créditos se guardan en `FONACOT_CREDITOS` (V, por persona): número de crédito, retención mensual según la cédula, mes de la primera cédula y fuente (Cédula · Declaración). **El sistema no calcula ni modifica la retención**: solo muestra la cifra de la cédula.
4. Alerta informativa, sin bloqueo: si la suma de las retenciones de Fonacot de la persona más los demás descuentos del art. 110 registrados en el sistema parece rebasar el límite, el sistema no lo calcula; solo recuerda en la ficha de la persona el límite del art. 110, fr. VII y remite a nómina.

---

## 14. Ciclo mensual de la cédula

### 14.1 Estados (`FONACOT_CEDULA_ESTADO`, por mes)

| Estado | Condición | Alerta |
| --- | --- | --- |
| Emitida | Llegó la fecha de emisión del calendario | RH: «Descargue la cédula del mes y aplique las retenciones en nómina» |
| Cargada | RH subió el archivo de la cédula | — |
| Incidencias registradas | RH marcó las incidencias del mes (sección 15) o declaró «Sin incidencias» | — |
| Pagada | RH subió el comprobante de pago (línea de captura y comprobante bancario) con fecha e importe | Cierra el mes |
| Vencida | Llegó la fecha límite sin estado Pagada | Crítica a RH y consultoría |

### 14.2 Alertas

| Momento | Destinatarios | Nivel |
| --- | --- | --- |
| Fecha de emisión (`FONACOT_CALENDARIO`) | RH | Informativa |
| 3 días hábiles antes de la fecha límite, sin estado Pagada | RH | Preventiva |
| Fecha límite, sin estado Pagada | RH, Ct | Crítica |
| Día hábil siguiente a la fecha límite, sin estado Pagada | RH, Ct, C | Crítica: «Entero extemporáneo: genera intereses moratorios y gastos de cobranza conforme al convenio, a cargo de la Empresa y sin trasladarse a las personas trabajadoras. El Instituto puede suspender nuevos créditos al personal.» |
| Cada `ALERTA_BAJA_INTERVALO` días hábiles después | RH, C | Crítica, hasta el pago |

### 14.3 Cotejo de importes (sin cálculo)

- RH captura dos cifras: el total de la cédula (`FONACOT_CEDULA_TOTAL`) y el importe pagado (`FONACOT_PAGO_IMPORTE`).
- Si el pagado es menor que el total y no hay incidencias registradas que expliquen la diferencia, alerta al contador y a consultoría: «Diferencia sin incidencia: la Empresa responde directamente de lo no descontado o no enterado (convenio, cláusula Décima Tercera).» No bloquea.
- Las retenciones hechas y no enteradas se consideran en depósito en poder de la Empresa (cláusula Novena): la alerta de Vencida lo dice.

### 14.4 Evidencia

Por mes: archivo de la cédula, incidencias registradas en el portal (captura de pantalla o acuse), línea de captura, comprobante bancario, fecha e importe. Se conservan con la regla de la sección 8 y entran al paquete probatorio de Fonacot (por mes o por persona).

---

## 15. Incidencias que deben reportarse al Instituto

El sistema detecta el hecho, crea la incidencia (`FONACOT_INCIDENCIA`) para cada persona con `FONACOT_CREDITO` = Sí y alerta a RH con el plazo de `FONACOT_PLAZOS`. La incidencia se cierra con la casilla «Reportada» y, opcionalmente, el acuse (regla 5.0).

| Hecho en el sistema | Fuente | Plazo (convenio FO411.07) | Mensaje |
| --- | --- | --- | --- |
| Ingreso de una persona con crédito vigente | Alta (`FONACOT_CREDITO` = Sí) o cédula | 7 días hábiles (Anexo A, art. 10) | «Avise el ingreso de una persona con crédito vigente» |
| Baja | Módulo 4 (`BAJA_FECHA`) | 5 días hábiles desde que la Empresa conoce la separación (cláusula Quinta) | Sección 16 |
| Incapacidad, licencia, permiso sin goce o suspensión que deja a la persona sin salario en el periodo | Módulo de permisos: C1 (después de los días de espera pagados), C2, C3, B3, B4, B5, permisos sin goce, D1 a D5; suspensión disciplinaria | 5 días hábiles (cláusulas Cuarta y Sexta) | «Reporte la incidencia en la cédula: en ese periodo no hay salario del cual descontar» |
| Defunción, incapacidad permanente total o invalidez | Módulo 4 (motivo Fallecimiento o Incapacidad) o captura de RH | 15 días hábiles, con el acta o el certificado (cláusula Séptima) | «Reporte el hecho al Instituto con el acta o el certificado» |
| Emplazamiento a huelga | Captura de RH | 3 días hábiles (cláusula Octava) | Informativa |
| Cambio de domicilio, sustitución patronal o de régimen | Configuración de la empresa (cambio de domicilio o de razón social) | 5 días hábiles (cláusula Décima Quinta); sin aviso, el Instituto suspende al centro | «Informe el cambio al Instituto» |

---

## 16. Baja y fallecimiento (interfaz con el módulo 4)

1. **Alerta de baja.** `FONACOT_AVISO_DIAS` del módulo 4 deja de estar «pendiente de verificar»: por omisión, 5 días hábiles (cláusula Quinta del convenio), tomado de `FONACOT_PLAZOS`. La alerta del módulo 4 y la incidencia de la sección 15 son la misma; se cierra una sola vez.
2. **[D5] Retención en el finiquito.** El convenio prohíbe seguir descontando cuando concluye la relación (cláusula Cuarta). Regla propuesta para el renglón automático «Crédito Fonacot» del módulo 4 (4.8):
   - solo procede la amortización que la cédula asigna al último periodo de salario que se paga en el finiquito, proporcional a los días de ese periodo;
   - nunca el saldo del crédito ni importes de otros conceptos del finiquito;
   - aviso en pantalla, sin bloqueo, si el importe capturado supera la retención mensual de la cédula: «Solo se retiene la amortización del último periodo; el saldo lo paga la Persona Trabajadora directamente al Instituto».
   - Si la persona quiere liquidar su crédito con el finiquito, lo hace ella ante el Instituto. La Empresa no recibe instrucciones de pago del crédito (FON-2 descartada).
3. **Fallecimiento.** No se agrega el renglón automático de Fonacot en el convenio de pago a beneficiarios (módulo 4, 7.8): se alerta el aviso de la cláusula Séptima (15 días hábiles con el acta de defunción). El descuento a beneficiarias del saldo de un crédito que el aviso puede extinguir sería improcedente.
4. **Aviso a la Persona Trabajadora [D7].** Con `FONACOT_AVISO_PERSONA` = Sí (empresa; Sí por omisión), en toda baja de una persona con `FONACOT_CREDITO` = Sí se genera FON-1 (sección 20), que se entrega con el paquete de baja.
5. La retención del último periodo se entera en la cédula siguiente, con la incidencia de baja.

---

## 17. Pantalla del módulo 8

1. **Afiliación:** ficha (12.3), estado, archivos y centros registrados.
2. **Cédulas:** una fila por mes con estado, fechas del calendario, total, pagado, diferencia, incidencias y archivos.
3. **Personas con crédito:** créditos (13.3), incidencias abiertas y cerradas, historial de cédulas.
4. **Incidencias pendientes:** bandeja con plazo y semáforo.
5. **Configuración:** `FONACOT_PLAZOS` y `FONACOT_CALENDARIO` (solo consultoría; X), alertas de afiliación y FON-1 (E).

---

## 18. Variables del módulo 8

### 18.1 Reutilizadas

`FONACOT_CREDITO` (A; pedida en el registro 5.5, falta darla de alta), `FONACOT_AVISO_DIAS` (E, módulo 4), `BAJA_FECHA`, `BAJA_MOTIVO`, eventos del módulo de permisos, catálogo de centros, `ALERTA_BAJA_INTERVALO`, calendario de días inhábiles, `TRAB_NOMBRE`, `TRAB_EMAIL`, `PATRON_RAZON_SOCIAL`, `LUGAR_FIRMA`, `FECHA_FIRMA`.

### 18.2 Nuevas

| Variable | Nivel | Tipo | Validación u omisión | Activa |
| --- | --- | --- | --- | --- |
| FONACOT_AFILIACION_ESTADO | E | Afiliada · En trámite · No procedente · No afiliada | Sin valor por omisión | 12 |
| FONACOT_NUM_CLIENTE | E | Texto | Obligatorio con Afiliada | Ficha; incidencias |
| FONACOT_AFILIACION_FECHA | E | Fecha | Con Afiliada | Ficha |
| FONACOT_CONVENIO_ARCHIVO / FONACOT_CONVENIO_VERSION | E | Archivo / texto | Sin archivo: alerta | Ficha; FONACOT_PLAZOS |
| FONACOT_RESPONSABLE | E | Usuario del sistema | Recomendado | Destinatario de alertas del módulo 8 |
| FONACOT_SOLICITUD_FECHA / FONACOT_NO_PROCEDENTE_MOTIVO | E | Fecha / texto + archivo | Según estado | 12.1 |
| FONACOT_AFILIACION_ALERTA_DIAS | E | Entero | 30 | 12.2 |
| FONACOT_REINTENTO_MESES | E | Entero | 12 | 12.1 |
| CENTRO_FONACOT | E (catálogo de centros) | Sí · No · No aplica | Sin valor por omisión | 12.2 |
| FONACOT_AVISO_PERSONA | E | Sí/No | Sí por omisión [D7] | FON-1 |
| FONACOT_PLAZOS | X | Tabla con vigencia y versión del convenio: incidencia, plazo, unidad | Valores de la sección 15 | 15 y 16 |
| FONACOT_CALENDARIO | X | Tabla anual: mes, fecha de emisión, fecha límite | Aprobación humana (módulo 4, 5.3) | 14 |
| FONACOT_CREDITOS | V | Tabla por persona: número de crédito, retención mensual, mes de inicio, fuente | Solo de la cédula o declarada | 13 |
| FONACOT_CEDULA | V | Por mes: archivo, fecha de carga, importación opcional [D6] | Archivo obligatorio para pasar a Cargada | 14 |
| FONACOT_CEDULA_ESTADO | S | Sección 14.1 | — | Alertas |
| FONACOT_CEDULA_TOTAL / FONACOT_PAGO_IMPORTE / FONACOT_PAGO_FECHA | V | Moneda / moneda / fecha | Capturadas | 14.3 |
| FONACOT_PAGO_EVIDENCIA | V | Archivos: línea de captura y comprobante | — | Pagada |
| FONACOT_SIN_INCIDENCIAS | V | Casilla por mes | — | 14.1 |
| FONACOT_INCIDENCIA | S/V | Registro: persona, tipo, fecha del hecho, plazo, reportada, acuse | Sección 15 | Bandeja |
| FONACOT_RETENCION_FINIQUITO (+ _LETRA) | V (módulo 4) | Moneda; texto | Es el importe del renglón «Crédito Fonacot» del finiquito; aviso si supera la retención mensual de la cédula [D5] | FON-1 |
| FONACOT_BAJA_REPORTE_FECHA | V | Fecha | Al cerrar la incidencia de baja | FON-1 |

---

# PARTE III. DEPENDENCIAS, CONTRADICCIONES, PENDIENTES, PRUEBAS Y TEXTOS

## 19. Dependencias

| Pieza | Qué necesitan estos módulos | Estado |
| --- | --- | --- |
| Módulo 11 (vacaciones y aguinaldo) | `AGUINALDO_MONTO`, `AGUINALDO_VALIDADO`, `AGUINALDO_FECHA_PAGO`; salida de la persona del cálculo anual por baja | Vigente; el encargo «usar AGUINALDO_FECHA_PAGO» queda cumplido aquí |
| Kit de PTU | Fechas, montos, `EX_TRABAJADOR`, R-3, D-11 y D-14 | **Encargo [D2]**: definición de «Pagada» en R-3 |
| Módulo 4 | Baja, finiquito, evidencia de pago capturada en el cierre de la baja, renglón automático de Fonacot, `FONACOT_AVISO_DIAS` | **Encargos [D3] y [D5]**: enviar al módulo 6 la evidencia del cierre; regla de importe del renglón Fonacot; fallecimiento sin renglón de Fonacot; `FONACOT_AVISO_DIAS` = 5 días hábiles por omisión |
| Módulo de permisos | Eventos que generan incidencias de Fonacot (15) | Solo lectura; sin cambio |
| Configuración de la empresa | Variables nuevas de afiliación y `CENTRO_FONACOT` en el catálogo de centros | **Se piden a Cerebro** |
| Alta | `FONACOT_CREDITO` | Ya pedida (registro 5.5); falta darla de alta |
| Firma electrónica v1.2 | D-14 de ex trabajadores; FON-1 sigue el paquete de baja (autógrafo) | Vigente |
| Parámetros globales (módulo 4, 5.3) | Mecánica de aprobación para `FONACOT_CALENDARIO`, `FONACOT_PLAZOS` y `PAGO_CLAVES_SAT` | Vigente |

## 20. Textos

### FON-1. Aviso sobre el crédito Fonacot al terminar la relación de trabajo [D7]

Se genera en toda baja (salvo fallecimiento) de una persona con `FONACOT_CREDITO` = Sí, si `FONACOT_AVISO_PERSONA` = Sí. Se entrega con el convenio y el recibo de finiquito y se firma de recibido en forma autógrafa, igual que el paquete de baja. Si la persona no se presenta, se envía a `TRAB_EMAIL` y queda la constancia de envío en la bitácora. No contiene renuncia de derechos ni declaraciones de la Persona Trabajadora.

```text
AVISO SOBRE SU CRÉDITO FONACOT

{{LUGAR_FIRMA}}, a {{FECHA_FIRMA}}.

{{TRAB_NOMBRE}}

{{PATRON_RAZON_SOCIAL}} le informa que, con motivo de la terminación de su relación de trabajo el {{BAJA_FECHA}}, [SI FONACOT_BAJA_REPORTE_FECHA capturada]el {{FONACOT_BAJA_REPORTE_FECHA}} reportó[FIN SI][SI FONACOT_BAJA_REPORTE_FECHA vacía]reportará[FIN SI] su baja al Instituto del Fondo Nacional para el Consumo de los Trabajadores.

[SI FONACOT_RETENCION_FINIQUITO > 0]
En su finiquito se retuvo la cantidad de {{FONACOT_RETENCION_FINIQUITO}} ({{FONACOT_RETENCION_FINIQUITO_LETRA}}), que corresponde a la amortización de su crédito por el último periodo de salario que se le paga. La Empresa la entregará al Instituto.
[FIN SI]

A partir de la terminación de la relación de trabajo, la Empresa ya no puede descontar de su salario los pagos de su crédito. El saldo pendiente debe cubrirlo directamente ante el Instituto o, si ingresa a otro centro de trabajo afiliado, mediante los descuentos que se apliquen en su nueva nómina, conforme a las condiciones de su crédito. Para conocer su saldo y las formas de pago, consulte los medios oficiales del Instituto.

______________________________
{{FIRMA_EMPRESA_NOMBRE}}, {{FIRMA_EMPRESA_CARGO}}

Recibí: ______________________________ {{TRAB_NOMBRE}}, el ___ de ________ de ____.
```

Reglas: Arial 12; una hoja; firma por la Empresa la persona de RH designada (`FIRMANTES_EMPRESA`) o, sin ella, el representante. El texto no menciona el monto del saldo ni seguros del crédito, porque la Empresa no los conoce con certeza.

### FON-2. Descartada (D5, 15/11/2026)

No se programa. La Empresa no recibe del finiquito pagos voluntarios del crédito.

## 21. Contradicciones detectadas

| # | Contradicción | Resolución (15/11/2026) |
| --- | --- | --- |
| 1 | Regla R-3 del kit: «Pagada» exige recibo D-14; el encargo pide que D-14 tome el UUID de «Pagada» | [D2]: «Pagada» = evidencia; firma de D-14 aparte |
| 2 | Módulo 4, sección 9, remite al módulo 6 la evidencia del finiquito; el mapa no la incluye en el alcance del módulo 6 | [D3]: el módulo 6 la guarda, sin alertas propias; se captura en el cierre de la baja del módulo 4 |
| 3 | Registro 5.5 y módulo 4 (5.1): baja ante Fonacot «configurable mientras se verifica» | 5 días hábiles por omisión (convenio FO411.07, cláusula Quinta), en `FONACOT_PLAZOS`; es plazo contractual, no legal |
| 4 | Módulo 4 (4.8): el renglón automático «Crédito Fonacot» no tiene regla de importe | [D5]: solo la amortización del último periodo; sin renglón en fallecimiento |
| 5 | Regla 5.0 (la casilla basta para avanzar) frente a la regla R-3 (CFDI o dispersión obligatorios para «Pagada») | [D1]: la casilla avanza a «Pago declarado», con alertas; la evidencia lleva a «Pagada» |

## 22. Pendientes que no bloquean la programación

- Cargar `FONACOT_CALENDARIO` 2026 y 2027 desde el calendario oficial del Instituto y confirmar la fecha límite real de entero.
- Confirmar los plazos de `FONACOT_PLAZOS` con el convenio que firmó cada cliente (persona física y persona moral).
- Verificar las claves vigentes del catálogo de tipos de percepción del complemento de nómina para `PAGO_CLAVES_SAT`.
- Verificar CFF, art. 30 y LSS, art. 15, fr. II para el plazo de conservación de 5 años.
- Verificar con el contador si el CFDI de nómina se puede emitir después de la dispersión y en qué plazo (la alerta «CFDI pendiente» usa `PAGO_EVIDENCIA_DIAS`).
- Fase posterior: verificación del estado del CFDI ante el SAT.

## 23. Casos de prueba

| Caso | Datos | Resultado esperado |
| --- | --- | --- |
| 1. Lote de aguinaldo con XML | 3 personas validadas; ZIP con 3 XML, clave correcta, importes iguales | 3 Pagadas; UUID guardados; paquete exportable |
| 2. Importe distinto | XML con $10.00 menos que `AGUINALDO_MONTO`; tolerancia $1.00 | Observada; con «Aceptar con motivo» del contador → Pago parcial (diferencia a la baja) |
| 3. Solo casilla | RH marca «pagado» sin archivo | Pago declarado; alerta a los 5 días hábiles; no cuenta como Pagada en el paquete |
| 4. Aguinaldo sin pagar | `AGUINALDO_FECHA_PAGO` 15/12/2026; persona en Pendiente | Crítica el 15/12; escalada a consultoría el 19/12/2026 (sábado: si es inhábil para la empresa, la alerta del límite legal se adelanta al día hábil anterior) |
| 5. Baja antes del pago | Baja el 10/12/2026 con aguinaldo validado sin pagar | La obligación anual se cancela con motivo «Pago en finiquito»; con la evidencia del finiquito, Pagada en finiquito |
| 6. Dispersión de PTU | Layout con neto igual a `MONTO_NETO`, sin XML | Pagada con alerta «CFDI pendiente»; D-14 sin folio fiscal; al cargar el UUID, D-14 versión 2 |
| 7. Ex trabajador | `EX_TRABAJADOR` = Sí, sin cobro | Aviso D-11 Parte 1 a más tardar en `FECHA_LIMITE_PAGO`; recordatorio a los 60 días; No reclamada al vencer `FECHA_TRASPASO_PTU` |
| 8. Lote que no cuadra | Comprobante global $100,000.00; suma del layout $99,500.00 | Lote Observado; ninguna obligación cambia de estado |
| 9. Empresa nueva no afiliada | Alta de la empresa con estado No afiliada | Alerta a consultoría al alta y cada 30 días; mensaje de 12.2 |
| 10. Baja con crédito | Persona con `FONACOT_CREDITO` = Sí, baja el lunes 23/11/2026 | Incidencia de baja con plazo de 5 días hábiles: lunes 30/11/2026; FON-1 en el paquete de baja |
| 11. Incapacidad | C2 registrada a una persona con crédito | Incidencia «Reporte la incidencia en la cédula», 5 días hábiles |
| 12. Cédula vencida | Sin comprobante el día hábil siguiente a la fecha límite del calendario | Estado Vencida; crítica a RH, contador y consultoría con el mensaje de 14.2 |
| 13. Diferencia sin incidencia | Total de cédula $8,000.00; pagado $7,200.00; sin incidencias | Alerta al contador y consultoría (cláusula Décima Tercera); no bloquea |

## 24. Impacto en el sistema

Variables que se piden a Cerebro (niveles 1 a 3):

| Variable | Nivel | Tipo | Validación | Qué activa |
| --- | --- | --- | --- | --- |
| FONACOT_AFILIACION_ESTADO, FONACOT_NUM_CLIENTE, FONACOT_AFILIACION_FECHA, FONACOT_CONVENIO_ARCHIVO, FONACOT_CONVENIO_VERSION, FONACOT_RESPONSABLE, FONACOT_SOLICITUD_FECHA, FONACOT_NO_PROCEDENTE_MOTIVO | Empresa | Sección 18.2 | Estado sin valor por omisión | Sección 12 (resuelve el hallazgo 11 de las pantallas: «afiliación a Fonacot» en el alta de la empresa) |
| FONACOT_AFILIACION_ALERTA_DIAS, FONACOT_REINTENTO_MESES, FONACOT_AVISO_PERSONA | Empresa | Entero / entero / Sí-No | 30 / 12 / Sí | 12.2, 12.1 y FON-1 |
| CENTRO_FONACOT | Empresa (catálogo de centros) | Sí · No · No aplica | Sin valor por omisión | 12.2 |
| PAGO_TOLERANCIA, PAGO_EVIDENCIA_DIAS, PAGO_ALERTAS_AGUINALDO, PAGO_ALERTAS_PTU, PAGO_CONSERVACION_ANIOS | Empresa | Sección 10.2 | Valores por omisión de 10.2 | Módulo 6 |
| FONACOT_CREDITO | Alta | Sí/No | Ya pedida en 5.5 | Secciones 13, 15 y 16; renglón automático del módulo 4 |

Tablas globales (X, AEXIS): `FONACOT_PLAZOS`, `FONACOT_CALENDARIO`, `PAGO_CLAVES_SAT`. Las demás variables son de evento o calculadas y viven en estos módulos.
