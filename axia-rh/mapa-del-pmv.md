# Axia RH — Mapa del PMV

Actualizado: 17 de noviembre de 2026, después de los cortes del módulo 5 (15/11), de los módulos 6 y 8 (15/11) y de vacaciones y aguinaldo (16/11) · Coordinación: «Cerebro»

Este documento muestra qué necesita cada módulo del PMV, qué ya existe, qué falta, qué choca entre conversaciones y qué debe hacer cada una. Complementa al «AXIARH - Registro de decisiones», que guarda las decisiones.

**Cómo se coordina:** cada conversación trabaja un documento y, al cerrar decisiones, hace un corte de estado. El corte se trae a Cerebro, que lo integra al registro, revisa que no choque con otros documentos y actualiza este mapa. Cerebro no ve las otras conversaciones: solo sabe lo que está en el registro, en este mapa y lo que se le trae.

Prioridad: **A** = sin esto el módulo no funciona o queda expuesto en una inspección · **B** = necesario para el PMV · **C** = puede esperar a la siguiente versión.

---

## Alcance del PMV

| # | Módulo | Qué debe lograr |
|---|---|---|
| 1 | Kit de contratación | Generar el contrato de cualquier tipo y todos los documentos de ingreso |
| 2 | RIT y su comisión mixta | Generar el reglamento, integrar la comisión, documentar su difusión y depósito, y operar el procedimiento disciplinario |
| 3 | PTU y su procedimiento | Generar la comisión mixta de PTU, el proyecto de reparto y la evidencia de pago |
| 4 | Terminación y finiquito | Generar el convenio, el recibo y los documentos de respaldo, y el precálculo neto estimado del finiquito |
| 5 | Modificación de condiciones | Documentar cada cambio de condiciones de trabajo |
| 6 | Validación de pago de PTU y aguinaldo | Alertar plazos y guardar la evidencia del pago |
| 7 | ~~Capacitación: comisión mixta y SIRCE~~ | (15/11/2026) Sale del PMV de Axia RH y pasa al proyecto de Axia CYA |
| 8 | Fonacot | Documentar la afiliación del centro de trabajo y controlar retenciones y bajas |
| 9 | Análisis de jornada | Validar jornadas, descansos y tiempo extra contra la ley y lo pactado |
| 10 | Permisos y licencias (pantalla de eventos) | Registrar permisos, licencias, incapacidades y suspensiones como fuente única de ausencias para nómina, IMSS, PTU, vacaciones, finiquito y análisis de jornada; alertar faltas y patrón de ausentismo |
| 11 | Vacaciones y aguinaldo (pantalla de eventos) | Calcular días, prima y aguinaldo; registrar solicitudes y disfrute de vacaciones como segunda fuente de ausencias justificadas; emitir VAC-2 en cada aniversario |

### Avance por módulo

| Módulo | Documentos redactados | Faltan | Situación |
|---|---|---|---|
| 1. Kit de contratación | Paquete completo (contrato A-D, módulos, kit integrado) | Pasada única con el corte del 13/11 (cláusula 22, Arial, carátula, FR-1); adenda de confidencialidad y asignación de correo; 12 variables | Versión para programación en corrido en el software (15/11/2026); **no cerrado** |
| 2. RIT y su comisión | RIT (rev. 1375), formatos FD-1 a FD-5, FR-1 y FR-2 (borrador), acta de la CMRIT (rev. 36); especificación v1.4 | Tercer corrido en el software; confirmar las propuestas 11.1; revisión de los formatos | Diseño para programación terminado; en corrido; **no cerrado** |
| 3. PTU | Kit D-01 a D-14, reglas R-1 a R-5 (precálculo neto), visor | Revisión final del usuario; verificaciones de los arts. 122 y 127, fr. VIII | Borrador completo (rev. 74) |
| 7. Capacitación | — | — | **Pasa a Axia CYA (15/11/2026)** |
| 4. Terminación | Convenio único por mutuo consentimiento, recibo, comunicados de respaldo, beneficiarios, constancia de servicios; precálculo neto; especificación v1.4 | Suspensión por temporada, incapacidad, hoja interna; encargos de la decisión 19 y de vacaciones | **Cerrado por el usuario y cargado en el software (12/11/2026)** — único módulo cerrado |
| 5. Modificación | MOD-1, MOD-2, MOD-4, MOD-5, ACT-1; especificación v1.0 con 13 casos de prueba | Correr en el software; MOD-6 (prioridad C); verificaciones | Diseño terminado (15/11/2026); **no cerrado** |
| 6. Validación de pagos | Obligaciones de pago con evidencia cotejada (CFDI o dispersión); especificación v1.0 | Correr en el software; verificaciones del SAT | Diseño terminado (15/11/2026); **no cerrado** |
| 8. Fonacot | Afiliación, cédula mensual, incidencias, retención en el finiquito, FON-1; especificación v1.0 (con el módulo 6) | Calendario de cédulas y fecha de entero | Diseño terminado (15/11/2026); **no cerrado** |
| 9. Análisis de jornada | — | Todo | **Sin conversación** |
| 10. Permisos y licencias | Catálogo de 18 eventos en cuatro familias, siete documentos y dos registros digitales; cadena de autorización; especificación v1.6 con lógica y textos | Verificaciones legales (afectan parámetros, no la estructura) | Diseño terminado (12/11/2026); especificación lista; **no cerrado** |
| 11. Vacaciones y aguinaldo | VAC-1, VAC-2, VAC-3, avisos N-1 a N-6; periodos de solicitud por antigüedad, días bloqueados y cupos; especificación v1.1 | Nuevo art. 36 del RIT; verificaciones legales; decidir el cuadro general de antigüedades | Diseño terminado (16/11/2026); **no cerrado** |

---

## Módulo 1. Kit de contratación

**Actualización 31/10/2026:** el paquete de contratación está cerrado por el usuario (contrato rev. 473, biblioteca rev. 80, visor integrado v8) y tiene versión para programación. La tabla siguiente queda como historial; la fuente vigente es el registro de decisiones.

| Documento | Estado | Prioridad |
|---|---|---|
| Contrato por tiempo indeterminado con carátula (v. 312) y biblioteca de módulos R, C, T y H (v. 33) | En revisión por el usuario | A |
| Variantes de temporalidad B (obra determinada), C (tiempo determinado) y D (temporada) | Notas de diseño en el contrato; **por incorporar** | A |
| Capacitación inicial como contrato autónomo | **Por decidir** | B |
| Perfil de puesto y lineamientos para generarlo con IA | Borrador | A |
| Aviso de privacidad para personas trabajadoras | Borrador | A |
| Aviso de privacidad para candidatos | Borrador | B |
| Convenio de confidencialidad + Anexo A | Borrador | B |
| Carta responsiva de herramientas físicas y digitales + inventario | Borrador (visor del kit v6) | A |
| Designación de beneficiarios | Borrador | A |
| Acuerdo de descuento | Borrador (otra conversación) | C |
| Constancia de recibo del RIT | **Falta** | A |
| Asignación de correo institucional | **Falta**; necesaria siempre que INTRANET = Sí | B |
| Designación del sistema de registro de jornada | Existe como sección B del Anexo 3; falta unificar con el kit | B |
| Oficio de asignación REPSE | Modelo propuesto | B |
| Adenda de confidencialidad | **Falta** | B |

**Faltantes**
- **A — Variantes de temporalidad.** El formulario debe exigir la causa de la temporalidad; sin ella, la relación se presume por tiempo indeterminado. El sistema necesita alertas de vencimiento y control de renovaciones sucesivas. Periodo de prueba solo en relaciones por tiempo indeterminado o por tiempo determinado de más de 180 días. Las labores discontinuas o de temporada son por tiempo indeterminado (art. 39-F, ya verificado por la conversación del contrato).
- **A — Unificar el Anexo 3 del contrato con el kit:** acuse de políticas, aceptación del registro de asistencia (sección B) y bloque de ubicación.
- **B — Integración pendiente de cláusulas del layout:** notificaciones, lugar de trabajo, prestaciones y perfil de puesto. Jornada, teletrabajo, híbrido y REPSE ya están integrados.

---

## Módulo 2. RIT y su comisión mixta

| Documento | Estado | Prioridad |
|---|---|---|
| Reglamento Interior de Trabajo (89 artículos, Anexo A de 60 conductas y escala, Anexo B de horarios, Anexos C y D opcionales) | **Cerrado para programación (12/11/2026)**; especificación v1.1 | A |
| Acta de integración de la CMRIT | Modelo maestro redactado; en revisión | A |
| Constancia de recibo del RIT por persona trabajadora (FR-1) | Borrador; en la especificación | A |
| Constancia de difusión (FR-2) | Borrador; en la especificación | A |
| Depósito ante el CFCRL | Autoridad verificada; falta el formato de solicitud o el registro de la constancia en el sistema | A |
| Formatos disciplinarios FD-1 a FD-5 (declaraciones manuscritas) | Borrador; en la especificación | A |

**Resuelto (12/11/2026):** formatos disciplinarios en borrador; el Anexo B se deposita de nuevo cuando cambia (art. 88); días en casa y horarios flexibles pasan a la política de trabajo híbrido (art. 22); traslado entre clientes REPSE en el art. 9.

**Dependencia del módulo 10 (permisos y licencias):** la conducta 60 (ausentismo reiterado) solo se puede seleccionar con la alerta de patrón del módulo de permisos, y la regla de evidencia no entregada del art. 31 (permisos de la tabla II) la ejecuta ese módulo con la casilla EVIDENCIA_DESCUENTO. COMISION_GOCE (fila fija de comisiones de la tabla I) se captura en el evento.

**Faltantes**
- **A — Acta de la CMRIT:** aplicar el criterio común del 02/11/2026.
- **B — Retroalimentación de la especificación v1.1** y confirmación de sus cinco propuestas de programación (11.1).

---

## Módulo 3. PTU y su procedimiento

| Documento | Estado | Prioridad |
|---|---|---|
| Kit D-01 a D-13 (integración, declaración, proyecto, observaciones, pago y contingencias; dictamen A, B o C) | Borrador completo, pendiente de revisión | A |
| Constancia de entrega de la declaración (D-05) | Borrador | A |
| Proyecto de reparto y constancia de exhibición (D-08, D-09) | Borrador | A |
| Acta de resolución de objeciones (D-10) | Borrador | B |
| Aviso sin cantidad repartible o con excepción legal (módulos A y C del dictamen) | Borrador | B |
| Constancia de pago (D-11) | Borrador; cubre parcialmente | A |
| Recibo individual de PTU | **Falta** | A |
| Control de PTU no cobrada | **Falta** como regla del sistema | B |
| Layout de importación de nómina | **Falta** | A |

**Regla del sistema que falta definir — A:** en la vía de captura, el reparto individual y el tope individual exigen días trabajados y salario devengado **por persona**. Con totales globales no se puede generar el Anexo 1 del dictamen. Propuesta en el punto 9 de las decisiones.

---

## Módulo 4. Terminación y precálculo de finiquito

**Actualización 15/11/2026:** terminado y cargado en el software con la especificación v1.4 (12/11/2026): convenio único por mutuo consentimiento, precálculo neto estimado, aviso de rescisión como servicio aparte. Ver registro 4.8.

**Actualización 31/10/2026:** el módulo tiene conversación propia y especificación para programación v1.0 («AXIARH - Modulo 4 - Especificacion para programacion»). Sus decisiones están en el registro, apartados 4.8 y 5.5. No se genera renuncia: toda salida voluntaria va por convenio, módulo B. La tabla siguiente queda como historial.

| Documento | Estado | Prioridad |
|---|---|---|
| Terminación al vencer el periodo de prueba o de capacitación | **Falta**; su candado exige el formato F-2 de la comisión | A |
| Terminación por vencimiento del plazo u obra (contratos determinados) | **Falta** | A |
| Renuncia voluntaria | **Falta** | A |
| Convenio de terminación por mutuo consentimiento | **Falta** | A |
| Aviso de rescisión | **Falta** | A |
| Acta administrativa de hechos | No se crea: la cubren FD-1, FD-2 y FD-5 del RIT (31/10/2026) | — |
| Recibo de finiquito | **Falta** | A |
| Constancia de salida | Borrador (otra conversación) | B |
| Acta de devolución y entrega de herramientas y cierre de accesos | **Falta**; documento formal propio (decisión 13) | B |
| Pago a beneficiarios por fallecimiento | **Falta**; debe seguir las reglas de reparto proporcional, abstención ante controversia y pago a menores del registro (4.3) | C |

**Conceptos del precálculo (bruto)**

| Concepto | Procede en |
|---|---|
| Salarios devengados | Siempre |
| Aguinaldo proporcional | Siempre |
| Vacaciones no disfrutadas y prima vacacional (con el porcentaje del RIT, PRIMA_VACACIONAL_PCT) | Siempre |
| PTU pendiente | Si hay reparto pendiente; ligado a D-08 B y D-11 |
| Prima de antigüedad | Despido o rescisión, con o sin causa; renuncia solo con 15 años o más |
| Indemnización constitucional y 20 días por año | Solo como escenario de negociación o de despido injustificado |

El precálculo dice «antes de impuestos y deducciones»; el recibo remite al CFDI de nómina. Cualquier descuento por daño a herramientas sigue la regla única del art. 46 del RIT (decisión 12). La devolución de herramientas se documenta con el acta, pero **no condiciona el pago del finiquito**: retenerlo por falta de devolución sería un riesgo.

**Faltantes**
- **A — Convenios y renuncias:** definir si el sistema prepara la ratificación ante el Centro de Conciliación.
- **A — Aviso de rescisión:** control del plazo y de la forma de entrega, con alerta de 5 días hábiles.
- **B — Alertas de baja ante el IMSS y ante Fonacot** (persona con crédito vigente).

---

## Módulo 5. Modificación de condiciones de trabajo

**Actualización 17/11/2026:** diseño terminado con la especificación v1.0 (registro 4.12). La matriz siguiente queda como historial; rige la sección 2 de la especificación.

| Documento | Estado | Prioridad |
|---|---|---|
| Convenio modificatorio (salario, puesto, jornada, modalidad) | **Falta** | A |
| Comunicado de cambio de centro de trabajo | Propuesto | B |
| Comunicado de aumento de salario | **Falta** | B |
| Convenio de cambio a teletrabajo o de regreso a modalidad presencial (y de paso a o desde híbrido) | **Falta** | B |
| Comunicado de modificación de días en casa del híbrido | **Falta**; con TELE_AVISO_DIAS | B |
| Constancia de entrega del perfil de puesto actualizado | **Falta**; con PERFIL_AVISO_DIAS (cláusula 1.4) | B |
| Oficio de asignación REPSE (cada rotación) | Modelo propuesto | B |
| Actualización anual de datos y de beneficiarios (coincide con la revisión anual de perfiles) | **Falta** | B |
| Aviso de sustitución patronal | **Falta** | C |

**Matriz de cambios (ajustada con el contrato el 26/10/2026)**

| Cambio | Cómo se documenta |
|---|---|
| Aumento de salario | Comunicado |
| Cambio de centro dentro del ámbito geográfico | Comunicado |
| Actualización del perfil sin cambiar la naturaleza del puesto | Aviso con PERFIL_AVISO_DIAS y constancia (cláusula 1.4) |
| Rotación REPSE con lugar de trabajo del cliente | Oficio de asignación |
| Modificar o revocar días en casa del **híbrido** | Comunicado con TELE_AVISO_DIAS (M-H.8: la base es presencial y los días son revocables) |
| Cambio a **teletrabajo** (más de 40%) o regreso a presencial desde teletrabajo | Convenio firmado |
| Cambio de puesto, funciones de distinta naturaleza o categoría superior | Convenio firmado (cláusula 1.4); sin nuevo periodo de prueba ni de capacitación |
| Cambio de jornada u horario fuera de lo pactado | Convenio firmado |
| Cualquier reducción | Convenio firmado |

---

## Módulo 6. Validación de pago de PTU y aguinaldo

- Calendario de alertas: aguinaldo con AGUINALDO_FECHA_PAGO (a más tardar el 19 de diciembre; cálculo provisional 30 días antes y validación del contador, módulo 11); PTU con las fechas calculadas del kit de PTU.
- (15/11/2026) El módulo 11 registra el pago del aguinaldo aquí, con el CFDI como evidencia; D-14 de PTU toma el UUID del estado Pagada.
- **Resuelto (15/11/2026):** ver registro 4.13. Texto anterior — **A — Definir «validar»:** el cliente marca «pagado» y sube el CFDI de nómina o la dispersión bancaria, por persona o por lote. D-11 de PTU debe usar la misma evidencia.
- Personal que ya salió: el aguinaldo va en el finiquito; la PTU del ejercicio se le debe aunque ya no trabaje (EX_TRABAJADORES del kit de PTU).
- Conservación de los comprobantes como evidencia para inspección.

---

## Módulo 7. Capacitación: comisión mixta y SIRCE

| Documento | Estado | Prioridad |
|---|---|---|
| Juego de cuatro instrumentos (convocatoria u oficio al sindicato, constancia de publicación, acta de la jornada de elección, acta de integración e instalación con Bases) | En revisión por el usuario | A |
| F-2 Opinión sobre el periodo de prueba o de capacitación | Redactado | A |
| F-1, F-3, F-4, F-5 (sesión, firma digitalizada, sustitución, informe anual) | Redactados | B |
| DC-3 (constancia de competencias) | Formato oficial; flujo de autentificación definido | A |
| Plan y programa de capacitación (DC-2) | Fuera del PMV: Axia Capacitación | — |
| Exportación para el SIRCE | **Falta**; plazos ya identificados (DC-3 en 20 días hábiles, SIRCE en 60) | B |

**Límite decidido (26/10/2026):** Axia RH cubre el SIRCE, la comisión mixta y el DC-1; DNC, plan y programa y gestión de cursos quedan en Axia Capacitación. Pendiente: confirmar si las constancias DC-3 de la capacitación inicial entran, porque las exige el candado de terminación.

---

## Módulo 8. Fonacot

**Actualización 17/11/2026:** diseño terminado con la especificación de los módulos 6 y 8 (registro 4.13). La «constancia de afiliación» no se genera: la sustituye la ficha de afiliación con el convenio del Instituto. La tabla siguiente queda como historial.

| Documento o función | Estado | Prioridad |
|---|---|---|
| Constancia de afiliación del centro de trabajo | **Falta** | A |
| Alerta para la afiliación de empresas nuevas | **Falta** | A |
| Control de retenciones y entero | **Falta** | B |
| Aviso de baja de personas con crédito vigente | **Falta**; se conecta con el módulo 4 | B |

Decidido (26/10/2026): el PMV solo alerta y guarda evidencia; no calcula retenciones. Verificar en las reglas vigentes del Instituto Fonacot los plazos antes de fijar las alertas.

---

## Módulo 9. Análisis de jornada

- Validar la jornada pactada y la real contra el máximo por tipo de jornada y año, el descanso semanal y en jornada continua, el tiempo extra, la prima dominical, los descansos y festivos trabajados, y el tiempo de comida que cuenta como jornada.
- Reglas ya fijadas por el RIT: horas extra solo con orden previa (el tiempo sin orden se paga); tolerancia TOLERANCIA_MIN. (12/11/2026) El usuario retiró la regla del efecto del retardo.
- (12/11/2026) Las ausencias sin evento del checador alimentan las alertas de faltas y de patrón de ausentismo del módulo 10; la lactancia reduce la jornada esperada.
- **Verificar** si la reforma de 2026 cambió los límites del tiempo extra y esperar las disposiciones de la STPS del registro electrónico (vigencia: 1 de enero de 2027).
- **Decidido (26/10/2026):** los datos salen del archivo del reloj checador del cliente. **A — Falta** definir el layout de importación (persona, fecha, entradas y salidas) y qué formatos de checador se aceptan.

---

## Módulo 10. Permisos y licencias

**Alta en el mapa (12/11/2026).** Es la pantalla de eventos que el registro ya reconocía (26/10/2026). Conversación propia, separada del RIT. Diseño: «AXIARH — Módulo de permisos y licencias (diseño)» (https://claude.ai/artifact/CzspqdB6hqBzpXk5r9UgKB). Especificación para programación: «AXIARH - Módulo de permisos y licencias - Especificación para programación», v1.4 del 12/11/2026, con lógica y textos, armonizada con el registro, el mapa y el RIT v1.1. Cadena de autorización y firma de la Empresa por RH designado: registro 4.9. Estado y decisiones: «Corte - Módulo de permisos y licencias».

| Documento o función | Estado | Prioridad |
|---|---|---|
| Catálogo de 18 eventos: A permisos, B licencias, C incapacidades del IMSS, D suspensiones del art. 42 | Terminado | A |
| Registros digitales SP-1 (permiso) y SUS-3 (reincorporación); notificación LIC-2 con acuse | Terminado | A |
| Documentos LIC-1 (lactancia), LIC-3 (licencia sin goce), INC-1 (aviso de accidente), INC-2 (transferencia de semanas prenatales), SUS-1 y SUS-2 (suspensiones) | Terminado | A |
| Alertas de faltas (ventana de 30 días) y de patrón de ausentismo | Terminado | A |

**Regla central:** el evento es la única fuente de ausencias para nómina, IMSS, PTU, vacaciones, finiquito y análisis de jornada.

**Lo que depende de este módulo**
- **RIT:** la conducta 60 del Anexo A y la regla de evidencia no entregada del art. 31.
- **PTU:** días computables (registro 4.7), en lugar de los «eventos de incidencias» que el kit de PTU dejó como dependencia.
- **Módulo 4:** situaciones protegidas (agrega B3), doble confirmación de la baja con B4 vigente y aviso de rescisión por SUS-2 vencido (fr. XIV Bis).
- **Módulo 9:** ausencias sin evento del checador y jornada reducida por lactancia.
- **Firma electrónica:** SP-1, SUS-3 y el acuse de LIC-2 se apoyan en el «Corte - Firma electrónica». Falta que su especificación admita como firmante a la persona de RH designada (FIRMANTES_EMPRESA).
- **RIT:** la cadena de autorización incluye los permisos legales, sin opción de negarlos; el art. 30, el art. 16 y la tabla II deben armonizarse.

**Pendientes:** solo verificaciones legales (sección 7 del corte), que afectan parámetros y no la estructura.

---

## Módulo 11. Vacaciones y aguinaldo

**Alta en el mapa (15/11/2026).** Pantalla de eventos con conversación propia. Especificación: «AXIARH - Módulo de vacaciones y aguinaldo - Especificación para programación», v1.0, con los textos aprobados. Decisiones: registro 4.10 y «Corte - Módulo de vacaciones y aguinaldo».

**Lo que depende de este módulo**
- **Permisos (módulo 10):** VAC-1 es la segunda fuente de ausencias justificadas; un solo evento por día; la incapacidad prevalece e interrumpe las vacaciones. AGUINALDO_COMPUTA lo administra este módulo. (Aplicado en la especificación de permisos v1.6.)
- **RIT:** art. 36 con VAC_PROGRAMACION_MODO (aplicado en la v1.4).
- **Módulo 4:** saldos, proporcionales y prescritos (solo informativos); no duplicar el aguinaldo ya pagado.
- **Módulo 6:** registro del pago del aguinaldo con CFDI.

---

## Hilos que deben ir en el mismo sentido en todas las conversaciones

| Hilo | Documentos que toca | Regla común |
|---|---|---|
| Perfil de puesto | Contrato, lineamientos, periodo de prueba, terminación, modificación, RIT, comisión de capacitación | Versionado; generado por IA con validación humana; el firmado no cambia; es la base de la evaluación y de la detección de necesidades de capacitación |
| Comisión Mixta de Capacitación | Contrato (Cláusula Tercera, 3.3 a 3.6), formato F-2, terminación, DC-3, SIRCE | Su opinión (o la constancia de que se solicitó) es requisito de la terminación al vencer el periodo; el contrato no regula la opinión |
| Comisiones mixtas (RIT, capacitación, PTU) | Las tres actas de integración | Misma estructura de instalación más bases; mismo criterio de designación y número de representantes (decisión 3) |
| Temporalidad | Contratos de todo tipo, alertas, terminación, PTU (eventuales) | La causa de la temporalidad se captura siempre; las renovaciones se controlan |
| Procedimiento disciplinario | RIT, Anexo A, formatos disciplinarios, aviso de rescisión, carta responsiva, módulo de permisos | Mismos formatos para sanción, para determinación de responsabilidad por daño y para la propuesta de rescisión; la conducta 60 nace de la alerta de patrón del módulo de permisos |
| Beneficiarios | Kit, cláusula 19, actualización anual, fallecimiento, finiquito | Una sola designación vigente; suma 100%; reparto proporcional si fallece una persona designada |
| Confidencialidad | Contrato (cláusula 14), RIT (conductas 36, 39, 56 y 58), convenio, adenda, terminación | Cláusula base para todos; convenio solo para acceso calificado; misma definición de reproducción y extracción |
| Jornada | Contrato, RIT (Anexo B), registro electrónico, análisis de jornada, finiquito | El contrato fija lo pactado; las reglas operativas van en el RIT; los horarios salen de un solo catálogo (decisión 5) |
| Datos personales | Aviso de privacidad, Anexo 3, RIT, comisiones, PTU | Un solo aviso que cubre salud, pruebas, biométricos, ubicación, nómina para PTU y firmas de conformidad (decisión 7) |
| Firma y evidencia | Todos | FIRMA_MODALIDAD y la misma cláusula de firma electrónica en todos los documentos |
| Notificaciones | Todos | Correo personal de la carátula; lo legalmente formal (rescisión) sigue su propia forma |

---

## Decisiones que necesita el usuario

Contradicciones entre conversaciones, con la propuesta de Cerebro. Responder «aprobado» por número, o indicar otra solución.

**Resueltas el 26/10/2026:**
- Aprobadas como se proponen: 1, 2, 3, 7, 9, 10, 11, 12, 16, 17 y 18.
- 5: el software ya tiene catálogo de horarios; el Anexo B y la cláusula de jornada salen de él.
- 6: la periodicidad de pago viene del perfil de puestos, no del alta.
- 8: sin alerta automática ni variable de días; el F-2 se imprime junto con los documentos de terminación.
- 13: **cambia la propuesta**: habrá un acta formal de devolución y entrega como documento propio del módulo 4.
- 14: el sistema exige 100%, pero el documento conserva la regla de partes iguales con fines informativos.
- 18: el logo del cliente se ofrece en otro nivel de servicio.

- 4: resuelta; el software ya maneja los eventos en pantallas propias (baja, permisos y licencias, contratos, PTU, vacaciones y aguinaldo).

**Pendiente:** 15 (el usuario lo revisará).

**Resuelta el 15/11/2026 — 19 (aprobada como se propone).** Situaciones protegidas en la baja. El módulo 4 v1.4 (decisión del usuario del 10 y 12/11) eliminó el bloqueo por situaciones protegidas y su mensaje. El módulo de permisos (decisión 6 del usuario, 12/11) envía SITUACION_PROTEGIDA para bloquear la baja (incapacidad en curso, maternidad, lactancia, Declaración Especial de Ausencia y licencia por hijo con cáncer) y pide doble confirmación con comisión permanente vigente (BAJA_CONFIRMACION_B4). **Propuesta de Cerebro:** respetar la decisión del módulo 4 (sin bloqueo) y convertir SITUACION_PROTEGIDA en una alerta crítica que exige doble confirmación con registro de quién confirma, igual que B4. Así no se impide operar, pero queda constancia de que la Empresa conocía la situación y decidió continuar.

| # | Contradicción | Propuesta de Cerebro |
|---|---|---|
| 1 | **Marca de variables en el texto.** El registro fija MAYÚSCULAS sin delimitador; el RIT y la PTU usan {{MAYÚSCULAS}}; las condiciones aparecen como [SI], ⟦SI⟧, [[SI]] u «Opcional —». | Nombre en MAYÚSCULAS_CON_GUION_BAJO y, dentro del texto, entre llaves dobles: {{REGISTRO_GEOLOC}}. Condiciones siempre [SI condición] … [FIN SI]. Las llaves le permiten al ingeniero localizar cada variable sin ambigüedad. |
| 2 | **Términos definidos en instrumentos colectivos.** El RIT, la comisión de capacitación y la PTU usan «el patrón» y «personas trabajadoras» en minúscula. | «la Empresa» en todos los documentos, salvo citas legales y denominaciones legales de las comisiones. En instrumentos colectivos, «las personas trabajadoras» en plural y minúscula; «la Persona Trabajadora» queda para documentos individuales. |
| 3 | **Designación de representantes obreros.** La CMRIT es por designación sin elecciones; la comisión de capacitación y la de PTU, por votación secreta. El número de representantes también difiere. | Votación para capacitación y PTU, porque sus actos afectan a cada persona (terminación del periodo y reparto) y su legitimidad será impugnada; **una sola jornada de elección** para ambas comisiones. La CMRIT conserva la designación con conformidad, o se elige en la misma jornada si el cliente quiere. Número: una variable común de representantes por parte (mínimo 1), igual en las tres. El personal de confianza vota y no es candidato en las tres. |
| 4 | **Datos que no caben en los tres niveles:** elecciones, sesiones, opiniones, ejercicio de PTU, terminaciones y modificaciones. | Agregar un **cuarto nivel: procedimientos y eventos**, que captura RH o consultoría cada vez que ocurren y que usa los datos de los niveles 1 a 3 sin repetirlos. |
| 5 | **Horarios.** El registro los define por puesto; el Anexo B del RIT, por centro y turno. | Catálogo de turnos en la configuración de la empresa (centro, nombre, tipo de jornada, días, entrada, salida, comida, descanso). Cada puesto se liga a uno o varios turnos. El Anexo B y la cláusula de jornada salen del mismo catálogo. |
| 6 | **Periodicidad de pago.** El registro la captura por persona; el RIT, como variable de empresa. | La empresa habilita las periodicidades y los días de pago; el alta elige entre las habilitadas (solo semanal en trabajo material); el RIT lista las habilitadas. |
| 7 | **Biométricos y ubicación.** El kit decidió que no dependen del consentimiento; el Anexo 3 del contrato da opción de negarse y un medio alterno; el registro habla de consentimiento separado. | Riesgo, explicado una vez: los datos biométricos pueden ser datos sensibles que requieren consentimiento expreso conforme a la LFPDPPP 2025 (verificar el texto vigente). Propuesta: la **ubicación** sin opción de negarse, fundada en la relación de trabajo y el registro de jornada; los **biométricos** con consentimiento expreso y un medio alterno (PIN o tarjeta) mientras se verifica la ley. El aviso y el Anexo 3 deben decir lo mismo. |
| 8 | **Alertas de la comisión de capacitación.** DIAS_AVISO es configurable en la Base 14; el registro fija alertas no configurables. | Sin variable: la Base 14 dice que la Empresa solicita la opinión con la anticipación que fija el sistema, y el sistema la solicita con la alerta de 3 semanas antes del vencimiento. |
| 9 | **PTU por captura.** Con totales globales no se calcula el reparto individual ni el tope. | La vía de captura pide, por persona, días trabajados y salario devengado del ejercicio; no se admiten solo totales globales. |
| 10 | **Pendientes de diseño de la PTU.** | El personal de confianza vota (igual que en capacitación); el tiempo en cualquier comisión mixta es tiempo de trabajo con goce de salario; el dictamen tiene una versión publicable sin salario diario (nombre, días computables y monto), y la versión completa queda a disposición de la comisión y de cada persona respecto de sus propios datos. |
| 11 | **Procedimiento previo a la rescisión.** El RIT lo deja facultativo, pero lo lista como pendiente. | Facultativo, como está. Un procedimiento obligatorio autoimpuesto puede volverse en contra de la Empresa si no se sigue; confirmar con la búsqueda de criterios judiciales que ya está en pendientes. |
| 12 | **Descuentos por daño.** La carta responsiva prohíbe compensar con salario o finiquito; el art. 46 del RIT permite el descuento con autorización previa firmada en el resguardo. | Una sola regla: el descuento procede solo si el Comité determina la negligencia con audiencia, existe la autorización previa firmada y se respetan los límites legales. La carta responsiva remite al art. 46 en lugar de prohibir. |
| 13 | **Acta de devolución de equipo.** El mapa la tenía como documento faltante; el inventario ya tiene fila de devolución y cancelación de accesos. | (Sustituida) Acta formal de devolución y entrega como documento propio; no condiciona el pago del finiquito. |
| 14 | **Beneficiarios.** El formulario exige que sumen 100%; el documento prevé partes iguales si no suman 100%. | Quitar del documento la regla de partes iguales; el sistema no permite generar una designación que no sume 100%. Se conserva el reparto proporcional por fallecimiento. |
| 15 | **Lineamientos frente al perfil de puesto.** Los lineamientos regulan 10 apartados, piden «a quién reporta», dicen «hasta 180 días» y activan teletrabajo desde el perfil. | Manda el formato del perfil (8 apartados, sin «Reporta a»). Los lineamientos se ajustan: periodo fijo según el atributo del puesto, y el perfil solo indica si el puesto admite días en casa (TELE_APTO); el módulo lo activa el alta. |
| 16 | **Repeticiones de la ley en el RIT** (reposo de 30 minutos, cómputo del tiempo de comida). | Aceptarlas como excepción operativa, porque el RIT debe poder aplicarse sin consultar la ley. Agregar la excepción a la convención de la sección 10 de las instrucciones. |
| 17 | **Coordinación de la comisión de capacitación.** El registro la fija como patronal; la Base 9 permite que la secretaría la supla. | La secretaría puede suplir solo para convocar y conducir una sesión, sin cambiar la titularidad de la coordinación. |
| 18 | **Marca en los documentos.** Algunos títulos dicen «AEXIS» y el registro usa «AXIARH». | Los documentos generados para el cliente no llevan marca del sistema. AEXIS o AXIARH solo en notas internas. |

---

## Revisión de las pantallas del software (26/10/2026)

Hallazgos para el ingeniero, de mayor a menor riesgo.

**Respuestas del usuario (26/10/2026):** 1, alerta y nueva firma del perfil cuando cambie, extendida a jornada, salario y prestaciones (aprobada); 3, máximos por año aceptados; 7, salario fijo por puesto; 4, catálogo de clientes REPSE (aprobado; abajo); 10 y 11, aceptados; 12, la comisión de seguridad e higiene se quita por ahora.

**Propuesta para el hallazgo 4 (centro de trabajo REPSE):** eliminar el centro genérico «Instalaciones del beneficiario»; crear en la configuración de la empresa un catálogo de clientes REPSE (razón social, RFC, domicilio de cada instalación, fecha y número del contrato de servicios, actividad REPSE que se presta); en el alta, con REPSE = Sí y lugar Cliente, el centro de trabajo se elige de las instalaciones de ese catálogo, su domicilio se imprime en el contrato y se genera el oficio de asignación; cada reasignación es un nuevo oficio desde el módulo 5.

**Jurídicos**
1. **Cambios al catálogo que alteran contratos vigentes.** «Si cambias una jornada, se actualizan los puestos que la usan» (y lo mismo al editar un puesto, sus prestaciones o el tabulador). Para las personas ya contratadas eso es una modificación de condiciones de trabajo: debe aplicarse solo a altas nuevas, o disparar el módulo 5 (comunicado o convenio según la matriz) para cada persona afectada, nunca cambiar en silencio sus condiciones.
2. **Motivo «Despido injustificado» en la baja.** Registrarlo en el sistema de la empresa es una confesión. Los motivos deben ser las formas legales de terminación; la indemnización se muestra como escenario de negociación.
3. **Límites de jornada fijos.** La pantalla «Lo que marca la LFT» muestra 48, 42 y 45 horas. Desde el 1 de enero de 2027 el máximo diurno es 46; debe usarse la tabla por año del registro (5.4).
4. **«Instalaciones del beneficiario del servicio» como centro de trabajo sin domicilio.** Con REPSE_LUGAR_TIPO = Cliente, el centro es el domicilio del cliente del oficio de asignación; un centro genérico no se puede imprimir en el contrato.
5. **Seguro de vida como prestación.** Si existe, la designación de beneficiarios debe advertir que los del seguro se designan en el formato de la aseguradora.
6. **Comisión mixta de capacitación:** la leyenda dice «obligatoria con más de 50»; también lo es si la empresa usa periodo de prueba o capacitación inicial.
7. **Tabulador por rango (mínimo y máximo) frente a «salario predeterminado».** Pendiente de decisión. Si hay rango, conviene documentar el criterio para ubicar a cada persona (antigüedad, desempeño) por el principio de igual salario por trabajo igual; el puesto de prueba ya muestra $315.04 a $872.73 para el mismo puesto.

**Del sistema**
8. Horario y horas por semana se escriben a mano: deben calcularse de los días y horas de entrada y salida, y el descanso semanal validarse contra los días laborados (el puesto de prueba dice 46 horas con «9 a 5» de lunes a sábado medio día, y descanso rotativo con días fijos).
9. El mínimo de 30 minutos de descanso aplica a la jornada continua; la leyenda lo exige siempre.
10. Faltan en «Agregar puesto»: periodicidad de pago (decidido: viene del puesto), sistemas y plataformas, información confidencial, propiedad intelectual del catálogo, puesto crítico para la seguridad y áreas con riesgo para embarazo, lactancia o menores.
11. Faltan en «Alta de la empresa»: folio, vigencia y actividades REPSE, correo para datos personales, dominio de correo institucional, forma y día de pago, afiliación a Fonacot, autoridad de inspección (federal o local) y la opción de varios registros patronales.
12. La comisión de seguridad e higiene aparece como pendiente en Axia RH, pero es materia de Axia NOMs (NOM-019). Decidir si en el PMV solo se alerta.
13. Sin validación de dígito verificador en registros anteriores (CURP de «amir»), y la ficha muestra «Forma de pago: Semanal» (es la periodicidad).

---

## Encargos vigentes (actualizado el 15/11/2026)

Cada conversación lee aquí lo que le toca cuando el usuario le dice «revisa el registro».

**RIT y CMRIT**
- Cumplidos según el corte del 15/11/2026: encargos 1 a 11 (incluidos el acta de la CMRIT con el criterio común, días computables, art. 30, art. 16 y tabla II, y firma de FR-1).
12. (15/11) El documento del Comité de Integridad y Disciplina se redacta en Axia Compliance; el RIT solo conserva la remisión del art. 79 y COMITE_INTEGRANTES como catálogo interno.
13. (17/11, encargo del usuario desde vacaciones) **Art. 36**: primer párrafo condicionado a los tres valores de VAC_PROGRAMACION_MODO (Calendario anual, texto vigente; Periodos de solicitud por antigüedad; A solicitud) y párrafo nuevo para todos los modos sobre días bloqueados y cupos, con la redacción propuesta en la sección 4 del «Corte - Módulo de vacaciones y aguinaldo». Conservar el disfrute continuo del periodo mínimo, la distribución del resto, la prohibición de compensar con dinero y la remisión al art. 30. Cambiar el modo con el RIT depositado exige nuevo depósito.
14. (17/11, del módulo 5) Especificación 2.6: el comunicado de horarios ajustados por reducción legal es MOD-2 «Ajuste legal de jornada» del módulo 5; el anexo de horarios lee la jornada de cada persona solo para el resumen.

**Paquete de contratación**
1. (12/11) Carta responsiva: valor de reposición por bien y autorización previa del descuento; remitir al art. 46 por su nombre o REF_ART_n, no por número (el RIT renumera).
2. (12/11, ampliado) Aviso de privacidad para personas trabajadoras: expedientes disciplinarios y declaraciones manuscritas, resultado confirmado de las pruebas, confidencialidad de los exámenes, expediente clínico por 2 años, incapacidades (folio, ramo, fechas), constancias de detención, Declaración Especial de Ausencia y datos de la bitácora de firma (IP, dispositivo, correo, celular).
3. (15/11) Aplicar a la cláusula 22 las instrucciones del apartado 9 del «Corte - Firma electrónica».
4. (15/11) Aplicar en una sola pasada las decisiones del corte del 13/11 (Arial, carátula de 1 a 2 páginas, FR-1 en el paquete y RIT_ENTREGA condicionada) y regenerar la versión para programación solo cuando el usuario lo pida.

**Paquete de contratación**
6. (18/11, de firma electrónica) Aviso de privacidad (Anexo 4): agregar la finalidad y la casilla de consentimiento de la verificación de identidad con INE y video de aceptación, solo en la contratación y solo con IDV_SERVICIO = Sí, y los datos de la bitácora de firma.
5. (17/11, del módulo 5) Cláusula 1.4, cierre: «ningún cambio disminuirá el salario» choca con la reducción por convenio (registro 4.12); limitarla a los mínimos legales y a lo devengado. La carátula imprime SALARIO_PERSONA.

**Comisión de capacitación:** (15/11/2026) sale de Axia RH y pasa al proyecto de Axia CYA, que hereda los encargos pendientes (criterio común de comisiones, corte pendiente desde el 26/10, SIRCE). Axia RH solo necesita que Axia CYA mantenga las variables F2_* que lee el módulo 4.

**Kit de PTU**
1. (17/11, de los módulos 6 y 8) Regla R-3: «Pagada» = CFDI o dispersión cotejados en el módulo 6; la firma de D-14 deja de ser condición del estado (D14_FIRMADO, alerta sin revertir). D-14 toma UUID_CFDI, FECHA_PAGO, FORMA_PAGO y REFERENCIA_DISPERSION de la obligación en «Pagada»; con dispersión sin UUID se genera sin el folio fiscal y se versiona al cargarlo.
2. (17/11) D-11, Parte 2: su Anexo 1 sale del módulo 6, sin cambio de texto.
3. (17/11, del módulo 5) Leer SALARIO_PERSONA y la versión de condiciones de cada persona.

**Módulo 4 (terminación)**
1. (15/11, decisión 19) Recibir SITUACION_PROTEGIDA del módulo de permisos como alerta crítica, sin bloqueo, con doble confirmación y registro de usuario, fecha y hora (BAJA_CONFIRMACION_PROTEGIDA, nueva, evento de baja); B4 con la misma mecánica (BAJA_CONFIRMACION_B4). Nunca se imprime.
2. (15/11) Adoptar la sección 11 de la especificación de vacaciones (saldos, proporcionales y prescritos solo informativos) y no duplicar el aguinaldo ya pagado en el año.
3. (15/11) Sección 7.7, regla 2 del acta de devolución: actualizarla al art. 46 vigente del RIT (investigación por los arts. 80 y 81; descuento con reconocimiento en FD-5 o determinación en FD-3, conforme al art. 27).
4. (15/11) Referencias al «Anexo A» del RIT como catálogo de conductas: decir «catálogo de conductas del RIT», sin letra.
5. (12/11) SUS-2 vencido (art. 47, fr. XIV Bis) es antecedente del aviso de rescisión, que es servicio aparte.
6. (17/11, de los módulos 6 y 8) Enviar al módulo 6 la evidencia del pago capturada en el cierre de la baja (comprobante del Anexo 2 y CFDI), con su cotejo; lo que el módulo 4 exige para cerrar no cambia.
7. (17/11) Renglón automático «Crédito Fonacot»: solo la amortización del último periodo de salario pagado (FONACOT_RETENCION_FINIQUITO), con aviso si supera la retención mensual de la cédula. En fallecimiento, sin renglón de Fonacot y con alerta del aviso de defunción (15 días hábiles).
8. (17/11) FONACOT_AVISO_DIAS = 5 días hábiles por omisión (convenio, cláusula Quinta); quitar «pendiente de verificar». La alerta es la misma incidencia de baja del módulo 8.
9. (17/11) Con FONACOT_AVISO_PERSONA = Sí y FONACOT_CREDITO = Sí, agregar FON-1 al paquete de baja (salvo fallecimiento).
10. (17/11, de vacaciones) Al dar de baja, liberar el cupo de los bloques de vacaciones que se cancelan.
11. (17/11, del módulo 5) Leer SALARIO_PERSONA y la versión de condiciones de la persona en el precálculo.

**Módulo 10 (permisos y licencias)**
1. (15/11, decisión 19) SITUACION_PROTEGIDA ya no bloquea la baja: el módulo 4 la muestra como alerta crítica con doble confirmación. Ajustar la sección 11 de la especificación.
2. (15/11) AGUINALDO_COMPUTA: B3 ya está decidido (no computa, decisión del usuario en el módulo de vacaciones); quitar «pendiente de decisión».
3. (15/11) Confirmar la lectura de SUSP_VACACIONES_GENERA que propone la especificación de vacaciones (3.1, paso 4).
4. (15/11) La conducta 60 es del catálogo de conductas del RIT (ya no «Anexo A»).
5. (17/11, del módulo 5) Registrar INCAPACIDAD_PARCIAL e INCAPACIDAD_PARCIAL_FECHA al cerrar C2 (situación protegida del módulo 5). Proponer si una reubicación aceptada en D4 (constancia MOD-5) evita SUS-2.
6. (17/11, de vacaciones) Admitir el valor «Cupo completo» de NEGATIVA_CAUSA, que solo usa el módulo de vacaciones.

**Módulo 11 (vacaciones y aguinaldo)**
1. (15/11) VAC_PROGRAMACION_MODO sin valor por omisión (regla general de pantalla del RIT), con una sola captura compartida con el RIT.
2. (17/11, de los módulos 6 y 8) Al registrarse una baja con AGUINALDO_VALIDADO y sin pago, avisar al contador que la persona sale de la nómina anual; el módulo 6 cancela su obligación con motivo «Pago en finiquito».
3. (17/11, del módulo 5) Leer SALARIO_PERSONA para la prima vacacional y el aguinaldo.

**Módulo 5 (modificación de condiciones):** sin encargos; TELE_AVISO_DIAS queda confirmada como variable de empresa (registro, sección 2).

**Módulo 9 (análisis de jornada)**
1. (17/11, del módulo 5) La jornada esperada se toma de la versión de condiciones de cada persona y de las constancias MOD-5 vigentes.

**Firma electrónica**
1. (12/11) Cumplido en la v1.2: firmante de RH designado.
2. (13/11) Agregar a la lista de firma autógrafa obligatoria el RIT y el acta de la CMRIT (depósito), FD-1 a FD-5 y FR-2; confirmar que la FR-1 sigue FIRMA_MODALIDAD en sus tres momentos.
4. (18/11, decisión del usuario) La verificación con INE y video es solo para la contratación: quitarla del cambio de correo o teléfono (secciones 5.7 y 5.9, encabezado de cambios de la v1.3 y guion de cambio de medio); ese cambio se verifica de forma presencial. Generar la v1.4.
5. (18/11) Aviso de privacidad: el encargo de agregar la finalidad y la casilla de consentimiento de la verificación con INE y video pasa al paquete de contratación (ver su encargo 6).
3. (17/11, del módulo 5) Tabla de la sección 11: MOD-5 «RH designado»; ACT-1 sin firma (registro digital); MOD-1 representante y MOD-2 y MOD-4 RH designado (ya previstos como convenios, comunicados y oficio de reasignación). FON-1: firma autógrafa de recibido.

## Encargos por conversación (historial del 26/10/2026)

Pegar en cada conversación después de que el usuario resuelva las decisiones anteriores.

**Contrato**
- Incorporar las variantes de temporalidad B, C y D con la causa obligatoria, y las reglas de prueba en tiempo determinado.
- Unificar el Anexo 3 con el kit (bloque de ubicación según la decisión 7).
- Integrar notificaciones, lugar de trabajo, prestaciones y perfil de puesto.
- Comparar la cláusula 19 con el documento de beneficiarios.
- Aplicar las decisiones 1, 5 y 6.

**Kit de contratación**
- Ajustar la carta responsiva: disparador con híbrido (ya en el registro) y remisión al art. 46 del RIT (decisión 12).
- Aviso de privacidad: cubrir datos de salud, pruebas de alcohol y drogas, exámenes médicos, firmas de conformidad de la CMRIT y uso de datos de nómina por la comisión de PTU; resolver biométricos (decisión 7).
- Ajustar lineamientos de perfiles (decisión 15) y beneficiarios (decisión 14).
- Redactar la asignación de correo institucional y la adenda de confidencialidad.

**RIT y CMRIT**
- Normalizar términos y marcas (decisiones 1 y 2); convertir los artículos 22, 34 y el transitorio segundo a [SI] … [FIN SI].
- Aplicar las decisiones 3, 5, 6, 11 y 16.
- Redactar los formatos disciplinarios, la constancia de recibo y la constancia de difusión.
- Regular días en casa, registro de jornada en días en casa y traslado entre clientes REPSE.

**Comisión de capacitación**
- Normalizar términos y marcas (decisiones 1 y 2).
- Aplicar las decisiones 3, 8 y 17; corregir la referencia a la «Cláusula Cuarta» (ahora Tercera, 3.3 a 3.6) y retirar la dependencia del aviso de privacidad sobre SIRCE.
- Sin cláusula de opinión en el contrato: el vínculo vive en la Base 14, el F-2 y el candado del sistema.

**PTU**
- Normalizar términos y marcas (decisiones 1 y 2); renombrar TIPO_PATRON a EMPRESA_TIPO_PERSONA.
- Aplicar las decisiones 3, 9 y 10.
- Redactar el recibo individual, el control de PTU no cobrada y el layout de importación de nómina; ligar D-11 con la evidencia del módulo 6 y con el finiquito.

**Conversaciones por abrir:** terminación y finiquito (módulo 4), modificación de condiciones (módulo 5), y reglas del sistema para validación de pagos, Fonacot y análisis de jornada (módulos 6, 8 y 9).

---

## Pendientes transversales

- **Resuelto (12/11/2026) — Firma electrónica:** ver registro 4.11 y la especificación v1.2. Texto anterior: definir el tipo de firma y cómo se conserva la prueba de integridad y fecha (por ejemplo, constancia de conservación conforme a la NOM-151). Hoy se cotiza aparte. (12/11/2026) Ya existe «Corte - Firma electrónica» y el módulo 10 ya lo usa (registros SP-1 y SUS-3 y acuse de LIC-2): bitácora, hoja de evidencias, SHA-256, copia al correo personal, NOM-151 opcional y firma autógrafa si falla la Plataforma.
- **A — Tabla de conservación de documentos:** unificar plazos; el RIT ya fija variables para expedientes disciplinarios y clínicos y la comisión de capacitación tiene la suya.
- **B — Parámetros legales globales** (UMA, ISR, subsidio, salarios mínimos, cuotas, exenciones, duraciones legales): una sola tabla versionada con monitor y aprobación (módulo 4, 5.3), compartida por PTU, vacaciones y aguinaldo, permisos y jornada.
- **B — Registro electrónico de jornada:** el contrato obliga a usar el sistema que designe la Empresa, pero la app del colaborador es fase 2.
- **B — Diccionario de variables único** al terminar los modelos; hay variables duplicadas con distinto nombre (SINDICATO en capacitación y PTU, CENTROS y TURNOS, N_REP y NUM_REP_TRAB, TIPO_PATRON y EMPRESA_TIPO_PERSONA). (12/11/2026) Además: PERSONA_JEFATURA es la jefatura inmediata y DIRECTOR_AREA (nueva) la dirección del área, ambas por puesto; JEFE_INMEDIATO se elimina; FIRMANTES_EMPRESA va en la configuración de la empresa; CENTRO_TRABAJO equivale a PERSONA_CENTRO del RIT; DIAS_EN_CASA_EMPRESA y DIAS_EN_CASA_ACTIVO son distintas.

## Decisiones de alcance

Tomadas el 26/10/2026: entran la comisión mixta de capacitación, todo tipo de contratos, Fonacot, SIRCE y análisis de jornada; la PTU se calcula por importación o captura; el finiquito se precalcula bruto.

Tomadas también el 26/10/2026:
- La capacitación inicial es solo una cláusula del contrato.
- De capacitación, Axia RH cubre el SIRCE, la comisión mixta y el DC-1; lo demás queda en Axia Capacitación.
- Fonacot: solo alertas y evidencia.
- Análisis de jornada: datos del reloj checador del cliente.

Pendiente de confirmar: si las constancias DC-3 de la capacitación inicial entran a Axia RH, porque el candado de la terminación las exige y el SIRCE las reporta.

## Orden sugerido de trabajo (17/11/2026)

1. Correr en el software los módulos 5, 6 y 8 y la especificación v1.1 de vacaciones.
2. RIT: nuevo art. 36 (encargo 13) y tercer corrido.
3. Paquete de contratación: corrido en el software y pasada única con el corte del 13/11 y la cláusula 1.4.
4. Módulo 9, análisis de jornada (conversación por abrir).
5. Cerebro: diccionario único de variables y tabla única de parámetros legales.
6. Revisión final y cierre de cada módulo por el usuario (hoy solo el módulo 4 está cerrado).

Historial: el orden del 26/10 se cumplió en sus pasos 1 a 5 y 7.
