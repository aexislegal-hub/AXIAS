# AXIA RH — Módulo de vacaciones y aguinaldo: textos de VAC-1, VAC-2, VAC-3 y avisos N-1 a N-6

Sexta versión, 17/11/2026. El usuario aprobó todos los textos: VAC-1, VAC-2 y VAC-3 el 15/11/2026, y los ajustes de periodos de solicitud por antigüedad, días bloqueados, cupos y avisos N-1 a N-6 el 16/11/2026. El 17/11/2026 el usuario aclaró la regla de los días bloqueados: lo que se registra primero prevalece. Por eso, en «Cómo se fijan las fechas», en VAC-2 (apartado 4) y en N-4, «vacaciones ya autorizadas» pasa a «vacaciones ya solicitadas o autorizadas». Las aprobaciones son provisionales hasta la revisión final del módulo. Este documento forma parte de la especificación para programación v1.2. Las decisiones están en «Corte - Módulo de vacaciones y aguinaldo».

> **Nota de Cerebro (21/11/2026).** Copia del documento del proyecto «AXIARH - Módulo de vacaciones y aguinaldo - Textos (borrador)», sin cambios. Estos textos siguen vigentes con la especificación v1.4 (`vacaciones-y-aguinaldo.md`).

## Reglas de armado

- Las variables se escriben `{{VARIABLE}}`. Los bloques `[SI …] … [FIN SI]` se evalúan y sus marcas nunca se imprimen.
- Se usan los bloques comunes de la especificación de permisos (17.1): encabezado con folio, datos de la persona, cierre y firma, y negativa a firmar.
- VAC-1 y VAC-3 son registros digitales, como SP-1 y SUS-3, y no se firman. Con `SALIDA` = Constancia se emite la constancia exportable. Con `SALIDA` = Respaldo se emite el formato en papel, que lleva firmas y bloque de negativa.
- VAC-2 se firma de recibido según `FIRMA_MODALIDAD`. Por la Empresa firma la persona de RH designada en `FIRMANTES_EMPRESA`.
- Los avisos N-1 a N-6 no se firman. Se envían por los canales de `VAC_NOTIFICACION_CANALES` y cada envío queda en la bitácora.
- Concordancia de número: con valor 1, singular («1 día», «1 año»); nunca «(s)».
- Todos los documentos van en Arial.

## Cómo se fijan las fechas

- La persona define sus fechas, porque la Ley le reconoce la distribución de sus días. Las solicita por la Plataforma y la solicitud pasa por la cadena de autorización. La cadena puede autorizar, devolver o reprogramar con una fecha alterna; nunca asignar.
- Con `VAC_PROGRAMACION_MODO` = Calendario anual (texto vigente del art. 36 del RIT), las preferencias que la persona registra durante `VAC_PREFERENCIAS_DIAS` forman el calendario.
- Con `VAC_PROGRAMACION_MODO` = Periodos de solicitud por antigüedad, la Empresa fija para cada año los periodos en que cada grupo de antigüedad solicita sus vacaciones. Primero solicita el grupo de mayor antigüedad. Al cierre de cada periodo de solicitud, si los lugares de un área no alcanzan, las fechas se asignan por orden de antigüedad.
- Con `VAC_PROGRAMACION_MODO` = A solicitud no hay calendario ni periodos de solicitud.
- En los tres modos, la Empresa puede señalar días en que no se programan vacaciones, por necesidades operativas o de capacitación, y fijar cuántas personas de un área pueden estar de vacaciones el mismo día. Ninguna de las dos medidas puede impedir que una persona disfrute su saldo dentro del plazo legal. Tampoco pueden modificar, sin la aceptación de la persona, las vacaciones que solicitó o que se le autorizaron antes de que la Empresa señalara esos días.
- Si la persona no solicita, recibe recordatorios (N-5) 60 y 30 días antes de `VAC_LIMITE_OTORGAMIENTO`.
- Después de `VAC_LIMITE_OTORGAMIENTO`, la persona puede seguir solicitando sus días pendientes hasta `VAC_FECHA_PRESCRIPCION` (aniversario + 18 meses), con alerta a RH y a consultoría. Esa fecha no se imprime en ningún documento ni aviso.

---

## VAC-1. Registro de vacaciones (constancia exportable y formato de respaldo)

Se genera con cada periodo de vacaciones solicitado (incluidos los del calendario y los de los periodos de solicitud) y con cada reprogramación.

**I. Periodo**

| Concepto | Dato |
| --- | --- |
| Año de servicios | {{VAC_ANTIGUEDAD_ANIOS}}, cumplido el {{VAC_ANIVERSARIO}} |
| Fechas | Del {{VAC_FECHA_INICIO}} al {{VAC_FECHA_FIN}} |
| Días de vacaciones | {{VAC_DIAS}} días laborables |
| Saldo del periodo después de este registro | {{VAC_SALDO}} días |
| Prima vacacional | {{PRIMA_VACACIONAL_PCT}} % del salario de los días de vacaciones; se paga {{MOMENTO_PAGO_PRIMA}} |

Los días de descanso semanal y los de descanso obligatorio comprendidos en el periodo no se cuentan como días de vacaciones.

**II. Solicitud y resolución**

[SI VAC_ORIGEN = Calendario] Fechas elegidas por la Persona Trabajadora e incluidas en el calendario anual de vacaciones. [FIN SI]

[SI VAC_ORIGEN = Periodo de solicitud] La Persona Trabajadora solicitó estas fechas por la Plataforma el {{EVENTO_SOLICITUD_FECHAHORA}}, dentro del periodo de solicitud del grupo «{{VAC_GRUPO_NOMBRE}}», que concluyó el {{VAC_SOLICITUD_FIN}}. [FIN SI]

[SI VAC_ORIGEN = Solicitud] La Persona Trabajadora solicitó estas fechas por la Plataforma el {{EVENTO_SOLICITUD_FECHAHORA}}. [FIN SI]

[SI VAC_ESTADO = Autorizado] Autorizadas el {{RESOLUCION_FECHA}} por: {{AUTORIZACIONES}}. [FIN SI]

[SI VAC_ESTADO = Reprogramado Y NEGATIVA_CAUSA = Cupo completo] En algunas de las fechas solicitadas ya se alcanzó el número de personas de su área que pueden estar de vacaciones al mismo tiempo. Cuando las solicitudes coinciden, los lugares se asignan por orden de antigüedad. Se proponen las siguientes fechas de inicio, por el mismo número de días: {{VAC_ALTERNATIVAS}}. La Persona Trabajadora puede aceptar una de ellas en la Plataforma o solicitar otras fechas. [FIN SI]

[SI VAC_ESTADO = Reprogramado Y NEGATIVA_CAUSA ≠ Cupo completo] {{NEGATIVA_AUTOR}} propuso reprogramar el periodo el {{RESOLUCION_FECHA}}, por el motivo siguiente: {{NEGATIVA_MOTIVO}}. Se propone que inicie el {{FECHA_ALTERNA}}, por el mismo número de días. La propuesta requiere la aceptación de la Persona Trabajadora en la Plataforma; si no la acepta, puede solicitar otras fechas. [SI NEGATIVA_NIVEL = Jefatura] También puede pedir a Recursos Humanos que revise la reprogramación; Recursos Humanos resolverá el mismo día. [FIN SI] [FIN SI]

**III. Interrupción por incapacidad**

[SI VAC_DIAS_INTERRUMPIDOS > 0] El periodo se interrumpió el {{VAC_INTERRUPCION_FECHA}} por una incapacidad que expidió el Instituto Mexicano del Seguro Social. {{VAC_DIAS_INTERRUMPIDOS}} días de vacaciones no se disfrutaron. Esos días regresan al saldo y la Persona Trabajadora puede solicitarlos al terminar la incapacidad. El salario y la prima ya pagados por esos días quedan a cuenta de los días que se disfruten después. [FIN SI]

[SI SALIDA = Constancia] Constancia emitida por la Plataforma el {{CONSTANCIA_FECHA}} a partir del registro {{VAC_FOLIO}}, en los términos de los apartados anteriores. [FIN SI]

[SI SALIDA = Respaldo] Formato de respaldo. Se usa cuando la Persona Trabajadora no tiene acceso a la Plataforma o cuando el sistema falla. Recursos Humanos lo captura en la Plataforma el mismo día y conserva el original. [FIN SI]

**Notas para programación**
- No existe «Negar». Las acciones son «Autorizar», «Reprogramar» (exige `NEGATIVA_CAUSA`, `NEGATIVA_MOTIVO`, `FECHA_ALTERNA` y la aceptación de la persona) y «Devolver para corrección». La causa «Cupo completo» solo la asigna el sistema, al cierre de un periodo de solicitud o al validar el cupo.
- La fecha alterna y las alternativas cumplen las validaciones de la sección 6 de la especificación, incluidos los días bloqueados y los cupos. Deben quedar dentro de `VAC_LIMITE_OTORGAMIENTO` mientras no haya vencido; después, antes de `VAC_FECHA_PRESCRIPCION`.
- Un bloqueo activado después de la solicitud no es motivo para devolverla ni para reprogramarla sin la aceptación de la persona (especificación, 4.6).
- En el formato de respaldo firman la Persona Trabajadora y quienes autorizaron, en el orden de la cadena.
- `VAC_INTERRUPCION_FECHA` es la fecha de inicio del certificado C1, C2 o C3. No se captura diagnóstico.
- Si la incapacidad empieza antes del periodo, las vacaciones no inician, los días vuelven al saldo y el apartado III no se imprime.

---

## VAC-2. Constancia de antigüedad y periodo vacacional

Se emite una constancia por persona y periodo en la fecha del aniversario (`VAC_ANIVERSARIO`).

La Empresa hace constar lo siguiente:

**1. Antigüedad.** La Persona Trabajadora presta sus servicios a la Empresa desde el {{FECHA_INICIO}}. El {{VAC_ANIVERSARIO}} cumplió {{VAC_ANTIGUEDAD_ANIOS}} [SI VAC_ANTIGUEDAD_ANIOS = 1] año [FIN SI][SI VAC_ANTIGUEDAD_ANIOS > 1] años [FIN SI] de servicios.

**2. Periodo de vacaciones.** Por esa antigüedad le corresponden {{VAC_DIAS_PERIODO}} días laborables de vacaciones pagadas, con una prima vacacional del {{PRIMA_VACACIONAL_PCT}} % sobre el salario de esos días, que se paga {{MOMENTO_PAGO_PRIMA}}. [SI VAC_PROPORCIONAL = Sí] Por la naturaleza de sus servicios, los días se calcularon en proporción a los días trabajados en el año. [FIN SI]

**3. Periodo para disfrutarlas.** La Persona Trabajadora debe disfrutar estas vacaciones entre el {{VAC_ANIVERSARIO}} y el {{VAC_LIMITE_OTORGAMIENTO}}. Las solicita por la Plataforma[SI VAC_PROGRAMACION_MODO ≠ Periodos de solicitud por antigüedad] con {{DIAS_ANTICIPACION_VACACIONES}} días naturales de anticipación[FIN SI]. Al menos uno de los periodos que solicite debe ser continuo y abarcar los días mínimos que establece la Ley. Fuera de ese mínimo, puede distribuir sus días como lo requiera.

[SI VAC_PROGRAMACION_MODO = Periodos de solicitud por antigüedad Y VAC_SOLICITUD_FIN no vencido] Por su antigüedad, la Persona Trabajadora pertenece al grupo «{{VAC_GRUPO_NOMBRE}}», que solicita sus vacaciones del {{VAC_SOLICITUD_INICIO}} al {{VAC_SOLICITUD_FIN}}. Si al cierre de ese periodo de solicitud varias personas de su área piden las mismas fechas y los lugares no alcanzan, se asignan por orden de antigüedad, y a quien no alcance lugar se le proponen otras fechas. Concluidos los periodos de solicitud, puede solicitar los días que le queden en las fechas disponibles. [FIN SI]

[SI VAC_PROGRAMACION_MODO = Periodos de solicitud por antigüedad Y VAC_SOLICITUD_FIN vencido] El periodo de solicitud de su grupo ya concluyó. Puede solicitar los días que le queden en las fechas disponibles, con {{DIAS_ANTICIPACION_VACACIONES}} días naturales de anticipación. [FIN SI]

[SI VAC_BLOQUES_PROGRAMADOS > 0] Fechas ya programadas a su elección:

| Del | Al | Días |
| --- | --- | --- |
| {{VAC_BLOQUE_INICIO}} | {{VAC_BLOQUE_FIN}} | {{VAC_BLOQUE_DIAS}} |

[FIN SI]

[SI VAC_BLOQUEOS_PERIODO > 0] Días en que no se programan vacaciones por necesidades operativas o de capacitación:

| Del | Al | Motivo |
| --- | --- | --- |
| {{VAC_BLOQUEO_INICIO}} | {{VAC_BLOQUEO_FIN}} | {{VAC_BLOQUEO_DESCRIPCION}} |

[FIN SI]

**4. Reglas del periodo.**
- Los días de descanso semanal y los de descanso obligatorio comprendidos en las fechas no se cuentan como días de vacaciones.
- Si durante las vacaciones el Instituto Mexicano del Seguro Social expide una incapacidad, las vacaciones se suspenden desde la fecha del certificado. Los días no disfrutados pueden solicitarse al terminar la incapacidad.
- Los días que la Empresa señale después para no programar vacaciones no modifican las vacaciones que la Persona Trabajadora ya haya solicitado o que ya se le hayan autorizado, salvo que ella lo acepte, y se le comunican por escrito.
- Mientras subsista la relación de trabajo, las vacaciones no pueden compensarse con dinero.
- El derecho a reclamar los días no disfrutados prescribe en los términos de la Ley.

[SI VAC2_VERSION > 1] Esta constancia sustituye a la emitida el {{VAC2_FECHA_ANTERIOR}}. [FIN SI]

Cierre y firma: bloque común. La Persona Trabajadora firma de recibido según `FIRMA_MODALIDAD`, y por la Empresa firma la persona designada en `FIRMANTES_EMPRESA`. Si la Persona Trabajadora se niega a firmar, firman dos testigos y la constancia se envía a su correo personal.

**Notas para programación**
- La tabla de días bloqueados lleva una fila por cada bloqueo Activo que aplica a la persona entre su aniversario y `VAC_LIMITE_OTORGAMIENTO` en la fecha de emisión. No se incluyen los bloqueos en Borrador. Los bloqueos activados después se comunican con N-4 y no generan una nueva versión.
- La constancia no cita las cifras del mínimo continuo ni la tabla de días: el sistema las toma de `PARAMETROS_LEGALES_VACACIONES` y valida las solicitudes.
- `VAC_LIMITE_OTORGAMIENTO` = aniversario + 6 meses. `VAC_FECHA_PRESCRIPCION` no se imprime.

---

## VAC-3. Constancia de disfrute y pago de prima (confirmación en la Plataforma)

Se genera al terminar cada periodo de vacaciones. La Persona Trabajadora confirma en la Plataforma al reincorporarse y RH valida.

La Empresa y la Persona Trabajadora hacen constar lo siguiente:

- **Disfrute.** La Persona Trabajadora disfrutó sus vacaciones del {{VAC_FECHA_INICIO}} al {{VAC_FECHA_FIN}}, {{VAC_DIAS}} días laborables correspondientes a su año de servicios número {{VAC_ANTIGUEDAD_ANIOS}}, y se reincorporó el {{VAC_REINCORPORACION_FECHA}}.
- [SI VAC_DIAS_INTERRUMPIDOS > 0] **Interrupción.** {{VAC_DIAS_INTERRUMPIDOS}} días no se disfrutaron por incapacidad y regresan al saldo. [FIN SI]
- **Pago.** La Persona Trabajadora recibió el salario de los días de vacaciones y la prima vacacional, por un importe bruto de {{VAC_PRIMA_MONTO}}[SI VAC_CFDI_UUID no vacía], amparados en el comprobante fiscal digital de nómina con folio fiscal {{VAC_CFDI_UUID}}[FIN SI].
- [SI VAC_SALDO > 0] **Saldo.** Quedan pendientes {{VAC_SALDO}} días del periodo[SI VAC_LIMITE_OTORGAMIENTO no vencido], que debe disfrutar a más tardar el {{VAC_LIMITE_OTORGAMIENTO}}[FIN SI]. [FIN SI]

[SI SALIDA = Constancia] Confirmada por la Persona Trabajadora en la Plataforma el {{VAC_CONFIRMACION_FECHAHORA}} y validada por {{FIRMA_EMPRESA_NOMBRE}}. [FIN SI]

[SI SALIDA = Respaldo] Formato de respaldo. Recursos Humanos lo captura en la Plataforma el mismo día y conserva el original. [FIN SI]

**Notas para programación**
- La Plataforma ofrece dos botones: «Confirmo» y «No estoy de acuerdo». El segundo exige `VAC3_OBSERVACION` y alerta a RH. La observación queda en el expediente.
- Si la persona no responde en `VAC_CONFIRMACION_DIAS` días hábiles, el sistema alerta a RH, que puede recabar la confirmación en el formato de respaldo. Como evidencia supletoria sirven el registro de jornada sin marcas en esas fechas y el CFDI.
- Si falta `VAC_CFDI_UUID`, el sistema alerta, pero no bloquea.
- La fecha límite del saldo solo se imprime mientras no haya vencido.

---

## Avisos N-1 a N-6

Asunto del correo: «Vacaciones – {{PATRON_RAZON_SOCIAL}}». El mismo texto se muestra en la Plataforma y, cuando exista, en la app. Encabezado común: «{{TRAB_NOMBRE}}:».

**N-1. Apertura del periodo de solicitud**
Del {{VAC_SOLICITUD_INICIO}} al {{VAC_SOLICITUD_FIN}} puede solicitar por la Plataforma sus vacaciones de {{VAC_ANIO_PROGRAMACION}}. Por su antigüedad, pertenece al grupo «{{VAC_GRUPO_NOMBRE}}». Días disponibles: {{VAC_SALDO_RESUMEN}}. Al cierre, si varias personas de su área piden las mismas fechas y los lugares no alcanzan, se asignan por orden de antigüedad. [SI VAC_BLOQUEOS_ANIO > 0] Días en que no se programan vacaciones: {{VAC_BLOQUEOS_RESUMEN}}. [FIN SI]

**N-2. Cierre próximo**
Su periodo de solicitud cierra el {{VAC_SOLICITUD_FIN}} y aún no ha solicitado sus vacaciones. Si no las solicita en este periodo, después podrá hacerlo en las fechas que sigan disponibles.

**N-3. Resultado de la asignación**
[SI resultado = Con lugar] Sus vacaciones del {{VAC_FECHA_INICIO}} al {{VAC_FECHA_FIN}} tienen lugar en su área y pasan a autorización. [FIN SI]
[SI resultado = Cupo completo] Para algunas de las fechas que solicitó, del {{VAC_FECHA_INICIO}} al {{VAC_FECHA_FIN}}, ya no hay lugar en su área. Los lugares se asignaron por orden de antigüedad. Puede aceptar en la Plataforma una de estas fechas de inicio: {{VAC_ALTERNATIVAS}}, o solicitar otras. [FIN SI]

**N-4. Días bloqueados**
Del {{VAC_BLOQUEO_INICIO}} al {{VAC_BLOQUEO_FIN}} no se programarán vacaciones en {{VAC_BLOQUEO_ALCANCE_TEXTO}}, por el siguiente motivo: {{VAC_BLOQUEO_DESCRIPCION}}. [SI la persona tiene vacaciones solicitadas o autorizadas en esas fechas antes de la activación del bloqueo] Las vacaciones que usted ya había solicitado o que ya se le autorizaron en esas fechas no cambian. Si la Empresa le propone moverlas, usted decide si acepta. [FIN SI]

**N-5. Recordatorio de saldo**
Tiene {{VAC_SALDO}} días de vacaciones de su año de servicios número {{VAC_ANTIGUEDAD_ANIOS}}, que debe disfrutar a más tardar el {{VAC_LIMITE_OTORGAMIENTO}}. Solicítelos por la Plataforma.

**N-6. Resolución de su solicitud**
[SI VAC_ESTADO = Autorizado] Sus vacaciones del {{VAC_FECHA_INICIO}} al {{VAC_FECHA_FIN}} fueron autorizadas. [FIN SI]
[SI VAC_ESTADO = Reprogramado] Se le propone otra fecha para sus vacaciones. Revísela en la Plataforma: puede aceptarla o solicitar otras fechas. [FIN SI]
[SI VAC_ESTADO = Devuelto] Su solicitud requiere una corrección: {{DEVOLUCION_MOTIVO}}. [FIN SI]

**Notas para programación**
- `VAC_SALDO_RESUMEN`: una línea por cada periodo con saldo: «N días del año de servicios número X, a disfrutar a más tardar el [fecha]» (con 1, «1 día»).
- `VAC_BLOQUEOS_RESUMEN`: una línea por cada bloqueo Activo del año que aplica a la persona: «del [fecha] al [fecha]: [descripción]».
- `VAC_BLOQUEO_ALCANCE_TEXTO`: «la Empresa», «el centro de trabajo [nombre]», «el área [nombre]» o «el puesto [nombre]».
- Los avisos nunca mencionan `VAC_FECHA_PRESCRIPCION`.
