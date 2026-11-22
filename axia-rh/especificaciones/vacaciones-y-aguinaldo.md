# AXIA RH — MÓDULO DE VACACIONES Y AGUINALDO

Especificación para programación · Versión 1.4 · 21/11/2026

**Fuentes:**
- «Corte - Módulo de vacaciones y aguinaldo» (21/11/2026).
- «AXIARH - Módulo de vacaciones y aguinaldo - Textos (borrador)», sexta versión del 17/11/2026, sin cambios.
- «AXIARH - Registro de decisiones» y «Axia RH - Mapa del PMV» (21/11/2026; encargos 4 y 5 del módulo 11).
- Especificación del RIT v1.7 (arts. 29 y 35 a 37).
- Especificación del módulo de permisos y licencias v1.9.
- Especificaciones de los módulos 4 (v1.5), 5 (v1.1), 6 y 8 (v1.0) y 9 (v1.1). (Nota de Cerebro, 21/11/2026: hoy rigen los módulos 6 y 8 v1.1 y el kit de PTU v1.2; no cambia nada de esta especificación.)
- Especificación del kit de PTU v1.0 (regla R-4).

**Alcance:** la pantalla «Vacaciones y Aguinaldo».
- Calcula la antigüedad y los días de vacaciones de cada persona.
- Registra las solicitudes y su autorización.
- Controla saldos, plazos y prescripción.
- Calcula la prima vacacional y el aguinaldo.
- Genera VAC-1, VAC-2 y VAC-3.

El módulo 6 valida el pago del aguinaldo y el módulo 4 hace el finiquito; ambos leen de este módulo.

## Cambios respecto de la versión 1.3

Si la v1.3 ya se cargó, basta aplicar esta tabla. No cambia ningún cálculo ni ningún texto.

| # | Sección | Cambio | Origen |
| --- | --- | --- | --- |
| 1 | 10.3 | Se corrige la nota del descanso proporcional. Ya no dice que el módulo 9 lo descuenta en nómina. Ahora dice que una falta confirmada o un día sin goce restan solo su propio día y que ninguno descuenta el proporcional del día de descanso, tampoco en nómina | Encargo 5 del mapa (21/11/2026); decisión del usuario del 21/11/2026 (registro 4.10 y 4.14); módulo 9 v1.1 |
| 2 | Fuentes, 15 | Referencia al módulo 9 v1.1 | Mapa del 21/11/2026 |

## Historial: cambios de la versión 1.3 respecto de la 1.2 (21/11/2026)

| # | Sección | Cambio | Origen |
| --- | --- | --- | --- |
| 1 | 10.3 | `AGUINALDO_COMPUTA` cuenta como no computables solo las faltas confirmadas del módulo 9; las «por confirmar» computan mientras RH no las confirme | Encargo 4 del mapa |
| 2 | 10.3 | La falta confirmada resta solo su propio día; el descanso no resta | Decisión del usuario |
| 3 | 10.3 | `AGUINALDO_COMPUTA` y `PTU_COMPUTA` cambian juntas | Registro 4.7 |
| 4 | 9, 10.4, 10.5, 11 | Alerta por faltas por confirmar; reversión de `AGUINALDO_VALIDADO` | Encargo 4 del mapa |
| 5 | 14.1 | Estado de la falta del módulo 9 | Registro 4.14 |
| 6 | 15, 16 | Dependencias al día | Mapa del 20/11/2026 |
| 7 | 17 | Casos de prueba 22 y 23 | — |

## Historial: cambios de la versión 1.2 respecto de la 1.1 (17/11/2026)

| # | Sección | Cambio | Origen |
| --- | --- | --- | --- |
| 1 | 4.1, 14 | `VAC_PROGRAMACION_MODO` sin valor por omisión; captura única con el RIT | Encargo 1 del mapa |
| 2 | 0, 8, 10, 11, 14 | Base `SALARIO_PERSONA` | Encargo 3 del mapa |
| 3 | 10.5, 9, 17 | Baja con `AGUINALDO_VALIDADO` y sin pago | Encargo 2 del mapa |
| 4 | 4.6, 13, 14 | Bloqueos en borrador; la suficiencia impide activar, no guardar | Registro 5.0 |
| 5 | 0, 3, 6 | Días laborables según la versión de condiciones y MOD-5 | Registro 2 |
| 6 | 0, 2 | Tabla global de parámetros legales | Registro 3 |
| 7 | 12.3 | Concordancia de número | Registro 5.0 |
| 8 | 15 | Permisos v1.6 reconoce este módulo | Registro 4.9 |
| 9 | 4.6, 5, 9, 13, 14, 17 | Prevalece lo que se registra primero frente a un bloqueo | Aclaración del usuario |

---

## 0. Convenciones

- Se aplican las convenciones de la especificación de permisos, sección 0:
  - Variables: `{{MAYÚSCULAS}}`.
  - Condiciones: `[SI …] … [FIN SI]`; las marcas nunca se imprimen.
  - Niveles de captura: **E** empresa, **O** organigrama, **A** alta, **V** evento, **S** calculada, **B** bitácora y **X** consultoría.
- Términos fijos de los textos: «la Empresa» y «la Persona Trabajadora».
- Formato:
  - Fechas largas; montos en MXN con dos decimales.
  - Arial en todos los documentos.
  - PDF generado en el servidor, sin encabezado ni pie del navegador.
- Reglas de pantalla del sistema (registro 5.0):
  - Se resaltan los campos faltantes.
  - Guardar nunca se bloquea; las validaciones solo impiden la versión definitiva o la activación.
  - Las opciones con campos dependientes se preguntan primero y no tienen valor por omisión, salvo que la Ley lo fije.
- **Días laborables:** se toman de la jornada de la versión de condiciones vigente de la persona (registro, sección 2) y de las constancias MOD-5 vigentes del módulo 5.
- **Días hábiles** (plazos de RH): calendario de días inhábiles del módulo 4.
- **Cifras legales:** ningún texto fija cifras que cambian por reforma. La tabla de días, el bloque continuo mínimo y el mínimo de menores viven en `PARAMETROS_LEGALES_VACACIONES`, dentro de la tabla global de parámetros legales con fecha de vigencia. Se activan solo con aprobación humana (módulo 4, 5.3).
- **Salario:** todo cálculo de este módulo usa `SALARIO_PERSONA` de la versión de condiciones vigente de la persona en la fecha que indica cada sección.
- **Fuentes de ausencias justificadas:**
  - Este módulo es la fuente de los días de vacaciones; el módulo de permisos, de los demás eventos.
  - Las faltas vienen del módulo 9 por medio del módulo de permisos, como «por confirmar» o «confirmadas».
  - Nómina, PTU, aguinaldo y análisis de jornada leen de esas fuentes.
  - Un día no puede tener vacaciones y otro evento de día completo; la incapacidad prevalece (sección 6, regla 5, y sección 7).

---

## 1. Arquitectura

1. **Periodo vacacional** (`VAC_PERIODO`): se crea uno por persona en cada aniversario de `FECHA_INICIO`. Contiene los días que corresponden, el saldo, los plazos y el estado.
2. **Registro de vacaciones** (`VAC_FOLIO`): cada bloque de fechas solicitado contra un periodo. Recorre los estados de la sección 5.
3. **Configuración de programación:** modo (4.1), periodos de solicitud por antigüedad (4.5), días bloqueados (4.6) y cupos (4.7).
4. **Cálculo de aguinaldo** (`AGUINALDO_ANIO`): uno por persona y año calendario.
5. **Documentos y avisos:** VAC-1 (registro digital por bloque), VAC-2 (constancia por periodo), VAC-3 (registro digital al terminar cada bloque) y avisos N-1 a N-6 (4.8).

La Persona Trabajadora elige sus fechas. La Empresa no asigna vacaciones. Lo que sí hace:
- ordena el turno para solicitarlas (4.5);
- señala los días en que no pueden programarse (4.6);
- limita cuántas personas de un área pueden ausentarse a la vez (4.7);
- por medio de la cadena, autoriza, devuelve o propone otra fecha.

Toda propuesta de la Empresa requiere la aceptación de la persona.

---

## 2. Parámetros legales (`PARAMETROS_LEGALES_VACACIONES`)

Forman parte de la tabla global de parámetros legales: versionada, con fecha de vigencia, monitor de fuentes oficiales y aprobación humana. Solo consultoría (X) la edita y solo se aplican los valores aprobados. Valores vigentes desde el 1/01/2023 (arts. 76, 78 y 179 LFT):

| Años de servicios cumplidos | Días laborables |
| --- | --- |
| 1 | 12 |
| 2 | 14 |
| 3 | 16 |
| 4 | 18 |
| 5 | 20 |
| 6 a 10 | 22 |
| 11 a 15 | 24 |
| 16 a 20 | 26 |
| 21 a 25 | 28 |
| 26 a 30 | 30 |
| 31 a 35 | 32 |
| Cada 5 años adicionales | + 2 |

| Parámetro | Valor |
| --- | --- |
| Bloque continuo mínimo (`VAC_BLOQUE_MINIMO`) | 12 días laborables |
| Mínimo para menores de 18 años (`VAC_MINIMO_MENORES`) | 18 días laborables |
| Plazo para conceder (`VAC_MESES_OTORGAMIENTO`) | 6 meses |
| Plazo de prescripción adicional (`VAC_MESES_PRESCRIPCION`) | 12 meses, contados desde el fin del plazo para conceder |

Un valor nuevo aprobado aplica a los periodos cuyo aniversario cae dentro de su vigencia o después. Los periodos anteriores conservan sus días.

---

## 3. Periodos vacacionales

### 3.1 Creación

- El periodo N se crea en `VAC_ANIVERSARIO` = `FECHA_INICIO` + N años. Si la fecha de inicio es 29 de febrero, en años no bisiestos el aniversario es el 28 de febrero.
- `VAC_ANTIGUEDAD_ANIOS` = N.
- `VAC_DIAS_PERIODO` se calcula así:
  1. Días de la tabla para N años.
  2. Si la persona es menor de 18 años en el aniversario (edad tomada de la CURP): el mayor entre los días de la tabla y `VAC_MINIMO_MENORES`.
  3. Con contrato de temporada (tipo D) o servicios discontinuos:
     - `VAC_PROPORCIONAL` = Sí.
     - Días = días de la tabla × días trabajados en el año de servicios ÷ 365, redondeado hacia arriba al entero.
     - Los días trabajados son los de relación activa, sin los de suspensión por fin de temporada.
  4. Suspensiones largas (B4, B5, D2, D3) del módulo de permisos dentro del año de servicios:
     - Los años siempre cuentan (decisión 7 de permisos).
     - Los días de la tabla se reducen en proporción a los días de suspensión: días de la tabla × (365 − días de suspensión) ÷ 365, redondeado hacia arriba.
     - Excepción: si RH marcó `SUSP_VACACIONES_GENERA` = Sí, se suman los `VACACIONES_DIAS_GENERADOS` que capturó, sin exceder los días que quitó la reducción (lectura confirmada con permisos, v1.7).
     - Ningún otro evento reduce los días: ni las incapacidades ni las faltas.
- `VAC_LIMITE_OTORGAMIENTO` = aniversario + `VAC_MESES_OTORGAMIENTO` (mismo día del mes; si ese día no existe, el último día del mes).
- `VAC_FECHA_PRESCRIPCION` = `VAC_LIMITE_OTORGAMIENTO` + `VAC_MESES_PRESCRIPCION`.
- Al crearse el periodo se genera VAC-2 (sección 12).

### 3.2 Saldo y estado del periodo

- `VAC_SALDO` = `VAC_DIAS_PERIODO` − días de bloques Autorizados, En curso o Disfrutados + `VAC_DIAS_INTERRUMPIDOS` devueltos.
- Los días de bloques Solicitados, En asignación o En autorización se muestran como «comprometidos» y no se pueden volver a solicitar.
- `VAC_ESTADO_SALDO`:

| Estado | Condición | Efecto |
| --- | --- | --- |
| Vigente | Hoy ≤ `VAC_LIMITE_OTORGAMIENTO` | Se solicita normalmente |
| Fuera de plazo | `VAC_LIMITE_OTORGAMIENTO` < hoy ≤ `VAC_FECHA_PRESCRIPCION` y saldo > 0 | Se puede solicitar; cada solicitud genera una alerta a RH y consultoría (art. 81) |
| Prescrito | Hoy > `VAC_FECHA_PRESCRIPCION` y saldo > 0 | Cambio automático, registrado en bitácora. No se solicita ni se paga; no se borra. El módulo 4 lo muestra solo como dato informativo |
| Agotado | Saldo = 0 | Cerrado |

- Ningún documento llama «caducidad» al paso a Prescrito.
- Una persona puede tener saldo en varios periodos. Las solicitudes se cargan primero al periodo más antiguo con saldo; la persona puede elegir otro periodo vigente.

### 3.3 Reingreso

- El reingreso es una relación nueva: nueva `FECHA_INICIO` y periodos desde el año 1. Los periodos anteriores quedan cerrados en el historial.
- Si el reingreso ocurre dentro de `REINGRESO_ALERTA_DIAS` naturales después de la baja anterior, se envía a consultoría una alerta, sin bloqueo: «Reingreso cercano a la baja: revise el riesgo de continuidad de la relación».
- No hay vacaciones anticipadas: antes del primer aniversario no hay periodo ni saldo.

---

## 4. Programación de fechas

### 4.1 Modos (`VAC_PROGRAMACION_MODO`, E)

**Captura:**
- Se captura una sola vez en la configuración de la empresa. La comparten el art. 36 del RIT y este módulo.
- No tiene valor por omisión: es obligatoria y se pregunta antes que sus campos dependientes, que solo aparecen al elegir el modo.
- Mientras no se elija, la pantalla de vacaciones solo admite solicitudes con `VAC_ORIGEN` = Solicitud y muestra el aviso «Elija el modo de programación de vacaciones en la configuración de la empresa».
- Cambiar el modo con el RIT depositado genera la alerta «RIT modificado: pendiente de depósito».

| Modo | Campos dependientes | Funcionamiento |
| --- | --- | --- |
| Calendario anual | `MES_CALENDARIO_VACACIONES`, `VAC_PREFERENCIAS_DIAS` | En los `VAC_PREFERENCIAS_DIAS` días naturales anteriores a `MES_CALENDARIO_VACACIONES`, cada persona registra sus fechas preferidas. Cada preferencia se convierte en una solicitud con `VAC_ORIGEN` = Calendario y pasa por la cadena. RH publica el calendario cuando todas están resueltas. Las preferencias no requieren `DIAS_ANTICIPACION_VACACIONES` |
| Periodos de solicitud por antigüedad | `VAC_ANIO_PROGRAMACION`, `VAC_PERIODOS_SOLICITUD` | La Empresa fija, para cada año, periodos de solicitud por grupos de antigüedad. Las solicitudes de cada grupo se asignan al cierre de su periodo, por antigüedad y conforme a los cupos (4.5). `VAC_ORIGEN` = Periodo de solicitud. El art. 36 del RIT ya prevé este modo (v1.5 y siguientes) |
| A solicitud | — | Sin calendario ni periodos de solicitud. `VAC_ORIGEN` = Solicitud |

Los días bloqueados (4.6), los cupos (4.7) y las notificaciones (4.8) aplican en los tres modos.

### 4.2 Solicitud

- La persona elige el periodo, la fecha de inicio y la fecha de fin. El sistema calcula `VAC_DIAS` y muestra el saldo resultante.
- `VAC_DIAS` cuenta los días laborables del rango. Excluye los descansos, los días de descanso obligatorio y los días bloqueados que le aplican.
- El calendario de selección marca desde el inicio los días bloqueados activos y los días sin cupo en el área de la persona.
- Las validaciones están en la sección 6.
- Con Periodos de solicitud por antigüedad, si la solicitud se hace dentro del periodo de solicitud de la persona, queda En asignación hasta el cierre (4.5). En los demás casos pasa directo a En autorización.

### 4.3 Cadena de autorización

Es la de la especificación de permisos, sección 3.4. «Vacaciones» es un concepto de la cadena, con su propia columna «Autorizan».
- Por omisión se usa la cadena completa: jefatura inmediata, RH y dirección del área, si existe.
- Se aplican igual:
  - `AUTORIZACION_PLAZO_DIAS`;
  - el suplente;
  - la regla de que nadie autoriza lo propio;
  - la regla de un solo paso cuando la misma persona ocupa dos.

Diferencias:

| Acción | Disponible | Requisitos | Efecto |
| --- | --- | --- | --- |
| Autorizar | Todos los pasos | — | Pasa al siguiente paso; en el último, queda Autorizado |
| Reprogramar | Todos los pasos | `NEGATIVA_CAUSA` (Requisitos no subsanados · Necesidad operativa concreta), `NEGATIVA_MOTIVO` y `FECHA_ALTERNA` | Estado Reprogramado: la Plataforma propone a la persona la nueva fecha de inicio, con los mismos días. Si acepta, la solicitud se reinicia con las fechas nuevas en el paso siguiente al que reprogramó. Si no acepta, la solicitud se cancela y puede pedir otras fechas. Si reprogramó la jefatura, la persona puede pedir a RH que lo revise; RH resuelve el mismo día |
| Devolver para corrección | Todos los pasos | `DEVOLUCION_MOTIVO` | Estado Devuelto; al corregirse, reinicia en el paso que devolvió |
| Negar | **No existe** | — | — |

- La `FECHA_ALTERNA` cumple las mismas validaciones que una solicitud (sección 6), incluidos los días bloqueados y los cupos.
- El bloque reprogramado debe terminar a más tardar en `VAC_LIMITE_OTORGAMIENTO` si el periodo está Vigente, o en `VAC_FECHA_PRESCRIPCION` si está Fuera de plazo.
- Un bloqueo activado después de la solicitud no es causa para devolverla ni para reprogramarla (4.6, regla 3). La cadena no puede usarlo como motivo.
- Si llega la fecha de inicio sin resolución y la solicitud se hizo con la anticipación debida, se envía una alerta a RH, que resuelve ese mismo día. Mientras tanto, la ausencia no se marca como falta.
- La persona puede cancelar su solicitud mientras el bloque no haya iniciado.
- Cada paso queda en la bitácora. `AUTORIZACIONES` (S) arma la lista que imprime VAC-1.

### 4.4 (Sustituida por 4.8)

### 4.5 Periodos de solicitud por antigüedad

Solo aplica con `VAC_PROGRAMACION_MODO` = Periodos de solicitud por antigüedad.

**Configuración (`VAC_PERIODOS_SOLICITUD`, E, una tabla por año de vacaciones `VAC_ANIO_PROGRAMACION`):**

| Columna | Tipo | Validación |
| --- | --- | --- |
| Grupo (`VAC_GRUPO_NOMBRE`) | Texto | Obligatorio; único en el año |
| Antigüedad desde (años) | Entero ≥ 0 | — |
| Antigüedad hasta (años) | Entero o vacío (sin límite) | ≥ «desde» |
| Apertura (`VAC_SOLICITUD_INICIO`) | Fecha | — |
| Cierre (`VAC_SOLICITUD_FIN`) | Fecha | ≥ apertura |

Reglas de configuración. La tabla siempre se guarda; si no cumple estas reglas, no se puede publicar:
1. Los rangos de antigüedad cubren de 0 años en adelante, sin huecos ni traslapes.
2. Los periodos de solicitud no se traslapan y siguen un orden fijo, que no se puede editar: abre primero el grupo de mayor antigüedad.
3. El sistema avisa, sin bloquear, si algún periodo de solicitud cierra después del `VAC_LIMITE_OTORGAMIENTO` de una persona del grupo con saldo vigente.
4. La tabla publicada se puede editar hasta la apertura de su primer periodo de solicitud. Después, solo se pueden ampliar las fechas de cierre de los periodos que no han cerrado, y cada cambio queda en la bitácora.

**Pertenencia al grupo:**
- Cada persona pertenece al grupo de sus años de servicios cumplidos a la apertura del primer periodo de solicitud del año.
- Los años se cuentan desde `FECHA_INICIO`; en un reingreso, desde la nueva fecha.
- La persona ve su grupo y las fechas de su periodo de solicitud desde que se publica la tabla.

**Qué se solicita:**
- Fechas del año `VAC_ANIO_PROGRAMACION`, cargadas a periodos vacacionales que ya existan en la fecha de inicio de las vacaciones (no hay vacaciones anticipadas).
- Si el periodo aún no existe al solicitar, la solicitud se admite cuando su aniversario cae antes de la fecha de inicio de las vacaciones. El saldo se valida con los días que tendrá ese periodo.

**Asignación al cierre de cada periodo de solicitud:**
1. El sistema toma las solicitudes En asignación: las del grupo que cierra y las pendientes de grupos anteriores (punto 4).
2. Las ordena por antigüedad, de mayor a menor (`FECHA_INICIO` más antigua primero). En caso de empate, por la fecha y hora de la solicitud.
3. En ese orden, verifica el cupo de cada día de la solicitud (4.7):
   - Si todos los días tienen lugar, la solicitud reserva el cupo y pasa a En autorización.
   - Si algún día no tiene lugar, pasa a Reprogramado con `NEGATIVA_CAUSA` = Cupo completo. El sistema propone hasta tres fechas de inicio alternativas (`VAC_ALTERNATIVAS`), con los mismos días, que cumplen todas las validaciones y quedan dentro del plazo del periodo.
4. La persona puede aceptar una alternativa o pedir otras fechas. Si pide otras mientras siga abierto algún periodo de solicitud posterior, su solicitud vuelve a En asignación y compite con su propia antigüedad en el siguiente cierre.
5. Sin cupos configurados, todas las solicitudes pasan a En autorización al cierre.
6. La asignación y su orden quedan en la bitácora: por cada cierre, persona, antigüedad, fechas y resultado.
7. Una solicitud En asignación que quedó protegida frente a un bloqueo (4.6, regla 3) compite por el cupo normalmente; el bloqueo no le resta lugar ni la excluye.

**Antes y después de los periodos de solicitud:**
- Antes de que abra su periodo de solicitud, la persona no puede solicitar fechas de `VAC_ANIO_PROGRAMACION`. Sí puede solicitar fechas del año en curso que no forman parte de la programación.
- Al cerrar el último periodo de solicitud, cualquier persona puede pedir los días que le queden en fechas libres. Esas solicitudes se atienden por orden de llegada, conforme a los cupos (`VAC_ORIGEN` = Solicitud).
- Quien no solicitó en su periodo de solicitud no pierde días: recibe los avisos de la sección 4.8 y puede solicitar después.

### 4.6 Días bloqueados (`VAC_BLOQUEOS`, E/V, todos los modos)

RH registra los días en que no pueden programarse vacaciones.

| Campo | Tipo | Validación |
| --- | --- | --- |
| Fecha de inicio y de fin | Fechas | Fin ≥ inicio |
| Alcance (`VAC_BLOQUEO_ALCANCE`) | Empresa · Centro de trabajo · Área · Puesto, con la selección correspondiente | Obligatorio |
| Motivo (`VAC_BLOQUEO_MOTIVO`) | Operativo · Capacitación | Obligatorio |
| Descripción (`VAC_BLOQUEO_DESCRIPCION`) | Texto | Obligatoria; se muestra a las personas |
| Estado (`VAC_BLOQUEO_ESTADO`) | Borrador · Activo | Borrador al guardar |
| Registro | Usuario, fecha y hora de guardado y de activación (`VAC_BLOQUEO_ACTIVACION`) | Bitácora |

Reglas:

1. **Guardar y activar:**
   - El bloqueo siempre se guarda en Borrador (registro 5.0).
   - Un bloqueo en Borrador no surte efectos: no limita solicitudes, no aparece en VAC-2 y no se notifica.
   - Solo pasa a Activo con el botón «Activar», que aplica la validación de suficiencia.
   - La fecha y hora de activación (`VAC_BLOQUEO_ACTIVACION`) es la que se compara en la regla 3.
2. **Suficiencia (impide activar):**
   - No se activa un bloqueo si, para alguna persona de su alcance con saldo Vigente, los días laborables libres entre hoy (o su aniversario, si es posterior) y su `VAC_LIMITE_OTORGAMIENTO` dejan de alcanzar para su saldo.
   - El cálculo incluye un bloque continuo de `VAC_BLOQUE_MINIMO` días, o del saldo si es menor.
   - Se consideran libres los días sin bloqueos activos y sin vacaciones solicitadas o autorizadas que los ocupen.
   - La pantalla muestra la lista de personas afectadas para que RH ajuste las fechas o el alcance.
3. **Prevalece lo que se registra primero (aclaración del usuario, 17/11/2026; registro 4.10):**
   - **Bloqueo primero.** Si el bloqueo se activó antes de la solicitud, los días bloqueados no pueden solicitarse (sección 6, regla 9).
   - **Solicitud primero.** Si la persona solicitó antes de la activación (`EVENTO_SOLICITUD_FECHAHORA` < `VAC_BLOQUEO_ACTIVACION`), el bloqueo no le aplica en esas fechas. La protección cubre las solicitudes en estado Solicitado, En asignación, En autorización, Devuelto, Reprogramado, Autorizado o En curso, y las preferencias del calendario anual ya registradas.
   - **Qué no hace el bloqueo con esas vacaciones:**
     - No las cancela, no las devuelve, no las mueve.
     - No es motivo para que la cadena las reprograme.
     - La solicitud sigue su curso normal; la cadena la resuelve con las reglas de 4.3 como si el bloqueo no existiera.
     - En la asignación por antigüedad compite por el cupo normalmente.
   - **Propuesta de la Empresa.** RH puede enviar a la persona una propuesta para moverlas (estado Reprogramado, causa Necesidad operativa concreta). Si la persona no acepta, conserva sus fechas y la solicitud sigue su curso.
   - Las fechas protegidas quedan en `VAC_BLOQUEO_EXCEPCIONES`.
   - **Cuándo se pierde la protección:**
     - Si la persona cancela la solicitud o no acepta una propuesta de la cadena hecha por otra causa (cupo o necesidad operativa ajena al bloqueo), la protección termina. Las fechas nuevas que pida se validan contra los bloqueos activos en ese momento.
     - Al corregir una solicitud devuelta, la protección se conserva solo en las fechas que ya estaban en la solicitud original.
4. **Lista al activar:** al activar un bloqueo, el sistema muestra a RH las vacaciones solicitadas o autorizadas que quedan dentro de él, todas protegidas por la regla 3, con el botón «Proponer reprogramación».
5. **Aviso:** al activarse un bloqueo, las personas de su alcance reciben el aviso N-4 (4.8). Quien tiene fechas protegidas recibe el párrafo de que sus vacaciones no cambian.
6. **Cambios:**
   - Un bloqueo activo puede eliminarse o acortarse en cualquier momento, con registro en la bitácora.
   - Ampliarlo lo regresa a Borrador para validar de nuevo la suficiencia. Mientras tanto, sigue vigente con sus fechas anteriores.
   - Los días añadidos por la ampliación cuentan como bloqueo nuevo para la regla 3: su activación es la de la ampliación.
7. **Cálculo de días:** los días bloqueados no consumen vacaciones; una solicitud no puede incluirlos, salvo las fechas protegidas (sección 6, regla 9).

### 4.7 Cupos por área (`VAC_CUPOS`, E, opcional, todos los modos)

| Campo | Tipo | Validación |
| --- | --- | --- |
| Alcance | Centro de trabajo · Área · Puesto, con la selección correspondiente | Obligatorio |
| Máximo de personas de vacaciones el mismo día (`VAC_CUPO_MAXIMO`) | Entero ≥ 1 | Obligatorio |

- Para un día y un alcance, ocupan cupo los bloques Autorizados y En curso, y las solicitudes que ya lo reservaron (En autorización). Si una persona cae en varios alcances con cupo, debe cumplir todos.
- Con Periodos de solicitud por antigüedad, el cupo se asigna por antigüedad al cierre de cada periodo de solicitud (4.5). En los demás modos, y fuera de esos periodos, se asigna por orden de llegada.
- Sin cupos configurados no hay límite.
- El sistema avisa, sin bloquear, si el cupo hace imposible que todas las personas del alcance disfruten su saldo dentro de su plazo: días laborables del año × cupo < suma de los saldos del alcance.

### 4.8 Notificaciones (todos los modos)

- **Canales** (`VAC_NOTIFICACION_CANALES`, E): Correo personal · App · Ambos (por omisión, Ambos). La Plataforma siempre muestra el aviso en «Pendientes». El correo se envía a `TRAB_EMAIL`.
- **App:** es fase 2 según el mapa del PMV. Mientras no exista, el canal «App» equivale a la notificación en la Plataforma; cuando exista, se envía además como notificación push.
- **Bitácora:** cada envío queda registrado con fecha, hora, canal, destinatario y resultado de la entrega. Es la evidencia de que la Empresa ofreció las vacaciones (art. 784, fr. X).
- Los textos fijos de N-1 a N-6 están en el documento de textos.

| Aviso | Momento | Modo | Destinatarios |
| --- | --- | --- | --- |
| N-1 Apertura del periodo de solicitud | Al abrir el periodo de solicitud del grupo | Periodos de solicitud | P |
| N-2 Cierre próximo | 3 días hábiles antes del cierre, si la persona tiene saldo y no ha solicitado | Periodos de solicitud | P |
| N-3 Resultado de la asignación | Al cierre del periodo de solicitud | Periodos de solicitud | P |
| N-4 Días bloqueados | Al activar un bloqueo | Todos | P del alcance; J |
| N-5 Recordatorio de saldo | 60 y 30 días naturales antes de `VAC_LIMITE_OTORGAMIENTO`, con saldo sin programar | Todos | P; copia a J y RH |
| N-6 Resolución de la solicitud | Al quedar Autorizado, Reprogramado o Devuelto | Todos | P |

---

## 5. Estados del registro (`VAC_ESTADO`)

| Estado | Significado | Transiciones |
| --- | --- | --- |
| Solicitado | Capturado por la persona, o por RH desde el formato de respaldo | → En asignación (Periodos de solicitud, dentro del periodo), En autorización, Cancelado |
| En asignación | Espera el cierre del periodo de solicitud (4.5) | → En autorización (con cupo), Reprogramado (cupo completo), Cancelado |
| En autorización | Recorre la cadena | → Autorizado, Reprogramado, Devuelto, Cancelado |
| Devuelto | La cadena pidió corregir | → En autorización o En asignación (al corregir), Cancelado |
| Reprogramado | Propuesta de otra fecha (de la cadena, por cupo o por propuesta de RH ante un bloqueo), pendiente de aceptación | → En autorización o En asignación (si acepta); si no acepta: Cancelado, salvo que la propuesta fuera de RH ante un bloqueo, en cuyo caso regresa al estado anterior con sus fechas (4.6, regla 3) |
| Autorizado | Aprobado por la cadena | → En curso; Cancelado (por la persona, antes del inicio); Reprogramado (incapacidad antes del inicio, 7.2, o propuesta de RH ante un bloqueo, 4.6) |
| En curso | Fecha de inicio alcanzada | → Disfrutado, Interrumpido |
| Interrumpido | Incapacidad durante el bloque (7.1) | → Disfrutado (por los días anteriores a la incapacidad) |
| Disfrutado | Terminó el bloque | Genera VAC-3; fin |
| Cancelado | Cancelado por la persona o por no aceptar una propuesta de la cadena | Fin; se liberan los días comprometidos y el cupo reservado |

La activación de un bloqueo no cambia el estado de ninguna solicitud. Cada cambio de estado queda en la bitácora con usuario, fecha y hora.

---

## 6. Validaciones

1. **Saldo:** `VAC_DIAS` ≤ saldo disponible del periodo, descontados los días comprometidos. Bloqueo.
2. **Periodo prescrito:** no se puede solicitar. Bloqueo.
3. **Anticipación:**
   - La fecha de inicio debe estar al menos `DIAS_ANTICIPACION_VACACIONES` días naturales después de la solicitud.
   - No aplica a las preferencias del calendario ni a las solicitudes hechas dentro de un periodo de solicitud.
   - Si no se cumple, no hay bloqueo: el sistema avisa a la persona y la cadena puede devolver o reprogramar con la causa «Requisitos no subsanados».
4. **Bloque continuo:**
   - Cada periodo debe tener, entre sus bloques Autorizados o Disfrutados, al menos uno continuo de `VAC_BLOQUE_MINIMO` días laborables, o del saldo total si es menor.
   - Si una solicitud deja el saldo restante por debajo del bloque mínimo y todavía no existe un bloque continuo, el sistema pregunta a la persona si quiere fraccionarlo.
   - Si confirma, la solicitud continúa, la confirmación queda en la bitácora y se envía una alerta a consultoría, sin bloqueo.
5. **Traslape con eventos:**
   - No se pueden solicitar vacaciones en días con evento de día completo de las familias C o D, de la familia B (salvo B1, lactancia) ni en días con otro bloque de vacaciones. Bloqueo.
   - Si después se registra un evento C sobre días de vacaciones, rige la sección 7.
6. **Días laborables:** según la jornada de la versión de condiciones de la persona y las constancias MOD-5 vigentes en cada fecha. Bloqueo si el rango no contiene días laborables.
7. **Relación vigente:** no se puede solicitar con baja registrada ni con fecha de inicio posterior a `BAJA_FECHA`.
8. **Primer aniversario:** no hay vacaciones antes del primer aniversario. Bloqueo.
9. **Días bloqueados:**
   - El rango no puede incluir días laborables con un bloqueo Activo que aplique a la persona y que se haya activado antes de la solicitud. Bloqueo.
   - Las fechas protegidas de `VAC_BLOQUEO_EXCEPCIONES` no se rechazan (4.6, regla 3).
   - El calendario de selección no permite elegir días bloqueados para una solicitud nueva.
10. **Cupo:** fuera de la asignación por antigüedad, no se admite una solicitud que exceda el cupo en algún día; el sistema muestra los días sin lugar y propone hasta tres fechas alternativas. Bloqueo.
11. **Periodo de solicitud:** con Periodos de solicitud por antigüedad, antes de que abra el periodo de solicitud de la persona no se admiten fechas de `VAC_ANIO_PROGRAMACION`. Bloqueo, con el mensaje «Su periodo de solicitud abre el {{VAC_SOLICITUD_INICIO}}».

Las validaciones 1 a 11 impiden enviar la solicitud, no guardarla: la persona puede guardar un borrador de solicitud (registro 5.0). Un borrador no es solicitud: no se protege frente a un bloqueo hasta que se envía.

---

## 7. Incapacidad e interrupción

### 7.1 Incapacidad durante el bloque

Si el módulo de permisos registra un evento C1, C2 o C3 cuyo certificado inicia en un día de un bloque En curso:

1. El bloque pasa a Interrumpido. `VAC_INTERRUPCION_FECHA` = inicio del certificado.
2. `VAC_DIAS_INTERRUMPIDOS` = días laborables del bloque desde esa fecha hasta su fin.
3. Esos días regresan al saldo del mismo periodo y se libera su cupo. Si el periodo vence o prescribe mientras dura la incapacidad:
   - `VAC_LIMITE_OTORGAMIENTO` y `VAC_FECHA_PRESCRIPCION` no se extienden;
   - se envía una alerta a RH y a consultoría para que la persona solicite esos días en cuanto regrese.
4. Los días de incapacidad se registran como evento C en el módulo de permisos y dejan de ser vacaciones (la incapacidad prevalece).
5. **Nómina:** el salario de vacaciones y la prima ya pagados por esos días quedan «a cuenta» de los días devueltos y no se pagan de nuevo cuando se disfruten. El sistema muestra el importe a cuenta al contador.
6. VAC-1 imprime el apartado III. VAC-3 se genera por los días disfrutados.
7. Los días devueltos se solicitan como solicitud nueva: se validan contra los bloqueos activos en la fecha de esa solicitud.

### 7.2 Incapacidad antes del inicio

Si al llegar la fecha de inicio de un bloque Autorizado hay una incapacidad vigente:
- El bloque no inicia y pasa a Reprogramado, sin fecha alterna.
- Los días vuelven al saldo, se libera el cupo y la persona solicita nuevas fechas al regresar.
- Si la prima ya se pagó, queda a cuenta, igual que en 7.1.

### 7.3 Datos

No se captura diagnóstico. Este módulo solo lee del certificado la fecha de inicio, la fecha de fin y el ramo.

---

## 8. Pago de vacaciones y prima

- `VAC_SALARIO_BASE` = `SALARIO_PERSONA` de la versión de condiciones vigente de la persona al iniciar el bloque. Es el salario ordinario, no el integrado.
- Salario de vacaciones = `VAC_SALARIO_BASE` × `VAC_DIAS`. Nómina lo paga en el periodo de pago que corresponda.
- `VAC_PRIMA_MONTO` = `VAC_SALARIO_BASE` × `VAC_DIAS` × `PRIMA_VACACIONAL_PCT` ÷ 100.
- Momento de la prima (`MOMENTO_PAGO_PRIMA`):
  - Con «al inicio del periodo», se envía a la nómina del periodo en que inicia el bloque.
  - Con «en la nómina inmediata anterior», a la nómina anterior al inicio.
- Interfaz con nómina, por bloque: persona, periodo, fechas, `VAC_DIAS`, `VAC_SALARIO_BASE`, `VAC_PRIMA_MONTO`, periodo de pago de la prima e importes a cuenta (7.1).
- `VAC_CFDI_UUID`: lo devuelve nómina o lo captura RH. Si no llega dentro de los 10 días hábiles siguientes al fin del bloque, se envía una alerta a RH, sin bloqueo.
- Mientras exista la relación, el sistema no ofrece pagar vacaciones sin disfrutarlas (art. 79).

---

## 9. Plazos y alertas

Destinatarios: **P** Persona Trabajadora, **J** jefatura, **RH**, **C** consultoría, **Ct** contador.

| Evento | Momento | Destinatarios | Acción |
| --- | --- | --- | --- |
| Modo de programación sin elegir | Al entrar a la pantalla | RH, C | «Elija el modo de programación de vacaciones» (4.1) |
| Periodo nuevo | Aniversario | P, RH | VAC-2 para firma o acuse |
| VAC-2 sin firma o acuse | 3 días hábiles después del envío | RH | Reenvío; negativa con testigos si procede |
| Ventana de preferencias (Calendario anual) | Inicio de `VAC_PREFERENCIAS_DIAS` | P | Aviso para registrar preferencias |
| Tabla de periodos de solicitud sin publicar | 60 días naturales antes del 1 de enero de `VAC_ANIO_PROGRAMACION` | RH | «Configure y publique los periodos de solicitud del año» |
| Apertura, cierre próximo y resultado de la asignación | Avisos N-1 a N-3 (4.8) | P | Avisos |
| Bloqueo activado | Al activarlo | P, J (N-4); RH (lista de vacaciones solicitadas o autorizadas protegidas dentro del bloqueo) | 4.6 |
| Bloqueo en borrador sin activar | 3 días hábiles después de guardarlo | RH | «Bloqueo sin activar: no surte efectos» |
| Cupo imposible | Al guardar el cupo | RH | Aviso (4.7) |
| Recordatorio de saldo | 60 y 30 días antes de `VAC_LIMITE_OTORGAMIENTO` | P, J, RH | N-5 |
| Límite para conceder vencido con saldo | `VAC_LIMITE_OTORGAMIENTO` | RH, C (crítica) | «Plazo legal para conceder vencido (art. 81)» |
| Solicitud con periodo Fuera de plazo | Al solicitar | RH, C | Informativa |
| Prescripción próxima | 90 días antes de `VAC_FECHA_PRESCRIPCION` | RH | Informativa |
| Prescripción | `VAC_FECHA_PRESCRIPCION` | RH, C | Paso automático a Prescrito |
| Paso de la cadena sin resolver | `AUTORIZACION_PLAZO_DIAS` | Autorizador, RH | Igual que en permisos |
| Inicio sin resolución | Fecha de inicio | RH | RH resuelve ese día |
| VAC-3 sin confirmación | `VAC_CONFIRMACION_DIAS` días hábiles después del regreso | RH | Recabar el formato de respaldo |
| VAC-3 «No estoy de acuerdo» | Al marcarlo | RH | Revisar y responder |
| Incapacidad que interrumpe | Al registrarse | RH, Ct | Días devueltos e importe a cuenta |
| Fraccionamiento del bloque mínimo | Al confirmarlo la persona | C | Informativa |
| Reingreso cercano | Al dar el alta | C | 3.3 |
| Aguinaldo | 30 días antes de `AGUINALDO_FECHA_PAGO` | RH, Ct | Cálculo provisional para revisión (10.4) |
| Faltas por confirmar en el aguinaldo | En el cálculo provisional y cada vez que se recalcula, si alguna persona tiene faltas por confirmar en el año | RH | «{{N}} faltas por confirmar en el año: confírmelas o descártelas antes de la validación del contador; mientras no se confirmen, cuentan como días computables» (10.4). Sin bloqueo |
| Baja con aguinaldo validado y sin pago | Al registrar la baja | Ct | «La persona sale de la nómina anual de aguinaldo; se paga en el finiquito» (10.5) |
| Faltas por confirmar a la baja | Al registrar la baja, si hay faltas por confirmar en el año | RH | Misma alerta, para el aguinaldo proporcional del finiquito (10.5). Sin bloqueo |

---

## 10. Aguinaldo

### 10.1 Parámetros

- `AGUINALDO_DIAS` (E): entero ≥ 15; por omisión, 15. Si el puesto tiene más días en `PRESTACIONES_EXTRA`, rige el mayor.
- `AGUINALDO_FECHA_PAGO` (E): día y mes, a más tardar el 19 de diciembre; por omisión, el 15 de diciembre. Si cae en día inhábil, se paga el día hábil anterior.

### 10.2 Cálculo

- **Periodo:**
  - `AGUINALDO_PERIODO_INICIO` es la fecha más reciente entre el 1 de enero y `FECHA_INICIO`; el fin es el 31 de diciembre.
  - El cálculo se hace al 31 de diciembre y considera computables los días que van de la fecha de cálculo al 31 de diciembre.
  - No se recalcula ni se descuenta por lo que ocurra después del pago.
- `AGUINALDO_DIAS_COMPUTABLES` = días naturales del periodo − días de eventos con `AGUINALDO_COMPUTA` = No.
- `AGUINALDO_SALARIO_BASE` = `SALARIO_PERSONA` de la versión de condiciones vigente de la persona en `AGUINALDO_FECHA_PAGO`.
- `AGUINALDO_MONTO` = `AGUINALDO_DIAS` × `AGUINALDO_DIAS_COMPUTABLES` ÷ días del año (365 o 366) × `AGUINALDO_SALARIO_BASE`, redondeado a centavos.

### 10.3 `AGUINALDO_COMPUTA` (tabla global, E; la administra este módulo)

Usa el mismo criterio que los días computables de la PTU (registro 4.7). La especificación de permisos la lee de este módulo.

| Concepto | Computa |
| --- | --- |
| Días laborados, descansos semanales y días de descanso obligatorio | Sí |
| Vacaciones (este módulo) | Sí |
| A1, A2, B2 | Sí |
| A3 con goce / A3 sin goce | Sí / No |
| A4 con goce / A4 sin goce o reclasificado | Sí / No |
| B1 lactancia | Sí |
| B3 licencia del IMSS por hijo con cáncer | No |
| B4, B5 | No |
| C1 enfermedad general | No; sí en los días de espera que paga la Empresa con `PAGO_DIAS_ESPERA` = Sí |
| C2 riesgo de trabajo, C3 maternidad | Sí |
| D1 | No; sí por la fr. III, solo si RH marca que se acreditó que la persona obró en defensa de la Empresa |
| D2, D3, D5 | No |
| D4 sin reubicación / D4 con reubicación aceptada (MOD-5) | No / Sí (los días cuentan como trabajados, permisos v1.8) |
| **Falta confirmada** (módulo 9, recibida por el módulo de permisos) | No |
| **Falta por confirmar** (módulo 9) | Sí, mientras RH no la confirme |
| Suspensión disciplinaria (FD-3 del RIT) | No |
| Suspensión por fin de temporada (módulo 4) | No |

Notas para programación:
- **Faltas (encargo 4 del mapa, 20/11/2026).**
  - Solo descuenta días la falta en estado Confirmada.
  - Una falta por confirmar computa como día normal hasta que RH la confirma.
  - Si una falta, confirmada o no, se borra porque llega un evento justificado (permisos, validación 1), el día se cuenta según ese evento.
- **Descanso (decisión del usuario, 21/11/2026; registro 4.10 y 4.14; módulo 9 v1.1).**
  - Una falta confirmada o un día sin goce restan solo su propio día.
  - Ninguno de los dos descuenta el proporcional del día de descanso, tampoco en nómina.
  - Los días de descanso semanal computan siempre, en el aguinaldo y en la PTU.
- **Tabla gemela.**
  - `AGUINALDO_COMPUTA` y `PTU_COMPUTA` (kit de PTU, R-4) cambian juntas.
  - Tienen dos diferencias deliberadas: los días de espera de C1 pagados por la Empresa y D1 por la fr. III computan para el aguinaldo, pero no para la PTU.
  - Todo cambio en una de las dos se avisa a quien administra la otra.
- Solo consultoría (X) edita la tabla, y cada cambio queda en la bitácora.

### 10.4 Proceso anual

1. 30 días antes de `AGUINALDO_FECHA_PAGO`, el sistema hace un cálculo provisional para todas las personas activas y avisa a RH y al contador.
2. RH revisa los días no computables por persona, con el detalle de los eventos.
   - La pantalla muestra aparte las **faltas por confirmar** de cada persona en el año, con un botón para confirmarlas o descartarlas.
   - Si quedan faltas por confirmar, se envía la alerta de la sección 9. No hay bloqueo.
   - El contador valida (`AGUINALDO_VALIDADO`, V: usuario y fecha). Al validar, la pantalla le muestra cuántas faltas por confirmar quedan.
   - Si después cambia un evento del año de esa persona, se revierte su validación. Cuentan como cambios de evento:
     - la confirmación de una falta;
     - el descarte de una falta;
     - la llegada de un evento justificado que borra una falta.
3. Con la validación, el sistema exporta a nómina la persona, los días computables, el salario base y el importe, y crea en el módulo 6 la obligación de pago de cada persona.
4. El módulo 6 registra el pago y su evidencia (CFDI). Sus alertas (`PAGO_ALERTAS_AGUINALDO`) avisan antes de `AGUINALDO_FECHA_PAGO` si no hay pago.
5. Después del pago, el aguinaldo no se recalcula: una falta del año que se confirme después no se descuenta (10.2).

### 10.5 Bajas

- **Baja antes del pago del año:**
  - El aguinaldo proporcional va en el finiquito (módulo 4), de `AGUINALDO_PERIODO_INICIO` a `BAJA_FECHA`, con la misma tabla de cómputo y con `SALARIO_PERSONA` vigente a la baja.
  - Solo descuentan las faltas confirmadas a la fecha del cálculo. Si hay faltas por confirmar, se envía a RH la alerta de la sección 9, sin bloqueo.
  - La persona sale del cálculo anual.
- **Baja con `AGUINALDO_VALIDADO` y sin pago registrado:**
  - Al registrarse la baja, el sistema avisa al contador: «{{TRAB_NOMBRE}} sale de la nómina anual de aguinaldo; el aguinaldo proporcional se paga en el finiquito».
  - Se retira a la persona de la exportación pendiente.
  - El módulo 6 cancela su obligación de pago de aguinaldo con motivo «Pago en finiquito».
  - Si ya se había exportado a nómina, el aviso pide al contador excluirla de la dispersión.
- **Baja después del pago del año:** el finiquito no incluye el aguinaldo de ese año ni descuenta lo ya pagado.

### 10.6 Fuera de alcance

El ISR y las exenciones del aguinaldo los calcula nómina. El PMV calcula en bruto.

---

## 11. Terminación (interfaz con el módulo 4)

El módulo 4 (v1.5) toma de este módulo, a la fecha de `BAJA_FECHA`:

- Por cada periodo Vigente o Fuera de plazo: saldo de días, salario base (`SALARIO_PERSONA` vigente a la baja) y prima.
- Proporcional del año en curso: días del periodo siguiente × días transcurridos desde el último aniversario (o desde `FECHA_INICIO`, si no ha cumplido el año) ÷ 365. Es la fórmula del caso de prueba A.3 del módulo 4.
- Periodos Prescritos: solo como dato informativo para consultoría; no se suman.
- Aguinaldo: según 10.5, con el número de faltas por confirmar como dato para la pantalla de la baja.

Al registrarse la baja, se cancelan los bloques Autorizados posteriores a `BAJA_FECHA` y las solicitudes pendientes, y se libera su cupo.

---

## 12. Documentos y avisos

### 12.1 Catálogo

| Clave | Pieza | Tipo | Se genera | Firma o acuse |
| --- | --- | --- | --- | --- |
| VAC-1 | Registro de vacaciones | Registro digital | Con cada bloque (calendario, periodo de solicitud o solicitud) y cada reprogramación | Nadie firma; constancia exportable, o formato de respaldo firmado por la persona y por quienes autorizaron |
| VAC-2 | Constancia de antigüedad y periodo vacacional | Documento | En cada aniversario; nueva versión si cambian las fechas del calendario | La persona firma de recibido según `FIRMA_MODALIDAD`; por la Empresa firma la persona designada en `FIRMANTES_EMPRESA`; si hay negativa, dos testigos y envío al correo personal |
| VAC-3 | Constancia de disfrute y pago de prima | Registro digital | Al terminar cada bloque (Disfrutado o Interrumpido) | La persona elige «Confirmo» o «No estoy de acuerdo» en la Plataforma y RH valida; formato de respaldo en papel |
| N-1 a N-6 | Avisos | Notificación | Según 4.8 | Sin firma; envío registrado en bitácora |

El aguinaldo no tiene documento propio: se acredita con el CFDI en el módulo 6.

### 12.2 Reglas de VAC-2

- Se genera al crearse el periodo (3.1), aunque no haya fechas programadas.
- La tabla de fechas solo se imprime si `VAC_BLOQUES_PROGRAMADOS` > 0.
- Con Periodos de solicitud por antigüedad, imprime el grupo y las fechas del periodo de solicitud de la persona, si aún no cierra; si ya cerró, imprime que puede solicitar en fechas libres.
- Imprime los días bloqueados que le aplican entre su aniversario y `VAC_LIMITE_OTORGAMIENTO`, solo los que están en estado Activo a la fecha de emisión. Un bloqueo activado después no genera nueva versión: se comunica con N-4.
- Imprime `VAC_LIMITE_OTORGAMIENTO`. **Nunca imprime `VAC_FECHA_PRESCRIPCION`.**
- Solo se emite una nueva versión (`VAC2_VERSION` + 1) cuando cambian las fechas de un bloque del calendario incluido en la versión anterior.

### 12.3 Reglas comunes

- Se usan los bloques de la especificación de permisos, sección 17.1. El folio es `VAC_FOLIO` en VAC-1 y VAC-3, y `VAC_PERIODO` en VAC-2.
- Los registros digitales siguen la sección 12.3 de permisos y la especificación de firma electrónica (v1.4).
- **Concordancia de número** (registro 5.0): con valor 1, singular («1 día», «1 año»); nunca «(s)». Aplica a VAC-1, VAC-2, VAC-3 y a los avisos (por ejemplo, `VAC_SALDO_RESUMEN` y N-5).
- Cada documento generado guarda la versión del modelo con la que se emitió.
- **Paquete probatorio por periodo:**
  - VAC-2.
  - Los VAC-1 y VAC-3 del periodo.
  - Los avisos enviados, con su bitácora.
  - La lista de asignación por antigüedad, si aplica.
  - Los bloqueos activos, con su fecha y hora de activación.
  - Los CFDI.

---

## 13. Pantallas

### 13.1 Portal de la Persona Trabajadora

- **Mis vacaciones:** periodos con días, saldo, días comprometidos, estado, límite para disfrutarlas (`VAC_LIMITE_OTORGAMIENTO`) y la VAC-2 de cada periodo. No muestra `VAC_FECHA_PRESCRIPCION`.
- **Mi periodo de solicitud** (solo con Periodos de solicitud por antigüedad): grupo, apertura, cierre y estado de la asignación.
- **Solicitar:**
  - Calendario con días bloqueados activos (con su descripción), días sin cupo y días no laborables.
  - Muestra al momento los días y el saldo, y aplica las validaciones de la sección 6.
  - Permite guardar un borrador; un borrador no reserva fechas frente a un bloqueo hasta que se envía.
- **Preferencias del calendario** (solo con Calendario anual, durante la ventana).
- **Pendientes:** avisos, propuestas por aceptar (con alternativas), VAC-2 por firmar y VAC-3 por confirmar.

### 13.2 Pantalla de RH «Vacaciones y Aguinaldo»

1. **Tablero de saldos:** una fila por persona y periodo, con aniversario, días, saldo, estado, límite y prescripción. Filtros por centro, área, grupo y estado; exportación.
2. **Calendario:** vista mensual por área, con bloques, bloqueos (activos y en borrador, distinguidos), fechas protegidas dentro de bloqueos y ocupación de cupo.
3. **Periodos de solicitud:** configuración, publicación, personas por grupo, seguimiento (quién ha solicitado), resultado y bitácora de cada asignación.
4. **Días bloqueados:**
   - Alta y edición en borrador.
   - Botón «Activar», con la validación de suficiencia y la lista de personas afectadas.
   - Lista de vacaciones solicitadas o autorizadas antes de la activación que quedan dentro del bloqueo (protegidas), con el botón «Proponer reprogramación».
5. **Cupos.**
6. **Solicitudes en curso:** con reasignación de suplente, igual que en permisos.
7. **Registro desde el formato de respaldo.** La fecha y hora de la solicitud es la que consta en el formato, que RH captura.
8. **Aguinaldo:**
   - Cálculo provisional por persona, con el detalle de los días no computables.
   - Columna de faltas por confirmar, con su acceso a confirmar o descartar.
   - Validación del contador.
   - Exportación a nómina.
   - Avisos de bajas (10.5).
9. **Configuración** (consultoría y RH, según permisos): parámetros de la sección 14. `VAC_PROGRAMACION_MODO` se muestra desde la configuración común con el RIT.

### 13.3 Autorizadores

Es la bandeja de la especificación de permisos, sección 3.3, con las solicitudes de vacaciones.
- Botones: «Autorizar», «Reprogramar» y «Devolver para corrección».
- Leyenda fija: «Las vacaciones son un derecho de la Persona Trabajadora. Puede autorizar las fechas o proponer otras; no puede negarlas.»
- Si la solicitud tiene fechas protegidas dentro de un bloqueo, se muestra además: «Esta solicitud se hizo antes de que se bloquearan esas fechas; el bloqueo no es motivo para reprogramarla.»

---

## 14. Diccionario de variables

### 14.1 Reutilizadas

- **Del RIT y de la configuración común:**
  - `VAC_PROGRAMACION_MODO` (captura única; ver 14.2).
  - `MES_CALENDARIO_VACACIONES` (solo con Calendario anual).
  - `DIAS_ANTICIPACION_VACACIONES`.
  - `PRIMA_VACACIONAL_PCT`.
  - `MOMENTO_PAGO_PRIMA`.
- **De permisos:**
  - Cadena de autorización: `CADENA_AUTORIZACION`, `AUTORIZACION_PLAZO_DIAS`, `AUTORIZADOR_SUPLENTE`, `NEGATIVA_CAUSA` (con el valor «Cupo completo», que solo usa este módulo), `NEGATIVA_MOTIVO`, `NEGATIVA_AUTOR`, `NEGATIVA_NIVEL`, `FECHA_ALTERNA`, `DEVOLUCION_MOTIVO`, `AUTORIZACIONES`, `RESOLUCION_FECHA`.
  - Registros y constancias: `EVENTO_SOLICITUD_FECHAHORA`, `CONSTANCIA_FECHA`, `SALIDA`.
  - Eventos que afectan el cálculo: `PAGO_DIAS_ESPERA`, `SUSP_VACACIONES_GENERA`, `VACACIONES_DIAS_GENERADOS`, `D4_REUBICACION`.
  - Negativa a firmar: `NEGATIVA_FIRMA`, `TESTIGO_1_NOMBRE`, `TESTIGO_2_NOMBRE`, `FECHA_ENVIO`.
  - Bloques comunes: `PATRON_RAZON_SOCIAL`, `TRAB_NOMBRE`, `TRAB_CURP`, `PUESTO`, `AREA`, `CENTRO_TRABAJO` (en el diccionario único, `CENTRO_NOMBRE`), `TRAB_EMAIL`, `LUGAR_FIRMA`, `FECHA_FIRMA`, `CLAUSULA_FIRMA_ELECTRONICA`, `FIRMA_EMPRESA_NOMBRE`, `FIRMA_EMPRESA_CARGO`.
- **Del módulo 9, por medio del módulo de permisos:** el estado de cada falta del año (Por confirmar · Confirmada), con su fecha. Este módulo solo lo lee; lo confirma o descarta RH con las reglas de los módulos 9 y 10.
- **Del alta, del organigrama y del módulo 5:**
  - Persona: `FECHA_INICIO`, CURP, **`SALARIO_PERSONA`** y la versión de condiciones de la persona (`JORNADA_VERSION`, `PRESTACIONES_VERSION`).
  - Puesto: `PRESTACIONES_EXTRA`, `PERSONA_JEFATURA`, `DIRECTOR_AREA`.
  - Firma: `FIRMA_MODALIDAD`, `FIRMANTES_EMPRESA`.
  - Constancias MOD-5 vigentes.
- **Del módulo 4:** `BAJA_FECHA` y el calendario de días inhábiles.
- **Del módulo 6:** `PAGO_ALERTAS_AGUINALDO` y la obligación de pago de aguinaldo de cada persona.
- **Del kit de PTU:** `PTU_COMPUTA`, solo para la regla de tabla gemela (10.3).

### 14.2 Variables del módulo

| Variable | Nivel | Tipo | Validación u omisión | Activa |
| --- | --- | --- | --- | --- |
| PARAMETROS_LEGALES_VACACIONES | X (tabla global de parámetros) | Tabla con vigencia | Sección 2; solo valores aprobados | Días, bloque mínimo, menores y plazos |
| VAC_PROGRAMACION_MODO | E (captura única, compartida con el RIT) | Calendario anual · Periodos de solicitud por antigüedad · A solicitud | **Sin valor por omisión**; obligatoria; se pregunta antes que sus campos dependientes | 4.1; art. 36 del RIT; VAC-1, VAC-2 |
| VAC_PREFERENCIAS_DIAS | E | Entero | 15; solo con Calendario anual | Ventana de preferencias |
| VAC_ANIO_PROGRAMACION | E | Año | Una tabla por año; solo con Periodos de solicitud | 4.5 |
| VAC_PERIODOS_SOLICITUD (VAC_GRUPO_NOMBRE, antigüedad desde y hasta, VAC_SOLICITUD_INICIO, VAC_SOLICITUD_FIN) | E | Tabla | Reglas de 4.5; se guarda siempre y se publica solo si cumple | Grupos, asignación, VAC-2, N-1 a N-3 |
| VAC_GRUPO_PERSONA | S | Grupo | Años cumplidos a la apertura del primer periodo de solicitud del año | Portal, VAC-2, N-1 |
| VAC_ALTERNATIVAS | S | Hasta 3 fechas de inicio | Cumplen la sección 6 y el plazo | VAC-1, N-3, N-6 |
| VAC_BLOQUEOS (fechas, VAC_BLOQUEO_ALCANCE, VAC_BLOQUEO_MOTIVO, VAC_BLOQUEO_DESCRIPCION) | E/V | Tabla | Siempre se guarda | Validación 9, VAC-2, N-4 (solo activos) |
| VAC_BLOQUEO_ESTADO | S/V | Borrador · Activo | Activar exige la suficiencia (4.6, regla 2) | Efectos del bloqueo |
| VAC_BLOQUEO_ACTIVACION | B | Fecha y hora | Se registra al activar (y al activar una ampliación, para los días añadidos); no editable | Comparación con `EVENTO_SOLICITUD_FECHAHORA` (4.6, regla 3) |
| VAC_BLOQUEO_EXCEPCIONES | S | Personas y fechas | Solicitudes enviadas antes de `VAC_BLOQUEO_ACTIVACION` y no canceladas | Validación 9; lista de RH; párrafo de N-4 |
| VAC_BLOQUEOS_PERIODO | S | Filas (del, al, motivo, descripción) | Bloqueos activos que aplican a la persona entre su aniversario y el límite, a la fecha de emisión | Tabla de VAC-2 |
| VAC_CUPOS (alcance, VAC_CUPO_MAXIMO) | E | Tabla, opcional | VAC_CUPO_MAXIMO ≥ 1 | Validación 10; asignación |
| VAC_NOTIFICACION_CANALES | E | Correo personal · App · Ambos | Ambos por omisión; la Plataforma siempre | 4.8 |
| VAC_CONFIRMACION_DIAS | E | Entero (días hábiles) | 3 | Alerta de VAC-3 |
| REINGRESO_ALERTA_DIAS | E | Entero | 90 | 3.3 |
| AGUINALDO_DIAS | E | Entero | ≥ 15; 15 | 10.2 |
| AGUINALDO_FECHA_PAGO | E | Día y mes | ≤ 19 de diciembre; 15 de diciembre | 10.4; módulo 6 |
| AGUINALDO_COMPUTA | E (global, editable por X; administrada por este módulo) | Tabla | Valores de 10.3; cambia junto con `PTU_COMPUTA` | 10.2; módulos 4 y 10 |
| AGUINALDO_FALTAS_POR_CONFIRMAR | S | Entero, por persona y año | Faltas del año en estado Por confirmar a la fecha del cálculo | Alerta de la sección 9; pantalla de aguinaldo; dato para el módulo 4 |
| VAC_PERIODO | S | Identificador | Uno por persona y aniversario | Folio de VAC-2 |
| VAC_ANIVERSARIO / VAC_ANTIGUEDAD_ANIOS | S | Fecha / entero | 3.1 | VAC-1, VAC-2, VAC-3 |
| VAC_DIAS_PERIODO | S | Entero | 3.1 | VAC-2; saldo |
| VAC_PROPORCIONAL | S | Sí/No | Sí con contrato tipo D o servicios discontinuos | Frase de VAC-2 |
| VAC_LIMITE_OTORGAMIENTO | S | Fecha | Aniversario + 6 meses | VAC-2, VAC-3, avisos, estado |
| VAC_FECHA_PRESCRIPCION | S | Fecha | Límite + 12 meses; nunca se imprime | Estado Prescrito |
| VAC_SALDO / VAC_ESTADO_SALDO | S | Entero / Vigente · Fuera de plazo · Prescrito · Agotado | 3.2 | Tablero, documentos, módulo 4 |
| VAC_FOLIO | S | Texto | Único por empresa | VAC-1, VAC-3 |
| VAC_ORIGEN | V/S | Calendario · Periodo de solicitud · Solicitud | — | VAC-1 |
| VAC_FECHA_INICIO / VAC_FECHA_FIN | V | Fecha | Sección 6 | Todos |
| VAC_DIAS | S | Entero | Días laborables del rango según la versión de condiciones | Todos; nómina |
| VAC_ESTADO | V/S | Sección 5 | — | Flujo y documentos |
| VAC_BLOQUES_PROGRAMADOS / VAC_BLOQUE_INICIO / _FIN / _DIAS | S | Entero / filas | Bloques autorizados a la fecha de emisión | Tabla de VAC-2 |
| VAC2_FECHA / VAC2_VERSION / VAC2_FECHA_ANTERIOR | S | Fecha / entero / fecha | 12.2 | VAC-2 |
| VAC_DIAS_INTERRUMPIDOS / VAC_INTERRUPCION_FECHA | S | Entero / fecha | 7.1 | VAC-1, apartado III; VAC-3 |
| VAC_REINCORPORACION_FECHA | S (editable por RH) | Fecha | Siguiente día laborable al fin del bloque | VAC-3 |
| VAC_SALARIO_BASE | S | Moneda | `SALARIO_PERSONA` vigente al iniciar el bloque | Nómina, prima |
| VAC_PRIMA_MONTO | S | Moneda | Sección 8 | Nómina, VAC-3 |
| VAC_CFDI_UUID | V | Texto (UUID) | Opcional; alerta si falta | VAC-3 |
| VAC3_OBSERVACION | V | Texto | Obligatoria con «No estoy de acuerdo» | Alerta a RH |
| VAC_CONFIRMACION_FECHAHORA | B | Fecha y hora | No editable | VAC-3 |
| VAC_AVISO_ENVIOS | B | Registro por envío (aviso, canal, fecha y hora, resultado) | No editable | Paquete probatorio |
| AGUINALDO_PERIODO_INICIO / AGUINALDO_DIAS_COMPUTABLES / AGUINALDO_MONTO | S | Fecha / entero / moneda | 10.2 | Exportación a nómina; módulo 6 |
| AGUINALDO_SALARIO_BASE | S | Moneda | `SALARIO_PERSONA` vigente en `AGUINALDO_FECHA_PAGO` | 10.2 |
| AGUINALDO_VALIDADO | V | Usuario y fecha del contador | Se revierte si cambia un evento del año, incluida la confirmación o el descarte de una falta | Exportación; obligación en el módulo 6; aviso de baja (10.5) |

### 14.3 Eliminadas (no programar)

- Variables: `VAC_PROGRAMACION_EMPRESA_DIAS`, `VAC_VENTANA_PROGRAMACION_DIAS`, `VAC_AVISO_REPROGRAMACION_DIAS`.
- Valores y acciones:
  - El valor «Programación de la Empresa» de `VAC_ORIGEN`.
  - La acción «Negar» en vacaciones.
  - El valor por omisión de `VAC_PROGRAMACION_MODO`.
  - La devolución automática de solicitudes en curso al activarse un bloqueo.
- Fila genérica «Falta injustificada» de `AGUINALDO_COMPUTA`: se sustituye por las filas de falta confirmada y falta por confirmar.
- Base salarial: el uso del salario del puesto (`SALARIO_DIARIO`, eliminada en todo el sistema) como base; rige `SALARIO_PERSONA`.

---

## 15. Dependencias

| Pieza | Qué necesita este módulo | Estado |
| --- | --- | --- |
| RIT, arts. 29 y 35 a 37 | Calendario, anticipación, prima, constancias, `VAC_PROGRAMACION_MODO`, tres modos y párrafo de días bloqueados y cupos | **Resuelto.** Art. 36 con los tres modos (v1.5) y el párrafo nuevo con la redacción final, «prevalece lo que se registra primero» (v1.6). Especificación vigente del RIT: v1.7 |
| Módulo de permisos v1.9 | Eventos para traslapes, interrupción y cómputo del aguinaldo; cadena; bloques comunes; `SUSP_VACACIONES_GENERA`; faltas del módulo 9 | **Encargos cumplidos:** «Cupo completo» (v1.7), B3 no computa (v1.7), lectura de `SUSP_VACACIONES_GENERA` confirmada (v1.7), D4 con reubicación (v1.8) y faltas por confirmar y confirmadas (v1.9) |
| Módulo 4 v1.5 | `BAJA_FECHA` y calendario de días inhábiles; lee saldos y aguinaldo (10.5 y 11) | **Encargos cumplidos en la v1.5:** sección 11, aguinaldo sin duplicar, cancelación de vacaciones y liberación del cupo, aviso de aguinaldo validado y `SALARIO_PERSONA` |
| Módulo 5 v1.1 | `SALARIO_PERSONA`, versión de condiciones y constancias MOD-5 | Vigente (registro 2 y 4.12) |
| Módulo 6 v1.0 | Obligación y pago del aguinaldo con CFDI; cancelación con motivo «Pago en finiquito» | Vigente (registro 4.13; sección 6 de su especificación) |
| Módulo 9 v1.1 | Faltas por confirmar y confirmadas para `AGUINALDO_COMPUTA`; los días de vacaciones justifican ausencias | Vigente (registro 4.14). Desde la v1.1, sin descuento del descanso proporcional |
| Kit de PTU v1.0 | `PTU_COMPUTA` (R-4), tabla gemela | Vigente (registro 4.7). Su encargo 4 aplica la misma regla de faltas confirmadas; la regla del descanso (10.3) también le aplica |
| Organigrama | Centros, áreas y puestos para el alcance de bloqueos y cupos | Vigente |
| Tabla global de parámetros legales | `PARAMETROS_LEGALES_VACACIONES` con aprobación y monitor | Pendiente transversal de Cerebro |
| App del colaborador | Notificaciones push | Fase 2; mientras tanto, notificación en la Plataforma |
| Firma electrónica v1.4 | Firma de VAC-2; registros digitales | Vigente |
| Nómina | Pago de salario, prima y aguinaldo; devolución del CFDI | Interfaz de 8 y 10.4 |

---

## 16. Pendientes que no bloquean la programación

- Cotejar con el Semanario Judicial: 2a./J. 15/98, 2a./J. 1/97, 2a./J. 63/2019, 2a./J. 31/2011, I.13o.T. J/8, III.T.268 L y la tesis colegiada sobre faltas y aguinaldo.
- Cotejar el texto oficial del Convenio 52 de la OIT y su ámbito.
- Buscar criterios sobre el fraccionamiento del bloque continuo (art. 78).
- Definir si las prestaciones extralegales regulares integran el salario ordinario para la prima y el aguinaldo (hoy la base es `SALARIO_PERSONA`).
- Cuadro general de antigüedades (art. 158): si entra al PMV, tomará la antigüedad de este módulo.
- Preferencia por antigüedad cuando hay contrato colectivo: sus reglas prevalecen y la tabla de 4.5 debe reflejarlas.

Si cambian, afectan parámetros o textos, no la estructura.

---

## 17. Casos de prueba

| Caso | Datos | Resultado esperado |
| --- | --- | --- |
| 1. Primer periodo | Inicio 1/03/2026; `SALARIO_PERSONA` $500.00; prima 25 % | Periodo 1 el 1/03/2027: 12 días; límite 1/09/2027; prescripción 1/09/2028; VAC-2 el 1/03/2027. Bloque de 12 días: salario $6,000.00; prima $1,500.00 |
| 2. Menor de edad | Persona de 17 años al aniversario 1 | 18 días |
| 3. Temporada | Tabla de 14 días; 200 días trabajados en el año | ⌈14 × 200 ÷ 365⌉ = ⌈7.67⌉ = 8 días |
| 4. Interrupción | Bloque del 6 al 21/07/2027 (12 días laborables); incapacidad C1 desde el 15/07 | Días laborables del 15 al 21 devueltos al saldo y cupo liberado; bloque Interrumpido; VAC-3 por los días anteriores; importe a cuenta informado al contador |
| 5. Recordatorio | Saldo de 12 días sin solicitud; límite 1/09/2027 | N-5 el 3/07/2027 y el 2/08/2027 |
| 6. Solicitud tardía | Solicitud el 10/10/2027 | Admitida; estado Fuera de plazo; alerta a RH y C |
| 7. Prescripción | Saldo de 4 días el 2/09/2028 | Estado Prescrito; no se puede solicitar; el módulo 4 lo muestra como informativo |
| 8. Aguinaldo proporcional | Inicio 1/03/2026; 15 días; `SALARIO_PERSONA` $500.00; 3 días C1 | 306 − 3 = 303 días; 15 × 303 ÷ 365 × 500 = **$6,226.03** |
| 9. Aguinaldo con riesgo de trabajo | Año completo 2026; 20 días C2; `SALARIO_PERSONA` $500.00 | 365 días; $7,500.00 |
| 10. Baja después del pago | Pago el 15/12/2026; baja el 28/12/2026 | Finiquito sin aguinaldo de 2026 ni descuento |
| 11. Asignación por antigüedad | Grupo «5 años o más», periodo de solicitud del 5 al 16/01/2027; área con cupo 1; A (inicio 2015) y B (inicio 2019) piden del 5 al 16/07/2027; B solicitó primero | Al cierre, A queda En autorización; B pasa a Reprogramado (Cupo completo) con hasta tres alternativas; ambos reciben N-3 |
| 12. Reintento en el siguiente cierre | B pide otras fechas mientras está abierto el periodo de solicitud del grupo «1 a 4 años» | La solicitud de B compite al cierre de ese periodo con su propia antigüedad (2019), antes que quienes ingresaron después |
| 13. Bloqueo insuficiente | Persona con saldo de 12 días y límite 30/06/2027; RH guarda un bloqueo de su área del 1/04 al 30/06/2027 que solo deja 9 días laborables libres | El bloqueo se guarda en Borrador; «Activar» lo rechaza y muestra a la persona en la lista de afectados; no surte efectos ni se notifica |
| 14. Bloqueo sobre vacaciones autorizadas | Bloqueo de capacitación del 10 al 12/05/2027, activado el 20/04; C tiene autorizadas del 3 al 14/05 | Las vacaciones de C no cambian; aparecen en la lista de RH como protegidas; RH puede proponer reprogramación; si C no acepta, conserva sus fechas |
| 15. Solicitud antes del periodo de solicitud | Persona del grupo «1 a 4 años» (periodo del 18 al 29/01/2027) solicita el 10/01/2027 fechas de 2027 | No se puede enviar; mensaje «Su periodo de solicitud abre el 18 de enero de 2027»; puede guardar borrador |
| 16. Baja con aguinaldo validado y sin pago | `AGUINALDO_VALIDADO` el 20/11/2026; baja el 5/12/2026 sin pago registrado | Aviso al contador; la persona sale de la exportación; el módulo 6 cancela su obligación con motivo «Pago en finiquito»; el finiquito incluye el aguinaldo del 1/01 al 5/12/2026 |
| 17. Salario individual | Puesto con salario base $450.00; `SALARIO_PERSONA` $520.00 | Prima, salario de vacaciones y aguinaldo se calculan con $520.00 |
| 18. Modo sin elegir | Empresa sin `VAC_PROGRAMACION_MODO` | La pantalla avisa; no hay calendario, periodos de solicitud ni campos dependientes; solo se admiten solicitudes con origen Solicitud |
| 19. Solicitud pendiente antes del bloqueo | D envía el 2/04/2027 una solicitud del 17 al 21/05; está En autorización. RH activa el 5/04 un bloqueo de capacitación del 18 al 20/05 | La solicitud de D no se devuelve ni cambia de estado; sus fechas quedan en `VAC_BLOQUEO_EXCEPCIONES`; la cadena no puede reprogramarla por el bloqueo; D recibe N-4 con el párrafo de que sus vacaciones no cambian |
| 20. Bloqueo antes de la solicitud | Bloqueo del 18 al 20/05/2027 activado el 5/04; E intenta solicitar el 6/04 del 17 al 21/05 | No se puede enviar; los días 18 a 20 aparecen bloqueados en el calendario; E puede pedir otras fechas |
| 21. Borrador frente a bloqueo | F guardó un borrador el 1/04 del 18 al 20/05 sin enviarlo; el bloqueo se activa el 5/04 | El borrador no está protegido; al enviarlo, la validación 9 lo rechaza |
| 22. Faltas por confirmar y confirmadas | Año completo 2026; `SALARIO_PERSONA` $500.00; 15 días; 2 faltas confirmadas y 3 por confirmar en el cálculo provisional del 15/11/2026 | Días computables: 365 − 2 = 363; 15 × 363 ÷ 365 × 500 = **$7,458.90**. Alerta a RH por las 3 faltas por confirmar; el contador puede validar. Los días de descanso de esas semanas computan |
| 23. Confirmación después de validar | Caso 22 validado el 20/11/2026; el 25/11 RH confirma una de las faltas por confirmar | Se revierte `AGUINALDO_VALIDADO` de esa persona; nuevo cálculo con 362 días: 15 × 362 ÷ 365 × 500 = **$7,438.36**; el contador valida de nuevo |

---

## 18. Textos

Se programan tal como están en «AXIARH - Módulo de vacaciones y aguinaldo - Textos (borrador)», sexta versión del 17/11/2026: VAC-1, VAC-2, VAC-3 y los avisos N-1 a N-6, con sus reglas de armado y notas. La v1.4 no cambia ningún texto. Cualquier cambio de texto se hace allí y se emite una nueva versión de esta especificación.
