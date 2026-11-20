# AXIARH — Registro de decisiones de los documentos maestros

Actualizado: 20 de noviembre de 2026 · Responsable: Damián Torres

Este documento es la base de todas las conversaciones del proyecto. Reúne el catálogo de documentos maestros, la arquitectura del sistema, las decisiones tomadas por documento y las reglas que el sistema debe aplicar. Todas las aprobaciones son **provisionales** hasta la revisión final de cada documento. Cuando una conversación tome una decisión nueva, se agrega aquí con su fecha. Las contradicciones entre conversaciones y su propuesta de solución están en «Axia RH - Mapa del PMV».

---

## 1. Catálogo de documentos maestros

| Documento | Grupo | Se genera | Estado |
|---|---|---|---|
| Paquete de contratación: contrato con carátula (tipos A indeterminado, B obra, C tiempo determinado, D temporada), biblioteca de módulos y kit integrado | Contratación | Siempre | **Cerrado por el usuario (26/10/2026)**; ajustes del 28/10, 31/10, 13/11, 15/11 y 17/11/2026 aplicados. Contrato rev. 501, biblioteca rev. 91. (20/11/2026) **Versión para programación vigente: la del 20/11/2026** (202 variables; incluye todos los cambios del 17/11 y sustituye a la del 15/11, de 203 variables, que ya no debe usarse). Sin los encargos 6 y 7 del mapa. Visor del paquete (v9) desactualizado |
| Perfil de puesto (Anexo 1 del contrato) | Contratación | Según PERFIL_MODALIDAD: solo con «Perfil de puesto»; lo genera la IA del sistema con los lineamientos y lo valida una persona | Cerrado con el paquete |
| Lineamientos para generar perfiles de puesto | Sistema | Base de la IA que genera los perfiles | Borrador |
| Aviso de privacidad para personas trabajadoras (Anexo 4) | Contratación | Siempre | Cerrado con el paquete; ajuste del 31/10 aplicado (pruebas y exámenes); ampliado el 17/11/2026 (ver 4.3 bis) |
| Aviso de privacidad para candidatos | Reclutamiento | En reclutamiento | Borrador (en el visor del kit; el documento de Claude Docs ya no es vigente) |
| Convenio de confidencialidad (+ Anexo A de información, activos y accesos) | Contratación (módulo) | Nivel de acceso «Calificado» | Borrador |
| Adenda de confidencialidad | Contratación | Personal contratado antes de adoptar el kit | Redactada (kit 3.8) |
| Carta responsiva de herramientas físicas y digitales (+ anexo de inventario) | Contratación | Hay equipo asignado, días en casa (teletrabajo o híbrido), correo institucional o sistemas asignados al puesto | Borrador |
| Designación de beneficiarios | Contratación | Siempre | Borrador |
| Acuerdo de descuento | Contratación | Hay descuento capturado | Borrador; se trabaja en otra conversación |
| Constancia de recibo del RIT (FR-1) | Contratación | En la emisión, en cada alta y en cada modificación; no se genera sin acuse de depósito. (13/11/2026) Se firma con la modalidad de los documentos de contratación de cada persona (FIRMA_MODALIDAD); al ingreso, dentro del paquete | Borrador (pestaña «Formatos» del RIT); incluida en la especificación del RIT |
| Documento de asignación de correo institucional | Contratación | INTRANET = Sí; se entrega con el contrato | Redactado (kit 3.5); reforzado el 15/11/2026 (ver 4.3 bis) |
| Documento de designación del sistema de registro de jornada | Contratación | Siempre | Existe como sección B del Anexo 3 del contrato; falta unificarlo con el kit |
| Oficio de asignación REPSE | Operación | Cada asignación de un trabajador REPSE a un cliente, solo si el lugar de trabajo es el del cliente | Modelo propuesto |
| Comunicado de cambio de centro de trabajo | Operación | Cada cambio de centro | Propuesto |
| Convenio de terminación de la relación de trabajo por mutuo consentimiento y finiquito (un solo modelo; sin módulos A a E-bis desde la v1.2) | Terminación | En toda baja salvo fallecimiento; el motivo interno no se imprime | **Terminado y cargado en el software (12/11/2026)**; especificación del módulo 4 v1.4; firma siempre autógrafa |
| Recibo de finiquito (Anexo 1 del convenio) | Terminación | En toda baja | Terminado; una sola hoja carta, con RFC de la Persona Trabajadora; firma autógrafa |
| Comunicado de terminación al vencer el periodo de prueba o de capacitación inicial | Terminación | Solo como respaldo, si se cumplen sus requisitos (evaluación, F-2, evidencia de capacitación) | Terminado |
| Comunicado de terminación por vencimiento del plazo o terminación de la obra | Terminación | Solo como respaldo, si se cumplen sus requisitos | Terminado |
| Convenio de pago a beneficiarios | Terminación | Fallecimiento | Terminado |
| Constancia de servicios (art. 132, fr. VIII) | Terminación | Opcional en cada baja o a solicitud (CONSTANCIA_SERVICIOS) | Terminado |
| Constancia de negativa a firmar | Terminación | Hoja aparte, con botón, solo cuando la persona se niega a firmar un comunicado | Terminado |
| Aviso de rescisión | — | **Servicio aparte de consultoría; el sistema no lo genera** (v1.3) | Fuera del sistema |
| Comunicado de suspensión por fin de temporada | Terminación / Modificaciones | Contratos de temporada | Por redactar |
| Documento de terminación por incapacidad (art. 54) | Terminación | Incapacidad por riesgo no profesional | Por redactar (prioridad C) |
| Hoja interna del escenario de negociación | Terminación (uso interno) | Solo en pantalla o para la Empresa; nunca se entrega | Por redactar (formato) |
| Constancia de salida (acta de entrega de bienes del kit; no es la constancia de servicios) | Terminación | Al terminar la relación | Borrador; se trabaja en otra conversación |
| Acta de devolución y entrega de herramientas | Terminación | Al terminar la relación, siempre que haya habido entrega de herramientas, cuentas, accesos o información | Plantilla en el paquete integrado; reglas de cierre en el módulo 4 (7.7) |
| Reglamento Interior de Trabajo (89 artículos en 13 capítulos; desde el 15/11/2026: Anexo A centros de trabajo, solo con más de un centro; Anexo B horarios, generado del catálogo de jornadas; Anexo C catálogo de conductas y escala) — https://claude.ai/artifact/1zoJd9K6M4EVpEuKdcisvW (rev. 1388; formatos rev. 39) | Colectivo | Precargado; ajustes mínimos; depósito ante el CFCRL | **Cerrado para programación (12/11/2026)**; especificación v1.7; en corrido en el software |
| Especificación para programación del RIT, sus formatos y el acta de la CMRIT v1.7 («AXIARH - RIT - Especificacion para programacion», 18/11/2026; la 1.2 y la 1.3 ya se corrieron en el software; si ya se cargó una versión posterior, basta aplicar las tablas de cambios que falten) | Sistema | — | Entregada; tercer corrido pendiente |
| Acta de integración y estatutos de la CMRIT (un solo instrumento) — https://claude.ai/artifact/XNGvnyBsNnkJ7fHZxy9Sqy (rev. 36) | Colectivo | Con el RIT, antes que él | Criterio común aplicado; incluida en la especificación del RIT; en revisión |
| Formatos disciplinarios FD-1 aviso de hechos, FD-2 acta de audiencia, FD-3 resolución, FD-4 falta leve, FD-5 daño o pérdida | Colectivo / Terminación | Cada expediente disciplinario (folio EXP_FOLIO); FD-1 a FD-3 documentan los hechos previos a una rescisión | Borrador (pestaña «Formatos» del RIT, rev. 33); incluidos en la especificación del RIT |
| Constancia de difusión del RIT (FR-2) | Colectivo | Por centro, con fotografía (fijación y entrega individual; sin verificación periódica desde el 13/11/2026); no se genera sin acuse de depósito | Borrador; incluida en la especificación del RIT |
| Juego de la Comisión Mixta de Capacitación, Adiestramiento y Productividad: oficio al sindicato o designación por las personas trabajadoras, acta de integración e instalación con Bases de Funcionamiento, y formatos F-1 a F-5; elección opcional con D-01 y D-02 del kit de PTU | Colectivo | Plantilla de más de 50 personas, o uso de periodo de prueba o capacitación inicial | En revisión por el usuario |
| Kit de PTU (D-01 a D-14 y reglas R-1 a R-5), con y sin sindicato; dictamen con módulos A, B y C — https://claude.ai/artifact/Us8yMoYr6pkYNNBs5RjwdH (rev. 74); visor https://claude.ai/artifact/1CaujwrX7eLtDVSgqjPxUK | Colectivo | Anual | Borrador completo, pendiente de revisión final |
| Recibo individual de PTU (D-14) | Colectivo | Cada pago de PTU, salvo si se pagó con el finiquito; sigue FIRMA_MODALIDAD | Borrador |
| Registros digitales del módulo de permisos y licencias: SP-1 registro de permiso y SUS-3 lista de reincorporación (la persona confirma en la Plataforma y RH valida) | Eventos | En cada evento resuelto en la Plataforma; formato en papel de respaldo (SALIDA = Respaldo) y constancia exportable (SALIDA = Constancia) | **Terminado (12/11/2026)** |
| Documentos del módulo de permisos y licencias: LIC-1 acuerdo de lactancia, LIC-2 notificación de comisión permanente (con acuse), LIC-3 convenio de licencia sin goce, INC-1 aviso de accidente de trabajo, INC-2 solicitud de transferencia de semanas prenatales, SUS-1 constancia de suspensión, SUS-2 aviso de suspensión por falta de documentos | Eventos | Según el tipo de evento; siguen FIRMA_MODALIDAD | **Terminado (12/11/2026)** |
| Especificación para programación del módulo de permisos y licencias v1.8 («AXIARH - Módulo de permisos y licencias - Especificación para programación», 17/11/2026, lógica y textos) | Sistema | — | Entregada |
| Módulo 5: MOD-1 convenio modificatorio (único, con apartados fijos y módulos variables), MOD-2 comunicado de modificación, MOD-4 oficio de reasignación REPSE, MOD-5 constancia de reasignación temporal, ACT-1 registro de actualización anual; MOD-6 aviso de sustitución patronal (prioridad C, sin redactar) | Modificaciones | Cada cambio de condiciones según la matriz de la especificación (sección 2) | **Diseño terminado (15/11/2026)**; especificación v1.0 lista para correr; **no cerrado** |
| Especificación para programación del módulo 5 v1.0 («AXIARH - Módulo 5 - Especificación para programación», 15/11/2026, con textos y 13 casos de prueba) | Sistema | — | Entregada |
| FON-1 aviso sobre el crédito Fonacot al terminar la relación | Terminación (módulo 8) | Baja con FONACOT_CREDITO = Sí y FONACOT_AVISO_PERSONA = Sí, salvo fallecimiento | Redactado; firma autógrafa de recibido |
| Especificación para programación de los módulos 6 y 8 v1.0 («AXIARH - Módulos 6 y 8 - Especificación para programación», 15/11/2026) | Sistema | — | Entregada; **no cerrado** |
| Documento de integración y funcionamiento del Comité de Integridad y Disciplina | Compliance (Axia Compliance) | El art. 79 del RIT remite a él; alimenta COMITE_INTEGRANTES | Por redactar (salió del RIT el 13/11/2026; incluye la sesión válida con dos integrantes) |
| Registros de vacaciones VAC-1 (solicitud y disfrute) y VAC-3 (confirmación de días), constancia VAC-2 del art. 81 y avisos N-1 a N-6 | Eventos | VAC-2 en cada aniversario; VAC-1, VAC-3 y avisos en la Plataforma y por los canales configurados | Diseño terminado (16/11/2026); textos aprobados; **no cerrado** |
| Especificación para programación del módulo de vacaciones y aguinaldo v1.2 («AXIARH - Módulo de vacaciones y aguinaldo - Especificación para programación», 17/11/2026; sustituye a la v1.1, que no se cargó) y sus textos, sexta versión (17/11/2026) | Sistema | — | Entregada |
| Políticas internas (desde el 15/11/2026 se desarrollan en Axia Compliance) (código de ética, vestimenta, TIC, vehículos, regalos y conflictos de interés, protocolo de acoso, riesgo psicosocial, exámenes médicos y pruebas, prevención de la fatiga, ergonomía y pausas activas, trabajo híbrido y jornada flexible, viáticos y traslados) y registro de políticas vigentes | Políticas | Documentos aparte; el RIT remite al registro de políticas. (12/11/2026) La política de vehículos solo se genera con VEHICULOS_ASIGNADOS = Sí; los arts. 9 y 22 del RIT remiten a las de viáticos y traslados y de trabajo híbrido y jornada flexible | Para después (el código de ética figura como hecho en el RIT) |

Kit de contratación del nivel básico: contrato, perfil de puesto, constancia de entrega de herramientas físicas o digitales, aviso de privacidad, convenio de confidencialidad si aplica y constancia de recibo del RIT.

---

## 2. Arquitectura del sistema

Cada dato se captura una sola vez, en el nivel que le corresponde.

| Nivel | Quién lo captura | Qué contiene |
|---|---|---|
| 1. Configuración de la empresa | Consultoría | (31/10/2026) PERFIL_MODALIDAD (Perfil de puesto / Lista de actividades), como valor por omisión; (13/11/2026) se elige en el alta. Datos generales, representante, centros de trabajo con domicilio completo, folio, vigencia y actividades REPSE registradas (cada una con su número y descripción), forma de pago, día de pago semanal, dominio de correo institucional, prestaciones extralegales por puesto (PRESTACIONES_EXTRA), apoyo de gastos y medios de contacto de teletrabajo, sistema de registro de jornada y si usa geolocalización, apoyo para los gastos del domicilio en la modalidad híbrida (HIBRIDO_APOYO_MODO y HIBRIDO_APOYO_MONTO), días de aviso de cambios al perfil de puesto (PERFIL_AVISO_DIAS), correo para asuntos de datos personales (AVISO_CORREO_DATOS), catálogo de propiedad intelectual (PI_CATALOGO), pena del convenio de confidencialidad (CONV_PENA y sus datos), parámetros del RIT (tolerancias, permisos, plazos, conservación, reincidencia) y datos colectivos (sindicato, número de personas trabajadoras, turnos) |
| 2. Organigrama | Consultoría | (31/10/2026) ACTIVIDADES_PRINCIPALES (de 5 a 10; obligatoria con Lista de actividades). Puestos con sus atributos legales, condiciones de trabajo, perfil de puesto versionado y, por puesto, sistemas y plataformas (PUESTO_SISTEMAS), información confidencial a la que accede (PUESTO_INFO_CATEGORIAS) y propiedad intelectual a la que accede (PUESTO_PI) |
| 3. Alta de la persona trabajadora | RH del cliente | Datos personales, puesto, centro de trabajo, ámbito geográfico, fecha de inicio, modalidad de inicio, salario, días en casa, trabajador REPSE y lugar de trabajo REPSE (Empresa o Cliente), origen de la modalidad híbrida (HIBRIDO_ORIGEN), equipo (tabla EQUIPO_DESCRIPCION: descripción, marca y modelo, serie, estado), beneficiarios, descuento, firma |

Regla general: las condiciones de trabajo vienen preestablecidas por la empresa y el puesto. A RH no se le pregunta nada que pueda definirse en los niveles 1 o 2.

(26/10/2026) Los eventos (baja, permisos y licencias, contratos y vencimientos, PTU, vacaciones y aguinaldo) ya tienen su propia pantalla en el software, separada del alta. Con eso queda cubierta la necesidad del cuarto nivel: cada evento captura sus datos en su pantalla y toma los de los niveles 1 a 3.

(26/10/2026) El software ya tiene un catálogo de horarios o turnos. El Anexo B del RIT y la cláusula de jornada deben generarse desde ese catálogo, sin capturar el horario dos veces.

(26/10/2026, aprobada) **Cambios al catálogo con personas ya contratadas.** Cuando cambia el perfil de puesto, el sistema genera una alerta y una nueva versión para firma de quienes ya firmaron la anterior, con el aviso de PERFIL_AVISO_DIAS días de la cláusula 1.4. (26/10/2026, aprobada) La misma lógica se extiende a jornada, salario y prestaciones del puesto: el cambio aplica de inmediato a las altas nuevas y, para las personas ya contratadas, genera el comunicado o el convenio que corresponda según la matriz del módulo 5; nunca cambia en silencio sus condiciones.

(15/11/2026, módulo 5) **Versión de condiciones por persona.** El catálogo del organigrama se versiona (PUESTO_VERSION, PERFIL_VERSION, JORNADA_VERSION, PRESTACIONES_VERSION). Cada persona queda ligada a la versión que firmó o se le comunicó y a su salario. Un cambio del catálogo aplica de inmediato a las altas nuevas; las personas vigentes pasan a la versión nueva al firmar MOD-1 o al surtir efectos MOD-2; si no firman, conservan la versión anterior sin plazo. Todos los módulos leen la versión de la persona. Concreta la regla del 26/10 de que el catálogo nunca cambia en silencio las condiciones de quien ya está contratado.

(15/11/2026) Variables nuevas de empresa: ACTUALIZACION_ANUAL_MES (mes fijo de la actualización anual de datos, coincidente con la revisión de perfiles); afiliación a Fonacot (FONACOT_AFILIACION_ESTADO sin valor por omisión, FONACOT_NUM_CLIENTE, FONACOT_AFILIACION_FECHA, FONACOT_CONVENIO_ARCHIVO, FONACOT_CONVENIO_VERSION, FONACOT_RESPONSABLE, FONACOT_SOLICITUD_FECHA, FONACOT_NO_PROCEDENTE_MOTIVO, FONACOT_AFILIACION_ALERTA_DIAS 30, FONACOT_REINTENTO_MESES 12, FONACOT_AVISO_PERSONA Sí); pagos (PAGO_TOLERANCIA 1.00, PAGO_EVIDENCIA_DIAS 5, PAGO_ALERTAS_AGUINALDO 10 y 3 hábiles, PAGO_ALERTAS_PTU 15 y 5 hábiles, PAGO_CONSERVACION_ANIOS 5); vacaciones (VAC_ANIO_PROGRAMACION, VAC_PERIODOS_SOLICITUD, VAC_BLOQUEOS, VAC_CUPOS, VAC_NOTIFICACION_CANALES). Catálogo de centros: CENTRO_FONACOT (sin valor por omisión). Alta: FONACOT_CREDITO. TELE_AVISO_DIAS sigue siendo variable de empresa (la usan los módulos T y H del contrato y MOD-2; el RIT ya no la imprime). Tablas globales nuevas con la mecánica de aprobación de parámetros: FONACOT_PLAZOS, FONACOT_CALENDARIO y PAGO_CLAVES_SAT.

(15 y 17/11/2026, paquete de contratación) Empresa: CORREO_AUDITORIA (No por omisión) y CORREO_RETENCION_MESES (24 por omisión; obligatoria con CORREO_AUDITORIA = Sí). Catálogo de jornadas: DESCANSO_SEMANAL Fijo o Rotativo; con Rotativo, DIAS_TRABAJO_SEMANA (1 a 6, por omisión 6) y DESCANSO_AVISO (Ninguna · Semana · Mes), sin tabla de días; JORNADA_TIPO calculada con los horarios (nunca «Rotativa»); HORAS_SEMANA calculada. Alta: SALARIO_PERSONA con precarga del puesto, PERFIL_MODALIDAD y ACTIVIDADES_PRINCIPALES (precarga del puesto), valor de reposición en EQUIPO_DESCRIPCION, INFONAVIT_DESCUENTO_TIPO, INFONAVIT_DESCUENTO_VALOR y FONACOT_DESCUENTO_MONTO (opcionales), contacto de emergencia en tres campos y TELE_DOMICILIO_IGUAL. Eliminadas: PUEDE_SALIR, TELE_APTO, SALARIO, SALARIO_LETRA y CENTAVOS.

(17/11/2026, encargos de Axia NOMs) Atributo de puesto PUESTO_TIPO_NOM035 (Operativo / Supervisor / Profesional o técnico / Gerente) en el organigrama. Datos del nivel 3 capturados por la persona trabajadora y guardados en su expediente: TRAB_ESTADO_CIVIL, TRAB_ESCOLARIDAD y TRAB_EXPERIENCIA_LABORAL (precarga en la siguiente captura). El nombre del centro es CENTRO_NOMBRE, del catálogo único de centros (sustituye a CENTRO_TRABAJO_NOMBRE; CENTRO_TRABAJO y PERSONA_CENTRO se unifican en el diccionario).

(17/11/2026, encargo de Axia NOMs) **Configuración propia por línea.** Cada línea Axia puede tener una configuración propia, por empresa y por centro, ligada a la empresa y a los centros de Axia RH, para los datos que solo usa esa línea (en Axia NOMs: responsables, perfil de seguridad y salud del centro y parámetros de cada NOM). No duplica datos de Axia RH: lo que use otra línea o se capture en el organigrama o el alta se sigue pidiendo por encargo.

(26/10/2026) La comisión de seguridad e higiene y su alerta salen de Axia RH por ahora.

(26/10/2026, aprobada) **Catálogo de clientes REPSE** en la configuración de la empresa: razón social, RFC, domicilio de cada instalación, fecha y número del contrato de servicios y actividad REPSE que se presta. Se elimina el centro genérico «Instalaciones del beneficiario». Con REPSE = Sí y lugar Cliente, el centro de trabajo se elige de las instalaciones del catálogo, su domicilio se imprime en el contrato y se genera el oficio de asignación; cada reasignación es un nuevo oficio desde el módulo de modificaciones. El catálogo sirve también como expediente por cliente.

### Atributos de cada puesto (organigrama)

| Atributo | Valores | Efecto |
|---|---|---|
| Clasificación | Base / Confianza | Contrato, RIT y elegibilidad como representante obrero en las comisiones |
| Puesto de dirección o administración, o técnico o profesional especializado | Sí / No | 180 días de prueba o 6 meses de capacitación. Es independiente de la clasificación base/confianza |
| Trabajo material | Sí / No | Solo pago semanal |
| (26/10/2026, aprobada) Periodicidad de pago | Semanal / Quincenal | Se define en el perfil de puestos, no en el alta; en trabajo material solo semanal. El RIT lista las periodicidades que usa la empresa |
| (26/10/2026, aprobada; **modificada el 15/11/2026**) Salario | Salario base del puesto y, por persona, SALARIO_PERSONA (igual o mayor) | El puesto fija el salario base. Desde el 15/11/2026 (módulo 5, decisión del usuario) cada persona puede tener SALARIO_PERSONA, sin exigir motivo objetivo; solo se valida el salario mínimo de la zona. Una cifra menor que la vigente solo por convenio (MOD-1). Nómina, vacaciones, aguinaldo, PTU y finiquito leen el salario de la persona |
| Nivel de acceso a la información | General / Calificado | Calificado activa el convenio de confidencialidad |
| Jornada, horario, días laborables, descanso (fijo o rotativo) | — | Cláusula de jornada |
| Tiempo de comida | — | Cláusula de jornada. (17/11/2026, decisión del usuario) Ya no se pregunta si la persona puede salir del centro durante el descanso (PUEDE_SALIR eliminada) |
| ~~Teletrabajo permitido~~ | — | (13/11/2026) Eliminado con TELE_APTO: las casillas de días en casa se muestran en el alta |
| Propiedad intelectual | Sí / No | Cláusula de obras e invenciones |
| Prestaciones extralegales (PRESTACIONES_EXTRA) | Las configuradas | Cláusula de prestaciones superiores si no está vacía |
| Perfil de puesto | Clave, versión, fecha | Anexo del contrato; cada edición crea una versión nueva |
| (26/10/2026) Sistemas, plataformas y repositorios (PUESTO_SISTEMAS) | Tabla: sistema, tipo de acceso, información | Perfil (apartado 4), inventario de la carta responsiva y Anexo A del convenio |
| (26/10/2026) Información confidencial a la que accede (PUESTO_INFO_CATEGORIAS) | Texto | Perfil (apartado 4) y Anexo A del convenio |
| (26/10/2026) Propiedad intelectual a la que accede (PUESTO_PI) | Selección de PI_CATALOGO | Anexo A del convenio |
| (26/10/2026, propuesto por el RIT) Puesto crítico para la seguridad (PUESTOS_CRITICOS_SEGURIDAD) | Sí / No | Pruebas de alcohol y drogas y retiro de funciones (RIT, art. 60) |
| (26/10/2026, propuesto por el RIT) Área con riesgo para embarazo o lactancia | Sí / No | RIT, art. 65 |
| (26/10/2026, propuesto por el RIT) Área vedada a menores | Sí / No | RIT, art. 67 |
| (02/11/2026) Excluido de PTU (PTU_EXCLUIDO) | Sí / No | Exclusión de directores, administradores y gerentes generales (art. 127, fr. I) en D-08 B; independiente del atributo de dirección del periodo de prueba |
| (12/11/2026) Jefatura inmediata (PERSONA_JEFATURA, ya usada en el RIT) | Puesto del organigrama | Primer paso de la cadena de autorización de permisos; sustituye a JEFE_INMEDIATO |
| (12/11/2026) Dirección del área (DIRECTOR_AREA, nueva) | Puesto del organigrama, opcional | Último paso de la cadena de autorización, si existe |

---

## 3. Convenciones de redacción

- Términos definidos: «la Empresa» (también para persona física con actividad empresarial; nunca «el patrón») y «la Persona Trabajadora».
- (26/10/2026) La normalización a «la Empresa» y «la Persona Trabajadora» ya se aplicó al contrato maestro y a la biblioteca de módulos. Quedan sin cambio las excepciones deliberadas: el bloque de firmas («LA PERSONA TRABAJADORA / LA EMPRESA»), la definición de la Empresa como quien «tiene el carácter de patrón», los términos que cita la ley, y «la empresa» en minúscula en las notas de diseño que se refieren al cliente del sistema. Falta normalizar el RIT, la comisión mixta de capacitación y el kit de PTU (ver el mapa).
- (26/10/2026, aprobada) Variables con nombre en MAYÚSCULAS_CON_GUION_BAJO y, dentro del texto, entre llaves dobles: {{REGISTRO_GEOLOC}}. Condiciones siempre [SI condición] … [FIN SI]; no se usan ⟦SI⟧, [[SI]] ni «Opcional —».
- (26/10/2026, aprobada) «la Empresa» en todos los documentos, salvo citas legales y denominaciones legales de las comisiones. En instrumentos colectivos se usa «las personas trabajadoras» en plural y minúscula; «la Persona Trabajadora» queda para los documentos individuales.
- Texto condicional: [SI condición] … [FIN SI]; las marcas nunca se imprimen.
- Modelos genéricos, sin referencias a giros. Los giros se tratarán como módulos (prioridad: REPSE, comisionistas y teletrabajo; después hotelería con propinas).
- El texto no fija cifras que cambian por reforma (jornada máxima); remite a la ley y el sistema valida.
- Lo operativo (reglas del registro de jornada, aclaraciones, tiempo extra) va en el RIT, no en el contrato.
- La versión en texto plano para programación se genera solo cuando el modelo maestro esté terminado.
- (13/11/2026, decisión del usuario) **Arial en todos los documentos de todos los módulos** (12 puntos en el cuerpo; títulos en negrita del mismo tamaño o uno mayor; papel carta). Única excepción: el ajuste del recibo de finiquito para que quepa en una hoja.
- (13/11/2026, decisión del usuario) El PDF se genera en el servidor, sin encabezado ni pie del navegador, en todos los módulos.
- (12/11/2026) Las cifras legales que cambian (UMA, tarifas del ISR, subsidio, salarios mínimos, cuotas del IMSS, exenciones, duraciones de permisos y vacaciones) viven en tablas globales con fecha de vigencia que administra AEXIS; se activan solo con aprobación humana y un monitor de fuentes oficiales alerta al administrador (módulo 4, 5.3). Ningún texto ni código las fija.

---

## 4. Decisiones por documento

### 4.1 Contrato individual de trabajo

**Estructura y forma**
- (Actualizado 26/10/2026) El PMV genera todo tipo de contratos laborales. El modelo base es por tiempo indeterminado y los demás tipos se generan con las variantes de la cláusula de temporalidad.
- Carátula a dos columnas con las condiciones generales de trabajo (la versión de 4 columnas se descartó porque los datos largos no caben).
- La firma electrónica no lleva variable en la carátula. Hay una variable para indicar si la firma es autógrafa o electrónica (FIRMA_MODALIDAD).
- El representante comparece con las facultades necesarias, en redacción única; no se pide el instrumento de facultades ni la opción de comparecencia.
- Se eliminaron las cláusulas de continuidad por fallecimiento o incapacidad de la persona física que es empresa.
- Hay una variable para cuando la empresa no tenga perfil de puestos: PERFIL_ORIGEN (Empresa / Sistema), que solo aplica con PERFIL_MODALIDAD = Perfil de puesto.
- (28/10/2026, aprobada) **PERFIL_MODALIDAD.** Con «Lista de actividades», la cláusula 1.1 enlista ACTIVIDADES_PRINCIPALES y no se genera el Anexo 1 ni el perfil del kit; las cláusulas de clasificación, labores conexas, actualización, prueba, capacitación inicial y confidencialidad y la Declaración II b) usan su variante; con prueba o capacitación inicial, la Empresa comunica por escrito los criterios de evaluación o el programa. Opción menos recomendable, permitida por decisión del usuario; riesgo explicado una vez. (13/11/2026) PERFIL_MODALIDAD pasa al alta; ACTIVIDADES_PRINCIPALES se captura en el alta con precarga del puesto.
- (26/10/2026, aprobada) Sin remisiones numéricas entre cláusulas: 25 identificadores estables (CL_*) como código interno, que no se imprimen.
- (26/10/2026, aprobada) Se elimina el Anexo 5. Anexos: 1 perfil de puesto, 2 beneficiarios, 3 acuses (incluye la carta responsiva), 4 aviso de privacidad.
- (26/10/2026, aprobada) No se cambia el título de la cláusula de formalización por medios electrónicos sin actualizar los documentos del kit que la citan.
- (26/10/2026) Sin acuse de recepción al final del contrato. El Anexo 3 es el único acuse: su primera fila acredita la entrega del ejemplar del contrato, la carátula y los anexos que le corresponden (variable ANEXOS_LISTA, la misma de la fila «Anexos» de la carátula).
- (26/10/2026, propuesta tomada de los contratos anteriores; provisional) Declaración II d): la Persona Trabajadora conoce que su patrón es la Empresa y que clientes, proveedores, empresas relacionadas o titulares de licencias, marcas o instalaciones no son su patrón por ese solo hecho, sin limitar las responsabilidades que la ley imponga a terceros.
- (26/10/2026, ídem) Cláusula 1.4: toda modificación al perfil de puesto se comunica por escrito con PERFIL_AVISO_DIAS días naturales de anticipación (variable de la empresa, por omisión 15) y con constancia; las modificaciones a funciones de distinta naturaleza o categoría superior, o a las condiciones de trabajo, requieren acuerdo previo y por escrito. (17/11/2026) El cierre ya no dice que «ningún cambio disminuirá el salario»: ningún cambio afectará los mínimos que la ley establece ni lo ya devengado; el inciso c) incluye «la reducción de su salario» entre los cambios que requieren acuerdo previo y por escrito (congruente con 4.12).
- (26/10/2026) Cláusula 1.2, labores conexas: se quita la frase «sin derecho a una compensación adicional». (Actualizado 26/10/2026, decisión del usuario) La estrategia es que las labores conexas o complementarias son parte de las actividades del puesto. La cláusula 1.2 dice que forman parte de las actividades del puesto y que la Persona Trabajadora las desempeña sin que implique cambio de puesto; ya no afirma que estén comprendidas en el salario. Aplicado al contrato (rev. 312). Riesgo explicado una vez (ver pendiente).
- (26/10/2026, ídem) Cláusula 10: la Persona Trabajadora entrega el aviso de retención de su crédito INFONAVIT dentro de 3 días hábiles; la Empresa aplica la retención desde que lo recibe. No se traslada a la Persona Trabajadora el pago de recargos u omisiones de la Empresa (el contrato anterior lo hacía por descuento vía nómina).

- (13/11/2026, provisional; pendiente de aplicar en el paquete) Carátula en 1 página, 2 como máximo, con cuadrícula de columnas combinadas (etiqueta y valor en casillas separadas, sin agrupar datos en una celda); verificar el art. 25 LFT antes de fusionar o quitar filas.
- (13/11/2026) Anexo 3, fila RIT_ENTREGA: solo con el RIT no depositado; con RIT depositado la sustituye la FR-1 de ingreso, que entra al paquete (ver 4.4, «Firma del RIT y de la FR-1»).
- (12/11/2026) Cláusula VIGÉSIMA SEGUNDA (formalización por medios electrónicos): se sustituyen la regla de generación y los apartados 22.1 a 22.5 con las instrucciones del apartado 9 del «Corte - Firma electrónica»: sin remisión al Código de Comercio; equivalencia pactada con la firma autógrafa; la Empresa firma por su representante con e.firma o, en documentos posteriores, por la persona designada; NOM-151 condicionada a NOM151_SERVICIO; firma autógrafa sustituta si falla la Plataforma. El título no cambia. (13/11/2026) Aplicada en el contrato; (18/11/2026) el apartado 9 del corte de firma electrónica se actualizó con INE y video y el cambio de medio presencial (encargo 7 del paquete).
- (15/11/2026) **Bloques de firma según FIRMA_MODALIDAD:** con Autógrafa, línea «Firma: ____»; con Electrónica, sellos FIRMA_SELLO_TRAB y FIRMA_SELLO_EMPRESA (derivadas; antes de firmar, «Pendiente de firma electrónica»), en el contrato, los Anexos 2, 3 y 4 y los documentos del kit. El párrafo de firma del final del contrato depende de FIRMA_MODALIDAD. Conservan línea autógrafa la autorización de descuento de la carta responsiva, los testigos de las negativas y los documentos de firma autógrafa obligatoria.
- (17/11/2026) La carátula imprime SALARIO_PERSONA y SALARIO_PERSONA_LETRA («… pesos NN/100 M.N.»); se eliminan SALARIO, SALARIO_LETRA y CENTAVOS; SALARIO_BASE_DIARIO del módulo C pasa a derivada (SALARIO_PERSONA de quien tiene salario base más comisión).
- (15/11/2026) **Créditos en el alta:** con INFONAVIT_CREDITO = Sí, INFONAVIT_DESCUENTO_TIPO (Porcentaje · Cuota fija · Veces salario mínimo, por confirmar) e INFONAVIT_DESCUENTO_VALOR; con FONACOT_CREDITO = Sí, FONACOT_DESCUENTO_MONTO (mensual). Opcionales, sin texto impreso; regla nueva después de la cláusula de seguridad social; aviso en prenómina si el Fonacot rebasa el 20 % del salario. (17/11/2026, decisión del usuario) FONACOT_DESCUENTO_MONTO es un valor esperado para la prenómina; la evidencia es la cédula mensual del módulo 8, que no calcula retenciones (4.13).
- (13/11/2026) Obra determinada: CAUSA_OBRA desplegable; con REPSE, «vigencia del contrato de servicios» lleva a obra determinada con OBRA_DESCRIPCION; la vigencia del contrato con el cliente como causa de tiempo determinado o temporada solo advierte (M-R.6). Domicilio de teletrabajo con TELE_DOMICILIO_IGUAL y TELE_DOMICILIO. Contacto de emergencia en nombre, parentesco y teléfono. La cláusula 13.2 remite al RIT y al módulo de permisos, sin plazos propios. (15/11/2026) M-R.2 conserva la remisión al perfil de puesto o a la lista de actividades.

**Temporalidad de contratación, periodo de prueba y capacitación inicial (Cláusula Tercera)**
- (26/10/2026) Las antiguas cláusulas Tercera y Cuarta se fusionaron en una sola, «Temporalidad de contratación» (estructura vigente: ver abajo, 3.1 a 3.4).
- (26/10/2026, aprobada; sustituye la estructura 3.3 a 3.6) Estructura con la redacción del usuario: 3.1 prueba o capacitación inicial según PRUEBA_OPCION; 3.2 en prueba solo se evalúa y en capacitación inicial solo se capacita; 3.3 terminación del periodo «sin responsabilidad para la Empresa» (arts. 39-A y 39-B); 3.4 salario y seguridad social durante el periodo, y periodos improrrogables, no simultáneos ni sucesivos, ni en más de una ocasión, ni en puestos distintos o ascensos (contenido del art. 39-D, sin citarlo).
- La opinión de la Comisión Mixta es interna y no se menciona en el contrato; vive en el formato F-2 y el candado, en el sistema.
- (26/10/2026, aprobada) Tipos B, C y D con causa de temporalidad obligatoria; prueba solo en tiempo indeterminado o en tiempo determinado mayor de 180 días.
- Periodo de prueba: 30 días; 180 si el puesto es de dirección o administración, o técnico o profesional especializado.
- Capacitación inicial: 3 meses; 6 con el mismo criterio. Quien llena el formulario no elige la duración.
- (26/10/2026) El periodo ampliado aplica a puestos de dirección o administración y a los técnicos o profesionales especializados. No depende de la clasificación base/confianza.
- El contrato solo menciona el programa de capacitación, sin su nombre.
- La terminación al vencer el periodo no es un aviso de rescisión; es un documento aparte del kit, separado de la opinión de la Comisión Mixta.
- El perfil de puesto es la base de evaluación del periodo; con Lista de actividades, la base son los criterios comunicados por escrito al inicio.
- (26/10/2026) Referencias legales verificadas: arts. 12 a 15, 39-A a 39-F y 330-D LFT.

**Jornada**
- Descanso semanal fijo (uno o varios días) o rotativo. (13 y 15/11/2026) Con descanso rotativo no hay tabla de días: DIAS_TRABAJO_SEMANA y aviso opcional DESCANSO_AVISO; la cláusula 6.2 dice que no pueden pasar más de seis días consecutivos de trabajo; el art. 69 se valida solo con descanso fijo. «Rotativa» no es tipo de jornada (art. 60 LFT).
- ~~Dos variantes según si la persona puede salir del centro durante la comida.~~ (13 y 17/11/2026, decisión del usuario) Se elimina PUEDE_SALIR de la carátula y del catálogo de jornadas. La cláusula 6.4 conserva como regla legal escrita que, si la persona no puede salir durante el descanso, ese tiempo cuenta como efectivo; el sistema ya no lo aplica al cálculo. Riesgo explicado una vez; decisión respetada.
- Cláusula 6.5: registro electrónico de jornada con aceptación expresa del sistema que designe la empresa. La ubicación se registra solo si la empresa lo tiene preestablecido (variable REGISTRO_GEOLOC). Hay un documento de designación del sistema. (26/10/2026, aprobada) La ubicación no requiere consentimiento. Los biométricos requieren consentimiento expreso, libre e independiente, recabado en una casilla propia del apartado 10 del aviso de privacidad; el medio alterno (PIN o tarjeta, SISTEMA_REGISTRO_ALTERNO) opera para quien no lo otorgue o lo revoque, sin consecuencia laboral, y también si el sistema falla. El Anexo 3 y la cláusula de jornada solo lo hacen constar. PUEDE_SALIR_B pasa a PUEDE_SALIR, dato del puesto (eliminada el 13 y 17/11/2026).
- (26/10/2026) Jornada única: la jornada de teletrabajo y la jornada ordinaria se regulan en una sola cláusula (la 6), sin texto de jornada propio en el módulo T. (26/10/2026, ajuste) Las cláusulas 6.7 y 6.8 se generan si DIAS_EN_CASA_ACTIVO = Sí (variable derivada: TELETRABAJO_ACTIVO o HIBRIDO_ACTIVO), es decir, tanto en teletrabajo como en trabajo híbrido. La cláusula 6.5b contiene la condición anidada correspondiente: en los días en casa la ubicación no se captura.

**Lugar de trabajo**
- Centro de trabajo de la lista de la empresa y ámbito geográfico de selección múltiple.
- Sin reglas de traslado. Decisión confirmada después de la advertencia de riesgo.

**Comunicaciones**
- El correo personal se designa en la carátula.
- El institucional se asigna en un documento independiente; las notificaciones laborales van al correo personal.
- (26/10/2026) El Anexo 3 ya no contiene la designación de medios institucionales (se eliminó su fila y la sección C). La cláusula 18.3 y su regla de generación remiten al «documento de asignación de correo institucional», que se genera con INTRANET = Sí y se entrega con el contrato.
- (26/10/2026) REGISTRO_GEOLOC: se quitó de la regla de generación la obligación de que el aviso de privacidad (Anexo 4) mencione la ubicación, porque el aviso la menciona siempre. (Actualizado 26/10/2026) El bloque de ubicación del Anexo 3 debe ajustarse a la regla aprobada: ubicación sin opción de negarse; biométricos con consentimiento expreso y medio alterno.
- (26/10/2026) Cláusula 19 (beneficiarios) alineada con el documento de designación: mantener actualizada la designación es responsabilidad de la Persona Trabajadora, que la confirma por escrito al menos una vez al año, y la designación no se refiere a ningún seguro de vida. No se pudo comparar con el texto literal del documento de designación del kit; queda por verificar su redacción.

**Módulos**
- (26/10/2026) El módulo T cubre el teletrabajo (más de 40% del tiempo en casa) y se activa con TELETRABAJO_ACTIVO. El trabajo híbrido (hasta 40%) tiene su propio módulo H (ver abajo). T y H son excluyentes.
- Propiedad intelectual. Pendiente confirmar si la cláusula base de confidencialidad incluye el pacto de titularidad de obras (art. 84 LFDA).
- Prestaciones superiores: solo cuando el cliente las tenga, preestablecidas (PRESTACIONES_EXTRA no vacía; se elimina PRESTACIONES_SUPERIORES). SEGURO_VIDA queda como ejemplo provisional hasta diseñar el paquete de prestaciones extralegales.
- (26/10/2026, aprobada) La cláusula de confidencialidad tiene su propia lista de «reproducir o extraer». CONF_CLAUSULA_BASE es su texto sin el apartado de información calificada ni numeración.

**Módulo R (REPSE)** — decisiones del 26/10/2026
- En el módulo se usa «el cliente» en lugar de «la persona beneficiaria».
- Las declaraciones incluyen el folio, la vigencia y la lista de **todas** las actividades especializadas registradas de la Empresa, cada una con su número y su descripción (REPSE_FOLIO, REPSE_VIGENCIA, REPSE_ACTIVIDADES). El contrato no identifica la actividad especializada de cada persona trabajadora. Decisión aplicada como propuesta, sin objeción; la acreditación de cuál actividad ejecuta cada persona se hace en el expediente por cliente.
- Lugar de trabajo REPSE (REPSE_LUGAR_TIPO, se captura en el alta; por omisión, Empresa): **Empresa** (el centro de trabajo es el domicilio de la Empresa, por omisión la matriz, y los servicios a clientes se ordenan mediante órdenes de servicio) o **Cliente** (el centro de trabajo es el domicilio del cliente, reasignable).
- El oficio de asignación se genera solo si REPSE_LUGAR_TIPO = Cliente. Confirmado por el usuario.
- Cláusula nueva de servicio al cliente (M-R.5): la atención al cliente forma parte de las funciones; la Persona Trabajadora observa las políticas de servicio al cliente de la Empresa y los lineamientos del cliente, que se le entregan por escrito con acuse (Anexo 3). Una queja del cliente se registra, se escucha a la Persona Trabajadora y la Empresa decide entre reasignar, aplicar una medida disciplinaria o, solo si los hechos encuadran en una causa legal, rescindir. La queja o la solicitud del cliente no son por sí mismas causa de rescisión; el contrato no crea causas de rescisión. Riesgo explicado una vez; la decisión se mantiene.
- La terminación del contrato de servicios entre la Empresa y un cliente no es por sí misma causa de terminación de la relación de trabajo (M-R.6).

**Módulo H (trabajo híbrido)** — decisiones del 26/10/2026 (provisionales)
- Se activa con HIBRIDO_ACTIVO: TELETRABAJO = Sí y PORC_TIEMPO_DOMICILIO entre 1 y 40. Con más de 40 se genera T, nunca ambos. El trabajo a distancia ocasional no requiere módulo.
- Fundamento verificado en el texto vigente de la LFT (última reforma DOF 14-05-2026): art. 330-A (el capítulo de teletrabajo rige cuando más del 40% del tiempo se presta en el domicilio o en el lugar elegido) y art. 132, fr. III (la Empresa proporciona útiles e instrumentos, salvo compromiso de usar herramienta propia). Por debajo del umbral no aplican las obligaciones especiales del teletrabajo, pero sí las generales.
- La modalidad base es presencial; los días en casa son revocables con aviso de TELE_AVISO_DIAS días (salvo causa urgente justificada). El regreso a lo presencial no disminuye salario ni condiciones.
- Reutiliza variables de T: TELE_DIAS, PORC_TIEMPO_DOMICILIO, TELE_DOMICILIO, TELE_AVISO_DIAS y TELE_CANALES. Nuevas: HIBRIDO_ORIGEN (alta: Solicitud de la Persona Trabajadora / Decisión de la Empresa), HIBRIDO_APOYO_MODO (empresa: Sin apoyo / Monto fijo / Reembolso) y HIBRIDO_APOYO_MONTO (empresa, solo con Monto fijo).
- Gastos del domicilio: con «Sin apoyo» el texto dice que corren por cuenta de la Persona Trabajadora porque la modalidad se pacta a su solicitud. Si HIBRIDO_ORIGEN = Decisión de la Empresa, el sistema bloquea «Sin apoyo». Riesgo explicado una vez: si la Empresa impone la modalidad y no apoya los gastos, pueden reclamarse.
- Jornada, contacto y desconexión no tienen texto propio: se rigen por las cláusulas 6.7 y 6.8 del contrato. Sin anexos propios; la carta responsiva y la política de uso de tecnologías de la información se acusan en el Anexo 3.
- Reglas del sistema: exigir carta responsiva con inventario si hay equipo asignado; alertar si la Empresa no tiene la política de uso de TIC; (31/10/2026) alertar si la Empresa no tiene la política de trabajo híbrido y jornada flexible, que regula la solicitud, la autorización y el cambio de los días en casa; ~~el perfil de puesto debe admitir días en casa (TELE_APTO)~~ (TELE_APTO eliminada el 13/11/2026).

### 4.2 Confidencialidad
1. Cláusula base reforzada en el contrato para todas las personas trabajadoras.
2. Conductas y consecuencias en el RIT (conductas 36, 39, 56 y 58 del catálogo de conductas del RIT, corregido el 12/11/2026; desde el 15/11 el catálogo es el Anexo C, o el B con un solo centro; deben coincidir con el contrato y con la definición de reproducción y extracción del convenio).
3. Convenio de confidencialidad como módulo para puestos con acceso calificado.
4. Adenda con el texto de la cláusula base para personal contratado antes de adoptar el kit.
- Convenio sin pena convencional en el texto base (responsabilidad por daños acreditados). Pena convencional solo por incumplimientos posteriores a la terminación, como módulo opcional.
- (26/10/2026) El convenio incorpora una cláusula que define la reproducción y la extracción de información: capturas y grabaciones de pantalla, fotografías, impresiones, escaneos, descargas y sincronización en nube personal, reenvíos, transcripciones, carga en herramientas de inteligencia artificial y acceso desde equipos no autorizados.
- (26/10/2026) El convenio lleva un Anexo A con la propiedad intelectual, los sistemas y plataformas, el correo institucional y las categorías de información a los que tiene acceso la Persona Trabajadora, alimentado por PI_CATALOGO, PUESTO_PI, PUESTO_SISTEMAS y PUESTO_INFO_CATEGORIAS. La relación es enunciativa y su firma acredita la prevención de confidencialidad.
- (26/10/2026) Vigencia del convenio: 3 años después de la terminación, igual que la cláusula 14.4 del contrato. Sin variable de plazo.

### 4.3 Designación de beneficiarios
- Actualizarla es responsabilidad de la persona trabajadora.
- El modelo prevé una actualización de datos al menos una vez al año.
- (26/10/2026) La cláusula 19 del contrato dice lo mismo (ver 4.1, Comunicaciones).
- Sin módulo de seguro de vida (no hay aseguradora). (26/10/2026) Si la empresa da seguro de vida como prestación, la designación imprime la advertencia de que los beneficiarios del seguro se designan en el formato de la aseguradora (SEGURO_VIDA).
- (26/10/2026, aprobada) Sin beneficiario sustituto y sin variable de quién recibe por la Empresa.
- (26/10/2026, provisional) Si fallece una persona designada y no se actualizó la designación, su porción se reparte entre las demás en proporción a sus porcentajes.
- (26/10/2026, provisional) Si hay controversia, la Empresa puede abstenerse de pagar hasta que la autoridad declare a los beneficiarios.
- (26/10/2026, provisional) Lo que corresponda a menores se paga a quien ejerza la patria potestad o la tutela.

### 4.3 bis Kit de contratación (26/10/2026)
- Alcance de la conversación del kit: aviso de privacidad para personas trabajadoras, aviso de privacidad para candidatos, convenio de confidencialidad y su Anexo A, carta responsiva, designación de beneficiarios, perfil de puesto y lineamientos para generar perfiles. Teletrabajo (con la NOM-037), constancia de salida y acuerdo de descuento se trabajan en otras conversaciones.
- Todo el kit usa la variable FIRMA_MODALIDAD del contrato y la misma cláusula de firma electrónica, que remite a la cláusula de formalización por medios electrónicos del contrato. No hay variable propia de aceptación digital. (26/10/2026) Excepción: la adenda de confidencialidad trae su propia cláusula de firma electrónica, porque se firma con personal cuyos contratos anteriores no tienen la cláusula 22.
- Formulario del kit: cada dato se captura una sola vez, en su nivel; los datos que ya pide el contrato no se vuelven a pedir.
- (26/10/2026) Se elimina PUESTO_REPORTA del formulario y la fila «Reporta a» del perfil de puesto. La línea de mando solo se usa como dato del cuestionario de levantamiento.

**Perfil de puesto**
- (26/10/2026, aprobada) Lo genera la IA del sistema con base en los «Lineamientos para generar perfiles de puesto», con un perfil por puesto y validación humana antes de firmarse.
- (26/10/2026, aprobada) La revisión anual de los perfiles coincide con la actualización anual de datos de las personas trabajadoras.
- (26/10/2026, provisional) El perfil no lleva salario, horario ni datos de la persona.
- (13/11/2026) El perfil ya no indica si el puesto admite días en casa (TELE_APTO eliminada).

**Aviso de privacidad para personas trabajadoras**
- Formato fijo que lista todos los datos que la Empresa puede tratar, con la mención «cuando se utilicen» (documento migratorio, biométricos, ubicación, audio y registros de uso de las herramientas de trabajo). Sin módulos ni versiones distintas por cliente.
- Comunicación de datos a terceros genérica, remitida a las excepciones de la ley; sin destinatarios específicos. Por eso no se agrega una remisión específica a la STPS vía SIRCE.
- Variables mínimas: datos de la Empresa, AVISO_CORREO_DATOS y datos de firma. Se eliminaron las de puestos con acceso a grabaciones, áreas con cámara y plazos de conservación.
- Una sola firma de acuse y consentimiento expreso para datos sensibles y financieros, y una sola finalidad voluntaria (uso de imagen).
- (26/10/2026, aprobada; sustituye la decisión anterior del kit) La **ubicación** se trata sin opción de negarse, con fundamento en la relación de trabajo y el registro de jornada. Los **biométricos** requieren consentimiento expreso, libre e independiente, con casilla propia en el apartado 10 del aviso, y medio alterno (PIN o tarjeta) también por falla del sistema. El aviso de privacidad y el Anexo 3 del contrato deben decir lo mismo.
- (26/10/2026, provisional) El aviso de candidatos es un documento propio del reclutamiento, separado del aviso de personas trabajadoras. Formato fijo, sin módulos ni listas de puestos: psicométricos, antecedentes y estudio socioeconómico solo «cuando la naturaleza del puesto lo justifique»; comunicación de datos genérica; tres casillas (salud, datos patrimoniales y bolsa de trabajo); aviso simplificado para vacantes en línea; nombre y fecha del candidato a mano. Variables nuevas: AVISO_URL, CAND_PLAZO_CONSERVACION y CAND_PLAZO_BOLSA.
- (31/10/2026) **La versión vigente del kit es la del paquete integrado (visor v9), no el visor v6**, que conserva tres diferencias: casilla de biométricos del aviso, condición del acta de devolución y omisión del perfil con Lista de actividades. Versión anterior: visor v6 (https://claude.ai/artifact/3EDzdAW3oyfGXoTXDjrvh3). Variables y dependencias en «Kit de contratación - Variables y dependencias» (55 variables, extraídas del texto). La carta responsiva, inciso d), remite al documento de asignación de correo institucional.
- (17/11/2026, confirmado por el usuario) **Aviso ampliado** (encargo 2): expedientes disciplinarios y declaraciones manuscritas; solicitudes, constancias y evidencia de permisos, licencias, vacaciones y suspensiones, incluidas constancias de detención o arresto y la Declaración Especial de Ausencia (tratadas como datos laborales, no sensibles; por verificar con la LFPDPPP 2025); monto de los descuentos de créditos; incapacidades solo con folio, ramo, fechas y duración; confidencialidad de los exámenes; inciso l) de firma electrónica (correo, celular y bitácora) con su finalidad n); expediente clínico durante la relación y hasta dos años después. Pendiente el encargo 6 (INE y video).
- (13/11/2026) El Anexo 3 es un documento independiente del kit (3.11); la FR-1 figura como 3.12.

**Carta responsiva**
- (26/10/2026) Se genera también cuando solo hay herramientas digitales: correo institucional o sistemas asignados al puesto, y cuando hay días en casa (teletrabajo o híbrido).
- (26/10/2026) El correo institucional se menciona como «asignado por la Empresa», sin remitir al Anexo 3 del contrato. El Anexo 3 solo contiene el acuse de políticas y la aceptación del registro de asistencia; el usuario lo unificará con el kit.
- Cubre herramientas físicas y digitales: titularidad de cuentas y contenidos, uso exclusivamente laboral, credenciales (lo realizado con ellas se presume hecho por la Persona Trabajadora, salvo prueba en contrario o reporte previo de pérdida o compromiso), prohibiciones de extracción, registros de actividad como prueba, dispositivos personales, entrega de contraseñas y prohibición de borrar información antes de la salida.
- (26/10/2026, provisional) La responsabilidad por dolo o negligencia se acredita mediante el procedimiento del RIT (art. 46). (12/11/2026) El art. 46 ya no menciona la autorización previa: la carta responsiva debe contenerla, junto con el valor de reposición de cada bien (ver 4.4).
- (26/10/2026, aprobada; sustituye la prohibición de compensar) Una sola regla de descuento por pérdida o daño: procede solo si el Comité determina la negligencia con audiencia, existe la autorización previa firmada en el resguardo y se respetan los límites legales. La carta responsiva remite al art. 46 del RIT.
- (26/10/2026, provisional) El mantenimiento y la reposición de las herramientas corresponden a la Empresa.
- (17/11/2026, confirmado por el usuario) EQUIPO_DESCRIPCION agrega «Valor de reposición»; la cláusula décima segunda usa ese valor ajustado por desgaste al momento de la pérdida o el daño; sin valor de reposición no procede descuento por ese bien (misma regla de FD-5). Cumple el encargo 1.

**Asignación de correo institucional**
- (15/11/2026) Reforzada a 12 cláusulas para acreditar la salida de información: confidencialidad por defecto; prohibiciones con excepción de los documentos propios de la persona; registros de actividad y revisión del contenido con garantías (orden escrita de persona distinta de la jefatura inmediata y constancia de quién, cuándo, para qué y qué se revisó); conservación e integridad de la evidencia; aviso de incidentes; declaración de no conservación al salir. La cláusula de registros solo con CORREO_AUDITORIA = Sí; CORREO_RETENCION_MESES por omisión 24 (decisión de la empresa, no obligación legal). Sin criterio judicial localizado sobre la revisión del correo institucional.

### 4.4 Reglamento Interior de Trabajo
- Precargado en la plataforma, con ajustes mínimos y generales.
- Numeración continua sin «Bis». No cita artículos de la LFT. No repite lo que la Ley ya regula.
- Excepción: protección de menores y de mujeres embarazadas o en lactancia lista las prohibiciones legales (lo observó un verificador de la STPS).
- Las políticas internas no se enumeran: el art. 4 remite a un registro de políticas vigentes a cargo de RH.
- (25/10/2026, aprobada) Los horarios pasan al Anexo B. Cuando la Ley reduzca la jornada máxima, se entienden reducidos de pleno derecho, sin modificar ni volver a depositar el RIT; la Empresa avisa con DIAS_AVISO_AJUSTE_HORARIO días (art. 8).
- (25/10/2026, aprobada) Art. 11 de pausas y prevención de la fatiga, que remite a las políticas de prevención de la fatiga y de ergonomía y pausas activas, a bipedestación (art. 54) y a riesgos psicosociales (art. 72).
- (25/10/2026, aprobada; sustituida el 12/11/2026) Descuento por pérdida o daño: la investigación se sigue conforme a los arts. 80 y 81; el descuento solo procede con reconocimiento (FD-5) o con determinación de responsabilidad (FD-3), conforme al art. 27 y dentro de los límites legales (art. 46). La autorización previa vive en el resguardo y la carta responsiva, no en el RIT.
- (25/10/2026, aprobada) Plazo para notificar la medida disciplinaria: 30 días naturales desde que la Empresa conoce la falta, sin exceder la prescripción legal.
- (25/10/2026, aprobada) El aviso de ausencia no justifica por sí solo la falta; RH la valora con la dirección y la jefatura.
- (25/10/2026, aprobada) La solicitud de vacaciones no implica autorización automática.
- (26/10/2026, aprobada) MESES_CANCELACION_ANTECEDENTES se separa de MESES_REINCIDENCIA.
- (24/10/2026, provisional) El RIT no aplica al personal de contratistas, prestadores de servicios especializados, proveedores ni visitantes.
- (24/10/2026, provisional) El Comité de Integridad y Disciplina, de integración patronal, atiende la materia disciplinaria.
- (24/10/2026, provisional) Medidas disciplinarias únicas: amonestación verbal registrada, amonestación escrita y suspensión de 1 a 8 días. Descuentos y multas no son medidas disciplinarias. (12/11/2026) El art. 77, fr. 4, menciona además la rescisión, como consecuencia que decide la Empresa conforme al art. 84, no como medida del Comité ni con resolución suya. La escala del Anexo A no cambia.
- (24/10/2026, provisional) Ruta para faltas leves en 4 pasos, a cargo de la jefatura y con revisión del Comité. Ruta para faltas graves y muy graves en 4 pasos: reporte, aviso de hechos, audiencia y resolución. Medidas provisionales siempre con goce de salario.
- (26/10/2026, aprobada) El procedimiento previo a la rescisión es facultativo (art. 84).
- (26/10/2026, aprobada) Se aceptan como excepción las repeticiones de la ley necesarias para aplicar el RIT (reposo de 30 minutos en jornada continua). (31/10/2026) El usuario retiró el cómputo del tiempo de comida del art. 10.
- (24/10/2026, provisional) Escala por nivel con reincidencia; la conducta intentada se califica en el nivel inferior. Catálogo de 58 conductas: 21 leves, 21 graves y 16 muy graves. (12/11/2026) Pasa a 60 conductas: 21 leves, 22 graves y 17 muy graves.
- (24/10/2026, provisional) Horas extra solo por orden previa de la jefatura. El tiempo laborado sin orden se paga y la omisión se atiende por vía disciplinaria.
- (24/10/2026, provisional) Aviso de ausencia antes del turno o dentro de los 60 minutos siguientes; justificación dentro de 2 días hábiles.
- (24/10/2026, provisional) Permisos y días por fallecimiento en tabla única, con cifras sugeridas configurables.
- (24/10/2026, provisional) Pruebas de alcohol y drogas: supuestos de aplicación, prueba confirmatoria y retiro de funciones críticas. Un resultado positivo no equivale por sí solo a la causal legal de rescisión.
- (24/10/2026, provisional; ajustada el 12/11/2026) Art. 59: obligación de someterse a exámenes periódicos; los resultados son confidenciales y solo sirven para verificar la aptitud. Se quitaron los tipos de examen y la mención del dictamen de aptitud.
- (31/10/2026, aprobada) Pruebas de alcohol y drogas: RH recibe solo el resultado confirmado (positivo o negativo), necesario para retirar a la persona de funciones críticas; el detalle clínico se queda con el servicio médico. El aviso de privacidad debe decir lo mismo.
- (24/10/2026, provisional) Riesgos de trabajo: la persona trabajadora no asume responsabilidad solidaria.
- (24/10/2026, provisional) Obligación de avisar el embarazo cuando el puesto implica riesgo, para reasignar sin reducción de salario.
- (24/10/2026, provisional) Declaración de conflictos de interés y de relaciones con línea jerárquica directa.
- (24/10/2026, provisional) Canal de denuncias con opción anónima y prohibición de represalias.
- (24/10/2026, provisional) Se eliminan la prohibición de copiar el RIT, la suspensión de labores «a juicio del patrón» y los «derechos de huelga y sindicato» del patrón.
- (26/10/2026) Depósito ante el Centro Federal de Conciliación y Registro Laboral, conforme al texto vigente de la LFT verificado el 24/10/2026.

- (31/10/2026, aprobada) Criterio de redacción del RIT: se omiten las obligaciones legales que no es necesario reproducir para aplicarlo; su omisión no implica que no se cumplan. Aplicado a los arts. 10, 11 (pausas facultativas salvo bipedestación), 14 (se quitó el efecto del retardo) y 27 (el reconocimiento de deuda ya no exige forma escrita y se quitó «sin soportes no hay descuento»).
- (31/10/2026, aprobada) Art. 22: días en casa y horarios flexibles se rigen por una política de trabajo híbrido y jornada flexible; en el RIT quedan registro sin ubicación, contacto, desconexión, herramientas, regreso sin reducción y teletrabajo pactado por escrito.
- (31/10/2026, aprobada) Art. 31: Tabla I de permisos legales, fija y no editable; Tabla II de permisos de la Empresa, catálogo editable PERMISOS_EMPRESA. El art. 32 solo se genera si la fila de fallecimiento sigue en el catálogo.
- (31/10/2026, aprobada; **sustituida el 13/11/2026**) ~~Art. 79 y Anexo C: Comité por puestos; art. 4 y Anexo D: ubicación de las políticas.~~ Ambos anexos salieron del RIT: la integración del Comité pasa a un documento propio (Axia Compliance) y el art. 4 solo remite al registro de políticas de RH.
- (31/10/2026, aprobada) Art. 75: la prohibición de publicar información confidencial incluye la operativa y la laboral. Riesgo (libertad sindical y de expresión) explicado una vez; se mantiene.
- (31/10/2026, provisional) Art. 9: con REPSE_EMPRESA = Sí, el traslado durante la jornada es tiempo de trabajo; si la prolonga, aplican los arts. 17 y 18; la Empresa cubre los gastos de los traslados que ordene.
- (31/10/2026, provisional) Formatos FD-1 a FD-5: citatorio de 1 a 5 días hábiles (desde el 18/11/2026, días naturales; ver «Encargos del 18/11/2026»); reprogramación una sola vez; medida provisional con goce de salario; FD-3 puede proponer la rescisión a RESCISION_RESPONSABLE; FD-5 toma el bien del resguardo y sin resguardo con valor de reposición no hay descuento; negativa a firmar con dos testigos y envío al correo personal. El aviso de rescisión es documento aparte del módulo 4.

- (31/10/2026, aprobada) Crear o cambiar una jornada del catálogo obliga a depositar de nuevo el Anexo B. El cambio aplica a las altas nuevas; al personal vigente se le genera comunicado o convenio (módulo 5). La reducción legal de jornada no requiere depósito (art. 8).
- (31/10/2026, aprobada; ajustada el 15/11/2026) Cambiar el catálogo de jornadas (Anexo B) o el catálogo de centros (Anexo A, si hay varios centros) genera la alerta «RIT modificado: pendiente de depósito». No se bloquea la FR-1: mientras no se deposite la versión nueva, se sigue entregando la vigente. La integración del Comité ya no forma parte del RIT y cambiarla no genera alerta ni versión.
- (31/10/2026, aprobada) Alerta anual de revisión del RIT.
- (31/10/2026, aprobada) No hay acta administrativa de hechos genérica: FD-1, FD-2 y FD-5 la cubren.
- (31/10/2026, aprobada) Art. 27 y descuentos: el sistema permite registrar el descuento y cargar la evidencia después; sin evidencia solo genera alertas, no bloquea. Riesgo explicado una vez (la Empresa debe probar la deuda y su aceptación si se impugna); se mantiene.
- (31/10/2026, aprobada) Art. 60: RH recibe solo el resultado confirmado de las pruebas de alcohol y drogas.
- (31/10/2026, aprobada; ajustada el 12/11/2026) Anexo A: tabla de correspondencia, no imprimible, con la fracción del art. 47 que actualiza cada conducta, si actualiza alguna. Desde la v1.3 del módulo 4 el aviso de rescisión es un servicio aparte: la tabla solo marca la posible rescisión en FD-1 y habilita la propuesta en FD-3; ya no alimenta el aviso.
- (31/10/2026, aprobada; ajustada) FD-1 registra dos fechas: cuándo conoció la falta la jefatura y cuándo se avisó al Comité. El plazo de un mes para rescindir se calcula desde la primera. El RIT obliga a las jefaturas a avisar al Comité de inmediato, y el aviso tardío es una conducta del Anexo A.

**Corte del RIT del 12/11/2026** (modelo maestro cerrado para programación, rev. 1340; especificación v1.1)
- (12/11/2026, cambio del usuario) Art. 50 condicionado a VEHICULOS_ASIGNADOS (empresa, Sí/No, No por omisión).
- (12/11/2026, cambio del usuario) Formatos: toda declaración de la persona trabajadora es de su puño y letra, con una regla común para quien no sabe o no puede escribir, o se niega. Se eliminan FD2_VERSION, FD2_MANIFESTACIONES_FINALES, FD4_VERSION y FD5_VERSION.
- (12/11/2026, cambio del usuario) Art. 61: el expediente clínico se conserva durante la relación y hasta 2 años después. Se elimina ANIOS_CONSERVACION_EXPEDIENTE_CLINICO.
- (12/11/2026, cambio del usuario) Art. 51: responsabilidad de la persona usuaria por el uso de sus cuentas. Art. 80: «la jefatura y/o Recursos Humanos».
- (12/11/2026) Art. 59: se eliminan PERIODICIDAD_EXAMEN_MEDICO, DIAS_INCAPACIDAD_EXAMEN_RETORNO y DIAS_AVISO_EXAMEN_MEDICO. DIAS_RESPUESTA_DIAS_EN_CASA y TELE_AVISO_DIAS ya no se imprimen en el RIT: pasan a la política de trabajo híbrido.
- (12/11/2026, aprobada; encargo del módulo de permisos) Art. 31, tabla I: la fila del voto incluye los procesos de revocación de mandato (art. 132, fr. IX); fila fija nueva, bloqueada para el cliente, de comisiones accidentales o permanentes del sindicato o del Estado (fr. X), con o sin goce según decida la Empresa (COMISION_GOCE, nivel evento); sin goce, no se descuenta el tiempo compensado con trabajo.
- (12/11/2026, aprobada) Art. 31, evidencia no entregada: un permiso de la tabla II sin evidencia en plazo puede tenerse por otorgado sin goce, por decisión de RH, con reversión en la nómina siguiente si la evidencia llega después; los de la tabla I conservan su salario.
- (12/11/2026, aprobada) Anexo A, conducta 60 (muy grave): ausentismo reiterado. Ligada a la fr. XV del art. 47 (a valorar) en la tabla de correspondencia; solo se puede seleccionar con una alerta ALERTA_PATRON_* del módulo de permisos; las faltas con medida firme no se vuelven a sancionar, sirven de antecedente y de evidencia.
- (12/11/2026) Art. 31: criterio de días computables para la PTU, igual al de 4.7. Cerrado el encargo 8 del mapa.
- (12/11/2026, provisional) Art. 13: medio alterno de registro y aclaraciones del registro (DIAS_ACLARACION_REGISTRO). Art. 41: opinión de la Comisión Mixta de Capacitación con MOD_PRUEBA = Sí, y representantes designados o elegidos. Art. 88: los Anexos B, C y D se depositan de nuevo cuando cambian.
- (12/11/2026, propuestas de programación de la especificación, 11.1, por confirmar) Alertas del plazo a 10, 5 y 2 días y cierre del expediente al vencer; una falta leve con reincidencia se va a FD-1 → FD-3; casilla EXP_TENTATIVA (evento, Sí/No; con Sí baja un nivel); la conducta 21 solo se aplica con acuse de la política; recuadro manuscrito de 15 renglones.
- (12/11/2026) Decisiones retiradas por el usuario: «un retardo solo autoriza a no pagar el tiempo no laborado» y el cómputo del tiempo de comida.

**Retroalimentación de los corridos en el software (13 y 15/11/2026, decisiones del usuario; especificación v1.4)**
- Art. 25: días de pago por periodicidad (DIA_PAGO_SEMANAL, DIAS_PAGO_QUINCENAL, DIAS_PAGO_RESUMEN); se elimina DIA_PAGO.
- Art. 66: lactario opcional (LACTARIO, sin valor por omisión, preguntado antes que la ubicación); sin lactario, reducción de una hora de la jornada durante la lactancia.
- Arts. 47, 58 y 74 opcionales: limpieza general, ubicación del procedimiento de primeros auxilios y canal de denuncias (sin canal se omite el art. 74; la prohibición de represalias sigue en el art. 38).
- FD-3 ya no nombra el puesto que decide la rescisión: turna el expediente a la Empresa; RESCISION_RESPONSABLE solo para la notificación interna.
- FR-2 sin verificación periódica de la fijación (se elimina RIT_REVISION_FIJACION_MESES); la fijación física se conserva porque la exige la Ley.
- Art. 79: la integración del Comité sale del RIT a un documento propio; se eliminan ANEXO_COMITE, INTEGRANTES_COMITE, COMITE_PUESTO y COMITE_CARACTER; COMITE_INTEGRANTES queda como catálogo interno.
- Se quita del RIT el anexo de ubicación de las políticas (la Ley no lo pide y puede motivar observación en el depósito); se eliminan ANEXO_POLITICAS y POLITICAS_*.
- Acta de la CMRIT: CURP de todos los integrantes y del Anexo 1 (requisito del depósito); concordancia singular y plural; vigencia «mientras la Empresa tenga centros de trabajo en operación».
- (15/11/2026) Nuevo orden de anexos: A centros de trabajo (solo con más de un centro: nombre, domicilio, estado y registro patronal IMSS), B horarios, C catálogo de conductas. Con un solo centro las letras se recorren; el sistema las resuelve por identificador (ANX_CENTROS, ANX_HORARIOS, ANX_CONDUCTAS). Los formatos nombran los anexos por su contenido. **Toda referencia externa debe decir «catálogo de conductas del RIT», sin letra.**
- (15/11/2026) Un solo catálogo de centros para el dictamen, el Anexo A, la carátula del acta y el Anexo 1; toda persona y todo turno pertenecen a un centro del catálogo; CURP repetida, bloqueo.
- (15/11/2026) Art. 36: VAC_PROGRAMACION_MODO (Calendario anual · A solicitud), sin valor por omisión; con A solicitud no se pide el mes. El segundo párrafo remite al art. 30 (la solicitud se autoriza por la cadena).
- (12/11/2026) Art. 30: cadena de autorización para todo permiso (ver 4.9); arts. 16 y tabla II, asuntos personales: remiten al art. 30, con la jefatura como primer nivel.

**Firma del RIT y de la FR-1 (13/11/2026, decisión del usuario; resuelve la contradicción entre la especificación del RIT, el paquete de contratación y firma electrónica)**
- Los documentos necesarios para el depósito del RIT ante el CFCRL (el RIT firmado por la Comisión Mixta y el acta de integración de la CMRIT) se firman de forma autógrafa.
- La FR-1, que se genera ya con el RIT depositado y acredita la entrega a cada persona, se firma en sus tres momentos (emisión, ingreso y modificación) con la misma modalidad que los documentos de contratación de esa persona (FIRMA_MODALIDAD). Es autógrafa solo cuando la persona firma en papel, cuando falla la Plataforma o cuando se niega a firmar (dos testigos y envío al correo personal).
- Por la Empresa firma el representante al ingreso, dentro del paquete de contratación, y la persona de RH designada (FIRMANTES_EMPRESA) en la emisión y en la modificación.
- FR1_MEDIO (papel o enlace) solo indica cómo se entrega el ejemplar del RIT; no determina la forma de firma.
- Con el RIT depositado, la FR-1 sustituye a la fila RIT_ENTREGA del Anexo 3 del contrato, que solo se genera si el RIT no está depositado (decisión del paquete de contratación, 13/11/2026).

**Encargos del 17/11/2026 (especificación v1.5; maestro rev. 1377, formatos rev. 33)**
- Art. 36 con los tres valores de VAC_PROGRAMACION_MODO y párrafo nuevo, siempre impreso, sobre días en que no se programan vacaciones y número de personas por área. En el texto de periodos de solicitud se quitó la anticipación, porque la frase común del artículo ya la fija. (18/11/2026) Párrafo nuevo ajustado a la redacción final del módulo de vacaciones (encargo 15, v1.6).
- Especificación 2.6: el ajuste legal de jornada se comunica con MOD-2 del módulo 5; el anexo de horarios no cambia condiciones individuales.
- El documento del Comité se redacta en Axia Compliance; el RIT conserva la remisión del art. 79 y COMITE_INTEGRANTES.

**Encargos del 18/11/2026 (especificación v1.6; maestro rev. 1383)**
- Art. 36, última frase del párrafo de días sin vacaciones: «Esas medidas no modifican, sin la conformidad de la persona trabajadora, las vacaciones que haya solicitado o que se le hayan autorizado antes de que la Empresa las dé a conocer.» Prevalece lo que se registra primero. VAC_PROGRAMACION_MODO es un solo campo para el RIT y el módulo de vacaciones (regla de pantalla 4).
- (18/11/2026, decisión del usuario) DIAS_EN_CASA_EMPRESA deja de derivarse de TELE_APTO (eliminada): es pregunta de la configuración de la empresa, Sí/No, sin valor por omisión. Alerta, sin bloqueo, si un alta tiene DIAS_EN_CASA_ACTIVO = Sí y la empresa dice No. Se descartó derivarla de las altas porque la primera alta con días en casa cambiaría el RIT y obligaría a un nuevo depósito sin que nadie lo decidiera. Cambiarla con el RIT depositado activa la alerta de depósito.
- Descanso rotativo: el anexo de horarios imprime «N días por semana» (TURNO_DIAS_TRABAJO_SEMANA) y «Rotativo», sin tabla de días; el tipo de jornada es el calculado (nunca «Rotativa»). Art. 12, frase nueva con TURNOS_ROTATIVOS = Sí: el día de descanso se asigna conforme al contrato, sin más de seis días consecutivos de trabajo. El RIT no usa PUEDE_SALIR.
- (18/11/2026, decisión del usuario) **Los plazos del expediente disciplinario se cuentan en días naturales**, no hábiles: reporte de la jefatura al Comité (art. 81 y conducta 43), audiencia (arts. 81 y FD-1), notificación de la resolución (art. 81 y FD-2), inicio de la suspensión (art. 81 y FD-3) y revisión de la falta leve (art. 80 y FD-4). El plazo de 30 días naturales del art. 83 no cambia. Resuelve el cómputo con descanso rotativo. (18/11/2026, aprobado por el usuario) Si la audiencia o el inicio de la suspensión caen en un día de descanso de la persona, pasan a su siguiente día laborable; si el plazo de revisión de la persona vence en su día de descanso, se extiende a su siguiente día laborable. La duración de la suspensión (1 a 8 días) se cuenta en días laborables del turno. Las fechas exactas las decide RH: el sistema las propone con estas reglas y RH puede cambiarlas, con las validaciones de plazo de la especificación (4.3). (18/11/2026) Aplicado en la especificación v1.7 (maestro rev. 1388, formatos rev. 39): arts. 80 y 81, párrafo final nuevo del art. 81 («Recursos Humanos fija la fecha de la audiencia y las del inicio y el término de la suspensión dentro de los plazos de este artículo y del artículo 83…»), conducta 43 («a más tardar al día siguiente de conocerla»), FD-2 y FD-4; los días de descanso obligatorio cuentan como días de descanso.

### 4.5 Comisión Mixta del RIT
- Acta de integración y estatutos fusionados en un solo instrumento.
- (31/10/2026) Número de representantes: NUM_REPRESENTANTES_POR_PARTE (mínimo 1). La falta de acuerdo se asienta y sigue aplicándose el texto vigente.
- Se redacta como designación de integrantes, sin documentar elecciones ni votaciones, con la conformidad de las personas trabajadoras.
- (02/11/2026, aprobada; sustituye el criterio del 26/10) **Criterio común de las tres comisiones (RIT, capacitación y PTU): en ninguna hay votación secreta.** Por omisión, las personas trabajadoras designan a su representación; el documento hace constar la designación, la aceptación de los representantes y que la Empresa no intervino. Refuerzo opcional: relación de conformidad firmada (CONFORMIDAD_FIRMAS). Elección formal opcional (DESIGNACION_OBRERA = Elección), sin voto secreto, en una jornada común con D-01 y D-02 del kit de PTU. Con sindicato, la designa el sindicato. El usuario no obliga al cliente a celebrar elecciones ni a conservar sus evidencias; riesgo explicado una vez, se mantiene.
- (02/11/2026) Variables comunes de las tres: DESIGNACION_OBRERA (sustituye a CMRIT_INTEGRACION_MODO), NUM_REPRESENTANTES_POR_PARTE (mínimo 1) y REPRESENTANTES_SUPLENTES (Sí por omisión). El personal de confianza participa pero no puede ser representante. Una persona puede representar en más de una comisión.
- Los firmantes alimentan la tabla de firmas del RIT. El RIT solo toma del acta FECHA_ACTA_INTEGRACION y los representantes.
- (12/11/2026) Criterio común aplicado en el acta de la CMRIT (rev. 33 y 36): DESIGNACION_OBRERA, REPRESENTANTES_SUPLENTES y CONFORMIDAD_FIRMAS; el Anexo 1 de conformidad solo con CONFORMIDAD_FIRMAS = Sí; la elección remite a D-02; sin votación secreta. Encargo 7 del mapa cumplido.

### 4.6 Comisión Mixta de Capacitación, Adiestramiento y Productividad
- Objeto reducido a las funciones legales. (24/10/2026) La Base 2 excluye expresamente la disciplina, las sanciones, la terminación, el salario y la nómina.
- El personal de confianza vota, pero no puede ser candidato.
- Coordinación fija patronal y secretaría obrera. (26/10/2026, aprobada) La secretaría puede suplir a la coordinación solo para convocar y conducir una sesión, sin cambiar su titularidad.
- (26/10/2026, aprobada) Sin alerta automática de solicitud de opinión en el PMV ni variable de días de aviso: el formato F-2 se genera e imprime junto con los documentos de terminación al vencer el periodo.
- (24/10/2026, aprobada) La cláusula del periodo de prueba o de la capacitación inicial se trabaja en el contrato; la terminación va al kit; la comisión solo conserva la Base 14 y el formato F-2.
- (02/11/2026) La integración sigue el criterio común (4.5): designación por omisión; la convocatoria, la constancia y el acta de elección propias se sustituyen por D-01 y D-02 del kit de PTU, solo si se elige el módulo de elección. Instrumento base: acta de integración e instalación con Bases de Funcionamiento. Formatos F-1 (acta de sesión), F-2 (opinión sobre el periodo), F-3 (firma digitalizada), F-4 (sustitución) y F-5 (informe anual).
- (24/10/2026, provisional) Variante con sindicato (oficio de designación; sin convocatoria, constancia ni acta de elección) y variante sin sindicato.
- (02/11/2026) Solo si se usa el módulo opcional de elección: mesa de personas trabajadoras, votación sin voto secreto, publicación al menos 5 días hábiles en cada centro y por medio digital, válida con más del 50 % del padrón y segunda jornada dentro de 10 días hábiles sin umbral.
- (24/10/2026, provisional) Requisitos de candidatura: prestar servicios en el centro, no ocupar puesto de confianza y no formar parte de la representación patronal. Los representantes patronales se designan por nombramiento escrito.
- (24/10/2026, provisional) Quórum: mitad más uno de los propietarios y al menos uno de cada representación. Acuerdos por mayoría de cada representación, sin voto de calidad; si no hay acuerdo, el acta registra la posición de cada parte. Duración del cargo, cinco causas de sustitución y procedimiento para cubrir vacantes.
- (24/10/2026, provisional) La comisión emite opinión, no dictamen, sobre los periodos de prueba y de capacitación inicial. Sin acuerdo, se registra la opinión de cada representación. Si no se emite a tiempo, se levanta constancia de que se solicitó oportunamente.
- (24/10/2026, provisional) La DC-3 se autentifica con al menos una firma de cada representación. La firma digitalizada solo procede por acuerdo unánime (F-3) y se revoca al sustituir al firmante. Si la plantilla es de 50 o menos, la Empresa autentifica la DC-3.
- (24/10/2026, provisional) La Empresa firma y conserva el DC-1. La lista de constancias se presenta por SIRCE (el DC-4 se eliminó en abril de 2025). Plazos: DC-3 dentro de 20 días hábiles y presentación en SIRCE dentro de 60 días hábiles.
- (24/10/2026, provisional) Módulo opcional de productividad (Base 3.11 y Base 17).
- (24/10/2026, provisional) Se usa la denominación legal de la comisión, con la aclaración de que es la misma de los periodos de prueba y capacitación inicial.

### 4.7 PTU
- Procedimiento con y sin sindicato.
- La cifra contable la captura el cliente. Turnos y centros de trabajo son variables.
- (24/10/2026, provisional) Kit de 13 documentos (D-01 a D-13) en cinco fases: integración, declaración anual, proyecto, observaciones, y pago con contingencias. Sustituye a los diez documentos anteriores.
- (24/10/2026, provisional) Fusiones: acta de integración y estatutos (D-03), con el mismo criterio que la CMRIT; el acta de entrega de la declaración absorbe la constancia del Anexo I (D-05); la constancia de publicación absorbe el cierre del periodo de observaciones (D-09); una sola plantilla de convocatoria a sesión (D-04).
- (24/10/2026, provisional) Dictamen con un solo módulo según el resultado: A sin cantidad repartible, B con reparto, C excepción legal. El módulo A se funda en la renta gravable para PTU, sin disminuir pérdidas de ejercicios anteriores.
- Representación patronal designada por la Empresa. Representación obrera según el criterio común (4.5). El personal de confianza no puede ser representante obrero.
- (24/10/2026, provisional) La copia de la declaración se entrega al sindicato o a los representantes obreros en su carácter de mayoría. La comisión no objeta ante el SAT. Sin acuerdo entre representaciones, el desacuerdo se somete al Inspector del Trabajo en 3 días hábiles.
- (24/10/2026, provisional) Plazos en días hábiles; el proyecto se publica a más tardar 45 días hábiles antes del límite de pago.
- (02/11/2026) D-01 y D-02 son el módulo opcional de elección, común a PTU y capacitación, con boleta separada por comisión.
- (02/11/2026, aprobada) CONFORMIDAD_FIRMAS se recomienda con RESULTADO = B, sin exigirla.
- (02/11/2026, aprobada) Días computables: laborados, vacaciones, permisos con goce de salario e incapacidades por riesgo de trabajo y maternidad. No se computan faltas, permisos sin goce, suspensiones ni incapacidades por enfermedad general. El RIT debe recoger el mismo criterio.
- (02/11/2026, aprobada) PTU no cobrada: un año para reclamar (art. 516) desde el día siguiente a la fecha límite de pago; vencido, el monto pasa al reparto siguiente. Una reclamación tardía se registra y se alerta a consultoría para hacer valer la prescripción, que no opera de oficio.
- (26/10/2026, provisional) Layout de importación por CURP con totales de control; errores bloquean D-08 B, advertencias no. Control de PTU no cobrada con cinco estados y recordatorio a los 60 días. PTU pendiente en el finiquito: con monto si el dictamen está firme; sin monto y con leyenda si no; «Pagada en finiquito» bloquea un segundo pago.
- (26/10/2026, aprobada) El personal de confianza vota en la elección, pero no puede ser representante obrero.
- (26/10/2026, aprobada) El tiempo dedicado a cualquier comisión mixta es tiempo de trabajo con goce de salario.
- (26/10/2026, aprobada) El dictamen tiene una versión publicable sin salario diario (nombre, días computables y monto); la versión completa queda a disposición de la comisión y de cada persona respecto de sus propios datos.
- (26/10/2026, aprobada) La vía de captura pide, por persona, días trabajados y salario devengado del ejercicio; no se admiten solo totales globales.
- (26/10/2026) Cálculo por dos vías: importación de nómina o captura (ver el mapa sobre los datos mínimos por persona).
- (12/11/2026, provisional) D-01 y D-02 sin voto secreto en ninguna variante: la votación se hace como acuerden las personas asistentes (mano alzada, lista firmada o boleta); D-02 ya no pide boletas como anexo.
- (12/11/2026, provisional) **Precálculo neto de la PTU (regla R-5)**, con los parámetros versionados del módulo 4: parte exenta hasta 15 veces REF_EXENCION (art. 93, fr. XIV LISR); ISR por el método del art. 174 RLISR (por omisión) o el del art. 96 LISR (PTU_ISR_METODO, por empresa); ex trabajadores y personas sin ingreso ordinario siempre por el art. 96; sin subsidio, sin cuotas IMSS ni amortización Infonavit (la PTU no integra el SBC); pensión alimenticia solo si la resolución comprende la PTU (PENSION_INCLUYE_PTU, PENSION_BASE_PTU en el alta); otras deducciones en tabla dinámica con aviso del art. 130 LFT. Neto negativo bloquea; el contador valida (PTU_CALCULO_VALIDADO) antes del D-14 final. D-14 imprime exento, gravado, ISR y deducciones mayores que cero.
- (13/11/2026, decisión del usuario) Fonacot no se descuenta de la PTU (cuota mensual fija retenida del salario, art. 110, fr. VII LFT); si la persona causa baja, la retención se ve en el finiquito.
- (13/11/2026) Art. 174 RLISR verificado (última reforma DOF 06-05-2016). El sistema aplica la tasa a la parte gravada; el contador puede sustituir la retención por la tasa sobre el total (criterio conservador).
- (12/11/2026) Días computables y aguinaldo: los días por persona se toman de los eventos del módulo de permisos y del registro de vacaciones (fuente única).

### 4.8 Terminación y precálculo de finiquito (actualizado el 15/11/2026 con el corte del módulo 4 del 12/11)

Documento de referencia: «AXIARH - Modulo 4 - Especificacion para programacion», **v1.4 (12/11/2026), terminada y cargada en el software**. Las decisiones del 26 y 27/10 que la v1.2 a la v1.4 sustituyeron quedan solo en el historial de la especificación.

**Paquete documental**
- (10/11/2026, decisión del usuario) Un solo convenio, siempre por mutuo consentimiento (art. 53, fr. I), en toda baja salvo fallecimiento; se eliminan los módulos A a E-bis. El motivo de baja (BAJA_MOTIVO) es un dato interno para el cálculo y los documentos de respaldo; no se imprime.
- (10/11/2026) Convenio reforzado: declaraciones de hechos de la Persona Trabajadora, finiquito y desistimiento amplios (frente a la Empresa, sus representantes, socios, empresas relacionadas y clientes), imputación de la gratificación a cualquier diferencia futura, PTU a salvo (art. 987), finiquito de la Empresa con excepciones (bienes, confidencialidad, hechos desconocidos), reconocimiento de documentos, leyenda manuscrita, huella y firma al margen; comprobante de transferencia como Anexo 2. Sin pena por retraso ni obligación de ratificar (27/10).
- (12/11/2026, decisión del usuario) El convenio y el recibo se firman siempre de forma autógrafa, aunque FIRMA_MODALIDAD = Electrónica.
- (12/11/2026) Recibo en una sola hoja carta, con RFC de la Persona Trabajadora; si no cabe, ajusta márgenes y espacios y, al final, tablas en Arial 10. Columna «Factor» sin fórmula.
- (10/11/2026) No se genera formato de renuncia. Los comunicados de fin del periodo y de vencimiento son documentos de respaldo que solo se generan si se cumplen sus requisitos; con «Continuar sin requisitos» la baja sigue con convenio y recibo y se registra usuario y fecha (CANDADOS_OMITIDOS). Riesgo explicado una vez: sin requisitos, la terminación depende de la firma del convenio.
- (10/11/2026) Constancia de servicios opcional (CONSTANCIA_SERVICIOS); la constancia de negativa a firmar es una hoja aparte que se genera con un botón; ningún documento imprime espacios para testigos.
- (26/10/2026) El escenario de negociación nunca se imprime en los documentos de la baja; solo en pantalla y en la hoja interna.

**Motivos de baja**
- (10/11/2026) Una sola lista de motivos legales, sin «¿quién decide?» y sin «despido injustificado»; solo son obligatorios motivo, fecha de baja y forma de pago.
- (10 y 12/11/2026, decisión del usuario) Se elimina el bloqueo por situaciones protegidas y, en la v1.3, también su mensaje fijo. - (15/11/2026, aprobada por el usuario; resuelve la contradicción con el módulo de permisos) **Situaciones protegidas sin bloqueo.** SITUACION_PROTEGIDA (incapacidad C1 o C2 en curso, maternidad C3, lactancia B1, Declaración Especial de Ausencia D5 y licencia por hijo con cáncer B3) ya no bloquea la baja: genera una alerta crítica en la pantalla «Retirar colaborador» y exige doble confirmación, con registro de usuario, fecha y hora (BAJA_CONFIRMACION_PROTEGIDA). La comisión permanente vigente (B4) sigue la misma mecánica con BAJA_CONFIRMACION_B4. El dato nunca se imprime. Así queda constancia de que la Empresa conocía la situación y decidió continuar.
- (12/11/2026, provisional; del módulo de permisos) Suspensión por falta de documentos (D4) vencida: actualiza la causa del art. 47, fr. XIV Bis; consultoría decide y prepara el aviso (servicio aparte). El sistema no termina la relación.
- (26/10/2026) Temporada: el fin de temporada suspende la relación (arts. 39-F y 42, fr. VIII); no se ofrece el motivo de vencimiento.

**Precálculo**
- (10/11/2026, decisión del usuario) **Neto estimado**: percepciones brutas, ISR ordinario (exenciones del art. 93 y tarifa del art. 96), ISR de separación (exento hasta 90 veces la unidad por año; tasa del USMO sobre la parte gravada; si los pagos por separación son menores que el USMO, se suman a la base ordinaria), subsidio para el empleo y cuotas obreras del IMSS. Leyenda «ISR y cuotas estimados; los definitivos constan en el CFDI de nómina». Unidad de referencia REF_EXENCION (UMA por omisión). Cotejado con la LISR vigente (última reforma DOF 01/04/2024) y el Anexo 8 RMF 2026.
- (12/11/2026) Parámetros 2026 precargados como aprobados; sin parámetro, el concepto dice «No calculado» (nunca $0.00) y no se puede validar. Caso de prueba en el Anexo A.3 de la especificación.
- (26/10/2026) Escenario de negociación en capas (finiquito; 90 días de SDI; 20 días por año solo con supuesto del art. 49 o rescisión del art. 52; riesgo de salarios vencidos e intereses). El excedente se llama «gratificación por terminación», salvo en la rescisión del art. 51.
- (26/10/2026, aprobada) Prima de antigüedad obligatoria y bloqueada donde la ley la impone; opcional (PA_INCLUIR) en los demás casos, con registro de quién la marcó. Salario topado al doble del mínimo del área.
- (26/10/2026, aprobada) Previsualización con cifras propias y umbrales que no bloquean; ningún convenio ni recibo en versión final sin CALCULO_VALIDADO; único bloqueo: neto negativo.
- (12/11/2026) Otras deducciones en tabla dinámica (Infonavit, Fonacot, pensión alimenticia, pérdida o daño, anticipo, otra), con renglones automáticos por créditos y pensión del alta; aviso si rebasa el art. 110, fr. I. Pérdida o daño solo con expediente concluido (art. 46 del RIT).
- (26/10/2026) La PTU pendiente no se suma; la PTU determinada y no pagada sí.
- (15/11/2026, del módulo de vacaciones) Saldos de vacaciones, proporcionales y días prescritos (solo informativos) según la sección 11 de la especificación de vacaciones; el aguinaldo ya pagado en el año no se duplica (encargo en el mapa).

**Servicios aparte y aviso de rescisión**
- (12/11/2026) El sistema ya no recomienda ratificación ni paraprocesal; el aviso de rescisión es un servicio aparte que el sistema no genera. Queda solo el mensaje informativo con los plazos de los arts. 47 y 517.

**Baja sin firma**
- (10/11/2026) Secuencia de alertas desde BAJA_FECHA (día 0, 2, 4 y después cada ALERTA_BAJA_INTERVALO días hábiles con escalamiento) con mensaje por motivo; cesa con los documentos firmados (BAJA_FIRMA_EVIDENCIA) o con «Cerrar seguimiento» (BAJA_SEGUIMIENTO_CERRADO). El finiquito nunca se retiene por falta de firma.

**Pago a beneficiarios**
- (26/10/2026, provisional) Ruta por designación (vigente, confirmada en los últimos 12 meses, sin controversia y total menor que BENEF_UMBRAL) o ruta Tribunal; solo el pago por resolución del Tribunal libera frente a terceros. El pago por designación nunca en efectivo.

**Acta de devolución**
- (26/10/2026) No condiciona el pago; faltantes y daños abren expediente conforme al art. 46 del RIT; cierre de accesos a más tardar el día hábil siguiente a la baja; requerimiento por correo si la persona no se presenta. La regla 2 de la sección 7.7 de la especificación conserva la redacción anterior del art. 46 (encargo en el mapa).

### 4.9 Permisos y licencias (12/11/2026)

Documento de referencia: «AXIARH - Módulo de permisos y licencias - Especificación para programación» (v1.8, 17/11/2026; la 1.5 armoniza con firma electrónica v1.2 y el RIT v1.3, la 1.6 con el módulo de vacaciones, la 1.7 aplica los encargos del 17/11 y la 1.8 la reubicación en D4). Las decisiones del módulo están en «Corte - Módulo de permisos y licencias»; aquí solo se registran las que tocan otros documentos.
- (12/11/2026) Conversación propia, separada del RIT. El RIT es la fuente de las reglas; el módulo las ejecuta.
- (12/11/2026; ajustada el 13/11) Fuente única: el evento de este módulo y el registro de vacaciones (VAC-1) son las únicas fuentes de ausencias justificadas para nómina, IMSS, PTU, aguinaldo, finiquito y análisis de jornada; ningún otro módulo captura ausencias. Un solo evento de día completo por persona y fecha, incluidos los días de vacaciones; la incapacidad prevalece.
- (12/11/2026) Catálogo de 18 eventos en cuatro familias: A permisos, B licencias, C incapacidades del IMSS y D suspensiones del art. 42. Lo que no encaja es falta y va por la vía disciplinaria del RIT.
- (12/11/2026) Los registros digitales SP-1, SUS-3 y el acuse de LIC-2 se apoyan en el «Corte - Firma electrónica» y en la cláusula de formalización por medios electrónicos del contrato.
- (12/11/2026, decisión del usuario) No se crea TRIBUNAL_COMPETENTE en el alta de la empresa. El art. 504, fr. V LFT (cotejado con el texto vigente) exige dar el aviso de accidente también al Tribunal, por lo que INC-1 lo menciona con texto fijo, sin variable. (12/11/2026) Aplicado en la especificación v1.4; TRIBUNAL_COMPETENTE eliminada.
- (13/11/2026) LIC-1: con LACTARIO = No solo se ofrece la reducción de una hora (art. 66 del RIT).
- (12/11/2026, decisión del usuario) **Cadena de autorización.** Los permisos que otorga la Ley (A1, A2, A3, B2), los permisos de la Empresa (A4) y la licencia sin goce (B5) se autorizan por jefatura inmediata (PERSONA_JEFATURA), RH y dirección del área (DIRECTOR_AREA) si existe. El representante legal no interviene. Cadena por omisión en CADENA_AUTORIZACION (empresa); cada concepto de PERMISOS_EMPRESA puede tener una más corta, con RH siempre como paso (B5, siempre completa). Nadie autoriza su propio permiso; quien ocupa dos pasos autoriza una vez. Cada paso tiene AUTORIZACION_PLAZO_DIAS días hábiles (1 por omisión); la falta de respuesta no es autorización y RH puede reasignar a un suplente. Si llega la fecha sin resolución y la solicitud se hizo a tiempo, RH resuelve ese día y la ausencia no es falta.
- (12/11/2026, decisión del usuario) **Permisos que otorga la Ley:** pasan por la cadena, pero no pueden negarse (art. 132, frs. IX, X y XXVII Bis, y art. 170 LFT). La cadena solo verifica datos, aviso y evidencia y puede «Devolver para corrección» (DEVOLUCION_MOTIVO); en A3 solo puede limitar el número de comisionados. Si llega la fecha sin autorización completa, RH lo registra y la ausencia nunca es falta. Licencias, incapacidades y suspensiones (B1, B3, B4, C y D) no pasan por la cadena: RH registra y la jefatura y la dirección reciben aviso.
- (12/11/2026) Negativa de permisos de la Empresa: solo por las causas del art. 33 del RIT (NEGATIVA_CAUSA: requisitos no subsanados o necesidad operativa concreta).
- (12/11/2026, decisión del usuario) **Firma de la Empresa:** en LIC-1, LIC-3, INC-2, SUS-1 y SUS-2 firma la persona de RH que la Empresa designe (FIRMANTES_EMPRESA, configuración de la empresa), solo entre puestos con funciones de dirección o administración, con usuario y código de un solo uso. El representante legal solo firma INC-1, con e.firma o de forma autógrafa. FIRMA_EMPRESA_NOMBRE y FIRMA_EMPRESA_CARGO pasan a derivarse del firmante designado. (12/11/2026) Resuelto: la especificación de firma electrónica prevé al firmante de RH desde la v1.1.
- (12/11/2026; resuelta el 13/11/2026 en el RIT v1.3) El art. 30 del RIT prevé la cadena para todo permiso, incluidos los legales, sin negarlos (si llega la fecha sin autorización completa, RH los registra y la ausencia no es falta); el art. 16 y la tabla II remiten al art. 30.
- (17/11/2026, especificación v1.7) SITUACION_PROTEGIDA ya no bloquea la baja (decisión 19, 4.8); el módulo envía además SITUACION_PROTEGIDA_TIPO para el texto de la alerta. B3 no computa para el aguinaldo. Al cerrar C2 se pregunta INCAPACIDAD_PARCIAL e INCAPACIDAD_PARCIAL_FECHA (dictamen del IMSS como evidencia, sin diagnóstico) para el módulo 5. NEGATIVA_CAUSA admite «Cupo completo», solo en vacaciones. La lectura de SUSP_VACACIONES_GENERA quedó confirmada con el módulo de vacaciones (los días generados no exceden los que quitó la reducción). La incapacidad interrumpe las vacaciones.
- (17/11/2026, decisión del usuario; especificación v1.8) **D4 con reubicación:** si la persona acepta la reasignación temporal (MOD-5, causa «Falta de documentos»), sustituye a la suspensión mientras dure: no se genera SUS-2, el evento queda «Con reubicación», se paga el salario y los días cuentan como trabajados para nómina, IMSS, PTU, aguinaldo y vacaciones. El plazo de dos meses sigue corriendo desde SUSP_CONOCIMIENTO_FECHA (arts. 43, fr. IV, y 47, fr. XIV Bis, cotejados), con alertas en los días 45 y 60; a los 60, consultoría decide. Si la reubicación termina sin regularizar, se genera SUS-2 desde esa fecha. Riesgo explicado una vez: no se localizó criterio sobre si la reubicación debilita la rescisión por tolerancia. Variables D4_REUBICACION y D4_REUBICACION_FIN, que entrega el módulo 5.

### 4.10 Vacaciones y aguinaldo (15 y 16/11/2026)

Documento de referencia: «AXIARH - Módulo de vacaciones y aguinaldo - Especificación para programación» (v1.2, 17/11/2026; sustituye a la v1.1, que no se cargó) y sus textos (sexta versión, 17/11/2026). Conversación propia; el RIT no se modifica desde ella. Decisiones completas en «Corte - Módulo de vacaciones y aguinaldo».
- (14/11/2026, decisión del usuario) RH no asigna vacaciones: la Persona Trabajadora elige las fechas y las solicita por la Plataforma con DIAS_ANTICIPACION_VACACIONES; la solicitud pasa por la cadena de permisos con las acciones Autorizar, Reprogramar (propuesta que la persona acepta o no) y Devolver; no existe Negar. Recordatorios 60 y 30 días antes de VAC_LIMITE_OTORGAMIENTO, con copia a jefatura y RH, como evidencia (art. 784, fr. X).
- (14/11/2026) VAC_PROGRAMACION_MODO: Calendario anual (con preferencias de cada persona) o A solicitud. (15/11/2026) Sin valor por omisión, por la regla general de pantalla del RIT; se captura una sola vez para el RIT y este módulo.
- (14 y 15/11/2026) VAC-2 (constancia del art. 81) en cada aniversario; imprime el periodo del aniversario al aniversario + 6 meses. Después la persona puede seguir pidiendo sus días hasta la prescripción (18 meses del aniversario), con alerta a RH y consultoría por cada solicitud tardía; la fecha de prescripción nunca se imprime. Al prescribir, el saldo pasa a Prescrito (no se borra).
- (14/11/2026) Una incapacidad (C1, C2, C3) suspende las vacaciones; los días vuelven al saldo y lo pagado queda a cuenta; si empieza antes, las vacaciones no inician; los plazos no se extienden (Convenio 52 OIT, art. 2.3; por verificar).
- (14/11/2026) Proporcionales solo a la terminación (módulo 4); sin vacaciones anticipadas; reingreso reinicia todo (alerta a consultoría dentro de REINGRESO_ALERTA_DIAS); temporada, art. 77 con redondeo hacia arriba; menores de 18 años, mínimo 18 días. Suspensiones largas (B4, B5, D2, D3): los años de servicio cuentan, los días se descuentan en proporción y se suman los VACACIONES_DIAS_GENERADOS que RH decida (lectura confirmada con permisos el 17/11/2026).
- (14/11/2026) Aguinaldo: AGUINALDO_DIAS ≥ 15 (prevalece el del puesto en PRESTACIONES_EXTRA), pago a más tardar el 19 de diciembre (AGUINALDO_FECHA_PAGO), base salario ordinario, cálculo al 31 de diciembre; proceso anual con cálculo provisional 30 días antes, revisión de RH, validación del contador (AGUINALDO_VALIDADO), exportación a nómina y registro del pago en el módulo 6. En bajas se paga en el finiquito, sin duplicar.
- (14/11/2026, decisión del usuario) AGUINALDO_COMPUTA con el criterio de días computables de la PTU (4.7): computan laborados, descansos y festivos, vacaciones, permisos con goce, B1, B2, C2, C3, días de espera pagados de C1 y D1 por la fr. III acreditada; no computan C1, permisos sin goce, B3, B4, B5, D1 a D5, faltas, suspensión disciplinaria ni fin de temporada.
- (16/11/2026, decisión del usuario) Tercer modo de VAC_PROGRAMACION_MODO: **periodos de solicitud por antigüedad**. Cada año se configuran grupos de antigüedad con su periodo de solicitud (primero el de mayor antigüedad); al cierre de cada periodo las solicitudes se asignan por antigüedad conforme a los cupos; sin lugar, queda Reprogramada con causa «Cupo completo» y hasta tres alternativas; al cerrar el último periodo se solicita en fechas libres. Quien no solicita no pierde días.
- (16/11/2026, decisión del usuario; ajustada el 17/11/2026) **Días bloqueados** por operación o capacitación, con alcance (empresa, centro, área o puesto). El bloqueo se guarda en borrador y solo se activa si no impide a nadie disfrutar sus días dentro del plazo legal (art. 81). (17/11/2026, aclaración del usuario) **Prevalece lo que se registra primero:** con el bloqueo activo, esos días no pueden solicitarse; las vacaciones solicitadas (en cualquier estado activo) o autorizadas antes de la activación no se modifican sin la aceptación de la persona, y la cadena no puede reprogramarlas por el bloqueo. Se compara EVENTO_SOLICITUD_FECHAHORA con VAC_BLOQUEO_ACTIVACION; un borrador de solicitud no está protegido. Se elimina la devolución automática de solicitudes al activar un bloqueo.
- (16/11/2026, aprobada) **Cupos por área** opcionales: máximo de personas de vacaciones el mismo día; por antigüedad con periodos de solicitud y por orden de llegada en los demás modos; si el cupo es imposible, aviso sin bloqueo.
- (16/11/2026, decisión del usuario) **Avisos N-1 a N-6** (apertura, cierre próximo, resultado, días bloqueados, saldo y resolución) por correo personal, app o ambos (VAC_NOTIFICACION_CANALES); siempre también en la Plataforma; cada envío en bitácora como evidencia (art. 784, fr. X). Las notificaciones push dependen de la app del colaborador (fase 2).
- (16/11/2026) VAC-2 imprime el grupo y periodo de solicitud de la persona y los días bloqueados vigentes; los bloqueos posteriores se comunican con N-4.
- (17/11/2026) Especificación v1.2: base SALARIO_PERSONA para vacaciones, prima, aguinaldo y finiquito; días laborables según la versión de condiciones y las constancias MOD-5; baja con AGUINALDO_VALIDADO y sin pago: aviso al contador y cancelación de la obligación en el módulo 6 con motivo «Pago en finiquito».
- (16/11/2026) Requiere el nuevo art. 36 del RIT (aplicado en el RIT v1.5; párrafo nuevo con la redacción final en la v1.6, 18/11/2026) antes de que un cliente use periodos de solicitud, bloqueos o cupos; cambiar de modo con el RIT depositado exige nuevo depósito. Con contrato colectivo, sus reglas de preferencia prevalecen.
- (14/11/2026) El cuadro general de antigüedades (art. 158) es otro instrumento; pendiente decidir si entra al PMV.

### 4.11 Firma electrónica (12/11/2026)

Documento de referencia: «AXIARH - Firma electrónica - Especificación para programación» (v1.4, 18/11/2026) y «Corte - Firma electrónica». Rige a toda la familia Axia.
- (12/11/2026, decisión del usuario) Dos tipos para la Persona Trabajadora: firma electrónica simple con código de un solo uso al correo personal y, según FES_CANAL_OTP, al celular (por omisión), o e.firma del SAT. Ninguno requiere PSC; la constancia NOM-151 es un servicio opcional por empresa (NOM151_SERVICIO).
- (12/11/2026) Bitácora, hoja de evidencias, hash SHA-256 y copia inmediata al correo personal; paquete probatorio exportable (art. 836-D LFT). La plataforma nunca recibe ni guarda la llave privada ni la contraseña de la e.firma.
- (12/11/2026) Primera firma con verificación presencial de identidad; a distancia, e.firma o autógrafa; la FES remota sin verificación se permite con alerta permanente.
- (12/11/2026) El representante firma siempre con e.firma; alerta 30 días antes del vencimiento del certificado y bloqueo de envíos con certificado vencido o revocado.
- (12/11/2026) **Quién firma por la Empresa:** todo lo que se firma en el alta, el representante; los documentos posteriores, según FIRMA_EMPRESA_DOC: representante (adenda de confidencialidad, convenios de modificación, constancia de designación, INC-1) o persona de RH designada en FIRMANTES_EMPRESA (solo puestos de confianza con funciones de dirección o administración; designación firmada por el representante con e.firma). Se puede subir un documento de RH a representante, nunca al revés. Sin firmante de RH vigente, firma el representante.
- (16/11/2026, decisión del usuario; especificación v1.3) **Verificación remota de identidad con INE y video de aceptación**, opcional para la persona y solo con IDV_SERVICIO = Sí (servicio que se cobra aparte): validación de la credencial con el INE, prueba de vida, cotejo facial y video de aceptación con guion y código aleatorio. Requiere consentimiento expreso (BIOMETRICO_FIRMA_CONSENT), con la alternativa sin biometría (presencial, e.firma o papel) y sin consecuencia laboral si se rechaza o falla. La plantilla biométrica se borra después del cotejo; se conservan el resultado, el video y la bitácora. Solo para quien tiene credencial para votar.
- (18/11/2026, decisión del usuario; corrige la v1.3; especificación v1.4) La verificación con INE y video **solo se usa en la contratación** (alta).
- (18/11/2026, decisión del usuario; decisión 17 del «Corte - Firma electrónica») **El cambio de correo o teléfono se verifica siempre de forma presencial, sin biometría.** Sustituye la parte de la decisión del 16/11/2026 que permitía usar INE y video en ese cambio.
- (12 y 13/11/2026) **Firma autógrafa obligatoria**, sea cual sea FIRMA_MODALIDAD: convenio de terminación, recibo de finiquito, acuerdo de descuento, el RIT y el acta de la CMRIT (depósito), FD-1 a FD-5, FR-2 y FON-1 (firma autógrafa de recibido). La FR-1 sigue FIRMA_MODALIDAD (4.4).
- (18/11/2026, decisión del usuario) **Acta de devolución y entrega de herramientas:** admite ambas formas, firma electrónica o autógrafa, según se haga la entrega. Es documento posterior al alta. Los testigos solo se usan si la persona se niega a firmar.

### 4.12 Modificación de condiciones de trabajo — módulo 5 (15/11/2026)

Documento de referencia: «AXIARH - Módulo 5 - Especificación para programación» (v1.0) y «AXIARH - Módulo 5 - Textos y reglas (borrador)». Modelo maestro terminado por el usuario el 15/11/2026 (aprobaciones provisionales). La matriz de cambios del mapa queda sustituida por la sección 2 de la especificación.
- (15/11/2026) **Convenio modificatorio único (MOD-1)** con apartados fijos de puesto y funciones, jornada, y salario y prestaciones, y módulos de ascenso, centro fuera del ámbito, híbrido, teletrabajo y regreso a presencial. Un cambio del perfil sin cambiar la naturaleza del puesto solo genera la firma de la nueva versión del perfil.
- (15/11/2026, decisión del usuario) **Reducciones** (salario, prestaciones, categoría o duración con salario proporcional) solo por convenio, nunca por comunicado; sin firma no hay reducción. El convenio no imprime plazo de inconformidad; queda una alerta interna, no visible para la persona, durante un mes desde la firma (MOD_REDUCCION_ALERTA_FIN). Riesgo explicado una vez (arts. 33, 51, fr. IV, 516 y 517 LFT); se mantiene.
- (15/11/2026, decisión del usuario) **Salario individual sin restricciones** (SALARIO_PERSONA; ver sección 2). Riesgo de igualdad salarial ya señalado en la revisión de pantallas (hallazgo 7).
- (15/11/2026) **Jornada:** convenio si aumenta la duración o cambia el tipo, los días, el descanso, el turno o el horario; comunicado solo para la reducción legal (lote del art. 8 del RIT, «Ajuste legal de jornada») y la reducción de horas sin reducir salario.
- (15/11/2026) **Días en casa:** presencial a híbrido, convenio; ajuste o revocación dentro del híbrido, comunicado con TELE_AVISO_DIAS; más de 40 %, convenio de teletrabajo; regreso de teletrabajo, comunicado si se ejerce la reversibilidad pactada y convenio si se pacta otra cosa.
- (15/11/2026) **Centro:** dentro del ámbito, comunicado sin plazo; fuera del ámbito, convenio. **REPSE:** entre clientes, oficio con ASIGNACION_AVISO_DIAS; de la Empresa a un cliente, oficio y comunicado; de un cliente a la Empresa, comunicado; fin del contrato con el cliente, alerta para reasignar, nunca baja.
- (15/11/2026, decisión del usuario) **Cambio de puesto** sin periodo de prueba ni capacitación inicial; se admiten el ascenso temporal con fecha de regreso y el ascenso con periodo de adaptación (máximo 90 días; 180 en puestos de dirección o administración o técnicos o profesionales especializados), cuyo único efecto si no se aprueba es el regreso al puesto anterior al día siguiente de comunicarlo por escrito. Riesgo explicado una vez (art. 39-D): se estructura como condición pactada desde el inicio, con salario del puesto nuevo, y no se denomina periodo de prueba.
- (15/11/2026) **Situaciones protegidas** (regreso tras el parto, incapacidad en curso, lactancia, incapacidad parcial por riesgo de trabajo): alerta crítica con doble confirmación, sin bloqueo (mismo criterio de la decisión 19). La reasignación por embarazo o lactancia, la reubicación en D4 y la incapacidad temporal para el puesto no son modificaciones: constancia MOD-5.
- (15/11/2026) **Firma:** todo sigue FIRMA_MODALIDAD; convenios, el representante; comunicados, oficio y constancias, RH designado. Negativa ante un comunicado: dos testigos y envío al correo personal, sin impedir el efecto. Convenio no firmado: el cambio no surte efectos.
- (17/11/2026, del módulo de permisos) MOD-5 por «Falta de documentos» aceptada sustituye a SUS-2 mientras dure (4.9); el módulo 5 devuelve D4_REUBICACION y D4_REUBICACION_FIN. (17/11/2026, paquete de contratación) La cláusula 1.4 del contrato ya no choca con la reducción por convenio (4.1).
- (15/11/2026) **Actualización anual** en ACTUALIZACION_ANUAL_MES, con registro digital ACT-1; con cambios, nueva designación de beneficiarios y verificación de correo o teléfono. Sustitución patronal: prioridad C.

### 4.13 Validación de pagos y Fonacot — módulos 6 y 8 (15/11/2026)

Documento de referencia: «AXIARH - Módulos 6 y 8 - Especificación para programación» (v1.0). Diseño terminado; no cerrado.
- (15/11/2026, decisión del usuario) **Validar un pago:** la casilla «pagado» no basta; sin evidencia el pago queda en «Pago declarado» con alertas. Solo el CFDI (XML cotejado: RFC del emisor, CURP del receptor, clave de percepción, importe y UUID único) o la dispersión por persona lo llevan a «Pagada»; el PDF o el UUID capturado se admiten con alerta. Es la excepción a la regla 5.0 de la casilla «documento firmado».
- (15/11/2026) Una obligación por persona, concepto y periodo, con estados equivalentes a los de la regla R-3 del kit de PTU; registro por persona o por lote con cuadre; alertas de aguinaldo hasta el límite legal y de PTU con las fechas del kit; conservación de 5 años desde el pago, nunca menos que el plazo legal; paquete probatorio exportable.
- (15/11/2026, decisión del usuario) «Pagada» se alcanza con la evidencia cotejada; D-14 se genera después con el UUID y su firma se controla aparte (D14_FIRMADO), sin revertir el estado.
- (15/11/2026, decisión del usuario) La evidencia del pago del finiquito se captura una sola vez, en el cierre de la baja del módulo 4, que la envía al módulo 6.
- (15/11/2026, decisión del usuario) **Fonacot en el finiquito:** solo se retiene la amortización del último periodo de salario pagado, nunca el saldo; sin descuento en fallecimiento (alerta del aviso de defunción al Instituto en 15 días hábiles, según el convenio). FON-2 descartada.
- (15/11/2026, decisión del usuario) La cédula mensual de Fonacot se sube como evidencia obligatoria; la importación por persona es opcional y solo coteja. Afiliación con cuatro estados y alerta a empresas nuevas como política del sistema (la Ley no fija plazo); la ficha de afiliación sustituye a la «constancia de afiliación».
- (15/11/2026, decisión del usuario) FON-1 (aviso a la persona con crédito que causa baja), con firma autógrafa de recibido; si no se presenta, envío al correo personal con constancia en bitácora.
- (17/11/2026, decisión del usuario, paquete de contratación) FONACOT_DESCUENTO_MONTO del alta es un valor esperado para la prenómina del usuario; la cédula mensual es la evidencia y el módulo 8 sigue sin calcular retenciones.

---

## 5. Reglas del formulario y del sistema

### 5.0 Reglas de pantalla de todo el sistema (13 y 15/11/2026, decisiones del usuario)
- Al generar con datos obligatorios vacíos, la pantalla resalta cada campo faltante, lo lista arriba con enlace y lleva al primero.
- Tablas editables con botones visibles de guardar y quitar por renglón; aviso al salir con renglones sin guardar.
- La casilla «documento firmado» basta para avanzar; el archivo firmado es opcional y su falta solo genera alerta. (15/11/2026) Excepción: en el módulo 6 la casilla «pagado» no da por cumplido un pago (4.13).
- Un dato, una captura: lo capturado en un documento llena los demás.
- Sin candados por fecha: se puede capturar, guardar, generar, imprimir y marcar como firmado un documento con fecha futura; solo se validan los órdenes entre fechas. Guardar nunca se bloquea; las validaciones solo impiden la versión definitiva.
- Campos que dependen de una opción: la opción se pregunta primero, sin valor por omisión si la Ley no lo fija; sus campos solo aparecen cuando aplican.
- Concordancia de número: con valor 1, singular; nunca «(s)» ni «(a)».

### 5.1 Alta de la persona trabajadora
- Nombre y domicilio por campos separados.
- CURP de 18 caracteres con dígito verificador. Edad y sexo se toman de la CURP.
- RFC prellenado con la CURP; el usuario agrega la homoclave.
- Correo personal obligatorio. El correo institucional es una casilla que genera su documento de asignación.
- Sin jefe inmediato, clasificación, atributo de dirección, trabajo material, lugar de pago, forma de pago, propiedad intelectual ni campos editables del perfil de puesto: todo eso viene de la empresa o del organigrama.
- Fecha de inicio vacía y obligatoria.
- (Actualizado 26/10/2026) La periodicidad de pago no se captura en el alta: viene del perfil de puestos. Días de pago calculados.
- ~~(26/10/2026) El salario tampoco se captura en el alta: es un monto fijo por puesto.~~ (15 y 17/11/2026) Sustituido: SALARIO_PERSONA se captura en el alta con precarga del salario base del puesto (sección 2).
- (13/11/2026) PERFIL_MODALIDAD y ACTIVIDADES_PRINCIPALES se capturan en el alta, con precarga del puesto.
- (15/11/2026) Descuentos de Infonavit y Fonacot opcionales (4.1). (17/11/2026) TRAB_ESTADO_CIVIL la captura la persona y se guarda en su expediente.
- Días en casa con casillas de días de la semana; el sistema calcula el porcentaje y el módulo: T (TELETRABAJO_ACTIVO, más de 40%) o H (HIBRIDO_ACTIVO, de 1 a 40%). (26/10/2026) La casilla se rotula «¿Trabaja días en casa?».
- La pregunta REPSE solo aparece si la empresa tiene folio. Sin datos de supervisores. (26/10/2026) Con REPSE = Sí, el alta captura el lugar de trabajo (Empresa o Cliente); solo con Cliente se capturan los datos del cliente y de la asignación (los del oficio de asignación). El contrato no lleva los datos del servicio especializado por persona: la declaración lista todas las actividades registradas de la Empresa.
- (26/10/2026) El equipo asignado se captura como tabla (EQUIPO_DESCRIPCION: descripción, marca y modelo, serie o identificador, estado y, desde el 17/11/2026, valor de reposición), una fila por bien.
- Beneficiarios: hasta 4, con porcentajes que suman 100. (26/10/2026, aprobada) El documento conserva la regla de partes iguales cuando los porcentajes no suman 100, con fines informativos.
- Sin carga masiva por ahora: primero se cierra el formulario.

### 5.2 Activación de módulos

| Módulo o texto | Se activa cuando |
|---|---|
| Convenio de confidencialidad y su Anexo A | Nivel de acceso Calificado |
| Párrafo de pena convencional del convenio | CONV_PENA = Sí (configuración de la empresa) |
| Teletrabajo (módulo T) | Días en casa entre días laborables mayor a 40% (TELETRABAJO_ACTIVO = Sí) |
| Trabajo híbrido (módulo H) (26/10/2026) | Días en casa entre días laborables de 1% a 40% (HIBRIDO_ACTIVO = Sí). Excluyente con T |
| Cláusulas 6.7 y 6.8 del contrato (26/10/2026) | DIAS_EN_CASA_ACTIVO = Sí (teletrabajo o híbrido) |
| Documento de asignación de correo institucional (26/10/2026) | INTRANET = Sí; se entrega con el contrato, no en el Anexo 3 |
| Módulo R (REPSE): declaraciones, lugar de trabajo, asignación y servicio al cliente | Trabajador REPSE = Sí |
| Oficio de asignación REPSE | Trabajador REPSE = Sí **y** REPSE_LUGAR_TIPO = Cliente |
| Fila REPSE del Anexo 3 (políticas de servicio al cliente y lineamientos del cliente, variable CLIENTE_LINEAMIENTOS_ENTREGA) | Trabajador REPSE = Sí |
| Propiedad intelectual | Atributo del puesto = Sí |
| Prestaciones superiores | El puesto tiene prestaciones configuradas |
| Carta responsiva | Hay equipo asignado, DIAS_EN_CASA_ACTIVO = Sí (teletrabajo o híbrido), se asigna correo institucional o el puesto tiene sistemas asignados (PUESTO_SISTEMAS no vacío) (actualizado 26/10/2026) |
| Acuerdo de descuento | Hay descuento capturado |
| ~~Variante de comida dentro del centro~~ | (17/11/2026) Eliminada con PUEDE_SALIR; la cláusula 6.4 queda como regla legal escrita |
| Cláusula de firma electrónica en cada documento del kit | FIRMA_MODALIDAD = Electrónica |
| Juego de la Comisión Mixta de Capacitación | PLANTILLA_NUM > 50, o se usa periodo de prueba o capacitación inicial (MOD_PRUEBA) |
| Variante sindical (oficio de designación) de las comisiones de capacitación y PTU | SINDICATO = Sí |
| Módulo A, B o C del dictamen de PTU | RESULTADO, derivado de la renta gravable y de la excepción legal |

### 5.5 Baja de la persona trabajadora (27/10/2026)

| Alerta | Plazo | Fundamento |
|---|---|---|
| Baja ante el IMSS | No más de 5 días hábiles | Art. 15, fr. I LSS |
| Aviso al juzgado y a acreedores alimentarios | 5 días hábiles siguientes a la terminación | Art. 110, fr. V LFT |
| Constancia de servicios | 3 días, si se solicita | Art. 132, fr. VIII LFT |
| Baja ante Fonacot (15/11/2026) | 5 días hábiles por omisión (FONACOT_AVISO_DIAS, de FONACOT_PLAZOS) | Convenio con el Instituto, cláusula Quinta (no la Ley) |
| Aviso de defunción a Fonacot (15/11/2026) | 15 días hábiles | Convenio, cláusula Séptima |
| Baja ante Infonavit | Configurable mientras se verifica | Pendiente |
| Alta ante el IMSS desde el primer día del periodo de prueba o capacitación | Al inicio de la relación | Art. 39-C LFT |
| Vencimiento de contrato determinado | 15 días naturales antes; contador de renovaciones desde la segunda | Política |
| Secuencia de baja sin firma | Ver 4.8 | Decisión del usuario |
| Cierre de accesos | BAJA_FECHA + 1 día hábil | Política |
| Entrega del comunicado de vencimiento | VENC_AVISO_DIAS hábiles antes (por omisión 5) | Política |

(12/11/2026) Se eliminaron las alertas de aviso de rescisión por el Tribunal y de prescripción para rescindir: el aviso es un servicio aparte y el plazo solo aparece en el mensaje informativo.

Datos que faltan en el alta para la baja: TRAB_NSS (necesario para la baja, no bloquea el contrato); pensión alimenticia (PENSION_ALIMENTICIA, PENSION_AUTORIDAD, PENSION_PORCENTAJE, PENSION_EXPEDIENTE); INFONAVIT_CREDITO y FONACOT_CREDITO; BENEF_CONFIRMACION_FECHA. Variables eliminadas por el módulo 4: RENUNCIA_*, RECIBE_NOMBRE, RECIBE_CARGO, RATIFICACION, RATIFICACION_UMBRAL, RATIF_DIAS y CONV_PENA_DIARIA.

### 5.3 Alertas del periodo (no configurables)

| Modalidad | Evaluaciones | Vencimiento |
|---|---|---|
| Capacitación inicial de 3 meses | Días 30, 60 y 75 | Alertas desde 3 semanas antes, cada vez más críticas |
| Capacitación inicial de 6 meses | Mensuales | Alerta 15 días antes del vencimiento |
| Periodo de prueba | Solo evaluación final | Alertas desde 3 semanas antes, cada vez más críticas |

(10/11/2026, sustituye el candado) Los requisitos ya no bloquean: sin ellos, «Continuar sin requisitos» permite la baja con convenio y recibo y solo deja de generarse el comunicado de respaldo (4.8). Texto anterior: el documento de terminación solo se habilita con la evaluación final, la opinión de la Comisión Mixta (formato F-2) o la constancia de que se solicitó oportunamente, y, en capacitación, las constancias de la capacitación impartida. Pasado el vencimiento, queda bloqueado.

### 5.4 Validaciones legales del sistema
- La jornada no puede exceder el máximo del año de la fecha de inicio. Tabla de máximos: 48 horas en 2026, 46 en 2027, 44 en 2028, 42 en 2029 y 40 en 2030, cada cambio el 1 de enero. Falta confirmar con el DOF los máximos de las jornadas nocturna y mixta.
- ~~Si no se puede salir a comer, ese tiempo cuenta como jornada.~~ (17/11/2026, decisión del usuario) Validación eliminada con PUEDE_SALIR; la cláusula 6.4 conserva la regla legal escrita.
- En jornada continua, mínimo 30 minutos de descanso.
- Salario no menor al mínimo de la zona del centro de trabajo.
- No se puede repetir el periodo de prueba ni la capacitación inicial con la misma persona. (31/10/2026) Se amplía a lo que prohíbe el art. 39-D: simultáneo o sucesivo, más de una ocasión, puestos distintos, ascensos y nueva relación con la misma Empresa.
- (26/10/2026) Módulo H: 1 ≤ PORC_TIEMPO_DOMICILIO ≤ 40; con HIBRIDO_ORIGEN = Decisión de la Empresa no se permite HIBRIDO_APOYO_MODO = Sin apoyo (bloqueo).
- (26/10/2026) REPSE: sin folio y vigencia cargados en el perfil de la empresa el módulo R se bloquea. Con REPSE_LUGAR_TIPO = Cliente no se genera el contrato sin el oficio de asignación completo.
- (26/10/2026) Representantes obreros de las comisiones: no pueden tener clasificación Confianza en el organigrama y deben pertenecer a uno de los centros.
- (26/10/2026) PTU: alerta si la copia de la declaración no se entrega dentro de 10 días hábiles; fechas límite de consulta, objeciones, observaciones, resolución y pago calculadas desde FECHA_PRESENTACION; límite de pago según el tipo de persona de la Empresa.

---

## 6. Alcance del PMV de Axia RH (26/10/2026)

- (Actualizado 15/11/2026: la comisión mixta de capacitación pasó a Axia CYA) Módulos: kit de contratación; RIT y su comisión mixta; PTU y su procedimiento; terminación y precálculo de finiquito; modificación de condiciones de trabajo; validación de pago de PTU y aguinaldo; comisión mixta de capacitación y SIRCE; Fonacot; análisis de jornada.
- La Comisión Mixta de Capacitación, Adiestramiento y Productividad entra al PMV.
- El PMV genera todo tipo de contratos laborales, no solo por tiempo indeterminado.
- La PTU se calcula importando la nómina o capturando datos por persona (días trabajados y salario devengado).
- ~~El finiquito se precalcula bruto~~ (10/11/2026) El finiquito y la PTU se precalculan netos estimados, con ISR y cuotas obreras; los definitivos constan en el CFDI y el contador valida.
- (26/10/2026) La capacitación inicial es solo una cláusula del contrato, no un contrato autónomo.
- (26/10/2026) De capacitación, Axia RH solo cubre el SIRCE, la Comisión Mixta de Capacitación, Adiestramiento y Productividad y el DC-1. Lo demás (DNC, plan y programa, cursos) queda para Axia Capacitación.
- (26/10/2026) La constancia DC-3 no entra a Axia RH. Para terminar la capacitación inicial, el sistema exige que se cargue la evidencia de la capacitación impartida (DC-3 u otra constancia generada fuera de Axia RH).
- (26/10/2026) Fonacot: el PMV solo alerta y guarda evidencia; no calcula retenciones. (17/11/2026) FONACOT_DESCUENTO_MONTO del alta es solo un valor esperado para la prenómina; la cédula del módulo 8 es la evidencia (4.13).
- (26/10/2026) Análisis de jornada: los datos salen del archivo del reloj checador del cliente.
- (26/10/2026) Acta formal de devolución y entrega de herramientas a la salida, como documento propio del módulo de terminación.
- (26/10/2026) Los documentos que recibe el cliente no llevan «AEXIS» ni «AXIARH». El logo del cliente se ofrece en otro nivel de servicio.
- (12 y 15/11/2026) Entran al PMV las pantallas de eventos «Permisos y licencias» y «Vacaciones y aguinaldo», con conversación y especificación propias.
- (15/11/2026) Módulos 5 (modificación de condiciones) y 6 y 8 (validación de pagos y Fonacot) con diseño terminado y especificación lista; no cerrados.
- (15/11/2026, decisión del usuario) **Líneas de la familia y repositorio.** Repositorio GitHub `aexislegal-hub/axias` con carpetas por línea: Axia RH, Axia NOMs, Axia CYA (capacitación y adiestramiento) y Axia Compliance. Las variables de empresa, organigrama y alta se deciden solo en Axia RH.
- (15/11/2026, decisión del usuario) **Cada línea Axia tiene su propio proyecto y su propio Cerebro**, con la misma estructura de trabajo que Axia RH (registro, mapa, cortes y encargos). El Cerebro de Axia RH es dueño de `base-comun/` y del diccionario de variables de empresa, organigrama y alta; los Cerebros de las demás líneas le piden esas variables como encargo.
- (15/11/2026, decisión del usuario) **Axia Compliance** desarrolla: anticorrupción, ética, el documento del Comité de Integridad y Disciplina, las políticas legales (teletrabajo y trabajo híbrido, prevención de la violencia y del hostigamiento) y las políticas organizacionales a las que remite el RIT (vestimenta, TIC, vehículos, regalos y conflictos de interés, exámenes médicos y pruebas, fatiga, ergonomía, viáticos y traslados, registro de políticas). Axia RH conserva las remisiones del RIT, el registro de acuses y la alerta del transitorio quinto.
- (15/11/2026, decisión del usuario; sustituye la del 26/10) **La Comisión Mixta de Capacitación, Adiestramiento y Productividad sale de Axia RH y pasa a Axia CYA**, con sus formatos F-1 a F-5, junto con DNC, plan y programa, cursos y DC-3. Por omisión se van también el SIRCE y el DC-1, salvo que el usuario indique otra cosa. Axia RH conserva: la cláusula de prueba o capacitación inicial del contrato, la remisión del art. 41 del RIT, el comunicado de respaldo del módulo 4 (que lee F2_EMITIDA, F2_FECHA, F2_SENTIDO y F2_SOLICITUD_FECHA de Axia CYA) y la exigencia de evidencia de la capacitación impartida para terminar la capacitación inicial.
- (15/11/2026) Estado real de cierre: el único módulo cerrado por el usuario es el 4 (terminación). Los demás están en diseño terminado o en corrido en el software; sus aprobaciones siguen provisionales.
- El detalle de faltantes, dependencias y contradicciones está en «Axia RH - Mapa del PMV».

---

## 7. Pendientes

- [x] (15/11/2026) Cerrado: situaciones protegidas en la baja, alerta crítica con doble confirmación, sin bloqueo (4.8).
- [ ] (15/11/2026) Decidir si el cuadro general de antigüedades (art. 158) entra al PMV (el módulo de vacaciones lo deja fuera por ahora).
- [ ] (17/11/2026) Módulo 5: verificar el plazo del aviso modificatorio de salario ante el IMSS, criterios sobre consentimiento tácito de modificaciones, el ascenso con periodo de adaptación frente al art. 39-D y la ratificación de convenios modificatorios (art. 33); redactar MOD-6 (prioridad C).
- [ ] (17/11/2026) Módulos 6 y 8: cargar el calendario oficial de cédulas de Fonacot y confirmar la fecha límite de entero (fuentes en conflicto); confirmar FONACOT_PLAZOS con el convenio de cada cliente; verificar el catálogo de percepciones del SAT, el art. 30 del CFF y el art. 15, fr. II LSS.
- [ ] (17/11/2026) Vacaciones: verificar la preferencia por antigüedad cuando haya contrato colectivo.
- [ ] (15/11/2026) Redactar el documento del Comité de Integridad y Disciplina (Axia Compliance).
- [ ] (15/11/2026) Vacaciones: verificar el Convenio 52 OIT (texto oficial y ámbito), las tesis citadas, el fraccionamiento del bloque continuo (art. 78), las prestaciones extralegales en el salario ordinario y la continuidad en reingresos.
- [ ] (15/11/2026) PTU: verificar el art. 127, fr. VIII (excedente del tope) y el art. 122 LFT.
- [ ] (12/11/2026) Módulo 4: cargar parámetros 2027 (tarifa, subsidio y salarios mínimos en diciembre; UMA en enero); plazos de baja ante Fonacot e Infonavit; revisar la LISR aprobada del paquete 2027.

- [ ] Confirmar si la cláusula base de confidencialidad incluye el pacto de titularidad de obras (art. 84 LFDA).
- [ ] Confirmar con el texto del DOF los máximos de las jornadas nocturna y mixta en la reducción gradual.
- [ ] Definir con cada cliente el apoyo para gastos de teletrabajo y los medios de contacto.
- [ ] Decidir si las prestaciones superiores se configuran por empresa o por puesto o nivel.
- [x] (17/11/2026) Cerrado: adenda de confidencialidad (kit 3.8), asignación de correo institucional (kit 3.5) y constancia de recibo del RIT (FR-1) redactadas.
- [x] (18/11/2026) Cerrado: firma del acta de devolución (4.11).
- [ ] (18/11/2026) Paquete: confirmar las opciones de INFONAVIT_DESCUENTO_TIPO contra el aviso de retención vigente y si el monto del Fonacot se captura mensual o por periodo de pago; verificar con la LFPDPPP 2025 si las constancias de detención y la Declaración Especial de Ausencia son datos sensibles.
- [ ] Integrar al contrato maestro las cláusulas ajustadas por el layout (notificaciones, jornada, lugar de trabajo, REPSE, teletrabajo, prestaciones, perfil de puesto). La integración de jornada, teletrabajo y REPSE ya se hizo el 26/10/2026; falta la revisión final.
- [x] (26/10/2026) Cerrado: variantes B, C y D incorporadas; paquete de contratación cerrado y diccionario de variables generado.
- [ ] (31/10/2026) Paquete de contratación: dar de alta en el formulario las 12 variables sin estructura (CANAL_AVISO_AUSENCIA, MEDIO_ENTREGA_RECIBOS, JORNADA_ID, CLIENTE_ACTIVIDAD_REPSE, REPSE_ACT_DESCRIPCION, REPSE_ACT_NUMERO, MODULO_REVISION_FECHA, MODULO_REVISION_MESES, TELE_AUTORIZACION_FECHA, TELE_AUTORIZACION_ORGANO, TELE_SOLICITUD_FECHA); verificar la LFPDPPP 2025; quitar la nota «por verificar» del módulo R; corregir formato de encabezados 3.1 y 3.3; diseñar el paquete de prestaciones extralegales.
- [ ] (31/10/2026) Unificar nombres de variables entre el paquete de contratación y el módulo 4: el contrato usa CAUSA_TEMPORALIDAD y FECHA_TERMINO; el módulo 4 pide TEMPORALIDAD_CAUSA, CONTRATO_FIN y OBRA_DESCRIPCION. Rigen los del contrato cerrado; el módulo 4 debe adoptarlos.
- [ ] (27/10/2026) Módulo 4: confirmar en el PDF oficial de la LFT los arts. 162, 485, 486, 501, 503, 517, 518 y 892 a 899; verificar plazos de baja ante Fonacot e Infonavit y si procede retener del finiquito; buscar criterios sobre prima de antigüedad en mutuo consentimiento, en relaciones determinadas y al vencer el periodo de prueba; revisar los transitorios de la reforma DOF 01-05-2026 (tiempo extra); confirmar el tratamiento fiscal de la gratificación; seguir la contradicción 165/2025; verificar el fundamento de la firma autógrafa obligatoria del recibo.
- [ ] (31/10/2026) Anexo T3 (teletrabajo): precisar que la inclusión en el RIT aplica si no hay contrato colectivo (art. 330-D).
- [x] (12/11/2026) Cerrado: el RIT incluye el medio alterno del registro de jornada y las aclaraciones (art. 13) y la opinión de la Comisión Mixta antes de terminar el periodo (art. 41); depósito de los Anexos B, C y D cuando cambian (art. 88); resultado confirmado de las pruebas (art. 60); días computables para PTU (art. 31).
- [ ] (27/10/2026) Módulo 4: redactar comunicado de suspensión por fin de temporada, terminación por incapacidad (art. 54) y hoja interna del escenario de negociación.
- [x] (31/10/2026) Cerrado: traslado entre clientes REPSE resuelto en el art. 9 del RIT (tiempo de trabajo; registro de llegadas y salidas; gastos a cargo de la Empresa).
- [ ] (26/10/2026) Confirmar en la fuente oficial del registro REPSE cómo se denomina y numera cada actividad especializada («número de la actividad», REPSE_ACT_NUMERO) y ajustar el formato de la declaración.
- [x] (26/10/2026) Cerrado: verificados en el texto vigente de la LFT los artículos 39-A a 39-F. El contrato cita el art. 39-D (prueba improrrogable, no simultánea ni sucesiva) (hoy sin cita: su contenido está en la 3.4) y el 39-F (labores discontinuas, de temporada o periódicas son por tiempo indeterminado) en la nota de la variante D.
- [x] (26/10/2026) Cerrado: se creó el módulo H (trabajo híbrido) en la biblioteca (ver 4.1).
- [ ] (26/10/2026) Contratos anteriores: se descartó del contrato maestro la delegación en la Comisión Mixta de decisiones sobre terminación, puesto, ascensos y lugar de trabajo, la terminación «a juicio del patrón» en obra determinada, la exclusión de domicilios de terceros como centros de trabajo y el pacto de beneficios colectivos no salariales. Quedan para otras conversaciones: horas extras (RIT), comisiones mixtas en el RIT, propinas, servicio al cliente de hotelería y protección de menores (módulos por giro), y el código de ética, el manual de inducción y la política de comunicación (políticas aparte, que se acusan en el Anexo 3).
- [x] (26/10/2026) Cerrado: cláusula 1.2 aplicada (labores conexas como parte de las actividades del puesto). Verificado en el texto vigente que el art. 56 Bis dice que las labores conexas «podrán recibir la compensación salarial correspondiente»; por eso la cláusula ya no excluye la compensación, aunque tampoco la reconoce. Decisión mantenida.
- [x] (26/10/2026) Cerrado: se quitó del contrato la regla que obligaba al aviso de privacidad (Anexo 4) a mencionar la ubicación; el bloque de ubicación del Anexo 3 se ajustó a la regla de biométricos.
- [ ] (26/10/2026) Política de tecnologías de la información: va después, con las demás políticas. Mientras no exista, la revisión del correo institucional que prevén la carta responsiva y el aviso de privacidad es impugnable.
- [ ] (26/10/2026) Módulo H: confirmar en el DOF la vigencia y el alcance de la NOM-037 respecto del trabajo híbrido; confirmar si el art. 330-A mide el porcentaje por días o por horas de la jornada (hoy el sistema calcula por días); confirmar el tratamiento salarial y fiscal del apoyo de monto fijo; confirmar el alcance de la cláusula 5.2 del contrato (todo lugar de prestación es centro de trabajo) respecto del domicilio de la Persona Trabajadora.
- [ ] (26/10/2026) RIT: contrastar la frecuencia de descansos por bipedestación con las disposiciones de la STPS; ajustar los arts. 13 y 22 cuando la STPS publique las disposiciones del registro electrónico de jornada (vigencia: 1 de enero de 2027); confirmar el plazo de 2 años de conservación del expediente clínico (art. 61) frente a las normas sanitarias; hacer condicional el transitorio segundo (solo si existe un RIT anterior).
- [ ] (12/11/2026) RIT: retroalimentación del usuario al correr la especificación v1.1; confirmar las cinco propuestas de programación (11.1); revisión de los formatos; verificar las fracciones del art. 47 de la tabla de correspondencia contra el texto oficial, los requisitos vigentes del depósito ante el CFCRL, los límites legales de descuento para la tabla del sistema y criterios sobre la fr. XV aplicada al ausentismo sistemático (conducta 60). Por cliente: integración del Comité, labores y áreas prohibidas, puestos críticos y laboratorio para las pruebas.
- [ ] (12/11/2026) Diccionario único: distinguir DIAS_EN_CASA_EMPRESA (empresa, RIT; desde el 18/11/2026 es pregunta de la empresa, sin valor por omisión) de DIAS_EN_CASA_ACTIVO (alta, contrato); PERSONA_JEFATURA es la jefatura inmediata y DIRECTOR_AREA la dirección del área, ambas por puesto (se elimina JEFE_INMEDIATO); FIRMANTES_EMPRESA va en la configuración de la empresa; CENTRO_TRABAJO (módulo de permisos) equivale a PERSONA_CENTRO (RIT) y debe quedar un solo nombre.
- [ ] (26/10/2026) Comisión de capacitación: verificar en la fuente oficial los arts. 39-A, 39-B, 153-D y 183 LFT; confirmar que no haya un acuerdo de la STPS posterior a abril de 2025 que modifique los formatos DC-1, DC-2 o DC-3; buscar criterios judiciales sobre procedimientos disciplinarios internos autoimpuestos; fijar valores por defecto de PERIODO_CARGO, PERIODICIDAD, ANOS_CONSERVACION, DIAS_OBJECION y DIAS_RESOLUCION.
- [ ] (02/11/2026) PTU: verificar el tratamiento del excedente por el tope individual (art. 127, fr. VIII) y el art. 122 LFT; agregar AUTORIDAD_INSPECCION al alta de la empresa. Recibo individual y control de PTU no cobrada: redactados.
- [ ] (26/10/2026) Kit: comprobar que el aviso cumple el contenido mínimo del art. 15 de la LFPDPPP 2025 (el reglamento nuevo no se ha publicado); revisar el aviso para candidatos con los mismos criterios; unificar el Anexo 3 del contrato con el kit.
