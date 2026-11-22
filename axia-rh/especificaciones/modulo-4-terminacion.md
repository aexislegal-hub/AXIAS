# AXIA RH — MÓDULO 4: TERMINACIÓN DE LA RELACIÓN DE TRABAJO Y PRECÁLCULO DE FINIQUITO

Especificación para programación · Versión 1.5 · 17/11/2026 (con los encargos 12 a 15 del mapa agregados el 20 y 21/11/2026)
Fuente: documento de trabajo «Axia RH — Módulo 4», registro de decisiones (4.8, 4.10, 4.12, 4.13 y 5.5), encargos del mapa del PMV al módulo 4 (15, 17 y 18/11/2026) y ajustes del usuario del 10 y 12/11/2026.

## Cambios respecto de la versión 1.4 (la que está cargada en el software)

Aplicar estos cambios sobre la 1.4. Ante cualquier duda, rige el texto completo de este documento. Todos vienen de decisiones ya registradas en otros módulos; ninguno cambia el texto del convenio.

| # | Sección | Cambio | Origen |
| --- | --- | --- | --- |
| 1 | 1, 2.4 (nueva), 8.2, 8.3 | **Situaciones protegidas sin bloqueo:** si el módulo de permisos envía `SITUACION_PROTEGIDA` = Sí, la pantalla muestra una alerta crítica y pide doble confirmación (`BAJA_CONFIRMACION_PROTEGIDA`). La comisión permanente vigente (B4) sigue la misma mecánica (`BAJA_CONFIRMACION_B4`). Nunca se imprime | Registro 4.8, decisión 19 (15/11) |
| 2 | 2.2 | Mensaje informativo si la persona tiene una suspensión por falta de documentos (D4) vencida | Registro 4.8 (12/11) |
| 3 | 4.3, 4.9 (nueva), 7.6, 8.2 | Vacaciones y aguinaldo se toman del módulo de vacaciones y aguinaldo: saldos por periodo, proporcional, prescritos solo informativos; el aguinaldo ya pagado en el año no se vuelve a pagar ni se descuenta | Registro 4.10 (15/11) |
| 4 | 4.3, 8.2 | El salario sale de `SALARIO_PERSONA` y de la versión de condiciones de la persona a `BAJA_FECHA`; en ascenso temporal, el salario del puesto ocupado | Registro 4.12 (15/11) |
| 5 | 4.8 | Renglón automático «Crédito Fonacot»: solo la amortización del último periodo de salario pagado (`FONACOT_RETENCION_FINIQUITO`), con aviso si supera la retención mensual de la cédula. En fallecimiento no hay renglón de Fonacot | Registro 4.13 (15/11) |
| 6 | 5.1 | Baja ante Fonacot: 5 días hábiles por omisión (`FONACOT_AVISO_DIAS`, de `FONACOT_PLAZOS`), por convenio y no por Ley. Alerta nueva del aviso de defunción a Fonacot (15 días hábiles) | Registro 4.13 y 5.5 (15/11) |
| 7 | 3, 7.10 (nueva) | FON-1 (aviso sobre el crédito Fonacot) entra al paquete de baja con `FONACOT_CREDITO` = Sí y `FONACOT_AVISO_PERSONA` = Sí, salvo fallecimiento | Registro 4.13 (15/11) |
| 8 | 1, 5.4 (nueva) | Cierre de la baja: la evidencia del pago (comprobante del Anexo 2 y CFDI) se captura una sola vez aquí y se envía al módulo 6, que la coteja | Registro 4.13 (15/11) |
| 9 | 5.5 (nueva) | Al registrar la baja: se cancelan las vacaciones autorizadas posteriores a `BAJA_FECHA` y se libera su cupo; si había aguinaldo validado sin pagar, se avisa al contador | Mapa, encargos 2 y 10 (15 y 17/11) |
| 10 | 7.7 | Regla 2 del acta de devolución alineada con el art. 46 vigente del RIT | Mapa, encargo 3 (15/11) |
| 11 | 9 | Dependencias actualizadas: módulos 5, 6, 8, 10 y 11; las variables F-2 vienen de Axia CYA | Registro 6 (15/11) |
| 12 (20/11) | 2.4 | El texto de la alerta de situación protegida es el del módulo de permisos y usa `SITUACION_PROTEGIDA_TIPO` | Mapa, encargo 1 (17/11) |
| 13 (20/11) | Todo el documento; 8.3 | `SALARIO_PERSONA` sustituye a `SALARIO_DIARIO` como base de cálculo y en las plantillas (convenio y recibo). Imprime el mismo dato; solo cambia el nombre | Mapa, diccionario único (18/11) |
| 14 (20/11) | 4.8 | Los renglones automáticos de Infonavit y Fonacot se precargan con el descuento del alta como sugerencia editable | Mapa, encargo 12 (18/11) |
| 15 (20/11) | 7.7 | Acta de devolución: el valor de reposición de cada bien se precarga de la carta responsiva | Mapa, encargo 13 (18/11) |
| 16 (20/11) | 7.1, 7.7, 8.2 | Acta de devolución: firma electrónica o autógrafa, según se haga la entrega (`DEV_FIRMA_FORMA`); por la Empresa, RH designado; testigos solo si la persona se niega | Mapa, encargo 14; registro 4.11 (18/11) |
| 17 (20/11) | 2.4, 8.1, 8.2 | El embarazo informado (`EMBARAZO_INFORMADO_FECHA`, del expediente) activa la alerta de situación protegida con doble confirmación, sin bloqueo | Decisión del usuario (20/11) |
| 18 (21/11) | 4.2, 8.2, 9 | «Otros devengados» precarga como «Sugerido» el tiempo extra, la prima dominical y los descansos y festivos laborados que el módulo 9 tenga pendientes a `BAJA_FECHA`; lo «por validar» solo genera aviso | Mapa, encargo 15 (20/11) |

Los cambios 12 a 17 se agregaron el 20/11/2026 y el 18 el 21/11/2026, cuando la 1.5 aún no se había cargado. Si ya se cargó, aplicar solo esos siete.

---

## 0. Convenciones

- Variables: `{{MAYÚSCULAS_CON_GUION_BAJO}}`. Se sustituyen por el dato; nunca se imprime la marca.
- Condiciones: `[SI condición] … [FIN SI]`. Si la condición es falsa, se omite todo el bloque. Las marcas nunca se imprimen.
- Condiciones anidadas: se permiten; cada `[SI]` cierra con su `[FIN SI]`.
- Términos fijos en los textos: «la Empresa» y «la Persona Trabajadora».
- Niveles de captura de cada variable:
  - **E** = configuración de la empresa.
  - **O** = organigrama o puesto.
  - **A** = alta de la Persona Trabajadora.
  - **V** = evento de baja (pantalla «Retirar colaborador»).
  - **S** = calculada por el sistema (no editable salvo que se indique).
  - **X** = tabla global que administra AEXIS.
- Montos: moneda MXN con dos decimales. Toda cantidad que se imprime en un documento contractual se imprime también en letra (`{{VAR_LETRA}}`).
- Fechas: se imprimen en formato largo («10 de noviembre de 2026»).
- **Días hábiles:** varios plazos se cuentan en días hábiles. Se necesita un calendario configurable de días inhábiles (fines de semana, días de descanso obligatorio y días que la empresa marque). El conteo empieza el día hábil siguiente al evento.
- Ningún texto fija cifras que cambian por reforma (salario mínimo, jornada, porcentajes legales). Esas cifras viven en tablas del sistema.
- **Formato de impresión:** todos los documentos del módulo (convenio, recibo, comunicados, constancias, acta, FON-1 y hoja interna) en Arial 12, incluidos títulos, tablas y bloques de firma. Los títulos van en negrita, del mismo tamaño. Única excepción: el ajuste del recibo para que quepa en una hoja (7.6). Tamaño de papel: carta. PDF con la impresión del navegador, sin encabezado ni pie del navegador. (Nota de Cerebro, 22/11/2026: rige la impresión del navegador; ver el registro, sección 3.)

---

## 1. Flujo de la pantalla «Retirar colaborador»

Objetivo: que RH cierre una baja con el mínimo de pasos. Solo son obligatorios el motivo, la fecha de baja y la forma de pago.

1. **Colaborador.** El sistema carga el expediente: contrato, puesto, salario y versión de condiciones de la persona (módulo 5), fechas, vacaciones y aguinaldo (módulo 11), carta responsiva, designación de beneficiarios, créditos, pensión alimenticia y eventos vigentes del módulo de permisos.
2. **Motivo** (`BAJA_MOTIVO`). Una sola lista (sección 2.1). Es un dato interno: decide el cálculo y los documentos de respaldo, pero **no se imprime** en el convenio ni en el recibo.
3. **Fecha de baja** (`BAJA_FECHA`). Con la fecha, el sistema revisa las situaciones protegidas (2.4) y la suspensión D4 vencida (2.2), y al guardar la baja aplica los efectos de 5.5.
4. **Datos del motivo.** Solo en fin del periodo y en vencimiento, y solo si se quiere el comunicado de respaldo (2.3). Todos opcionales.
5. **Cálculo.** Previsualización por concepto, otros devengados, prima de antigüedad, gratificación y escenario de negociación (sección 4).
6. **Deducciones y pago.** Otras deducciones (tabla dinámica, 4.8), forma de pago (`CONV_FORMA_PAGO`) y si es diferido (`CONV_PAGO_DIFERIDO`, con sus parcialidades).
7. **Documentos.** «¿Se entrega constancia de servicios?» (`CONSTANCIA_SERVICIOS`). El acta de devolución se genera sola si hay carta responsiva; FON-1, si aplica (7.10).
8. **Validación del contador** (`CALCULO_VALIDADO`) y generación. Sin validación solo se generan borradores con marca de agua «BORRADOR — CÁLCULO NO VALIDADO».
9. **Cierre y seguimiento.** Registrar el pago y su evidencia (5.4), subir los documentos firmados o cerrar el seguimiento (5.2).

---

## 2. Motivos de baja

### 2.1 Catálogo

No existe el motivo «Despido injustificado» ni «Despido sin causa». Una salida por decisión de la Empresa sin causa legal se registra como «Mutuo consentimiento»; la indemnización solo aparece en el escenario de negociación (4.6).

| `BAJA_MOTIVO` | Fundamento (interno) | Documento de respaldo que genera el sistema | Mensaje informativo |
| --- | --- | --- | --- |
| Voluntad de la Persona Trabajadora | Art. 53, fr. I LFT | Ninguno | — |
| Mutuo consentimiento | Art. 53, fr. I | Ninguno | — |
| Rescisión por causa imputable a la Persona Trabajadora | Art. 47 | Ninguno (el aviso es servicio aparte) | Mensaje de rescisión (2.2) |
| Rescisión por causa imputable a la Empresa | Arts. 51 y 52 | Ninguno | «Consulte a su asesor antes de firmar» |
| Fin del periodo de prueba o de capacitación inicial | Arts. 39-A, 39-B | Comunicado 7.4, solo si se cumplen los requisitos de 2.3 | Requisitos (2.3) |
| Vencimiento del plazo o terminación de la obra | Arts. 36, 37, 53, fr. III | Comunicado 7.5, solo si se cumplen los requisitos de 2.3 | Requisitos (2.3) |
| Incapacidad (riesgo no profesional) | Arts. 53, fr. IV, 54 | Ninguno (documento propio pendiente, prioridad C) | — |
| Fallecimiento | Arts. 53, fr. II, 115, 162, fr. V, 501 | Convenio de pago a beneficiarios (7.8) en lugar del convenio 7.2 | — |

En todos los motivos, salvo fallecimiento, se genera el mismo convenio (7.2), por mutuo consentimiento, y el recibo (7.6). **No se genera formato de renuncia.**

### 2.2 Mensajes informativos de rescisión (sin captura)

Al elegir «Rescisión por causa imputable a la Persona Trabajadora» se muestra:

> «El aviso de rescisión no se elabora en el sistema: es un servicio aparte. Si la Persona Trabajadora firma el convenio, el aviso no es necesario. Si no lo firma, el aviso debe entregarse en persona al separarla o comunicarse por medio del Tribunal dentro de los 5 días hábiles siguientes, y la rescisión debe hacerse dentro del mes siguiente a que la Empresa conoció la falta (arts. 47 y 517 LFT).»

**Suspensión por falta de documentos vencida (nuevo en 1.5).** Si la persona tiene un evento D4 del módulo de permisos cuyo `SUSP_LIMITE` ya pasó y no se ha reincorporado, al elegir cualquier motivo se muestra, sin bloquear:

> «La suspensión por falta de documentos venció el {{SUSP_LIMITE}}. Puede actualizarse la causa de rescisión de la fracción XIV Bis del artículo 47 de la Ley Federal del Trabajo. Consultoría decide y prepara el aviso de rescisión (servicio aparte). El sistema no termina la relación por sí mismo.»

### 2.3 Requisitos con opción de continuar

Los requisitos ya no bloquean la baja. Si falta alguno, el sistema muestra qué falta y dos botones: «Completar» y «Continuar sin requisitos».

| Motivo | Requisitos para generar el comunicado de respaldo |
| --- | --- |
| Fin del periodo | Evaluación final (`EVAL_FECHA`, `EVAL_RESUMEN`) con resultado no aprobatorio; F-2 firmado o constancia de solicitud (`F2_*`); en capacitación inicial, evidencia de la capacitación (`CAPACITACION_EVIDENCIA`); `BAJA_FECHA` igual al último día del periodo |
| Vencimiento | `CAUSA_TEMPORALIDAD` en el contrato; tipo de relación distinto de temporada |

Con «Continuar sin requisitos»:

- La baja sigue con el convenio (7.2) y el recibo (7.6). Solo **no** se genera el comunicado de respaldo.
- Mensaje fijo, una sola vez: «Sin estos requisitos, la terminación depende de que la Persona Trabajadora firme el convenio. Si no lo firma, la separación puede considerarse despido injustificado.»
- El sistema registra en automático el usuario y la fecha (`CANDADOS_OMITIDOS`). No pide justificación.

Bloqueos que se mantienen (no tienen opción de continuar):

| Validación | Efecto |
| --- | --- |
| Neto del finiquito negativo | Bloqueo |
| `BAJA_FECHA` anterior a `FECHA_INICIO` | Bloqueo |
| Versión final sin `CALCULO_VALIDADO` | Solo borrador con marca de agua |

### 2.4 Situaciones protegidas y comisión permanente (nueva en 1.5)

Ninguna de estas situaciones bloquea la baja. Exigen doble confirmación para que quede constancia de que la Empresa conocía la situación y decidió continuar.

**Situaciones protegidas.** El módulo de permisos envía `SITUACION_PROTEGIDA` = Sí mientras exista alguno de estos eventos a `BAJA_FECHA`: incapacidad C1 o C2 en curso, maternidad C3, lactancia B1, Declaración Especial de Ausencia D5 o licencia por hijo con cáncer B3. Con Sí:

1. Alerta crítica en la pantalla, antes del paso 4:

   > «Esta persona está en una situación que la ley protege ({{SITUACION_PROTEGIDA_TIPO}}). Darla de baja puede generar un reclamo. ¿Confirma que lo revisó con consultoría?»

   El texto es el de la especificación de permisos (sección 11). `SITUACION_PROTEGIDA_TIPO` lo envía ese módulo: Incapacidad en curso, Maternidad, Lactancia, Declaración Especial de Ausencia o Licencia por hijo con cáncer.

2. Si RH confirma, segunda confirmación: «Confirmo que la Empresa conoce esta situación y decide continuar con la baja.»
3. El sistema registra usuario, fecha y hora en `BAJA_CONFIRMACION_PROTEGIDA`. Sin las dos confirmaciones no se avanza al paso 4; «Cancelar» deja la baja guardada como borrador.
4. Si hay varias situaciones, la alerta las lista todas, separadas por comas, y basta una doble confirmación.
5. **Embarazo informado (decisión del usuario, 20/11/2026).** Si el expediente tiene `EMBARAZO_INFORMADO_FECHA` y todavía no hay evento C3, se muestra la misma alerta con «Embarazo informado» como situación, con la misma doble confirmación y el mismo registro en `BAJA_CONFIRMACION_PROTEGIDA`. Solo alerta: nunca bloquea.
6. La calidad de representante obrero en una comisión no es situación protegida para la baja (decisión del usuario, 20/11/2026): no genera alerta.

**Comisión permanente vigente (B4).** Misma mecánica, con este texto:

> «Esta persona tiene una licencia por comisión permanente con derecho a regresar a su puesto hasta el {{COMISION_FECHA_LIMITE}}. Darla de baja puede generar un reclamo. ¿Confirma la baja?»

Registra usuario, fecha y hora en `BAJA_CONFIRMACION_B4`.

Reglas comunes:

- Las confirmaciones nunca se imprimen en ningún documento; quedan en la bitácora del expediente.
- Si cambia `BAJA_FECHA` después de confirmar, el sistema revisa de nuevo y, si la situación sigue, pide otra vez las dos confirmaciones.
- Si la situación aparece después de validar el cálculo (por ejemplo, se registra tarde una incapacidad), se muestra la alerta en el seguimiento (5.2) y se pide la doble confirmación; los documentos ya generados no cambian.

---

## 3. Paquete documental por motivo

| Motivo | Convenio 7.2 | Recibo 7.6 | Respaldo | Acta de devolución 7.7 | Constancia de servicios 7.9 | FON-1 (7.10) |
| --- | --- | --- | --- | --- | --- | --- |
| Voluntad | Sí | Sí | — | Si `CARTA_RESPONSIVA` = Sí | Si `CONSTANCIA_SERVICIOS` = Sí | Si `FONACOT_CREDITO` = Sí y `FONACOT_AVISO_PERSONA` = Sí |
| Mutuo consentimiento | Sí | Sí | — | Ídem | Ídem | Ídem |
| Rescisión art. 47 | Sí | Sí | — (aviso: servicio aparte) | Ídem | Ídem | Ídem |
| Rescisión art. 51 | Sí | Sí | — | Ídem | Ídem | Ídem |
| Fin del periodo | Sí | Sí | Comunicado 7.4 si cumple 2.3 | Ídem | Ídem | Ídem |
| Vencimiento de plazo u obra | Sí | Sí | Comunicado 7.5 si cumple 2.3 | Ídem | Ídem | Ídem |
| Incapacidad | Sí | Sí | — | Ídem | Ídem | Ídem |
| Fallecimiento | No: convenio de beneficiarios 7.8 | Sí, anexo del 7.8 | — | No (requerimiento de devolución a beneficiarios) | No | No (alerta de aviso de defunción, 5.1) |

- La «constancia de salida» del kit de contratación es el acta de entrega de bienes; no es la constancia de servicios de 7.9.

---

## 4. Motor de precálculo

### 4.1 Principios

- El precálculo es **neto estimado** (decisión del usuario, 10/11/2026): el sistema calcula percepciones brutas, ISR, subsidio para el empleo, cuotas obreras del IMSS y demás deducciones (4.7).
- Toda presentación del neto lleva la leyenda «ISR y cuotas estimados; los definitivos constan en el CFDI de nómina».
- El precálculo es una **previsualización**: el sistema propone cada monto, quien calcula puede sustituirlo y el contador valida (secciones 4.4 y 4.5). El cálculo de impuestos también puede sustituirse con cifra propia.
- **Condiciones de la persona (1.5).** El salario, el puesto, la jornada y las prestaciones son los de la versión de condiciones de la persona vigente a `BAJA_FECHA` (módulo 5), nunca los del catálogo. Si la persona no firmó un convenio modificatorio, conserva su versión anterior.

### 4.2 Conceptos que proceden por motivo

Leyenda: **Sí** = se calcula siempre · **Opcional** = casilla `PA_INCLUIR` editable · **Fija** = casilla bloqueada en Sí · **No** = no se calcula · **Info** = solo informativo.

| Concepto | Voluntad | Mutuo consentimiento | Rescisión art. 47 | Rescisión art. 51 | Fin del periodo | Vencimiento plazo u obra | Fallecimiento |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Salarios devengados y otros devengados | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| Aguinaldo proporcional (4.9) | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| Vacaciones pendientes y proporcionales (4.9) | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| Prima vacacional | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| Prestaciones superiores devengadas (por puesto) | Sí | Sí | Sí | Sí | Sí | Sí | Sí |
| PTU pendiente | Info | Info | Info | Info | Info | Info | Info |
| Prima de antigüedad | Fija con 15 años o más; Opcional con menos | Opcional | Fija | Fija | Opcional | Opcional | Fija (sin requisito de antigüedad) |
| Indemnización art. 50 | No | Escenario de negociación | Solo escenario de riesgo | Sí, obligatoria | No | No | No |
| Indemnización art. 54 | — | — | — | — | — | — | — (con motivo Incapacidad: Sí) |

Reglas:

- `PA_INCLUIR` registra quién la marcó o desmarcó y cuándo.
- **PTU pendiente:** no se suma al finiquito; se paga en la fecha de reparto aunque la persona ya no trabaje. El convenio deja a salvo el derecho (art. 987 LFT). Si el reparto ya se determinó y no se pagó, se suma como concepto «PTU determinada no pagada».
- **Otros devengados y prestaciones** (`OTROS_DEVENGADOS`), pantalla:
  - Se muestra **un** renglón vacío por omisión.
  - Botón «+ Agregar concepto» debajo de la tabla: agrega un renglón cada vez. Sin límite.
  - Cada renglón tiene un botón para quitarlo.
  - Columnas: Tipo (Tiempo extra / Prima dominical / Descanso laborado / Festivo laborado / Prestación del puesto / Otro), Concepto, Base, Cantidad, Importe, Soporte.
  - Soporte **opcional** (texto). Un renglón vacío no se imprime.
- **Precarga del tiempo extra pendiente (21/11/2026, del módulo 9).** Al llegar a este paso, el sistema agrega un renglón por cada concepto que el módulo 9 tenga pendiente a `BAJA_FECHA`: lo validado y no exportado a nómina y los ajustes pendientes (sección 8.3 de la especificación del módulo 9).
  - Tipo: Tiempo extra, Prima dominical, Descanso laborado o Festivo laborado, según lo envíe el módulo 9. Cantidad: horas o días. Importe: el bruto estimado del módulo 9 (`SALARIO_PERSONA` y tasas de la tabla del sistema). Soporte: periodo y folio del módulo 9.
  - El importe se marca «Sugerido» hasta que RH lo confirma, lo cambia o quita el renglón (misma mecánica de 4.8).
  - Lo que el módulo 9 tenga «por validar» (tiempo extra sin orden previa, PN-09) no se precarga. Aviso, sin bloqueo: «Hay tiempo extra por validar en el análisis de jornada. Resuélvalo antes de validar el cálculo: el tiempo trabajado sin orden se paga.»
  - Sin módulo 9 (la empresa no lo usa u opera en modo «Solo archivo»), no hay precarga y RH captura a mano.

### 4.3 Fórmulas

| Concepto | Fórmula | Base |
| --- | --- | --- |
| Antigüedad | Años, meses y días de `FECHA_INICIO` a `BAJA_FECHA`, incluido el periodo de prueba o capacitación | — |
| Salario diario (`SALARIO_PERSONA`) | Salario diario de la versión de condiciones de la persona vigente a `BAJA_FECHA` (módulo 5). Ya es diario: no se divide entre los días de la periodicidad. En ascenso temporal o con periodo de adaptación, el del puesto que ocupa | — |
| Aguinaldo proporcional | Según 4.9: `AGUINALDO_DIAS` × días computables (`AGUINALDO_COMPUTA`) de `AGUINALDO_PERIODO_INICIO` a `BAJA_FECHA` ÷ 365. Cero si el aguinaldo del año ya se pagó | `SALARIO_PERSONA` |
| Vacaciones pendientes | Suma de los saldos de los periodos Vigentes y Fuera de plazo del módulo 11 (4.9) | `SALARIO_PERSONA` |
| Vacaciones proporcionales | Días del periodo siguiente × días transcurridos desde el último aniversario (o desde `FECHA_INICIO`, si no ha cumplido el año) ÷ 365 (módulo 11, sección 11) | `SALARIO_PERSONA` |
| Prima vacacional | Importe total de vacaciones × `PRIMA_VACACIONAL_PCT` | — |
| Prima de antigüedad | 12 × (años completos + fracción del año en curso) × `SALARIO_TOPADO` | `SALARIO_TOPADO` |
| Salario topado | Menor entre `SALARIO_PERSONA` y 2 × salario mínimo del área geográfica del centro de trabajo. Si el centro abarca varias áreas: 2 × promedio de los mínimos | Tabla de salarios mínimos por año y zona |
| Salario diario integrado (`SDI`) | Cuota diaria + parte proporcional de prestaciones. Si el salario es variable: promedio de los 30 días efectivamente trabajados antes de `BAJA_FECHA` (si hubo aumento en ese lapso, promedio desde el aumento) | — |
| Indemnización constitucional | 90 × `SDI` | `SDI` |
| 20 días por año (art. 50, fr. II) | 20 × años de servicio (incluida la fracción) × `SDI` | `SDI` |
| Art. 50, fr. I (relación por tiempo determinado) | Menos de un año: salarios de la mitad del tiempo servido. Más de un año: 6 meses por el primero + 20 días por cada año siguiente | `SDI` |
| Art. 54 | 30 × `SDI` + 12 días por año × `SALARIO_TOPADO` | — |

La tabla de salarios mínimos es configurable por año y zona (general y Zona Libre de la Frontera Norte). Nunca se escribe un monto en el texto de un documento.

### 4.4 Previsualización, cifras propias y umbrales

1. **Previsualización.** El sistema muestra cada concepto con base, cantidad (días u horas) e importe calculado.
2. **Cifras propias** (`CIFRA_PROPIA`). Quien calcula puede sustituir el importe de cualquier concepto. Se guarda: cifra calculada, cifra propia, motivo (obligatorio), usuario y fecha. El documento imprime la cifra vigente.
3. **Umbrales de verificación.** Se marca el concepto para revisión (no se bloquea) si:
   - la cifra propia difiere de la calculada más que `UMBRAL_DESVIACION_PCT` (por omisión 0: toda diferencia se marca); o
   - el importe del concepto rebasa su monto de alerta en `UMBRALES_CONCEPTO`.
4. **Bloqueo único:** neto negativo.

### 4.5 Validación del contador

- Ningún convenio ni recibo se genera en versión final sin `CALCULO_VALIDADO` = Sí, con `CONTADOR_NOMBRE` y `VALIDACION_FECHA`.
- Cualquier cambio posterior en un monto revierte la validación a No.
- Sin validación, los documentos se generan como borrador con marca de agua.

### 4.6 Escenario de negociación

Se muestra en pantalla y en una hoja interna imprimible. **Nunca** se imprime en el convenio, los comunicados ni el recibo.

Leyenda fija de la hoja: «Escenario interno para la toma de decisiones. No constituye reconocimiento de adeudo ni de despido».

| Capa | Contenido | Cuándo se muestra |
| --- | --- | --- |
| 1. Finiquito | Conceptos de 4.2 que proceden por el motivo | Siempre |
| 2. Indemnización constitucional | 90 × `SDI` | Mutuo consentimiento; rescisión art. 47 (como riesgo); fin del periodo o vencimiento con requisitos omitidos |
| 3. Indemnización ampliada | 20 días por año, o art. 50, fr. I en tiempo determinado | Solo si se actualiza un supuesto del art. 49 o hay rescisión por la Persona Trabajadora |
| Riesgo de juicio (informativo) | Salarios vencidos hasta 12 meses; después, intereses de 2% mensual sobre 15 meses de salario | Mismos casos que la capa 2 |

El usuario puede capturar un monto adicional pactado (`CONV_GRATIFICACION`); el sistema muestra qué porcentaje representa de las capas 2 y 3. En los documentos, el excedente sobre el finiquito se denomina «gratificación por terminación», nunca «indemnización», salvo en la rescisión del art. 51, donde la indemnización legal aparece como concepto del recibo (`INDEMNIZACION_MONTO`).

### 4.7 Cálculo de impuestos y cuotas (neto estimado)

Todos los valores numéricos (UMA, tarifas, subsidio, salarios mínimos, cuotas) viven en tablas de parámetros con fecha de vigencia (5.3). El código no contiene cifras. Cada cálculo guarda el identificador de la versión de parámetros que usó.

**Paso 1. Clasificar las percepciones**

| Grupo | Conceptos | Tratamiento |
| --- | --- | --- |
| Ordinarias | Salarios devengados, otros devengados, vacaciones, prima vacacional, aguinaldo, prestaciones superiores, PTU determinada no pagada | Exenciones del art. 93 LISR y tarifa mensual del art. 96 |
| Por separación | Prima de antigüedad, indemnizaciones (art. 50 o 54), gratificación por terminación | Exención del art. 93, fr. XIII y tasa del art. 96 (pagos del art. 95) |

**Paso 2. Exenciones** (parámetro `REF_EXENCION`: unidad de referencia, por omisión UMA; el contador puede cambiarla a salario mínimo)

| Concepto | Exento | Fundamento |
| --- | --- | --- |
| Aguinaldo | Hasta 30 veces la unidad de referencia diaria, por año calendario | Art. 93, fr. XIV LISR |
| Prima vacacional | Hasta 15 veces la unidad de referencia diaria | Art. 93, fr. XIV |
| PTU | Hasta 15 veces la unidad de referencia diaria | Art. 93, fr. XIV |
| Prima dominical | Hasta 1 vez la unidad de referencia diaria por cada domingo laborado | Art. 93, fr. XIV |
| Tiempo extra y descanso laborado sin descanso sustituto | Persona con salario mínimo: exento hasta el límite legal. Demás: 50 % de lo pagado dentro del límite legal, sin exceder 5 veces la unidad de referencia por semana de servicios. Lo que rebasa el límite legal está gravado al 100 % | Art. 93, fr. I |
| Prestaciones distintas del salario de quien gana el salario mínimo | Exentas si se calculan sobre el salario mínimo y no exceden los mínimos legales | Art. 93, fr. I |
| Pagos por separación | Hasta 90 veces la unidad de referencia por cada año de servicio. Los años son los mismos usados para calcular los conceptos; la fracción mayor de 6 meses cuenta como año completo | Art. 93, fr. XIII |

Nota: el art. 93 habla de «salario mínimo general del área geográfica». Cuando funciona como unidad de medida (topes de exención), se usa la UMA por la desindexación del salario mínimo; por eso `REF_EXENCION` vale UMA por omisión. Cuando define a quién aplica la regla («trabajadores del salario mínimo»), se compara con el salario mínimo real de la zona del centro de trabajo.

Las exenciones de aguinaldo, prima vacacional y PTU se reducen por lo ya exento en el mismo año calendario, si el dato existe en nómina (`EXENTO_ACUMULADO_ANIO`); si no existe, el sistema calcula como si no hubiera pagos previos y lo indica al contador.

**Paso 3. ISR de las percepciones ordinarias**

1. Base gravable ordinaria = percepciones ordinarias − exentos.
2. ISR = tarifa mensual del art. 96 vigente a `BAJA_FECHA` (tabla del Anexo 8 de la RMF del año), aplicada a la base gravable.
   - Si `SALARIO_PERSONA` es igual al salario mínimo del área geográfica del centro de trabajo, los salarios devengados no causan retención (art. 96, primer párrafo) y se restan de la base. Las demás percepciones gravadas sí se gravan. Mensaje al contador: «Persona con salario mínimo: no se retuvo ISR sobre el salario».
3. Subsidio para el empleo: se aplica según el decreto vigente (porcentaje de la UMA mensual y límite de ingresos de la tabla de parámetros), proporcional a los días del periodo (monto mensual ÷ 30.4 × días).
4. ISR ordinario = ISR − subsidio (no menor que cero).

**Paso 4. ISR de los pagos por separación**

1. Base gravable de separación = pagos por separación − exento del paso 2.
2. Último sueldo mensual ordinario (`USMO`): por omisión, `SALARIO_PERSONA` × 30. Si el salario es variable o hubo cambios, el contador lo captura.
3. Tasa = ISR del USMO con la tarifa mensual ÷ USMO.
4. ISR de separación = base gravable de separación × tasa.
   - La tasa se aplica a la parte gravada, no al total: lo exento por la fr. XIII del art. 93 no causa impuesto.
5. Si el total de los pagos por separación (antes de exenciones) es menor que el USMO, no se usa la tasa: la base gravable de separación se suma a la base gravable ordinaria y se aplica la tarifa mensual a la suma (arts. 95, fr. I y 96 LISR). El ISR de separación es la diferencia entre el ISR de la suma y el ISR del paso 3, inciso 2 (antes del subsidio), para que el recibo lo muestre en su renglón.
6. Mensaje al contador: «Los pagos por separación se timbran en un CFDI aparte (régimen de indemnización o separación).»
7. Aviso de cálculo anual (no bloquea): si `BAJA_FECHA` es del 1 al 31 de diciembre, la persona ingresó antes del 1 de enero de ese año y sus ingresos por salarios del año no rebasan el tope del Anexo A, el sistema muestra: «La Empresa debe hacer el cálculo anual de esta persona (art. 97 LISR). El ISR del finiquito es estimado y puede cambiar con el ajuste anual.» Si la baja es antes del 1 de diciembre, no hay cálculo anual a cargo de la Empresa.

**Paso 5. Cuotas obreras del IMSS**

Sobre los salarios devengados del último periodo (días de `DEV_DIAS`), con el SBC vigente y las cuotas obreras de la tabla de parámetros. No se calculan cuotas sobre vacaciones pagadas a la terminación, aguinaldo, prima de antigüedad ni pagos por separación, salvo que el contador lo indique (`IMSS_CONCEPTOS_GRAVADOS`, editable).

**Paso 6. Neto estimado**

Neto = percepciones brutas − ISR ordinario − ISR de separación − cuotas obreras − créditos (Infonavit, Fonacot) − pensión alimenticia − descuentos autorizados.

**Reglas**

- El contador puede sustituir cualquier resultado (ISR, subsidio, cuotas, USMO) con cifra propia (4.4).
- Sin `CALCULO_VALIDADO` no hay versión final (4.5).
- **Parámetros iniciales.** Al instalar el módulo se cargan como aprobados los parámetros 2026 del Anexo A. Sin ellos el cálculo no funciona.
- Si a `BAJA_FECHA` no hay parámetros vigentes para el año, el sistema calcula con los últimos aprobados y muestra: «Parámetros de [año] pendientes de aprobación; el cálculo puede variar.»
- Si no existe ningún parámetro aprobado del que dependa un concepto, ese concepto muestra «No calculado» (nunca $0.00), el resultado se rotula «Neto sin impuestos (incompleto)» y no se permite validar el cálculo hasta cargar el parámetro.
- Un ISR o una cuota en $0.00 solo se muestra cuando el cálculo realmente da cero (por ejemplo, ingreso exento).
- Caso de prueba: ver Anexo A.3.

### 4.8 Otras deducciones (tabla dinámica)

Misma mecánica que «Otros devengados y prestaciones» (4.2):

- Un renglón vacío por omisión, botón «+ Agregar deducción» debajo de la tabla y botón para quitar cada renglón. Sin límite. Un renglón vacío no se imprime.
- Columnas: Tipo, Concepto, Importe, Soporte (opcional).
- Tipos: Crédito Infonavit · Crédito Fonacot · Pensión alimenticia · Pérdida o daño · Anticipo o préstamo de la Empresa · Otra deducción autorizada.
- Si el alta tiene `INFONAVIT_CREDITO`, `FONACOT_CREDITO` o `PENSION_ALIMENTICIA` = Sí, el sistema agrega en automático el renglón de ese tipo para que RH lo revise. RH puede quitarlo.
- **Precarga como sugerencia editable (20/11).** El importe propuesto se marca «Sugerido» hasta que RH lo confirma o lo cambia:
  - Infonavit: con `INFONAVIT_DESCUENTO_TIPO` = Cuota fija, `INFONAVIT_DESCUENTO_VALOR` proporcional a los días del último periodo de salario pagado. Con Porcentaje o Veces salario mínimo, RH captura el importe a mano; la pantalla muestra el tipo y el valor del alta como referencia (decisión del usuario, 20/11/2026).
  - Fonacot: `FONACOT_DESCUENTO_MONTO` (importe mensual del alta) proporcional a los días del último periodo de salario pagado. Rige además la regla de Fonacot de abajo: si la cédula del módulo 8 tiene la retención del periodo, se precarga esa y no la del alta.
  - Pensión alimenticia: el importe queda vacío; RH lo captura conforme a la resolución.
  - Sin dato en el alta, el importe queda vacío con el aviso «Descuento pendiente de capturar».
- **Crédito Fonacot (1.5).** El importe del renglón es `FONACOT_RETENCION_FINIQUITO`: solo la amortización que la cédula asigna al último periodo de salario que se paga en el finiquito, proporcional a los días de ese periodo. Nunca el saldo del crédito ni importes de otros conceptos del finiquito. Si el importe capturado supera la retención mensual de la cédula, aviso sin bloqueo: «Solo se retiene la amortización del último periodo; el saldo lo paga la Persona Trabajadora directamente al Instituto». La retención se entera en la cédula siguiente con la incidencia de baja (módulo 8).
- **Fallecimiento (1.5).** No se agrega el renglón automático de Fonacot en el pago a beneficiarios (7.8); se activa la alerta del aviso de defunción (5.1).
- Avisos (no bloquean): «Pérdida o daño» sin soporte → «Solo procede con expediente concluido (reconocimiento en FD-5 o determinación en FD-3)»; la suma de «Pérdida o daño», «Anticipo o préstamo» y «Otra» mayor que el límite del art. 110, fr. I LFT → «Rebasa el límite legal de descuento».
- Bloqueo: neto negativo.
- Las deducciones se restan en el paso 6 de 4.7 y se imprimen en el recibo, una fila por renglón, con su concepto.

### 4.9 Vacaciones y aguinaldo desde el módulo 11 (nueva en 1.5)

El módulo 4 no calcula saldos de vacaciones ni días de aguinaldo: los lee del módulo de vacaciones y aguinaldo (su sección 11) a la fecha de `BAJA_FECHA`.

| Dato | Qué toma el módulo 4 | Se suma al finiquito |
| --- | --- | --- |
| Periodos Vigentes o Fuera de plazo | Saldo de días de cada periodo, salario base (`SALARIO_PERSONA` vigente a la baja) y prima | Sí, en «Vacaciones de periodos cumplidos no disfrutados» |
| Proporcional del año en curso | Días del periodo siguiente × días transcurridos desde el último aniversario (o desde `FECHA_INICIO`) ÷ 365 | Sí, en «Vacaciones proporcionales del año en curso» |
| Periodos Prescritos | Días y fecha de prescripción | **No.** Solo se muestran en pantalla, como dato informativo para consultoría; no se imprimen |
| Aguinaldo, baja antes del pago del año | Proporcional de `AGUINALDO_PERIODO_INICIO` a `BAJA_FECHA`, con la tabla de días computables `AGUINALDO_COMPUTA` | Sí |
| Aguinaldo, baja después del pago del año | — | No: el finiquito no incluye el aguinaldo de ese año ni descuenta lo ya pagado |

- Si el módulo 11 no tiene datos de la persona (expediente anterior a su uso), RH captura los saldos con cifra propia (4.4) y motivo.
- La prima vacacional se calcula sobre el importe total de vacaciones (pendientes y proporcionales) con `PRIMA_VACACIONAL_PCT`.

---

## 5. Alertas y cierre

### 5.1 Alertas de la baja

| Alerta | Se activa | Plazo | Fundamento |
| --- | --- | --- | --- |
| Baja ante el IMSS | En toda baja | No más de 5 días hábiles desde `BAJA_FECHA` | Art. 15, fr. I LSS |
| Aviso al juzgado y a los acreedores alimentarios | Si la persona tiene pensión alimenticia registrada | 5 días hábiles siguientes a la terminación | Art. 110, fr. V LFT |
| Constancia de servicios | Si `CONSTANCIA_SERVICIOS` = Sí, o si la Persona Trabajadora la solicita después | 3 días | Art. 132, fr. VIII LFT |
| Baja ante Fonacot | Persona con `FONACOT_CREDITO` = Sí, salvo fallecimiento | `FONACOT_AVISO_DIAS` días hábiles desde `BAJA_FECHA` (5 por omisión, de `FONACOT_PLAZOS`) | Convenio de afiliación con el Instituto, cláusula Quinta (plazo contractual, no legal). Es la misma incidencia de baja del módulo 8: se cierra una sola vez |
| Aviso de defunción a Fonacot (1.5) | Fallecimiento de una persona con `FONACOT_CREDITO` = Sí | 15 días hábiles, con el acta de defunción | Convenio, cláusula Séptima |
| Suspensión de descuentos Infonavit | Persona con crédito Infonavit | Configurable (`INFONAVIT_AVISO_DIAS`) | Pendiente de verificar |
| Cierre de accesos | Toda baja con accesos registrados | `BAJA_FECHA` + 1 día hábil | Política interna |
| Vencimiento de contrato | Contratos por tiempo determinado | 15 días naturales antes de `FECHA_TERMINO`; contador de renovaciones con alerta desde la segunda | Política interna |
| Entrega del comunicado de vencimiento | Contratos por tiempo determinado | `VENC_AVISO_DIAS` hábiles antes del vencimiento (por omisión 5) | Política interna |
| Supuesto del art. 49 | Antigüedad < 1 año, confianza, eventual, hogar, plataformas o contacto directo y permanente | Inmediata, en el escenario de negociación | Art. 49 LFT |

Eliminadas respecto de la 1.1: aviso de rescisión por el Tribunal y prescripción para rescindir (la información de rescisión pasa al mensaje fijo de 2.2). Las situaciones protegidas no son alertas de plazo: se atienden en 2.4.

### 5.2 Seguimiento de baja sin firma

Se activa en toda baja en `BAJA_FECHA` y se repite hasta que ocurra una de dos cosas:

- se suben los documentos firmados (`BAJA_FIRMA_EVIDENCIA`); o
- RH oprime «Cerrar seguimiento» (`BAJA_SEGUIMIENTO_CERRADO`), con nota opcional.

El sistema no registra si se contrató el paraprocesal ni su acuse.

| Día hábil desde `BAJA_FECHA` | Nivel | Mensaje |
| --- | --- | --- |
| 0 | Informativa | «Baja sin documentos firmados. Suba la firma o, si la Persona Trabajadora no firmará, considere el procedimiento paraprocesal (servicio aparte).» |
| 2 | Preventiva | Mensaje por motivo (tabla siguiente) |
| 4 | Crítica | Mensaje por motivo |
| 5 y después, cada `ALERTA_BAJA_INTERVALO` días hábiles (por omisión 5) | Crítica, escalada a consultoría | Mensaje por motivo |

| Motivo | Mensaje por motivo |
| --- | --- |
| Mutuo consentimiento | «Sin firma, la relación de trabajo sigue vigente.» |
| Voluntad | «Sin firma ni escrito de la Persona Trabajadora no hay prueba de la salida voluntaria. Documente sus inasistencias.» |
| Rescisión art. 47 | «Sin firma, la rescisión depende del aviso (servicio aparte). El plazo para comunicarlo por el Tribunal vence el día hábil 5.» |
| Fin del periodo / Vencimiento | «Entregue el comunicado de respaldo con constancia de negativa ante dos testigos.» Si no se generó comunicado: mismo mensaje que mutuo consentimiento |
| Rescisión art. 51 / Incapacidad | «Riesgo de baja pendiente. Consulte a su asesor.» |

Reglas:

1. **El finiquito nunca se retiene por falta de firma.** Se paga en su fecha por transferencia a la cuenta de nómina; el CFDI es la prueba.
2. La secuencia es independiente de las alertas del IMSS, de Fonacot y de pensión alimenticia.

### 5.3 Alerta de actualización de parámetros

Los parámetros son globales (los administra AEXIS, no cada cliente) y se guardan como versiones con fecha de vigencia. Ningún valor nuevo se aplica sin aprobación humana.

| Parámetro | Fuente oficial que se vigila | Cuándo cambia normalmente |
| --- | --- | --- |
| UMA (diaria, mensual, anual) | INEGI y DOF | Publicación en enero; vigencia desde el 1 de febrero |
| Tarifas del ISR (art. 96: mensual, semanal, decenal, quincenal) | Anexo 8 de la Resolución Miscelánea Fiscal (DOF) | Diciembre, para el año siguiente |
| Subsidio para el empleo (porcentaje de la UMA mensual, límite de ingresos) | Decreto en el DOF | Diciembre o enero; puede traer reglas de transición |
| Salarios mínimos (general y Zona Libre de la Frontera Norte) | Resolución de la CONASAMI en el DOF | Diciembre, para el 1 de enero |
| Cuotas obreras del IMSS y tope del SBC | Ley del Seguro Social y DOF | Por reforma |
| Exenciones del art. 93 LISR | DOF (reformas a la LISR) | Por reforma |

**Funcionamiento**

1. **Monitor.** Revisa periódicamente las fuentes de la tabla (`PARAM_MONITOR_FRECUENCIA`, por omisión diario en diciembre, enero y febrero, y semanal el resto del año). Si detecta una publicación nueva, crea una alerta.
2. **Alerta.** Llega al administrador de AEXIS: «Se publicó [parámetro] en [fuente] el [fecha]. Revise y cargue los valores nuevos.» Incluye el enlace a la publicación.
3. **Carga y aprobación.** El administrador captura los valores y su fecha de vigencia, y los aprueba (`PARAM_APROBADO_POR`, `PARAM_APROBADO_FECHA`). Una segunda persona puede revisar antes de activar (opcional, `PARAM_DOBLE_REVISION`).
4. **Activación.** El parámetro aprobado se aplica a los cálculos con `BAJA_FECHA` dentro de su vigencia. Los cálculos ya validados no cambian.
5. **Aviso a clientes.** Si hay bajas en proceso (sin validar) afectadas por el cambio, el sistema avisa a su RH y a su contador: «Cambió [parámetro]. Recalcule y valide de nuevo.»
6. **Recordatorio de calendario.** Aunque el monitor no detecte nada, el sistema alerta al administrador el 2 de enero y el 2 de febrero si no se han cargado la tarifa, el subsidio, los salarios mínimos o la UMA del año.

### 5.4 Cierre de la baja: registro del pago (nueva en 1.5)

La evidencia del pago del finiquito se captura **una sola vez**, aquí, y el módulo 6 la recibe, la coteja y la guarda. El módulo 6 no tiene captura propia para el finiquito.

1. Al validarse el cálculo (`CALCULO_VALIDADO` = Sí), el módulo 6 crea la obligación «Finiquito» por `TOTAL_NETO`; con pago diferido, una obligación por cada parcialidad de `CONV_PARCIALIDADES`.
2. En la pantalla de cierre, RH registra por cada pago: fecha, medio (el de `CONV_FORMA_PAGO`) e importe, y carga la evidencia:
   - comprobante de la transferencia (el mismo archivo es el Anexo 2 del convenio, si `CONV_FORMA_PAGO` = Transferencia y `CONV_PAGO_DIFERIDO` = No); y
   - CFDI de nómina en XML (o el PDF o el UUID, que el módulo 6 admite con alerta).
3. El sistema envía el registro y los archivos al módulo 6 (`PAGO_REGISTRO`, `PAGO_EVIDENCIA`), que aplica su cotejo (especificación de los módulos 6 y 8, sección 4.3) y fija el estado del pago.
4. Lo que el módulo 4 exige para cerrar la baja no cambia: el registro del pago no es requisito para cerrar el seguimiento de 5.2, y el estado del módulo 6 no bloquea nada aquí. Si falta la evidencia, las alertas son las del módulo 6.
5. Con pago diferido, cada parcialidad se registra desde el expediente de la baja, cuando se paga.

### 5.5 Efectos de la baja en otros módulos (nueva en 1.5)

Al guardar la baja con `BAJA_FECHA`, el sistema avisa a los demás módulos:

| Módulo | Efecto |
| --- | --- |
| Vacaciones y aguinaldo (11) | Cancela los bloques de vacaciones Autorizados posteriores a `BAJA_FECHA` y las solicitudes pendientes, y libera su cupo. Si la persona tenía `AGUINALDO_VALIDADO` sin pago, avisa al contador que sale del cálculo anual y, si ya se había exportado a nómina, le pide excluirla de la dispersión |
| Validación de pagos (6) | Si existía la obligación anual de aguinaldo sin pago, la cancela con motivo «Pago en finiquito»; pasa a «Pagada en finiquito» cuando el finiquito tenga evidencia de pago |
| Fonacot (8) | Abre la incidencia de baja (o el aviso de defunción) de 5.1 |

Si la baja se anula antes de cerrarse, los bloques de vacaciones cancelados no se restauran solos: el sistema avisa a RH para que la persona los solicite de nuevo.

---

## 6. Servicios que se contratan aparte — ELIMINADA

El sistema ya no muestra recomendaciones de servicios aparte (ratificación, paraprocesal). Se conserva solo el mensaje informativo de rescisión (2.2) y los mensajes del seguimiento (5.2).

---

## 7. Plantillas

### 7.1 Reglas comunes

- Los datos de la Empresa y de la Persona Trabajadora se toman del diccionario del contrato y del kit (prefijo `PATRON_` por compatibilidad).
- **Constancia de negativa (hoja aparte).** No se imprime en ningún documento. En la pantalla de seguimiento hay un botón «Generar constancia de negativa», que imprime esta hoja solo cuando la Persona Trabajadora se niega a firmar un comunicado:

```text
CONSTANCIA DE NEGATIVA A FIRMAR

Siendo las ____ horas del ___ de ________ de ____, en ______________________, se entregó personalmente a {{TRAB_NOMBRE}} el documento denominado {{DOCUMENTO_NEGADO}}, quien lo leyó y se negó a firmarlo de recibido.

Nombre y firma de quien entrega: ______________________
Testigo: ______________________ (nombre y firma)     Testigo: ______________________ (nombre y firma)
```

- Firma autógrafa obligatoria en el convenio (7.2), en el recibo de finiquito (art. 101 LFT) y en el recibido de FON-1, aunque `FIRMA_MODALIDAD` = Electrónica. Ninguno lleva cláusula de firma electrónica.
- El acta de devolución (7.7) es la excepción del paquete de baja: admite firma electrónica o autógrafa, según se haga la entrega.
- El convenio (7.2) se firma al margen de cada hoja y al calce, con huella digital de la Persona Trabajadora.

### 7.2 Convenio de terminación de la relación de trabajo por mutuo consentimiento y finiquito

Se genera en toda baja, salvo fallecimiento. El motivo interno (`BAJA_MOTIVO`) no se imprime. El recibo (7.6) es su Anexo 1. Sin cambios en la 1.5.

```text
CONVENIO DE TERMINACIÓN DE LA RELACIÓN DE TRABAJO POR MUTUO CONSENTIMIENTO Y FINIQUITO que celebran, por una parte, {{PATRON_RAZON_SOCIAL}}, a quien en lo sucesivo se denominará «la Empresa», representada en este acto por {{REP_NOMBRE}}, en su carácter de {{REP_CARACTER}}, y, por la otra, {{TRAB_NOMBRE}}, por su propio derecho, a quien en lo sucesivo se denominará «la Persona Trabajadora», y a quienes en conjunto se denominará «las Partes», al tenor de los antecedentes, declaraciones y cláusulas siguientes:

ANTECEDENTES

PRIMERO. Relación de trabajo. La Persona Trabajadora ingresó a prestar sus servicios personales y subordinados a la Empresa el {{FECHA_INICIO}}, en una relación de trabajo {{TIPO_RELACION_TEXTO}}.

SEGUNDO. Condiciones de trabajo. A la fecha de este convenio, las condiciones de trabajo de la Persona Trabajadora son las siguientes:

| Puesto                     | {{PUESTO}}            |
| Centro de trabajo          | {{CT_DOMICILIO}}      |
| Salario diario             | {{SALARIO_PERSONA}}    |
| Salario diario integrado   | {{SDI}}               |
| Jornada y descanso         | {{JORNADA_RESUMEN}}   |
| Antigüedad                 | {{ANTIGUEDAD_TEXTO}}  |

TERCERO. Terminación. Las Partes han decidido de común acuerdo dar por terminada la relación de trabajo con efectos al {{BAJA_FECHA}}, por así convenir a sus intereses.[SI CONV_HECHOS] Las Partes hacen constar, además, lo siguiente: {{CONV_HECHOS}}.[FIN SI]

DECLARACIONES

I. Declara la Empresa, por conducto de su representante:

a) Que su domicilio es {{PATRON_DOMICILIO}}.

b) Que su representante cuenta con las facultades necesarias para celebrar este convenio, las cuales no le han sido revocadas ni limitadas en forma alguna.

c) Que es su voluntad celebrar este convenio en los términos que en él se establecen.

II. Declara la Persona Trabajadora, bajo protesta de decir verdad:

a) Identidad. Que su CURP es {{TRAB_CURP}}, que su domicilio es {{TRAB_DOMICILIO}} y que se identifica con identificación oficial vigente, cuya copia firmada se agrega a este convenio.

b) Capacidad y voluntad. Que comparece por su propio derecho, en pleno uso de sus facultades, de manera libre y voluntaria, y que en la celebración de este convenio no existe error, dolo, mala fe, violencia ni intimidación, ni ha recibido presión, amenaza o promesa de ninguna persona para firmarlo.

c) Conocimiento del contenido. Que leyó íntegramente este convenio y sus anexos, que se le explicó su contenido y alcance, que tuvo la oportunidad de consultarlo con la persona de su confianza que estimó conveniente, con el tiempo que consideró necesario, y que está conforme con todos sus términos.

d) Causa de la terminación. Que la terminación de la relación de trabajo obedece al acuerdo de las Partes que consta en este convenio.

e) Único patrón. Que la Empresa fue su único patrón por los servicios que prestó, y que los clientes, proveedores, empresas relacionadas o terceros en cuyas instalaciones o en cuyo beneficio haya prestado servicios no tuvieron por ese solo hecho el carácter de patrón respecto de ella.

f) Salario. Que su último salario diario fue el señalado en el antecedente segundo, que lo recibió siempre a través de los medios de pago de la Empresa y que no percibió cantidades en efectivo, bonos ni pagos de cualquier otra naturaleza fuera de nómina.

g) Salarios y prestaciones. Que durante la relación de trabajo la Empresa le pagó oportunamente sus salarios y prestaciones, con excepción de los que se liquidan en este convenio.

h) Jornada. Que laboró la jornada pactada y que el tiempo extraordinario que, en su caso, laboró por orden de la Empresa le fue pagado, con excepción del que se incluye en el recibo de finiquito.

i) Descansos y vacaciones. Que disfrutó sus días de descanso semanal y obligatorio y sus periodos de vacaciones, o le fueron pagados, con excepción de los que se liquidan en este convenio.

j) Seguridad social. Que la Empresa la inscribió ante el Instituto Mexicano del Seguro Social durante la relación de trabajo.

k) Salud. Que no sufrió riesgos de trabajo que no hayan sido reportados y atendidos, y que, a la fecha, no tiene conocimiento de padecer enfermedad o lesión derivada de su trabajo.

l) Trato. Que durante la relación de trabajo no fue objeto de actos de discriminación, hostigamiento o acoso que no hubiera hecho del conocimiento de la Empresa.

m) Bienes e información. Que entregó a la Empresa todos los bienes, herramientas, documentos, información, cuentas y accesos que tuvo bajo su resguardo, y que no conserva copia de información de la Empresa en ningún medio, salvo lo que se haga constar en el acta de devolución.

n) Procedimientos. Que no tiene pendiente ninguna solicitud de conciliación, demanda, queja o denuncia de carácter laboral en contra de la Empresa, o que, si la tiene, se desiste de ella conforme a la cláusula novena.

III. Declaran las Partes que se reconocen mutuamente la personalidad con que comparecen y que este convenio contiene la relación circunstanciada de los hechos que lo motivan y de los derechos comprendidos en él.

CLÁUSULAS

PRIMERA. Terminación. Las Partes convienen en dar por terminada la relación de trabajo por mutuo consentimiento, con efectos al {{BAJA_FECHA}}, con fundamento en el artículo 53, fracción I, de la Ley Federal del Trabajo.

SEGUNDA. Último día de servicios. Las Partes reconocen que el {{BAJA_FECHA}} fue el último día en que la Persona Trabajadora prestó servicios a la Empresa y que no los prestó con posterioridad a esa fecha por ningún concepto.

TERCERA. Derechos comprendidos. Por los servicios prestados y por la terminación de la relación de trabajo, a la Persona Trabajadora le corresponden los conceptos y cantidades que se desglosan en el recibo de finiquito que se agrega como Anexo 1 y forma parte de este convenio, por concepto de salarios devengados, prestaciones devengadas[SI PA_INCLUIR = Sí] y prima de antigüedad[FIN SI], por la cantidad bruta de {{TOTAL_BRUTO}} ({{TOTAL_BRUTO_LETRA}}), antes de impuestos y deducciones.

[SI CONV_GRATIFICACION > 0]
Además, la Empresa otorga a la Persona Trabajadora una gratificación por terminación de {{CONV_GRATIFICACION}} ({{CONV_GRATIFICACION_LETRA}}), que se incluye en el Anexo 1. Las Partes convienen en que esta gratificación se imputará a cualquier cantidad que llegara a determinarse a favor de la Persona Trabajadora por cualquier concepto derivado de la relación de trabajo o de su terminación, incluso en el supuesto de que alguna estipulación de este convenio llegara a declararse sin efectos.
[FIN SI]

CUARTA. Participación en las utilidades. [SI PTU_PENDIENTE = Sí]Los derechos de la Persona Trabajadora respecto de la participación en las utilidades del ejercicio {{PTU_EJERCICIO}} quedan a salvo hasta que se determine el reparto individual, y la Empresa se la pagará en la fecha que corresponda conforme a la ley, en el domicilio o por los medios señalados en la cláusula décima cuarta.[FIN SI][SI PTU_PENDIENTE = No]La Persona Trabajadora reconoce que la Empresa le pagó la participación en las utilidades que le correspondió en los ejercicios en que tuvo derecho a ella.[FIN SI]

QUINTA. Deducciones. De la cantidad bruta se aplicarán únicamente las retenciones y descuentos que la ley ordena o permite, que se detallan en el Anexo 1 y en el comprobante fiscal digital de nómina que la Empresa emitirá.

SEXTA. Pago.
[SI CONV_PAGO_DIFERIDO = No]
La Empresa paga en este acto a la Persona Trabajadora la cantidad neta de {{TOTAL_NETO}} ({{TOTAL_NETO_LETRA}}) mediante {{CONV_FORMA_PAGO}}[SI CONV_FORMA_PAGO = Transferencia] a la cuenta registrada para el pago de su salario, cuyo comprobante se agrega como Anexo 2[FIN SI], cantidad que la Persona Trabajadora recibe a su entera satisfacción.
[FIN SI]
[SI CONV_PAGO_DIFERIDO = Sí]
La Empresa pagará a la Persona Trabajadora la cantidad neta de {{TOTAL_NETO}} ({{TOTAL_NETO_LETRA}}) en las fechas y montos siguientes: {{CONV_PARCIALIDADES}}, mediante {{CONV_FORMA_PAGO}}[SI CONV_FORMA_PAGO = Transferencia] a la cuenta registrada para el pago de su salario[FIN SI]. Cada pago se acreditará con el comprobante respectivo.
[FIN SI]

SÉPTIMA. Finiquito y desistimiento de acciones. Con el pago a que se refiere la cláusula anterior, por quedar cubiertas todas y cada una de las prestaciones que le corresponden conforme a la Ley Federal del Trabajo y al contrato de trabajo, la Persona Trabajadora otorga a la Empresa el finiquito más amplio que en derecho proceda y manifiesta que no tiene ni se reserva derecho ni acción alguna de carácter laboral, civil, mercantil, penal, administrativo, de seguridad social o de cualquier otra índole que ejercitar con posterioridad en contra de la Empresa, ni de sus representantes, socios o accionistas, administradores, empleados, empresas filiales, subsidiarias o relacionadas, ni de los clientes o beneficiarios de los servicios en que haya participado, por concepto de salarios, salarios vencidos, tiempo extraordinario, prima dominical, días de descanso semanal u obligatorio laborados, vacaciones, prima vacacional, aguinaldo, prima de antigüedad, indemnizaciones, bonos, comisiones, ni por ningún otro concepto derivado de la relación de trabajo o de su terminación, deslindándolos de cualquier responsabilidad.

OCTAVA. Finiquito de la Empresa. La Empresa, por conducto de su representante, manifiesta que no se reserva acción alguna en contra de la Persona Trabajadora derivada de la relación de trabajo y le otorga el finiquito correspondiente, con excepción de las acciones que deriven de las cláusulas décima segunda y décima tercera y de hechos que la Empresa desconozca a la fecha de firma de este convenio.

NOVENA. Desistimiento. Si la Persona Trabajadora hubiera presentado alguna solicitud de conciliación, demanda, queja o denuncia de carácter laboral en contra de cualquiera de las personas señaladas en la cláusula séptima, se desiste de ella en este acto y se obliga a presentar el desistimiento ante la autoridad que conozca de ella, dentro de los 5 días hábiles siguientes a la firma de este convenio.

DÉCIMA. Reconocimiento de documentos. La Persona Trabajadora reconoce como suyas las firmas que obran en su contrato de trabajo, recibos de nómina, registros de asistencia, convenios y demás documentos de su expediente laboral, así como su contenido.

DÉCIMA PRIMERA. Seguridad social, vivienda y retiro. La Empresa presentará el aviso de baja ante el Instituto Mexicano del Seguro Social dentro del plazo legal. Los derechos de la Persona Trabajadora en materia de seguridad social, vivienda y ahorro para el retiro se rigen por sus leyes y se ejercen ante los institutos correspondientes.

DÉCIMA SEGUNDA. Bienes e información. La Persona Trabajadora ratifica que entregó todos los bienes, herramientas, documentos, información, cuentas y accesos de la Empresa[SI CARTA_RESPONSIVA = Sí], según el acta de devolución que se levanta en esta misma fecha[FIN SI]. Si después de la firma apareciera en su poder algún bien o información de la Empresa, se obliga a devolverlo dentro de los 3 días hábiles siguientes a que se le requiera, sin conservar copia. La Empresa conserva sus acciones por los bienes no devueltos y por los daños que se le causen.

DÉCIMA TERCERA. Confidencialidad. La Persona Trabajadora se obliga a guardar la confidencialidad de la información de la Empresa, de sus clientes y de sus proveedores en los términos del contrato de trabajo[SI NIVEL_ACCESO_INFO = Calificado] y del convenio de confidencialidad[FIN SI], durante el plazo pactado en ellos, y a no utilizar esa información para captar clientes o personal de la Empresa ni para competir con ella. La Empresa conserva sus acciones por el incumplimiento de esta obligación y por los daños que se le causen.[SI CONV_PENA = Sí] El incumplimiento posterior a la terminación dará lugar, además, a la pena convencional pactada en el convenio de confidencialidad.[FIN SI]

DÉCIMA CUARTA. Comunicaciones posteriores. Para cualquier comunicación relacionada con este convenio, el pago de la participación en las utilidades, la entrega de comprobantes fiscales o la expedición de constancias, la Persona Trabajadora señala su domicilio indicado en las declaraciones y el correo electrónico {{TRAB_EMAIL}}, y se obliga a informar por escrito a la Empresa cualquier cambio.

DÉCIMA QUINTA. Datos personales y registro del acto. La Empresa conservará el expediente laboral de la Persona Trabajadora durante los plazos legales, conforme a su aviso de privacidad. Las Partes consienten en que el acto de firma de este convenio se registre en fotografía o video, como medio de prueba de su celebración.

DÉCIMA SEXTA. Divisibilidad. Si alguna estipulación de este convenio llegara a considerarse contraria a la ley, solo esa estipulación carecerá de efectos y las demás conservarán su validez.

DÉCIMA SÉPTIMA. Ejemplares y firma. Este convenio se firma por duplicado, al margen de cada hoja y al calce. La Persona Trabajadora imprime además su huella digital, escribe de su puño y letra la leyenda que aparece al final y recibe en este acto un ejemplar con sus anexos.

Firman en {{LUGAR_FIRMA}}, el {{FECHA_FIRMA}}.

LA EMPRESA                                   LA PERSONA TRABAJADORA
______________________________               ______________________________
{{REP_NOMBRE}}, {{REP_CARACTER}}             {{TRAB_NOMBRE}}
                                             Huella digital: [recuadro]

Leyenda que escribe de su puño y letra la Persona Trabajadora:
«Leí este convenio, estoy de acuerdo con él y recibí mi pago».
______________________________________________________________________
______________________________________________________________________

Anexo 1. Recibo de finiquito.
[SI CONV_FORMA_PAGO = Transferencia Y CONV_PAGO_DIFERIDO = No]Anexo 2. Comprobante de la transferencia.[FIN SI]
Copia firmada de la identificación oficial de la Persona Trabajadora.
```

Reglas del convenio:

- Firma siempre autógrafa, con firma al margen de cada hoja, huella digital y leyenda manuscrita, sea cual sea `FIRMA_MODALIDAD` del contrato. El convenio no se envía a firma electrónica.
- Anexo 2: el sistema muestra «Adjunte el comprobante de la transferencia» como recordatorio, sin hacerlo obligatorio para cerrar la baja. El archivo es el mismo que se registra en 5.4.
- `CONV_PENA` se toma de la configuración de la empresa (pena del convenio de confidencialidad); no se captura en la baja.
- `CONV_HECHOS` es opcional y no admite textos que imputen conductas a la Persona Trabajadora (aviso, no bloqueo).
- `CONV_PARCIALIDADES`: tabla de fecha y monto; la suma debe igualar `TOTAL_NETO`. Si la última fecha rebasa 6 meses desde la firma, alerta (no bloquea).
- Las condiciones van dentro de las cláusulas: la numeración no cambia.
- Si la Persona Trabajadora no firma: sección 5.2.

### 7.3 Aviso de rescisión — ELIMINADO (respecto de la 1.1)

El aviso de rescisión es un servicio aparte. El sistema no lo genera ni captura sus datos. Ver los mensajes de 2.2.

### 7.4 Comunicado de terminación al vencer el periodo de prueba o de capacitación inicial

Documento de respaldo. Solo se genera si se cumplen los requisitos de 2.3. `EVAL_RESUMEN` se toma de la evaluación final; no se redacta libremente.

```text
COMUNICADO DE TERMINACIÓN DE LA RELACIÓN DE TRABAJO AL VENCER EL {{PERIODO_TIPO_MAYUS}}

{{LUGAR_FIRMA}}, a {{BAJA_FECHA}}.

{{TRAB_NOMBRE}}
Puesto: {{PUESTO}}

En su contrato de trabajo, firmado el {{CONTRATO_FECHA}}, se pactó un {{PERIODO_TIPO}} de {{PERIODO_DURACION}}, del {{FECHA_INICIO}} al {{PERIODO_FIN}}, para [SI PRUEBA_OPCION = Periodo de prueba]verificar que usted cumple con los requisitos y conocimientos necesarios para desarrollar el trabajo[FIN SI][SI PRUEBA_OPCION = Capacitación inicial]que usted adquiriera los conocimientos o habilidades necesarios para el puesto[FIN SI].

La Empresa evaluó su desempeño el {{EVAL_FECHA}}, con el resultado siguiente: {{EVAL_RESUMEN}}.[SI PRUEBA_OPCION = Capacitación inicial] Durante el periodo se le impartió la capacitación que consta en {{CAPACITACION_EVIDENCIA}}.[FIN SI]

[SI F2_EMITIDA = Sí]
La Comisión Mixta de Capacitación, Adiestramiento y Productividad emitió su opinión el {{F2_FECHA}}, en el sentido siguiente: {{F2_SENTIDO}}.
[FIN SI]
[SI F2_EMITIDA = No]
La Empresa solicitó la opinión de la Comisión Mixta de Capacitación, Adiestramiento y Productividad el {{F2_SOLICITUD_FECHA}}, sin que se emitiera dentro del plazo.
[FIN SI]

Tomando en cuenta la evaluación, [SI F2_EMITIDA = Sí]la opinión de la Comisión [FIN SI]y la naturaleza del puesto, la Empresa determina que usted no [SI PRUEBA_OPCION = Periodo de prueba]acreditó satisfacer los requisitos y conocimientos necesarios para desarrollar las labores del puesto[FIN SI][SI PRUEBA_OPCION = Capacitación inicial]acreditó la competencia requerida para el puesto[FIN SI]. En consecuencia, la relación de trabajo termina con esta fecha, sin responsabilidad para la Empresa, con fundamento en el artículo {{PERIODO_ARTICULO}} de la Ley Federal del Trabajo.

Las prestaciones que le corresponden se detallan en el recibo de finiquito que se le presenta con este comunicado.

______________________________
{{REP_NOMBRE}}, {{REP_CARACTER}}

Recibí: ______________________________ {{TRAB_NOMBRE}}, el ___ de ________ de ____.

```

`PERIODO_ARTICULO` = «39-A» si `PRUEBA_OPCION` = Periodo de prueba; «39-B» si es Capacitación inicial. Respecto de la 1.1 se quitó la referencia al perfil de puesto (`PERFIL_CLAVE`, `PERFIL_VERSION`), que no existe con ese nombre en el contrato.

### 7.5 Comunicado de terminación por vencimiento del plazo o terminación de la obra

Documento de respaldo. Solo se genera si se cumplen los requisitos de 2.3. Se recomienda entregarlo antes del vencimiento (`VENC_AVISO_DIAS`).

```text
COMUNICADO DE TERMINACIÓN DE LA RELACIÓN DE TRABAJO POR {{VENCIMIENTO_TITULO}}

{{LUGAR_FIRMA}}, a {{FECHA_FIRMA}}.

{{TRAB_NOMBRE}}
Puesto: {{PUESTO}}

En su contrato de trabajo, firmado el {{CONTRATO_FECHA}}, se pactó una relación de trabajo [SI TIPO_RELACION = Tiempo determinado]por tiempo determinado, del {{FECHA_INICIO}} al {{FECHA_TERMINO}}[FIN SI][SI TIPO_RELACION = Obra determinada]para la obra determinada consistente en {{OBRA_DESCRIPCION}}[FIN SI], por la causa siguiente: {{CAUSA_TEMPORALIDAD}}.

[SI TIPO_RELACION = Tiempo determinado]
El plazo pactado vence el {{BAJA_FECHA}} y la causa que justificó la temporalidad concluye en esa fecha[SI VENCIMIENTO_HECHOS], porque {{VENCIMIENTO_HECHOS}}[FIN SI].
[FIN SI]
[SI TIPO_RELACION = Obra determinada]
La obra concluyó el {{BAJA_FECHA}}.
[FIN SI]

En consecuencia, la relación de trabajo termina el {{BAJA_FECHA}}, con fundamento en el artículo 53, fracción III, de la Ley Federal del Trabajo. Ese día será su último día de servicios.

Las prestaciones que le corresponden se detallan en el recibo de finiquito que se le presenta con este comunicado.

______________________________
{{REP_NOMBRE}}, {{REP_CARACTER}}

Recibí: ______________________________ {{TRAB_NOMBRE}}, el ___ de ________ de ____.

```

`VENCIMIENTO_TITULO` = «VENCIMIENTO DEL PLAZO» o «TERMINACIÓN DE LA OBRA». `VENCIMIENTO_HECHOS` es opcional.

### 7.6 Recibo de finiquito

Anexo 1 del convenio. Si el convenio no se firma, es el único documento de pago. Contiene solo «recibí» por los conceptos de la sección A; el finiquito amplio está en el convenio. No menciona la causa de terminación.

```text
RECIBO DE FINIQUITO

| Empresa                  | {{PATRON_RAZON_SOCIAL}}  |
| RFC                      | {{PATRON_RFC}}           |
| Persona Trabajadora      | {{TRAB_NOMBRE}}          |
| RFC                      | {{TRAB_RFC}}             |
| Puesto                   | {{PUESTO}}               |
| Fecha de inicio          | {{FECHA_INICIO}}         |
| Fecha de terminación     | {{BAJA_FECHA}}           |
| Antigüedad               | {{ANTIGUEDAD_TEXTO}}     |

A. PERCEPCIONES

| Concepto                                                  | Base               | Factor            | Importe              |
| Salarios devengados del {{DEV_DESDE}} al {{BAJA_FECHA}}   | {{SALARIO_PERSONA}} | {{DEV_FACTOR}}    | {{DEV_IMPORTE}}      |
[SI OTROS_DEVENGADOS] Una fila por cada renglón capturado y no vacío: concepto · base · factor · importe [FIN SI]
[SI AGUI_IMPORTE > 0] | Aguinaldo proporcional {{ANIO}} | {{SALARIO_PERSONA}} | {{AGUI_FACTOR}} | {{AGUI_IMPORTE}} | [FIN SI]
[SI VAC_PEND_IMPORTE > 0] | Vacaciones de periodos cumplidos no disfrutados | {{SALARIO_PERSONA}} | {{VAC_PEND_FACTOR}} | {{VAC_PEND_IMPORTE}} | [FIN SI]
| Vacaciones proporcionales del año en curso                | {{SALARIO_PERSONA}} | {{VAC_PROP_FACTOR}} | {{VAC_PROP_IMPORTE}} |
| Prima vacacional                                          | {{PV_BASE}}        | {{PRIMA_VACACIONAL_PCT}} | {{PV_IMPORTE}}  |
[SI PA_INCLUIR = Sí] | Prima de antigüedad | {{SALARIO_TOPADO}} | {{PA_FACTOR}} | {{PA_IMPORTE}} | [FIN SI]
[SI PRESTACIONES_SUPERIORES] Una fila por cada prestación superior devengada [FIN SI]
[SI PTU_DETERMINADA_NO_PAGADA > 0] | PTU determinada no pagada, ejercicio {{PTU_EJERCICIO}} | — | — | {{PTU_IMPORTE}} | [FIN SI]
[SI INDEMNIZACION_MONTO > 0] | Indemnización | {{SDI}} | {{IND_FACTOR}} | {{IND_IMPORTE}} | [FIN SI]
[SI CONV_GRATIFICACION > 0] | Gratificación por terminación | — | — | {{CONV_GRATIFICACION}} | [FIN SI]
| TOTAL DE PERCEPCIONES                                     |                    |                   | {{TOTAL_BRUTO}}      |

B. DEDUCCIONES

| Concepto                                  | Importe                |
| Impuesto sobre la renta                   | {{ISR}}                |
| Cuotas obreras IMSS                       | {{IMSS_OBRERA}}        |
[SI DEDUCCIONES] Una fila por cada renglón de «Otras deducciones» (4.8): concepto · importe [FIN SI]
| TOTAL DE DEDUCCIONES                      | {{TOTAL_DEDUCCIONES}}  |

C. NETO: {{TOTAL_NETO}} ({{TOTAL_NETO_LETRA}}), que se paga mediante {{CONV_FORMA_PAGO}}[SI CONV_PAGO_DIFERIDO = Sí] en las fechas señaladas en el convenio[FIN SI]. El detalle fiscal consta en el comprobante fiscal digital de nómina.

[SI PTU_PENDIENTE = Sí]
D. La participación de utilidades del ejercicio {{PTU_EJERCICIO}} no se incluye; se pagará en la fecha de reparto que corresponda conforme a la ley.
[FIN SI]

Recibí [SI CONV_PAGO_DIFERIDO = No]el importe neto señalado[FIN SI][SI CONV_PAGO_DIFERIDO = Sí]el desglose de las cantidades que se me pagarán[FIN SI] por los conceptos de la sección A.

{{LUGAR_FIRMA}}, a {{FECHA_FIRMA}}.

______________________________
{{TRAB_NOMBRE}}
```

Reglas del recibo:

- Firma autógrafa siempre.
- **Una sola hoja tamaño carta** (21.59 × 27.94 cm), sin excepción. Formato base: márgenes de 2 cm, interlineado sencillo, Arial 12, un solo renglón en blanco entre secciones y la firma al pie de la misma hoja. No se imprimen filas con importe cero ni bloques condicionales falsos.
- Si el contenido no cabe con el formato base, el sistema ajusta en este orden hasta que quepa: (1) márgenes de 1.5 cm; (2) sin renglones en blanco entre secciones; (3) las tablas A y B en Arial 10, con encabezado, neto y firma en Arial 12. Nunca pasa a una segunda hoja. Si aun así no cabe, la pantalla avisa: «El recibo excede una hoja; reduzca o agrupe renglones de otros devengados o deducciones».
- **Factor**: solo el número, nunca la fórmula. Es la cantidad que, multiplicada por la base, da el importe: días (4 decimales, por ejemplo 0.4932; los salarios devengados en días enteros, por ejemplo 12) o porcentaje (prima vacacional, por ejemplo 25 %). `PV_BASE` es el importe total de vacaciones del recibo.
- La pantalla de cálculo puede mostrar la fórmula como ayuda al contador; los documentos impresos no.
- Los importes son los vigentes tras cifras propias (4.4); solo se genera en versión final con `CALCULO_VALIDADO` = Sí.
- `ISR` (suma del ISR ordinario y de separación) e `IMSS_OBRERA` salen del cálculo 4.7. La leyenda de estimación solo se muestra en pantalla: el recibo impreso lleva las cifras validadas por el contador.
- Los periodos de vacaciones prescritos nunca se imprimen (4.9).
- Una deducción de «Pérdida o daño» solo se descuenta con el expediente concluido (7.7, regla 2); si no ha concluido antes del pago, no se descuenta.

### 7.7 Acta de devolución y entrega de herramientas y cierre de accesos

La plantilla ya existe en el kit de contratación. Este módulo agrega estas reglas de comportamiento:

1. **No condiciona el pago.** El finiquito se paga en su fecha aunque el acta no se haya firmado o haya faltantes.
2. **Faltantes o daños (actualizada en 1.5, art. 46 vigente del RIT).** Cada bien con «Se devuelve = No» o con daño se investiga conforme al procedimiento de los arts. 80 y 81 del RIT: FD-5 y, si la persona no reconoce, FD-1 → FD-3. El descuento solo procede con reconocimiento en FD-5 o con determinación de responsabilidad en FD-3, conforme al art. 27 del RIT, con resguardo que tenga valor de reposición y dentro de los límites del art. 110, fr. I LFT. Si el expediente no concluye antes del pago, el finiquito se paga completo y no se descuenta. Las referencias a los artículos del RIT se resuelven con `REF_ART_n` (el RIT renumera).
3. **Cierre de accesos.** Cada cuenta de `DEV_ACCESOS` requiere fecha de baja, igual o anterior a `BAJA_FECHA` + 1 día hábil.
4. **Persona que no se presenta.** RH registra la inasistencia y el sistema genera un requerimiento de devolución dirigido a `TRAB_EMAIL`, con plazo de 5 días hábiles. No se retiene el finiquito.
5. **Plazo:** el acta se levanta en la misma fecha del convenio o, a más tardar, dentro de 3 días hábiles.
6. **Valor de reposición (20/11).** Cada bien de `DEV_BIENES` se precarga con la descripción y el valor de reposición de la columna de `EQUIPO_DESCRIPCION` de la carta responsiva vigente. RH puede corregirlo con motivo. Un bien sin valor de reposición no admite descuento (regla 2); la pantalla lo marca «Sin valor de reposición: no procede descuento».
7. **Firma (20/11; registro 4.11).** RH elige cómo se firma (`DEV_FIRMA_FORMA`: Electrónica · Autógrafa), sin valor por omisión, según se haga la entrega:
   - Electrónica: la Persona Trabajadora firma con su tipo de firma (especificación de firma electrónica) y por la Empresa firma la persona de RH designada (`FIRMANTES_EMPRESA`); sin ella, el representante (aprobado por el usuario, 20/11/2026).
   - Autógrafa: firman en papel la Persona Trabajadora y quien recibe por la Empresa (`DEV_RECIBE`); se carga el escaneo.
   - Testigos solo si la persona se niega a firmar: constancia de negativa (7.1) con dos testigos y envío del acta a `TRAB_EMAIL`. Si rechaza la firma electrónica, el acta pasa a autógrafa.
   - La plantilla del kit imprime el bloque de testigos solo con negativa.

### 7.8 Convenio de pago a beneficiarios

Rutas (`BENEF_RUTA`, calculada):

- **Designación:** designación vigente (`BENEF_CONFIRMACION_FECHA` con 12 meses o menos), sin controversia y total menor que `BENEF_UMBRAL`. Se paga a los designados en sus porcentajes, con acta de defunción, identificación y declaración bajo protesta.
- **Tribunal:** sin designación, con controversia, con menores sin representante acreditado o con total que rebasa `BENEF_UMBRAL`. El sistema recomienda abstenerse de pagar hasta la declaración de beneficiarios. `BENEF_UMBRAL` recomienda la ruta, no bloquea.
- Si un designado falleció, su porción se reparte entre los demás en proporción a sus porcentajes.
- Lo que corresponde a menores se paga a quien ejerza la patria potestad o la tutela.
- El pago por designación nunca se hace en efectivo.
- Sin renglón de Fonacot en el recibo anexo (4.8); alerta del aviso de defunción (5.1).

```text
CONVENIO DE PAGO A BENEFICIARIOS

En {{LUGAR_FIRMA}}, el {{FECHA_FIRMA}}, {{PATRON_RAZON_SOCIAL}} (la Empresa), representada por {{REP_NOMBRE}}, y las personas que se indican, en su carácter de beneficiarias de {{TRAB_NOMBRE}} (la Persona Trabajadora fallecida), hacen constar lo siguiente:

1. La Persona Trabajadora prestó servicios a la Empresa desde el {{FECHA_INICIO}} en el puesto de {{PUESTO}} y falleció el {{BAJA_FECHA}}, según acta de defunción {{DEFUNCION_ACTA}}. La relación de trabajo terminó en esa fecha, conforme al artículo 53, fracción II, de la Ley Federal del Trabajo.

2. [SI BENEF_RUTA = Designación]En la designación de beneficiarios firmada el {{BENEF_DESIGNACION_FECHA}} y confirmada el {{BENEF_CONFIRMACION_FECHA}}, la Persona Trabajadora designó a las personas y porcentajes siguientes: {{BENEFICIARIOS}}.[SI BENEF_FALLECIDO = Sí] La porción de {{BENEF_FALLECIDO_NOMBRE}}, fallecida, se distribuye entre las demás en proporción a sus porcentajes.[FIN SI][FIN SI][SI BENEF_RUTA = Tribunal]Por resolución de {{TRIBUNAL}} de fecha {{RESOLUCION_FECHA}}, expediente {{RESOLUCION_EXPEDIENTE}}, se declaró beneficiarias a las personas siguientes: {{BENEFICIARIOS_DECLARADOS}}.[FIN SI]

3. Las prestaciones pendientes de pago se detallan en el recibo anexo e incluyen la prima de antigüedad.

4. La Empresa paga a cada beneficiaria la cantidad que le corresponde:
{{BENEF_PAGOS}}
(Tabla: nombre · porcentaje · importe neto · forma de pago)
[SI BENEF_MENORES = Sí]Lo que corresponde a {{MENOR_NOMBRE}} se paga a {{MENOR_REPRESENTANTE}}, quien acredita ejercer la patria potestad o la tutela con {{MENOR_REPRESENTACION_DOC}}.[FIN SI]

5. [SI BENEF_RUTA = Designación]Cada beneficiaria declara, bajo protesta de decir verdad, que no conoce a otra persona con derecho a recibir estas prestaciones y se obliga a responder frente a quien acredite un derecho preferente por lo que haya recibido en exceso.[FIN SI]

6. Las beneficiarias reconocen que con este pago quedan cubiertos los salarios y prestaciones devengados y no cobrados por la Persona Trabajadora y la prima de antigüedad, y no se reservan acción alguna en contra de la Empresa por esos conceptos. [SI SEGURO_VIDA = Sí]Este convenio no comprende el seguro de vida, cuyos beneficiarios y trámite se rigen por la póliza y el formato de la aseguradora. [FIN SI]Tampoco comprende prestaciones de seguridad social, vivienda o retiro.

Firmas de la Empresa y de cada beneficiaria, con huella digital.
```

### 7.9 Constancia de servicios

Se genera si `CONSTANCIA_SERVICIOS` = Sí en la baja, o después, desde el expediente, cuando la Persona Trabajadora la solicite. Nunca menciona la causa de terminación, el desempeño ni recomendaciones. Mensaje junto a la casilla: «Si la Persona Trabajadora la solicita, la Empresa debe expedirla dentro de 3 días (art. 132, fr. VIII LFT).»

```text
CONSTANCIA DE SERVICIOS

{{LUGAR_FIRMA}}, a {{FECHA_FIRMA}}.

A quien corresponda:

{{PATRON_RAZON_SOCIAL}} hace constar que {{TRAB_NOMBRE}}, con CURP {{TRAB_CURP}}, prestó sus servicios a esta Empresa del {{FECHA_INICIO}} al {{BAJA_FECHA}}, con el puesto de {{PUESTO}}.

Se expide la presente a solicitud de la persona interesada, para los fines que a ella convengan.

______________________________
{{REP_NOMBRE}}, {{REP_CARACTER}}
{{PATRON_RAZON_SOCIAL}}
```

### 7.10 FON-1. Aviso sobre el crédito Fonacot (nueva en 1.5)

- **Se genera** en toda baja, salvo fallecimiento, de una persona con `FONACOT_CREDITO` = Sí, si `FONACOT_AVISO_PERSONA` = Sí (configuración de la empresa; Sí por omisión).
- **Texto:** el de la especificación de los módulos 6 y 8, sección 20. Se programa una sola vez y el módulo 4 solo lo agrega al paquete de baja; no se duplica aquí.
- **Datos que le pasa el módulo 4:** `BAJA_FECHA`, `FONACOT_RETENCION_FINIQUITO` (el importe del renglón Fonacot de 4.8; si es cero o no hay renglón, el párrafo de la retención no se imprime), `LUGAR_FIRMA` y `FECHA_FIRMA`. `FONACOT_BAJA_REPORTE_FECHA` viene del módulo 8.
- **Firma:** por la Empresa, la persona de RH designada (`FIRMANTES_EMPRESA`) o, sin ella, el representante; la Persona Trabajadora firma de recibido en forma autógrafa, con el convenio y el recibo.
- **Si la persona no se presenta:** se envía a `TRAB_EMAIL` y queda la constancia de envío en la bitácora.

---

## 8. Diccionario de variables

### 8.1 Variables existentes que se reutilizan

Del contrato y del kit: `PATRON_RAZON_SOCIAL`, `PATRON_RFC`, `PATRON_DOMICILIO`, `REP_NOMBRE`, `REP_CARACTER`, `TRAB_NOMBRE`, `TRAB_CURP`, `TRAB_RFC`, `TRAB_NSS`, `TRAB_DOMICILIO`, `TRAB_EMAIL`, `PUESTO`, `FECHA_INICIO`, `TIPO_RELACION`, `TIPO_RELACION_TEXTO`, `FECHA_TERMINO`, `CAUSA_TEMPORALIDAD`, `OBRA_DESCRIPCION`, `PRUEBA_OPCION`, `NIVEL_ACCESO_INFO`, `EQUIPO_DESCRIPCION`, `DEV_BIENES`, `DEV_ACCESOS`, `FIRMA_MODALIDAD`, `LUGAR_FIRMA`, `FECHA_FIRMA`, `SEGURO_VIDA`, `CT_DOMICILIO` (con REPSE en instalaciones del cliente: `CLIENTE_INSTALACION_DOMICILIO`).

Del módulo 5 (1.5): `SALARIO_PERSONA` y la versión de condiciones de la persona (`PUESTO_VERSION`, `JORNADA_VERSION`, `PRESTACIONES_VERSION`).

Del módulo de vacaciones y aguinaldo (1.5, especificación v1.2): saldos por periodo y su estado (Vigente, Fuera de plazo, Prescrito), `AGUINALDO_PERIODO_INICIO`, `AGUINALDO_COMPUTA`, `AGUINALDO_VALIDADO` y el registro del pago del aguinaldo del año.

Del módulo de permisos (1.5): `SITUACION_PROTEGIDA`, `SITUACION_PROTEGIDA_TIPO`, `COMISION_FECHA_LIMITE` y, del evento D4, `SUSP_LIMITE`.

Del alta (20/11): `INFONAVIT_DESCUENTO_TIPO`, `INFONAVIT_DESCUENTO_VALOR`, `FONACOT_DESCUENTO_MONTO` y la columna de valor de reposición de `EQUIPO_DESCRIPCION`; del kit: `DEV_RECIBE`.

De los módulos 6 y 8 (1.5): `PAGO_REGISTRO`, `PAGO_EVIDENCIA`, `FONACOT_BAJA_REPORTE_FECHA`, `FONACOT_PLAZOS` (X), `FIRMANTES_EMPRESA`. De la empresa: `FONACOT_AVISO_PERSONA`.

`CONTRATO_FECHA` es derivada: la `FECHA_FIRMA` del contrato vigente en el expediente.

Verificar nombre en el diccionario único: `TRAB_RFC` (el alta captura el RFC prellenado con la CURP más la homoclave; registro 5.1), `JORNADA_RESUMEN`, `CARTA_RESPONSIVA`, `BENEFICIARIOS`, `PRIMA_VACACIONAL_PCT`.

Faltan en el alta: `PENSION_ALIMENTICIA`, `PENSION_AUTORIDAD`, `PENSION_PORCENTAJE`, `PENSION_EXPEDIENTE`; `INFONAVIT_CREDITO` y `FONACOT_CREDITO`; `BENEF_CONFIRMACION_FECHA`.

### 8.2 Variables del módulo

| Variable | Nivel | Tipo | Validación | Activa o imprime |
| --- | --- | --- | --- | --- |
| BAJA_MOTIVO | V | Opción (2.1) | Obligatoria; sin «despido injustificado» | Cálculo, documento de respaldo, mensajes. **No se imprime** |
| BAJA_FECHA | V | Fecha | Obligatoria; ≥ FECHA_INICIO | Todos; revisión de 2.4 y efectos de 5.5 |
| BAJA_CONFIRMACION_PROTEGIDA (1.5) | V | Registro: usuario, fecha y hora de cada una de las dos confirmaciones, situaciones mostradas | Obligatoria si `SITUACION_PROTEGIDA` = Sí o hay `EMBARAZO_INFORMADO_FECHA` sin C3 a `BAJA_FECHA` | Avance al paso 4 (2.4). **No se imprime** |
| EMBARAZO_INFORMADO_FECHA (20/11) | A (expediente) | Fecha en que la trabajadora informó el embarazo; la captura RH cuando se le informa; deja de usarse al registrarse C3 | Opcional; sin valor por omisión | Alerta de 2.4. **No se imprime** |
| BAJA_CONFIRMACION_B4 (1.5) | V | Registro: usuario, fecha y hora | Obligatoria si hay B4 vigente a `BAJA_FECHA` | Avance al paso 4 (2.4). **No se imprime** |
| CANDADOS_OMITIDOS | S | Registro: usuario, fecha, requisitos faltantes | Automático al oprimir «Continuar sin requisitos» | Suprime el comunicado de respaldo (2.3) |
| ANTIGUEDAD_TEXTO | S | Texto | Años, meses y días | Convenio; recibo |
| SALARIO_PERSONA | A/S (módulo 5) | Moneda, diario | Vigente a BAJA_FECHA según la versión de condiciones de la persona; en ascenso, el del puesto ocupado | Convenio; recibo; base de cálculo |
| SDI | S | Moneda | Sección 4.3 | Convenio; recibo; escenario |
| SALARIO_TOPADO | S | Moneda | Sección 4.3 | Prima de antigüedad |
| SALARIO_MINIMO (tabla) | E (global) | Tabla: año, zona, monto | Obligatoria | SALARIO_TOPADO |
| AGUINALDO_DIAS | E | Entero | ≥ 15 | Aguinaldo |
| VAC_PEND_DIAS / VAC_PROP_DIAS | S | Decimal | Del módulo de vacaciones (4.9) | Recibo |
| VAC_PRESCRITOS (1.5) | S | Días y fecha por periodo | Del módulo de vacaciones | Solo pantalla, informativo; **no se imprime** |
| OTROS_DEVENGADOS | V | Tabla dinámica: tipo, concepto, base, cantidad, importe, soporte; internos, no impresos (21/11): estado (Sugerido · Confirmado) y folio de origen del módulo 9 | 1 renglón por omisión; «+ Agregar concepto»; quitar renglón; sin límite; soporte opcional; renglón vacío no se imprime; precarga del módulo 9 (4.2) | Recibo |
| PRESTACIONES_SUPERIORES | O/S | Tabla por puesto, de la versión de la persona | — | Recibo |
| PA_INCLUIR | V | Sí/No | Bloqueada en Sí en los casos legales (4.2) | Recibo; convenio, cláusula tercera |
| PTU_PENDIENTE / PTU_EJERCICIO | S | Sí/No; año | Del kit de PTU | Convenio, cláusula de PTU; recibo |
| PTU_DETERMINADA_NO_PAGADA / PTU_IMPORTE | S | Moneda | Del kit de PTU | Recibo |
| INDEMNIZACION_MONTO | S | Moneda | Solo rescisión art. 51 o incapacidad art. 54 | Recibo |
| CONV_HECHOS | V | Texto largo | Opcional; aviso si imputa conductas | Convenio, antecedente tercero |
| CONV_GRATIFICACION | V | Moneda | ≥ 0; muestra % de capas 2 y 3 | Convenio, cláusula de gratificación; recibo |
| CONV_FORMA_PAGO | V | Opción: Transferencia / Cheque / Efectivo | Obligatoria; efectivo pide confirmación; prohibido en pago a beneficiarios por designación | Convenio; recibo; medio del registro de pago (5.4) |
| CONV_PAGO_DIFERIDO | V | Sí/No | Sí: recomienda ratificación | Convenio, cláusula de pago; recibo; una obligación por parcialidad en el módulo 6 |
| CONV_PARCIALIDADES | V | Tabla: fecha, monto | Suma = TOTAL_NETO; alerta si la última fecha rebasa 6 meses | Convenio |
| TOTAL_BRUTO / TOTAL_DEDUCCIONES / TOTAL_NETO (+ _LETRA) | S | Moneda; texto | Neto ≥ 0 | Convenio; recibo; obligación «Finiquito» del módulo 6 |
| ISR / IMSS_OBRERA | S | Moneda | Cálculo 4.7; «No calculado» si falta parámetro | Recibo |
| DEDUCCIONES | V | Tabla dinámica: tipo, concepto, importe, soporte | 1 renglón por omisión; «+ Agregar deducción»; renglones automáticos por créditos y pensión del alta; avisos de 4.8 | Recibo; neto |
| FONACOT_RETENCION_FINIQUITO (+ _LETRA) (1.5) | V/S | Moneda | Importe del renglón «Crédito Fonacot»; aviso si supera la retención mensual de la cédula; no existe en fallecimiento | Recibo; FON-1; cédula siguiente (módulo 8) |
| DEV_FACTOR / AGUI_FACTOR / VAC_PEND_FACTOR / VAC_PROP_FACTOR / PA_FACTOR / IND_FACTOR / PV_BASE | S | Número (4 decimales) o moneda | Importe ÷ base | Recibo, columna Factor |
| DOCUMENTO_NEGADO | V | Opción: comunicado de fin del periodo / comunicado de vencimiento / otro | Al generar la constancia de negativa | Constancia de negativa |
| CIFRA_PROPIA | V | Por concepto: monto, motivo, usuario, fecha | Motivo obligatorio | Recibo; convenio |
| UMBRAL_DESVIACION_PCT | E | Porcentaje | Por omisión 0 | Previsualización |
| UMBRALES_CONCEPTO | E | Tabla: concepto, monto de alerta | Opcional | Previsualización; recomendación de ratificación |
| CALCULO_VALIDADO / CONTADOR_NOMBRE / VALIDACION_FECHA | V | Sí/No; texto; fecha | Obligatoria para versión final; se revierte si cambia un monto | Todos los documentos con montos; obligación del módulo 6 |
| CONSTANCIA_SERVICIOS | V | Sí/No | Por omisión No | Genera 7.9 |
| ISR_ORDINARIO / ISR_SEPARACION / SUBSIDIO_EMPLEO / ISR | S | Moneda | Sección 4.7; sustituibles con cifra propia | Recibo (ISR = ordinario + separación) |
| EXENTO_ORDINARIO / EXENTO_SEPARACION | S | Moneda | Sección 4.7, paso 2 | Pantalla de cálculo |
| EXENTO_ACUMULADO_ANIO | S/V | Moneda por concepto | De nómina si existe; si no, 0 con aviso | Paso 2 |
| USMO | S/V | Moneda | Por omisión SALARIO_PERSONA × 30; editable por el contador | Tasa del ISR de separación |
| IMSS_CONCEPTOS_GRAVADOS | V | Selección de conceptos | Por omisión solo salarios devengados | Cuotas obreras |
| REF_EXENCION | E (global) | Opción: UMA / Salario mínimo | Por omisión UMA | Exenciones del paso 2 |
| PARAMETROS (tablas versionadas: UMA, TARIFA_ISR_96, SUBSIDIO_EMPLEO, SALARIO_MINIMO, CUOTAS_IMSS, EXENCIONES_93) | X | Tablas con vigencia | Solo se activan aprobadas | Cálculo 4.7 |
| PARAM_APROBADO_POR / PARAM_APROBADO_FECHA / PARAM_DOBLE_REVISION | X | Texto; fecha; Sí/No | — | Activación de parámetros (5.3) |
| PARAM_MONITOR_FRECUENCIA | X | Calendario | Por omisión diario dic-feb, semanal el resto | Monitor (5.3) |
| DEV_FIRMA_FORMA (20/11) | V | Opción: Electrónica / Autógrafa | Sin valor por omisión; obligatoria para generar el acta | Acta de devolución, bloque de firma (7.7, regla 7) |
| BAJA_FIRMA_EVIDENCIA | V | Archivo | — | Cierra el seguimiento 5.2 |
| BAJA_SEGUIMIENTO_CERRADO | V | Botón + nota opcional; registra usuario y fecha | — | Cierra el seguimiento 5.2 |
| ALERTA_BAJA_INTERVALO | E | Entero (días hábiles) | Por omisión 5 | Seguimiento 5.2 |
| PERIODO_TIPO / PERIODO_TIPO_MAYUS / PERIODO_DURACION / PERIODO_FIN / PERIODO_ARTICULO | S | Texto; fecha | Del contrato | Comunicado 7.4 |
| EVAL_FECHA / EVAL_RESUMEN | V | Fecha; texto | Opcionales; requisito del comunicado 7.4 | Comunicado 7.4 |
| F2_EMITIDA / F2_FECHA / F2_SENTIDO / F2_SOLICITUD_FECHA | V (de Axia CYA) | Sí/No; fecha; texto; fecha | Opcionales; requisito del comunicado 7.4 | Comunicado 7.4 |
| CAPACITACION_EVIDENCIA | V | Archivo | Opcional; requisito del comunicado 7.4 en capacitación inicial | Comunicado 7.4 |
| VENCIMIENTO_TITULO | S | Texto | Según TIPO_RELACION | Comunicado 7.5 |
| VENCIMIENTO_HECHOS | V | Texto | Opcional | Comunicado 7.5 |
| VENC_AVISO_DIAS | E | Entero | Por omisión 5 | Alerta 5.1 |
| FONACOT_AVISO_DIAS | E | Entero (días hábiles) | 5 por omisión, de `FONACOT_PLAZOS` (convenio, cláusula Quinta) | Alerta 5.1 e incidencia de baja del módulo 8 |
| INFONAVIT_AVISO_DIAS | E | Entero | Pendiente de verificación legal | Alerta 5.1 |
| DEV_DESDE / DEV_DIAS / DEV_IMPORTE, AGUI_*, VAC_*_IMPORTE, PV_IMPORTE, PA_DIAS, PA_IMPORTE, IND_DIAS, IND_IMPORTE, ANIO | S | Varios | Sección 4.3 | Recibo |
| BENEF_RUTA | S | Opción: Designación / Tribunal | Sección 7.8 | Convenio de beneficiarios |
| BENEF_UMBRAL | E | Moneda | Umbral de verificación | Recomendación de ruta |
| BENEF_DESIGNACION_FECHA / BENEF_FALLECIDO / BENEF_FALLECIDO_NOMBRE | A/V | Fecha; Sí/No; texto | — | Convenio de beneficiarios |
| DEFUNCION_ACTA | V | Texto + archivo | Obligatoria | Convenio de beneficiarios; aviso de defunción a Fonacot |
| TRIBUNAL / RESOLUCION_FECHA / RESOLUCION_EXPEDIENTE / BENEFICIARIOS_DECLARADOS | V | Texto; fecha; texto; tabla | Ruta Tribunal | Convenio de beneficiarios |
| BENEF_PAGOS | V | Tabla: nombre, porcentaje, importe neto, forma de pago | Suma = neto | Convenio de beneficiarios |
| BENEF_MENORES / MENOR_NOMBRE / MENOR_REPRESENTANTE / MENOR_REPRESENTACION_DOC | V | Sí/No; texto; texto; archivo | — | Convenio de beneficiarios |

### 8.3 Variables eliminadas (no programar)

Ya eliminadas en la 1.1 (confirmar que no existan): `RENUNCIA_FECHA`, `RENUNCIA_FIRMA`, `RENUNCIA_MOTIVO_INFORMADO`, `RENUNCIA_MOTIVO`, `RECIBE_NOMBRE`, `RECIBE_CARGO`, `RATIFICACION`, `RATIFICACION_UMBRAL`, `RATIF_DIAS`, `CONV_PENA_DIARIA`.

Eliminadas en las versiones 1.2 y 1.3 respecto de la 1.1:

| Variable eliminada | Motivo |
| --- | --- |
| `BAJA_DECIDE` | El motivo se elige de una sola lista |
| `BAJA_MOTIVO_TEXTO` | La causa ya no se imprime en el convenio ni en el recibo |
| `CARTA_PROPIA`, `CARTA_PROPIA_FECHA` | El convenio es siempre por mutuo consentimiento |
| `PAGO_REFERENCIA`, `PAGO_FECHA`, `PAGO_LUGAR`, `CFDI_UUID`, `CFDI_DIAS` | Se quitan del convenio y del recibo. El registro del pago vive ahora en el módulo 6 (5.4) |
| `RATIFICACION_SERVICIO`, `PARAPROCESAL_SERVICIO`, `PARAPROCESAL_ACUSE`, `PARAPROCESAL_FECHA`, `EMPRESA_JURISDICCION`, `CENTRO_CONCILIACION` | Los servicios aparte ya no se registran |
| `RESC_FRACCIONES`, `RESC_HECHOS`, `RESC_FECHA_CONOCIMIENTO`, `RESC_PROCEDIMIENTO_RIT`, `RESC_FECHA_AVISO_HECHOS`, `RESC_FECHA_AUDIENCIA`, `RESC_EXPEDIENTE`, `RESC_ENTREGA`, `RESC_FECHA_AVISO`, `RESC_FECHA_ENTREGA`, `RESC_TRAB_CAUSA` | El aviso de rescisión es servicio aparte |
| `TESTIGO_1`, `TESTIGO_2`, `NEGATIVA_FIRMA`, `NEGATIVA_HORA`, `NEGATIVA_LUGAR` | La constancia de negativa se imprime en blanco y se llena a mano |
| `CONCEPTOS_LISTA`, `DEDUCCIONES_LISTA` | El convenio remite al Anexo 1 |
| `VENCIMIENTO_TEXTO`, `OBRA_EVIDENCIA`, `PERFIL_CLAVE`, `PERFIL_VERSION` | Ya no se usan en los textos |
| `PTU_FECHA_ESTIMADA` | El convenio y el recibo remiten a la fecha legal de reparto |
| `CONSTANCIA_SALIDA` | Sustituida por `CONSTANCIA_SERVICIOS` |
| `INFONAVIT_IMPORTE`, `FONACOT_IMPORTE`, `PENSION_IMPORTE`, `DANO_IMPORTE`, `DANO_EXPEDIENTE`, `ANTICIPO_IMPORTE`, `DESCUENTO_DANO`, `ANTICIPOS` (1.3) | Sustituidas por la tabla `DEDUCCIONES` |
| `AGUI_DIAS`, `VAC_PEND_DIAS`, `VAC_PROP_DIAS`, `PA_DIAS`, `IND_DIAS` en documentos (1.3) | En los documentos se imprime el factor; las variables pueden seguir existiendo en el cálculo |
| `SALARIO_DIARIO` (1.5, 20/11) | Sustituida por `SALARIO_PERSONA` (diccionario único, 18/11/2026). Imprime el mismo dato |

Recuperada en la 1.5: `SITUACION_PROTEGIDA`, que la 1.2 había eliminado. Ahora la envía el módulo de permisos y solo activa la alerta con doble confirmación de 2.4; nunca bloquea ni se imprime.

---

## 9. Dependencias con otros módulos

| Módulo | Qué necesita este módulo | Qué le envía este módulo |
| --- | --- | --- |
| Contrato de trabajo | `CAUSA_TEMPORALIDAD`, `FECHA_TERMINO` y `OBRA_DESCRIPCION` en las variantes por tiempo u obra determinada (nombres ya unificados con el contrato) | — |
| Axia CYA (comisión de capacitación) | `F2_EMITIDA`, `F2_FECHA`, `F2_SENTIDO` y `F2_SOLICITUD_FECHA` del formato F-2 (solo para el comunicado de respaldo) | — |
| Kit de contratación | Acta de devolución (reglas 1 y 2 de 7.7); fecha de confirmación anual de la designación de beneficiarios | — |
| Kit de PTU | `PTU_PENDIENTE` y `PTU_EJERCICIO`; padrón de ex trabajadores con domicilio y correo | — |
| Módulo 5 (modificación) | `SALARIO_PERSONA` y versión de condiciones a `BAJA_FECHA`; en ascenso, el salario del puesto ocupado | — |
| Módulo 6 (validación de pagos) | Estado del pago del finiquito (solo consulta) | Obligación «Finiquito» al validar; registro y evidencia del pago capturados en 5.4 |
| Módulo 8 (Fonacot) | Retención mensual de la cédula; `FONACOT_BAJA_REPORTE_FECHA`; texto de FON-1 | Incidencia de baja o aviso de defunción; `FONACOT_RETENCION_FINIQUITO` |
| Módulo 9 (jornada) | Tiempo extra pendiente a `BAJA_FECHA` (validado y no exportado, y ajustes pendientes) con horas o días, tipo, importe y folio; aviso de lo «por validar» (4.2) | `BAJA_FECHA` y calendario de días inhábiles |
| Módulo 10 (permisos) | `SITUACION_PROTEGIDA`, B4 vigente, D4 vencido (`SUSP_LIMITE`) | — |
| Módulo 11 (vacaciones y aguinaldo) | Saldos por periodo, proporcional, prescritos, aguinaldo proporcional o ya pagado (especificación v1.2, secciones 10.5 y 11) | Baja registrada: cancelar bloques posteriores y liberar cupo; aviso al contador si había aguinaldo validado sin pagar |

Se elimina la dependencia con los formatos disciplinarios del RIT (el aviso de rescisión salió del sistema). Con el RIT solo queda la regla del art. 46 en 7.7.

## 10. Pendientes que no bloquean la programación

- Plazo de aviso de baja ante Infonavit (variable configurable mientras se verifica). El de Fonacot quedó en 5 días hábiles por convenio.
- Comunicado de suspensión por fin de temporada.
- Documento de terminación por incapacidad (art. 54), prioridad C.
- Formato de la hoja interna del escenario de negociación.
- Verificaciones legales en curso (prima de antigüedad en casos opcionales; transitorios de la reforma de jornada; criterio de la SCJN sobre el aviso de rescisión). Si cambian, afectan valores por omisión y textos, no la estructura.
- Parámetros 2027: tarifa, subsidio y salarios mínimos en diciembre de 2026; UMA en enero de 2027 (alerta 5.3).

---

## Anexo A. Parámetros iniciales 2026 y caso de prueba

Se cargan al instalar el módulo como versión aprobada (`PARAM_APROBADO_POR` = «Carga inicial AEXIS», `PARAM_APROBADO_FECHA` = fecha de instalación). Después se actualizan por la alerta 5.3.

### A.1 Valores

| Parámetro | Valor | Vigencia | Fuente |
| --- | --- | --- | --- |
| UMA diaria / mensual / anual | $117.31 / $3,566.22 / $42,818.15 | 01/02/2026 – 31/01/2027 | INEGI, DOF 09/01/2026 |
| UMA diaria (para enero de 2026) | $113.14 | 01/02/2025 – 31/01/2026 | INEGI 2025 |
| Subsidio para el empleo | 15.02 % de la UMA mensual ($535.65 al mes); solo si los ingresos del mes no exceden $11,492.66 | 01/02/2026 en adelante | Decreto, DOF 31/12/2025 |
| Subsidio para el empleo (enero de 2026) | 15.59 % de la UMA mensual de 2025 | 01/01/2026 – 31/01/2026 | Mismo decreto, transitorio |
| Salario mínimo general | $315.04 diarios | 01/01/2026 | CONASAMI, DOF |
| Salario mínimo Zona Libre de la Frontera Norte | $440.87 diarios | 01/01/2026 | CONASAMI, DOF |
| Cuotas obreras IMSS | Enfermedades y maternidad, excedente de 3 UMA: 0.40 % · Prestaciones en dinero: 0.25 % · Gastos médicos de pensionados: 0.375 % · Invalidez y vida: 0.625 % · Cesantía en edad avanzada y vejez: 1.125 % · Tope del SBC: 25 UMA | Vigentes | LSS arts. 25, 28, 106, 107, 147 y 168 |
| Tope de ingresos anuales para cálculo anual del retenedor | $400,000.00 | Vigente | Art. 97, inciso b) LISR |
| Exenciones art. 93 LISR | Aguinaldo 30 · prima vacacional 15 · PTU 15 · prima dominical 1 por domingo · tiempo extra 50 % hasta 5 por semana · separación 90 por año de servicio (unidad: UMA) | Vigentes | Art. 93, fr. I, XIII y XIV LISR |

Tarifa mensual del art. 96 LISR para 2026 (Anexo 8 RMF 2026, DOF 28/12/2025, apartado B, fracción V):

| Límite inferior | Límite superior | Cuota fija | % sobre el excedente del límite inferior |
| --- | --- | --- | --- |
| 0.01 | 844.59 | 0.00 | 1.92 |
| 844.60 | 7,168.51 | 16.22 | 6.40 |
| 7,168.52 | 12,598.02 | 420.95 | 10.88 |
| 12,598.03 | 14,644.64 | 1,011.68 | 16.00 |
| 14,644.65 | 17,533.64 | 1,339.14 | 17.92 |
| 17,533.65 | 35,362.83 | 1,856.84 | 21.36 |
| 35,362.84 | 55,736.68 | 5,665.16 | 23.52 |
| 55,736.69 | 106,410.50 | 10,457.09 | 30.00 |
| 106,410.51 | 141,880.66 | 25,659.23 | 32.00 |
| 141,880.67 | 425,641.99 | 37,009.69 | 34.00 |
| 425,642.00 | En adelante | 133,488.54 | 35.00 |

### A.2 Regla del subsidio en el finiquito

Por omisión, el subsidio se calcula proporcional a los días del último periodo: $535.65 ÷ 30.4 × días. El contador puede sustituirlo con cifra propia.

### A.3 Caso de prueba (baja del 27/11/2026, ingreso 16/11/2026, `SALARIO_PERSONA` $500.00, SDI $524.66, USMO $15,000.00, gratificación $50,000.00, sin situaciones protegidas, sin crédito Fonacot, aguinaldo del año no pagado)

Valores esperados con los parámetros de A.1, para verificar la programación:

| Paso | Resultado esperado |
| --- | --- |
| Percepciones ordinarias | $6,493.16 (salarios $6,000.00 + aguinaldo $246.58 + vacaciones $197.26 + prima vacacional $49.32) |
| Exentos | Aguinaldo $246.58 y prima vacacional $49.32 (por debajo de 30 y 15 UMA) |
| Base gravable ordinaria | $6,197.26 |
| ISR ordinario antes de subsidio | $358.79 |
| Subsidio (12 días) | $211.44 |
| ISR ordinario | $147.35 |
| Pagos por separación | $50,197.26 (gratificación + prima de antigüedad) |
| Exento de separación | $0.00: antigüedad de 12 días, menor de 6 meses, equivale a 0 años |
| ISR del USMO / tasa | $1,402.82 / 9.3521 % |
| ISR de separación | $4,694.51 |
| Cuotas obreras IMSS (12 días) | $157.82 |
| Neto estimado | $51,690.74 |

### A.4 Casos de prueba de la 1.5

| Caso | Datos | Resultado esperado |
| --- | --- | --- |
| 1. Situación protegida | Persona con C3 (maternidad) vigente a `BAJA_FECHA` | Alerta crítica con el evento y su fecha; sin las dos confirmaciones no se pasa al paso 4; con ellas, `BAJA_CONFIRMACION_PROTEGIDA` con usuario, fecha y hora; nada se imprime |
| 2. Comisión permanente | B4 vigente | Mensaje de 2.4 con `COMISION_FECHA_LIMITE`; doble confirmación en `BAJA_CONFIRMACION_B4` |
| 3. Cambio de fecha | Se confirma el caso 1 y luego se cambia `BAJA_FECHA` dentro del mismo evento | Se piden de nuevo las dos confirmaciones |
| 4. D4 vencida | D4 con `SUSP_LIMITE` anterior a hoy, sin reincorporación | Mensaje informativo de 2.2; no bloquea |
| 5. Aguinaldo ya pagado | Baja el 22/12/2026; aguinaldo del año en «Pagada» en el módulo 6 | Sin renglón de aguinaldo en el recibo; sin descuento |
| 6. Aguinaldo validado sin pagar | Baja el 10/12/2026; `AGUINALDO_VALIDADO` = Sí, sin pago | Aguinaldo proporcional en el finiquito; aviso al contador; la obligación anual pasa a cancelada con motivo «Pago en finiquito» |
| 7. Vacaciones prescritas | Persona con un periodo Prescrito de 6 días y uno Vigente de 4 | Solo los 4 días se pagan; los 6 se ven en pantalla como informativos y no se imprimen |
| 8. Fonacot | `FONACOT_CREDITO` = Sí; retención mensual de la cédula $1,200.00; último periodo pagado de 15 días; RH captura $2,000.00 | Aviso sin bloqueo; FON-1 en el paquete con el importe que quede; alerta de baja a 5 días hábiles |
| 9. Fallecimiento con Fonacot | Baja por fallecimiento con `FONACOT_CREDITO` = Sí | Sin renglón de Fonacot; sin FON-1; alerta del aviso de defunción a 15 días hábiles |
| 10. Cierre con evidencia | Pago por transferencia con comprobante y XML del CFDI | El comprobante es el Anexo 2; el módulo 6 recibe ambos y coteja; el cierre de la baja no cambia |
| 11. Vacaciones autorizadas posteriores | Bloque Autorizado del 14 al 18/12/2026; baja el 30/11/2026 | El bloque se cancela y su cupo se libera al guardar la baja |
| 12. Salario de la persona | Puesto con salario base $400.00; `SALARIO_PERSONA` $450.00 | El finiquito usa $450.00 |
| 13. Precarga Fonacot (20/11) | `FONACOT_DESCUENTO_MONTO` $1,200.00; último periodo de 15 días; sin cédula del periodo | Renglón «Sugerido» con $1,200.00 × 15 ÷ 30.4; RH lo confirma o lo cambia |
| 14. Precarga Infonavit (20/11) | `INFONAVIT_DESCUENTO_TIPO` = Porcentaje | Importe vacío; la pantalla muestra el tipo y el valor del alta |
| 15. Acta sin valor de reposición (20/11) | Bien de la carta responsiva sin valor de reposición, marcado «Se devuelve = No» | Marca «no procede descuento»; el finiquito no lleva deducción por ese bien |
| 16. Acta con negativa (20/11) | `DEV_FIRMA_FORMA` = Electrónica; la persona rechaza firmar | El acta pasa a autógrafa; constancia de negativa con dos testigos; envío a `TRAB_EMAIL` |
| 17. Embarazo informado (20/11) | `EMBARAZO_INFORMADO_FECHA` capturada, sin C3 | Alerta con «Embarazo informado» y doble confirmación; la baja continúa |
| 18. Tiempo extra pendiente (21/11) | Módulo 9 con 6 horas de tiempo extra validadas y no exportadas y una prima dominical en ajuste pendiente; además, 2 horas «por validar» | Dos renglones «Sugerido» en «Otros devengados» con el importe y el folio del módulo 9; aviso de lo «por validar», sin bloqueo |

Estos valores sirven para probar el programa; el contador valida cada caso real.
