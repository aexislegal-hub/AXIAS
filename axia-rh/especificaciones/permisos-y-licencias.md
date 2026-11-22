# AXIA RH — MÓDULO DE PERMISOS Y LICENCIAS

Especificación para programación · Versión 1.9 · 21/11/2026
Fuente: «AXIARH — Módulo de permisos y licencias (diseño)» (https://claude.ai/artifact/CzspqdB6hqBzpXk5r9UgKB), «Corte - Módulo de permisos y licencias», «Corte - Firma electrónica» y decisiones del usuario del 12/11/2026.

**Alcance de esta versión:** la lógica completa del módulo (eventos, pantallas, estados, validaciones, plazos, alertas, efectos en otros módulos y variables) y los textos de los siete documentos y los dos registros (sección 17), revisados por el usuario. Visor de los textos: https://claude.ai/artifact/RxLxU4yPFpCGmcxiQkbftL.

**Control de cambios**

| Versión | Fecha | Cambio |
| --- | --- | --- |
| 1.0 | 12/11/2026 | Lógica del módulo, sin textos |
| 1.1 | 12/11/2026 | Se agregan los textos revisados (sección 17); se ajustan la sección 12 y las validaciones de LACTANCIA_INICIO y LIC3_SOLICITUD_FECHA |
| 1.2 | 12/11/2026 | Cadena de autorización de permisos (3.4); firma de la Empresa por RH designado y no por el representante (12.2); se armoniza con la especificación de firma electrónica (TIPO_FIRMA); textos de SP-1 y LIC-3 ajustados |
| 1.3 | 12/11/2026 | Los permisos que otorga la Ley (A1, A2, A3, B2) también pasan por la cadena de autorización, sin opción de negar; nueva acción «Devolver para corrección» |
| 1.4 | 12/11/2026 | Armonización con el registro, el mapa y el RIT v1.1: INC-1 sin TRIBUNAL_COMPETENTE (encargo del mapa); causas de negativa del art. 33 del RIT (NEGATIVA_CAUSA); solicitud vencida a RH (art. 33); A3 solo se niega por el límite de comisionados; PERSONA_JEFATURA en lugar de JEFE_INMEDIATO; firmas del formato de respaldo de SP-1 |
| 1.5 | 13/11/2026 | Armonización con la especificación de firma electrónica v1.2 (firmante de RH designado ya previsto; sin firmante vigente, firma el representante), con el RIT v1.3 (LACTARIO opcional: sin lactario, LIC-1 solo admite reducción; días de pago por periodicidad) y con las reglas de todo el sistema del 13/11/2026 (Arial, PDF en el servidor, archivo firmado opcional) |
| 1.6 | 13/11/2026 | Armonización con el módulo de vacaciones y aguinaldo: el registro de vacaciones es la segunda fuente de ausencias justificadas; validación 1 y faltas incluyen los días de vacaciones; columna de aguinaldo con los valores de `AGUINALDO_COMPUTA` que fija ese módulo (B3 pendiente, por omisión No) |
| 1.7 | 17/11/2026 | Encargos del mapa del 17/11: situaciones protegidas como alerta crítica con doble confirmación, sin bloqueo (decisión 19); B3 no computa para el aguinaldo; lectura de `SUSP_VACACIONES_GENERA` confirmada con el módulo de vacaciones; «catálogo de conductas del RIT»; `INCAPACIDAD_PARCIAL` al cerrar C2; valor «Cupo completo» de `NEGATIVA_CAUSA` (solo vacaciones); la incapacidad interrumpe las vacaciones |
| 1.8 | 17/11/2026 | D4 con reubicación aceptada (MOD-5) sustituye a la suspensión mientras dure (decisión del usuario) |
| 1.9 | 21/11/2026 | Encargos 7 y 8 del mapa del 20/11: faltas «por confirmar» y «confirmadas» del módulo 9; D1 y D5 como datos sensibles (decisión 32) |
| 1.9 (nota de Cerebro) | 21/11/2026 | INC-1 toma el salario de `SALARIO_PERSONA` (se elimina `SALARIO_DIARIO`) y `AUTORIDAD_INSPECCION` guarda solo el nombre de la autoridad (decisión P2 del diccionario único). Aplicado por Cerebro con autorización del usuario |

---

## 0. Convenciones

- Variables: `{{MAYÚSCULAS_CON_GUION_BAJO}}`. Condiciones: `[SI condición] … [FIN SI]`. Las marcas nunca se imprimen.
- Términos fijos en los textos: «la Empresa» y «la Persona Trabajadora».
- Niveles de captura:
  - **E** = configuración de la empresa.
  - **O** = organigrama o puesto.
  - **A** = alta de la Persona Trabajadora.
  - **V** = evento (pantalla «Permisos y licencias»).
  - **S** = calculada por el sistema (no editable salvo que se indique).
  - **B** = bitácora de la Plataforma (no editable por nadie).
- Fechas en formato largo («17 de noviembre de 2026»); fecha y hora con horas y minutos.
- **Reglas de todo el sistema (13/11/2026):** todos los documentos en Arial; el PDF se genera en el servidor, sin encabezado ni pie del navegador; la pantalla resalta los campos faltantes y tiene botones visibles de guardar en las tablas editables; la casilla «documento firmado» basta para avanzar y el archivo firmado es opcional (alerta, sin bloqueo); los datos capturados en un documento llenan los demás.
- **Días hábiles:** se usa el calendario configurable de días inhábiles del módulo 4 (fines de semana, días de descanso obligatorio y días que marque la empresa). El conteo empieza el día hábil siguiente al hecho.
- Ningún texto ni regla fija cifras que cambian por reforma (duración de la paternidad, semanas de maternidad, subsidios). Esas cifras viven en tablas del sistema con fecha de vigencia.
- **Principio de fuente única:** el evento de este módulo y el registro de vacaciones (VAC-1, módulo de vacaciones y aguinaldo) son las únicas fuentes de ausencias justificadas para nómina, IMSS, PTU, aguinaldo, finiquito y análisis de jornada. Ningún otro módulo captura ausencias por su cuenta; todos leen de estas dos.

---

## 1. Arquitectura

- Cuatro familias de eventos: **A permisos** (no suspenden la relación), **B licencias** (la suspenden total o parcialmente), **C incapacidades del IMSS** (las paga el IMSS), **D suspensiones del art. 42 LFT**.
- Flujo de todo evento: **1. Captura → 2. Resolución → 3. Evidencia → 4. Cierre o regreso**. Si la evidencia no llega, se pasa por la reclasificación (sección 7).
- Los efectos en otros módulos empiezan desde la captura (por ejemplo, una incapacidad en curso ya bloquea la baja), no desde el cierre.
- Lo que el checador marca como ausencia sin evento llega al módulo 9 como **falta** y alimenta las alertas de faltas y patrón de ausentismo (sección 9).
- Quedan fuera: la suspensión por fin de temporada (módulo 4) y la suspensión colectiva por contingencia sanitaria (no es evento individual). Las vacaciones tienen su propia pantalla y su propio registro (VAC-1), que es la segunda fuente de ausencias justificadas.

---

## 2. Catálogo de eventos (`EVENTO_TIPO`)

Origen: **Ley** = permiso o licencia que otorga la Ley (no se puede negar); **Empresa** = lo concede la Empresa.

| Clave | Evento | Origen | Inicia | Resuelve | ¿Se puede negar? | Salario | Evidencia | Documento o registro | Suspende la relación |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A1 | Paternidad o adopción (padres) | Ley | Persona | Cadena de autorización (3.4), sin negar | No | Con goce | Acta de nacimiento o constancia de adopción | SP-1 (registro) | No |
| A2 | Voto, revocación de mandato, jurado, servicios electorales o censales | Ley | Persona | Cadena de autorización (3.4), sin negar | No | Con goce | Constancia, cuando exista | SP-1 (registro) | No |
| A3 | Comisión accidental del sindicato o del Estado | Ley | Persona | Cadena de autorización (3.4), sin negar; solo puede limitarse por el número de comisionados | No, salvo el límite de comisionados | `COMISION_GOCE` (lo elige RH en cada caso) | Oficio del sindicato o de la autoridad | SP-1 (registro) | No |
| A4 | Permisos de la Empresa (catálogo `PERMISOS_EMPRESA`: fallecimiento, matrimonio, hospitalización, guardería, citas médicas, asuntos personales, por horas y los que agregue la empresa) | Empresa | Persona | Cadena de autorización (3.4) | Sí, por escrito y con motivo, en cualquier paso | Según el catálogo | La del catálogo | SP-1 (registro) | No |
| B1 | Lactancia | Ley | Persona | RH | No | Tiempo pagado | Acta de nacimiento | LIC-1 | No (reduce la jornada) |
| B2 | Adopción (madres) | Ley | Persona | Cadena de autorización (3.4), sin negar | No | Con goce | Constancia de adopción | SP-1 (registro) | Sí (descanso) |
| B3 | Licencia del IMSS por hijo con cáncer (art. 140 Bis LSS) | Ley | Persona | RH registra | No | Subsidio del IMSS | Licencia del IMSS | Solo registro con evidencia | Sí |
| B4 | Comisión permanente del sindicato o del Estado | Ley | Persona | RH | No | Sin goce | Oficio de designación | LIC-2 (notificación) | Sí |
| B5 | Licencia sin goce pactada | Empresa | Persona | Cadena de autorización (3.4); discrecional | Sí, en cualquier paso | Sin goce | Solicitud firmada | LIC-3 | Sí |
| C1 | Incapacidad por enfermedad general (incluye la contagiosa) | Ley | Persona | RH registra | No | Subsidio del IMSS; días de espera según `PAGO_DIAS_ESPERA` | Certificado de incapacidad | Solo registro con evidencia | Sí |
| C2 | Incapacidad por riesgo de trabajo | Ley | Hecho; RH | RH registra | No | Subsidio del IMSS | Certificado y formato del IMSS de probable riesgo | INC-1 (aviso a la autoridad, si es accidente) | Sí |
| C3 | Maternidad (prenatal, posnatal y prórroga) | Ley | Persona | RH registra | No | Subsidio del IMSS; 50 % en la prórroga | Certificados de incapacidad | INC-2, solo si transfiere semanas | Sí |
| D1 | Prisión preventiva o arresto (art. 42, frs. III y IV) | Ley | Hecho; RH | RH, al acreditarse | No | Sin salario | Constancia de la autoridad | SUS-1 | Sí |
| D2 | Cargo del art. 5 constitucional o servicio de armas (fr. V) | Ley | Persona | RH | No | Sin salario | Nombramiento o convocatoria | SUS-1 | Sí |
| D3 | Representante ante organismos estatales (fr. VI) | Ley | Persona | RH | No | Sin salario | Nombramiento | SUS-1 | Sí |
| D4 | Falta de documentos legales imputable a la persona (fr. VII) | Ley | Empresa | RH, con visto bueno de consultoría | — | Sin salario; con reubicación aceptada, con salario | Documento vencido o faltante | SUS-2; con reubicación, MOD-5 del módulo 5 | Sí; con reubicación, No |
| D5 | Declaración Especial de Ausencia (art. 132, fr. XXIX) | Ley | Hecho; RH | RH, al recibir la resolución | No | Sin salario | Resolución judicial | Solo registro con evidencia | Sí |
| D6 | Regreso de una licencia o suspensión | — | Persona o Empresa | RH | — | — | — | SUS-3 (registro) | — |

`PERMISO_ORIGEN` (S) = Ley para A1, A2, A3, B1, B2, B3, B4, C y D; Empresa para A4 y B5. Los permisos que otorga la Ley (A1, A2, A3 y B2) pasan por la cadena de autorización, pero no pueden negarse (3.4, regla 6). Las licencias, incapacidades y suspensiones de origen Ley (B1, B3, B4, C y D) no pasan por la cadena: RH las registra y la jefatura y la dirección reciben aviso.

---

## 3. Pantallas

### 3.1 Portal de la Persona Trabajadora

- **Solicitar:** A1, A2, A3, A4, B1, B2 y B5. La persona elige el tipo, fechas (y horario en permisos por horas) y adjunta la evidencia si ya la tiene. En A4 ve los topes disponibles del catálogo (veces al mes, días al año).
- **Informar:** C1, C2 y C3 (subir el certificado del IMSS), B3 (subir la licencia del IMSS), B4, D2 y D3 (subir el nombramiento).
- **Mis eventos:** estado, plazo de la evidencia, documentos para firmar y acuses pendientes.
- **Acusar recibo** de LIC-2 y **confirmar** la lista de reincorporación (SUS-3).
- Si la persona no tiene acceso al portal, RH captura en su nombre a partir del formato de respaldo en papel (sección 12.3).

### 3.2 Pantalla de RH «Permisos y licencias»

1. **Persona.** Carga expediente: puesto, jornada del catálogo, centro de trabajo, saldo de permisos del catálogo, eventos vigentes.
2. **Tipo** (`EVENTO_TIPO`). Lista de la sección 2.
3. **Datos del tipo.** Solo los campos de ese tipo (sección 14).
4. **Resolución** (`EVENTO_ESTADO`). En los permisos con cadena (A1 a A4, B2, B5) la resuelve la cadena (3.4); en los demás, RH registra. En origen Ley no existe «Negado», salvo el límite de comisionados en A3.
5. **Evidencia.** Archivo y plazo (`EVIDENCIA_FECHA_LIMITE`).
6. **Documentos.** Genera el documento o registro que corresponda (sección 12) y lo envía a firma o acuse.
7. **Cierre o regreso.** Registra la fecha real de fin o de regreso y dispara SUS-3 cuando aplica.

### 3.3 Autorizadores (jefatura inmediata, RH y dirección del área)

- Bandeja de autorizaciones con las solicitudes A1, A2, A3, A4, B2 y B5 que esperan su paso, y avisos de las licencias, incapacidades y suspensiones de su personal.
- Botones «Autorizar», «Devolver para corrección» y «Negar». «Negar» solo existe en origen Empresa (A4, B5) y, en A3, solo por el límite de comisionados. Negar exige `NEGATIVA_CAUSA` (A4 y B5: «Requisitos no subsanados» o «Necesidad operativa concreta», que es la que admite el RIT; A3: «Número de comisionados») y `NEGATIVA_MOTIVO`, y permite proponer `FECHA_ALTERNA`; con «Necesidad operativa concreta», el sistema pide proponer otra fecha cuando sea posible. Devolver exige `DEVOLUCION_MOTIVO`. Cada autorizador ve las autorizaciones previas. En los permisos de origen Ley la pantalla muestra: «Este permiso lo otorga la Ley y no puede negarse. Si falta un dato o la evidencia, devuélvalo para corrección.»
- RH ve además todas las solicitudes en curso, puede reasignar un paso a un suplente y revisa las negativas de la jefatura.

### 3.4 Cadena de autorización

1. **Orden.** Los permisos que otorga la Ley (A1, A2, A3, B2), los permisos de la Empresa (A4) y la licencia sin goce (B5) se autorizan en este orden: jefatura inmediata (`PERSONA_JEFATURA`), Recursos Humanos y dirección del área (`DIRECTOR_AREA`), si existe en el organigrama. El representante legal no interviene.
2. **Configuración.** La cadena por omisión se fija en `CADENA_AUTORIZACION` (E). Cada concepto del catálogo `PERMISOS_EMPRESA` puede usar una cadena más corta (columna «Autorizan»; por ejemplo, permisos por horas: jefatura y RH). RH es siempre un paso. B5 usa siempre la cadena completa.
3. **Misma persona.** Si una persona ocupa dos pasos (la jefatura inmediata es también la dirección del área), autoriza una sola vez y la bitácora registra los dos pasos como cumplidos.
4. **Nadie autoriza su propio permiso.** Si quien solicita ocupa un paso de la cadena, ese paso pasa a su superior en el organigrama o, si no existe, a RH.
5. **Plazo por paso.** Cada paso resuelve dentro de `AUTORIZACION_PLAZO_DIAS` días hábiles (por omisión 1) desde que recibe la solicitud. La falta de respuesta no es autorización: al vencer, alerta al autorizador y a RH; RH puede reasignar el paso a un suplente (`AUTORIZADOR_SUPLENTE`, con registro). Con un paso vencido, la Persona Trabajadora puede pedir a RH que resuelva; RH resuelve el mismo día.
6. **Permisos de la Ley.** No existe «Negar». La cadena verifica los datos, el aviso y la evidencia y puede devolver la solicitud para corrección; en A3 solo puede limitar el número de comisionados cuando perjudique la operación (con `NEGATIVA_MOTIVO`). La devolución no suspende el derecho: si llega la fecha del permiso sin autorización completa, RH lo registra ese día (estado Registrado) y la ausencia nunca se marca como falta.
7. **Devolución.** «Devolver para corrección» regresa la solicitud a la Persona Trabajadora con `DEVOLUCION_MOTIVO`; al corregirla, la cadena reinicia en el paso que la devolvió.
8. **Negativa (A4 y B5; en A3, solo por el número de comisionados).** Una negativa en cualquier paso termina la solicitud (Negado) y registra `NEGATIVA_AUTOR` y `NEGATIVA_NIVEL`. Si negó la jefatura, la Persona Trabajadora puede pedir a RH que la revise; RH resuelve el mismo día y, si autoriza, la solicitud sigue a la dirección del área. Si negó RH o la dirección, la negativa es definitiva para esa solicitud.
9. **Llega la fecha sin resolución (A4, B5).** Si la Persona Trabajadora pidió el permiso a tiempo y la cadena no ha resuelto al iniciar el permiso, el sistema alerta a RH, que resuelve ese mismo día. Mientras tanto, la ausencia no se marca como falta.
10. **Aviso urgente.** Con `AVISO_URGENTE` = Sí, la cadena corre después del hecho, en el mismo orden.
11. **Cancelación.** La Persona Trabajadora puede cancelar su solicitud mientras no haya iniciado el permiso.
12. **Constancia.** Cada paso queda en la bitácora (usuario, cargo, fecha y hora, decisión). `AUTORIZACIONES` (S) arma la lista que se imprime en SP-1.

---

## 4. Estados (`EVENTO_ESTADO`)

| Estado | Significado | Transiciones |
| --- | --- | --- |
| Solicitado | Capturado por la persona o por RH | → En autorización (A1 a A4, B2, B5), Registrado (B1, B3, B4, C, D), Cancelado |
| En autorización | Recorre la cadena (3.4) | → Autorizado (último paso), Negado (cualquier paso; A4, B5 y, por el límite de comisionados, A3), Devuelto, Registrado (permiso legal sin autorización completa al iniciar), Cancelado |
| Devuelto | La cadena pidió corregir datos o evidencia | → En autorización (al corregir), Cancelado |
| Registrado | Licencia, incapacidad o suspensión registrada por RH, o permiso legal que RH registró al iniciar sin autorización completa | → En curso |
| Autorizado | Permiso autorizado por la cadena | → En curso |
| Negado | Permiso de la Empresa negado con motivo | Fin, salvo revisión de RH de una negativa de la jefatura (→ En autorización). Puede generarse una nueva solicitud |
| Cancelado | La persona canceló la solicitud antes del inicio | Fin |
| En curso | Fecha de inicio alcanzada | → Evidencia pendiente, Cerrado |
| Evidencia pendiente | Terminó el evento y falta la evidencia | → Cerrado (llega la evidencia), Reclasificado |
| Reclasificado | RH decidió pasar a sin goce (sección 7) | → Cerrado; se revierte si llega la evidencia |
| Con reubicación | Solo D4: la persona aceptó la reasignación temporal (MOD-5 del módulo 5); no hay suspensión | → Cerrado (regulariza el documento), En curso (termina la reubicación sin regularizar: se genera SUS-2 desde esa fecha) |
| Cerrado | Evento terminado con evidencia o sin requerirla | Fin |

Cada cambio de estado queda en la bitácora (usuario, fecha y hora).

---

## 5. Validaciones

1. **Un solo evento de día completo por persona y fecha, incluidos los días de vacaciones (VAC-1).** No se registra un permiso, licencia o suspensión en días de vacaciones programadas, ni el módulo de vacaciones programa días con evento B (salvo B1), C o D. Si se registra una incapacidad del IMSS (C1, C2, C3) en días ya marcados como vacaciones, la incapacidad prevalece: el sistema avisa al módulo de vacaciones y aguinaldo, que suspende las vacaciones desde la fecha del certificado y devuelve los días al saldo (lo pagado queda a cuenta); si la incapacidad empieza antes de las vacaciones, estas no inician. Si se registra en días ya marcados como permiso o falta, la incapacidad prevalece: el registro anterior se reclasifica y, si había una falta con expediente disciplinario o descuento, el sistema alerta al Comité del RIT y revierte el descuento.
2. **Permisos legales:** pasan por la cadena, pero la opción «Negar» no existe (salvo el límite de comisionados en A3); solo se pueden devolver para corrección. Las filas legales del catálogo (tabla I del RIT) no se editan ni se quitan.
3. **Paternidad:** se cuenta en días laborables según el catálogo de jornadas de la persona; el sistema excluye descansos y festivos. La duración vive en la tabla de parámetros legales (hoy 5 días; vigilar reforma).
4. **Topes de `PERMISOS_EMPRESA`:** se aplican solos; el exceso pasa a sin goce, como dice la tabla II del RIT.
5. **Incapacidades:** folio, ramo (EG / RT / Maternidad), fechas y días. **No existe campo de diagnóstico.**
6. **D1 y D5 (datos sensibles, decisión 32 del registro):** la evidencia (constancia de detención o arresto, resolución de Declaración Especial de Ausencia) y el tipo del evento solo los ve el personal de RH autorizado para datos sensibles (sección 13). El documento cita la fracción legal, nunca los hechos ni el delito.
7. **B5:** `LIC3_FECHA_REGRESO` ≤ inicio + `LIC3_MAX_DIAS`; la prórroga genera una nueva versión del convenio.
8. **INC-2:** `TRANSF_SEMANAS` de 0 a 4; con más de 0, el archivo de la autorización médica es obligatorio antes de generar el documento.
9. **B1:** `LACTANCIA_FIN` ≤ el máximo legal (cómputo por confirmar: desde el parto o desde el regreso). Con `LACTARIO` = Sí, la trabajadora elige entre reposos y reducción; con `LACTARIO` = No, solo se ofrece la reducción de una hora (RIT, art. 66) y la opción de reposos no aparece. Con Reposos y `UBICACION_LACTARIO` vacío, alerta (no bloquea).
10. **D4:** no se genera SUS-2 sin el visto bueno de consultoría (`D4_VISTO_BUENO`) y sin `SUSP_DOCUMENTO_FUNDAMENTO` (ley o reglamento). Antes de generar SUS-2, la pantalla ofrece la reubicación temporal (MOD-5 del módulo 5, causa «Falta de documentos»):
    - Si la persona la acepta (`D4_REUBICACION` = Sí), la reubicación sustituye a la suspensión mientras dure: no se genera SUS-2, el evento pasa a «Con reubicación», se paga el salario y los días cuentan como trabajados para nómina, IMSS, PTU, aguinaldo y vacaciones.
    - El plazo legal no cambia: `SUSP_LIMITE` = `SUSP_CONOCIMIENTO_FECHA` + 2 meses (arts. 43, fr. IV, y 47, fr. XIV Bis LFT), con las alertas de los días 45 y 60. A los 60 días, consultoría decide.
    - Si la reubicación termina antes de que la persona regularice (`D4_REUBICACION_FIN`), se genera SUS-2 con suspensión desde esa fecha y la misma `SUSP_LIMITE`.
    - Si la persona regulariza, el evento se cierra y MOD-5 concluye con el regreso a su puesto.

---

## 6. Plazos y alertas

Destinatarios: **P** = Persona Trabajadora, **RH**, **J** = jefatura, **C** = consultoría, **Ct** = contador.

| Evento | Plazo | Alerta | Al vencer |
| --- | --- | --- | --- |
| Cada paso de la cadena (A4, B5) | `AUTORIZACION_PLAZO_DIAS` días hábiles desde que lo recibe (por omisión 1) | Autorizador al recibir; autorizador y RH al vencer | La falta de respuesta no es autorización; RH reasigna a un suplente o, si llegó la fecha del permiso, resuelve el mismo día (3.4) |
| Evidencia de un permiso | 10 días hábiles desde el fin del evento | P y RH en los días 5 y 9 | Legal: se conserva con goce; nueva alerta a P y RH; aviso a C. Empresa: casilla `EVIDENCIA_DESCUENTO` (sección 7) |
| Entrega de la incapacidad | 2 días hábiles desde su expedición | P y RH el día 2 | Alerta a RH; los días no se marcan como falta mientras exista aviso de ausencia |
| Aviso de accidente (INC-1) | 72 horas desde el accidente | RH y C inmediata; crítica a las 48 horas | Alerta crítica a C |
| Fallecimiento por riesgo de trabajo | Inmediato | RH y C, crítica | INC-1 con datos de posibles beneficiarios |
| Regreso tras suspensión D | Art. 45: día siguiente (frs. I, II, IV, VII) o dentro de 15 días (frs. III, V, VI) | RH 3 días antes y el día límite | Las ausencias posteriores se registran como faltas; C revisa la vía del RIT |
| Falta de documentos (D4) | Hasta 2 meses desde que la Empresa conoció el hecho, con o sin reubicación | RH y C en los días 45 y 60 | Se actualiza la causa del art. 47, fr. XIV Bis; C decide (con reubicación: mantenerla o rescindir); el sistema no termina la relación |
| Comisión permanente (B4) | Regreso dentro de 6 años | RH anual y 90 días antes del sexto año | C |
| Acuse de LIC-2 | 3 días hábiles desde el envío | RH | Nuevo envío y registro del intento |
| Licencia sin goce (B5) | Fecha de regreso del LIC-3 | P y RH 5 días hábiles antes | Faltas desde el día siguiente |
| Lactancia (B1) | Hasta `LACTANCIA_FIN` | P y RH 15 días antes | Fin automático del acuerdo; la jornada vuelve a la pactada |
| Ausencias sin goce ante el IMSS | 8 o más días consecutivos | Ct y RH, informativa | Sin acción automática (sección 8) |
| Faltas y patrón de ausentismo | Sección 9 | Sección 9 | Sección 9 |

---

## 7. Evidencia vencida y reclasificación

- **Origen Empresa con goce (A4):** al vencer el plazo, RH ve la casilla `EVIDENCIA_DESCUENTO` (Sí/No), precargada según `EVIDENCIA_VENCIDA_EFECTO` (E). Con Sí, el permiso pasa a sin goce y nómina ajusta en el periodo siguiente. El sistema **nunca descuenta solo**: registra quién decidió y cuándo.
- **Reversión:** si la evidencia llega después, el ajuste se revierte en la nómina siguiente a la entrega y el estado pasa a Cerrado.
- **Origen Ley:** no hay descuento. Se conserva con goce, se alerta de nuevo a P y RH y se avisa a C.
- **Dependencia:** la regla está en el art. 31 del RIT. Mientras el RIT del cliente no esté depositado (RIT_ESTADO distinto de «Depositado y vigente»), se recomienda que `EVIDENCIA_VENCIDA_EFECTO` se precargue en Alerta.

---

## 8. Nómina e IMSS

- `DIAS_SIN_GOCE_PERIODO` (S): suma por persona y periodo de pago de los días sin goce (A3 sin compensación, A4 sin goce o reclasificado, B4, B5 y suspensiones D; no incluye D4 en estado «Con reubicación»). Se entrega a nómina.
- **Ausencias sin goce menores de 8 días:** nómina las reporta para la cotización solo del seguro de enfermedades y maternidad (art. 31 LSS; texto oficial por verificar).
- **8 o más días consecutivos sin goce:** el sistema **solo informa** a Ct y RH que procede el aviso de baja por ausentismo. No lo propone por omisión: la persona pierde la cobertura y un aviso de baja cercano a una controversia puede usarse en contra de la Empresa. En B5, la decisión se registra en `LIC3_AVISO_BAJA_IMSS` y se imprime en el LIC-3.
- **Incapacidades:** no se presenta aviso de baja mientras haya una incapacidad en curso.
- **Reingreso:** si hubo aviso de baja por ausentismo, el regreso exige `IMSS_REINGRESO_FECHA` antes de cerrar SUS-3.
- **Días de espera (C1):** si `PAGO_DIAS_ESPERA` = Sí, nómina paga al 100 % los días que no subsidia el IMSS.

---

## 9. Faltas y patrón de ausentismo

**Fuente:** el módulo 9 envía las ausencias sin evento justificado de este módulo ni vacaciones registradas (VAC-1) en dos estados: **falta por confirmar** (PN-01, sin descuento hasta que RH la confirme) y **falta confirmada**. Las que RH descarta no llegan. No cuentan como faltas los permisos autorizados (con o sin goce), las incapacidades, las suspensiones, los días de vacaciones ni los días con evento justificado. Si después llega un evento justificado por esos días (por ejemplo, una incapacidad), la falta se borra, esté confirmada o por confirmar (validación 1).

**Regla de faltas (ventana móvil de 30 días):**

- La ventana es cualquier periodo de 30 días naturales, no el mes calendario. El sistema revisa diario, para cada persona, las faltas de los 30 días que terminan ese día.
- **3 faltas en la ventana (confirmadas y por confirmar):** alerta preventiva a RH, «en el límite», con cada falta etiquetada («confirmada» o «por confirmar»).
- **4.ª falta confirmada en la ventana:** alerta crítica a RH y C: se actualiza la causa del art. 47, fr. X LFT y corre el plazo de un mes para rescindir (art. 517). El sistema muestra la fecha límite (fecha de la cuarta falta + 1 mes; criterio de inicio del plazo por verificar). Solo cuentan las faltas confirmadas.
- **4 o más faltas en la ventana con alguna por confirmar:** alerta a RH, «posible cuarta falta: confirme o descarte las faltas pendientes», porque el plazo para rescindir puede correr desde que la Empresa conoce la falta y no desde que la confirma. No es la alerta crítica.

**Patrón de ausentismo (sin necesidad de llegar a 3 faltas):** cuenta las faltas confirmadas y las por confirmar. El sistema revisa los últimos `ALERTA_PATRON_MESES` meses y alerta a RH y C, con el historial de fechas y el estado de cada falta («confirmada» o «por confirmar»), si se cumple **cualquiera** de estos indicadores:

| Indicador | Regla | Valor por omisión |
| --- | --- | --- |
| Acumuladas | Faltas en el periodo ≥ `ALERTA_PATRON_FALTAS` | 6 |
| Recurrentes | Número de periodos de 30 días del periodo revisado con al menos una falta ≥ `ALERTA_PATRON_RECURRENCIA` | 4 de 6 |
| Pegadas | % de faltas en un día laborable inmediatamente anterior o posterior a un descanso semanal, un día de descanso obligatorio o un día de pago ≥ `ALERTA_PATRON_ADYACENCIA_PCT` | 50 |

- «Inmediatamente anterior o posterior» se calcula con el catálogo de jornadas de la persona y los días de pago de su periodicidad (`DIA_PAGO_SEMANAL` o `DIAS_PAGO_QUINCENAL`, del RIT).
- La alerta de patrón se repite como máximo una vez por mes por persona, salvo que aparezca un indicador nuevo.
- La alerta no genera sanción. Texto fijo de la alerta: «El patrón de ausentismo no es por sí solo causa de rescisión. Atienda cada falta por la vía del RIT; consultoría evalúa si procede otra medida.» La conducta 60 del catálogo de conductas del RIT (ausentismo reiterado) solo puede seleccionarse si existe esta alerta.

---

## 10. Efectos en otros módulos

### 10.1 Tabla de efectos por evento

| Evento | Día computable para PTU | Año de servicios (vacaciones y antigüedad) | Aguinaldo | Salario del día |
| --- | --- | --- | --- | --- |
| A1, A2, B2 y A4 con goce | Sí | Cuenta | Cuenta | Lo paga la Empresa |
| A3 sin compensación, A4 sin goce | No | Cuenta | No | No se paga |
| B1 lactancia | Sí (día laborado) | Cuenta | Cuenta | Íntegro, jornada reducida |
| B3 | No | Cuenta | No | Subsidio del IMSS |
| B4 y B5 | No | Cuenta | No | No se paga |
| C1 | No | Cuenta | No, salvo los días de espera que paga la Empresa con `PAGO_DIAS_ESPERA` = Sí | Subsidio del IMSS; días de espera según `PAGO_DIAS_ESPERA` |
| C2 | Sí | Cuenta | Cuenta | Subsidio del IMSS |
| C3 | Sí | Cuenta | Cuenta | Subsidio del IMSS |
| D1 a D5 (D4 con reubicación: Sí en PTU y aguinaldo, con salario) | No | Cuenta | No, salvo D1 por la fr. III si se acredita que la persona obró en defensa de la Empresa (se pagan salarios) | No se paga |

- Aguinaldo: la columna refleja `AGUINALDO_COMPUTA`, tabla de parámetros por tipo de evento que administra el módulo de vacaciones y aguinaldo (criterio de los días computables para la PTU, registro 4.7). Esa tabla incluye también filas que no son eventos de este módulo (falta injustificada, suspensión disciplinaria y suspensión por fin de temporada, que no computan). B3 no computa (decisión del usuario en el módulo de vacaciones). El criterio cambia sin tocar código.
- **Vacaciones en suspensiones largas (B4, B5, D2, D3):** el año de servicios siempre cuenta para la antigüedad y para la fila de la tabla de días que corresponde. Los días de suspensión reducen en proporción los días del periodo vacacional en que caen (especificación de vacaciones, 3.1, paso 4), salvo que RH marque `SUSP_VACACIONES_GENERA` = Sí al cerrar el evento y capture `VACACIONES_DIAS_GENERADOS`, que el módulo de vacaciones suma a ese periodo. Lectura confirmada (17/11/2026). Reglas para que las dos especificaciones coincidan:
  - `VACACIONES_DIAS_GENERADOS` no puede exceder los días que la reducción quitó por esa suspensión (días de la tabla × días de suspensión ÷ 365, redondeado hacia arriba), para que el periodo nunca supere los días de la tabla.
  - Si la suspensión abarca dos años de servicios, este módulo entrega al de vacaciones los días de suspensión de cada año por separado, y `VACACIONES_DIAS_GENERADOS` se reparte en la misma proporción.
  - Si el periodo se crea en el aniversario con la suspensión todavía en curso, el módulo de vacaciones aplica la reducción con los días transcurridos y suma los días generados cuando RH cierre el evento con Sí.

### 10.2 Interfaces

| Módulo | Qué recibe de este módulo |
| --- | --- |
| Nómina | `DIAS_SIN_GOCE_PERIODO`, ajustes por `EVIDENCIA_DESCUENTO` y su reversión, días de espera, horas de permisos por horas |
| Módulo 3 (PTU, cálculo automático, regla R-4) | Días por persona y tipo de evento para los días computables |
| Módulo 4 (terminación) | `SITUACION_PROTEGIDA` y `SITUACION_PROTEGIDA_TIPO` (alerta crítica con doble confirmación, sin bloqueo), aviso de B4 con doble confirmación, días sin goce para salarios devengados, saldos de vacaciones; D4 vencido para el aviso de rescisión (fr. XIV Bis) |
| Módulo 5 (modificaciones) | Alerta de regreso al mismo puesto durante un año desde el parto (C3); reubicación en D4 con MOD-5: si la persona la acepta, el módulo 5 devuelve `D4_REUBICACION` = Sí y su fecha de fin, y este módulo no genera SUS-2 (validación 10). La lactancia y la licencia sin goce **no** son modificaciones; `INCAPACIDAD_PARCIAL` e `INCAPACIDAD_PARCIAL_FECHA` al cerrar C2 (situación protegida del módulo 5) |
| Módulo 9 (jornada) | Eventos que justifican ausencias; jornada esperada reducida en B1; recibe de vuelta las ausencias sin evento como «falta por confirmar» y «falta confirmada» para la sección 9 |
| Vacaciones y aguinaldo | Eventos por persona y fecha (bloqueo de fechas y regla de interrupción por incapacidad); días generados en suspensiones largas cuando RH lo decide; días de cada evento para el aguinaldo con `AGUINALDO_COMPUTA`. Este módulo recibe de vuelta los días de vacaciones (VAC-1) para la validación 1 y para no marcar faltas |

---

## 11. Situaciones protegidas y baja

- `SITUACION_PROTEGIDA` (S) = Sí mientras exista: C1 o C2 en curso, C3, B1, D5 o B3. No bloquea la baja (decisión 19 del mapa, 15/11/2026): el módulo 4 la muestra como alerta crítica y pide doble confirmación, con registro de usuario, fecha y hora en `BAJA_CONFIRMACION_PROTEGIDA` (variable del módulo 4). Texto de la alerta: «Esta persona está en una situación que la ley protege ({{SITUACION_PROTEGIDA_TIPO}}). Darla de baja puede generar un reclamo. ¿Confirma que lo revisó con consultoría?». No se imprime. Es la parte que aporta este módulo: el módulo 4 suma las demás situaciones protegidas del registro (embarazo informado, representante obrero en funciones).
- **B4 vigente:** no bloquea. Al intentar la baja, el módulo 4 muestra: «Esta persona tiene una licencia por comisión permanente con derecho a regresar a su puesto hasta el {{COMISION_FECHA_LIMITE}}. Darla de baja puede generar un reclamo. ¿Confirma la baja?» y pide una segunda confirmación. Registra usuario y fecha en `BAJA_CONFIRMACION_B4`.

---

## 12. Documentos y registros

Los textos están en la sección 17. Esta tabla define cuándo se genera cada pieza, quién firma y cómo sale.

### 12.1 Catálogo

| Clave | Pieza | Tipo | Se genera | Firma o acuse |
| --- | --- | --- | --- | --- |
| SP-1 | Registro de permiso | Registro | A1 a A4 y B2 | Nadie firma; constancia exportable o formato de respaldo (12.3) |
| LIC-1 | Acuerdo de lactancia (módulo A reposos, B reducción) | Documento | B1 | Trabajadora y RH designado, según `FIRMA_MODALIDAD` |
| LIC-2 | Notificación de licencia por comisión permanente | Notificación | B4 | Acuse de la persona por la Plataforma o el correo |
| LIC-3 | Convenio de licencia sin goce | Documento | B5, al terminar la cadena de autorización | Persona y RH designado, según `FIRMA_MODALIDAD` |
| INC-1 | Aviso de accidente de trabajo | Documento externo | C2 por accidente; fallecimiento | Representante de la Empresa (`REP_NOMBRE`), con e.firma o autógrafa |
| INC-2 | Solicitud de transferencia de semanas prenatales | Documento | C3 con `TRANSF_SEMANAS` > 0 | Trabajadora y RH designado, según `FIRMA_MODALIDAD` |
| SUS-1 | Constancia de suspensión | Documento | D1, D2, D3 | RH designado; la persona si está disponible; negativa con testigos |
| SUS-2 | Aviso de suspensión por falta de documentos | Documento | D4 | RH designado; la persona firma de recibido; negativa con testigos |
| SUS-3 | Lista de reincorporación | Registro | Fin de B4, B5 y toda D; fin de C2 o C3 de más de `REINCORPORACION_UMBRAL_DIAS` | La persona confirma en la Plataforma y RH valida |

### 12.2 Firma

- **Persona Trabajadora.** Rige la «Especificación de firma electrónica»: con `FIRMA_MODALIDAD` = Electrónica, firma según `TIPO_FIRMA` (FES con código al correo y, según `FES_CANAL_OTP`, al celular; o e.firma), con los estados, la bitácora, la hoja de evidencias, el hash SHA-256, la copia al correo personal y la constancia NOM-151 (solo si `NOM151_SERVICIO` = Sí) que ahí se describen.
- **Empresa.** En LIC-1, LIC-3, INC-2, SUS-1 y SUS-2 firma la persona de RH designada (`FIRMANTES_EMPRESA`), conforme a la especificación de firma electrónica v1.2: designación firmada por el representante con e.firma (5.6), firma con usuario y código de un solo uso a su correo institucional y, según `FES_CANAL_OTP`, a su celular, o con su e.firma si la registró (5.5); tipo «RH designado» en `FIRMA_EMPRESA_DOC` (sección 11). `FIRMA_EMPRESA_NOMBRE` y `FIRMA_EMPRESA_CARGO` se toman del firmante. El firmante de RH no firma un documento en el que él mismo es la Persona Trabajadora.
- **Excepción.** INC-1 lo firma el representante legal (`REP_NOMBRE`) con e.firma, por el flujo de la especificación de firma electrónica, o de forma autógrafa.
- **Sin firmante de RH vigente.** El documento pasa al representante, con alerta; no se manda a papel (especificación de firma electrónica, sección 11).
- Si la Plataforma falla o la persona no puede usarla, se firma de forma autógrafa.
- La negativa a firmar (SP-1 y SUS-3 con respaldo, SUS-1 y SUS-2) se documenta con dos testigos y envío al correo personal (`NEGATIVA_FIRMA`).
- En el formato de respaldo de SP-1 firman quienes autorizaron, en el orden de la cadena.

### 12.3 Registros digitales (SP-1 y SUS-3) y notificación (LIC-2)

- El registro de la Plataforma es la prueba: guarda usuario, fecha y hora, IP y dispositivo de cada acción (misma bitácora del corte de firma electrónica) y no se puede alterar sin dejar rastro.
- **`SALIDA` = Constancia** (por omisión): el sistema exporta la constancia con el cierre de bitácora (fechas y horas de solicitud, resolución o confirmación, y quién las hizo). No lleva firmas.
- **`SALIDA` = Respaldo:** formato en papel para personal sin dispositivo o falla del sistema. Lleva firmas. RH lo captura en la Plataforma el mismo día y marca «documento firmado»; la imagen del original es opcional (alerta si falta, sin bloqueo).
- **LIC-2:** se envía por la Plataforma y al correo personal; sin acuse en 3 días hábiles, alerta y reenvío.
- El sistema exporta un paquete probatorio por evento: documento o constancia, hoja de evidencias y evidencia del evento.

---

## 13. Privacidad y accesos

| Dato | Quién lo ve |
| --- | --- |
| Certificados de incapacidad (folio, ramo, fechas) | RH y la persona; la jefatura solo ve «Incapacidad» y las fechas |
| Evidencia de D1 y D5 (constancia de detención o arresto, resolución de Declaración Especial de Ausencia), SUS-1 de D1 y el tipo de esos eventos | Solo el personal de RH autorizado para datos sensibles (`DATOS_SENSIBLES_ACCESO`, configuración de la empresa); consultoría, solo si la Empresa la incluye en esa lista. Son datos sensibles (decisión 32 del registro; inciso m del aviso de privacidad) |
| D1 y D5 para la jefatura, la dirección y en reportes generales | Solo «Suspensión» y las fechas; nunca el tipo, la fracción ni la evidencia |
| Diagnósticos | No se capturan |
| Licencia del IMSS por hijo con cáncer | RH y la persona; la jefatura solo ve «Licencia» y las fechas |
| Motivo de un permiso de asuntos personales | No se pide |

El aviso de privacidad para personas trabajadoras ya cubre estos datos: incapacidades con folio, ramo y fechas, y la privación de la libertad y la ausencia declarada como datos sensibles (inciso m), con consentimiento expreso. Cada consulta de la evidencia de D1 y D5 queda en la bitácora (usuario, fecha y hora).

---

## 14. Diccionario de variables

### 14.1 Reutilizadas

Del contrato y del kit: `PATRON_RAZON_SOCIAL`, `PATRON_DOMICILIO`, `REP_NOMBRE`, `REP_CARACTER`, `TRAB_NOMBRE`, `TRAB_CURP`, `TRAB_DOMICILIO`, `TRAB_EMAIL`, `PUESTO`, `SALARIO_PERSONA` (INC-1: el de la versión de condiciones de la persona en la fecha del accidente), `AREA`, `LUGAR_FIRMA`, `FECHA_FIRMA`, `FIRMA_MODALIDAD`, `NEGATIVA_FIRMA`, `CLAUSULA_FIRMA_ELECTRONICA`, `BENEF_CONFIRMACION_FECHA`. Del RIT: `PERMISOS_EMPRESA`, `PERMISO_LEY_*`, `PAGO_DIAS_ESPERA`, `UBICACION_LACTARIO`, `LACTARIO_EQUIPAMIENTO`. De la especificación de firma electrónica: `TIPO_FIRMA`, `MEDIO_IDENTIFICACION`, `FES_CANAL_OTP`, `NOM151_SERVICIO`, `FIRMA_ENLACE_DIAS`, `FIRMA_EVIDENCIA`, `PORTAL_DESCARGA`. Catálogo de jornadas y calendario de días inhábiles.

Del RIT: `PERSONA_JEFATURA` (jefatura inmediata, tomada del organigrama; el registro, 5.1, no la captura en el alta). Por confirmar el nombre en el diccionario único: `CENTRO_TRABAJO` (equivale a `PERSONA_CENTRO` del RIT) y `DIRECTOR_AREA` (nueva).

### 14.2 Variables del módulo

| Variable | Nivel | Tipo | Validación | Activa |
| --- | --- | --- | --- | --- |
| EVIDENCIA_VENCIDA_EFECTO | E | Sin goce / Alerta | Ver sección 7 | Precarga de EVIDENCIA_DESCUENTO |
| LIC3_MAX_DIAS | E | Entero | > 0; por omisión 90 | Tope de B5 |
| REINCORPORACION_UMBRAL_DIAS | E | Entero | Por omisión 30 | SUS-3 en C2 y C3 |
| ALERTA_PATRON_MESES | E | Entero | Por omisión 6 | Sección 9 |
| ALERTA_PATRON_FALTAS | E | Entero | Por omisión 6 | Sección 9 |
| ALERTA_PATRON_RECURRENCIA | E | Entero | ≤ periodos de 30 días en la ventana; por omisión 4 | Sección 9 |
| ALERTA_PATRON_ADYACENCIA_PCT | E | Porcentaje | 1 a 100; por omisión 50 | Sección 9 |
| AUTORIDAD_INSPECCION | E | Texto (solo el nombre de la autoridad; el ámbito sale de `COMPETENCIA`) | Diccionario único, 1.1 (decisión P2); sin valor por omisión | INC-1 |
| AGUINALDO_COMPUTA | E (global; la administra el módulo de vacaciones y aguinaldo) | Tabla: tipo de evento, Sí/No | Valores de la sección 10.1; B3 por omisión No | Aguinaldo |
| PARAMETROS_LEGALES_PERMISOS | E (global) | Tabla con vigencia: días de paternidad, semanas de maternidad y adopción, meses de lactancia, plazo de suspensión por falta de documentos, plazo de comisión permanente | Solo se activan aprobados | Validaciones y alertas |
| EVENTO_FOLIO | S | Texto | Único por empresa | Todos |
| EVENTO_TIPO | V | Lista A1 a D6 | Obligatoria | Todo el flujo |
| EVENTO_FECHA_INICIO / EVENTO_FECHA_FIN / EVENTO_HORARIO | V | Fecha / fecha / hora | Sin traslape de día completo; horario solo en permisos por horas | Todos |
| EVENTO_ESTADO | V/S | Sección 4 | «Negado» solo en origen Empresa y, en A3, por el número de comisionados | Alertas |
| PERMISO_ORIGEN | S | Ley / Empresa | Del tipo | SP-1, reglas |
| EVENTO_TIPO_NOMBRE / EVENTO_GOCE | S | Texto | Del catálogo y la resolución | SP-1 |
| EVIDENCIA_DESCRIPCION | Catálogo | Texto | De la tabla I o II del RIT | SP-1 |
| EVENTO_EVIDENCIA | V | Archivo | — | Cierre |
| EVIDENCIA_FECHA_LIMITE | S | Fecha | Fin del evento + 10 días hábiles | Alertas |
| EVIDENCIA_DESCUENTO | V | Sí/No + usuario y fecha | Solo origen Empresa con goce, al vencer | Nómina; reversión |
| RESOLUCION_FECHA | V | Fecha | ≥ solicitud | SP-1 |
| NEGATIVA_MOTIVO / FECHA_ALTERNA | V | Texto / fecha | Motivo obligatorio al negar | SP-1 |
| AVISO_URGENTE / AVISO_URGENTE_MEDIO / AVISO_URGENTE_FECHA | V | Sí/No / texto / fecha | Medio y fecha obligatorios con Sí | SP-1 |
| FIRMA_EMPRESA_NOMBRE / FIRMA_EMPRESA_CARGO | S | Texto | Del firmante designado (FIRMANTES_EMPRESA); en SUS-3, de quien valida en RH | Firmas |
| FIRMANTES_EMPRESA | E | Tabla (especificación de firma electrónica, 3.1) | La define y valida la especificación de firma electrónica; sin firmante vigente, firma el representante | Firma de la Empresa (12.2) |
| LACTARIO | E (del RIT) | Sí/No | Sí por omisión | Con No, LIC-1 solo admite reducción (validación 9) |
| CADENA_AUTORIZACION | E | Pasos ordenados: Jefatura, RH, Dirección | RH obligatorio; por omisión los tres | 3.4 |
| PERMISOS_EMPRESA, columna «Autorizan» | E (catálogo) | Subconjunto de CADENA_AUTORIZACION | Incluye RH; por omisión la cadena completa | 3.4 |
| AUTORIZACION_PLAZO_DIAS | E | Entero | 1 a 5; por omisión 1 | Alertas de la cadena |
| PERSONA_JEFATURA / DIRECTOR_AREA | O | Usuario | Dirección opcional; pueden ser la misma persona | 3.4 |
| NEGATIVA_CAUSA | V | Requisitos no subsanados / Necesidad operativa concreta / Número de comisionados (solo A3) / Cupo completo (solo módulo de vacaciones) | Obligatoria al negar o reprogramar; «Cupo completo» no aparece en las pantallas de este módulo | 3.3, 3.4; VAC-1 |
| AUTORIZADOR_SUPLENTE | V | Usuario + quién reasignó y cuándo | Solo RH reasigna | 3.4 |
| AUTORIZACIONES | S | Lista: nombre, cargo, fecha y hora de cada paso | De la bitácora | SP-1 |
| DEVOLUCION_MOTIVO | V | Texto | Obligatorio al devolver | 3.4 |
| NEGATIVA_AUTOR / NEGATIVA_NIVEL | S | Nombre y cargo / Jefatura, RH, Dirección | Del paso que negó | SP-1 |
| TESTIGO_1_NOMBRE / TESTIGO_2_NOMBRE / FECHA_ENVIO | V | Texto / fecha | Obligatorios con NEGATIVA_FIRMA = Sí | Bloque de negativa |
| SALIDA | V (al exportar) | Constancia / Respaldo | Por omisión Constancia | SP-1, SUS-3 |
| CONSTANCIA_FECHA | S | Fecha | Fecha de exportación | SP-1, SUS-3 |
| EVENTO_SOLICITUD_FECHAHORA / EVENTO_RESOLUCION_FECHAHORA / CONFIRMACION_FECHAHORA | B | Fecha y hora | No editables | Constancias |
| COMISION_TIPO / COMISION_ORGANO / COMISION_GOCE | V | Accidental, Permanente / texto / Con goce, Sin goce salvo compensación | COMISION_GOCE obligatoria en A3, sin valor por omisión | SP-1, LIC-2 |
| COMISION_CARGO / COMISION_DOCUMENTO / COMISION_DOCUMENTO_FECHA | V | Texto / archivo / fecha | Obligatorios en B4 | LIC-2 |
| COMISION_FECHA_LIMITE | S | Fecha | Inicio + plazo legal | LIC-2, alertas, baja |
| ACUSE_MEDIO / ACUSE_FECHAHORA | B | Plataforma, Correo / fecha y hora | — | LIC-2 |
| LIC3_SOLICITUD_FECHA / LIC3_FECHA_REGRESO / LIC3_CAUSA | V | Fecha / fecha / texto opcional | Solicitud no posterior al inicio; regreso ≤ inicio + LIC3_MAX_DIAS | LIC-3 |
| LIC3_AVISO_BAJA_IMSS | V | Sí/No | Solo con 8 días o más; lo marca Ct con RH | LIC-3 |
| LACTANCIA_MODALIDAD / LACTANCIA_INICIO / LACTANCIA_HORARIO | V | Reposos, Reducción / fecha / horas | La trabajadora elige la modalidad (con LACTARIO = No, solo Reducción); inicio no anterior al regreso posnatal | LIC-1, jornada |
| LACTANCIA_FIN | S | Fecha | ≤ máximo legal | LIC-1, alertas |
| INCAP_FOLIO / INCAP_RAMO / INCAP_DIAS | V | Texto / EG, RT, Maternidad / entero | Folio obligatorio; sin diagnóstico | C1 a C3 |
| INCAPACIDAD_PARCIAL / INCAPACIDAD_PARCIAL_FECHA | V (al cerrar C2) | Sí/No / fecha | Se pregunta siempre al cerrar C2; con Sí, fecha del dictamen del IMSS obligatoria y el dictamen como evidencia (sin diagnóstico); sin dictamen todavía, alerta a RH a los 30 días | Situación protegida del módulo 5 y antecedente de la readaptación; no se imprime |
| RT_FECHA_HORA / RT_LUGAR / RT_HECHOS / RT_TESTIGOS / RT_ATENCION | V | Fecha y hora / texto / texto / tabla / texto | Obligatorios en accidente | INC-1 |
| RT_FALLECIMIENTO / RT_FALLECIMIENTO_FECHA / RT_POSIBLES_BENEFICIARIOS | V | Sí/No / fecha / tabla | Precarga de la designación de beneficiarios, editable | INC-1 |
| FECHA_PROBABLE_PARTO / PRENATAL_INICIO | V / S | Fecha | Del certificado del IMSS | INC-2 |
| TRANSF_SEMANAS / TRANSF_AUTORIZACION / TRANSF_AUTORIZACION_FECHA / TRANSF_MEDICO_ORIGEN | V | 0 a 4 / archivo / fecha / IMSS, Servicio de salud de la Empresa, Médico particular | Autorización obligatoria con > 0 | INC-2 |
| TRANSF_OPINION / TRANSF_OPINION_TEXTO | V | Sin objeción, Con observaciones / texto | Texto obligatorio con observaciones | INC-2 |
| SUSP_FRACCION | V | III, IV, V, VI, VII, IX (D5) | Obligatoria en D | SUS-1, SUS-2, plazos |
| SUSP_EVIDENCIA / SUSP_EVIDENCIA_FECHA / SUSP_CARGO / SUSP_ORGANISMO | V | Archivo / fecha / texto / texto | Según la fracción | SUS-1 |
| TRAB_DISPONIBLE_FIRMA | V | Sí/No | Por omisión Sí | SUS-1 |
| SUSP_REGRESO_LIMITE | S | Fecha | Art. 45 | Alertas |
| SUSP_DOCUMENTO / SUSP_DOCUMENTO_FUNDAMENTO / SUSP_DOCUMENTO_ESTADO / SUSP_DOCUMENTO_VENCIMIENTO | V | Texto / texto / Vencido, No presentado / fecha | Fundamento obligatorio | SUS-2 |
| SUSP_CONOCIMIENTO_FECHA / SUSP_IMPUTABILIDAD | V | Fecha / texto | Obligatorios en D4 | SUS-2 |
| SUSP_LIMITE | S | Fecha | Conocimiento + 2 meses | SUS-2, alertas |
| DATOS_SENSIBLES_ACCESO | E | Lista de usuarios de RH (y, si la Empresa lo decide, de consultoría) | Al menos uno; nombre por confirmar en el diccionario único | Acceso a la evidencia y al tipo de D1 y D5 (sección 13) |
| D4_VISTO_BUENO | V | Usuario de consultoría y fecha | Obligatorio para generar SUS-2 | SUS-2 |
| D4_REUBICACION / D4_REUBICACION_FIN | S (del módulo 5, MOD-5 aceptada) | Sí/No / fecha | Solo D4; con Sí no se genera SUS-2 mientras dure | Estado «Con reubicación»; SUS-2 al terminar sin regularizar |
| EVENTO_ORIGEN_TIPO / EVENTO_ORIGEN_NOMBRE / EVENTO_ORIGEN_INICIO / EVENTO_ORIGEN_FIN | S | Del evento que termina | — | SUS-3 |
| REINCORPORACION_FECHA | V | Fecha | ≥ fin del evento | SUS-3 |
| EXAMEN_RETORNO / EXAMEN_RETORNO_FECHA | V | Sí/No / fecha | Según las reglas de exámenes del RIT | SUS-3 |
| HERRAMIENTAS_SUSPENDIDAS | V | Sí/No | Sí si se aplicó la devolución temporal del LIC-3 | SUS-3 |
| BENEF_CONFIRMACION_VENCIDA | S | Sí/No | Más de 12 meses desde BENEF_CONFIRMACION_FECHA | SUS-3 |
| IMSS_REINGRESO_FECHA | V | Fecha | Obligatoria si hubo aviso de baja por ausentismo | SUS-3 |
| SUSP_VACACIONES_GENERA / VACACIONES_DIAS_GENERADOS | V | Sí/No / entero | Solo B4, B5, D2, D3; decide RH | SUS-3, vacaciones |
| SITUACION_PROTEGIDA / SITUACION_PROTEGIDA_TIPO | S | Sí/No / texto (Incapacidad en curso, Maternidad, Lactancia, Declaración Especial de Ausencia, Licencia por hijo con cáncer) | Sección 11 | Alerta crítica con doble confirmación en el módulo 4; no se imprime |
| BAJA_CONFIRMACION_B4 | V (módulo 4) | Usuario y fecha | Obligatoria si hay B4 vigente | Baja |
| DIAS_SIN_GOCE_PERIODO | S | Entero por persona y periodo | — | Nómina, IMSS, PTU |
| FALTAS_VENTANA_30_CONFIRMADAS / FALTAS_VENTANA_30_POR_CONFIRMAR | S | Entero por persona y día | Sección 9; la alerta crítica solo usa las confirmadas | Alertas de faltas |
| PATRON_INDICADORES | S | Registro: indicador cumplido, valor, fechas y estado de cada falta | Sección 9 | Alerta de patrón |

### 14.3 Eliminadas (no programar)

`ALERTA_PATRON_VENTANAS` (sustituida por los tres indicadores de la sección 9). `TRIBUNAL_COMPETENTE` (decisión del 12/11/2026: INC-1 menciona al Tribunal laboral competente con texto fijo). `JEFE_INMEDIATO` (se usa `PERSONA_JEFATURA`).

---

## 15. Dependencias

| Pieza | Qué necesita este módulo |
| --- | --- |
| RIT (especificación v1.4) | Art. 30 (cadena de autorización, incluidos los permisos que otorga la Ley, sin negarlos; si llega la fecha sin autorización completa, RH los registra) y art. 33 (causas de negativa y solicitud sin respuesta); art. 16 y tabla II, asuntos personales (se autorizan conforme al art. 30); tablas I y II del art. 31 (catálogo y regla de evidencia); art. 66 (LACTARIO); art. 25 (días de pago); conducta 60; reglas de exámenes de retorno |
| Contrato | Cláusula de formalización por medios electrónicos |
| Especificación de firma electrónica (v1.2) | Bitácora, hoja de evidencias, hash, envío al correo, firma autógrafa sustituta; firmante de RH designado (FIRMANTES_EMPRESA, FIRMA_EMPRESA_DOC, sección 11) |
| Organigrama | Jefatura inmediata y dirección del área de cada puesto |
| Kit de contratación | Designación de beneficiarios; inventario de la carta responsiva |
| Módulo 4 | Bloqueo por situación protegida y doble confirmación por B4; calendario de días inhábiles |
| Módulo 9 | Ausencias sin evento, por confirmar y confirmadas (fuente de faltas) |
| Módulo de vacaciones y aguinaldo | Registro de vacaciones (VAC-1) como segunda fuente de ausencias justificadas; regla de interrupción de las vacaciones por incapacidad; tabla `AGUINALDO_COMPUTA` |
| Catálogo de jornadas | Días laborables, descansos y festivos de cada persona |
| Días de pago del RIT (DIA_PAGO_SEMANAL, DIAS_PAGO_QUINCENAL) | Indicador «pegadas» del patrón de ausentismo |

## 16. Pendientes que no bloquean la programación

- Verificar el texto oficial del art. 31 LSS y de los subsidios de incapacidad y maternidad; quién paga la adopción de madres; desde cuándo corren los meses de lactancia; Infonavit durante incapacidades y ausencias; ley de Declaración Especial de Ausencia; inicio del plazo de prescripción por faltas; criterios sobre la fr. XV aplicada al ausentismo sistemático; formato vigente del IMSS de probable riesgo de trabajo; reforma de paternidad (5 días vigentes). Si cambian, afectan parámetros y, en su caso, textos (nueva versión del modelo), no la estructura.

---

## 17. Textos de los documentos y registros

Textos revisados por el usuario (12/11/2026). Se programan tal como están.

**Reglas de armado**

- `{{VARIABLE}}` se sustituye por el valor capturado; `[SI …] … [FIN SI]` se evalúa y la marca nunca se imprime. Las condiciones con «no vacía» se cumplen cuando la variable tiene valor.
- Las «Notas para programación» y los párrafos que dicen en qué evento se genera cada pieza no se imprimen.
- Todo documento lleva el encabezado y el bloque de datos de la persona (17.1), salvo INC-1, que lleva sus datos en el cuerpo y su propio cierre.
- Bloque de cierre y firma: se imprime en LIC-1, LIC-3, INC-2, SUS-1 y SUS-2; en SP-1 y SUS-3 solo con `SALIDA` = Respaldo; LIC-2 no lo lleva (lleva el acuse); INC-1 usa su propio cierre. En el respaldo de SP-1, el lado de la Empresa lleva una línea de firma por cada paso de la cadena (nombre y cargo de cada autorizador), en el orden de la cadena.
- Bloque de negativa a firmar: SP-1 y SUS-3 con `SALIDA` = Respaldo, SUS-1 y SUS-2.
- En SUS-3 la numeración y las viñetas se recalculan según los apartados activos.
- Cifras escritas en el texto: «media hora» y «una hora» (LIC-1), «seis años» (LIC-2), «dos meses» (SUS-2), «quince días» (SUS-1) y «cinco días hábiles» (LIC-3, pactada). Son cifras legales estables o pactadas. Si se modifica en `PARAMETROS_LEGALES_PERMISOS` alguna de las legales, el sistema avisa que el texto debe revisarse y no genera el documento con la cifra anterior.
- Todos los textos se versionan: cada documento generado guarda la versión del modelo con la que se emitió.

### 17.1 Bloques comunes

Todos los documentos comparten encabezado, datos de la persona, cierre y firma. Así el ingeniero arma una sola plantilla y cada documento solo aporta su cuerpo.

**Encabezado**

> {{PATRON_RAZON_SOCIAL}} [TÍTULO DEL DOCUMENTO] · Folio {{EVENTO_FOLIO}}

**Datos de la persona** (bloque fijo bajo el encabezado)

> Persona Trabajadora: {{TRAB_NOMBRE}} · CURP: {{TRAB_CURP}}  
> Puesto: {{PUESTO}} · Área: {{AREA}} · Centro de trabajo: {{CENTRO_TRABAJO}}

**Cierre y firma**

> {{LUGAR_FIRMA}}, a {{FECHA_FIRMA}}.  
> [SI FIRMA_MODALIDAD = Electrónica] {{CLAUSULA_FIRMA_ELECTRONICA}} [FIN SI]  
> LA PERSONA TRABAJADORA · LA EMPRESA ({{FIRMA_EMPRESA_NOMBRE}}, {{FIRMA_EMPRESA_CARGO}})

**Negativa a firmar** (SP-1 y SUS-3 con SALIDA = Respaldo, SUS-1 y SUS-2)

> [SI NEGATIVA_FIRMA = Sí] La Persona Trabajadora se negó a firmar el presente documento, que se le leyó y entregó en presencia de {{TESTIGO_1_NOMBRE}} y {{TESTIGO_2_NOMBRE}}, quienes firman como testigos. Una copia se envió el {{FECHA_ENVIO}} al correo personal {{TRAB_EMAIL}}. [FIN SI]

**Notas para programación**

- Quien firma por la Empresa no es siempre el representante legal: en los documentos firma la persona de Recursos Humanos que la Empresa designe (FIRMANTES_EMPRESA), y los permisos se autorizan en la Plataforma por la cadena de autorización, sin firma del representante. Por eso se usan FIRMA_EMPRESA_NOMBRE y FIRMA_EMPRESA_CARGO y no REP_NOMBRE. Solo INC-1 lo firma el representante.
- Los documentos no repiten la Ley: remiten a ella cuando la duración o el pago dependen de una cifra que puede cambiar.

**Registros digitales (12/11/2026).** Cuando el evento se solicita y resuelve en la Plataforma, el registro es la prueba y no se firma un documento aparte. El registro guarda quién hizo cada acción, la fecha y hora, y no se puede alterar sin dejar rastro. El sistema emite una constancia exportable cuando se necesita (inspección, conciliación, juicio). Para personal sin acceso a un dispositivo o si el sistema falla, se usa el formato en papel de respaldo, que RH captura en la Plataforma el mismo día. Su valor probatorio descansa en la cláusula de formalización por medios electrónicos del contrato y en el «Corte - Firma electrónica» (sección 12.2).

### 17.2 SP-1. Registro de permiso (constancia exportable y formato de respaldo)

Eventos A1 a A4 y B2. No se firma: la solicitud y la resolución quedan en la Plataforma. El texto siguiente es la constancia que el sistema exporta y, impreso, el formato en papel de respaldo; solo el respaldo lleva firmas.

**I. Solicitud**

La Persona Trabajadora solicita el permiso siguiente, en los términos del Reglamento Interior de Trabajo:

| Concepto | Dato |
| --- | --- |
| Permiso | {{EVENTO_TIPO_NOMBRE}} |
| Fechas | Del {{EVENTO_FECHA_INICIO}} al {{EVENTO_FECHA_FIN}} |
| Horario (solo permisos por horas) | {{EVENTO_HORARIO}} |
| Salario | {{EVENTO_GOCE}} |
| Evidencia que debe entregarse | {{EVIDENCIA_DESCRIPCION}}, a más tardar el {{EVIDENCIA_FECHA_LIMITE}} |

[SI AVISO_URGENTE = Sí] Por la urgencia del caso, la Persona Trabajadora avisó por {{AVISO_URGENTE_MEDIO}} el {{AVISO_URGENTE_FECHA}}, y completa esta solicitud a su regreso. [FIN SI]

[SI EVENTO_TIPO = A3] La Persona Trabajadora desempeñará una comisión accidental de {{COMISION_ORGANO}}, de la que dio aviso con oportunidad. [SI COMISION_GOCE = Sin goce salvo compensación] El tiempo de la comisión no se paga, salvo que la Persona Trabajadora lo compense con un tiempo igual de trabajo efectivo, en las fechas que acuerde con su jefatura. [FIN SI] [SI COMISION_GOCE = Con goce] La Empresa pagará el salario del tiempo de la comisión. [FIN SI] [FIN SI]

[SI PERMISO_ORIGEN = Ley] Este permiso lo otorga la Ley. La evidencia no lo condiciona: sirve para acreditar su otorgamiento. Si no se entrega en el plazo, la Empresa la requerirá de nuevo a la Persona Trabajadora. [FIN SI]

[SI PERMISO_ORIGEN = Empresa Y EVENTO_GOCE = Con goce] Si la Persona Trabajadora no entrega la evidencia en el plazo, la Empresa podrá tener el permiso por otorgado sin goce de salario y ajustar el importe en la nómina siguiente. Si la entrega después, el ajuste se revertirá en la nómina siguiente a la entrega. [FIN SI]

**II. Resolución**

[SI EVENTO_ESTADO = Registrado] Permiso registrado por Recursos Humanos el {{RESOLUCION_FECHA}}. [FIN SI]

[SI EVENTO_ESTADO = Autorizado] Permiso autorizado el {{RESOLUCION_FECHA}}, {{EVENTO_GOCE}}, por: {{AUTORIZACIONES}}. [FIN SI]

[SI EVENTO_ESTADO = Negado] {{NEGATIVA_AUTOR}} no autorizó el permiso el {{RESOLUCION_FECHA}}, por el motivo siguiente: {{NEGATIVA_MOTIVO}}. [SI FECHA_ALTERNA no vacía] Se propone como fecha alterna el {{FECHA_ALTERNA}}. [FIN SI] [SI NEGATIVA_NIVEL = Jefatura] Si la Persona Trabajadora no está de acuerdo, puede pedir a Recursos Humanos que revise la negativa; Recursos Humanos resolverá el mismo día. [FIN SI] [FIN SI]

**III. Efectos**

El permiso no modifica las condiciones de trabajo. [SI EVENTO_GOCE = Sin goce] El tiempo sin goce no se paga y no se cuenta como día trabajado para la participación de utilidades; no interrumpe la antigüedad. [FIN SI]

[SI SALIDA = Constancia] Constancia emitida por la Plataforma el {{CONSTANCIA_FECHA}} a partir del registro {{EVENTO_FOLIO}}: solicitud registrada el {{EVENTO_SOLICITUD_FECHAHORA}} por {{TRAB_NOMBRE}}; resolución registrada el {{EVENTO_RESOLUCION_FECHAHORA}}, en los términos del apartado II. [FIN SI]

[SI SALIDA = Respaldo] Formato de respaldo. Se usa cuando la Persona Trabajadora no tiene acceso a la Plataforma o el sistema falla. Recursos Humanos lo captura en la Plataforma el mismo día y conserva el original. [FIN SI]

**Notas para programación.** La opción «Negado» no existe cuando PERMISO_ORIGEN = Ley, salvo el límite de comisionados en A3. Al vencer el plazo de la evidencia, RH decide con la casilla EVIDENCIA_DESCUENTO si descuenta o no. El sistema la precarga según EVIDENCIA_VENCIDA_EFECTO y registra quién decidió y cuándo; nunca descuenta solo. La regla está en el art. 31 del RIT. Los permisos de la Empresa (A4) se autorizan en la Plataforma por la cadena de autorización (jefatura inmediata, RH y, si existe, dirección del área); los que otorga la Ley también pasan por la cadena, sin opción de negar. En el formato de respaldo firman quienes autorizan, en ese orden.

### 17.3 LIC-1. Acuerdo de lactancia

Se genera en el evento B1. Módulo A (reposos) o módulo B (reducción de jornada), según LACTANCIA_MODALIDAD; la trabajadora elige. Con LACTARIO = No, solo se genera el módulo B.

La Empresa y la Persona Trabajadora celebran el presente acuerdo para el ejercicio del derecho de lactancia, al tenor de las cláusulas siguientes.

**Primera. Objeto y periodo.** Este acuerdo regula cómo ejerce la Persona Trabajadora su derecho de lactancia del {{LACTANCIA_INICIO}} al {{LACTANCIA_FIN}}, periodo que no excede el máximo que fija la Ley.

**Segunda. Modalidad elegida.** La Persona Trabajadora eligió libremente la modalidad siguiente:

[SI LACTANCIA_MODALIDAD = Reposos] Dos reposos extraordinarios por día, de media hora cada uno, en el horario {{LACTANCIA_HORARIO}}, en el espacio para lactancia ubicado en {{UBICACION_LACTARIO}}. Los reposos son tiempo de trabajo pagado y no se descuentan. [FIN SI]

[SI LACTANCIA_MODALIDAD = Reducción] Las partes acuerdan reducir en una hora su jornada diaria durante el periodo. Su horario será {{LACTANCIA_HORARIO}}. La reducción no disminuye su salario ni sus prestaciones, y la hora reducida no se registra como retardo, salida anticipada ni falta. [FIN SI]

**Tercera. Cambio de modalidad o término anticipado.** La Persona Trabajadora puede pedir por escrito, en cualquier momento, cambiar de modalidad o terminar el acuerdo antes de la fecha prevista. El cambio surte efectos el día hábil siguiente a la solicitud y se documenta con un nuevo acuerdo.

**Cuarta. Cambio de horario.** Si cambia el turno u horario de la Persona Trabajadora, el horario de los reposos o de la jornada reducida se ajusta por escrito, sin disminuir el derecho.

**Quinta. Conclusión.** El acuerdo concluye el {{LACTANCIA_FIN}} sin necesidad de aviso. Desde el día siguiente rige la jornada pactada en el contrato de trabajo.

**Sexta. Protecciones.** Durante el periodo de lactancia se aplican las protecciones que establece el Reglamento Interior de Trabajo para las personas en periodo de lactancia.

**Séptima. Naturaleza.** Este acuerdo no modifica las condiciones de trabajo pactadas: regula temporalmente el ejercicio de un derecho legal.

**Notas para programación.** LACTANCIA_FIN lo calcula el sistema; falta confirmar si los 6 meses corren desde el parto o desde el regreso al trabajo. Con LACTANCIA_MODALIDAD = Reposos y UBICACION_LACTARIO vacío, el sistema alerta: el lactario del art. 66 del RIT no está configurado. El análisis de jornada toma la jornada reducida del periodo.

### 17.4 LIC-2. Notificación de licencia por comisión permanente

Evento B4. RH la envía por la Plataforma y al correo personal; la persona acusa recibo. No requiere firma.

La Empresa hace constar lo siguiente:

- **Designación.** La Persona Trabajadora fue designada para desempeñar el cargo de {{COMISION_CARGO}} en {{COMISION_ORGANO}}, con carácter permanente, según {{COMISION_DOCUMENTO}} de fecha {{COMISION_DOCUMENTO_FECHA}}, del que entregó copia y dio aviso a la Empresa con oportunidad.
- **Licencia.** Desde el {{EVENTO_FECHA_INICIO}}, la Persona Trabajadora deja de prestar sus servicios para desempeñar la comisión. Durante ella, la Empresa no paga salario. La relación de trabajo subsiste.
- **Derecho a regresar.** La Persona Trabajadora puede volver al puesto que ocupaba, conservando todos sus derechos, siempre que regrese dentro de los seis años siguientes al inicio de la comisión, es decir, a más tardar el {{COMISION_FECHA_LIMITE}}.
- **Aviso de regreso.** Para organizar su reincorporación, la Persona Trabajadora avisará su regreso por escrito con la mayor anticipación posible. La falta de aviso no afecta su derecho a regresar.
- **Comunicaciones.** Mientras dure la comisión, las comunicaciones de la Empresa se enviarán al correo personal {{TRAB_EMAIL}}. La Persona Trabajadora informará cualquier cambio de correo o domicilio.
- **Seguridad social.** Los efectos de la licencia ante el Instituto Mexicano del Seguro Social y el Infonavit se rigen por las leyes de la materia.

Acuse: la Persona Trabajadora acusó recibo por {{ACUSE_MEDIO}} el {{ACUSE_FECHAHORA}}.

**Notas para programación.** COMISION_FECHA_LIMITE = inicio + 6 años. Mientras B4 esté vigente, el módulo 4 muestra el aviso y pide doble confirmación antes de cualquier baja. Las alertas son anuales y 90 días antes del límite. Al regreso se genera SUS-3.

### 17.5 LIC-3. Convenio de licencia sin goce

Se genera en el evento B5, cuando la cadena de autorización aprueba la licencia. Lo firman la Persona Trabajadora y la persona de RH designada (FIRMANTES_EMPRESA).

**Declaraciones**

I. La Persona Trabajadora solicitó por escrito, el {{LIC3_SOLICITUD_FECHA}}, una licencia sin goce de salario[SI LIC3_CAUSA no vacía] por {{LIC3_CAUSA}}[FIN SI].

II. La Empresa accede a la solicitud de forma voluntaria. La licencia no deriva de una obligación legal ni constituye precedente para otras solicitudes.

**Cláusulas**

**Primera. Periodo.** La licencia comprende del {{EVENTO_FECHA_INICIO}} al {{EVENTO_FECHA_FIN}}. La Persona Trabajadora se reincorpora el {{LIC3_FECHA_REGRESO}}, en su horario habitual.

**Segunda. Efectos.** Durante la licencia se suspenden la obligación de la Persona Trabajadora de prestar el servicio y la de la Empresa de pagar el salario. La relación de trabajo subsiste: la licencia no es terminación ni renuncia.

**Tercera. Derechos que se conservan.** La Persona Trabajadora conserva su puesto y sus condiciones de trabajo. La licencia no interrumpe su antigüedad. El tiempo de la licencia no se cuenta como día trabajado para la participación de utilidades.

**Cuarta. Seguridad social.** Antes de firmar, la Empresa informó a la Persona Trabajadora los efectos de la licencia ante el Instituto Mexicano del Seguro Social y el Infonavit. [SI LIC3_AVISO_BAJA_IMSS = Sí] La Persona Trabajadora queda informada de que la Empresa presentará ante el IMSS el aviso que la ley prevé para las ausencias sin pago de salario, lo que suspende su cobertura durante la licencia; al regreso, la Empresa presentará el aviso de reingreso. [FIN SI]

**Quinta. Créditos y descuentos.** Durante la licencia no hay salario del cual aplicar los descuentos que la Empresa hace por nómina. La Persona Trabajadora atenderá directamente esas obligaciones con sus acreedores, y la Empresa dará los avisos que la ley le exija.

**Sexta. Herramientas y accesos.** La Empresa puede pedir la devolución temporal de las herramientas asignadas y suspender los accesos a sus sistemas durante la licencia. Se restablecen al regreso. La obligación de confidencialidad sigue vigente.

**Séptima. Regreso anticipado.** La Persona Trabajadora puede reincorporarse antes de la fecha pactada si lo avisa por escrito con al menos cinco días hábiles de anticipación, salvo que la Empresa acepte un plazo menor.

**Octava. Prórroga.** La licencia solo puede prorrogarse por escrito, firmado por ambas partes antes de su vencimiento.

**Novena. Falta de regreso.** Si la Persona Trabajadora no se presenta el {{LIC3_FECHA_REGRESO}} sin causa justificada, sus ausencias se registrarán como faltas desde ese día, con los efectos que prevean la Ley y el Reglamento Interior de Trabajo. La relación no se tiene por terminada por ese solo hecho.

**Décima. Sin renuncia de derechos.** Este convenio no implica renuncia de derechos de ninguna de las partes.

**Notas para programación.** El sistema bloquea LIC3_FECHA_REGRESO posterior a inicio + LIC3_MAX_DIAS; la prórroga genera una nueva versión. LIC3_AVISO_BAJA_IMSS lo marca el contador con RH cuando la licencia es de 8 días o más; con Sí, la cláusula cuarta lo hace constar para que la Persona Trabajadora sepa que pierde la cobertura. El plazo de cinco días hábiles de la séptima está aprobado provisionalmente (12/11/2026).

### 17.6 INC-1. Aviso de accidente de trabajo

Se genera en el evento C2 cuando el riesgo es un accidente, y de inmediato si la persona fallece. Lo firma el representante de la Empresa; la Persona Trabajadora no firma. No lleva el bloque de datos de la persona de las reglas comunes: sus datos van en el cuerpo.

**Destinatarios:** la Secretaría del Trabajo y Previsión Social, {{AUTORIDAD_INSPECCION}} y el Tribunal laboral competente.

{{PATRON_RAZON_SOCIAL}}, por conducto de {{REP_NOMBRE}}, en su carácter de {{REP_CARACTER}}, da aviso del accidente de trabajo siguiente:

| Dato | Información |
| --- | --- |
| a) Empresa y domicilio | {{PATRON_RAZON_SOCIAL}}, {{PATRON_DOMICILIO}} |
| b) Persona trabajadora, domicilio, puesto y salario | {{TRAB_NOMBRE}}, {{TRAB_DOMICILIO}}; {{PUESTO}}; salario diario de {{SALARIO_PERSONA}} |
| c) Lugar y hora del accidente, y hechos | {{RT_LUGAR}}, {{RT_FECHA_HORA}}. {{RT_HECHOS}} |
| d) Testigos y domicilios | {{RT_TESTIGOS}} |
| e) Lugar de atención médica | {{RT_ATENCION}} |

[SI RT_FALLECIMIENTO = Sí] La persona trabajadora falleció el {{RT_FALLECIMIENTO_FECHA}}. Según la información con que cuenta la Empresa, las personas que podrían tener derecho a la indemnización son: {{RT_POSIBLES_BENEFICIARIOS}}. [FIN SI]

Este aviso se presenta para cumplir la obligación legal de informar. No implica reconocimiento de responsabilidad ni calificación del riesgo, que corresponde al Instituto Mexicano del Seguro Social.

{{LUGAR_FIRMA}}, a {{FECHA_FIRMA}}. — {{REP_NOMBRE}}, {{REP_CARACTER}}.

**Notas para programación.** Plazo: 72 horas desde el accidente; alerta inmediata y crítica a las 48 horas. Con fallecimiento, el aviso se da en cuanto se conoce. RT_HECHOS debe ser sucinto y sin juicios sobre la culpa. RT_POSIBLES_BENEFICIARIOS se precarga de la designación de beneficiarios, editable, con la leyenda de que no prejuzga quién tiene derecho. AUTORIDAD_INSPECCION es solo el nombre de la autoridad; el ámbito sale de COMPETENCIA (diccionario único, decisión P2); el Tribunal laboral competente va con texto fijo, sin variable (art. 504, fr. V LFT). El sistema guarda el acuse de cada autoridad.

### 17.7 INC-2. Solicitud de transferencia de semanas prenatales

Se genera en el evento C3 solo si TRANSF_SEMANAS es mayor que 0. Firman la trabajadora y RH.

**I. Solicitud.** La Persona Trabajadora, con fecha probable de parto el {{FECHA_PROBABLE_PARTO}}, solicita de forma expresa y voluntaria transferir {{TRANSF_SEMANAS}} de las semanas de descanso previas al parto para disfrutarlas después de él. Con la transferencia, su descanso prenatal iniciaría el {{PRENATAL_INICIO}}.

**II. Autorización médica.** Se anexa la autorización escrita expedida por {{TRANSF_MEDICO_ORIGEN}} el {{TRANSF_AUTORIZACION_FECHA}}. [SI TRANSF_MEDICO_ORIGEN = Médico particular] La autorización contiene el nombre y número de cédula profesional de quien la expide, la fecha y el estado médico de la trabajadora. [FIN SI]

**III. Opinión de la Empresa.** Considerando la naturaleza del trabajo que desempeña la Persona Trabajadora:

[SI TRANSF_OPINION = Sin objeción] la Empresa no tiene objeción a la transferencia. [FIN SI]

[SI TRANSF_OPINION = Con observaciones] la Empresa expresa lo siguiente: {{TRANSF_OPINION_TEXTO}}. [FIN SI]

**IV. Previsiones.**

- Si su estado de salud lo requiere, el descanso prenatal puede iniciar antes, conforme al certificado de incapacidad que expida la institución de seguridad social.
- Las fechas de los descansos se ajustan a los certificados de incapacidad que expida la institución de seguridad social y a la fecha real del parto.
- Mientras siga laborando, la Persona Trabajadora goza de las protecciones que establece el Reglamento Interior de Trabajo para las personas embarazadas.

**Notas para programación.** TRANSF_SEMANAS acepta de 0 a 4. Con más de 0, el sistema exige el archivo de la autorización antes de generar el documento. Si el puesto está marcado como área con riesgo para embarazo, el sistema alerta para que la opinión considere la reasignación del art. 65 del RIT. La opinión de la Empresa no puede consistir en negar la transferencia si la autorización médica existe: es una opinión que el médico toma en cuenta.

### 17.8 SUS-1. Constancia de suspensión

Se genera en los eventos D1, D2 y D3. Cambia solo el párrafo de la causa y el del regreso, según SUSP_FRACCION.

La Empresa hace constar lo siguiente:

**1. Causa.**

[SI SUSP_FRACCION = III o IV] La Persona Trabajadora se encuentra a disposición de una autoridad, lo que le impide prestar sus servicios, según la constancia recibida el {{SUSP_EVIDENCIA_FECHA}}. [FIN SI]

[SI SUSP_FRACCION = V] La Persona Trabajadora debe desempeñar {{SUSP_CARGO}}, de los servicios o cargos que la Constitución prevé, según {{SUSP_EVIDENCIA}}. [FIN SI]

[SI SUSP_FRACCION = VI] La Persona Trabajadora fue designada representante ante {{SUSP_ORGANISMO}}, según {{SUSP_EVIDENCIA}}. [FIN SI]

**2. Efectos.** Desde el {{EVENTO_FECHA_INICIO}} se suspenden la obligación de la Persona Trabajadora de prestar el servicio y la de la Empresa de pagar el salario, sin responsabilidad para ninguna de las partes. La relación de trabajo subsiste y la Persona Trabajadora conserva su puesto.

[SI SUSP_FRACCION = III] Si se acredita que la Persona Trabajadora obró en defensa de la persona o de los intereses de la Empresa, ésta le pagará los salarios que haya dejado de percibir. [FIN SI]

**3. Regreso.** La Persona Trabajadora deberá regresar a su trabajo:

[SI SUSP_FRACCION = IV] al día siguiente de que termine el arresto. [FIN SI] [SI SUSP_FRACCION = III] dentro de los quince días siguientes a que obtenga su libertad. [FIN SI] [SI SUSP_FRACCION = V o VI] dentro de los quince días siguientes a que concluya el servicio, el cargo o la designación, sin que la suspensión exceda el plazo que fija la Ley. [FIN SI]

Si no regresa en el plazo sin causa justificada, sus ausencias se registrarán como faltas desde el día siguiente, con los efectos que prevean la Ley y el Reglamento Interior de Trabajo.

**4. Comunicaciones.** Mientras dure la suspensión, las comunicaciones de la Empresa se enviarán al correo personal {{TRAB_EMAIL}}.

[SI TRAB_DISPONIBLE_FIRMA = No] La Persona Trabajadora no está disponible para firmar. La constancia se envió el {{FECHA_ENVIO}} a su correo personal y se le entregará en mano a su regreso. [FIN SI]

**Notas para programación.** SUSP_REGRESO_LIMITE lo calcula el sistema al registrar el fin de la causa. En D1, el documento nunca describe los hechos ni el delito; la evidencia y este documento solo los ve el personal de RH autorizado para datos sensibles (sección 13). En D2 y D3 la suspensión puede durar hasta 6 años; las alertas siguen la regla de B4. Si el proceso de D1 es por un delito contra la Empresa o sus compañeros, el sistema alerta a consultoría sin mostrarle la evidencia, salvo que esté en `DATOS_SENSIBLES_ACCESO` (el plazo de 15 días tiene una excepción legal).

### 17.9 SUS-2. Aviso de suspensión por falta de documentos

Se genera en el evento D4, con visto bueno de consultoría. Lo firma RH; la Persona Trabajadora firma de recibido.

**1. Hechos.** El puesto de {{PUESTO}} exige, conforme a {{SUSP_DOCUMENTO_FUNDAMENTO}}, contar con {{SUSP_DOCUMENTO}}. [SI SUSP_DOCUMENTO_ESTADO = Vencido] Ese documento venció el {{SUSP_DOCUMENTO_VENCIMIENTO}}. [FIN SI] [SI SUSP_DOCUMENTO_ESTADO = No presentado] La Persona Trabajadora no lo ha presentado. [FIN SI] La Empresa conoció este hecho el {{SUSP_CONOCIMIENTO_FECHA}}. Su obtención o renovación corresponde a la Persona Trabajadora: {{SUSP_IMPUTABILIDAD}}.

**2. Suspensión.** Como sin ese documento la Persona Trabajadora no puede prestar el servicio, desde el {{EVENTO_FECHA_INICIO}} se suspenden su obligación de prestarlo y la de la Empresa de pagar el salario. La suspensión no excede de dos meses contados desde que la Empresa conoció el hecho, es decir, hasta el {{SUSP_LIMITE}}. La relación de trabajo subsiste.

**3. Requerimiento.** Se requiere a la Persona Trabajadora para que entregue a Recursos Humanos el documento vigente. Se reincorporará al día siguiente de entregarlo.

**4. Efecto de no regularizar.** Si al {{SUSP_LIMITE}} no ha entregado el documento, la Empresa podrá rescindir la relación de trabajo sin responsabilidad, por la causa que la Ley prevé para ese supuesto.

**5. Comunicaciones.** Las comunicaciones de la Empresa se enviarán al correo personal {{TRAB_EMAIL}}.

**Notas para programación.** Antes de generar el aviso, consultoría confirma dos cosas: que el documento lo exige una ley o un reglamento (no basta una política de la Empresa) y que la falta es imputable a la persona (por ejemplo, no tramitó la renovación; no lo es si la autoridad está en trámite por causa ajena). SUSP_LIMITE = SUSP_CONOCIMIENTO_FECHA + 2 meses; alertas en los días 45 y 60. Al vencer, el caso pasa a consultoría para el aviso de rescisión del módulo 4 (art. 47, fr. XIV Bis); el sistema no termina la relación. Si la persona acepta la reubicación temporal (MOD-5 del módulo 5), no se genera este aviso mientras dure; el plazo de dos meses sigue corriendo (validación 10). Si la reubicación termina sin regularizar, el aviso se genera con suspensión desde esa fecha.

### 17.10 SUS-3. Lista de reincorporación (confirmación en la Plataforma)

Se genera al terminar B4, B5 y toda suspensión D, y al terminar C2 o C3 cuando duraron más de REINCORPORACION_UMBRAL_DIAS. No se firma: la persona confirma cada punto en la Plataforma al regresar y RH lo valida. El texto es la constancia exportable o el formato de respaldo.

La Empresa y la Persona Trabajadora hacen constar lo siguiente:

- **Reincorporación.** Después de {{EVENTO_ORIGEN_NOMBRE}}, del {{EVENTO_ORIGEN_INICIO}} al {{EVENTO_ORIGEN_FIN}}, la Persona Trabajadora se reincorporó el {{REINCORPORACION_FECHA}}.
- **Puesto y condiciones.** Se reincorpora al puesto de {{PUESTO}}, con la jornada y las condiciones pactadas en su contrato y el salario vigente para su puesto.
- [SI EXAMEN_RETORNO = Sí] **Examen de retorno.** La Persona Trabajadora se presentará el {{EXAMEN_RETORNO_FECHA}} al examen médico de retorno que prevé el Reglamento Interior de Trabajo. La Empresa solo recibe el dictamen de aptitud. [FIN SI]
- [SI HERRAMIENTAS_SUSPENDIDAS = Sí] **Herramientas y accesos.** La Empresa restablece los accesos a sus sistemas y entrega las herramientas devueltas temporalmente, conforme al inventario de la carta responsiva. [FIN SI]
- [SI BENEF_CONFIRMACION_VENCIDA = Sí] **Datos y beneficiarios.** La Persona Trabajadora confirma o actualiza sus datos y su designación de beneficiarios en este acto. [FIN SI]
- [SI EVENTO_ORIGEN_TIPO = C3] **Lactancia.** Se informa a la Persona Trabajadora su derecho de lactancia. Si lo ejerce, se documenta con el acuerdo de lactancia. [FIN SI]
- [SI IMSS_REINGRESO_FECHA no vacía] **Seguridad social.** La Empresa presentó el aviso de reingreso ante el Instituto Mexicano del Seguro Social el {{IMSS_REINGRESO_FECHA}}. [FIN SI]
- [SI SUSP_VACACIONES_GENERA = Sí] **Vacaciones.** Por el tiempo de {{EVENTO_ORIGEN_NOMBRE}}, la Persona Trabajadora tiene {{VACACIONES_DIAS_GENERADOS}} días de vacaciones, que disfrutará conforme al Reglamento Interior de Trabajo. [FIN SI]

[SI SALIDA = Constancia] Confirmada por la Persona Trabajadora en la Plataforma el {{CONFIRMACION_FECHAHORA}} y validada por {{FIRMA_EMPRESA_NOMBRE}}. [FIN SI]

**Notas para programación.** La numeración se recalcula según los apartados activos. BENEF_CONFIRMACION_VENCIDA = Sí si pasaron más de 12 meses desde BENEF_CONFIRMACION_FECHA, igual que la regla anual del kit. Si la persona no se presenta en la fecha límite, no se genera SUS-3: corre la regla de faltas. En B4, B5, D2 y D3, RH decide caso por caso con SUSP_VACACIONES_GENERA si el tiempo de la suspensión genera vacaciones; con No, el apartado no se imprime.
