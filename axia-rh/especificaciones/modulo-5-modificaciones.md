# AXIA RH — MÓDULO 5: MODIFICACIÓN DE CONDICIONES DE TRABAJO

Especificación para programación · Versión 1.1 · 20/11/2026
Fuente: «AXIARH - Módulo 5 - Textos y reglas (borrador)», tercera versión, «Corte - Módulo 5» y encargos del mapa del PMV del 18/11/2026. El usuario dio por terminado el modelo maestro el 15/11/2026; sus aprobaciones siguen siendo provisionales hasta la revisión final.

## Cambios respecto de la versión 1.0

La 1.0 no se ha corrido en el software; esta versión la sustituye completa. Si ya se cargó, basta aplicar esta tabla.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 11.4 (MOD-5), apartado 3 | Con causa «Falta de documentos», el texto dice que la reasignación no modifica el plazo legal para regularizar la situación, y su fecha de vencimiento (`SUSP_LIMITE`) |
| 2 | 11.4, notas; 9; 12.2 | MOD-5 por «Falta de documentos» aceptada devuelve al módulo de permisos `D4_REUBICACION` = Sí y, al concluir, `D4_REUBICACION_FIN`. Se quita «verificar con el módulo de permisos» |
| 3 | 0; 12.2 | Importes en letra con la fórmula de la carátula del contrato («… pesos NN/100 M.N.»): `SALARIO_PERSONA_LETRA` en MOD-1 y `SALARIO_NUEVO_LETRA` en MOD-2 usan la misma función |
| 4 | 11.1, cláusula de ascenso | Corrección de redacción: «regresará a su puesto de {{PUESTO_ANTERIOR}} al día siguiente de esa comunicación» |
| 5 | 13 | Estado de los encargos actualizado con el registro del 20/11/2026 (versionado, SALARIO_PERSONA, ACTUALIZACION_ANUAL_MES, TELE_AVISO_DIAS, cláusula 1.4, INCAPACIDAD_PARCIAL, firma electrónica v1.4) |
| 6 | 15 | Caso de prueba 14: reubicación en D4 |

**Alcance:** la pantalla de eventos «Modificar condiciones» y el proceso de cambios del catálogo. Determina el instrumento de cada cambio, genera los documentos, controla su firma y sus efectos, mantiene la versión de condiciones de cada persona y alerta a nómina, IMSS, consultoría y los demás módulos. No genera el aviso de sustitución patronal (MOD-6, prioridad C) ni la nueva versión del perfil de puesto (documento del kit; este módulo solo la dispara).

---

## 0. Convenciones

- Variables `{{MAYÚSCULAS_CON_GUION_BAJO}}`; condiciones `[SI condición] … [FIN SI]`; las marcas nunca se imprimen. Se permiten condiciones anidadas.
- Términos fijos de los textos: «la Empresa» y «la Persona Trabajadora».
- Niveles de captura: **E** configuración de la empresa · **O** organigrama o puesto (incluye el catálogo de jornadas) · **A** alta · **V** evento (pantalla «Modificar condiciones» o lote del catálogo) · **S** calculada por el sistema · **B** bitácora (no editable) · **X** solo consultoría.
- Fechas en formato largo; montos en MXN con dos decimales y en letra cuando se imprimen en un convenio o comunicado.
- Importes en letra: misma fórmula que la carátula del contrato, «… pesos NN/100 M.N.» (por ejemplo, $500.00 se imprime «quinientos pesos 00/100 M.N.»). Una sola función para `SALARIO_PERSONA_LETRA`, `SALARIO_NUEVO_LETRA` y cualquier otro importe en letra del módulo.
- Arial en todos los documentos (12 en el cuerpo; títulos en negrita del mismo tamaño o uno mayor; papel carta). PDF con la impresión del navegador, sin encabezado ni pie del navegador. (Nota de Cerebro, 22/11/2026: rige la impresión del navegador; ver el registro, sección 3.)
- Reglas de pantalla de todo el sistema (registro 5.0): campos faltantes resaltados y listados; tablas con «Guardar» y «Quitar» por renglón; la casilla «documento firmado» basta para avanzar y el archivo firmado es opcional (alerta sin bloqueo); un dato, una captura; sin candados por fecha (las validaciones solo impiden la versión definitiva); la opción se pregunta antes que sus campos y sin valor por omisión si la Ley no lo fija; concordancia de número.
- Días hábiles: calendario de días inhábiles del módulo 4.
- Ningún texto fija cifras que cambian por reforma. La jornada se valida con la tabla de máximos y el salario con la tabla de salarios mínimos por zona (parámetros globales, módulo 4, 5.3).
- Cada documento guarda la versión del modelo con que se emitió.

---

## 1. Arquitectura

1. **Evento de modificación** (`MOD_FOLIO`): una persona, una fecha de efectos, uno o varios cambios (`MOD_CAMBIOS`). El sistema elige el instrumento con la matriz (sección 2) y genera un solo documento por instrumento.
2. **Lote de catálogo** (`CATALOGO_CAMBIO_ID`): un cambio de puesto, perfil, jornada, salario del puesto o prestaciones del puesto crea una versión nueva del elemento del catálogo y un evento de modificación por cada persona ligada a la versión anterior.
3. **Versión de condiciones por persona** (sección 5): puesto, perfil, jornada, prestaciones y salario de cada persona. Es la fuente de condiciones para todos los módulos.
4. **Campaña anual** (ACT-1): una por empresa y año, en `ACTUALIZACION_ANUAL_MES`.
5. **Documentos:** MOD-1 convenio modificatorio, MOD-2 comunicado, MOD-4 oficio de reasignación REPSE, MOD-5 constancia de reasignación temporal y ACT-1 registro de actualización anual (textos en la sección 11). Las claves MOD-3 y MOD-1R no existen.

---

## 2. Catálogo de cambios e instrumento

| Cambio | Instrumento | Regla |
| --- | --- | --- |
| Actualización del perfil o de las actividades principales sin cambiar la naturaleza del puesto | Nueva versión del perfil (kit), con `PERFIL_AVISO_DIAS` | Solo se firma ese documento. RH confirma en pantalla que no cambian clasificación, nivel de acceso, jornada, salario ni categoría; si marca que alguna cambia, el evento pasa a MOD-1 |
| Aumento de salario individual o del puesto, o mejora de prestaciones | MOD-2 | El salario individual es libre siempre que sea mayor que el vigente |
| Ajuste por nuevo salario mínimo | MOD-2 (lote) | Solo para quienes quedarían por debajo del mínimo de su zona |
| Cambio de centro dentro de `CT_AMBITO` | MOD-2 | Sin plazo de aviso |
| Cambio de centro fuera de `CT_AMBITO` | MOD-1, módulo de centro | — |
| Reasignación REPSE entre clientes o instalaciones | MOD-4 | Con `ASIGNACION_AVISO_DIAS` |
| De domicilio de la Empresa a instalaciones de un cliente | MOD-4 y MOD-2 | Dentro del ámbito |
| De instalaciones de un cliente al domicilio de la Empresa | MOD-2 | Dentro del ámbito |
| Paso de presencial a híbrido | MOD-1, módulo H | — |
| Ajuste o revocación de días en casa del híbrido, sin rebasar el 40 % | MOD-2 | Con `TELE_AVISO_DIAS` |
| Días en casa que rebasan el 40 %, o paso de presencial a teletrabajo | MOD-1, módulo T | Voluntario y por escrito |
| Regreso de teletrabajo a presencial | MOD-2 (reversibilidad pactada) o MOD-1 (otro pacto) | Con `TELE_AVISO_DIAS` |
| Cambio de puesto, funciones de distinta naturaleza o categoría superior | MOD-1 | Sin periodo de prueba ni de capacitación inicial |
| Ascenso temporal o con periodo de adaptación | MOD-1, módulo de ascenso | Solo a categoría superior |
| Cambio de jornada: más duración, otro tipo, otros días o descanso, otro turno u otro horario | MOD-1 | — |
| Reducción de horas sin reducir el salario | MOD-2 | — |
| Reducción legal de la jornada (art. 8 del RIT) | MOD-2 (lote) | Generado por el RIT (su especificación, 2.6) |
| Reducción de salario, prestaciones, categoría o duración con salario proporcional | Solo MOD-1 | Nunca comunicado; sin firma no hay reducción; alerta interna de un mes (8) |
| Reasignación por embarazo, lactancia, falta de documentos (D4) o incapacidad temporal para el puesto | MOD-5 | No cambia la versión de condiciones |
| Readaptación por riesgo de trabajo | MOD-1 con `MOD_ORIGEN` = Readaptación | Situación protegida (7) |
| Lactancia y licencia sin goce | No son modificaciones | Módulo de permisos (LIC-1, LIC-3) |
| Actualización anual de datos y beneficiarios | ACT-1 | — |
| Sustitución patronal | MOD-6 | Fuera de esta versión |

Si un evento combina cambios de MOD-1 y de MOD-2 con la misma fecha de efectos, se genera solo MOD-1 con todos.

---

## 3. Pantallas

### 3.1 RH — «Modificar condiciones» (evento individual)

1. **Persona.** Carga la ficha de condiciones vigentes (3.3) y las situaciones protegidas.
2. **Cambios** (`MOD_CAMBIOS`, selección múltiple): Puesto · Jornada · Salario · Prestaciones · Centro de trabajo · Asignación REPSE · Días en casa (híbrido) · Teletrabajo · Regreso a presencial · Reasignación temporal · Perfil de puesto.
3. **Datos de cada cambio.** Solo los campos del cambio elegido. Los valores nuevos se eligen del catálogo (puesto, jornada, centro, cliente) o se capturan (salario, días en casa). Junto a cada dato se muestra el valor vigente.
4. **Origen** (`MOD_ORIGEN`): Solicitud de la Persona Trabajadora · Propuesta de la Empresa · Readaptación (sin valor por omisión; en lotes, Cambio del catálogo, automático).
5. **Fecha de efectos** (`MOD_FECHA_EFECTOS`).
6. **Resultado.** El sistema muestra el instrumento, las validaciones (6), las alertas (7 y 8) y los documentos que dispara el cambio (`MOD_DOCUMENTOS_LISTA`).
7. **Generar y enviar.** Borrador con marca de agua mientras haya validaciones pendientes; versión definitiva y envío a firma o entrega.
8. **Seguimiento.** Estado (4), firma, negativa, evidencia.

### 3.2 RH — Lote del catálogo

- Se abre al guardar un cambio en el organigrama o en el catálogo de jornadas que afecte a personas vigentes. Mensaje: «Este cambio aplica de inmediato a las altas nuevas. Para las N personas que ocupan el puesto o el turno se generará el documento que corresponde. Sus condiciones no cambian hasta que lo firmen o surta efectos».
- Pide `MOD_FECHA_EFECTOS` y genera un evento por persona.
- Tablero: generados, enviados, firmados, negativas, pendientes y «Condiciones anteriores vigentes», con filtros y exportación.

### 3.3 Ficha de condiciones vigentes

Por persona: puesto y versión de perfil, jornada, salario, prestaciones, centro y ámbito, modalidad (presencial, híbrido, teletrabajo), asignación REPSE, reasignación temporal vigente, y el historial cronológico de contrato, convenios, comunicados y oficios.

### 3.4 Portal de la Persona Trabajadora

Documentos para firmar o de recibido; la ficha de sus condiciones vigentes; ACT-1 durante la campaña. La alerta interna de reducción (8) nunca se muestra.

### 3.5 RH — Campaña de actualización anual

Se abre el día 1 de `ACTUALIZACION_ANUAL_MES`. Muestra por persona: pendiente, confirmado sin cambios, confirmado con cambios, sin respuesta. Valida cada ACT-1 y dispara la designación de beneficiarios o el cambio de correo o teléfono cuando corresponde.

---

## 4. Estados

### 4.1 Evento de modificación (`MOD_ESTADO`)

| Estado | Significa | Pasa a |
| --- | --- | --- |
| Borrador | Capturado; editable | Listo · Cancelado |
| Listo | Validado; documento definitivo generado | En firma (MOD-1) · Entregado (MOD-2, MOD-4, MOD-5) |
| En firma | MOD-1 enviado a la Persona Trabajadora y al representante | Firmado · Rechazado · Vencido |
| Firmado | MOD-1 firmado por ambas partes | Vigente (en la fecha de efectos) |
| Entregado | Comunicado, oficio o constancia entregado, firmado de recibido o con negativa documentada | Vigente (en la fecha de efectos) |
| Vigente | Surtió efectos: la persona pasa a la versión nueva (5) | Concluido (ascenso temporal, ascenso no confirmado o reasignación temporal terminada) |
| Rechazado / Vencido | MOD-1 no firmado | Fin; la persona conserva sus condiciones; nuevo evento si se insiste |
| Cancelado | Cancelado antes de la firma o de la entrega | Fin |
| Concluido | Regreso al puesto anterior o fin de la reasignación | Fin |

La firma electrónica sigue los estados de su especificación (sección 4); este estado los resume.

### 4.2 Ascenso (`ASCENSO_ESTADO`)

En curso → Firme (evaluación satisfactoria o vencimiento sin resultado) · Regreso (resultado no satisfactorio comunicado por escrito a más tardar el último día) · Concluido (temporal al llegar `ASCENSO_FECHA_FIN`) · Definitivo (temporal que continúa por instrucción de la Empresa sin nuevo convenio).

### 4.3 ACT-1 (`ACT_ESTADO`)

Pendiente → Confirmado sin cambios · Confirmado con cambios (con sus documentos derivados) · Sin respuesta (a los 45 días) → Validado por RH.

---

## 5. Versión de condiciones por persona

- El catálogo de puestos, perfiles, jornadas y prestaciones es versionado. Cada persona guarda `PUESTO_VERSION`, `PERFIL_VERSION`, `JORNADA_VERSION`, `PRESTACIONES_VERSION` y su salario `SALARIO_PERSONA` (por omisión, el del puesto).
- La persona pasa a la versión nueva solo cuando el evento queda Vigente: MOD-1 firmado, o MOD-2 entregado, en la fecha de efectos.
- Sin firma de MOD-1, conserva la versión anterior sin plazo y aparece en el tablero como «Condiciones anteriores vigentes».
- Nómina, vacaciones y aguinaldo, PTU, finiquito, el RIT (Anexo B, solo como resumen de turnos), el módulo 9 y los documentos posteriores leen la versión de cada persona, nunca la del catálogo.
- Ascenso: durante el periodo, la persona tiene la versión del puesto nuevo y conserva como «puesto titular» la anterior; al regresar, recupera la versión vigente del puesto titular a esa fecha.
- MOD-5 no cambia la versión: registra una reasignación temporal con su propio horario para el módulo 9.

---

## 6. Validaciones

| Validación | Efecto |
| --- | --- |
| Salario resultante menor que el mínimo de la zona del centro de trabajo, también al cambiar de centro | Bloqueo |
| Jornada resultante mayor que el máximo legal vigente en la fecha de efectos | Bloqueo |
| Jornada continua sin el descanso mínimo; más de seis días de trabajo sin descanso | Bloqueo |
| Reducción de salario, prestaciones, categoría o duración con salario proporcional por MOD-2 | Bloqueo: solo MOD-1 |
| Fecha de efectos de una reducción anterior a la fecha de firma | Bloqueo |
| Aumento con fecha de efectos anterior a la emisión | Permitido; alerta a nómina para pagar la diferencia |
| Periodo de prueba o de capacitación inicial en un cambio de puesto | No existe la opción |
| Módulo de ascenso sin cambio a categoría superior | No se ofrece |
| `ASCENSO_ADAPTACION_DIAS` vacío, menor que 1 o mayor que 90 (180 si el puesto nuevo tiene `PUESTO_DIRECCION_TECNICO` = Sí) | Bloqueo |
| Días en casa: 1 a 40 % solo con módulo H; más de 40 % solo con módulo T | Bloqueo; el sistema propone el instrumento |
| `HIBRIDO_ORIGEN` = Decisión de la Empresa con `HIBRIDO_APOYO_MODO` = Sin apoyo | Bloqueo |
| MOD-2 de días en casa sin módulo H vigente; MOD-2 de reversibilidad sin módulo T vigente | Bloqueo |
| Centro fuera de `CT_AMBITO` por MOD-2 | Bloqueo: MOD-1 con módulo de centro |
| REPSE: cliente sin contrato vigente en el catálogo, sin confirmación del objeto social con soporte, o REPSE vencido | Bloqueo |
| `MOD_CAMBIO_RESIDENCIA` = Sí sin `MOD_APOYO_TRASLADO` | Bloqueo |
| MOD-5 por falta de documentos sin D4 registrado | Bloqueo |
| Fecha de efectos futura | Permitida |

---

## 7. Situaciones protegidas

Alerta crítica con doble confirmación y registro de usuario, fecha y hora (`MOD_CONFIRMACION_PROTEGIDA`), sin bloqueo, cuando el cambio afecta a una persona:

- dentro del año siguiente al parto (fin de C3), si el cambio la saca de su puesto;
- con incapacidad en curso (C1, C2, C3) o en lactancia (B1);
- con incapacidad parcial por riesgo de trabajo (`INCAPACIDAD_PARCIAL` = Sí), salvo la readaptación que no reduce el salario;
- representante obrero en una comisión mixta que pasa a un puesto de confianza (alerta adicional para sustituirla conforme a las reglas de la comisión);
- firmante designado de RH que deja un puesto de confianza (la designación se revoca sola, especificación de firma electrónica 5.6).

Texto: «Esta persona está en una situación que la ley protege. El cambio puede impugnarse. Confirme que lo revisó con consultoría.» El dato nunca se imprime.

---

## 8. Plazos y alertas

Destinatarios: **P** Persona Trabajadora · **RH** · **C** consultoría · **Ct** contador · **N** nómina.

| Evento | Momento | Destinatarios | Acción |
| --- | --- | --- | --- |
| MOD-1 sin firma | Recordatorios y vencimiento de la especificación de firma | P, RH | El cambio no surte efectos |
| MOD-1 con reducción, al generar | Inmediata | C | Informativa |
| MOD-1 con reducción, firmado | Desde la firma hasta `MOD_REDUCCION_ALERTA_FIN` (firma + 1 mes) | RH, C | Alerta interna en el expediente: «Reducción firmada el {{MOD_FIRMA_FECHA}}: durante un mes la persona puede separarse con causa. Atienda cualquier reclamo con consultoría.» Aviso 7 días antes del fin; cierre automático. Nunca visible para P |
| MOD-2, MOD-4, MOD-5 con negativa | Al registrarla | RH | Dos testigos y envío al correo personal; no impide el efecto |
| MOD-4 | `ASIGNACION_AVISO_DIAS` antes de `ASIGNACION_INICIO` | RH | Alerta si se emite con menos anticipación sin `ASIGNACION_URGENTE` |
| Perfil nuevo | `PERFIL_AVISO_DIAS` naturales antes de su aplicación | RH | Alerta si se emite con menos anticipación |
| Ascenso temporal | 15 días naturales antes de `ASCENSO_FECHA_FIN` y el día | RH | Confirmar regreso o nuevo convenio |
| Ascenso con adaptación | A la mitad del periodo y 7 días antes del fin | RH, jefatura | Registrar `ASCENSO_RESULTADO`; sin resultado al vencer, Firme en automático |
| Cambio de salario vigente | Fecha de efectos | N, Ct | Aviso modificatorio ante el IMSS (plazo por verificar en la LSS) |
| Cambio de centro con otro registro patronal | Fecha de efectos | N, Ct | Baja y alta ante el IMSS con el registro patronal del nuevo centro |
| Cambio de centro a otro estado | Fecha de efectos | Ct | Impuesto estatal sobre nómina |
| Cambio de puesto | Al generar | RH | Documentos del puesto nuevo (`MOD_DOCUMENTOS_LISTA`) |
| Fin del contrato con un cliente REPSE | Al registrarse en el catálogo | RH, C | Reasignar a las personas asignadas; nunca baja |
| Nuevo salario mínimo aprobado | Al aprobarse en la tabla global | RH, N | Lote de MOD-2 con efectos al inicio de vigencia |
| Campaña ACT-1 | Día 1 de `ACTUALIZACION_ANUAL_MES`; días 15 y 30; día 45 | P; RH el día 45 | Recordatorios; «Sin respuesta» |
| Reasignación temporal | 7 días antes de `REASIGNACION_FIN` y al cesar la causa | RH | Confirmar regreso por escrito |

---

## 9. Efectos en otros módulos

| Módulo | Qué recibe de este módulo |
| --- | --- |
| Nómina | `SALARIO_PERSONA` vigente por fecha; diferencias de aumentos retroactivos; prestaciones de la versión de la persona; fin del apoyo de gastos de días en casa |
| Paquete de contratación | La carátula de documentos posteriores imprime `SALARIO_PERSONA`; nuevos perfiles, convenio de confidencialidad, carta responsiva, asignación de correo y acta de devolución que dispara un cambio de puesto o de modalidad |
| RIT | Lote de «Ajuste legal de jornada» (MOD-2); el Anexo B resume turnos del catálogo; las personas con condiciones anteriores no cambian por depositar uno nuevo |
| Módulo 4 | Salario, puesto y jornada de la versión de la persona en `BAJA_FECHA`; en ascenso temporal, el salario del puesto ocupado |
| Vacaciones y aguinaldo | `SALARIO_PERSONA` vigente al iniciar cada bloque y a `AGUINALDO_FECHA_PAGO` |
| PTU | Salario devengado por persona según sus versiones del ejercicio |
| Permisos | `D4_REUBICACION` y `D4_REUBICACION_FIN` (MOD-5 por falta de documentos); de permisos recibe `INCAPACIDAD_PARCIAL` (al cerrar C2), `SUSP_DOCUMENTO`, `SUSP_LIMITE` y la alerta de regreso tras el parto |
| Módulo 9 | Jornada esperada por la versión de la persona y por la reasignación temporal |
| Firma electrónica | Firmantes y estados (10) |

---

## 10. Firma y evidencia

| Documento | Persona Trabajadora | Empresa | Momento (`FIRMA_EMPRESA_DOC`) |
| --- | --- | --- | --- |
| MOD-1 | Firma según `FIRMA_MODALIDAD` | Representante (`REP_NOMBRE`), siempre e.firma si es electrónica | Posterior, «Representante» (decidido) |
| MOD-2 | Firma de recibido según `FIRMA_MODALIDAD` | RH designado | Posterior, «RH designado» |
| MOD-4 | Firma de recibido | RH designado | Posterior, «RH designado» |
| MOD-5 | Firma de recibido | RH designado | Posterior, «RH designado» (agregar a la tabla de firma) |
| ACT-1 | Confirma en la Plataforma | RH valida | Registro digital, sin firma |

- Sin firmante de RH vigente, firma el representante, con alerta (especificación de firma electrónica, sección 11).
- Negativa en MOD-2, MOD-4 y MOD-5: bloque común de negativa con dos testigos y envío al correo personal. En MOD-1 no hay negativa con testigos: sin firma no hay cambio.
- Bloque de firma según `FIRMA_MODALIDAD`: con Autógrafa, línea «Firma: ____»; con Electrónica, sellos `FIRMA_SELLO_TRAB` y `FIRMA_SELLO_EMPRESA` y la cláusula `CLAUSULA_FIRMA_ELECTRONICA`.
- Bitácora, hoja de evidencias, hash y copia al correo personal conforme a la especificación de firma electrónica. Paquete probatorio por persona: contrato, convenios, comunicados, oficios y constancias en orden cronológico, con la ficha de condiciones vigentes a cada fecha.

---

## 11. Textos de los documentos

Textos revisados por el usuario el 15/11/2026. Se programan tal como están. Los bloques comunes (encabezado, datos de la persona, cierre y firma, negativa) son los de la especificación de permisos, 17.1, con folio `MOD_FOLIO`. Las «Notas para programación» no se imprimen. En MOD-1, las cláusulas condicionales y las que siguen se numeran en orden con ordinales («QUINTA», «SEXTA»…), sin huecos.

### 11.1 MOD-1. Convenio modificatorio de las condiciones de trabajo

**CONVENIO MODIFICATORIO DE LAS CONDICIONES DE TRABAJO** · Folio {{MOD_FOLIO}}

Que celebran, por una parte, {{PATRON_RAZON_SOCIAL}}, representada por {{REP_NOMBRE}}, en su carácter de {{REP_CARACTER}} («la Empresa»), y, por la otra, {{TRAB_NOMBRE}}, por su propio derecho («la Persona Trabajadora»), al tenor de los antecedentes y cláusulas siguientes.

**ANTECEDENTES**

I. Las partes celebraron un contrato individual de trabajo {{TIPO_RELACION_TEXTO}} el {{CONTRATO_FECHA}}. La relación inició el {{FECHA_INICIO}}.[SI MOD_CONVENIOS_PREVIOS no vacía] El contrato fue modificado por los convenios de fechas {{MOD_CONVENIOS_PREVIOS}}.[FIN SI]

II. [SI MOD_ORIGEN = Solicitud de la Persona Trabajadora] La Persona Trabajadora solicitó por escrito el {{MOD_SOLICITUD_FECHA}} los cambios que este convenio formaliza.[FIN SI][SI MOD_ORIGEN = Propuesta de la Empresa] La Empresa propuso a la Persona Trabajadora los cambios que este convenio formaliza[SI MOD_MOTIVO no vacía], por lo siguiente: {{MOD_MOTIVO}}[FIN SI].[FIN SI][SI MOD_ORIGEN = Cambio del catálogo] La Empresa actualizó las condiciones del puesto de {{PUESTO_ANTERIOR}} con efectos para las personas que ingresen a partir del {{CATALOGO_CAMBIO_FECHA}}. Conforme al contrato, ese cambio no modifica por sí solo las condiciones pactadas con la Persona Trabajadora, por lo que la Empresa le propuso adoptarlas mediante este convenio.[FIN SI][SI MOD_ORIGEN = Readaptación] Con motivo del riesgo de trabajo que sufrió la Persona Trabajadora, la institución de seguridad social determinó el {{INCAPACIDAD_PARCIAL_FECHA}} que no puede desempeñar su puesto, pero sí otro, por lo que la Empresa le proporciona el que se describe en este convenio.[FIN SI]

III. La Persona Trabajadora declara que la Empresa le explicó los cambios, que leyó este convenio y sus anexos, que tuvo la oportunidad de consultarlo con la persona que eligió y que lo firma libremente.

**CLÁUSULAS**

**PRIMERA. Objeto y efectos.** Las partes modifican las condiciones de trabajo de la Persona Trabajadora en los términos de este convenio, con efectos a partir del {{MOD_FECHA_EFECTOS}}. Las condiciones que este convenio no modifica continúan en los términos del contrato y de los convenios anteriores. Este convenio no interrumpe la relación de trabajo ni la antigüedad, que se cuenta desde el {{FECHA_INICIO}}.

**SEGUNDA. Puesto y funciones.**

[SI MOD_CAMBIA_PUESTO = Sí] A partir de la fecha de efectos, la Persona Trabajadora ocupará el puesto de {{PUESTO_NUEVO}}, en el área de {{AREA_NUEVA}}, en lugar del puesto de {{PUESTO_ANTERIOR}}. El puesto se clasifica como {{CLASIFICACION_NUEVA}} en atención a la naturaleza de sus funciones. [SI PERFIL_MODALIDAD = Perfil de puesto] Sus funciones son las descritas en el perfil de puesto {{PERFIL_CLAVE}}, versión {{PERFIL_VERSION}}, que se agrega como Anexo 1 de este convenio y sustituye al perfil anexo al contrato.[FIN SI][SI PERFIL_MODALIDAD = Lista de actividades] Sus actividades principales son: {{ACTIVIDADES_PRINCIPALES}}.[FIN SI] Las labores conexas o complementarias de este puesto forman parte de sus actividades en los términos del contrato. El cambio de puesto no está sujeto a periodo de prueba ni de capacitación inicial.[SI ASCENSO_TIPO no vacía] El cambio se pacta en los términos de la cláusula de ascenso de este convenio.[FIN SI] [FIN SI]

[SI MOD_CAMBIA_PUESTO = No] La Persona Trabajadora continúa en el puesto de {{PUESTO}}, en el área de {{AREA}}, con las funciones pactadas.[FIN SI]

**TERCERA. Jornada.**

[SI MOD_CAMBIA_JORNADA = Sí] A partir de la fecha de efectos, la jornada de la Persona Trabajadora será la siguiente, en lugar de la pactada:

| Concepto | Anterior | Nueva |
| --- | --- | --- |
| Tipo de jornada | {{JORNADA_TIPO_ANTERIOR}} | {{JORNADA_TIPO}} |
| Días laborados | {{DIAS_LABORADOS_ANTERIOR}} | {{DIAS_LABORADOS}} |
| Horario | {{HORARIO_ANTERIOR}} | {{HORARIO}} |
| Duración semanal | {{HORAS_SEMANA_ANTERIOR}} horas | {{HORAS_SEMANA}} horas |
| Descanso semanal | {{DESCANSO_ANTERIOR}} | {{DESCANSO_SEMANAL_TEXTO}} |
| Descanso dentro de la jornada | {{DESCANSO_MINUTOS_ANTERIOR}} minutos | {{DESCANSO_MINUTOS}} minutos |

La duración semanal no excederá el máximo legal vigente, y las reglas de jornada, descansos y registro de asistencia del contrato y del reglamento interior de trabajo se aplican a la nueva jornada.[FIN SI]

[SI MOD_CAMBIA_JORNADA = No] La jornada de la Persona Trabajadora continúa en los términos pactados: {{JORNADA_RESUMEN}}.[FIN SI]

**CUARTA. Salario y prestaciones.** A partir de la fecha de efectos, el salario diario de la Persona Trabajadora es de ${{SALARIO_PERSONA}} ({{SALARIO_PERSONA_LETRA}})[SI PRESTACIONES_EXTRA no vacía] y sus prestaciones superiores a la ley son: {{PRESTACIONES_EXTRA}}[FIN SI].

[SI MOD_MODULO_ASCENSO = Sí]

**[ORDINAL]. Ascenso.**

[SI ASCENSO_TIPO = Temporal] La Persona Trabajadora ocupará el puesto de {{PUESTO_NUEVO}} de forma temporal, del {{MOD_FECHA_EFECTOS}} al {{ASCENSO_FECHA_FIN}}, por la causa siguiente: {{ASCENSO_CAUSA}}. Durante ese tiempo conserva la titularidad de su puesto de {{PUESTO_ANTERIOR}} y percibe el salario y las prestaciones del puesto que ocupa temporalmente. Si la causa termina antes, la Empresa se lo comunicará por escrito y la ocupación temporal concluirá en la fecha que señale. Al concluir, la Persona Trabajadora regresará a su puesto de {{PUESTO_ANTERIOR}}, con el salario, la jornada y las prestaciones vigentes para ese puesto en esa fecha. Como así se pacta desde ahora, el regreso no constituye una reducción de salario ni de condiciones. Si al llegar la fecha de fin la Persona Trabajadora continúa en el puesto por instrucción de la Empresa sin un nuevo convenio, el cambio se tendrá por definitivo.[FIN SI]

[SI ASCENSO_TIPO = Con periodo de adaptación] La Persona Trabajadora ocupará el puesto de {{PUESTO_NUEVO}} sujeta a un periodo de adaptación de {{ASCENSO_ADAPTACION_DIAS}} días naturales contados desde la fecha de efectos, durante el cual la Empresa le impartirá la capacitación siguiente: {{ASCENSO_CAPACITACION}}, y evaluará su desempeño en el puesto nuevo conforme a [SI PERFIL_MODALIDAD = Perfil de puesto]los indicadores del perfil de puesto (Anexo 1)[FIN SI][SI PERFIL_MODALIDAD = Lista de actividades]los criterios que le comunica por escrito con este convenio[FIN SI]. Durante el periodo, la Persona Trabajadora conserva la titularidad de su puesto de {{PUESTO_ANTERIOR}} y percibe el salario y las prestaciones del puesto nuevo. Si la evaluación es satisfactoria, o si el periodo concluye sin que la Empresa le comunique por escrito un resultado no satisfactorio, el cambio queda firme. Si la evaluación no es satisfactoria, la Empresa se lo comunicará por escrito, con el resultado, a más tardar el último día del periodo, y la Persona Trabajadora regresará a su puesto de {{PUESTO_ANTERIOR}} al día siguiente de esa comunicación, con el salario, la jornada y las prestaciones vigentes para ese puesto, lo que no constituye reducción de salario ni de condiciones porque así se pacta desde ahora. Este periodo no es un periodo de prueba ni de capacitación inicial: su resultado no afecta la relación de trabajo, que continúa en todo caso.[FIN SI]

[FIN SI]

[SI MOD_MODULO_CENTRO = Sí]

**[ORDINAL]. Centro de trabajo y ámbito geográfico.** A partir de la fecha de efectos, el centro de trabajo de la Persona Trabajadora es [SI REPSE_LUGAR_TIPO = Cliente]las instalaciones del cliente {{CLIENTE_RAZON_SOCIAL}} ubicadas en {{CLIENTE_INSTALACION_DOMICILIO}}, conforme al oficio de asignación que se le entrega con este convenio[FIN SI][SI REPSE_LUGAR_TIPO ≠ Cliente]el ubicado en {{CT_DOMICILIO}}[FIN SI], y su ámbito geográfico comprende {{CT_AMBITO}}, en lugar de {{CT_ANTERIOR}} y {{CT_AMBITO_ANTERIOR}}.[SI MOD_CAMBIO_RESIDENCIA = Sí] El cambio implica el cambio de residencia de la Persona Trabajadora, por lo que la Empresa le otorgará el apoyo siguiente: {{MOD_APOYO_TRASLADO}}.[FIN SI]

[FIN SI]

[SI MOD_MODULO_H = Sí]

**[ORDINAL]. Trabajo híbrido.** Las partes incorporan a la relación de trabajo la modalidad híbrida en los términos siguientes: [el sistema inserta, sin cambios de redacción, las cláusulas M-H.1 a M-H.8 de la biblioteca de módulos, con la numeración de este convenio]. A partir de la fecha de efectos se aplican también los apartados del contrato sobre los días en casa (horario, canales de comunicación y desconexión).

[FIN SI]

[SI MOD_MODULO_T = Sí]

**[ORDINAL]. Teletrabajo.** [SI TELE_ORIGEN = Cambio desde presencial]La Persona Trabajadora solicitó o aceptó por escrito el {{TELE_SOLICITUD_FECHA}} el cambio a la modalidad de teletrabajo.[FIN SI] Las partes pactan la modalidad de teletrabajo en los términos siguientes: [el sistema inserta, sin cambios de redacción, las cláusulas M-T.1 a M-T.11 de la biblioteca, conforme a su apartado 4.6]. Se agregan los Anexos T1, T2 y T3, que se firman con este convenio. [SI HIBRIDO_ACTIVO_ANTERIOR = Sí] Esta modalidad sustituye a la modalidad híbrida pactada anteriormente.[FIN SI]

[FIN SI]

[SI MOD_REGRESO_PRESENCIAL = Sí]

**[ORDINAL]. Regreso a la modalidad presencial.** A partir de la fecha de efectos, la Persona Trabajadora presta sus servicios de forma presencial en el centro de trabajo de la carátula[SI MOD_MODULO_CENTRO = Sí] o en el que señala este convenio[FIN SI], y queda sin efectos la modalidad {{MODALIDAD_ANTERIOR}}. El regreso no disminuye su salario ni sus demás condiciones de trabajo. La Persona Trabajadora devolverá el equipo que se le haya entregado solo para los días en casa, conforme al acta de devolución, y la Empresa dejará de cubrir el apoyo de gastos del domicilio desde esa fecha.

[FIN SI]

**[ORDINAL]. Documentos que se actualizan.** Con este convenio se entregan a la Persona Trabajadora los documentos siguientes, que forman parte de él: {{MOD_DOCUMENTOS_LISTA}}.

**[ORDINAL]. Seguridad social.** La Empresa presentará ante el Instituto Mexicano del Seguro Social y demás instituciones los avisos que deriven de este convenio, en los plazos legales.

**[ORDINAL]. Sin renuncia de derechos.** Este convenio no implica renuncia de los derechos de ninguna de las partes. Si alguna estipulación se considerara contraria a la ley, solo esa estipulación carecerá de efectos y las demás conservarán su validez.

**[ORDINAL]. Ejemplares.** La Persona Trabajadora recibe en este acto un ejemplar firmado de este convenio y de sus anexos.

Cierre y firma: bloque común. LA PERSONA TRABAJADORA · LA EMPRESA ({{REP_NOMBRE}}, {{REP_CARACTER}}).

**Notas para programación**
- Las cláusulas segunda a cuarta se imprimen siempre. La segunda y la tercera tienen variante «cambia» o «continúa». La cuarta solo enuncia el salario y las prestaciones vigentes desde la fecha de efectos, sin comparar con los anteriores ; el salario anterior queda en la ficha de condiciones y en la bitácora. Las demás cláusulas son condicionales y el sistema las numera en orden (ordinales), sin huecos.
- La validación del salario mínimo de la zona sigue en el sistema (6); el texto ya no la repite.
- `MOD_CAMBIA_*` se derivan de `MOD_CAMBIOS`. Las variables «_ANTERIOR» se toman de la versión vigente de la persona; las nuevas, de la versión nueva del catálogo o del evento.
- `MOD_DOCUMENTOS_LISTA` se arma con lo que el cambio dispara (8): perfil (Anexo 1), Anexos T1 a T3, carta responsiva, convenio de confidencialidad, oficio de asignación.
- Con `MOD_REDUCCION` = Sí: alerta a consultoría al generar y alerta interna de un mes desde la firma (8); `MOD_REDUCCION_ALERTA_FIN` = fecha de firma + 1 mes (mismo día del mes siguiente; si no existe, el último día del mes). Nada de esto se imprime ni se muestra a la Persona Trabajadora. Una reducción nunca se documenta por comunicado.
- La cláusula de ascenso solo se ofrece con cambio de puesto a categoría superior.
- No se envía a firma sin cálculo de salario mínimo y jornada máxima (6).

### 11.2 MOD-2. Comunicado de modificación de condiciones de trabajo

**COMUNICADO DE MODIFICACIÓN DE CONDICIONES DE TRABAJO** · Folio {{MOD_FOLIO}}

Bloque de datos de la persona.

La Empresa le comunica lo siguiente, con efectos a partir del {{MOD_FECHA_EFECTOS}}:

[SI MOD_TIPO contiene Aumento de salario] **Salario.** Su salario diario aumenta de ${{SALARIO_ANTERIOR}} a ${{SALARIO_NUEVO}} ({{SALARIO_NUEVO_LETRA}}).[SI MOD_FECHA_EFECTOS anterior a FECHA_FIRMA] La diferencia correspondiente al periodo transcurrido desde la fecha de efectos se le pagará en la nómina siguiente.[FIN SI] [FIN SI]

[SI MOD_TIPO contiene Salario mínimo] **Salario.** Por la entrada en vigor del nuevo salario mínimo, su salario diario se ajusta de ${{SALARIO_ANTERIOR}} a ${{SALARIO_NUEVO}} ({{SALARIO_NUEVO_LETRA}}). [FIN SI]

[SI MOD_TIPO contiene Mejora de prestaciones] **Prestaciones.** A sus prestaciones se agrega o mejora lo siguiente: {{PRESTACIONES_MEJORA}}. Se otorgan en los términos de {{PRESTACIONES_POLITICA}}. [FIN SI]

[SI MOD_TIPO contiene Centro de trabajo] **Centro de trabajo.** Su centro de trabajo será el ubicado en {{CT_DOMICILIO}}, en lugar de {{CT_ANTERIOR}}, dentro del ámbito geográfico pactado en su contrato. El cambio no modifica su puesto, jornada, salario ni prestaciones.[SI REPSE_LUGAR_TIPO_ANTERIOR = Cliente] A partir de esa fecha concluye su asignación a las instalaciones de {{CLIENTE_ANTERIOR}}.[FIN SI] [FIN SI]

[SI MOD_TIPO contiene Días en casa] **Días en casa.** [SI HIBRIDO_REVOCACION = No]Sus días en casa serán {{TELE_DIAS}}, en lugar de {{TELE_DIAS_ANTERIOR}}, equivalentes a {{PORC_TIEMPO_DOMICILIO}}% del tiempo de su jornada.[FIN SI][SI HIBRIDO_REVOCACION = Sí]Queda sin efectos la modalidad híbrida y, a partir de esa fecha, presta sus servicios de forma presencial en su centro de trabajo.[FIN SI] El aviso se da con {{TELE_AVISO_DIAS}} días de anticipación conforme a la cláusula de ajuste de la modalidad híbrida de su contrato[SI MOD_CAUSA_URGENTE = Sí], salvo por la causa urgente siguiente: {{MOD_CAUSA_URGENTE_TEXTO}}[FIN SI]. El cambio no disminuye su salario ni sus demás condiciones de trabajo. [FIN SI]

[SI MOD_TIPO contiene Reversibilidad] **Regreso a la modalidad presencial.** Conforme a la cláusula de reversibilidad de la modalidad de teletrabajo de su contrato, [SI REVERSIBILIDAD_ORIGEN = Empresa]la Empresa le comunica su decisión de que regrese[FIN SI][SI REVERSIBILIDAD_ORIGEN = Persona Trabajadora]la Empresa atiende su solicitud del {{REVERSIBILIDAD_SOLICITUD_FECHA}} de regresar[FIN SI] a la modalidad presencial en el centro de trabajo ubicado en {{CT_DOMICILIO}}, con {{TELE_AVISO_DIAS}} días de anticipación. El regreso no disminuye su salario ni sus demás condiciones de trabajo. El equipo entregado solo para el teletrabajo se devuelve conforme al acta de devolución, y el apoyo de gastos concluye en esa fecha. [FIN SI]

[SI MOD_TIPO contiene Reducción de horas] **Jornada.** Su jornada se reduce de {{HORAS_SEMANA_ANTERIOR}} a {{HORAS_SEMANA}} horas semanales, con el horario {{HORARIO}}, sin disminución de su salario ni de sus prestaciones. [FIN SI]

[SI MOD_TIPO contiene Ajuste legal de jornada] **Jornada.** Por la reducción de la jornada máxima que establece la ley, su horario se ajusta a {{HORARIO}}, con una duración semanal de {{HORAS_SEMANA}} horas, sin disminución de su salario ni de sus prestaciones, conforme al reglamento interior de trabajo. [FIN SI]

Las condiciones de trabajo que este comunicado no menciona continúan en los términos de su contrato.

Cierre y firma: bloque común; la Persona Trabajadora firma de recibido. Por la Empresa, RH designado. Bloque de negativa a firmar.

**Notas para programación**
- `MOD_TIPO` es selección múltiple; un comunicado puede llevar varios apartados con la misma fecha de efectos.
- Los apartados solo admiten cambios que no reducen condiciones (6). El de días en casa solo con módulo H vigente y sin rebasar el 40 %; el de reversibilidad solo con módulo T vigente.
- «Ajuste legal de jornada» lo genera el lote del RIT (2.6 de su especificación); es el «comunicado de horarios ajustados».
- La negativa a firmar de recibido no impide los efectos.

### 11.3 MOD-4. Oficio de reasignación (REPSE)

**OFICIO DE ASIGNACIÓN** · Folio {{MOD_FOLIO}}

Bloque de datos de la persona.

Conforme a la cláusula de asignación de su contrato, la Empresa le comunica su asignación siguiente:

| Concepto | Dato |
| --- | --- |
| Cliente (razón social y RFC) | {{CLIENTE_RAZON_SOCIAL}} / {{CLIENTE_RFC}} |
| Contrato de servicios (fecha y número) | {{SERVICIO_CONTRATO_FECHA}} |
| Lugar de prestación | {{CLIENTE_INSTALACION_DOMICILIO}} |
| Fecha de inicio de la asignación | {{ASIGNACION_INICIO}} |
| Asignación que sustituye | [SI CLIENTE_ANTERIOR no vacía]{{CLIENTE_ANTERIOR}}, {{CLIENTE_INSTALACION_ANTERIOR}}[FIN SI][SI CLIENTE_ANTERIOR vacía]Domicilio de la Empresa[FIN SI] |

1. **Condiciones.** La asignación corresponde a su puesto, se encuentra dentro del ámbito geográfico de su contrato y no modifica su jornada, salario ni prestaciones.
2. **Dirección del trabajo.** Las instrucciones sobre sus funciones, horario y disciplina las da únicamente la Empresa, por conducto de las personas que ella designe. Si recibe instrucciones directas del cliente, infórmelas de inmediato a la Empresa.
3. **Lineamientos del cliente.** [SI CLIENTE_LINEAMIENTOS_ENTREGA no vacía]Con este oficio se le entregan las políticas de servicio al cliente de la Empresa y los lineamientos del cliente, que debe observar.[FIN SI] Cumplirá además las reglas de acceso y seguridad de las instalaciones del cliente.
4. **Aviso.** Esta asignación se le comunica con {{ASIGNACION_AVISO_DIAS}} días de anticipación[SI ASIGNACION_URGENTE = Sí], salvo por la causa urgente siguiente: {{ASIGNACION_URGENTE_TEXTO}}[FIN SI].

Declaración de la Empresa: el servicio no forma parte del objeto social ni de la actividad económica preponderante del cliente, conforme a la declaración de este de fecha {{CLIENTE_DECLARACION_FECHA}}.

Cierre y firma: bloque común; la Persona Trabajadora firma de recibido. Por la Empresa, RH designado. Bloque de negativa a firmar.

**Notas para programación**
- Toma el formato del oficio inicial (biblioteca 2.3) y agrega la asignación que sustituye, las condiciones y el aviso.
- Con cambio fuera del ámbito, el sistema no genera el oficio solo: genera MOD-1 con módulo de centro y el oficio como anexo.
- Validaciones de la biblioteca 2.4 (REPSE vigente, confirmación de objeto social con soporte, alerta de puesto que replica uno del cliente).

### 11.4 MOD-5. Constancia de reasignación temporal

**CONSTANCIA DE REASIGNACIÓN TEMPORAL** · Folio {{MOD_FOLIO}}

Bloque de datos de la persona.

1. **Causa.** [SI REASIGNACION_CAUSA = Embarazo]La Persona Trabajadora informó su embarazo y su puesto se encuentra en un área en que se presentan condiciones de riesgo para ese estado, conforme al reglamento interior de trabajo.[FIN SI][SI REASIGNACION_CAUSA = Lactancia]La Persona Trabajadora se encuentra en periodo de lactancia y su puesto se encuentra en un área en que se presentan condiciones de riesgo para ese estado, conforme al reglamento interior de trabajo.[FIN SI][SI REASIGNACION_CAUSA = Falta de documentos]La Persona Trabajadora no cuenta con {{SUSP_DOCUMENTO}}, que su puesto exige, y la Empresa le ofrece desempeñar temporalmente otras funciones que no lo requieren, mientras lo regulariza.[FIN SI][SI REASIGNACION_CAUSA = Incapacidad temporal para el puesto]Conforme a {{REASIGNACION_SOPORTE}}, la Persona Trabajadora no puede desempeñar temporalmente las funciones de su puesto, pero sí otras.[FIN SI]

2. **Funciones temporales.** Del {{REASIGNACION_INICIO}} [SI REASIGNACION_FIN no vacía]al {{REASIGNACION_FIN}}[FIN SI][SI REASIGNACION_FIN vacía]hasta que cese la causa[FIN SI], la Persona Trabajadora desempeñará las funciones siguientes: {{REASIGNACION_FUNCIONES}}, en {{REASIGNACION_LUGAR}}, con el horario {{REASIGNACION_HORARIO}}.

3. **Condiciones.** La reasignación no disminuye su salario ni sus prestaciones, no modifica su puesto ni su antigüedad y no es una medida disciplinaria. [SI REASIGNACION_CAUSA = Falta de documentos]Mientras desempeñe estas funciones no se suspende la relación de trabajo. La reasignación no modifica el plazo que la ley señala para regularizar su situación, que vence el {{SUSP_LIMITE}}.[FIN SI]

4. **Regreso.** Al concluir la causa, la Persona Trabajadora regresa a su puesto y funciones, lo que la Empresa le confirmará por escrito.

5. **Confidencialidad.** [SI REASIGNACION_CAUSA ≠ Falta de documentos]La causa de la reasignación es información confidencial y solo la conocen Recursos Humanos y quien deba conocerla para organizar el trabajo.[FIN SI]

Cierre y firma: bloque común; la Persona Trabajadora firma de recibido. Por la Empresa, RH designado. Bloque de negativa a firmar.

**Notas para programación**
- No cambia la versión de condiciones de la persona (5); nómina sigue igual.
- Embarazo y lactancia: se genera desde el aviso del art. 65 del RIT o desde B1; alerta a RH y al análisis de jornada si el horario cambia (sin horas extra ni trabajo nocturno, conforme al capítulo X del RIT).
- Falta de documentos: solo con D4 registrado y antes de generar SUS-2. Al quedar Vigente, el módulo 5 envía al módulo de permisos `D4_REUBICACION` = Sí; al concluir la reasignación (regularización, fin capturado o cancelación), envía `D4_REUBICACION_FIN`. Mientras dure, el módulo de permisos no genera SUS-2, el evento queda «Con reubicación», los días se pagan y cuentan como trabajados, y el plazo de dos meses sigue corriendo desde `SUSP_CONOCIMIENTO_FECHA` (registro 4.9). Si la reubicación termina sin regularizar, el módulo de permisos genera SUS-2 desde esa fecha.
- La causa nunca se describe con diagnósticos.

### 11.5 ACT-1. Registro de actualización anual de datos y beneficiarios

Se abre una vez al año, en `ACTUALIZACION_ANUAL_MES`, para todas las personas activas, y al reincorporarse de una suspensión si la confirmación tiene más de 12 meses (SUS-3). No se firma: la persona confirma en la Plataforma y RH valida.

La Persona Trabajadora hace constar, en la fecha de este registro, lo siguiente:

- **Datos de contacto.** Confirma o actualiza su domicilio, teléfono, correo electrónico personal, estado civil y contacto para emergencias: {{ACT_DATOS_RESUMEN}}.[SI ACT_CAMBIO_CORREO_TELEFONO = Sí] El cambio de correo electrónico o de teléfono surte efectos cuando Recursos Humanos verifica su identidad y la Persona Trabajadora lo confirma con un código de verificación.[FIN SI]
- **Beneficiarios.** [SI ACT_BENEFICIARIOS = Sin cambios]Confirma su designación de beneficiarios de fecha {{BENEF_DESIGNACION_FECHA}}.[FIN SI][SI ACT_BENEFICIARIOS = Con cambios]Actualiza su designación de beneficiarios, que firma en este acto en el formato de designación.[FIN SI]
- **Cuenta de pago.** [SI ACT_CAMBIO_CUENTA = Sí]Solicita el cambio de la cuenta para el pago de su salario, que surtirá efectos cuando lo confirme por escrito conforme a su contrato.[FIN SI][SI ACT_CAMBIO_CUENTA = No]Confirma la cuenta registrada para el pago de su salario.[FIN SI]
- **Declaración.** Declara que los datos registrados son correctos y que comunicará cualquier cambio dentro del plazo de su contrato.

[SI SALIDA = Constancia] Confirmado por la Persona Trabajadora en la Plataforma el {{CONFIRMACION_FECHAHORA}} y validado por {{FIRMA_EMPRESA_NOMBRE}}. [FIN SI]
[SI SALIDA = Respaldo] Formato de respaldo. Recursos Humanos lo captura en la Plataforma el mismo día y conserva el original. [FIN SI]

**Notas para programación**
- Al validar, el sistema actualiza `BENEF_CONFIRMACION_FECHA` (la usan el pago a beneficiarios del módulo 4 y SUS-3).
- Cambio de correo o teléfono: flujo 5.7 de la especificación de firma electrónica. Cambio de beneficiarios: genera la designación del kit para firma.
- Recordatorios a la persona a los 15 y 30 días de abierta la campaña; sin respuesta a los 45, alerta a RH.
- Coincide con la revisión anual de perfiles (registro 4.3 bis): en el mismo mes se abre la alerta de revisión de perfiles para RH.
- No incluye datos de salud ni escolaridad.

---

## 12. Diccionario de variables

### 12.1 Reutilizadas

- Del contrato y el kit: `PATRON_RAZON_SOCIAL`, `REP_NOMBRE`, `REP_CARACTER`, `TRAB_NOMBRE`, `TRAB_CURP`, `TRAB_EMAIL`, `TIPO_RELACION_TEXTO`, `FECHA_INICIO`, `CONTRATO_FECHA` (derivada), `PUESTO`, `AREA`, `CLASIFICACION`, `PUESTO_DIRECCION_TECNICO`, `PERFIL_MODALIDAD`, `PERFIL_CLAVE`, `PERFIL_VERSION`, `ACTIVIDADES_PRINCIPALES`, `PERFIL_AVISO_DIAS`, `PRESTACIONES_EXTRA`, `JORNADA_TIPO`, `DIAS_LABORADOS`, `HORARIO`, `HORAS_SEMANA`, `DESCANSO_SEMANAL`, `DESCANSO_MINUTOS`, `JORNADA_RESUMEN`, `PERIODICIDAD`, `CT_DOMICILIO`, `CT_AMBITO`, `NIVEL_ACCESO_INFO`, `FIRMA_MODALIDAD`, `TIPO_FIRMA`, `CLAUSULA_FIRMA_ELECTRONICA`, `FIRMA_SELLO_TRAB`, `FIRMA_SELLO_EMPRESA`, `LUGAR_FIRMA`, `FECHA_FIRMA`, `BENEF_DESIGNACION_FECHA`, `BENEF_CONFIRMACION_FECHA`.
- De la biblioteca: `TELE_DIAS`, `PORC_TIEMPO_DOMICILIO`, `TELE_AVISO_DIAS`, `TELE_ORIGEN`, `TELE_SOLICITUD_FECHA`, `HIBRIDO_ORIGEN`, `HIBRIDO_APOYO_MODO`, `HIBRIDO_APOYO_MONTO`, `REPSE_LUGAR_TIPO`, `ASIGNACION_AVISO_DIAS`, `ASIGNACION_INICIO`, `CLIENTE_RAZON_SOCIAL`, `CLIENTE_RFC`, `CLIENTE_INSTALACION_DOMICILIO`, `SERVICIO_CONTRATO_FECHA`, `CLIENTE_DECLARACION_FECHA`, `CLIENTE_LINEAMIENTOS_ENTREGA`; cláusulas M-H.1 a M-H.8 y M-T.1 a M-T.11 y Anexos T1 a T3.
- De firma electrónica: `FIRMANTES_EMPRESA`, `FIRMA_EMPRESA_NOMBRE`, `FIRMA_EMPRESA_CARGO`, `FIRMA_EMPRESA_DOC`.
- De permisos: bloques comunes, `SALIDA`, `CONSTANCIA_FECHA`, `CONFIRMACION_FECHAHORA`, `NEGATIVA_FIRMA`, `TESTIGO_1_NOMBRE`, `TESTIGO_2_NOMBRE`, `FECHA_ENVIO`, `SUSP_DOCUMENTO`, `SUSP_CONOCIMIENTO_FECHA`, `SUSP_LIMITE`.
- Globales: tablas de salarios mínimos por zona y de jornada máxima por año; calendario de días inhábiles.

### 12.2 Variables del módulo

| Variable | Nivel | Tipo | Validación u omisión | Activa |
| --- | --- | --- | --- | --- |
| SALARIO_PERSONA / SALARIO_PERSONA_LETRA | A, V / S | Moneda / texto | Por omisión el del puesto; ≥ mínimo de la zona; menor que el vigente solo por MOD-1. Letra: «… pesos NN/100 M.N.» (0) | MOD-1 cláusula cuarta; nómina y demás módulos |
| PUESTO_VERSION, PERFIL_VERSION, JORNADA_VERSION, PRESTACIONES_VERSION | O (catálogo versionado) / S (persona) | Identificador | Cambian solo con un evento Vigente | Todos los módulos (5) |
| ACTUALIZACION_ANUAL_MES | E | Mes | Obligatoria | Campaña ACT-1; alerta de revisión de perfiles |
| INCAPACIDAD_PARCIAL / INCAPACIDAD_PARCIAL_FECHA | V (al cerrar C2, módulo de permisos) | Sí/No / fecha | Fecha obligatoria con Sí | Situación protegida; antecedente de readaptación |
| CATALOGO_CAMBIO_ID / CATALOGO_CAMBIO_FECHA | S | Identificador / fecha | Uno por cambio del catálogo | Lote; antecedente II de MOD-1 |
| MOD_FOLIO | S | Texto | Único por empresa | Todos los documentos |
| MOD_ESTADO | S | Sección 4.1 | — | Flujo |
| MOD_CAMBIOS | V | Selección múltiple (3.1) | Al menos uno | Instrumento y derivadas |
| MOD_CAMBIA_PUESTO, MOD_CAMBIA_JORNADA, MOD_CAMBIA_SALARIO, MOD_CAMBIA_PRESTACIONES | S | Sí/No | De MOD_CAMBIOS | MOD-1 cláusulas segunda y tercera; alertas |
| MOD_REDUCCION / MOD_REDUCCION_CONCEPTOS | S | Sí/No / texto | Sí si algún valor nuevo es menor que el vigente | Instrumento MOD-1; alertas internas; no se imprime |
| MOD_REDUCCION_ALERTA_FIN | S | Fecha | Firma de MOD-1 + 1 mes (mismo día del mes siguiente; si no existe, el último día del mes) | Alerta interna (8) |
| MOD_FIRMA_FECHA | B | Fecha | De la bitácora de firma | Alerta interna |
| MOD_ORIGEN | V | Solicitud de la Persona Trabajadora · Propuesta de la Empresa · Cambio del catálogo (S en lotes) · Readaptación | Sin valor por omisión | MOD-1 antecedente II |
| MOD_SOLICITUD_FECHA / MOD_MOTIVO | V | Fecha / texto | Fecha obligatoria con Solicitud; motivo opcional | MOD-1 antecedente II |
| MOD_FECHA_EFECTOS | V | Fecha | Reglas de 6 | Todos |
| MOD_CONVENIOS_PREVIOS | S | Lista de fechas | Del expediente | MOD-1 antecedente I |
| PUESTO_NUEVO, AREA_NUEVA, CLASIFICACION_NUEVA / PUESTO_ANTERIOR | V (del catálogo) / S | Texto | Del organigrama | MOD-1 cláusulas segunda y de ascenso |
| JORNADA_TIPO_ANTERIOR, DIAS_LABORADOS_ANTERIOR, HORARIO_ANTERIOR, HORAS_SEMANA_ANTERIOR, DESCANSO_ANTERIOR, DESCANSO_MINUTOS_ANTERIOR / DESCANSO_SEMANAL_TEXTO | S | Texto | De la versión vigente y de la nueva | MOD-1 cláusula tercera |
| SALARIO_ANTERIOR / SALARIO_NUEVO / SALARIO_NUEVO_LETRA | S / V / S | Moneda / texto | Letra con la misma función que SALARIO_PERSONA_LETRA (0) | MOD-2; ficha y bitácora (no se imprimen en MOD-1) |
| MOD_MODULO_ASCENSO / ASCENSO_TIPO | S / V | Sí/No / Temporal · Con periodo de adaptación | Solo con cambio a categoría superior | Cláusula de ascenso |
| ASCENSO_FECHA_FIN / ASCENSO_CAUSA | V | Fecha / texto | Obligatorios con Temporal; fin > efectos | Cláusula de ascenso; alertas |
| ASCENSO_ADAPTACION_DIAS / ASCENSO_CAPACITACION | V | Entero / texto | 1 a 90; hasta 180 con PUESTO_DIRECCION_TECNICO = Sí del puesto nuevo; capacitación obligatoria | Cláusula de ascenso; alertas |
| ASCENSO_RESULTADO / ASCENSO_RESULTADO_FECHA / ASCENSO_ESTADO | V / V / S | Satisfactorio · No satisfactorio / fecha / 4.2 | No satisfactorio: comunicado escrito a más tardar el último día | Regreso o firmeza |
| MOD_MODULO_CENTRO, CT_ANTERIOR, CT_AMBITO_ANTERIOR | S | Sí/No / texto | Sí si el centro nuevo está fuera de CT_AMBITO | Cláusula de centro |
| MOD_CAMBIO_RESIDENCIA / MOD_APOYO_TRASLADO | V | Sí/No / texto | Apoyo obligatorio con Sí | Cláusula de centro |
| MOD_MODULO_H, MOD_MODULO_T, MOD_REGRESO_PRESENCIAL, MODALIDAD_ANTERIOR, HIBRIDO_ACTIVO_ANTERIOR | S | Sí/No / texto | De los días en casa capturados y la modalidad vigente | Cláusulas de modalidad |
| MOD_DOCUMENTOS_LISTA | S | Lista | Documentos que dispara el cambio (8) | MOD-1 cláusula de documentos |
| MOD_TIPO | V | Aumento de salario · Salario mínimo · Mejora de prestaciones · Centro de trabajo · Días en casa · Reversibilidad · Reducción de horas · Ajuste legal de jornada | Selección múltiple; solo cambios que no reducen | MOD-2 |
| PRESTACIONES_MEJORA / PRESTACIONES_POLITICA | V | Texto | Obligatorios con Mejora de prestaciones | MOD-2 |
| TELE_DIAS_ANTERIOR / HIBRIDO_REVOCACION | S / V | Texto / Sí/No | — | MOD-2 |
| MOD_CAUSA_URGENTE / MOD_CAUSA_URGENTE_TEXTO | V | Sí/No / texto | Texto obligatorio con Sí | MOD-2 |
| REVERSIBILIDAD_ORIGEN / REVERSIBILIDAD_SOLICITUD_FECHA | V | Empresa · Persona Trabajadora / fecha | Fecha obligatoria con Persona Trabajadora | MOD-2 |
| REPSE_LUGAR_TIPO_ANTERIOR, CLIENTE_ANTERIOR, CLIENTE_INSTALACION_ANTERIOR | S | Texto | De la asignación vigente | MOD-2, MOD-4 |
| ASIGNACION_URGENTE / ASIGNACION_URGENTE_TEXTO | V | Sí/No / texto | Texto obligatorio con Sí | MOD-4 |
| REASIGNACION_CAUSA | V | Embarazo · Lactancia · Falta de documentos · Incapacidad temporal para el puesto | Sin valor por omisión | MOD-5 |
| REASIGNACION_INICIO / REASIGNACION_FIN | V | Fecha | Fin opcional («hasta que cese la causa») | MOD-5; alertas |
| REASIGNACION_FUNCIONES / REASIGNACION_LUGAR / REASIGNACION_HORARIO | V | Texto | Obligatorios; horario validado contra el capítulo X del RIT en embarazo y lactancia | MOD-5; módulo 9 |
| REASIGNACION_SOPORTE | V | Texto + archivo | Obligatorio con Incapacidad temporal; sin diagnóstico | MOD-5 |
| D4_REUBICACION / D4_REUBICACION_FIN | S (las entrega este módulo al de permisos) | Sí/No / fecha | Sí al quedar Vigente un MOD-5 con causa «Falta de documentos»; fin = fecha en que concluye la reasignación | Evento D4 «Con reubicación»; SUS-2 desde el fin si no se regularizó |
| MOD_CONFIRMACION_PROTEGIDA | V | Usuario, fecha y hora | Obligatoria con situación protegida | No se imprime |
| ACT_ESTADO | S | 4.3 | — | Campaña |
| ACT_DATOS_RESUMEN | S | Texto | Datos confirmados o actualizados | ACT-1 |
| ACT_BENEFICIARIOS | V (Plataforma) | Sin cambios · Con cambios | — | ACT-1; designación del kit |
| ACT_CAMBIO_CORREO_TELEFONO / ACT_CAMBIO_CUENTA | S | Sí/No | — | ACT-1; flujo de verificación |

### 12.3 Eliminadas (no programar)

`MOD3_DESCRIPCION`, `MOD_INCONFORMIDAD_LIMITE`, `MOD_INCONFORMIDAD_FECHA`, `MOD_INCONFORMIDAD_TEXTO`, `MOD_INCONFORMIDAD_DECISION`, `MOD_INCONFORMIDAD_RESPUESTA`, `MOD_REDUCCION_CONTRAPRESTACION` y los documentos MOD-3 y MOD-1R. No existe el botón «Manifestar inconformidad».

---

## 13. Dependencias y encargos

Estado al 20/11/2026, según el registro de decisiones.

| Pieza | Qué necesita este módulo | Estado |
| --- | --- | --- |
| Organigrama y catálogo de jornadas | Versionado por elemento y liga de cada persona a su versión | Registrado (registro, sección 2, 15/11/2026) |
| Alta | `SALARIO_PERSONA` con precarga del puesto (sustituye el «salario fijo por puesto») | Registrado (sección 2 y 4.1, 17/11/2026) |
| Configuración de la empresa | `ACTUALIZACION_ANUAL_MES`; `TELE_AVISO_DIAS` como variable de empresa | Registrado (sección 2, 15/11/2026) |
| Contrato | Cláusula 1.4: el cierre ya no dice «ningún cambio disminuirá el salario» | Resuelto (registro 4.1, 17/11/2026) |
| Biblioteca | M-H.1 a M-H.8, M-T.1 a M-T.11, Anexos T1 a T3 y oficio 2.3, sin cambios | Vigente |
| Permisos | `INCAPACIDAD_PARCIAL` al cerrar C2; D4 con reubicación (`D4_REUBICACION`, `D4_REUBICACION_FIN`) | Resuelto (especificación de permisos v1.7 y v1.8) |
| RIT | El lote de 2.6 genera MOD-2 «Ajuste legal de jornada» | Resuelto (especificación del RIT v1.5) |
| Firma electrónica | MOD-5 «RH designado» y ACT-1 sin firma en la tabla de la sección 11 | Resuelto (especificación de firma electrónica v1.4) |
| Nómina, módulo 4, vacaciones y aguinaldo, PTU, módulo 9 | Leer la versión y el salario de cada persona | Módulo 4 v1.5 y vacaciones v1.2 ya lo leen; módulo 9, encargo vigente del mapa |

---

## 14. Pendientes que no bloquean la programación

- Plazo del aviso modificatorio de salario ante el IMSS (LSS); mientras tanto la alerta es informativa en la fecha de efectos.
- Criterios judiciales sobre el consentimiento a la modificación de condiciones y sobre el regreso al puesto anterior en ascensos condicionados (art. 39-D).
- Ratificación de convenios modificatorios (art. 33).
- MOD-6, aviso de sustitución patronal (prioridad C).

Si cambian, afectan textos o alertas, no la estructura.

---

## 15. Casos de prueba

| Caso | Datos | Resultado esperado |
| --- | --- | --- |
| 1. Aumento individual | Salario vigente $500.00; nuevo $600.00; efectos el 1 del mes en curso, emitido el día 10 | MOD-2 «Aumento de salario» con párrafo de diferencia; `SALARIO_PERSONA` = $600.00 desde el día 1; alerta a nómina y contador |
| 2. Reducción por comunicado | Salario $600.00 → $550.00 por MOD-2 | Bloqueo: «La reducción solo se documenta con convenio» |
| 3. Reducción por convenio | MOD-1 firmado el 31/01/2027 con salario menor | Vigente; alerta interna hasta el 28/02/2027; aviso a RH el 21/02/2027; nada visible para la persona |
| 4. Convenio no firmado | Lote de cambio de horario de 9:00–18:00 a 10:00–19:00 para 20 personas; 18 firman | 18 pasan a la versión nueva; 2 quedan en «Condiciones anteriores vigentes» y nómina y el módulo 9 siguen leyendo el horario anterior |
| 5. Ascenso con adaptación | Puesto nuevo sin PUESTO_DIRECCION_TECNICO; 120 días | Bloqueo (máximo 90) |
| 6. Ascenso no satisfactorio | 60 días; resultado no satisfactorio comunicado el día 55 | Regreso al puesto titular el día 56, con el salario vigente de ese puesto; estado Concluido |
| 7. Ascenso sin resultado | 60 días; sin `ASCENSO_RESULTADO` al vencer | Firme en automático |
| 8. Días en casa | 5 días laborados; híbrido de 2 a 3 días en casa | 60 % > 40 %: MOD-2 bloqueado; el sistema propone MOD-1 con módulo T |
| 9. Centro en otra zona | Salario $400.00; nuevo centro en la Zona Libre de la Frontera Norte (mínimo 2026: $440.87) | Bloqueo por salario mínimo |
| 10. Situación protegida | Cambio de puesto a una persona a 8 meses del parto | Alerta crítica, doble confirmación y registro; sin bloqueo |
| 11. REPSE vencido | Reasignación con folio REPSE vencido | Bloqueo de MOD-4 |
| 12. Perfil que cambia la naturaleza | RH marca que cambia la clasificación | El evento pasa de nueva versión del perfil a MOD-1 |
| 13. ACT-1 sin respuesta | Campaña abierta el 1/03; sin respuesta | Recordatorios el 16/03 y el 31/03; «Sin respuesta» y alerta a RH el 15/04 |
| 14. Reubicación en D4 | D4 registrado con `SUSP_CONOCIMIENTO_FECHA` 2/03/2027 (`SUSP_LIMITE` 2/05/2027); MOD-5 aceptado el 5/03; la persona regulariza el 20/04 | MOD-5 imprime el vencimiento del 2 de mayo de 2027; `D4_REUBICACION` = Sí el 5/03 y `D4_REUBICACION_FIN` = 20/04; sin SUS-2; días pagados y computables |
