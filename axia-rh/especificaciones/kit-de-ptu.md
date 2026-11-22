# AXIA RH — MÓDULO 3: PROCEDIMIENTO DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES (PTU)

Especificación para programación · Versión 1.2 · 21/11/2026
Fuente: «Kit maestro – Procedimiento de PTU» (Claude Docs, rev. 87), «Corte - Kit de PTU» (20/11/2026), registro de decisiones (4.5, 4.7, 4.13 y 5.4) y encargos del mapa del PMV al kit (17/11/2026). Aprobaciones provisionales hasta la revisión final del usuario.

> **Nota de Cerebro (21/11/2026, autorizada por el usuario).** En esta copia se aplicó el encargo 5 del mapa: el cambio 3 y el final de R-4 (5.2) ya no dicen que el módulo 9 descuenta el descanso proporcional en nómina (el módulo 9 v1.1 no lo descuenta). La regla de cálculo no cambia. Cerebro aplicó el mismo cambio en la versión del proyecto el 21/11/2026.
>
> **Nota de Cerebro (21/11/2026, decisiones P1 a P10 del diccionario único, aplicadas por Cerebro con autorización del usuario).** `AUTORIDAD_INSPECCION` guarda solo el nombre de la autoridad; el ámbito federal o local sale de `COMPETENCIA` (decisión P2). `REGISTRO_PATRONAL` es el `CENTRO_REGISTRO_PATRONAL` del catálogo de centros (decisión P1). Los textos no cambian.

## Cambios respecto de las versiones 1.0 y 1.1

Si la 1.0 ya se cargó, basta aplicar esta tabla (los cambios 5 a 7 son de la 1.2). Ante cualquier duda, rige el texto completo.

| # | Sección | Cambio | Origen |
| --- | --- | --- | --- |
| 1 | 5.2 (R-4, tabla `PTU_COMPUTA`) | La fila «Falta injustificada» se divide: **falta confirmada** del módulo 9 (no computa) y **falta por confirmar** (computa mientras RH no la confirme) | Encargo 4 del mapa (20/11/2026); registro 4.14 |
| 2 | 5.2 (R-4, reglas) | Con faltas por confirmar al calcular, alerta a RH sin bloquear; confirmar o descartar una falta después de `CALCULO_CONFIRMADO` revierte la confirmación de esa persona; con D-08 B firme se atiende como observación (D-10) | Mismo encargo; gemelo de la regla de `AGUINALDO_VALIDADO` |
| 3 | 5.2 y 5.4 | Cada falta confirmada o día sin goce resta solo su propio día; ninguno resta el día de descanso. `PTU_COMPUTA` y `AGUINALDO_COMPUTA` cambian juntas | Decisión del usuario (21/11/2026) |
| 4 | Anexo A.3 | Casos 17 y 18 | — |
| 5 | 8 y 8.1 (nueva) | Los documentos de la Comisión se firman de forma electrónica o autógrafa con `FIRMA_COMISION`, por documento; sustituye el uso de `FIRMA_MODALIDAD` en esos documentos | Decisión del usuario (21/11/2026) |
| 6 | 10.2, 11.3 | `FIRMA_COMISION` en el diccionario; se cierra el pendiente del nivel de firma | Ídem |
| 7 | Anexo A.3 | Casos 19 y 20 | — |

El módulo genera los 14 documentos del procedimiento (D-01 a D-14), calcula el reparto individual, precalcula el neto de cada persona y controla el pago y la PTU no cobrada junto con el módulo 6. Funciona con y sin sindicato y para cualquier resultado del ejercicio: sin cantidad repartible (A), con reparto (B) o con excepción legal (C).

---

## 0. Convenciones

- Variables: `{{MAYÚSCULAS_CON_GUION_BAJO}}`. Se sustituyen por el dato; nunca se imprime la marca.
- Condiciones: `[SI condición] … [FIN SI]`. Operadores `=`, `>`, `<`, `Y`, `O`. Cada alternativa es su propia condición; no existe «si no». Si la condición es falsa, se omite todo el bloque. Se permiten condiciones anidadas; cada `[SI]` cierra con su `[FIN SI]`. Las marcas nunca se imprimen.
- Términos fijos en los textos: «la Empresa» y, en estos instrumentos colectivos, «las personas trabajadoras» (plural y minúscula). La denominación legal de la comisión se conserva: «Comisión Mixta de Participación de los Trabajadores en las Utilidades».
- Niveles de captura:
  - **E** = configuración de la empresa (incluye el catálogo de centros y de turnos).
  - **O** = organigrama o puesto.
  - **A** = alta de la persona trabajadora.
  - **V** = evento: pantalla «PTU» (Comisión o ejercicio).
  - **S** = calculada por el sistema (no editable salvo que se indique).
  - **X** = tabla global que administra AEXIS (parámetros con vigencia, aprobación humana).
  - **Módulo 6** = dato que vive en la obligación de pago del módulo 6.
- Montos: MXN con dos decimales. Factores del reparto con 9 decimales.
- Fechas: formato largo («30 de mayo de 2026»).
- **Días hábiles:** calendario de días inhábiles del módulo 4 (fines de semana, descansos obligatorios y días que marque la empresa). El conteo empieza el día hábil siguiente al hecho.
- Ningún texto ni código fija cifras que cambian (porcentaje de PTU, UMA, tarifas): viven en tablas X.
- Formato de impresión: Arial 12, títulos en negrita del mismo tamaño o uno mayor, papel carta, PDF generado en el servidor sin encabezado ni pie del navegador.
- Reglas de pantalla del registro 5.0: guardar nunca se bloquea; sin candados por fecha (solo se valida el orden entre fechas); los campos que dependen de una opción aparecen después de ella; la casilla «documento firmado» basta para avanzar (salvo el pago, que sigue el módulo 6); concordancia de número (con valor 1, singular; nunca «(s)»).
- Los documentos generados para el cliente no llevan «AEXIS» ni «AXIARH».

---

## 1. Arquitectura

| Entidad | Qué es | Se crea |
| --- | --- | --- |
| Comisión (`PTU_COMISION`) | Integración vigente: propietarios, suplentes, coordinador y secretario, con su historial de sustituciones | Con D-03; se modifica con D-13 |
| Jornada de elección (opcional) | Datos de la elección formal: padrón, mesas, votos | Solo con `SINDICATO` = No y `DESIGNACION_OBRERA` = Elección (D-01, D-02) |
| Ejercicio PTU (`PTU_EJERCICIO`) | Un evento por empresa y ejercicio fiscal | Al capturar `FECHA_PRESENTACION` de la declaración anual |
| Persona del reparto | Una fila por persona con relación vigente en algún momento del ejercicio: días, salario, límite, bruto, neto, estado de pago | Al elegir `VIA_CALCULO` (R-1, R-2 o R-4) |
| Sesión | Cada convocatoria (D-04) y su acta (D-05, D-07, D-10, D-12) | Desde el ejercicio |
| Observación | Cada observación al proyecto, con folio, materia, resolución y ajuste | En el periodo de observaciones |
| Contingencia | Complementaria, resolución del SAT (D-12) o sustitución de integrante (D-13) | En cualquier momento del año |

Reglas generales:

- La Comisión opera por tiempo indefinido para los ejercicios sucesivos; D-01 a D-03 se generan una vez y solo se repiten al renovarla completa.
- El personal de confianza vota en la elección, pero no puede ser representante obrero: el selector de `REP_TRAB_*` excluye personas con clasificación Confianza y personas de otros centros (registro 5.4). Una persona puede representar en más de una comisión.
- El tiempo dedicado a la Comisión es tiempo de trabajo con goce de salario (no genera evento de ausencia).
- El kit no hace referencia a la CMRIT ni a la comisión de capacitación.

---

## 2. Pantallas y flujo

### 2.1 Configuración (nivel E)

`SINDICATO`, `DESIGNACION_OBRERA` (solo con `SINDICATO` = No; Designación por omisión), `NUM_REPRESENTANTES_POR_PARTE` (mínimo 1; común con la CMRIT), `REPRESENTANTES_SUPLENTES` (Sí por omisión), `EMPRESA_TIPO_PERSONA`, `PTU_ISR_METODO` (Art. 174 RLISR por omisión), `PTU_AVISO_RECORDATORIO_DIAS` (60), `TRABAJO_HOGAR` (No), `AUTORIDAD_INSPECCION` (solo el nombre de la autoridad; el ámbito sale de `COMPETENCIA`) y, del catálogo de centros, domicilio, municipio, registro patronal y lugares de publicación.

### 2.2 Pantalla «Comisión» (fase 0)

1. Si `SINDICATO` = No y `DESIGNACION_OBRERA` = Elección: capturar la jornada y generar D-01 (aviso) y, después de la jornada, D-02 (constancia y acta). Validación: `FECHA_INICIO_PUBLICACION` ≤ `FECHA_ELECCION` − 5 días hábiles; la elección es válida con más de 50 % del padrón en la primera jornada; si no, segunda jornada dentro de 10 días hábiles, sin umbral. Sin voto secreto: la votación se hace como acuerden las personas asistentes.
2. Capturar propietarios y suplentes de ambas representaciones, coordinador (de la Empresa) y secretario (obrero). Con `SINDICATO` = Sí, el oficio sindical es el Anexo 1 de D-03.
3. `CONFORMIDAD_FIRMAS` (No por omisión). El sistema la recomienda con un aviso cuando hay un ejercicio con `RESULTADO` = B; no la exige.
4. Generar D-03 (acta de integración y estatutos).
5. Sustituciones: D-13 (sección 2.4).

### 2.3 Pantalla «Ejercicio PTU» (fases 1 a 4)

| Paso | Captura | Documento | Condición para avanzar |
| --- | --- | --- | --- |
| 1. Declaración | `EJERCICIO`, `FECHA_PRESENTACION`, `NUM_OPERACION`, `RENTA_GRAVABLE_PTU`, excepción del art. 126 (`FRACCION_126`, `HECHO_EXCEPCION`, `DOCUMENTO_EXCEPCION`, `FECHA_FIN_EXCEPCION`) | — | Calcula `RESULTADO` y el calendario (sección 3) |
| 2. Convocatoria | Datos de la sesión | D-04 | — |
| 3. Entrega de la declaración | Asistentes, fojas, lugar y horario de consulta | D-05 (acta) y D-06 (aviso de consulta, sin firmas; evidencia: fotografía fechada por lugar) | Alerta si la sesión rebasa 10 días hábiles desde `FECHA_PRESENTACION` |
| 4. Datos por persona (solo B) | `VIA_CALCULO` y R-1, R-2 o R-4 | Reporte de validación | Sin errores; con Automático, `CALCULO_CONFIRMADO` = Sí |
| 5. Proyecto | Sesión de formulación | D-07 y D-08 (módulo A, B o C) | D-08 B solo con datos por persona validados |
| 6. Publicación y observaciones | `FECHA_PUBLICACION`, observaciones con folio | D-09 al cierre; D-10 si hay observaciones | D-10 a más tardar en `FECHA_LIMITE_RESOLUCION` |
| 7. Precálculo (solo B) | R-5; `PTU_CALCULO_VALIDADO` | — | Neto ≥ 0 por persona |
| 8. Pago (solo B) | El pago se registra en el módulo 6 | D-11 Parte 1 (avisos), D-14 (recibos), D-11 Parte 2 (constancia) | Ver sección 7 |

Con `RESULTADO` = A o C, el flujo termina en D-09 (publicación) y no hay pasos 7 y 8.

### 2.4 Contingencias (cualquier momento)

- `EVENTO` = Complementaria o Resolución SAT → D-12 (sesión extraordinaria). La copia de la complementaria se entrega conforme a D-05 y los plazos de consulta y objeción se computan desde la sesión. Con `DIFERENCIA_POSITIVA` = Sí y sin impugnación, reparto adicional: el sistema abre un sub-ejercicio con D-08 B por la diferencia y obligaciones «PTU adicional» en el módulo 6, con `FECHA_LIMITE_PAGO_ADICIONAL` = notificación + 60 días. Con `IMPUGNACION_EMPRESA` = Sí, el reparto adicional se suspende hasta que la resolución quede firme y se exige capturar `GARANTIA` (art. 122 LFT, verificado; texto vigente con última reforma DOF 14-05-2026).
- `EVENTO` = Sustitución → D-13. `CAUSA_VACANTE` es lista: terminación de la relación de trabajo, renuncia al cargo, promoción a puesto de confianza, revocación o ausencia injustificada a dos sesiones consecutivas. Una baja en el alta o un cambio a un puesto de confianza de un integrante obrero genera alerta para levantar D-13.

---

## 3. Calendario y alertas

| Hito | Regla | Fundamento | Alerta |
| --- | --- | --- | --- |
| Entrega de copia y anexos a disposición | 10 días hábiles desde `FECHA_PRESENTACION` (o de la complementaria) | Art. 121, fr. I LFT; art. 9 del Reglamento de los arts. 121 y 122 | Preventiva a 5 días; crítica al vencer sin D-05 |
| Consulta de anexos (`FECHA_FIN_CONSULTA`) | 30 días hábiles desde la entrega | Art. 10 del Reglamento | Informativa |
| Objeciones ante el SAT (`FECHA_LIMITE_OBJECIONES`) | 30 días hábiles siguientes a la consulta (sindicato o mayoría; la Comisión no objeta) | Art. 121, fr. II LFT; art. 13 del Reglamento | Informativa |
| Publicación del proyecto (`FECHA_PUBLICACION`) | A más tardar 45 días hábiles antes de `FECHA_LIMITE_PAGO` | Criterio preventivo | Preventiva a 10 días hábiles; crítica al vencer |
| Observaciones (`FECHA_FIN_OBSERVACIONES`) | 15 días hábiles desde la publicación | Art. 125, fr. III LFT | — |
| Resolución (`FECHA_LIMITE_RESOLUCION`) | 15 días hábiles desde el cierre de observaciones | Art. 125, fr. IV LFT | Crítica si hay observaciones sin D-10 |
| Pago (`FECHA_LIMITE_PAGO`) | 30 de mayo (moral) o 29 de junio (física) del año siguiente al ejercicio | Art. 122 LFT | Las del módulo 6 (`PAGO_ALERTAS_PTU`, 15 y 5 días hábiles) |
| Pago adicional | 60 días desde la notificación de la resolución del SAT | Art. 122 LFT | Las del módulo 6 |
| Aviso a ex trabajadores (D-11 Parte 1) | A más tardar en `FECHA_LIMITE_PAGO` | R-3 | Crítica en esa fecha si falta |
| Traspaso (`FECHA_TRASPASO_PTU`) | Un año desde el día siguiente a `FECHA_LIMITE_PAGO` | Art. 516 LFT | Consultoría, 30 días antes |

Reglas:

- La presentación de objeciones ante el SAT no suspende el pago; el sistema no ofrece pausar alertas por objeción.
- Si un plazo de días naturales vence en día inhábil, la alerta se adelanta al día hábil anterior.
- Sin candados por fecha: los documentos se pueden generar con fechas futuras; el sistema solo valida el orden (entrega ≤ publicación ≤ fin de observaciones ≤ resolución ≤ pago).

---

## 4. Resultado del ejercicio

| `RESULTADO` | Condición | Dictamen | Documentos de pago |
| --- | --- | --- | --- |
| A | `RENTA_GRAVABLE_PTU` ≤ 0 y sin excepción | D-08 módulo A (reserva para complementaria o resolución) | No |
| B | `RENTA_GRAVABLE_PTU` > 0 y sin excepción | D-08 módulo B | D-11 y D-14 |
| C | Excepción del art. 126 capturada | D-08 módulo C | No |

La renta gravable para PTU es la del art. 9 LISR sin disminuir la PTU pagada ni las pérdidas fiscales de ejercicios anteriores. La captura la hace el cliente.

---

## 5. Motor del reparto (solo `RESULTADO` = B)

### 5.1 Vías de datos

| `VIA_CALCULO` | Origen | Regla |
| --- | --- | --- |
| Automático | Datos del sistema (alta, módulo 5, eventos de permisos y vacaciones) | R-4 |
| Importación | Archivo de nómina por CURP | R-1 |
| Captura | Pantalla con una fila por persona, prellenada | R-2 |

En las tres vías el sistema exige datos **por persona**; no se admiten totales globales. Errores bloquean D-08 B; advertencias no, y quedan en el Anexo 1 de D-07.

### 5.2 Reglas R-1, R-2 y R-4

#### R-1. Layout de importación de nómina

Un archivo CSV o XLSX por ejercicio, una fila por persona que prestó servicios en el ejercicio (activas y bajas). La llave es la CURP: cada fila se cruza con el alta, y del alta y el organigrama se toman los datos que no vienen en la nómina.

| Campo | Tipo | Obligatorio | Validación | Uso |
| --- | --- | --- | --- | --- |
| EJERCICIO | Año | Sí | Igual al ejercicio del evento PTU | Control |
| CURP | Texto (18) | Sí | Formato y dígito verificador; debe existir en el sistema; sin duplicados | Llave con el alta |
| NUM_EMPLEADO | Texto | No | — | Recibo y versión publicable |
| FECHA_INGRESO | Fecha | Sí | Coincide con el alta; si no, advertencia | Días posibles |
| FECHA_BAJA | Fecha | Si causó baja | Dentro del ejercicio o vacía | EX_TRABAJADOR y avisos |
| DIAS_TRABAJADOS | Entero | Sí | 0 a días naturales del ejercicio; no mayor que los días entre ingreso y baja | Primera mitad del reparto |
| DIAS_INC_RIESGO | Entero | Sí (0 si no hay) | No mayor que los días del periodo | Se suman como días en servicio activo |
| DIAS_INC_MATERNIDAD | Entero | Sí (0 si no hay) | Ídem | Se suman como días en servicio activo |
| SALARIO_DEVENGADO | Moneda | Sí | Mayor que 0 si DIAS_TRABAJADOS > 0; advertencia si es menor que el salario mínimo de la zona por los días | Segunda mitad del reparto |
| SALARIO_VARIABLE | Sí / No | Sí | — | Con Sí, SALARIO_DEVENGADO es el promedio de percepciones del ejercicio |
| SALARIO_DIARIO | Moneda | No | Si se importa, se coteja con SALARIO_PERSONA; la diferencia es advertencia | Solo cotejo; el límite de tres meses usa SALARIO_PERSONA |
| PTU_RECIBIDA_1, _2 y _3 | Moneda | No | 0 o mayor | Límite por promedio de tres años; si el sistema tiene el historial, lo toma de ahí |

**Regla de salario.** SALARIO_DEVENGADO es la cuota diaria en efectivo por los días del ejercicio, sin gratificaciones, percepciones ni demás prestaciones, ni tiempo extraordinario. El layout lo dice en su encabezado y el reporte de validación lo recuerda.

**Regla de días.** DIAS_TRABAJADOS incluye los días laborados, las vacaciones y los permisos con goce de salario. Las incapacidades por riesgo de trabajo y por maternidad se reportan aparte y el sistema las suma. No se computan las faltas, los permisos sin goce, las suspensiones ni las incapacidades por enfermedad general.

**Datos que no se importan.** Se toman del sistema: clasificación base o confianza (organigrama), exclusión por dirección, administración o gerencia general (atributo de puesto PTU_EXCLUIDO), tipo de relación y eventualidad (alta), sindicalización cuando SINDICATO = Sí (alta), y domicilio, correo y teléfono (alta).

**Totales de control.** El cliente captura además el total de días y el total de salarios de su nómina. El sistema los compara con la suma de las filas; la diferencia es advertencia, no sustituye los datos por persona.

**Reporte de validación.** Cada importación genera un reporte con errores y advertencias. Los errores (CURP inexistente, duplicados, días fuera de rango, salario faltante) bloquean D-08 B. Las advertencias no bloquean, pero quedan en el Anexo 1 de D-07.

#### R-2. Captura por persona

Con VIA_CALCULO = Captura, la pantalla del evento PTU lista a todas las personas con relación vigente en algún momento del ejercicio, prellenadas desde el alta (CURP, nombre, fechas) y con su salario diario (SALARIO_PERSONA de la versión de condiciones vigente al cierre del ejercicio o a la baja). Por cada una se capturan los mismos campos obligatorios de R-1: días trabajados, días de incapacidad por riesgo y por maternidad, salario devengado y salario variable; el salario diario es el SALARIO_PERSONA prellenado. No se admiten totales globales. Se aplican las mismas validaciones y el mismo reporte.

#### R-4. Cálculo automático

Con VIA_CALCULO = Automático, el sistema calcula los datos por persona con lo que ya tiene registrado, sin importar ni capturar nómina:

| Dato | Cómo lo obtiene el sistema |
| --- | --- |
| Personas con derecho | Altas con relación vigente en algún momento del ejercicio; excluye puestos con PTU_EXCLUIDO = Sí y eventuales con menos de 60 días |
| Días computables | Días naturales de la relación dentro del ejercicio, menos los días de eventos que la tabla PTU_COMPUTA marca como no computables (abajo) |
| Salario devengado | SALARIO_PERSONA de la versión de condiciones vigente en cada periodo (con su historial de cambios por MOD-1 o MOD-2) por los días computables de ese periodo |
| Salario diario | SALARIO_PERSONA vigente al cierre del ejercicio o a la fecha de baja, para el límite de tres meses |
| PTU de los últimos tres años | Historial de repartos del sistema; sin historial, se toma 0 y se avisa |

El sistema genera un reporte por persona que RH revisa y confirma (CALCULO_CONFIRMADO); sin confirmación no se genera D-08 B. Alertas que no bloquean: personas con salario variable (deben pasar a captura, porque el sistema no conoce sus percepciones), ejercicios sin incidencias registradas (el cálculo supone días completos y puede aumentar la participación) y cambios de salario fuera del sistema.

Tabla PTU_COMPUTA (17/11/2026). Indica, por tipo de evento del módulo de permisos y del registro de vacaciones, si el día cuenta para la primera mitad del reparto. Es gemela de AGUINALDO_COMPUTA (módulo de vacaciones y aguinaldo) y coincide con la columna «Día computable para PTU» de la tabla de efectos del módulo de permisos; se administra aparte para que una pueda cambiar sin la otra.

| Evento o registro | Computa | Fundamento o criterio |
| --- | --- | --- |
| Días sin evento (laborados, descansos semanales y festivos) | Sí | Servicio prestado durante la relación |
| Vacaciones (VAC-1) | Sí | Criterio aprobado (registro 4.7) |
| A1, A2, B2 y A4 con goce de salario | Sí | Permisos con goce (registro 4.7) |
| A3 con goce (COMISION_GOCE = Sí) | Sí | Permiso con goce |
| A3 sin goce y A4 sin goce | No | Permisos sin goce |
| B1 lactancia | Sí | Día laborado con jornada reducida |
| B3, B4 y B5 | No | Licencias sin salario a cargo de la Empresa |
| C1 enfermedad general, incluidos los días de espera que pague la Empresa | No | Registro 4.7; el pago voluntario de los días de espera no los convierte en servicio activo |
| C2 riesgo de trabajo | Sí | Servicio activo (art. 127, fr. IV) |
| C3 maternidad | Sí | Servicio activo (art. 127, fr. IV) |
| D1 a D5 | No | Suspensiones (registro 4.7) |
| D4 con reubicación aceptada (MOD-5) | Sí | Se trabaja con salario |
| Falta confirmada (módulo 9), suspensión disciplinaria y suspensión por fin de temporada | No | Registro 4.7 |
| Falta por confirmar (módulo 9) | Sí, mientras RH no la confirme | Ausencia sin evento aún no calificada; solo la falta confirmada descuenta (registro 4.14) |

Reglas: la tabla vive con los parámetros versionados y solo cambia con aprobación humana; un cambio no altera dictámenes firmes. Cada día tiene un solo evento (la incapacidad prevalece), por lo que ningún día se descuenta dos veces. Con VIA_CALCULO = Importación o Captura, la tabla no se aplica a los días que reporta el cliente, pero el sistema la usa para advertir si DIAS_TRABAJADOS no coincide con los eventos registrados. Los 60 días de las personas eventuales se cuentan con días computables. (21/11/2026, encargo 4 del mapa) Al calcular con VIA_CALCULO = Automático, si hay faltas por confirmar del ejercicio, el sistema alerta a RH para confirmarlas o descartarlas, sin bloquear; confirmar o descartar una falta después de CALCULO_CONFIRMADO revierte la confirmación de esa persona, y después de D-08 B firme se atiende como observación (D-10). Cada falta confirmada o día sin goce resta solo su propio día; ninguno resta el día de descanso, igual que en AGUINALDO_COMPUTA (decisión del usuario, 21/11/2026; las dos tablas cambian juntas).

### 5.3 Algoritmo del reparto

1. **Total a repartir.** `UTILIDAD_REPARTIBLE` = `RENTA_GRAVABLE_PTU` × `PORCENTAJE_PTU` (tabla X). `TOTAL_A_REPARTIR` = `UTILIDAD_REPARTIBLE` + `MONTO_NO_RECLAMADO_ANTERIOR` (traspasos de R-3).
2. **Personas con derecho.** Todas las que prestaron servicios en el ejercicio, activas y bajas, menos: puestos con `PTU_EXCLUIDO` = Sí (art. 127, fr. I); eventuales con menos de 60 días computables (fr. VII); personas trabajadoras del hogar si `TRABAJO_HOGAR` = Sí (fr. VI).
3. **Salario computado (tope de confianza, art. 127, fr. II).** `SALARIO_REFERENCIA` = salario diario más alto entre las personas sindicalizadas (`SINDICATO` = Sí y `SINDICALIZADO` = Sí) o, a falta de ellas, entre las de planta (clasificación Base). `SALARIO_MAXIMO_CONFIANZA` = `SALARIO_REFERENCIA` × 1.20. Para cada persona de confianza: salario computado = menor entre su salario diario y `SALARIO_MAXIMO_CONFIANZA`; su salario devengado computado = salario computado × días con salario (en Automático) o salario devengado × (salario computado ÷ salario diario) (en Importación y Captura).
4. **Primera mitad (días).** `FACTOR_DIAS` = (`TOTAL_A_REPARTIR` ÷ 2) ÷ suma de días computables. `PTU_POR_DIAS` = días computables × `FACTOR_DIAS`.
5. **Segunda mitad (salarios).** `FACTOR_SALARIOS` = (`TOTAL_A_REPARTIR` ÷ 2) ÷ suma de salarios devengados computados. `PTU_POR_SALARIOS` = salario devengado computado × `FACTOR_SALARIOS`.
6. **Bruta.** `PTU_POR_DIAS` + `PTU_POR_SALARIOS`.
7. **Límite individual (art. 127, fr. VIII).** Límite = mayor entre `SALARIO_PERSONA` × 90 (salario vigente al cierre del ejercicio o a la baja) y el promedio de `PTU_RECIBIDA_1`, `_2` y `_3`. Si la bruta excede el límite: `TOPE_APLICADO` = Sí, `MONTO_PTU` = límite y el excedente individual se acumula en `MONTO_EXCEDENTE`.
8. **Excedente.** No se paga, no se redistribuye entre las demás personas ni se agrega a la utilidad repartible de ejercicios posteriores, y no es PTU no reclamada (decisión del usuario, 17/11/2026). D-08 B, QUINTO, lo hace constar con texto fijo; D-11 cuadra «menos el excedente».
9. **Redondeo.** Cada importe individual se redondea a centavos. La diferencia entre la suma de las brutas y `TOTAL_A_REPARTIR` por redondeo se muestra en el cuadre; si es mayor que `PAGO_TOLERANCIA` (módulo 6), el sistema alerta.
10. **Anexo 1 de D-08.** Versión completa (nombre, situación, días computables, salario computado, por días, por salarios, límite aplicado y participación final), a disposición de la Comisión y de cada persona respecto de sus datos. Versión publicable: nombre, días computables y monto; es la única que se fija.

Caso de prueba: Anexo A.1.

### 5.4 Tabla `PTU_COMPUTA`

Ver R-4 (5.2). Debe coincidir con la columna «Día computable para PTU» de la tabla de efectos del módulo de permisos (10.1). Es tabla aparte de `AGUINALDO_COMPUTA`: las dos difieren solo en los días de espera de C1 pagados por la Empresa y en D1 por la fr. III, que computan para el aguinaldo y no para la PTU. Las faltas siguen la misma regla en las dos: solo la confirmada descuenta, y solo su propio día.

---

## 6. Precálculo de deducciones (R-5)

Con RESULTADO = B, el sistema calcula por persona el neto estimado de la participación, con los mismos parámetros versionados del módulo 4 (UMA, tarifa mensual del art. 96 LISR del Anexo 8 de la RMF, REF_EXENCION). Es una previsualización: el contador puede sustituir cualquier cifra con motivo y valida el cálculo (PTU_CALCULO_VALIDADO) antes de generar D-14 en versión final. Toda presentación lleva la leyenda «ISR estimado; el definitivo consta en el CFDI de nómina».

| Paso | Cálculo | Fundamento |
| --- | --- | --- |
| 1. Parte exenta | Menor entre la participación bruta y 15 veces la unidad de referencia diaria (REF_EXENCION; UMA por omisión), menos lo ya exento por PTU en el mismo año, si existe | Art. 93, fr. XIV LISR |
| 2. Parte gravada | Participación bruta − parte exenta | Art. 93, fr. XV LISR |
| 3. ISR, método general | ISR = tarifa mensual aplicada a (ingreso mensual ordinario + parte gravada) − tarifa mensual aplicada al ingreso mensual ordinario | Art. 96 LISR |
| 3 bis. ISR, método opcional | Parte gravada ÷ 365 × 30.4 = PTU mensual; diferencia = tarifa a (ingreso ordinario + PTU mensual) − tarifa al ingreso ordinario; tasa = diferencia ÷ PTU mensual; ISR = parte gravada × tasa | Art. 174 RLISR |
| 4. Seguridad social y vivienda | Sin cuotas obreras del IMSS ni amortización Infonavit: la participación no integra el salario base de cotización | Art. 27, fr. IV LSS |
| 5. Pensión alimenticia | Solo si la resolución judicial comprende la participación: porcentaje de la resolución sobre la base que ella indique (bruta o neta de ISR) | Art. 110, fr. V LFT |
| 6. Otras deducciones | Tabla dinámica (anticipo o préstamo de la Empresa, otra autorizada), con aviso: la participación está protegida como el salario y solo admite los descuentos del art. 110 LFT | Art. 130 LFT |
| 7. Neto estimado | Participación bruta − ISR − pensión − otras deducciones | — |

Reglas:

- **Método.** PTU_ISR_METODO se configura por empresa: «Art. 174 RLISR» (por omisión, porque retiene menos en el mes de pago; texto verificado en el Reglamento vigente, última reforma DOF 06-05-2016, fracciones I a V) o «Art. 96 LISR». Para quien ya no labora, o no tiene ingreso mensual ordinario, siempre se usa el método general con ingreso ordinario en cero. Con el art. 174, el sistema aplica la tasa a la parte gravada, porque la exenta no causa impuesto (art. 93, fr. XIV LISR); como la fracción IV del art. 174 dice «sin deducción alguna», el contador puede sustituir la retención por la que resulte de aplicar la tasa a la participación total, criterio más conservador.
- **Ingreso mensual ordinario** (INGRESO_MENSUAL_ORDINARIO): por omisión, SALARIO_PERSONA vigente × 30.4; el contador puede capturarlo.
- **Subsidio para el empleo:** no se aplica en el precálculo. Aviso: «Si la PTU se paga en la nómina ordinaria, el subsidio del mes puede cambiar la retención».
- **Fonacot:** no se descuenta de la PTU. El crédito se paga con una cuota mensual fija que la Empresa retiene del salario conforme a la cédula del Instituto (art. 110, fr. VII LFT); la PTU no cambia esa cuota. Si la persona causa baja, la retención se ve en el finiquito (módulo 4).
- **Pensión alimenticia:** con PENSION_ALIMENTICIA = Sí y PENSION_INCLUYE_PTU sin capturar, el sistema no calcula la pensión y muestra «Revise si la resolución comprende la PTU».
- **Bloqueo:** neto negativo. Sin parámetro aprobado, el concepto muestra «No calculado», nunca $0.00.
- **Personas pagadas con el finiquito:** el precálculo no se repite; la retención es la del recibo de finiquito.

Caso de prueba (parámetros 2026: UMA $117.31; tarifa mensual del Anexo 8 RMF 2026): participación bruta $18,000.00, ingreso mensual ordinario $15,000.00, sin pensión. Parte exenta $1,759.65; parte gravada $16,240.35. Método del art. 174: PTU mensual $1,352.62, tasa 17.92 %, ISR $2,910.27, neto $15,089.73. Método del art. 96: ISR $3,381.77, neto $14,618.23.

---

## 7. Pago, control de PTU no cobrada y finiquito

### 7.1 Estados (R-3)

Cada persona con participación mayor a cero tiene un estado de pago en el módulo 6:

1. **Pendiente de pago**, desde que el dictamen queda firme.
2. **Pagada**, con el CFDI o la dispersión cotejados en el módulo 6. La firma de D-14 no es condición de este estado: se controla aparte con D14_FIRMADO y, si falta, solo genera alerta a RH, sin revertir el estado.
3. **Pagada en finiquito**, cuando se pagó con el concepto «PTU pendiente»; bloquea un segundo pago.
4. **Pendiente con aviso**, para quien no ha cobrado y ya recibió el aviso de D-11 Parte 1.
5. **No reclamada**, al vencer el plazo de traspaso sin cobro.

Alertas: el aviso de D-11 se envía a más tardar en la fecha límite de pago; un recordatorio a los PTU_AVISO_RECORDATORIO_DIAS días (60 por omisión); y alerta a consultoría 30 días antes de FECHA_TRASPASO_PTU.

Al vencer FECHA_TRASPASO_PTU, un año contado desde el día siguiente a FECHA_LIMITE_PAGO (plazo de prescripción del art. 516 LFT), el sistema marca a la persona como No reclamada y suma su monto a MONTO_NO_RECLAMADO_ANTERIOR del primer reparto que se determine después, con un registro de traspaso por persona.

Si la persona reclama después de ese plazo, el sistema no paga: registra la reclamación y alerta a consultoría para que la Empresa haga valer la prescripción, que no opera de oficio.

### 7.2 Relación con el módulo 6

- Con D-08 B firme y `PTU_CALCULO_VALIDADO` = Sí, el módulo 6 crea una obligación «PTU {ejercicio}» por persona con `MONTO_PTU` > 0, por el neto de R-5. Con reparto adicional, obligaciones «PTU adicional {ejercicio}».
- «Pagada» solo con CFDI o dispersión cotejados en el módulo 6. D-14 toma de la obligación `UUID_CFDI`, `FECHA_PAGO`, `FORMA_PAGO` y `REFERENCIA_DISPERSION`.
- D-11 Parte 2 solo se habilita cuando cada persona del Anexo 1 del dictamen está en Pagada, Pagada en finiquito o Pendiente con aviso. Su Anexo 1 lo genera el módulo 6 (persona, monto, fecha, UUID o referencia, estado y `D14_FIRMADO`).

### 7.3 Personas que causan baja

| Situación | Regla |
| --- | --- |
| Baja después del cierre del ejercicio, dictamen no firme | El finiquito muestra «PTU pendiente» sin monto, con la leyenda «se paga en la fecha de reparto»; la obligación nace después con `EX_TRABAJADOR` = Sí y aviso D-11 Parte 1 |
| Baja con dictamen firme y PTU no pagada | El finiquito puede incluir «PTU determinada no pagada»; si se paga ahí, la obligación pasa a «Pagada en finiquito» y se bloquea un segundo pago. El precálculo R-5 no se repite: la retención es la del recibo de finiquito |
| Ex trabajador | Siempre ISR por el art. 96 con ingreso ordinario en cero; D-11 Parte 1 al último domicilio, correo o teléfono del alta |

### 7.4 Recibo D-14 y su firma

- Versión final solo con la obligación en «Pagada» y `PTU_CALCULO_VALIDADO` = Sí; antes, borrador.
- Con dispersión sin UUID (`CFDI_REGISTRADO` = No): sin renglón del folio fiscal y con la referencia de la dispersión. Al cargarse el UUID, o si el CFDI se cancela y sustituye, nueva versión.
- **Firma (20/11/2026).** `FIRMA_D14` (por persona): por omisión, la `FIRMA_MODALIDAD` de la persona; RH la cambia a Autógrafa cuando la persona firma en papel (pago en ventanilla o persona sin acceso a la Plataforma, como quien ya no labora), cuando falla la Plataforma o cuando se niega (dos testigos y envío al correo personal). Con Electrónica: sello `FIRMA_SELLO_TRAB` («Pendiente de firma electrónica» antes de firmar) y cláusula de firma electrónica. Con Autógrafa: línea de firma. Solo firma la persona trabajadora.
- `D14_FIRMADO` se marca con cualquiera de las dos formas; si falta, alerta a RH a los `PAGO_EVIDENCIA_DIAS` días hábiles, sin revertir «Pagada».
- Si la PTU se pagó con el finiquito, D-14 no se genera: la evidencia es el recibo de finiquito.

---

## 8. Firma de los documentos

| Documento | Quién firma | Forma |
| --- | --- | --- |
| D-01 aviso de convocatoria, D-06 aviso de consulta, D-11 Parte 1 aviso a ex trabajadores | Nadie (avisos) | Evidencia: fotografía fechada por lugar de publicación (D-01, D-06) o constancia de envío (D-11 Parte 1) |
| D-02, D-03, D-04, D-05, D-07, D-08, D-09, D-10, D-11 Parte 2, D-12, D-13 | Integrantes de la Comisión y, donde el texto lo indica, el representante legal, la mesa o el sindicato | `FIRMA_COMISION`, por documento (sección 8.1) |
| D-14 recibo individual | La persona trabajadora | `FIRMA_D14` (7.4) |

---

### 8.1 Firma de los documentos de la Comisión (`FIRMA_COMISION`, 21/11/2026)

Decisión del usuario: las actas y constancias de la Comisión se pueden firmar de forma electrónica o autógrafa.

1. `FIRMA_COMISION` se elige al generar cada documento (Electrónica · Autógrafa), sin valor por omisión.
2. Electrónica solo si todos los firmantes tienen usuario en la Plataforma. Si firma alguien externo (representante sindical, integrante de mesa sin usuario), la pantalla solo ofrece Autógrafa.
3. Con Electrónica: cada firmante firma con su tipo de firma (especificación de firma electrónica); la tabla de firmas imprime el sello de cada uno (`FIRMA_SELLO_*`; antes de firmar, «Pendiente de firma electrónica») y el documento cierra con `CLAUSULA_FIRMA_ELECTRONICA`. El documento queda firmado cuando firman todos.
4. Con Autógrafa: la tabla imprime la columna «Firma» en blanco y RH carga el escaneo; la casilla «documento firmado» basta para avanzar (regla 5.0).
5. Si un firmante rechaza la firma electrónica o falla la Plataforma, el documento se regenera como Autógrafa, con la misma fecha y contenido; la bitácora conserva la versión anterior.
6. Los avisos (D-01, D-06 y D-11 Parte 1) no se firman. D-14 sigue `FIRMA_D14` (7.4).

---

## 9. Plantillas

Texto vigente del modelo maestro (rev. 87). Las notas «Regla del sistema» que aparecen dentro de cada documento son instrucciones para el programador y no se imprimen.

### Fase 0 – Integración de la Comisión

Se genera una vez y se repite solo al renovar la Comisión completa. Por omisión, la representación obrera se acredita en D-03 con la manifestación de las personas designadas, sin exigir elección ni evidencias de ella. D-01 y D-02 son un módulo opcional para el cliente que decida celebrar una elección formal (DESIGNACION_OBRERA = Elección). Con SINDICATO = Sí, la representación obrera se acredita con el oficio sindical.


#### D-01. Aviso de convocatoria a la jornada de elección (módulo opcional)

[SI SINDICATO = No Y DESIGNACION_OBRERA = Elección]

**AVISO A LAS PERSONAS TRABAJADORAS DE {{RAZON_SOCIAL}}**

**Jornada de elección de representantes de las personas trabajadoras en la Comisión Mixta de Participación de los Trabajadores en las Utilidades**

Se convoca a las personas trabajadoras de {{RAZON_SOCIAL}} a elegir a sus representantes en la Comisión Mixta de Participación de los Trabajadores en las Utilidades.

1. **Qué se elige.** {{NUM_REPRESENTANTES_POR_PARTE}} representantes propietarios [SI REPRESENTANTES_SUPLENTES = Sí] y {{NUM_REPRESENTANTES_POR_PARTE}} suplentes [FIN SI]. Serán propietarios quienes obtengan más votos, [SI REPRESENTANTES_SUPLENTES = Sí] y suplentes quienes les sigan [FIN SI].
2. **Quién puede postularse.** Quien preste servicios en alguno de los centros de trabajo, no ocupe un puesto de confianza y no forme parte de la representación de la Empresa. El registro se hace ante {{CONTACTO_REGISTRO}} hasta el {{FECHA_LIMITE_REGISTRO}}, o ante la mesa antes de iniciar la votación.
3. **Quién vota.** Todas las personas trabajadoras que aparezcan en el padrón, incluido el personal de confianza. El padrón se publica junto con este aviso y puede corregirse ante la mesa el día de la elección.
4. **Cuándo y dónde.** Una mesa por turno o centro: {{TABLA_MESAS}} (turno o centro, fecha, horario y lugar).
5. **Cómo se vota.** En forma personal y libre, de la manera que acuerden las personas asistentes (a mano alzada, por lista firmada o por boleta). No se requiere voto secreto. La mesa de elección la integran personas trabajadoras elegidas por quienes asistan; la Empresa solo facilita el espacio y los materiales y no interviene en la votación ni en el cómputo.
6. **Validez.** La elección es válida si vota al menos la mitad más una de las personas del padrón. Si no se alcanza, se celebrará una segunda jornada dentro de los 10 días hábiles siguientes, válida con cualquier participación.
7. **Resultados.** Se publicarán en los mismos lugares que este aviso a más tardar el día hábil siguiente al cierre.

Este aviso permanece publicado del {{FECHA_INICIO_PUBLICACION}} al {{FECHA_ELECCION}} en {{LUGARES_PUBLICACION}} y en {{MEDIO_DIGITAL}}.

{{MUNICIPIO_ESTADO}}, a {{FECHA_AVISO}}. {{RAZON_SOCIAL}}.

[FIN SI]

> **Regla del sistema.** FECHA_INICIO_PUBLICACION ≤ FECHA_ELECCION − 5 días hábiles, en cada centro y por medio digital.


#### D-02. Constancia de publicación y acta de la jornada de elección (módulo opcional)

[SI SINDICATO = No Y DESIGNACION_OBRERA = Elección]

**Parte 1. Constancia de publicación**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_CONSTANCIA}}, {{PERSONA_QUE_PUBLICO}}, {{PUESTO_PERSONA_QUE_PUBLICO}}, y la persona trabajadora {{TESTIGO_1}}, como testigo, hacen constar:

**PRIMERO.** El aviso de convocatoria de fecha {{FECHA_AVISO}} se fijó el {{FECHA_INICIO_PUBLICACION}} en {{LUGARES_PUBLICACION}} y se difundió por {{MEDIO_DIGITAL}}, junto con el padrón.

**SEGUNDO.** El aviso permaneció visible hasta el {{FECHA_ELECCION}}. [SI INCIDENCIA_PUBLICACION = Sí] Se registró la siguiente incidencia y la forma en que se subsanó: {{DESCRIPCION_INCIDENCIA}}. [FIN SI]

**TERCERO.** Se agregan como Anexo 1 las fotografías fechadas de cada lugar de publicación y la captura de la difusión digital.

| Nombre | Carácter | Firma |
| --- | --- | --- |
| {{PERSONA_QUE_PUBLICO}} | Persona que publicó |  |
| {{TESTIGO_1}} | Testigo |  |

**Parte 2. Acta de la jornada de elección**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_ELECCION}}, se celebró la jornada de elección convocada el {{FECHA_AVISO}}, conforme a lo siguiente:

**PRIMERO. Mesa.** Las personas trabajadoras asistentes eligieron a {{PRESIDENTE_MESA}}, {{SECRETARIO_MESA}} y {{ESCRUTADOR_MESA}} como integrantes de la mesa de elección. [SI TURNOS_MESAS > 1] Se instalaron las mesas por turno o centro que constan en el Anexo 2, cada una con su propia hoja de cómputo. [FIN SI] La Empresa se limitó a facilitar el lugar y los materiales.

**SEGUNDO. Participación.** Votaron {{NUM_VOTANTES}} de las {{NUM_PADRON}} personas del padrón ({{PORC_PARTICIPACION}} %). [SI PORC_PARTICIPACION > 50] La elección es válida. [FIN SI] [SI PORC_PARTICIPACION <= 50 Y JORNADA = Primera] No se alcanzó la participación mínima; se convoca a segunda jornada para el {{FECHA_SEGUNDA_JORNADA}}. [FIN SI] [SI JORNADA = Segunda] La elección es válida por tratarse de la segunda jornada. [FIN SI]

**TERCERO. Resultados.** El cómputo fue el siguiente:

| Candidatura | Votos |
| --- | --- |
| {{CANDIDATURA}} | {{VOTOS}} |

Votos nulos: {{VOTOS_NULOS}}. [SI EMPATE = Sí] El empate entre {{CANDIDATURAS_EMPATADAS}} se resolvió mediante {{MECANISMO_DESEMPATE}}, acordado por la mesa antes del cómputo. [FIN SI]

**CUARTO. Personas electas.**

| Propietarios | Suplentes, en orden de prelación |
| --- | --- |
| {{REP_TRAB_PROPIETARIOS}} | [SI REPRESENTANTES_SUPLENTES = Sí] {{REP_TRAB_SUPLENTES}} [FIN SI] |

La mesa verificó que ninguna persona electa ocupa un puesto de confianza ni forma parte de la representación de la Empresa.

| Nombre | Cargo en la mesa | Firma |
| --- | --- | --- |
| {{PRESIDENTE_MESA}} | Presidencia |  |
| {{SECRETARIO_MESA}} | Secretaría |  |
| {{ESCRUTADOR_MESA}} | Escrutinio |  |

**Anexos:** 1. Fotografías y difusión digital · 2. Padrón firmado por mesa · 3. Hojas de cómputo.

[FIN SI]


#### D-03. Acta de integración y estatutos de la Comisión

**ACTA DE INTEGRACIÓN Y ESTATUTOS DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}}**

**Datos de la Empresa:** {{RAZON_SOCIAL}} · RFC {{RFC}} · Registro patronal {{REGISTRO_PATRONAL}} · Centro de trabajo: {{DOMICILIO_CENTRO}}.

En {{MUNICIPIO_ESTADO}}, el {{FECHA_ACTA}}, en {{DOMICILIO_CENTRO}}, se hace constar la integración de la Comisión Mixta de Participación de los Trabajadores en las Utilidades (la «Comisión»), con fundamento en el artículo 123, apartado A, fracción IX, de la Constitución Política de los Estados Unidos Mexicanos y en los artículos 117 a 131 de la Ley Federal del Trabajo.


##### Primera parte. Integración

**PRIMERO. Representación de las personas trabajadoras.**

[SI SINDICATO = No] Las personas trabajadoras designaron como sus representantes propietarios a {{REP_TRAB_PROPIETARIOS}} [SI REPRESENTANTES_SUPLENTES = Sí] y como suplentes a {{REP_TRAB_SUPLENTES}}, en ese orden de prelación [FIN SI]. Estas personas manifiestan que fueron designadas por sus compañeras y compañeros de trabajo y aceptan la representación. La Empresa no intervino en su designación. [SI DESIGNACION_OBRERA = Elección] La designación consta en el acta de la jornada de elección de fecha {{FECHA_ELECCION}} (Anexo 1). [FIN SI] [SI CONFORMIDAD_FIRMAS = Sí] Se agrega como Anexo 1 la relación de personas trabajadoras que manifiestan su conformidad con la designación. [FIN SI] [FIN SI]

[SI SINDICATO = Sí] Mediante oficio de fecha {{FECHA_OFICIO_SINDICATO}} (Anexo 1), {{SINDICATO_NOMBRE}}, titular del contrato colectivo de trabajo, por conducto de {{SINDICATO_REPRESENTANTE}}, designó como propietarios a {{REP_TRAB_PROPIETARIOS}} y como suplentes a {{REP_TRAB_SUPLENTES}}. [FIN SI]

Se verificó que ninguna de estas personas ocupa un puesto de confianza.

**SEGUNDO. Representación de la Empresa.** Mediante nombramiento escrito de {{REPRESENTANTE_LEGAL}} (Anexo 2), la Empresa designa como propietarios a {{REP_EMPRESA_PROPIETARIOS}} y como suplentes a {{REP_EMPRESA_SUPLENTES}}. Esta designación corresponde exclusivamente a la Empresa y no se somete a votación.

**TERCERO. Aceptación.** Las personas designadas aceptan el cargo y se obligan a desempeñarlo conforme a la Ley Federal del Trabajo y a estos estatutos.

**CUARTO. Cargos internos.** {{COORDINADOR}}, de la representación de la Empresa, es Coordinador. {{SECRETARIO}}, de la representación de las personas trabajadoras, es Secretario.

**QUINTO. Integración resultante.**

| Representación | Propietario | Suplente | Cargo |
| --- | --- | --- | --- |
| Empresa | {{REP_EMPRESA_PROPIETARIOS}} | {{REP_EMPRESA_SUPLENTES}} | Coordinador (uno) |
| Personas trabajadoras | {{REP_TRAB_PROPIETARIOS}} | {{REP_TRAB_SUPLENTES}} | Secretario (uno) |


##### Segunda parte. Estatutos

**Artículo 1. Objeto.** La Comisión tiene por objeto:

a) formular el proyecto que determine la participación individual de cada persona trabajadora y fijarlo en lugar visible del establecimiento (art. 125, fr. I, LFT);

b) recibir las observaciones de las personas trabajadoras al proyecto y resolverlas dentro de los quince días siguientes al vencimiento del plazo para formularlas (art. 125, frs. III y IV, LFT); y

c) servir de canal operativo para la entrega de la copia de la declaración anual, conforme al artículo 5.

**Artículo 2. Límites.** La Comisión no determina ni modifica la renta gravable, que resulta de la declaración anual de la Empresa. No formula objeciones ante la autoridad fiscal: ese derecho corresponde al sindicato titular del contrato colectivo o a la mayoría de las personas trabajadoras. Su integración no otorga facultades de intervención en la dirección o administración de la Empresa (art. 131 LFT).

**Artículo 3. Vigencia y sustitución.** La Comisión opera por tiempo indefinido para los ejercicios sucesivos. Una persona integrante deja el cargo por:

a) terminación de su relación de trabajo;

b) renuncia escrita al cargo;

c) en la representación de las personas trabajadoras, su promoción a un puesto de confianza;

d) revocación por quien la designó, notificada por escrito a la Comisión; o

e) ausencia injustificada a dos sesiones consecutivas.

La vacante la cubre el suplente según su orden de prelación (D-13). Sin suplentes, quien designó al integrante designa a otro dentro de 10 días hábiles; en la representación de las personas trabajadoras, las personas trabajadoras designan a otra persona o el sindicato emite nueva designación.

**Artículo 4. Cargos internos.** El Coordinador convoca, conduce las sesiones y custodia el expediente. El Secretario levanta las actas, lleva el registro de observaciones y recibe los escritos dirigidos a la Comisión. El Secretario puede suplir al Coordinador solo para convocar y conducir una sesión, sin cambiar su titularidad.

**Artículo 5. Entrega de la declaración anual.** La Empresa entrega la copia de la declaración anual y pone a disposición sus anexos en sesión de la Comisión. [SI SINDICATO = Sí] La recibe el representante del sindicato titular, quien es convocado a esa sesión. [FIN SI] [SI SINDICATO = No] La reciben los representantes de las personas trabajadoras en su carácter de representantes de la mayoría, y la Empresa lo hace del conocimiento de toda la plantilla mediante aviso. [FIN SI]

**Artículo 6. Sesiones.** La Comisión celebra, por lo menos, las sesiones de entrega de la declaración, formulación del proyecto y, en su caso, resolución de observaciones. Puede celebrar sesiones extraordinarias a solicitud de cualquier integrante. La convocatoria se notifica por escrito o por medio electrónico con al menos 3 días hábiles de anticipación, salvo que asistan todos los integrantes.

**Artículo 7. Quórum y acuerdos.** La sesión se instala con la mitad más uno de los propietarios y al menos uno de cada representación. Un acuerdo es válido con la mayoría de cada representación, sin voto de calidad.

**Artículo 8. Desacuerdo.** Si las representaciones no se ponen de acuerdo sobre el proyecto o sobre una observación, el acta registra la postura y los cálculos de cada una. Dentro de los 3 días hábiles siguientes, el Coordinador o cualquier integrante somete el desacuerdo al Inspector del Trabajo de {{AUTORIDAD_INSPECCION}}, cuya decisión se incorpora al proyecto (art. 125, fr. II, LFT).

**Artículo 9. Información.** La Empresa pone a disposición de la Comisión las listas de asistencia y de raya y los demás elementos de que disponga (art. 125, fr. I, LFT) dentro de los 5 días hábiles siguientes a la solicitud. Si no los entrega, la Comisión lo hace constar en acta.

**Artículo 10. Confidencialidad.** Los datos de la declaración anual y sus anexos son de carácter fiscal y no pueden darse a conocer a terceros (art. 121, fr. I, LFT). La información de nómina contiene datos personales: las personas integrantes solo la usan para los fines de la Comisión y la devuelven o destruyen al concluir cada ejercicio, salvo la que forme parte del expediente.

**Artículo 11. Expediente.** Las actas, dictámenes, constancias y escritos se integran en un expediente con folio consecutivo, físico o electrónico, bajo custodia del Coordinador en el domicilio del centro de trabajo. Todas las personas integrantes tienen acceso a él.

**Artículo 12. Publicaciones.** Las publicaciones de la Comisión se fijan en {{LUGARES_PUBLICACION}}. De cada una se deja constancia firmada con fotografías fechadas.

**Artículo 13. Observaciones.** Las observaciones al proyecto se presentan por escrito o en el formato que la Comisión ponga a disposición, ante el Secretario, quien entrega acuse. Deben señalar el nombre de la persona trabajadora, el dato que objeta y la razón. La resolución se notifica por escrito a quien la formuló.

**Artículo 14. Resoluciones fuera de sesión.** Son válidas si constan por escrito firmado por todas las personas integrantes propietarias.

**Artículo 15. Tiempo de trabajo.** El tiempo dedicado a las sesiones y actividades de la Comisión es tiempo de trabajo con goce de salario.

**Artículo 16. No represalia.** Ninguna persona integrante es objeto de medida disciplinaria o trato desfavorable por las opiniones o votos que emita en la Comisión.

**Artículo 17. Reforma.** Estos estatutos solo se reforman por acuerdo de ambas representaciones, en sesión cuya convocatoria lo señale.

Se cierra el acta el {{FECHA_ACTA}} a las {{HORA_CIERRE}} horas.

| Nombre | Representación y cargo | Firma |
| --- | --- | --- |
| {{COORDINADOR}} | Empresa · Coordinador |  |
| {{REP_EMPRESA_PROPIETARIOS}} | Empresa |  |
| {{SECRETARIO}} | Personas trabajadoras · Secretario |  |
| {{REP_TRAB_PROPIETARIOS}} | Personas trabajadoras |  |
| {{REPRESENTANTE_LEGAL}} | Representante legal de la Empresa |  |

**Anexos:** 1. Según el caso y si existen: oficio sindical, acta de la jornada de elección (D-02) o relación de conformidad · 2. Nombramiento de la representación de la Empresa · 3. Identificaciones.


### Fase 1 – Declaración anual

Se genera cada ejercicio dentro de los 10 días hábiles siguientes a FECHA_PRESENTACION. El sistema alerta si la fecha de la sesión excede ese plazo.


#### D-04. Convocatoria a sesión de la Comisión (plantilla única)

**CONVOCATORIA A SESIÓN {{TIPO_SESION}} DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}}**

{{COORDINADOR}}, Coordinador de la Comisión, con fundamento en el artículo 6 de sus estatutos, convoca a sus integrantes {{INTEGRANTES_CONVOCADOS}} a sesión el {{FECHA_SESION}} a las {{HORA_SESION}} horas, en {{LUGAR_SESION}}, con el siguiente orden del día:

1. Verificación de quórum.
2. {{ASUNTO_SESION}}: entrega de la declaración anual del ejercicio {{EJERCICIO}} / formulación del proyecto de participación del ejercicio {{EJERCICIO}} / resolución de observaciones al proyecto / {{ASUNTO_EXTRAORDINARIO}}.
3. Acuerdos y cierre.

[SI ASISTENTES_EXTERNOS = Sí] Se cita también, sin derecho a voto, a {{ASISTENTES_EXTERNOS_LISTA}}. [FIN SI]

[SI DOCUMENTOS_REQUERIDOS = Sí] Se solicita a la Empresa presentar en la sesión: {{LISTA_DOCUMENTOS}}. [FIN SI]

{{MUNICIPIO_ESTADO}}, a {{FECHA_CONVOCATORIA}}. {{COORDINADOR}}, Coordinador.

| Integrante | Medio y fecha de notificación | Firma de recibido |
| --- | --- | --- |
| {{INTEGRANTE}} |  |  |


#### D-05. Acta de entrega de la declaración anual y puesta a disposición de anexos

**ACTA DE SESIÓN ORDINARIA DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}} · ENTREGA DE LA DECLARACIÓN ANUAL DEL EJERCICIO {{EJERCICIO}}**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_SESION}}, a las {{HORA_SESION}} horas, en {{LUGAR_SESION}}, conforme a la convocatoria de fecha {{FECHA_CONVOCATORIA}}, se reunieron las personas integrantes de la Comisión que firman al final. Asiste también {{REPRESENTANTE_LEGAL}}, en representación de la Empresa. [SI SINDICATO = Sí] Asiste {{SINDICATO_REPRESENTANTE}}, en representación de {{SINDICATO_NOMBRE}}. [FIN SI]

**PRIMERO. Quórum.** Asisten {{NUM_ASISTENTES_EMPRESA}} integrantes de la representación de la Empresa y {{NUM_ASISTENTES_TRAB}} de la representación de las personas trabajadoras; la sesión queda instalada conforme al artículo 7 de los estatutos.

**SEGUNDO. Datos de la declaración.** La Empresa informa que presentó ante el Servicio de Administración Tributaria la declaración anual del impuesto sobre la renta del ejercicio {{EJERCICIO}} el {{FECHA_PRESENTACION}}, con número de operación {{NUM_OPERACION}}. [SI COMPLEMENTARIA = Sí] Presentó también declaración complementaria el {{FECHA_COMPLEMENTARIA}}, con número de operación {{NUM_OPERACION_COMPLEMENTARIA}}, que sustituye a la anterior para efectos de este procedimiento. [FIN SI]

**TERCERO. Entrega de la copia.** En este acto, la Empresa entrega copia de la declaración y de su acuse de recibo [SI SINDICATO = Sí] a {{SINDICATO_REPRESENTANTE}}, en representación de {{SINDICATO_NOMBRE}}, titular del contrato colectivo de trabajo [FIN SI] [SI SINDICATO = No] a {{REP_TRAB_PROPIETARIOS}}, en su carácter de representantes electos por la mayoría de las personas trabajadoras [FIN SI], quienes la reciben y firman de recibido. La copia consta de {{NUM_FOJAS}} fojas; un tanto con firma de recibido se agrega como Anexo 1 y el acuse del SAT como Anexo 2.

**CUARTO. Oportunidad de la entrega.** Entre la fecha de presentación y la de esta sesión transcurrieron {{DIAS_HABILES_TRANSCURRIDOS}} días hábiles. [SI DIAS_HABILES_TRANSCURRIDOS > 10] La entrega se realiza fuera del plazo de diez días hábiles, por lo que los plazos de consulta y de objeción se computan a partir de esta fecha. [FIN SI]

**QUINTO. Anexos a disposición.** Los anexos de la declaración quedan a disposición en {{LUGAR_CONSULTA}}, en horario de {{HORARIO_CONSULTA}}, del {{FECHA_SESION}} al {{FECHA_FIN_CONSULTA}} (30 días hábiles), así como en la oficina del SAT en la que se presentó o se encuentra la declaración. Las consultas se registran en la bitácora del Anexo 3.

**SEXTO. Información de derechos.** A más tardar el {{FECHA_LIMITE_OBJECIONES}}, [SI SINDICATO = Sí] el sindicato titular [FIN SI] [SI SINDICATO = No] la mayoría de las personas trabajadoras [FIN SI] puede formular ante el SAT las objeciones que juzgue convenientes a la declaración. Este derecho no corresponde a la Comisión como órgano. La presentación de objeciones no suspende el pago de la participación que, en su caso, resulte.

**SÉPTIMO. Confidencialidad.** Quienes reciben la copia quedan advertidos de que los datos de la declaración y sus anexos son de carácter fiscal y no pueden darse a conocer a terceras personas, conforme al artículo 121, fracción I, de la Ley Federal del Trabajo.

**OCTAVO. Aviso a la plantilla.** La Empresa publica el aviso de consulta (D-06) en {{LUGARES_PUBLICACION}} a más tardar el día hábil siguiente.

**NOVENO. Alcance.** La recepción de la copia no implica conformidad con su contenido ni revisión de sus cifras.

[SI MANIFESTACIONES = Sí] **DÉCIMO. Manifestaciones.** {{MANIFESTACIONES_ASISTENTES}} [FIN SI]

Se cierra el acta a las {{HORA_CIERRE}} horas del mismo día.

| Nombre | Carácter | Firma |
| --- | --- | --- |
| {{COORDINADOR}} | Representación de la Empresa · Coordinador |  |
| {{REP_EMPRESA_PROPIETARIOS}} | Representación de la Empresa |  |
| {{SECRETARIO}} | Representación de las personas trabajadoras · Secretario |  |
| {{REP_TRAB_PROPIETARIOS}} | Representación de las personas trabajadoras |  |
| {{REPRESENTANTE_LEGAL}} | Por la Empresa, quien entrega |  |
| [SI SINDICATO = Sí] {{SINDICATO_REPRESENTANTE}} [FIN SI] | Por el sindicato, quien recibe |  |

**Anexos:** 1. Copia de la declaración con firma de recibido · 2. Acuse del SAT · 3. Bitácora de consulta (fecha, nombre, hora de entrada y salida, firma).


#### D-06. Aviso de consulta de la declaración anual

**AVISO A LAS PERSONAS TRABAJADORAS DE {{RAZON_SOCIAL}} · DECLARACIÓN ANUAL DEL EJERCICIO {{EJERCICIO}}**

El {{FECHA_SESION}} la Empresa entregó copia de su declaración anual del ejercicio {{EJERCICIO}} [SI SINDICATO = Sí] al sindicato {{SINDICATO_NOMBRE}} [FIN SI] [SI SINDICATO = No] a los representantes de las personas trabajadoras en la Comisión Mixta de Participación de los Trabajadores en las Utilidades, {{REP_TRAB_PROPIETARIOS}} [FIN SI].

1. **Consulta de anexos.** En {{LUGAR_CONSULTA}}, en horario de {{HORARIO_CONSULTA}}, hasta el {{FECHA_FIN_CONSULTA}}. No se permite fotografiar ni copiar los anexos.
2. **Objeciones.** [SI SINDICATO = Sí] El sindicato titular [FIN SI] [SI SINDICATO = No] La mayoría de las personas trabajadoras [FIN SI] puede presentar objeciones ante el SAT a más tardar el {{FECHA_LIMITE_OBJECIONES}}. Para dudas, acudir con {{SECRETARIO}}.
3. **Confidencialidad.** Los datos de la declaración son de carácter fiscal y no pueden darse a conocer a terceras personas.
4. **Siguiente paso.** La Comisión publicará el proyecto de participación a más tardar el {{FECHA_PUBLICACION_PROYECTO}}.

Publicado el {{FECHA_PUBLICACION_AVISO}} en {{LUGARES_PUBLICACION}}.

> **Regla del sistema.** El aviso no lleva firmas; su prueba es la fotografía fechada en cada lugar de publicación, que se integra al expediente.


### Fase 2 – Proyecto de participación

La convocatoria se genera con D-04 (asunto: formulación del proyecto). El dictamen D-08 se genera con un solo módulo según RESULTADO. Con RESULTADO = B, el sistema no genera D-08 mientras el reporte de validación de los datos por persona tenga errores (ver reglas del sistema).


#### D-07. Acta de sesión de formulación del proyecto

**ACTA DE SESIÓN ORDINARIA DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}} · FORMULACIÓN DEL PROYECTO DEL EJERCICIO {{EJERCICIO}}**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_SESION}}, a las {{HORA_SESION}} horas, en {{LUGAR_SESION}}, conforme a la convocatoria de fecha {{FECHA_CONVOCATORIA}}, se reunieron las personas integrantes de la Comisión que firman al final. Asisten, sin derecho a voto, {{REPRESENTANTE_LEGAL}} y {{RESPONSABLE_INFORMACION}}, {{PUESTO_RESPONSABLE_INFORMACION}}.

**PRIMERO. Quórum.** Asisten {{NUM_ASISTENTES_EMPRESA}} integrantes de la representación de la Empresa y {{NUM_ASISTENTES_TRAB}} de la representación de las personas trabajadoras; la sesión queda instalada.

**SEGUNDO. Documentos.** La Empresa pone a disposición de la Comisión los documentos que se relacionan en el Anexo 1:

- La declaración anual del ejercicio {{EJERCICIO}} y su acuse, entregados en sesión de {{FECHA_SESION_ENTREGA}}.
- [SI RESULTADO = B] La relación por persona de días trabajados y salario devengado en el ejercicio, obtenida [SI VIA_CALCULO = Automático] del cálculo automático del sistema, confirmado por {{RESPONSABLE_CAPTURA}} el {{FECHA_CONFIRMACION_CALCULO}} [FIN SI] [SI VIA_CALCULO = Importación] de la nómina importada al sistema el {{FECHA_IMPORTACION}} [FIN SI] [SI VIA_CALCULO = Captura] de la captura realizada por {{RESPONSABLE_CAPTURA}} el {{FECHA_CAPTURA}} [FIN SI], con su reporte de validación; las listas de raya o nóminas y de asistencia que la respaldan; las constancias de incapacidades por riesgo de trabajo y por maternidad; la relación de personas de confianza con su salario; y la relación de personas que dejaron de prestar servicios durante el ejercicio, con su último domicilio y medio de contacto. [FIN SI]
- [SI RESULTADO = C] El documento que acredita la causa de excepción: {{DOCUMENTO_EXCEPCION}}. [FIN SI]

[SI DOCUMENTOS_FALTANTES = Sí] No se entregaron los siguientes documentos solicitados: {{DOCUMENTOS_FALTANTES_LISTA}}. La Empresa se compromete a entregarlos el {{FECHA_ENTREGA_FALTANTES}}. [FIN SI]

**TERCERO. Exposición de la base.** {{RESPONSABLE_INFORMACION}} expone que la renta gravable del ejercicio {{EJERCICIO}} para efectos de la participación, determinada conforme al artículo 9 de la Ley del Impuesto sobre la Renta, es de {{RENTA_GRAVABLE_PTU}}, y responde las preguntas de las personas integrantes. [SI PREGUNTAS_RELEVANTES = Sí] Se registran las siguientes preguntas y respuestas: {{PREGUNTAS_Y_RESPUESTAS}}. [FIN SI]

**CUARTO. Formulación del proyecto.** Analizados los documentos, la Comisión: [SI ACUERDO = Sí] aprueba por mayoría de cada representación el dictamen que se agrega como Anexo 2, en su versión completa y en su versión publicable, y acuerda publicar esta última el {{FECHA_PUBLICACION}} en {{LUGARES_PUBLICACION}}. [FIN SI] [SI ACUERDO = No] no alcanza acuerdo. La representación de la Empresa sostiene: {{POSTURA_EMPRESA}}. La representación de las personas trabajadoras sostiene: {{POSTURA_TRABAJADORES}}. Conforme al artículo 8 de los estatutos, el desacuerdo se somete al Inspector del Trabajo a más tardar el {{FECHA_LIMITE_INSPECTOR}}. [FIN SI]

**QUINTO. Expediente.** Esta acta y sus anexos se integran al expediente con el folio {{FOLIO}}.

Se cierra el acta a las {{HORA_CIERRE}} horas del mismo día.

| Nombre | Carácter | Firma |
| --- | --- | --- |
| {{COORDINADOR}} | Representación de la Empresa · Coordinador |  |
| {{REP_EMPRESA_PROPIETARIOS}} | Representación de la Empresa |  |
| {{SECRETARIO}} | Representación de las personas trabajadoras · Secretario |  |
| {{REP_TRAB_PROPIETARIOS}} | Representación de las personas trabajadoras |  |

**Anexos:** 1. Relación de documentos recibidos y reporte de validación · 2. Dictamen (D-08), versión completa y publicable.


#### D-08. Dictamen de participación de las personas trabajadoras en las utilidades

**DICTAMEN DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}} · EJERCICIO {{EJERCICIO}}**

La Comisión, integrada por {{REP_EMPRESA_PROPIETARIOS}}, por la representación de la Empresa, y por {{REP_TRAB_PROPIETARIOS}}, por la representación de las personas trabajadoras, con fundamento en el artículo 125 de la Ley Federal del Trabajo, emite el siguiente dictamen, aprobado en sesión de {{FECHA_SESION}}.

**PRIMERO. Base de la participación.** De la declaración anual del impuesto sobre la renta del ejercicio {{EJERCICIO}}, presentada ante el SAT el {{FECHA_PRESENTACION}} con número de operación {{NUM_OPERACION}} [SI COMPLEMENTARIA = Sí], conforme a la declaración complementaria de {{FECHA_COMPLEMENTARIA}} [FIN SI], se desprende que la renta gravable determinada conforme al artículo 9 de la Ley del Impuesto sobre la Renta, sin disminuir la participación pagada en el ejercicio ni las pérdidas fiscales pendientes de aplicar de ejercicios anteriores, es de {{RENTA_GRAVABLE_PTU}}.


##### Módulo A – Sin cantidad repartible

[SI RESULTADO = A]

**SEGUNDO. Inexistencia de cantidad repartible.** La renta gravable es igual a cero [SI RENTA_GRAVABLE_PTU < 0] o el ejercicio arrojó pérdida fiscal [FIN SI]; por tanto, no existe cantidad a repartir en términos del artículo 120 de la Ley Federal del Trabajo. La participación individual de cada persona trabajadora, incluidas las que dejaron de prestar servicios durante el ejercicio, es de $0.00.

**TERCERO. Reserva.** Este dictamen se emite sin perjuicio del reparto que proceda si la Empresa presenta declaración complementaria que modifique la renta gravable, o si la autoridad fiscal determina una renta gravable mayor. En esos supuestos la Comisión sesiona conforme a D-12.

[FIN SI]


##### Módulo B – Con reparto

[SI RESULTADO = B]

**SEGUNDO. Cantidad a repartir.** Aplicando a la renta gravable el porcentaje de {{PORCENTAJE_PTU}} fijado por la Comisión Nacional para la Participación de los Trabajadores en las Utilidades de las Empresas, la cantidad a repartir es de {{UTILIDAD_REPARTIBLE}}. [SI MONTO_NO_RECLAMADO_ANTERIOR > 0] Se adicionan {{MONTO_NO_RECLAMADO_ANTERIOR}} de utilidades no reclamadas del ejercicio {{EJERCICIO_ANTERIOR}}, conforme al artículo 122 de la Ley Federal del Trabajo, para un total de {{TOTAL_A_REPARTIR}}. [FIN SI]

**TERCERO. Personas con derecho.** Participan las personas trabajadoras que prestaron servicios durante el ejercicio, incluidas las que ya no laboran para la Empresa, con las siguientes reglas del artículo 127 de la Ley Federal del Trabajo:

a) No participan quienes ocuparon puestos de dirección, administración o gerencia general (PTU_EXCLUIDO = Sí): {{LISTA_EXCLUIDOS_DIRECCION}}.

b) El personal de confianza participa; si su salario excede el del trabajador sindicalizado de más alto salario o, a falta de este, el del trabajador de planta de más alto salario, se toma ese salario aumentado en 20 % como máximo. Salario de referencia: {{SALARIO_REFERENCIA}}; salario máximo aplicable: {{SALARIO_MAXIMO_CONFIANZA}}.

c) Las personas eventuales participan si trabajaron al menos 60 días durante el ejercicio.

d) Se consideran en servicio activo las trabajadoras durante los periodos pre y postnatales y las personas trabajadoras durante la incapacidad temporal por riesgo de trabajo. Se computan también como días trabajados las vacaciones y los permisos con goce de salario.

e) [SI TRABAJO_HOGAR = Sí] No participan las personas trabajadoras del hogar. [FIN SI]

**CUARTO. Determinación individual.** Con los días trabajados y el salario devengado de cada persona, [SI VIA_CALCULO = Automático] calculados por el sistema con los registros de la Empresa [FIN SI] [SI VIA_CALCULO = Importación] tomados de la nómina importada [FIN SI] [SI VIA_CALCULO = Captura] capturados por persona [FIN SI], la cantidad a repartir se divide en dos partes iguales (art. 123 LFT):

a) la primera, por igual entre las personas con derecho, en proporción a los días trabajados por cada una, con independencia de su salario. Factor por día: {{FACTOR_DIAS}};

b) la segunda, en proporción al monto de los salarios devengados por cada una durante el ejercicio. Se considera salario la cantidad que recibe en efectivo por cuota diaria, sin incluir gratificaciones, percepciones y demás prestaciones, ni las sumas por tiempo extraordinario; en salario variable, se toma el promedio de las percepciones del ejercicio (art. 124 LFT). Factor por peso de salario: {{FACTOR_SALARIOS}}.

**QUINTO. Límite individual.** La participación de cada persona no excede el mayor de: tres meses de su salario o el promedio de la participación recibida en los últimos tres años (art. 127, fr. VIII, LFT). [SI MONTO_EXCEDENTE > 0] La cantidad que excede el límite de cada persona, que en conjunto asciende a {{MONTO_EXCEDENTE}}, no forma parte de la participación, no se redistribuye entre las demás personas trabajadoras ni se agrega a la utilidad repartible de ejercicios posteriores. [FIN SI]

**SEXTO. Resultado individual.** La participación de cada persona consta en el Anexo 1 en dos versiones:

a) **Versión completa:** nombre, situación (activa o baja y fecha), días computables, salario computado, participación por días, participación por salarios, límite aplicable y participación final. Queda a disposición de la Comisión y de cada persona respecto de sus propios datos, ante el Secretario.

b) **Versión publicable:** nombre, días computables y monto de la participación. Es la única que se fija en los lugares de publicación.

**SÉPTIMO. Pago.** La Empresa paga la participación a más tardar el {{FECHA_LIMITE_PAGO}}, mediante {{FORMA_PAGO}}, con las retenciones y deducciones que resulten del precálculo validado (R-5) y con el recibo individual (D-14). La presentación de objeciones ante el SAT no suspende el pago.

**OCTAVO. Personas que ya no laboran.** El listado de personas que dejaron de prestar servicios y tienen derecho a participación se publica con este dictamen, en su versión publicable, y se les da aviso conforme a D-11. Pueden cobrar en {{LUGAR_PAGO_EX}}, en horario de {{HORARIO_PAGO_EX}}. Las cantidades no reclamadas en el año en que sean exigibles se agregan a la utilidad repartible del año siguiente.

[FIN SI]


##### Módulo C – Excepción legal

[SI RESULTADO = C]

**SEGUNDO. Excepción.** La Empresa se ubica en el supuesto del artículo 126, fracción {{FRACCION_126}}, de la Ley Federal del Trabajo, porque {{HECHO_EXCEPCION}}, lo que se acredita con {{DOCUMENTO_EXCEPCION}}, que se agrega como Anexo 1. En consecuencia, no está obligada al reparto respecto del ejercicio {{EJERCICIO}}.

**TERCERO. Vigencia de la excepción.** La excepción concluye el {{FECHA_FIN_EXCEPCION}}; a partir del ejercicio siguiente el reparto se determina conforme a las reglas generales.

[FIN SI]


##### Puntos comunes

**PUBLICACIÓN.** Este dictamen se fija [SI RESULTADO = B] en su versión publicable [FIN SI] el {{FECHA_PUBLICACION}} en {{LUGARES_PUBLICACION}} y permanece publicado hasta el {{FECHA_FIN_OBSERVACIONES}}.

**OBSERVACIONES.** Las personas trabajadoras pueden formular observaciones por escrito ante {{SECRETARIO}}, Secretario de la Comisión, a más tardar el {{FECHA_FIN_OBSERVACIONES}}. La Comisión las resuelve a más tardar el {{FECHA_LIMITE_RESOLUCION}}.

| Nombre | Representación | Firma |
| --- | --- | --- |
| {{COORDINADOR}} | Empresa · Coordinador |  |
| {{REP_EMPRESA_PROPIETARIOS}} | Empresa |  |
| {{SECRETARIO}} | Personas trabajadoras · Secretario |  |
| {{REP_TRAB_PROPIETARIOS}} | Personas trabajadoras |  |


### Fase 3 – Observaciones al proyecto

D-09 se genera siempre al vencer el periodo de observaciones. D-10 solo con OBJECIONES = Sí y debe firmarse a más tardar el {{FECHA_LIMITE_RESOLUCION}}.


#### D-09. Constancia de publicación del dictamen y cierre del periodo de observaciones

**CONSTANCIA DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}} · PUBLICACIÓN DEL DICTAMEN DEL EJERCICIO {{EJERCICIO}}**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_CONSTANCIA}}, las personas integrantes de la Comisión que firman al final hacen constar:

**PRIMERO. Publicación.** El dictamen aprobado en sesión de {{FECHA_SESION_DICTAMEN}} se fijó [SI RESULTADO = B] en su versión publicable [FIN SI] el {{FECHA_PUBLICACION}} en {{LUGARES_PUBLICACION}} y permaneció visible hasta el {{FECHA_FIN_OBSERVACIONES}}. [SI EX_TRABAJADORES = Sí] En los mismos lugares se publicó el listado de personas que dejaron de prestar servicios con derecho a participación. [FIN SI] Se agregan como Anexo 1 las fotografías fechadas al fijarlo y al retirarlo.

[SI INCIDENCIA_PUBLICACION = Sí] Se registró la siguiente incidencia y la forma en que se subsanó: {{DESCRIPCION_INCIDENCIA}}. [FIN SI]

**SEGUNDO. Observaciones recibidas.** [SI OBJECIONES = No] Durante el periodo no se recibió ninguna observación por escrito ni en el formato puesto a disposición, según el registro del Secretario. El dictamen queda firme en sus términos. [FIN SI] [SI OBJECIONES = Sí] Durante el periodo se recibieron {{NUM_OBSERVACIONES}} observaciones, relacionadas en el Anexo 2 con su folio y fecha de recepción. Se resuelven conforme a D-10 a más tardar el {{FECHA_LIMITE_RESOLUCION}}. [FIN SI]

**TERCERO. Alcance.** Esta constancia se refiere exclusivamente a las observaciones al proyecto previstas en el artículo 125 de la Ley Federal del Trabajo. No se pronuncia sobre las objeciones a la declaración anual que, en su caso, se presenten ante el SAT.

| Nombre | Representación | Firma |
| --- | --- | --- |
| {{COORDINADOR}} | Empresa · Coordinador |  |
| {{REP_EMPRESA_PROPIETARIOS}} | Empresa |  |
| {{SECRETARIO}} | Personas trabajadoras · Secretario |  |
| {{REP_TRAB_PROPIETARIOS}} | Personas trabajadoras |  |

**Anexos:** 1. Fotografías fechadas · 2. Registro de observaciones (folio, fecha, nombre, materia).


#### D-10. Acta de resolución de observaciones

[SI OBJECIONES = Sí]

**ACTA DE SESIÓN DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}} · RESOLUCIÓN DE OBSERVACIONES AL DICTAMEN DEL EJERCICIO {{EJERCICIO}}**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_SESION}}, a las {{HORA_SESION}} horas, en {{LUGAR_SESION}}, conforme a la convocatoria de fecha {{FECHA_CONVOCATORIA}}, se reunieron las personas integrantes de la Comisión que firman al final.

**PRIMERO. Quórum.** Asisten {{NUM_ASISTENTES_EMPRESA}} integrantes de la representación de la Empresa y {{NUM_ASISTENTES_TRAB}} de la representación de las personas trabajadoras; la sesión queda instalada.

**SEGUNDO. Resolución.** La Comisión analiza cada observación y resuelve:

| Folio | Persona trabajadora | Materia | Resolución | Razones | Efecto en su participación |
| --- | --- | --- | --- | --- | --- |
| {{FOLIO_OBSERVACION}} | {{NOMBRE}} | {{MATERIA}} | Procedente / Improcedente / Parcialmente procedente | {{RAZONES}} | {{AJUSTE}} |

[SI DESACUERDO_OBSERVACION = Sí] Respecto de las observaciones {{FOLIOS_SIN_ACUERDO}} no hubo acuerdo entre las representaciones; sus posturas constan en el Anexo 1 y se someten al Inspector del Trabajo conforme al artículo 8 de los estatutos. [FIN SI]

**TERCERO. Ajustes al dictamen.** [SI AJUSTES = Sí] Por las observaciones procedentes se modifica el Anexo 1 del dictamen en los renglones {{RENGLONES_MODIFICADOS}}. Las versiones completa y publicable ajustadas se agregan como Anexo 2 y sustituyen a las anteriores para efectos del pago. [FIN SI] [SI AJUSTES = No] Ninguna observación modifica el dictamen, que queda firme en sus términos. [FIN SI]

**CUARTO. Notificación.** El Secretario entrega a cada persona que formuló una observación copia de la parte de esta acta que le corresponde, a más tardar el {{FECHA_LIMITE_NOTIFICACION}}, recabando su firma de recibido. Si se niega a firmar, se hace constar con la firma de dos testigos.

**QUINTO. Publicación.** [SI AJUSTES = Sí] La versión publicable ajustada se fija en {{LUGARES_PUBLICACION}} el día hábil siguiente. [FIN SI]

Se cierra el acta a las {{HORA_CIERRE}} horas del mismo día.

| Nombre | Carácter | Firma |
| --- | --- | --- |
| {{COORDINADOR}} | Representación de la Empresa · Coordinador |  |
| {{REP_EMPRESA_PROPIETARIOS}} | Representación de la Empresa |  |
| {{SECRETARIO}} | Representación de las personas trabajadoras · Secretario |  |
| {{REP_TRAB_PROPIETARIOS}} | Representación de las personas trabajadoras |  |

**Anexos:** 1. Posturas en caso de desacuerdo · 2. Dictamen ajustado · 3. Acuses de notificación.

[FIN SI]


### Fase 4 – Pago

D-11 y D-14 se generan solo con RESULTADO = B. El estado de pago de cada persona se toma del módulo 6 (validación de pago) y, para quienes causan baja, del finiquito; ningún pago se registra dos veces.


#### D-11. Aviso a personas que ya no laboran y constancia de cumplimiento del pago

[SI RESULTADO = B]

**Parte 1. Aviso individual** (uno por persona con EX_TRABAJADOR = Sí y monto mayor a cero; se envía al último domicilio, correo o teléfono registrado en su alta)

{{NOMBRE_PERSONA}}:

Por los servicios que prestó a {{RAZON_SOCIAL}} durante el ejercicio {{EJERCICIO}}, le corresponde una participación en las utilidades de {{MONTO_PTU}}, antes de retenciones fiscales. Puede cobrarla en {{LUGAR_PAGO_EX}}, de {{HORARIO_PAGO_EX}}, a partir del {{FECHA_INICIO_PAGO}}, presentando identificación oficial. [SI PAGO_TRANSFERENCIA = Sí] También puede solicitar el pago por transferencia escribiendo a {{CORREO_PAGO}} e indicando una cuenta CLABE a su nombre. [FIN SI]

La cantidad no reclamada en el año en que sea exigible se agregará a la utilidad repartible del año siguiente, conforme al artículo 122 de la Ley Federal del Trabajo.

{{MUNICIPIO_ESTADO}}, a {{FECHA_AVISO}}. {{RAZON_SOCIAL}}.

**Parte 2. Constancia de cumplimiento del pago**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_CONSTANCIA_PAGO}}, {{REPRESENTANTE_LEGAL}}, por la Empresa, y {{COORDINADOR}} y {{SECRETARIO}}, por la Comisión, hacen constar:

**PRIMERO. Pagos realizados.** La Empresa pagó la participación del ejercicio {{EJERCICIO}} a {{NUM_PAGADAS}} personas por un total de {{MONTO_PAGADO}}, entre el {{FECHA_INICIO_PAGO}} y el {{FECHA_FIN_PAGO}}. El Anexo 1 relaciona, por persona, el monto, la fecha y la evidencia validada en el sistema:

a) folio fiscal (UUID) del CFDI de nómina con la percepción de participación de utilidades; o

b) referencia y fecha de la dispersión bancaria, con el comprobante del lote.

El Anexo 1 indica, además, si el recibo individual (D-14) de cada persona está firmado.

**SEGUNDO. Pagos realizados con el finiquito.** [SI PAGADAS_EN_FINIQUITO > 0] {{PAGADAS_EN_FINIQUITO}} personas que causaron baja recibieron su participación con el finiquito, según el concepto «PTU pendiente» y el folio fiscal del CFDI relacionados en el Anexo 2. Esos montos no se vuelven a pagar. [FIN SI]

**TERCERO. Pendientes de cobro.** [SI NUM_PENDIENTES > 0] Quedan pendientes de cobro {{NUM_PENDIENTES}} personas por {{MONTO_PENDIENTE}}, relacionadas en el Anexo 3 con la fecha y el medio del aviso enviado. Las cantidades permanecen a su disposición y se controlan conforme a la regla de PTU no cobrada. [FIN SI]

**CUARTO. Cuadre.** La suma de lo pagado, lo pagado con el finiquito y lo pendiente es igual a la cantidad a repartir del dictamen, {{TOTAL_A_REPARTIR}}, [SI MONTO_EXCEDENTE > 0] menos el excedente por el límite individual, {{MONTO_EXCEDENTE}} [FIN SI].

| Nombre | Carácter | Firma |
| --- | --- | --- |
| {{REPRESENTANTE_LEGAL}} | Por la Empresa |  |
| {{COORDINADOR}} | Comisión · Coordinador |  |
| {{SECRETARIO}} | Comisión · Secretario |  |

**Anexos:** 1. Relación de pagos con su evidencia · 2. Pagos con el finiquito · 3. Pendientes de cobro con su aviso.

[FIN SI]

> **Reglas del sistema.**
> D-11 Parte 2 solo se habilita cuando cada persona del Anexo 1 del dictamen tiene uno de estos estados en el módulo 6: Pagada (con CFDI o dispersión cotejados), Pagada en finiquito o Pendiente con aviso enviado. Su Anexo 1 lo genera el módulo 6 (persona, monto, fecha, UUID o referencia de la dispersión, estado y D14_FIRMADO). Un recibo D-14 sin firma no impide la constancia.
> Si una persona causa baja después del cierre del ejercicio y antes del pago, el finiquito muestra el concepto «PTU pendiente»: con el monto del dictamen, si ya está firme; sin monto y con la leyenda «se paga en la fecha de reparto», si aún no lo está.
> Si la PTU se paga con el finiquito, el sistema la marca Pagada en finiquito y bloquea un segundo pago en el reparto.


#### D-14. Recibo individual de participación en las utilidades

[SI RESULTADO = B]

**RECIBO DE PARTICIPACIÓN EN LAS UTILIDADES · EJERCICIO {{EJERCICIO}}**

**Empresa:** {{RAZON_SOCIAL}} · RFC {{RFC}} · Registro patronal {{REGISTRO_PATRONAL}}.

**Persona trabajadora:** {{NOMBRE_PERSONA}} · CURP {{CURP}} · Número de empleado {{NUM_EMPLEADO}} · Situación: [SI EX_TRABAJADOR = No] activa [FIN SI] [SI EX_TRABAJADOR = Sí] baja el {{FECHA_BAJA}} [FIN SI].

| Concepto | Dato |
| --- | --- |
| Días computables | {{DIAS_COMPUTABLES}} |
| Salario computado | {{SALARIO_COMPUTADO}} |
| Participación por días | {{PTU_POR_DIAS}} |
| Participación por salarios | {{PTU_POR_SALARIOS}} |
| Límite individual aplicado | [SI TOPE_APLICADO = Sí] {{MONTO_TOPE}} [FIN SI] [SI TOPE_APLICADO = No] No aplica [FIN SI] |
| Participación bruta | {{MONTO_PTU}} |
| Parte exenta | {{PTU_EXENTA}} |
| Parte gravada | {{PTU_GRAVADA}} |
| Retención de ISR | {{RETENCION_ISR}} |
| [SI PENSION_PTU > 0] Pensión alimenticia ({{PENSION_PORCENTAJE}}) | {{PENSION_PTU}} [FIN SI] |
| [SI OTRAS_DEDUCCIONES_PTU > 0] Otras deducciones: {{OTRAS_DEDUCCIONES_CONCEPTOS}} | {{OTRAS_DEDUCCIONES_PTU}} [FIN SI] |
| Neto pagado | {{MONTO_NETO}} |
| Forma y fecha de pago | {{FORMA_PAGO}}, {{FECHA_PAGO}}[SI CFDI_REGISTRADO = No] · referencia de la dispersión {{REFERENCIA_DISPERSION}}[FIN SI] |
| [SI CFDI_REGISTRADO = Sí] Folio fiscal del CFDI | {{UUID_CFDI}} [FIN SI] |

Recibí de {{RAZON_SOCIAL}} la cantidad neta indicada por concepto de mi participación en las utilidades del ejercicio {{EJERCICIO}}, determinada conforme al dictamen de la Comisión Mixta de Participación de los Trabajadores en las Utilidades de fecha {{FECHA_SESION_DICTAMEN}}. La firma acredita la recepción del monto indicado.

[SI FIRMA_D14 = Electrónica] {{CLAUSULA_FIRMA_ELECTRONICA}} [FIN SI]

{{MUNICIPIO_ESTADO}}, a {{FECHA_PAGO}}.

| Nombre | Firma |
| --- | --- |
| {{NOMBRE_PERSONA}} | [SI FIRMA_D14 = Autógrafa] Firma: ______________________ [FIN SI][SI FIRMA_D14 = Electrónica] {{FIRMA_SELLO_TRAB}} [FIN SI] |

[FIN SI]

> **Reglas del sistema.** El recibo se genera en versión final cuando la obligación de la persona está en «Pagada» en el módulo 6 y el cálculo está validado (PTU_CALCULO_VALIDADO); antes, solo como borrador. Toma de la obligación UUID_CFDI, FECHA_PAGO, FORMA_PAGO y REFERENCIA_DISPERSION, y los montos del Anexo 1 del dictamen y del precálculo (R-5). Con pago por dispersión sin UUID todavía (CFDI_REGISTRADO = No), se genera sin el renglón del folio fiscal y con la referencia de la dispersión; al cargarse el UUID, o si el CFDI se cancela y se sustituye, se genera una nueva versión. La firma se controla con D14_FIRMADO: sin la casilla, alerta a RH a los PAGO_EVIDENCIA_DIAS días hábiles, sin revertir «Pagada». Si el pago se hizo con el finiquito, el recibo no se genera: la evidencia es el recibo de finiquito con el concepto «PTU pendiente».

> Firma de D-14 (20/11/2026, decisión del usuario). El recibo se firma de forma electrónica o autógrafa. FIRMA_D14 toma por omisión la FIRMA_MODALIDAD de la persona; pasa a Autógrafa cuando la persona lo firma en papel (pago en ventanilla o persona sin acceso a la Plataforma, como quien ya no labora), cuando falla la Plataforma o cuando se niega a firmar (dos testigos y envío al correo personal). Con Electrónica, el recibo imprime el sello FIRMA_SELLO_TRAB (antes de firmar, «Pendiente de firma electrónica») y la cláusula de firma electrónica; con Autógrafa, la línea de firma. Solo firma la persona trabajadora; la Empresa no firma el recibo. D14_FIRMADO se marca con cualquiera de las dos formas.


### Contingencias

D-12 y D-13 se generan cuando ocurre el EVENTO correspondiente, en cualquier momento del año.


#### D-12. Acta de sesión extraordinaria por cambio en la base

[SI EVENTO = Complementaria O EVENTO = Resolución SAT]

**ACTA DE SESIÓN EXTRAORDINARIA DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}} · EJERCICIO {{EJERCICIO}}**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_SESION}}, a las {{HORA_SESION}} horas, en {{LUGAR_SESION}}, se reunieron las personas integrantes de la Comisión que firman al final, con quórum conforme al artículo 7 de los estatutos.

**PRIMERO. Hecho que motiva la sesión.**

[SI EVENTO = Complementaria] La Empresa presentó el {{FECHA_COMPLEMENTARIA}} declaración complementaria del ejercicio {{EJERCICIO}}, con número de operación {{NUM_OPERACION_COMPLEMENTARIA}}, que modifica la renta gravable para efectos de la participación de {{RENTA_ANTERIOR}} a {{RENTA_NUEVA}}. La copia se entrega en este acto conforme a D-05, y los plazos de consulta y objeción se computan desde hoy. [FIN SI]

[SI EVENTO = Resolución SAT] El SAT notificó a la Empresa el {{FECHA_NOTIFICACION_SAT}} la resolución {{NUM_RESOLUCION}}, que aumenta la renta gravable del ejercicio {{EJERCICIO}} a {{RENTA_NUEVA}}. [SI IMPUGNACION_EMPRESA = Sí] La Empresa informa que impugnó la resolución el {{FECHA_IMPUGNACION}}; el reparto adicional se suspende hasta que quede firme, con garantía del interés de las personas trabajadoras mediante {{GARANTIA}}. [FIN SI] [FIN SI]

**SEGUNDO. Reparto adicional.** [SI DIFERENCIA_POSITIVA = Sí Y IMPUGNACION_EMPRESA = No] La diferencia genera un reparto adicional de {{MONTO_ADICIONAL}}. La Comisión formula el proyecto conforme a D-08, módulo B, y lo publica a más tardar el {{FECHA_PUBLICACION_ADICIONAL}}. [SI EVENTO = Resolución SAT] El pago se hace dentro de los 60 días siguientes a la notificación de la resolución, a más tardar el {{FECHA_LIMITE_PAGO_ADICIONAL}}. [FIN SI] [FIN SI] [SI DIFERENCIA_POSITIVA = No] La modificación no genera cantidad adicional a repartir: {{RAZON_SIN_ADICIONAL}}. [FIN SI]

| Nombre | Carácter | Firma |
| --- | --- | --- |
| {{COORDINADOR}} | Representación de la Empresa · Coordinador |  |
| {{REP_EMPRESA_PROPIETARIOS}} | Representación de la Empresa |  |
| {{SECRETARIO}} | Representación de las personas trabajadoras · Secretario |  |
| {{REP_TRAB_PROPIETARIOS}} | Representación de las personas trabajadoras |  |

[FIN SI]


#### D-13. Acta de sustitución de integrante

[SI EVENTO = Sustitución]

**ACTA DE SUSTITUCIÓN DE INTEGRANTE DE LA COMISIÓN MIXTA DE PARTICIPACIÓN DE LOS TRABAJADORES EN LAS UTILIDADES DE {{RAZON_SOCIAL}}**

En {{MUNICIPIO_ESTADO}}, el {{FECHA_ACTA}}, las personas integrantes de la Comisión que firman al final hacen constar:

**PRIMERO. Vacante.** {{INTEGRANTE_SALIENTE}}, de la representación {{REPRESENTACION_SALIENTE}}, deja el cargo a partir del {{FECHA_VACANTE}} por {{CAUSA_VACANTE}}, lo que se acredita con {{DOCUMENTO_SOPORTE}}.

**SEGUNDO. Sustitución.** [SI HAY_SUPLENTE = Sí] Ocupa el cargo {{SUPLENTE_QUE_ENTRA}}, suplente según el orden de prelación del acta de integración, quien lo acepta. [FIN SI] [SI HAY_SUPLENTE = No] {{QUIEN_DESIGNA}} designó a {{NUEVO_INTEGRANTE}} mediante {{DOCUMENTO_DESIGNACION}}, que se agrega como Anexo 1, quien acepta el cargo. [FIN SI] [SI REPRESENTACION_SALIENTE = Personas trabajadoras] Se verificó que la persona que entra no ocupa un puesto de confianza. [FIN SI]

**TERCERO. Cargo interno.** [SI SALIENTE_TENIA_CARGO = Sí] La Comisión designa a {{NUEVO_TITULAR_CARGO}} como {{CARGO_VACANTE}}. [FIN SI]

**CUARTO. Entrega de expediente.** [SI SALIENTE_TENIA_CARGO = Sí Y EXPEDIENTE_ENTREGADO = Sí] {{INTEGRANTE_SALIENTE}} entregó el expediente el {{FECHA_ENTREGA_EXPEDIENTE}}. [FIN SI] [SI SALIENTE_TENIA_CARGO = Sí Y EXPEDIENTE_ENTREGADO = No] No fue posible recabar la entrega; la Empresa conserva el expediente en el domicilio del centro de trabajo y la Comisión lo revisa en su próxima sesión. [FIN SI]

| Nombre | Carácter | Firma |
| --- | --- | --- |
| {{INTEGRANTES_VIGENTES}} | Integrantes |  |
| {{PERSONA_QUE_ENTRA}} | Integrante que acepta |  |

[FIN SI]

> **Regla del sistema.** CAUSA_VACANTE es una lista: terminación de la relación de trabajo, renuncia al cargo, promoción a puesto de confianza, revocación o ausencia injustificada a dos sesiones consecutivas. Una baja en el alta o un cambio a un puesto de Confianza en el organigrama de un integrante dispara la alerta de sustitución.

---

## 10. Diccionario de variables

### 10.1 Variables de las plantillas

Extraídas del texto de D-01 a D-14 (incluye las que solo aparecen en condiciones). «V» sin más detalle: dato del evento que se captura en la pantalla del documento indicado.

| Variable | Nivel | Tipo | Validación | Activa o imprime |
| --- | --- | --- | --- | --- |
| ACUERDO | V | Sí/No | — | D-07 |
| AJUSTE | V | Texto | — | D-10 |
| AJUSTES | V | Sí/No | — | D-10 |
| ASISTENTES_EXTERNOS | V | Sí/No | — | D-04 |
| ASISTENTES_EXTERNOS_LISTA | V | Texto | — | D-04 |
| ASUNTO_EXTRAORDINARIO | V | Texto | — | D-04 |
| ASUNTO_SESION | V | Texto | — | D-04 |
| AUTORIDAD_INSPECCION | E | Texto (solo el nombre de la autoridad; el ámbito federal o local sale de `COMPETENCIA`) | Diccionario único, 1.1 (decisión P2). Sin valor por omisión; vacía, D-03 imprime el marcador visible | D-03, art. 8 de los estatutos |
| CANDIDATURA | V | Texto | — | D-02 |
| CANDIDATURAS_EMPATADAS | V | Texto | — | D-02 |
| CARGO_VACANTE | V | Texto | — | D-13 |
| CAUSA_VACANTE | V | Lista (regla de D-13) | — | D-13 |
| CFDI_REGISTRADO | S | Sí/No | Sí si la obligación tiene UUID_CFDI | D-14 |
| CLAUSULA_FIRMA_ELECTRONICA | S | Texto común del kit de contratación | — | Documentos firmados electrónicamente |
| COMPLEMENTARIA | V | Sí/No | — | D-05, D-08 |
| CONFORMIDAD_FIRMAS | V | Sí/No | No por omisión; recomendada con RESULTADO = B | Anexo de conformidad de D-03 |
| CONTACTO_REGISTRO | V | Texto | — | D-01 |
| COORDINADOR | V | Persona (representación de la Empresa) | — | Actas |
| CORREO_PAGO | V | Texto | — | D-11 |
| CURP | A | Texto (18) | Equivale a TRAB_CURP | D-14 |
| DESACUERDO_OBSERVACION | V | Sí/No | — | D-10 |
| DESCRIPCION_INCIDENCIA | V | Texto | — | D-02, D-09 |
| DESIGNACION_OBRERA | E | Designación / Elección | Solo con SINDICATO = No; Designación por omisión | D-01, D-02 y párrafo de elección de D-03 |
| DIAS_COMPUTABLES | S/V | Entero | R-1, R-2 o R-4 | D-08 Anexo 1, D-14 |
| DIAS_HABILES_TRANSCURRIDOS | V | Texto | — | D-05 |
| DIFERENCIA_POSITIVA | S | Sí/No | RENTA_NUEVA > RENTA_ANTERIOR | D-12 |
| DOCUMENTOS_FALTANTES | V | Texto + archivo | — | D-07 |
| DOCUMENTOS_FALTANTES_LISTA | V | Texto + archivo | — | D-07 |
| DOCUMENTOS_REQUERIDOS | V | Texto + archivo | — | D-04 |
| DOCUMENTO_DESIGNACION | V | Texto + archivo | — | D-13 |
| DOCUMENTO_EXCEPCION | V | Texto + archivo | — | D-07, D-08 |
| DOCUMENTO_SOPORTE | V | Texto + archivo | — | D-13 |
| DOMICILIO_CENTRO | E (catálogo de centros) | Texto | — | D-03 |
| EJERCICIO | V | Texto | — | D-04, D-05, D-06, D-07, D-08, D-09, D-10, D-11, D-12, D-14 |
| EJERCICIO_ANTERIOR | V | Texto | — | D-08 |
| EMPATE | V | Sí/No | — | D-02 |
| ESCRUTADOR_MESA | V | Texto | — | D-02 |
| EVENTO | V | Complementaria / Resolución SAT / Sustitución | — | D-12 o D-13 |
| EXPEDIENTE_ENTREGADO | V | Sí/No | — | D-13 |
| EX_TRABAJADOR | S | Sí/No | Sí si FECHA_BAJA ≤ fecha de pago | D-11 Parte 1, D-14, R-5 |
| EX_TRABAJADORES | S | Sí/No | Sí si alguna persona con monto > 0 es EX_TRABAJADOR | D-08 B, D-09, D-11 |
| FACTOR_DIAS | S | Decimal (9) | Mitad ÷ suma de días computables | D-08 B |
| FACTOR_SALARIOS | S | Decimal (9) | Mitad ÷ suma de salarios devengados computados | D-08 B |
| FECHA_ACTA | V | Fecha | — | D-03, D-13 |
| FECHA_AVISO | V | Fecha | — | D-01, D-02, D-11 |
| FECHA_BAJA | A/S | Fecha | De la baja (módulo 4) | D-14 |
| FECHA_CAPTURA | V | Fecha | — | D-07 |
| FECHA_COMPLEMENTARIA | V | Fecha | — | D-05, D-08, D-12 |
| FECHA_CONFIRMACION_CALCULO | V | Fecha | — | D-07 |
| FECHA_CONSTANCIA | V | Fecha | — | D-02, D-09 |
| FECHA_CONSTANCIA_PAGO | V | Fecha | — | D-11 |
| FECHA_CONVOCATORIA | V | Fecha | — | D-04, D-05, D-07, D-10 |
| FECHA_ELECCION | V | Fecha | — | D-01, D-02, D-03 |
| FECHA_ENTREGA_EXPEDIENTE | V | Fecha | — | D-13 |
| FECHA_ENTREGA_FALTANTES | V | Fecha | — | D-07 |
| FECHA_FIN_CONSULTA | S | Fecha | Calendario (sección 3) | D-05, D-06 |
| FECHA_FIN_EXCEPCION | V | Fecha | — | D-08 |
| FECHA_FIN_OBSERVACIONES | S | Fecha | FECHA_PUBLICACION + 15 días hábiles | D-08, D-09 |
| FECHA_FIN_PAGO | V | Fecha | — | D-11 |
| FECHA_IMPORTACION | V | Fecha | — | D-07 |
| FECHA_IMPUGNACION | V | Fecha | — | D-12 |
| FECHA_INICIO_PAGO | V | Fecha | — | D-11 |
| FECHA_INICIO_PUBLICACION | V | Fecha | ≤ FECHA_ELECCION − 5 días hábiles | D-01, D-02 |
| FECHA_LIMITE_INSPECTOR | V | Fecha | — | D-07 |
| FECHA_LIMITE_NOTIFICACION | V | Fecha | — | D-10 |
| FECHA_LIMITE_OBJECIONES | S | Fecha | Calendario | D-05, D-06 |
| FECHA_LIMITE_PAGO | S | Fecha | 30/05 (moral) o 29/06 (física) del año siguiente | D-08, R-3, módulo 6 |
| FECHA_LIMITE_PAGO_ADICIONAL | S | Fecha | 60 días desde la notificación de la resolución | D-12, módulo 6 |
| FECHA_LIMITE_REGISTRO | V | Fecha | — | D-01 |
| FECHA_LIMITE_RESOLUCION | S | Fecha | FECHA_FIN_OBSERVACIONES + 15 días hábiles | D-08 a D-10 |
| FECHA_NOTIFICACION_SAT | V | Fecha | — | D-12 |
| FECHA_OFICIO_SINDICATO | V | Fecha | — | D-03 |
| FECHA_PAGO | Módulo 6 | Fecha | — | D-14 |
| FECHA_PRESENTACION | V | Fecha | Obligatoria; dispara el calendario | D-05, D-08 |
| FECHA_PUBLICACION | S/V | Fecha | ≤ FECHA_LIMITE_PAGO − 45 días hábiles (alerta) | D-07 a D-09 |
| FECHA_PUBLICACION_ADICIONAL | V | Fecha | — | D-12 |
| FECHA_PUBLICACION_AVISO | V | Fecha | — | D-06 |
| FECHA_PUBLICACION_PROYECTO | V | Fecha | — | D-06 |
| FECHA_SEGUNDA_JORNADA | V | Fecha | — | D-02 |
| FECHA_SESION | V | Fecha | — | D-04, D-05, D-06, D-07, D-08, D-10, D-12 |
| FECHA_SESION_DICTAMEN | V | Fecha | — | D-09, D-14 |
| FECHA_SESION_ENTREGA | V | Fecha | — | D-07 |
| FECHA_VACANTE | V | Fecha | — | D-13 |
| FIRMA_D14 | V (por persona) | Electrónica / Autógrafa | Por omisión FIRMA_MODALIDAD de la persona | Sello o línea de firma y cláusula de D-14 |
| FIRMA_SELLO_TRAB | S | Derivada de la firma electrónica | «Pendiente de firma electrónica» antes de firmar | D-14 |
| FOLIO | V | Texto | — | D-07 |
| FOLIOS_SIN_ACUERDO | V | Lista o tabla | — | D-10 |
| FOLIO_OBSERVACION | V | Texto | — | D-10 |
| FORMA_PAGO | V / módulo 6 | Texto | — | D-08 B, D-14 |
| FRACCION_126 | V | Texto | — | D-08 |
| GARANTIA | V | Texto | Obligatoria con IMPUGNACION_EMPRESA = Sí | D-12 |
| HAY_SUPLENTE | V | Sí/No | — | D-13 |
| HECHO_EXCEPCION | V | Texto | — | D-08 |
| HORARIO_CONSULTA | V | Hora | — | D-05, D-06 |
| HORARIO_PAGO_EX | V | Hora | — | D-08, D-11 |
| HORA_CIERRE | V | Hora | — | D-03, D-05, D-07, D-10 |
| HORA_SESION | V | Hora | — | D-04, D-05, D-07, D-10, D-12 |
| IMPUGNACION_EMPRESA | V | Sí/No | — | D-12 |
| INCIDENCIA_PUBLICACION | V | Sí/No | — | D-02, D-09 |
| INTEGRANTE | V | Texto | — | D-04 |
| INTEGRANTES_CONVOCADOS | V | Lista o tabla | — | D-04 |
| INTEGRANTES_VIGENTES | V | Lista o tabla | — | D-13 |
| INTEGRANTE_SALIENTE | V | Texto | — | D-13 |
| JORNADA | V | Primera / Segunda | — | D-02 |
| LISTA_DOCUMENTOS | V | Lista o tabla | — | D-04 |
| LISTA_EXCLUIDOS_DIRECCION | S | Lista | Personas con PTU_EXCLUIDO = Sí | D-08 B |
| LUGARES_PUBLICACION | E/V | Texto | Por centro; se precarga del catálogo de centros | D-01 a D-10 |
| LUGAR_CONSULTA | V | Texto | — | D-05, D-06 |
| LUGAR_PAGO_EX | V | Texto | — | D-08, D-11 |
| LUGAR_SESION | V | Texto | — | D-04, D-05, D-07, D-10, D-12 |
| MANIFESTACIONES | V | Sí/No | — | D-05 |
| MANIFESTACIONES_ASISTENTES | V | Texto | — | D-05 |
| MATERIA | V | Texto | — | D-10 |
| MECANISMO_DESEMPATE | V | Texto | — | D-02 |
| MEDIO_DIGITAL | V | Texto | — | D-01, D-02 |
| MONTO_ADICIONAL | V | Moneda | — | D-12 |
| MONTO_EXCEDENTE | S | Moneda | Suma de excedentes del límite individual; no se paga | D-08 B QUINTO, D-11 cuadre |
| MONTO_NETO | S | Moneda | ≥ 0 (bloqueo) | D-14 |
| MONTO_NO_RECLAMADO_ANTERIOR | S | Moneda | Suma de traspasos de R-3 | D-08 B |
| MONTO_PAGADO | S | Moneda | Del módulo 6 | D-11 |
| MONTO_PENDIENTE | S | Moneda | Del módulo 6 | D-11 |
| MONTO_PTU | S | Moneda | Participación final de la persona (después del límite) | D-11, D-14 |
| MONTO_TOPE | S | Moneda | Límite aplicado | D-14 |
| MUNICIPIO_ESTADO | E (catálogo de centros) | Texto | — | Todos |
| NOMBRE | V | Texto | — | D-10 |
| NOMBRE_PERSONA | A | Texto | Equivale a TRAB_NOMBRE | D-11, D-14 |
| NUEVO_INTEGRANTE | V | Texto | — | D-13 |
| NUEVO_TITULAR_CARGO | V | Texto | — | D-13 |
| NUM_ASISTENTES_EMPRESA | V | Entero | — | D-05, D-07, D-10 |
| NUM_ASISTENTES_TRAB | V | Entero | — | D-05, D-07, D-10 |
| NUM_EMPLEADO | A | Texto | Opcional | D-14 |
| NUM_FOJAS | V | Entero | — | D-05 |
| NUM_OBSERVACIONES | V | Entero | — | D-09 |
| NUM_OPERACION | V | Texto | Acuse del SAT | D-05, D-08 |
| NUM_OPERACION_COMPLEMENTARIA | V | Entero | — | D-05, D-12 |
| NUM_PADRON | V | Entero | — | D-02 |
| NUM_PAGADAS | S | Entero | Del módulo 6 | D-11 |
| NUM_PENDIENTES | S | Entero | Del módulo 6 | D-11 |
| NUM_REPRESENTANTES_POR_PARTE | E | Entero | Mínimo 1; común con la CMRIT | Integrantes y firmas |
| NUM_RESOLUCION | V | Entero | — | D-12 |
| NUM_VOTANTES | V | Entero | — | D-02 |
| OBJECIONES | S | Sí/No | Sí si hay observaciones registradas | D-09, D-10 |
| OTRAS_DEDUCCIONES_CONCEPTOS | S | Texto | Conceptos de la tabla | D-14 |
| OTRAS_DEDUCCIONES_PTU | V | Tabla dinámica: tipo, concepto, importe, soporte | Aviso art. 130 LFT | D-14 |
| PAGADAS_EN_FINIQUITO | S | Entero | Del módulo 4 / 6 | D-11 Parte 2 |
| PAGO_TRANSFERENCIA | V | Sí/No | — | D-11 |
| PENSION_PORCENTAJE | A | Porcentaje | De la resolución | D-14 |
| PENSION_PTU | S | Moneda | R-5 paso 5 | D-14 |
| PERSONA_QUE_ENTRA | V | Texto | — | D-13 |
| PERSONA_QUE_PUBLICO | V | Texto | — | D-02 |
| PORCENTAJE_PTU | X | Porcentaje | 10 % vigente; tabla con vigencia | D-08 B |
| PORC_PARTICIPACION | S | Porcentaje | NUM_VOTANTES ÷ NUM_PADRON; válida > 50 % en la primera jornada | D-02 |
| POSTURA_EMPRESA | V | Texto | — | D-07 |
| POSTURA_TRABAJADORES | V | Texto | — | D-07 |
| PREGUNTAS_RELEVANTES | V | Sí/No | — | D-07 |
| PREGUNTAS_Y_RESPUESTAS | V | Texto | — | D-07 |
| PRESIDENTE_MESA | V | Texto | — | D-02 |
| PTU_EXENTA | S | Moneda | R-5 paso 1; sustituible | D-14 |
| PTU_GRAVADA | S | Moneda | R-5 paso 2 | D-14 |
| PTU_POR_DIAS | S | Moneda | Días × FACTOR_DIAS | D-14 |
| PTU_POR_SALARIOS | S | Moneda | Salario devengado computado × FACTOR_SALARIOS | D-14 |
| PUESTO_PERSONA_QUE_PUBLICO | V | Texto | — | D-02 |
| PUESTO_RESPONSABLE_INFORMACION | V | Texto | — | D-07 |
| QUIEN_DESIGNA | V | Texto | — | D-13 |
| RAZONES | V | Texto | — | D-10 |
| RAZON_SIN_ADICIONAL | V | Texto | — | D-12 |
| RAZON_SOCIAL | E | Texto | Equivale a PATRON_RAZON_SOCIAL | Todos |
| REFERENCIA_DISPERSION | Módulo 6 | Texto | — | D-14 |
| REGISTRO_PATRONAL | E (catálogo de centros) | Texto | Del centro | D-03, D-14 |
| RENGLONES_MODIFICADOS | V | Lista o tabla | — | D-10 |
| RENTA_ANTERIOR | V | Moneda | — | D-12 |
| RENTA_GRAVABLE_PTU | V | Moneda (admite negativo) | Obligatoria | RESULTADO; D-07, D-08 |
| RENTA_NUEVA | V | Moneda | — | D-12 |
| REPRESENTACION_SALIENTE | V | Texto | — | D-13 |
| REPRESENTANTES_SUPLENTES | E | Sí/No | Sí por omisión | Suplentes en D-01 a D-03 y D-13 |
| REPRESENTANTE_LEGAL | E | Texto | Equivale a REP_NOMBRE | D-03, D-05, D-07, D-11 |
| REP_EMPRESA_PROPIETARIOS | V | Lista de personas del alta | — | D-03 y actas |
| REP_EMPRESA_SUPLENTES | V | Lista | — | D-03 |
| REP_TRAB_PROPIETARIOS | V | Lista de personas del alta | Sin clasificación Confianza; del centro | D-02, D-03 y actas |
| REP_TRAB_SUPLENTES | V | Lista de personas del alta | Ídem; solo con REPRESENTANTES_SUPLENTES = Sí | D-02, D-03 |
| RESPONSABLE_CAPTURA | V | Texto | — | D-07 |
| RESPONSABLE_INFORMACION | V | Texto | — | D-07 |
| RESULTADO | S | A / B / C | A si renta ≤ 0; B si > 0; C con excepción del art. 126 | D-07, D-08, D-09, D-11, D-14 |
| RETENCION_ISR | S | Moneda | R-5 pasos 3 o 3 bis; sustituible | D-14 |
| RFC | E | Texto | Equivale a PATRON_RFC | D-03, D-14 |
| SALARIO_COMPUTADO | S | Moneda | Salario diario, topado si es confianza | D-08 Anexo 1, D-14 |
| SALARIO_MAXIMO_CONFIANZA | S | Moneda | SALARIO_REFERENCIA × 1.20 | D-08 B |
| SALARIO_REFERENCIA | S | Moneda | Salario diario más alto de sindicalizados (con SINDICATO = Sí) o de planta | D-08 B |
| SALIENTE_TENIA_CARGO | V | Sí/No | — | D-13 |
| SECRETARIO | V | Persona (representación obrera) | — | Actas |
| SECRETARIO_MESA | V | Texto | — | D-02 |
| SINDICATO | E | Sí/No | Obligatoria | D-01 a D-06, D-13; variante sindical |
| SINDICATO_NOMBRE | V | Texto | — | D-03, D-05, D-06 |
| SINDICATO_REPRESENTANTE | V | Texto | — | D-03, D-05 |
| SUPLENTE_QUE_ENTRA | V | Texto | — | D-13 |
| TABLA_MESAS | V | Lista o tabla | — | D-01 |
| TESTIGO_1 | V | Texto | — | D-02 |
| TIPO_SESION | V | Texto | — | D-04 |
| TOPE_APLICADO | S | Sí/No | Sí si la bruta rebasa el límite | D-14 |
| TOTAL_A_REPARTIR | S | Moneda | UTILIDAD_REPARTIBLE + MONTO_NO_RECLAMADO_ANTERIOR | D-08 B, D-11 |
| TRABAJO_HOGAR | E | Sí/No | No por omisión | D-08 B |
| TURNOS_MESAS | E | Entero | Del catálogo de turnos | D-02 |
| UTILIDAD_REPARTIBLE | S | Moneda | RENTA_GRAVABLE_PTU × PORCENTAJE_PTU | D-08 B |
| UUID_CFDI | Módulo 6 | Texto | De la obligación en Pagada | D-14 |
| VIA_CALCULO | V | Automático / Importación / Captura | Obligatoria con RESULTADO = B | R-1, R-2, R-4; D-07, D-08 |
| VOTOS | V | Texto | — | D-02 |
| VOTOS_NULOS | V | Texto | — | D-02 |

### 10.2 Variables del motor y de otros niveles

| Variable | Nivel | Tipo | Validación | Activa o imprime |
| --- | --- | --- | --- | --- |
| PTU_EXCLUIDO | O | Sí/No | Independiente del atributo de dirección del periodo de prueba | Exclusión art. 127, fr. I (R-4, D-08 B) |
| SINDICALIZADO | A | Sí/No | Solo con SINDICATO = Sí | SALARIO_REFERENCIA |
| CLASIFICACION (Base / Confianza) | O | Lista | — | Tope de confianza; elegibilidad de representantes |
| TIPO_RELACION y eventualidad | A | Lista | — | Regla de 60 días |
| SALARIO_PERSONA y versión de condiciones | A / módulo 5 | Moneda con historial | Se lee por periodo | R-2, R-4, R-5, límite individual, SALARIO_REFERENCIA |
| PENSION_ALIMENTICIA / PENSION_INCLUYE_PTU / PENSION_BASE_PTU | A | Sí/No; Sí/No; Bruta / Neta de ISR | PENSION_INCLUYE_PTU sin dato: no se calcula | R-5 paso 5 |
| INGRESO_MENSUAL_ORDINARIO | V | Moneda | Por omisión SALARIO_PERSONA × 30.4; editable | R-5 |
| PTU_CALCULO_VALIDADO (+ contador y fecha) | V | Sí/No | Se revierte si cambia un monto | D-14 final; obligación del módulo 6 |
| CALCULO_CONFIRMADO / FECHA_CONFIRMACION_CALCULO | V | Sí/No; fecha | Obligatoria con VIA_CALCULO = Automático | Habilita D-08 B; D-07 |
| PTU_ESTADO_PAGO | Módulo 6 | Pendiente de pago / Pagada / Pagada en finiquito / Pendiente con aviso / No reclamada | R-3 | D-11, alertas |
| D14_FIRMADO | Módulo 6 | Casilla + archivo opcional | Alerta a RH a los PAGO_EVIDENCIA_DIAS días hábiles; no revierte Pagada | Anexo 1 de D-11 Parte 2 |
| FECHA_TRASPASO_PTU | S | Fecha | Un año desde el día siguiente a FECHA_LIMITE_PAGO | Estado No reclamada; traspaso |
| PTU_RECIBIDA_1, _2, _3 | S/V | Moneda | Del historial del sistema; si no, del layout; si no, 0 con aviso | Límite por promedio |
| FIRMA_COMISION | V (por documento) | Electrónica / Autógrafa | Sin valor por omisión; Electrónica solo si todos los firmantes tienen usuario | Sellos o línea de firma y cláusula de firma electrónica en D-02 a D-05, D-07 a D-10, D-11 Parte 2, D-12 y D-13 (8.1) |
| PTU_COMPUTA | X | Tabla por tipo de evento: Sí/No | Con vigencia; aprobación humana | Días computables (R-4); advertencias (R-1, R-2) |
| REF_EXENCION, UMA, TARIFA_ISR_96 | X | Tablas versionadas del módulo 4 | Solo aprobadas | R-5 |
| Campos del layout R-1 | V (importación) | Ver 5.2 | Errores bloquean D-08 B | Anexo 1 de D-07 y D-08 |

### 10.3 Equivalencias con el diccionario único (verificar al unificar)

| En este kit | En el contrato y el módulo 4 |
| --- | --- |
| `RAZON_SOCIAL` | `PATRON_RAZON_SOCIAL` |
| `RFC` | `PATRON_RFC` |
| `REPRESENTANTE_LEGAL` | `REP_NOMBRE` |
| `NOMBRE_PERSONA` | `TRAB_NOMBRE` |
| `CURP` | `TRAB_CURP` |
| `DOMICILIO_CENTRO` / `MUNICIPIO_ESTADO` | Catálogo único de centros (`CENTRO_NOMBRE` y domicilio) |
| `FECHA_BAJA` | `BAJA_FECHA` |

### 10.4 Variables eliminadas (no programar)

| Variable | Motivo |
| --- | --- |
| `TIPO_PATRON` | Sustituida por `EMPRESA_TIPO_PERSONA` |
| `NUM_REP_TRAB`, `NUM_REP_POR_PARTE`, `N_REP` | Sustituidas por `NUM_REPRESENTANTES_POR_PARTE` |
| `REP_PATRON_2`, `REP_TRAB_2`, `SUPLENTE_*` | Sustituidas por `REP_EMPRESA_*` y `REP_TRAB_*` |
| `CMCAP_ACTIVA`, `CMRIT_INTEGRACION_MODO` | El kit no hace referencia a otras comisiones; el criterio común usa `DESIGNACION_OBRERA` |
| `TRATAMIENTO_EXCEDENTE` | El excedente no se reparte; texto fijo en D-08 B (17/11/2026) |
| Voto secreto y boletas como anexo de D-02 | Eliminados (12/11/2026) |
| Fonacot como deducción de la PTU | No se descuenta (13/11/2026) |
| `SALARIO_DIARIO` como base de cálculo | Sustituida por `SALARIO_PERSONA`; en el layout R-1 queda solo como cotejo opcional (20/11/2026) |


---

## 11. Dependencias y pendientes

### 11.1 Dependencias con otros módulos

| Módulo | Qué necesita este módulo | Qué le envía este módulo |
| --- | --- | --- |
| Configuración de la empresa | `SINDICATO`, `DESIGNACION_OBRERA`, `NUM_REPRESENTANTES_POR_PARTE`, `REPRESENTANTES_SUPLENTES`, `EMPRESA_TIPO_PERSONA`, `PTU_ISR_METODO`, `TRABAJO_HOGAR`, `AUTORIDAD_INSPECCION`, catálogos de centros y turnos | — |
| Organigrama | Clasificación Base o Confianza; `PTU_EXCLUIDO` | — |
| Alta | CURP, nombre, fechas, tipo de relación, `SINDICALIZADO`, domicilio, correo, teléfono, `FIRMA_MODALIDAD`, pensión alimenticia (`PENSION_INCLUYE_PTU`, `PENSION_BASE_PTU`) | — |
| Módulo 5 | `SALARIO_PERSONA` con historial y versión de condiciones | — |
| Módulo de permisos (10) y de vacaciones (11) | Eventos por persona y día (fuente única de ausencias) | — |
| Módulo 4 | Parámetros versionados y `REF_EXENCION`; bajas y `PTU_PENDIENTE` | `PTU_PENDIENTE`, `PTU_EJERCICIO`, monto si el dictamen está firme; padrón de ex trabajadores |
| Módulo 6 | Estado de cada obligación, `UUID_CFDI`, `FECHA_PAGO`, `FORMA_PAGO`, `REFERENCIA_DISPERSION`, `D14_FIRMADO`; Anexo 1 de D-11 Parte 2 | Obligaciones «PTU» y «PTU adicional» con el neto validado; `FECHA_LIMITE_PAGO` y `FECHA_LIMITE_PAGO_ADICIONAL` |
| Firma electrónica | Sello `FIRMA_SELLO_TRAB`, bitácora y cláusula común | D-14 para firma |
| Axia CYA | Usa D-01 y D-02 para la elección conjunta (boleta separada por comisión) | — |

### 11.2 Pendientes que no bloquean la programación

1. `AUTORIDAD_INSPECCION` definida en el diccionario único (solo el nombre; el ámbito sale de `COMPETENCIA`). Mientras la pantalla de la empresa no la tenga, D-03 imprime el campo vacío como marcador visible.
2. Revisión final del usuario del modelo maestro (aprobaciones provisionales).

### 11.3 Decisiones resueltas en la v1.2

- Sin pendientes de decisión: el nivel de firma de los documentos colectivos quedó resuelto con `FIRMA_COMISION` (21/11/2026).

---

## Anexo A. Casos de prueba

### A.1 Reparto (R-4 y 5.3)

Ejercicio 2025; sin sindicato; total a repartir $100,000.00. Límite = `SALARIO_PERSONA` × 90.

| Persona | Datos | Resultado esperado |
| --- | --- | --- |
| Ana | Base, $400.00, sin eventos; historial $9,000 / $10,000 / $11,000 | 365 días; devengado $146,000.00; por días $14,415.48; por salarios $16,687.62; bruta $31,103.10; límite $36,000.00; final $31,103.10 |
| Luis | Base, $200.00; 10 días C1 y 15 días C2; historial $6,000 / $7,000 / $8,000 | 355 días; devengado $71,000.00; bruta $22,135.75; límite $18,000.00; final $18,000.00; `TOPE_APLICADO` = Sí |
| Rosa | Confianza, $1,200.00; historial $10,000 / $12,000 / $14,000 | Salario computado $480.00; 365 días; devengado computado $175,200.00; bruta $34,440.63; límite $108,000.00; final $34,440.63 |
| Sara | Base, $250.00, baja el 30/06/2025; sin historial | 181 días; devengado $45,250.00; bruta $12,320.52; límite $22,500.00; final $12,320.52; aviso «sin historial»; `EX_TRABAJADOR` = Sí |
| Pedro | Eventual, 45 días | Sin derecho (menos de 60) |

Controles: `FACTOR_DIAS` 39.494470774; `FACTOR_SALARIOS` 0.114298777; suma de brutas $100,000.00; `MONTO_EXCEDENTE` $4,135.75; total pagado $95,864.25; D-11 cuadra «menos el excedente»; D-08 B imprime el párrafo del QUINTO.

### A.2 Precálculo (R-5)

Parámetros 2026 (UMA $117.31; tarifa mensual del Anexo 8 RMF 2026, la misma del módulo 4, Anexo A.1). Bruta $18,000.00; ingreso mensual ordinario $15,000.00; sin pensión.

| Método | Resultado esperado |
| --- | --- |
| Art. 174 RLISR | Exenta $1,759.65; gravada $16,240.35; PTU mensual $1,352.62; tasa 17.92 %; ISR $2,910.27; neto $15,089.73 |
| Art. 96 LISR | ISR $3,381.77; neto $14,618.23 |
| Ex trabajador con método 174 configurado | Se usa el art. 96 con ingreso ordinario en cero y se avisa |

### A.3 Reglas

| Caso | Datos | Resultado esperado |
| --- | --- | --- |
| 1. Resultado A | `RENTA_GRAVABLE_PTU` = −50,000 | D-08 módulo A con la frase de pérdida fiscal; sin D-11 ni D-14 |
| 2. Importación con error | CURP inexistente en el layout | D-08 B bloqueado; error en el reporte |
| 3. Cotejo de salario | `SALARIO_DIARIO` del layout ≠ `SALARIO_PERSONA` | Advertencia; el límite usa `SALARIO_PERSONA` |
| 4. Días con C1 pagado | Persona con 3 días de espera de C1 pagados por la Empresa | No computan para la PTU; sí para el aguinaldo |
| 5. D4 con reubicación | 20 días de D4 con MOD-5 aceptada | Computan |
| 6. Pensión sin dato | `PENSION_ALIMENTICIA` = Sí y `PENSION_INCLUYE_PTU` vacío | No calcula la pensión; aviso «Revise si la resolución comprende la PTU» |
| 7. Neto negativo | Otras deducciones mayores que la bruta menos ISR | Bloqueo |
| 8. Pago por dispersión sin UUID | Obligación en Pagada con dispersión | D-14 sin folio fiscal, con referencia; al cargar el UUID, nueva versión |
| 9. Recibo sin firma | Pagada; `D14_FIRMADO` = No a los `PAGO_EVIDENCIA_DIAS` | Alerta a RH; el estado no se revierte; D-11 Parte 2 se genera |
| 10. Firma en papel | `FIRMA_MODALIDAD` = Electrónica; RH elige `FIRMA_D14` = Autógrafa | D-14 con línea de firma y sin cláusula electrónica |
| 11. No reclamada | Pendiente con aviso; llega `FECHA_TRASPASO_PTU` | Estado No reclamada; el monto entra a `MONTO_NO_RECLAMADO_ANTERIOR` del siguiente reparto |
| 12. Reclamación tardía | La persona reclama después del traspaso | No se paga; se registra y se alerta a consultoría |
| 13. Pagada en finiquito | PTU determinada pagada en el recibo de finiquito | Estado Pagada en finiquito; sin D-14; bloqueo de segundo pago |
| 14. Resolución del SAT impugnada | `EVENTO` = Resolución SAT; `IMPUGNACION_EMPRESA` = Sí | D-12 con `GARANTIA` obligatoria; sin reparto adicional mientras no quede firme |
| 15. Elección con baja participación | Primera jornada con 45 % del padrón | D-02 con segunda jornada dentro de 10 días hábiles, sin umbral |
| 16. Suplentes desactivados | `REPRESENTANTES_SUPLENTES` = No | D-01 a D-03 y D-13 sin menciones, filas ni columnas de suplentes |
| 17. Falta por confirmar | Persona con 2 faltas por confirmar y 1 confirmada en el ejercicio; VIA_CALCULO = Automático | Se resta 1 día; alerta a RH por las 2 por confirmar; no bloquea |
| 18. Falta confirmada después | RH confirma una de esas faltas después de `CALCULO_CONFIRMADO` | Se revierte la confirmación de esa persona y se recalcula su día |
| 19. Acta con firma electrónica | D-07 con `FIRMA_COMISION` = Electrónica; los cuatro integrantes tienen usuario | Sellos en la tabla de firmas y cláusula al final; firmado cuando firman los cuatro |
| 20. Firmante externo | D-03 con `SINDICATO` = Sí (firma el representante sindical sin usuario) | Solo se ofrece Autógrafa |

Estos valores sirven para probar el programa; el contador valida cada caso real.

---

## Fuentes

- Reglamento de los Artículos 121 y 122 de la LFT (DOF 05/06/2014) – El Conta
- Reglamento arts. 121 y 122 LFT, art. 9 – El Conta
- Artículo 125 LFT – mLey
- Porcentaje de PTU vigente (10 %) – BDO México
- Ley Federal del Trabajo, texto vigente (última reforma DOF 14-05-2026), arts. 117 a 131 y 516.
- Reglamento de la LISR (última reforma DOF 06-05-2016), art. 174.
- Anexo 8 de la RMF 2026 (DOF 28-12-2025), tarifa mensual del art. 96 LISR.
