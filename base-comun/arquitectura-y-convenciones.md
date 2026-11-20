# Base común de la familia Axia

Generado automáticamente a partir de `axia-rh/registro-de-decisiones.md` (versión del 20 de noviembre de 2026). **No se edita a mano**: cualquier cambio se hace en el registro de Axia RH y Cerebro vuelve a generar este archivo.

Contiene la arquitectura del sistema (niveles de captura y atributos de puesto) y las convenciones de redacción que comparten todos los productos Axia. Un proyecto distinto de Axia RH que necesite una variable nueva de empresa, organigrama o alta la pide como encargo a Cerebro.

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
