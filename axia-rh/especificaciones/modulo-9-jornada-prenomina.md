# AXIA RH — MÓDULO 9: ANÁLISIS DE JORNADA Y VISOR DE PRE-NÓMINA

Especificación para programación · Versión 1.1 · 21/11/2026
Fuente: decisiones del usuario del 20/11/2026 en la conversación del módulo 9; «AXIARH - Registro de decisiones» (secciones 2, 4.1, 4.4, 4.9, 4.10, 4.14, 5.0 y 5.4, actualizado al 21/11/2026); «Axia RH - Mapa del PMV» (encargos del 21/11/2026); especificaciones del RIT v1.4, permisos v1.6 a v1.9, vacaciones v1.0 a v1.3, módulo 4 v1.4 y v1.5, módulo 5 v1.0 y módulos 6 y 8 v1.0; LFT compilada por la Cámara de Diputados (última reforma DOF 14-05-2026).

## Cambios respecto de la versión 1.0 (encargos 3, 4 y 5 del mapa, 21/11/2026)

La 1.0 no se ha corrido en el software. Si ya se cargó, basta aplicar esta tabla; ante cualquier duda rige el texto completo.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 4.5; 8.1; 17; 18 | **Sin descuento del descanso proporcional** (decisión del usuario del 21/11/2026, registro 4.10 y 4.14; sustituye la decisión 5 del 20/11). La falta confirmada y el día sin goce descuentan solo el salario de su propio día. Se elimina la fórmula del art. 72 y el renglón «Descanso proporcional (art. 72)» de la salida a nómina. Caso 6: $480.00 |
| 2 | 5 (PN-18); 14.2; 15 | `BIOMETRICO_CONSENTIMIENTO` se renombra **`BIOMETRICO_JORNADA_CONSENT`** (nombre fijado por Cerebro); se quita «confirmar el nombre con el kit». Es distinta de `BIOMETRICO_FIRMA_CONSENT` |
| 3 | 6.2; 8.4 (nueva); 9; 10; 18 | **Personas con baja.** Desde que se registra la baja, la persona no se exporta en ninguna exportación posterior y todos sus conceptos variables no exportados quedan como «Revisar en el finiquito», fuera de la salida a nómina. Evita el doble pago, porque el módulo 4 precarga esos conceptos en el finiquito y no avisa a este módulo (decisión del usuario en el módulo 4). Caso 19 nuevo |

**Alcance.** Un solo motor de análisis de jornada cuya pantalla de resultados es el visor de pre-nómina. Importa el archivo del reloj checador del cliente, arma la jornada esperada de cada persona y día, compara, clasifica incidencias, permite a RH resolverlas con soporte, entrega a nómina cantidades e importes brutos estimados por concepto y conserva la evidencia. **No** timbra, **no** calcula ISR ni cuotas del IMSS y **no** captura ausencias: la fuente única de ausencias justificadas es el módulo de permisos (eventos) y el módulo de vacaciones (VAC-1). La app de registro del colaborador es fase 2.

**Partes provisionales.** Las disposiciones generales de la STPS del art. 132, fr. XXXIV LFT (vigencia 1/01/2027) no estaban publicadas al cierre de esta versión. Lo que depende de ellas se marca **[DEPENDE STPS]** (sección 16).

---

## 0. Convenciones

- Variables `{{MAYÚSCULAS_CON_GUION_BAJO}}`; condiciones `[SI …] … [FIN SI]`; las marcas nunca se imprimen.
- Términos fijos: «la Empresa» y «la Persona Trabajadora».
- Niveles: **E** empresa · **O** organigrama o puesto · **K** catálogo de jornadas · **A** alta · **V** evento (pantallas de este módulo) · **S** calculada · **B** bitácora · **X** solo consultoría (global).
- Reglas de pantalla de todo el sistema (registro 5.0): campos faltantes resaltados; tablas con botones visibles de guardar y quitar; sin candados por fecha; guardar nunca se bloquea; opciones sin valor por omisión cuando la Ley no lo fija; concordancia de número; Arial; PDF generado en el servidor.
- **Días hábiles para la aclaración (art. 13 del RIT):** los días laborables del centro de trabajo, según el turno de la persona (art. 5 del RIT), sin los días de descanso obligatorio. No se usa aquí el calendario del módulo 4.
- Ninguna cifra que cambia por reforma se fija en código ni en textos: vive en `TE_LIMITES` y en `JORNADA_MAXIMA` (tabla global con vigencia y aprobación, mecánica del módulo 4, 5.3).
- Montos en MXN con dos decimales; horas en minutos enteros internamente y en horas con dos decimales en pantalla.

---

## 1. Arquitectura

### 1.1 Modos (`PRENOMINA_MODO`, E)

| Modo | Fuentes | Qué alimenta |
| --- | --- | --- |
| **Conectado** | Versión de condiciones de la persona (módulo 5), incluida la reasignación temporal MOD-5; catálogo de jornadas; rol (opcional); eventos del módulo de permisos; VAC-1; órdenes de tiempo extra (`TE_ORDEN`); calendario de días de descanso obligatorio; `SALARIO_PERSONA`; créditos y descuentos del alta | Alertas de faltas y de patrón del módulo de permisos; `AGUINALDO_COMPUTA` (faltas confirmadas); días computables de PTU; tiempo extra pendiente del módulo 4; claves para el cotejo del módulo 6 |
| **Solo archivo** | Horarios capturados o importados para ese corte | Nada. Lo que RH clasifica queda en el corte |

- Una empresa opera en un solo modo; no se mezclan en el mismo periodo. El cambio de modo aplica desde el periodo siguiente.
- El modo «Solo archivo» se ofrece **solo a clientes de Axia RH** (decisión del 20/11/2026); no es un servicio para terceros. Uso típico: empresa cuyo organigrama, altas o eventos aún no están cargados.
- En «Solo archivo» toda ausencia queda «por confirmar»; nunca se califica como falta injustificada. Los resultados llevan la leyenda «Diagnóstico del archivo del reloj checador; no sustituye el registro de jornada de la Empresa».

### 1.2 Unidades

- **Periodo de pago:** el de la periodicidad del puesto en la versión de la persona (semanal o quincenal). El visor trabaja por empresa y periodo.
- **Semana de cómputo:** inicia en `SEMANA_INICIO` (E, sin valor por omisión). Los límites semanales (jornada máxima, tiempo extra, descanso) se calculan por semana de cómputo, aunque el periodo de pago sea quincenal.
- **Día de jornada:** el día del turno, no el del calendario. Un turno nocturno que cruza la medianoche pertenece al día en que inicia.

---

## 2. Importación

### 2.1 Formatos aceptados

| Formato | Contenido mínimo | Opcional |
| --- | --- | --- |
| Un renglón por marcaje (CSV o XLSX) | `CHECADOR_ID`, fecha, hora | Tipo (entrada, salida, inicio de reposo, fin de reposo), dispositivo, modo de verificación (biométrico, PIN, tarjeta, manual, remoto), CURP, `NUM_EMPLEADO` |
| Un renglón por día (CSV o XLSX) | `CHECADOR_ID`, fecha, entrada, salida | Inicio y fin de reposo, más pares de entrada y salida, dispositivo, modo de verificación, CURP, `NUM_EMPLEADO` |

- Mapeo de columnas guardado por empresa y dispositivo (`CHECADOR_MAPEO`). Sin mapeo no se importa.
- Se aceptan varios archivos por periodo (varios dispositivos o centros).
- Sin integración directa ni API con el checador en el PMV.
- Las columnas de ubicación, si existen, se descartan al importar en los días en casa (cláusula 6.5b del contrato) y no se guardan.

### 2.2 Identificación de la persona

1. `CHECADOR_ID` (A) es obligatorio para ligar marcas.
2. Si el renglón trae CURP o `NUM_EMPLEADO`, el sistema verifica que coincidan con la persona del `CHECADOR_ID`; si no coinciden, el renglón va a PN-06.
3. Un `CHECADOR_ID` sin persona, o una marca anterior al alta o posterior a la baja, va a PN-06 y se excluye hasta conciliar.

### 2.3 Integridad

- El archivo original se conserva sin cambios, con su hash SHA-256 (`PRENOMINA_ARCHIVO_HASH`), usuario, fecha y hora de carga. El mismo hash en el mismo periodo se rechaza como duplicado.
- Las marcas importadas nunca se sobrescriben. Las correcciones van en una capa aparte (sección 7.3).
- **Errores de archivo** (formato, mapeo, fechas fuera del periodo en su totalidad): bloquean la importación de ese archivo. **Errores de renglón:** se excluyen, se listan en un reporte descargable y no detienen a las demás personas.

### 2.4 Depuración y asignación

1. **Duplicados:** marcas de la misma persona separadas por menos de `CHECADOR_DUPLICADO_MIN` minutos (E, por omisión 2) se tratan como una; se conserva la primera y las demás quedan en la bitácora como «duplicada».
2. **Asignación al turno:** cada marca se asigna al turno cuya ventana la contiene: de la entrada pactada menos `CHECADOR_VENTANA_HORAS` (E, por omisión 4) a la salida pactada más `CHECADOR_VENTANA_HORAS`. Una marca fuera de toda ventana en un día sin turno se asigna al día calendario y se analiza como trabajo en día de descanso o festivo.
3. **Marcas sin tipo:** dentro del turno, en orden cronológico, se alternan entrada y salida; si `CHECADOR_REGISTRA_COMIDA` = Sí, los pares intermedios son reposos. Un número impar de marcas genera PN-02.
4. **Traslados REPSE (art. 9 del RIT):** con `REPSE_EMPRESA` = Sí y varias llegadas y salidas en el día, el tiempo entre una salida y la siguiente llegada es jornada, salvo que el par esté marcado como reposo.
5. **Zona horaria:** las horas se interpretan con `CENTRO_ZONA_HORARIA` del centro de la persona.

### 2.5 Versiones

- Volver a importar un periodo genera una versión nueva (`PRENOMINA_VERSION`); la anterior queda en el historial.
- Antes de «Exportado», la versión nueva sustituye el cálculo del periodo.
- Después de «Exportado», las diferencias entre versiones se registran como ajustes del periodo siguiente (sección 8.3).

### 2.6 Frecuencia

- Al menos una importación por periodo de pago; se recomienda semanal.
- Alerta a RH «Periodo sin importación» si faltan 2 días hábiles para el día de pago y el periodo no tiene archivo.
- Motivo (no se imprime): el plazo de 30 días del art. 83 del RIT corre desde que la jefatura conoce la falta.

---

## 3. Jornada esperada por persona y día

### 3.1 Construcción (modo Conectado)

En este orden; cada capa sustituye a la anterior para el día:

1. **Turno de la versión de condiciones** de la persona (módulo 5, `JORNADA_ID`) vigente en la fecha.
2. **Reasignación temporal MOD-5** con horario distinto, en sus fechas.
3. **Rol** (archivo opcional, `ROL_PERIODO`): persona, fecha y turno o «descanso». Prevalece sobre el turno base para puestos con varios turnos o descanso rotativo.
4. **Descanso rotativo sin rol:** la persona labora `DIAS_TRABAJO_SEMANA` días por semana de cómputo; los días laborados en exceso, empezando por el último de la semana, se tratan como descanso laborado (PN-13).
5. **Días de descanso obligatorio** (art. 74 LFT, calendario de días inhábiles del módulo 4, incluida la jornada electoral).
6. **Eventos del módulo de permisos** (todas las familias) y **VAC-1**: el día pasa a «ausencia justificada» del tipo correspondiente, con o sin goce. La incapacidad prevalece.
7. **Lactancia (B1):** con `LACTANCIA_MODALIDAD` = Reducción, la jornada esperada baja una hora en el horario de `LACTANCIA_HORARIO`; con Reposos, hasta 60 minutos de reposo registrados al día no se descuentan del tiempo laborado.
8. **Suspensión disciplinaria** (FD-3 del RIT, fechas de suspensión) y **fin de temporada** (módulo 4): ausencia esperada sin goce; no es falta.
9. **Días en casa** (`TELE_DIAS` de la versión): el día se marca «en casa»; se espera registro de origen remoto, sin ubicación.
10. **Antes del alta y después de la baja:** sin jornada esperada.

### 3.2 Modo Solo archivo

RH captura o importa los horarios del corte (persona, días, entrada, salida, reposo). No se leen eventos ni versiones.

### 3.3 Validaciones del catálogo que usa este módulo (encargo al catálogo de jornadas)

| Validación | Efecto |
| --- | --- |
| Horas diarias del turno ≤ máximo diario del art. 61 según su tipo (diurna, nocturna, mixta) | Bloqueo. Los topes diarios operan como máximos aunque la jornada se distribuya de común acuerdo (art. 58) |
| Horas semanales del turno ≤ `JORNADA_MAXIMA` del año | Bloqueo. Lectura literal: el mismo tope semanal para todo tipo de jornada, más el tope diario de cada tipo |
| Semana que incluye el 1 de enero | Tope prorrateado por días de cada año |

`JORNADA_MAXIMA` (X): 2026 48 · 2027 46 · 2028 44 · 2029 42 · 2030 40 horas, cada cambio el 1 de enero (transitorio segundo, DOF 01-05-2026).

---

## 4. Reglas de cálculo

### 4.1 Tiempo laborado del día

1. **Inicio:** la marca de entrada, aunque sea anterior a la hora pactada (art. 9 del RIT). **Fin:** la marca de salida.
2. **Reposos:**
   - Con `CHECADOR_REGISTRA_COMIDA` = Sí: se descuenta el reposo registrado. Si es menor que 30 minutos en jornada continua, PN-15 (art. 63 LFT); si excede el pactado, PN-15 (conducta 4).
   - Con `CHECADOR_REGISTRA_COMIDA` = No: se presume el reposo pactado en el turno y se descuenta.
   - El sistema no evalúa en automático si la persona podía salir durante el reposo (decisión 29 del paquete).
3. Minuto a minuto; sin redondeo a la baja.

### 4.2 Tiempo extra

- **Cálculo diario (método neto):** tiempo extra del día = minutos laborados − minutos de la jornada esperada del día, si es positivo. Un retardo compensado con salida posterior no genera tiempo extra.
- En día de descanso o de descanso obligatorio laborado, el día se paga por PN-13 o PN-14; solo los minutos que excedan la jornada diaria pactada cuentan como tiempo extra.
- **Orden previa:** cada bloque de tiempo extra se cruza con `TE_ORDEN`.
  - Orden capturada antes del inicio del tiempo extra, dentro de las horas autorizadas: «con orden» (PN-08).
  - Sin orden, orden capturada después o minutos que excedan las horas autorizadas: «sin orden previa» (PN-09).
  - Orden de tipo «Siniestro» (art. 65 LFT; art. 19 del RIT): se paga sencillo (art. 67) y no cuenta para los límites.

### 4.3 Clasificación doble y triple (`TE_LIMITES`, X)

| Año | Tope semanal con 100 % más | Máximo diario | Máximo de días | Excedente semanal con 200 % más | Ordinaria + extra por día |
| --- | --- | --- | --- | --- | --- |
| 2026 | 9 | 4 | 4 | 4 | 12 |
| 2027 | 9 | 4 | 4 | 4 | 12 |
| 2028 | 10 | 4 | 4 | 4 | 12 |
| 2029 | 11 | 4 | 4 | 4 | 12 |
| 2030 | 12 | 4 | 4 | 4 | 12 |

Fundamento: arts. 66 y 68 LFT y transitorio cuarto (DOF 01-05-2026). Que el máximo diario y el de días rijan junto con el tope gradual del transitorio es una lectura propia; por eso vive en la tabla.

Asignación por semana de cómputo, en orden cronológico de los días y, dentro del día, de los minutos:

1. Si la persona es menor de 18 años (edad de la CURP): todo el tiempo extra se paga con 200 % más desde el primer minuto (art. 178 LFT) y genera PN-11.
2. Si no: los minutos del día van a «doble» mientras (a) no se rebasen las horas del máximo diario en ese día, (b) el día sea uno de los primeros días con tiempo extra hasta el máximo de días y (c) quede tope semanal con 100 % más.
3. Lo que no cabe en «doble» va a «triple» hasta el excedente semanal con 200 % más.
4. Lo que rebase el excedente semanal, o los minutos de un día cuya suma de ordinaria y extra pase de 12 horas, se paga también como «triple» y genera PN-10 (alerta crítica). Nunca se deja de pagar lo laborado.
5. Semana que incluye el 1 de enero: se usa el menor de los topes semanales de los dos años.
6. Con orden o sin orden, la clasificación de pago es la misma.

### 4.4 Importes brutos estimados

- `TASA_HORA` = `SALARIO_PERSONA` ÷ horas diarias pactadas de la versión (horas semanales del turno ÷ días laborables del turno).
- Doble = `TASA_HORA` × 2 × horas · Triple = `TASA_HORA` × 3 × horas · Siniestro = `TASA_HORA` × horas.
- Prima dominical = `SALARIO_PERSONA` × `PRIMA_DOMINICAL_PCT` ÷ 100 por domingo laborado (art. 71).
- Descanso laborado (art. 73) y festivo laborado (art. 75) = `SALARIO_PERSONA` × 2, adicional al salario del día.
- Menores de 18 en domingo o día de descanso obligatorio: salario conforme a los arts. 73 y 75 (art. 178), además de la prima dominical en domingo (interpretación; ver sección 17).
- Las tasas (100 %, 200 %, mínimo de la prima dominical) viven en `TE_LIMITES` y en la tabla de parámetros; el código no las fija.
- No se calculan ISR, exenciones ni cuotas: los define nómina.

### 4.5 Faltas y días sin goce

- Falta confirmada (PN-01 confirmada) o día sin goce del módulo de permisos: se descuenta solo `SALARIO_PERSONA` de ese día.
- **Nunca se descuenta la parte proporcional del día de descanso** (decisión del usuario del 21/11/2026). Es más favorable que el art. 72 LFT; no genera riesgo legal.
- No se descuentan retardos ni salidas anticipadas (PN-03, PN-04).

---

## 5. Catálogo de incidencias

| Clave | Incidencia | Regla | Efecto en nómina | Conducta del catálogo del RIT | Bloqueo |
| --- | --- | --- | --- | --- | --- |
| PN-01 | Ausencia sin evento | Día laborable esperado, sin marcas, sin evento ni VAC-1, sin PN-07 | «Falta por confirmar»: sin descuento hasta que RH la confirme | 23, 44 (vía módulo de permisos) | No |
| PN-02 | Registro incompleto | Número impar de marcas o falta entrada o salida | Ninguno hasta que RH corrija | 3 | Detiene los conceptos variables de la persona en el periodo |
| PN-03 | Retardo | Entrada después de la hora pactada + `TOLERANCIA_MIN` | Ninguno | 1; cuenta para la 22 (`RETARDOS_FALTA_GRAVE` en ventana móvil de 30 días) | No |
| PN-04 | Salida anticipada | Salida antes de la hora pactada sin permiso del módulo de permisos | Ninguno automático | 24 | No |
| PN-05 | Trabajo durante vacaciones, incapacidad, suspensión o licencia | Marcas en día con VAC-1 o evento B (salvo B1), C o D | Crítica; RH concilia con el módulo de origen | — | Detiene los conceptos variables |
| PN-06 | Marcaje sin persona, antes del alta o después de la baja | Sección 2.2 | Excluido hasta conciliar | — | Excluye las marcas |
| PN-07 | Posible falla del checador | En un centro y día, el porcentaje de personas esperadas sin marcas ≥ `FALLA_CHECADOR_PCT` | Suspende PN-01 ese día en ese centro; RH confirma con el medio alterno o el registro manual (art. 13 del RIT) | — | No |
| PN-08 | Tiempo extra con orden | 4.2 y 4.3 | Doble y triple según 4.3 | — | No |
| PN-09 | Tiempo extra sin orden previa | 4.2 | «Por validar»: la jefatura confirma o RH corrige el registro con soporte (7.3). Lo no corregido se paga como PN-08 | 5 (a quien omitió la orden) | No; si llega a «Validado» sin resolver, se paga |
| PN-10 | Rebasa límites legales | 4.3, paso 4; o jornada ordinaria semanal > `JORNADA_MAXIMA` | Se paga lo laborado; alerta crítica a RH y consultoría | — | No |
| PN-11 | Persona protegida | Menor de 18 con tiempo extra, domingo o día de descanso obligatorio (art. 178); menor de 16 con más de 6 h diarias o periodos de más de 3 h (art. 177); embarazo o lactancia (B1) con tiempo extra (art. 166), solo si el embarazo consta en el sistema | Crítica; menores: 4.3, paso 1 | — | No |
| PN-12 | Domingo laborado | Marcas en domingo | Prima dominical | — | No |
| PN-13 | Descanso laborado | Marcas en día de descanso del turno o del rol, o día en exceso del descanso rotativo | Salario doble adicional | — | No |
| PN-14 | Festivo laborado | Marcas en día de descanso obligatorio | Salario doble adicional | — | No |
| PN-15 | Comida o reposo irregular | Solo con `CHECADOR_REGISTRA_COMIDA` = Sí: reposo < 30 min en jornada continua (art. 63) o mayor que el pactado | Ninguno | 4 (si excede) | No |
| PN-16 | Día en casa sin registro | Día en casa esperado sin marcas de origen remoto | Ninguno; alerta «registro faltante» a RH. No es falta por confirmar | — | No |
| PN-17 | Más de seis días seguidos de trabajo | Cómputo continuo entre semanas (art. 69) | Ninguno; alerta | — | No |
| PN-18 | Verificación biométrica sin consentimiento | Modo de verificación biométrico para persona con `BIOMETRICO_JORNADA_CONSENT` = No o revocado | Ninguno; alerta de privacidad a RH | — | No |

- **Ninguna incidencia impone sanción.** Las que tienen conducta generan un «expediente sugerido» con la conducta precargada; RH decide si abre FD-4 o FD-1 por la vía del RIT. La fecha en que la alerta se mostró a la jefatura precarga `EXP_FECHA_CONOCIMIENTO_JEFATURA`.
- Los bloqueos **nunca** detienen el salario ordinario: la persona se exporta con los días pagados según la jornada esperada y los conceptos variables bloqueados quedan como ajuste del periodo siguiente cuando se resuelven.

---

## 6. Flujo y estados

### 6.1 Flujo

Importar → depurar y asignar → cruzar con jornada esperada, eventos, órdenes y festivos → clasificar → revisión de RH → validar → exportar → cerrar.

### 6.2 Estados del periodo (`PRENOMINA_ESTADO`)

| Estado | Cómo se llega | Qué permite |
| --- | --- | --- |
| Importado | Al menos un archivo cargado | Ver resultados; corregir |
| En revisión | RH abre la bandeja de incidencias | Resolver incidencias, confirmar faltas, validar tiempo extra sin orden |
| Validado | RH valida (`PRENOMINA_VALIDACION`: usuario, fecha y hora) | Exportar. Un cambio posterior regresa a En revisión |
| Exportado | Se genera el archivo para nómina (sin las personas con baja registrada, 8.4) | Envía el resumen a cada persona (7.1); abre el plazo de aclaración |
| Cerrado | Vence `DIAS_ACLARACION_REGISTRO` y no quedan aclaraciones abiertas | El periodo queda «conforme para nómina» (art. 13 del RIT). Cambios posteriores: solo ajustes del periodo siguiente |

La validación de RH no espera al cierre: la nómina se paga con lo registrado y las aclaraciones resueltas entran como ajustes del periodo siguiente (art. 17 del RIT: el tiempo extra se paga en la nómina del periodo en que se laboró).

### 6.3 Faltas por confirmar

- RH confirma o descarta cada PN-01 antes de «Validado»; puede descartarla con soporte (falla del checador, evento registrado después).
- Lo no resuelto al validar queda «por confirmar» y no descuenta. Después de «Cerrado», solo puede confirmarse como ajuste del periodo siguiente, con soporte.
- Si después llega un evento justificado por ese día, la falta se borra (validación 1 del módulo de permisos) y el descuento se revierte en el periodo siguiente.

---

## 7. Aclaraciones y correcciones

### 7.1 Consulta de la Persona Trabajadora (portal)

- Pantalla «Mis registros» en el portal de la Plataforma, de solo lectura: días del periodo, marcas, tiempo laborado, tiempo extra, incidencias que le afectan y estado del periodo. No muestra conductas ni expedientes sugeridos.
- Al pasar a «Exportado», el sistema envía al correo personal (`TRAB_EMAIL`) el resumen del periodo, con la leyenda: «Puede consultar sus registros y solicitar su aclaración por la Plataforma dentro de los {{DIAS_ACLARACION_REGISTRO}} días hábiles siguientes al cierre del periodo de pago. Sin aclaración en ese plazo, el registro se tiene por conforme para el cálculo de la nómina, sin perjuicio de sus derechos.» El envío queda en la bitácora.

### 7.2 Aclaraciones (art. 13 del RIT)

- La persona solicita por la Plataforma dentro de `DIAS_ACLARACION_REGISTRO` días hábiles (sección 0) desde el cierre del periodo de pago, señalando día y motivo; puede adjuntar soporte.
- RH responde dentro de `DIAS_RESPUESTA_NOMINA` días hábiles: «Procede» (genera corrección y ajuste) o «No procede» (con motivo). La respuesta se envía al correo personal.
- Sin aclaración en plazo, el registro de la persona queda «Conforme».

### 7.3 Correcciones

- Solo RH. Obligatorios: motivo, soporte (archivo) y tipo (olvido de marca, falla del checador, registro manual firmado del art. 13.3 del RIT, permanencia sin labor acreditada, otro). Se guardan usuario, fecha y hora, valor anterior y valor nuevo.
- Cada corrección se avisa a la persona por la Plataforma y al correo personal.
- La marca original nunca se borra.
- Una corrección que reduce tiempo ya pagado no se descuenta en automático: sigue la vía de pago en exceso del art. 28 del RIT (notificación y plan de recuperación con reconocimiento).

---

## 8. Salida a nómina

### 8.1 Archivo de exportación

Una fila por persona y periodo (CSV o XLSX), con `CONCEPTO_CLAVE_NOMINA` por concepto (clave interna del sistema de nómina del cliente y su clave SAT de `PAGO_CLAVES_SAT`, para que el módulo 6 coteje el CFDI).

| Concepto | Cantidad | Importe bruto estimado | Fuente |
| --- | --- | --- | --- |
| Días pagados | Días | — | Jornada esperada y eventos |
| Faltas confirmadas | Días | Descuento del salario de cada día (4.5) | PN-01 confirmada |
| Días sin goce | Días | Descuento del salario de cada día (4.5) | Módulo de permisos |
| Incapacidades y días de espera pagados | Días | Solo días de espera con `PAGO_DIAS_ESPERA` = Sí | Módulo de permisos |
| Vacaciones y prima vacacional | Días | Del módulo de vacaciones | VAC-1 |
| Horas extra con 100 % más | Horas | 4.4 | PN-08, PN-09 |
| Horas extra con 200 % más | Horas | 4.4 | PN-08, PN-09, PN-10, PN-11 |
| Horas por siniestro | Horas | 4.4 | `TE_ORDEN` tipo Siniestro |
| Prima dominical | Domingos | 4.4 | PN-12 |
| Descansos laborados | Días | 4.4 | PN-13 |
| Festivos laborados | Días | 4.4 | PN-14 |
| Apoyo de gastos de días en casa | Periodo | `HIBRIDO_APOYO_MONTO` o reembolso | Versión de la persona |
| Infonavit esperado | — | Según `INFONAVIT_DESCUENTO_TIPO` y `_VALOR`; «Descuento pendiente de capturar» si falta | Alta |
| Fonacot esperado | — | `FONACOT_DESCUENTO_MONTO` proporcional al periodo; aviso si rebasa el 20 % del salario | Alta (la cédula del módulo 8 es la evidencia) |
| Pensión alimenticia | — | Según `PENSION_PORCENTAJE` | Alta |
| Descuentos de los arts. 27 y 46 del RIT | — | Importe del acuerdo de descuento, con estado de evidencia (FD-5 o FD-3); sin evidencia, alerta, no bloqueo | RIT |
| Ajustes de periodos anteriores | — | Diferencias por concepto, con folio de origen | 8.3 |

- Aviso, sin bloqueo, si la suma de descuentos por deudas rebasa los límites del art. 110 LFT (tabla del sistema).
- Los importes son estimados y brutos; nómina determina los definitivos.

### 8.2 Validación previa a la exportación

- Bloqueo de la exportación del periodo: archivo con PN-06 sin conciliar que afecte a una persona activa sin otra marca (solo esa persona se exporta sin conceptos variables), o periodo sin `CONCEPTO_CLAVE_NOMINA` para algún concepto con importe.
- Nunca se bloquea por PN-02, PN-05 o PN-09: rige la regla de 5 (salario ordinario siempre).

### 8.3 Ajustes

Aclaraciones procedentes, faltas descartadas o confirmadas después, incapacidades que llegan tarde, reversiones del art. 31 del RIT (evidencia de permisos) y diferencias de una importación posterior a «Exportado» se registran como ajustes con folio de origen y se exportan en el periodo siguiente, salvo la regla de 8.4.

### 8.4 Personas con baja

1. Al registrarse la baja en el módulo 4 (`BAJA_FECHA`), la persona queda fuera de toda exportación a nómina que se genere después, incluida la del periodo que contiene `BAJA_FECHA` si aún no se había exportado. Las exportaciones ya generadas no cambian.
2. Todos sus conceptos variables no exportados (validados y no exportados, por validar, bloqueados y ajustes pendientes) pasan al estado **«Revisar en el finiquito»**, con su periodo, folio, horas e importe bruto estimado. No entran a la salida a nómina.
3. Lo que cambie o aparezca después del registro de la baja (aclaración procedente, corrección, falta descartada, incapacidad que llega tarde) también queda «Revisar en el finiquito» y genera alerta a RH y consultoría: «Concepto posterior a la baja; revise si debe incluirse en el finiquito o pagarse por separado».
4. Si la baja se cancela en el módulo 4, los conceptos regresan a su estado anterior y la persona vuelve a exportarse.
5. Motivo (no se imprime): el módulo 4 precarga como «Sugerido» los conceptos pendientes del módulo 9 a `BAJA_FECHA` y, por decisión del usuario, no informa a este módulo cuáles pagó. Con esta regla, este módulo nunca los manda a nómina; el finiquito es la única vía de pago. Lo que el módulo 4 no haya precargado (por ejemplo, PN-09 por validar) queda visible aquí con su etiqueta para que RH lo revise.

---

## 9. Alertas

| Alerta | Momento | Destinatarios |
| --- | --- | --- |
| Periodo sin importación | 2 días hábiles antes del día de pago | RH |
| Incidencias críticas (PN-05, PN-10, PN-11) | Al clasificar | RH; PN-10 y PN-11 también consultoría |
| Tiempo extra sin orden (PN-09) | Al clasificar | Jefatura y RH |
| Faltas por confirmar sin resolver | Al intentar validar | RH |
| Expediente sugerido (conductas 1, 3, 4, 5, 22, 24) | Al clasificar | Jefatura y RH |
| Aclaración recibida | Al recibirla | RH; vencimiento de respuesta a `DIAS_RESPUESTA_NOMINA` |
| Posible falla del checador (PN-07) | Al clasificar | RH |
| Registro faltante en día en casa (PN-16) | Al clasificar | RH |
| Más de seis días seguidos (PN-17) | Al clasificar | RH |
| Privacidad (PN-18) | Al importar | RH |
| Turno o jornada sobre el máximo del año siguiente | `DIAS_AVISO_AJUSTE_HORARIO` antes del 1 de enero | RH (lo genera el RIT, 2.6) |
| Concepto posterior a la baja | Al aparecer o cambiar un concepto de una persona con baja registrada (8.4) | RH y consultoría |

---

## 10. Efectos en otros módulos

| Módulo | Qué recibe de este módulo | Qué le da a este módulo |
| --- | --- | --- |
| Permisos y licencias | Ausencias sin evento: «por confirmar» (alertas preventivas y patrón, etiquetadas) y «confirmadas» (alerta de cuarta falta, art. 47, fr. X) | Eventos, LACTANCIA_MODALIDAD, días sin goce |
| Vacaciones y aguinaldo | Faltas confirmadas para `AGUINALDO_COMPUTA` | VAC-1, prima vacacional |
| PTU | Faltas confirmadas y días laborados por persona | — |
| Módulo 4 | Tiempo extra pendiente a `BAJA_FECHA` (validado no exportado y ajustes pendientes), con horas, tipo e importe; precarga «Otros devengados» con tipo Tiempo extra, Prima dominical, Descanso laborado y Festivo laborado (cambio 18 de su v1.5) | `BAJA_FECHA` y su registro, que excluye a la persona de la exportación y deja sus conceptos como «Revisar en el finiquito» (8.4); calendario de días inhábiles. El módulo 4 no informa qué conceptos pagó |
| Módulo 5 | — | Versión de condiciones, MOD-5, `SALARIO_PERSONA` |
| Módulo 6 | Claves SAT por concepto para el cotejo | `PAGO_CLAVES_SAT` |
| Módulo 8 | — | Cédula como evidencia del Fonacot esperado |
| RIT | Expedientes sugeridos; alerta de conductas | `TOLERANCIA_MIN`, `RETARDOS_FALTA_GRAVE`, `DIAS_ACLARACION_REGISTRO`, `DIAS_RESPUESTA_NOMINA`, catálogo de conductas |

En modo «Solo archivo» no hay efectos en otros módulos.

---

## 11. Evidencia y conservación

- **Paquete probatorio** exportable por persona y periodo: archivo original con su hash, marcas asignadas, jornada esperada, correcciones con soporte, órdenes de tiempo extra, aclaraciones y respuestas, resumen enviado con su constancia de envío, y archivo exportado a nómina.
- **Entrega a la autoridad (art. 132, fr. XXXIV):** exportación por centro y rango de fechas con inicio y fin de la jornada de cada persona. **[DEPENDE STPS]** formato y campos.
- **Conservación:** durante la relación de trabajo y `REGISTRO_CONSERVACION_ANIOS` años después de su terminación (E, mínimo 1, por omisión 1; arts. 804, fr. III, y 805 LFT). Sin borrado automático: alerta de depuración.

---

## 12. Pantallas

1. **Importación:** carga de archivos, mapeo por dispositivo, reporte de errores, versiones e historial con hash.
2. **Visor del periodo:** tabla persona × día con semáforo (sin incidencias, informativa, por resolver, crítica), filtros por centro, área, jefatura e incidencia; totales por concepto.
3. **Bandeja de incidencias:** por tipo; acciones: confirmar o descartar falta, validar o corregir tiempo extra sin orden, corregir registro con soporte, abrir expediente sugerido, conciliar PN-06.
4. **Ficha persona-periodo:** jornada esperada contra real día por día, marcas originales y corregidas, cálculo de tiempo extra con su clasificación, conceptos e importes.
5. **Órdenes de tiempo extra (jefatura):** captura previa con horas autorizadas, fecha y motivo; tipo Extraordinaria o Siniestro.
6. **Aclaraciones:** bandeja de RH con plazos.
7. **Validación y exportación.**
8. **Configuración:** parámetros de la sección 14 (empresa) y consulta de `TE_LIMITES` y `JORNADA_MAXIMA` (solo consultoría edita).
9. **Portal de la Persona Trabajadora:** «Mis registros» y aclaraciones (7.1, 7.2).

---

## 13. Parámetros legales

| Tabla | Contenido | Fundamento |
| --- | --- | --- |
| `JORNADA_MAXIMA` (X) | Máximo semanal por año: 48, 46, 44, 42, 40 (2026 a 2030); máximos diarios por tipo: 8, 7 y 7.5 | Arts. 59 y 61 LFT; transitorio segundo |
| `TE_LIMITES` (X) | Sección 4.3; tasas 100 % y 200 %; rama de menores | Arts. 66, 68 y 178 LFT; transitorio cuarto |
| Prima dominical mínima | 25 % | Art. 71 LFT |

Mecánica de vigencia, aprobación y monitor: módulo 4, 5.3 (tabla única de parámetros de Cerebro).

---

## 14. Diccionario de variables

### 14.1 Reutilizadas

`SALARIO_PERSONA`, versión de condiciones y `JORNADA_ID` (módulo 5); catálogo de jornadas (`TURNO_*`, `DESCANSO_SEMANAL`, `DIAS_TRABAJO_SEMANA`, `JORNADA_TIPO`); `TELE_DIAS`, `HIBRIDO_APOYO_MODO`, `HIBRIDO_APOYO_MONTO`; `REPSE_EMPRESA`; eventos del módulo de permisos, `LACTANCIA_MODALIDAD`, `LACTANCIA_HORARIO`, `PAGO_DIAS_ESPERA`; VAC-1; `TOLERANCIA_MIN`, `RETARDOS_FALTA_GRAVE`, `DIAS_ACLARACION_REGISTRO`, `DIAS_RESPUESTA_NOMINA`, `DIAS_AVISO_AJUSTE_HORARIO`, `EXP_FECHA_CONOCIMIENTO_JEFATURA` (RIT); `PERSONA_JEFATURA`; `INFONAVIT_CREDITO`, `INFONAVIT_DESCUENTO_TIPO`, `INFONAVIT_DESCUENTO_VALOR`, `FONACOT_CREDITO`, `FONACOT_DESCUENTO_MONTO`, `PENSION_ALIMENTICIA`, `PENSION_PORCENTAJE` (alta); `PAGO_CLAVES_SAT` (módulo 6); `BAJA_FECHA` y calendario de días inhábiles (módulo 4); `TRAB_EMAIL`, CURP.

### 14.2 Variables del módulo

| Variable | Nivel | Tipo | Validación u omisión | Activa |
| --- | --- | --- | --- | --- |
| PRENOMINA_MODO | E | Conectado · Solo archivo | Sin valor por omisión; uno por empresa; solo clientes de Axia RH | 1.1 |
| CHECADOR_ID | A | Texto (uno por dispositivo si difiere) | Obligatorio para importar; único por empresa | 2.2 |
| NUM_EMPLEADO | A | Texto | Opcional; único por empresa (si no existe ya en el diccionario) | 2.2 |
| CHECADOR_MAPEO | E | Plantilla por dispositivo | Obligatoria para importar | 2.1 |
| CHECADOR_DUPLICADO_MIN | E | Minutos | 2 | 2.4 |
| CHECADOR_VENTANA_HORAS | E | Horas | 4 | 2.4 |
| CHECADOR_REGISTRA_COMIDA | E (o por centro) | Sí/No | Sin valor por omisión | 4.1; PN-15 |
| FALLA_CHECADOR_PCT | E | Porcentaje | 50 | PN-07 |
| SEMANA_INICIO | E | Día de la semana | Sin valor por omisión | 1.2; 4.3 |
| PRIMA_DOMINICAL_PCT | E | Porcentaje | 25; ≥ 25 | 4.4; PN-12 |
| CONCEPTO_CLAVE_NOMINA | E | Tabla: concepto, clave interna, clave SAT | Clave SAT de PAGO_CLAVES_SAT; obligatoria por concepto con importe | 8.1 |
| REGISTRO_CONSERVACION_ANIOS | E | Entero | ≥ 1; 1 | 11 |
| CENTRO_ZONA_HORARIA | Catálogo de centros | Lista | Obligatoria | 2.4 |
| BIOMETRICO_JORNADA_CONSENT | A (la otorga la persona en la casilla de biométricos del apartado 10 del aviso) | Sí / No, con fecha | Con No o revocado opera SISTEMA_REGISTRO_ALTERNO; distinta de BIOMETRICO_FIRMA_CONSENT | PN-18 |
| JORNADA_MAXIMA | X | Tabla con vigencia | Solo aprobados | 3.3; PN-10 |
| TE_LIMITES | X | Tabla con vigencia | Solo aprobados | 4.3 |
| ROL_PERIODO | V | Archivo: persona, fecha, turno o descanso | Opcional | 3.1 |
| TE_ORDEN | V | Persona, fecha, horas autorizadas, tipo (Extraordinaria · Siniestro), motivo, autorizador, fecha y hora de captura | Captura posterior al inicio = sin orden previa | 4.2 |
| PRENOMINA_ESTADO | S | Sección 6.2 | — | Flujo |
| PRENOMINA_VERSION | S | Entero | — | 2.5 |
| PRENOMINA_ARCHIVO_HASH | S | SHA-256 | Único por periodo | 2.3; 11 |
| PRENOMINA_VALIDACION | S | Usuario, fecha y hora | Se revierte con cambios | 6.2 |
| PN_RESOLUCION | V | Por incidencia: acción, usuario, fecha, soporte | Soporte obligatorio en correcciones | 5; 7.3 |
| TASA_HORA | S | Moneda | 4.4 | Importes |

### 14.3 No se usan

`PUEDE_SALIR` (eliminada por la decisión 29 del paquete). `SALARIO_DIARIO` como base: la sustituye `SALARIO_PERSONA`.

---

## 15. Dependencias y encargos

| Pieza | Qué se necesita |
| --- | --- |
| Cerebro | Dar de alta las variables de empresa, alta y catálogo de centros de 14.2; `JORNADA_MAXIMA` y `TE_LIMITES` en la tabla única de parámetros |
| Catálogo de jornadas | Validaciones de 3.3 (tope diario por tipo como máximo; tope semanal literal; prorrateo en la semana del 1 de enero) |
| Módulo de permisos | Recibir faltas «por confirmar» y «confirmadas» con la regla de 10; la alerta de cuarta falta solo con confirmadas |
| Módulo 4 | Leer el tiempo extra pendiente y los conceptos de 10 para «Otros devengados» |
| Vacaciones y aguinaldo; PTU | Usar solo faltas confirmadas |
| Módulo 6 | Cotejo por la clave SAT de `CONCEPTO_CLAVE_NOMINA` |
| Axia Compliance | Política de registro de jornada que limite las entradas anticipadas y regule el uso del checador (la jornada cuenta desde la marca de entrada, art. 9 del RIT) |
| Kit de contratación | `BIOMETRICO_JORNADA_CONSENT` en su diccionario (encargo 8 del paquete, a cargo de Cerebro) |

---

## 16. Partes provisionales [DEPENDE STPS]

Disposiciones generales del art. 132, fr. XXXIV LFT (transitorio quinto: vigencia 1/01/2027), no publicadas al 20/11/2026 según fuentes secundarias. Al publicarse, revisar:

1. Ámbito y excepciones (personas o empresas excluidas; trabajo en casa).
2. Datos mínimos del registro (si exige reposos, centro, dispositivo, modo de verificación).
3. Forma y plazo de entrega a la autoridad (11).
4. Requisitos del medio alterno y del registro manual (art. 13 del RIT; PN-07).
5. Conservación (11).
6. Cómo se acredita que el registro «fue acordado» (cláusula 6.5 del contrato, documento de designación y resumen del periodo de 7.1).

Si cambian, afectan valores, campos y textos de esta especificación y, en su caso, los arts. 13 y 22 del RIT; no la estructura.

---

## 17. Pendientes que no bloquean la programación

- Lecturas propias por confirmar con criterios o disposiciones: convivencia del máximo diario y de días del art. 66 con el tope gradual del transitorio cuarto; asignación cronológica de doble y triple; quinto día o quinta hora como triple; método neto del tiempo extra diario; tope semanal literal para nocturna y mixta; topes diarios como máximos frente a la distribución del art. 58; prima dominical además del pago de los arts. 73 y 75 para menores en domingo.
- Art. 784, fr. VIII LFT: la carga de la prueba del patrón sigue en 9 h semanales de tiempo extra; desde 2028 el tope legal la rebasa. Sin efecto en el diseño; vigilar criterios.
- El aviso del 20 % del Fonacot viene del paquete de contratación; su fundamento lo verifica esa conversación.

---

## 18. Casos de prueba

Datos comunes salvo indicación: año 2026; turno diurno de lunes a sábado, 09:00 a 17:30 con 30 min de comida (8 h efectivas, 48 h semanales); descanso el domingo; `SALARIO_PERSONA` $480.00; `TASA_HORA` $60.00; `CHECADOR_REGISTRA_COMIDA` = No; `TOLERANCIA_MIN` 10; `SEMANA_INICIO` lunes; `PRIMA_DOMINICAL_PCT` 25.

| # | Datos | Resultado esperado |
| --- | --- | --- |
| 1 | Tiempo extra con orden: lunes 3 h, martes 3 h, miércoles 3 h, jueves 2 h | Doble 9 h = $1,080.00; triple 2 h = $360.00 |
| 2 | Con orden, 1 h de lunes a viernes | Doble 4 h (lunes a jueves) = $480.00; triple 1 h (viernes, quinto día) = $180.00 |
| 3 | Con orden, martes 5 h | Doble 4 h = $480.00; triple 1 h = $180.00 |
| 4 | Persona de 17 años, 2 h con orden | Triple 2 h = $360.00; PN-11 crítica |
| 5 | Con orden: lunes 4, martes 4, miércoles 4, jueves 3 (15 h) | Doble 9 h (lunes, martes y 1 h del miércoles) = $1,080.00; triple 6 h = $1,080.00; PN-10 por 2 h sobre el excedente semanal |
| 6 | Falta confirmada el martes | Descuento $480.00 (solo el día; sin descuento del descanso) |
| 7 | Descanso los lunes; labora el domingo como día laborable | Prima dominical $120.00 |
| 8 | Labora su domingo de descanso | Descanso laborado $960.00 + prima dominical $120.00 |
| 9 | Labora el 16 de septiembre, día laborable | Festivo laborado $960.00 |
| 10 | Entrada 08:20, salida 17:30, sin orden | 40 min de tiempo extra sin orden previa; PN-09 por validar; si no se corrige, doble $80.00; expediente sugerido conducta 5 |
| 11 | Entrada 09:15, salida 17:45 | Tiempo laborado 8 h; sin tiempo extra (método neto); PN-03 sin efecto en nómina; cuenta para la conducta 1 |
| 12 | En un centro, 60 % de las personas sin marcas un día (`FALLA_CHECADOR_PCT` 50) | PN-07; no se generan PN-01 ese día en ese centro |
| 13 | Entrada a las 09:00 sin salida | PN-02; conceptos variables detenidos; salario ordinario se exporta |
| 14 | Turno nocturno de 7 h × 6 días en 2030 | El catálogo bloquea: 42 h > 40 h |
| 15 | Semana del lunes 28/12/2026 al domingo 3/01/2027 | Máximo semanal prorrateado (48 × 4 + 46 × 3) ÷ 7 = 47.14 h; tope semanal de tiempo extra con 100 % más: 9 h |
| 16 | Lactancia con reducción; marca 7 h | Jornada esperada 7 h; sin PN-04 |
| 17 | Día en casa sin marcas | PN-16; no se genera PN-01 |
| 18 | Ausencia sin evento en modo Conectado, confirmada por RH antes de validar | El módulo de permisos la recibe como confirmada; descuento como en el caso 6 ($480.00) |
| 19 | Periodo semanal validado con 3 h de tiempo extra con orden (doble $360.00), no exportado; el mismo día RH registra la baja | La persona no entra a la exportación; las 3 h quedan «Revisar en el finiquito» con su importe; el módulo 4 las precarga como «Sugerido». Una aclaración procedente posterior queda también «Revisar en el finiquito», con alerta a RH y consultoría |
