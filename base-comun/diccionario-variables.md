# AXIA RH — Diccionario único de variables

Versión 1.0 · 21/11/2026 · Responsable: Cerebro de Axia RH (dueño de las variables de empresa, organigrama y alta). Aprobaciones provisionales hasta la revisión final del usuario.

**Fuentes:** «Paquete de contratación — Variables y dependencias» (versión final, 21/11/2026, 205 variables; contrato rev. 507, biblioteca rev. 91), registro de decisiones (21/11/2026) y especificaciones vigentes: RIT v1.7, kit de PTU v1.2, módulo 4 v1.5, módulo 5 v1.1, módulos 6 y 8 v1.1, módulo 9 v1.1, permisos y licencias v1.9, vacaciones y aguinaldo v1.4 y firma electrónica v1.5.

---

## 0. Cómo se usa

- **Alcance.** Este diccionario fija el nombre, el nivel, el tipo y la validación de cada dato que se captura en la **configuración de la empresa** (con sus catálogos), en el **organigrama** (con el catálogo de jornadas) y en el **alta** (con el expediente de la persona), y de las **tablas globales**. Las variables de evento y las calculadas de un solo módulo viven en la especificación de ese módulo; aquí solo se listan las que leen varios módulos (sección 6).
- **Un dato, un campo.** El sistema guarda un solo campo por dato, con el **nombre canónico** de este diccionario. Si una especificación o una plantilla usa otro nombre, la sección 7 da la equivalencia y el motor de plantillas lo resuelve al canónico. No hace falta renombrar las especificaciones ya entregadas.
- **Texto que activa.** El detalle de en qué cláusula o documento se imprime cada variable del paquete de contratación está en su archivo de variables (columnas «Documento y apartado» y «Activa»). Aquí solo se indica qué módulos la usan.
- **Marcas.** ⚑ nivel inferido de una regla, por confirmar. ◆ propuesta de Cerebro que espera decisión del usuario (sección 8). Las variables nuevas de este diccionario se listan en la sección 10, «Impacto en el sistema».
- **Claves de módulo.** PAQ paquete de contratación (contrato, biblioteca y kit) · RIT · PTU (módulo 3) · M4 terminación · M5 modificación · M6 validación de pagos · M8 Fonacot · M9 análisis de jornada · PER permisos y licencias · VAC vacaciones y aguinaldo · FIR firma electrónica · CMR acta de la CMRIT · NOM Axia NOMs · CYA Axia CYA.

---

## 1. Configuración de la empresa (nivel 1)

### 1.1 Datos generales y representante

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| PATRON_TIPO_PERSONA | Moral · Física | Obligatoria; con Física se muestran nacionalidad, edad, sexo, estado civil y CURP | PAQ, PTU (como EMPRESA_TIPO_PERSONA), M6 |
| PATRON_RAZON_SOCIAL | Texto | Obligatoria | Todos |
| PATRON_NOMBRE_COMERCIAL ◆ | Texto | Opcional | RIT (como NOMBRE_COMERCIAL) |
| PATRON_RFC | Texto | 12 caracteres (moral) o 13 (física) | PAQ, RIT, PTU, M4, M6 |
| PATRON_DOMICILIO | Texto por campos | Obligatoria; domicilio fiscal | PAQ, RIT, PER, M4 |
| PATRON_ACTIVIDAD | Texto | Obligatoria | PAQ, RIT |
| PATRON_REG_PATRONAL | Texto | ◆ P1: pasa a derivada del centro de la persona | PAQ |
| PATRON_NACIONALIDAD, PATRON_EDAD, PATRON_SEXO, PATRON_ESTADO_CIVIL, PATRON_CURP | Texto / número | Solo persona física; mayor de edad; formato CURP | PAQ |
| REP_NOMBRE | Texto | Obligatoria; puede haber más de un representante | Todos |
| REP_CARACTER | Texto | Obligatoria | PAQ, PER, M4, M5 |
| REP_EFIRMA_RFC, REP_EFIRMA_VIGENCIA | Texto / fecha | Se leen del certificado (.cer) del representante; alerta 30 días antes del vencimiento | FIR |
| COMPETENCIA | Federal · Local | Obligatoria; según la actividad de la Empresa. ◆ P2: única fuente del ámbito federal o local | PAQ, PTU, PER |
| AUTORIDAD_INSPECCION | Texto | Confirmada el 21/11/2026; ◆ P2: solo el nombre de la autoridad, prellenado según COMPETENCIA | PTU (D-03), PER (INC-1) |
| RH_RESPONSABLE_NOMBRE | Texto | — | RIT (FD-1, FR-2) |
| RESCISION_RESPONSABLE | Puesto | No se imprime | RIT |

### 1.2 REPSE

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| REPSE_FOLIO | Texto | Obligatoria si la Empresa presta servicios especializados | PAQ, RIT, M5 |
| REPSE_VIGENCIA | Fecha | Alertas a 90, 60 y 30 días; bloqueo del módulo R al vencer | PAQ |
| REPSE_ACTIVIDADES (REPSE_ACT_NUMERO, REPSE_ACT_DESCRIPCION) | Lista | Cada actividad con su número y descripción del registro | PAQ |
| ASIGNACION_AVISO_DIAS | Entero | Solo si el catálogo de clientes tiene instalaciones | PAQ, M5 |
| REPSE_EMPRESA | Sí/No calculada | Sí con REPSE_FOLIO y REPSE_VIGENCIA vigentes. ◆ P7 | RIT (art. 9), M9 |
| REPSE_APLICA ⚑ | Sí/No | ◆ P7: el paquete la ubica en la empresa; el registro 5.1 la pregunta en el alta | PAQ |

### 1.3 Registro de jornada y firma electrónica

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| SISTEMA_REGISTRO_NOMBRE ⚑ | Texto | Obligatoria; sin designación no se genera el contrato | PAQ |
| SISTEMA_REGISTRO_TIPO ⚑ | Aplicación móvil · Dispositivo · Plataforma en línea | Obligatoria | PAQ |
| REGISTRO_GEOLOC | Sí/No | La preestablece la Empresa; la ubicación no admite negativa | PAQ, M9 |
| REGISTRO_BIOMETRICO | Sí/No | Con Sí exige SISTEMA_REGISTRO_ALTERNO; la casilla del aviso se imprime siempre (decisión del 21/11/2026) | PAQ, M9 |
| SISTEMA_REGISTRO_ALTERNO ⚑ | Texto | Obligatoria con REGISTRO_BIOMETRICO = Sí; solo PIN o tarjeta | PAQ, M9 |
| PLATAFORMA_FIRMA ⚑ | Texto | Obligatoria si algún alta usa firma electrónica | PAQ, FIR |
| PORTAL_DESCARGA ⚑ | Texto | ◆ P8: en la empresa, prellenado con la intranet | PAQ, FIR |
| FES_CANAL_OTP | Correo · Correo y SMS | Por omisión Correo y SMS | PAQ, FIR |
| NOM151_SERVICIO | Sí/No | Por omisión No | PAQ, FIR |
| IDV_SERVICIO | Sí/No | Por omisión No; se cobra aparte | PAQ, FIR |
| FIRMA_ENLACE_DIAS | Entero | 5; de 1 a 30 | FIR |
| FIRMANTES_EMPRESA | Tabla | Persona, puesto (solo Confianza), correo institucional, celular, inicio, fin, folio de designación | FIR, PAQ, PER, M5, VAC, M8 |
| FIRMA_EMPRESA_DOC | Por tipo de documento y momento | Representante · RH designado · Sin firma de la Empresa; valores fijos de FIR, sección 11 | FIR, PAQ |
| DATOS_SENSIBLES_ACCESO | Lista de usuarios | Al menos uno; lista única de toda la plataforma para datos sensibles (registro 4.9) | PER, FIR, M8, expediente clínico |

### 1.4 Comunicaciones, intranet y datos personales

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| INTRANET_NOMBRE ⚑ | Texto | Obligatoria si algún alta tiene INTRANET = Sí | PAQ |
| INTRANET_ACUSE_MEDIO ⚑ | Texto | Debe registrar usuario, fecha y hora | PAQ |
| CANAL_AVISO_AUSENCIA ⚑ | Texto | Prellenado con la intranet | PAQ |
| MEDIO_ENTREGA_RECIBOS ⚑ | Texto | Prellenado con la intranet | PAQ |
| AVISO_CORREO_DATOS | Correo | Obligatoria | PAQ |
| AVISO_URL | Texto | Sin exigir http ni https; obligatoria si publica vacantes en línea | PAQ |
| CAND_PLAZO_CONSERVACION, CAND_PLAZO_BOLSA | Texto (plazo) | Obligatorias | PAQ |
| CORREO_AUDITORIA | Sí/No | Por omisión No | PAQ |
| CORREO_RETENCION_MESES ⚑ | Entero | 24; obligatoria con CORREO_AUDITORIA = Sí | PAQ |

### 1.5 Contratación, confidencialidad y perfiles

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| PERFIL_AVISO_DIAS | Entero | 15; > 0 | PAQ, M5 |
| PERFIL_ORIGEN | Empresa · Sistema | Solo con PERFIL_MODALIDAD = Perfil de puesto; con Sistema exige aprobación | PAQ |
| PI_ACTIVAR | Sí/No | ◆ P5 (nivel); validar con especialista | PAQ |
| PI_CATALOGO | Tabla | Opcional; alimenta PUESTO_PI | PAQ |
| CONV_PENA | Sí/No | No | PAQ |
| CONV_PENA_MONTO, CONV_PENA_DIAS | Moneda / entero | > 0; obligatorias con CONV_PENA = Sí | PAQ |
| CONF_CLAUSULA_BASE | Texto del sistema | No editable | PAQ |
| MODULO_REVISION_MESES | Entero | — | PAQ |
| ACTUALIZACION_ANUAL_MES | Mes | Obligatoria | M5 |
| MOD_PRUEBA ◆ | Sí/No | ◆ P6: hoy no la define ningún documento | RIT (art. 41), comisión de capacitación (CYA) |

### 1.6 Teletrabajo y trabajo híbrido

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| DIAS_EN_CASA_EMPRESA | Sí/No | Sin valor por omisión; alerta si un alta tiene DIAS_EN_CASA_ACTIVO = Sí y aquí dice No | RIT |
| TELE_AVISO_DIAS ⚑ | Entero | — | PAQ, M5 |
| TELE_CANALES ⚑ | Texto | — | PAQ |
| HIBRIDO_APOYO_MODO | Sin apoyo · Monto fijo · Reembolso | Con HIBRIDO_ORIGEN = Decisión de la Empresa no admite Sin apoyo | PAQ, M5, M9 |
| HIBRIDO_APOYO_MONTO | Moneda | Solo con Monto fijo | PAQ, M5, M9 |
| TELE_COMPENSACION_MODO, TELE_COMPENSACION_MONTO, TELE_POLITICA_COMPENSACION, TELE_REVISION_MESES, TELE_SUPERVISION, TELE_VIGENCIA ⚑ | Varios | Módulo T | PAQ |

### 1.7 Condiciones generales y RIT

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| DIA_PAGO_SEMANAL | Día | Obligatorio si algún puesto paga semanal | RIT, PAQ (DIA_PAGO), PER |
| DIAS_PAGO_QUINCENAL | Opción | Obligatorio si algún puesto paga quincenal | RIT, PAQ (DIA_PAGO), PER |
| REGLA_AJUSTE_JORNADA | Opción | — | RIT |
| DIAS_AVISO_AJUSTE_HORARIO | Entero | 15 | RIT, M9 |
| DIAS_ACLARACION_REGISTRO | Entero | 5 | RIT, M9 |
| TOLERANCIA_MIN | Entero | 10 | RIT, M9 |
| RETARDOS_FALTA_GRAVE | Entero | 4 | RIT, M9 |
| DIAS_ACLARACION_NOMINA / DIAS_RESPUESTA_NOMINA | Entero | 10 / 5 | RIT, M9 |
| PAGO_DIAS_ESPERA | Sí/No | No | RIT, PER, VAC, M9 |
| PRIMA_VACACIONAL_PCT | Porcentaje | 25; ≥ 25 | RIT, VAC, M4 |
| MOMENTO_PAGO_PRIMA | Opción | — | RIT, VAC |
| LACTARIO | Sí/No | Sin valor por omisión; se pregunta antes que la ubicación | RIT, PER |
| UBICACION_LACTARIO / LACTARIO_EQUIPAMIENTO | Texto | Solo con LACTARIO = Sí | RIT, PER |
| VEHICULOS_ASIGNADOS | Sí/No | No | RIT |
| ANIOS_CONSERVACION_DISCIPLINARIOS | Entero | 5 | RIT |
| MESES_REINCIDENCIA / MESES_CANCELACION_ANTECEDENTES | Entero | 12 / 12 (≥ reincidencia) | RIT |
| MINUTOS_LIMPIEZA, HORARIO_LIMPIEZA_GENERAL, PERIODICIDAD_MANTENIMIENTO, MINUTOS_DESCANSO_BIPEDESTACION, HORAS_ENTRE_DESCANSOS_BIPEDESTACION, SIMULACROS_AL_ANIO, UBICACION_PROCEDIMIENTO_PRIMEROS_AUXILIOS | Varios | Valores de RIT 8.2 | RIT |
| CANAL_DENUNCIAS / DIAS_ACUSE_DENUNCIA | Texto / entero | Opcional / 5 | RIT |
| RIT_ANTERIOR / FECHA_DEPOSITO_RIT_ANTERIOR | Sí/No / fecha | No | RIT |
| DIAS_EMISION_POLITICAS | Entero | 60 | RIT |
| COMITE_INTEGRANTES | Catálogo interno | Lo alimenta el documento del Comité (Axia Compliance) | RIT |

### 1.8 Comisiones mixtas (criterio común)

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| SINDICATO | Sí/No | Obligatoria | RIT, CMR, PTU |
| SINDICATO_NOMBRE | Texto | Con SINDICATO = Sí; PTU lo precarga en el evento | CMR, PTU |
| DESIGNACION_OBRERA | Designación · Elección | Designación; solo con SINDICATO = No | CMR, PTU, CYA |
| NUM_REPRESENTANTES_POR_PARTE | Entero | ≥ 1 | CMR, PTU, CYA |
| REPRESENTANTES_SUPLENTES | Sí/No | Sí | CMR, PTU, CYA |
| CMRIT_PLAZO_RIT_DIAS, DIAS_DIFUSION_RIT, CMRIT_DIAS_CONVOCATORIA, CMRIT_DIAS_VACANTE, CMRIT_ANIOS_CONSERVACION, CMRIT_DURACION_CARGO_ANIOS | Entero | 60 / 10 / 5 / 30 / 5 / 2 | CMR |

CONFORMIDAD_FIRMAS no es dato de empresa: se decide en cada acta (dato del evento en CMR y en PTU).

### 1.9 PTU, vacaciones, aguinaldo y permisos

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| PTU_ISR_METODO | Art. 174 RLISR · Art. 96 LISR | Art. 174 | PTU |
| PTU_AVISO_RECORDATORIO_DIAS | Entero | 60 | PTU, M6 |
| TRABAJO_HOGAR | Sí/No | No | PTU |
| VAC_PROGRAMACION_MODO | Calendario anual · Periodos de solicitud por antigüedad · A solicitud | Sin valor por omisión; un solo campo para RIT y VAC | RIT, VAC |
| MES_CALENDARIO_VACACIONES | Mes | Solo con Calendario anual | RIT, VAC |
| DIAS_ANTICIPACION_VACACIONES | Entero | 15 | RIT, VAC |
| VAC_PREFERENCIAS_DIAS, VAC_ANIO_PROGRAMACION, VAC_PERIODOS_SOLICITUD, VAC_BLOQUEOS, VAC_CUPOS, VAC_NOTIFICACION_CANALES, VAC_CONFIRMACION_DIAS, REINGRESO_ALERTA_DIAS | Varios | VAC, sección 14.2 | VAC |
| AGUINALDO_DIAS | Entero | ≥ 15; 15 | VAC, M4 |
| AGUINALDO_FECHA_PAGO | Día y mes | ≤ 19 de diciembre; 15 de diciembre | VAC, M6 |
| PERMISOS_EMPRESA (con DIAS_PERMISO_MATRIMONIO, DIAS_PERMISO_HOSPITALIZACION, DIAS_ADAPTACION_GUARDERIA, HORAS_CITA_MEDICA, CITAS_MEDICAS_AL_MES, DIAS_ASUNTOS_PERSONALES, PERMISOS_HORAS_AL_MES, GOCE_PERMISO_HOSPITALIZACION, DIAS_FALLECIMIENTO_GRADO_1/2/3, KM_FUNERAL_FORANEO, DIAS_FUNERAL_FORANEO) | Catálogo editable | Precargado con las filas del maestro; columna «Autorizan» | RIT, PER |
| CADENA_AUTORIZACION | Pasos ordenados | RH obligatorio; por omisión Jefatura, RH, Dirección | PER, VAC |
| AUTORIZACION_PLAZO_DIAS | Entero | 1 a 5; 1 | PER, VAC |
| EVIDENCIA_VENCIDA_EFECTO | Sin goce · Alerta | Alerta mientras el RIT no esté depositado | PER |
| LIC3_MAX_DIAS, REINCORPORACION_UMBRAL_DIAS | Entero | 90 / 30 | PER |
| ALERTA_PATRON_MESES, ALERTA_PATRON_FALTAS, ALERTA_PATRON_RECURRENCIA, ALERTA_PATRON_ADYACENCIA_PCT | Entero / porcentaje | 6 / 6 / 4 / 50 | PER |

### 1.10 Terminación, pagos y Fonacot

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| ALERTA_BAJA_INTERVALO | Entero (días hábiles) | 5 | M4, M6, M8 |
| VENC_AVISO_DIAS | Entero | 5 | M4 |
| FONACOT_AVISO_DIAS | Entero (días hábiles) | 5, de FONACOT_PLAZOS | M4, M8 |
| INFONAVIT_AVISO_DIAS | Entero | Pendiente de verificación legal | M4 |
| UMBRAL_DESVIACION_PCT / UMBRALES_CONCEPTO | Porcentaje / tabla | 0 / opcional | M4 |
| BENEF_UMBRAL | Moneda | — | M4 |
| PAGO_TOLERANCIA | Moneda | 1.00 | M6, PTU |
| PAGO_EVIDENCIA_DIAS | Entero | 5 | M6, PTU |
| PAGO_ALERTAS_AGUINALDO / PAGO_ALERTAS_PTU | Lista de días | 10 y 3 hábiles / 15 y 5 hábiles | M6 |
| PAGO_CONSERVACION_ANIOS | Entero | 5; nunca menos que el art. 804 | M6 |
| FONACOT_AFILIACION_ESTADO | Afiliada · En trámite · No procedente · No afiliada | Sin valor por omisión | M8 |
| FONACOT_NUM_CLIENTE, FONACOT_AFILIACION_FECHA, FONACOT_CONVENIO_ARCHIVO, FONACOT_CONVENIO_VERSION, FONACOT_RESPONSABLE, FONACOT_SOLICITUD_FECHA, FONACOT_NO_PROCEDENTE_MOTIVO | Varios | Según estado (M8, 18.2) | M8 |
| FONACOT_AFILIACION_ALERTA_DIAS / FONACOT_REINTENTO_MESES | Entero | 30 / 12 | M8 |
| FONACOT_AVISO_PERSONA | Sí/No | Sí | M8, M4 |

### 1.11 Análisis de jornada

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| PRENOMINA_MODO | Conectado · Solo archivo | Sin valor por omisión; solo clientes de Axia RH | M9 |
| CHECADOR_MAPEO | Plantilla por dispositivo | Obligatoria para importar | M9 |
| CHECADOR_DUPLICADO_MIN / CHECADOR_VENTANA_HORAS | Minutos / horas | 2 / 4 | M9 |
| CHECADOR_REGISTRA_COMIDA | Sí/No (o por centro) | Sin valor por omisión | M9 |
| FALLA_CHECADOR_PCT | Porcentaje | 50 | M9 |
| SEMANA_INICIO | Día | Sin valor por omisión | M9 |
| PRIMA_DOMINICAL_PCT | Porcentaje | 25; ≥ 25 | M9 |
| CONCEPTO_CLAVE_NOMINA | Tabla: concepto, clave interna, clave SAT | Clave SAT de PAGO_CLAVES_SAT | M9, M6 |
| REGISTRO_CONSERVACION_ANIOS | Entero | 1; ≥ 1 | M9 |

---

## 2. Catálogos de la empresa

### 2.1 Catálogo único de centros de trabajo

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| CENTRO_NOMBRE | Texto | Obligatoria; único | Todos (sustituye a CENTRO_TRABAJO_NOMBRE) |
| CENTRO_DOMICILIO | Calle, número, colonia, código postal, municipio | Obligatoria | PAQ (CT_DOMICILIO), RIT, PTU, M4, M5 |
| CENTRO_ESTADO | Entidad federativa | Obligatoria | RIT, PTU |
| CENTRO_REGISTRO_PATRONAL | Texto | Obligatoria. ◆ P1: fuente única del registro patronal | RIT, PTU, PAQ |
| CENTRO_ZONA_SM ◆ | General · Zona Libre de la Frontera Norte | ◆ P3: sin valor por omisión | Validación de salario mínimo (PAQ, M5), SALARIO_TOPADO (M4) |
| CENTRO_ZONA_HORARIA | Lista | Obligatoria | M9, FIR |
| CENTRO_FONACOT | Sí · No · No aplica | Sin valor por omisión | M8 |
| LUGARES_PUBLICACION | Texto | Por centro; se precarga en los documentos de las comisiones | PTU, CMR |

Derivadas del catálogo: NUM_CENTROS_TRABAJO, CENTRO_MUNICIPIO_ESTADO (municipio y estado de CENTRO_DOMICILIO y CENTRO_ESTADO).

### 2.2 Catálogo de jornadas (se liga a cada puesto con JORNADA_ID)

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| JORNADA_ID | Referencia | Liga el puesto con el turno; no se captura en el alta | PAQ, M5, M9 |
| Nombre y centro del turno | Texto / centro | Todo turno pertenece a un centro del catálogo | RIT, M9 |
| JORNADA_TIPO | Diurna · Nocturna · Mixta | Calculada con los horarios; nunca «Rotativa» | PAQ, RIT, M9 |
| DIAS_LABORADOS | Selección de días | Solo con descanso fijo | PAQ, RIT, M9 |
| HORARIO (entrada y salida por día) | Horas | No se edita en el alta | PAQ, RIT, M9 |
| DESCANSO_MINUTOS | Entero | ≥ 30 en jornada continua | PAQ, RIT, M9 |
| DESCANSO_SEMANAL | Fijo · Rotativo | — | PAQ, RIT, M9 |
| DESCANSO_DIAS | Selección de días | Obligatoria con Fijo | PAQ, RIT |
| DIAS_TRABAJO_SEMANA | Entero 1 a 6 | Solo con Rotativo; 6 | PAQ, RIT, M9 |
| DESCANSO_AVISO / DIAS_ANTICIPACION | Ninguna · Semana · Mes / entero | Solo con Rotativo; DIAS_ANTICIPACION es la anticipación del aviso del descanso rotativo (no confundir con DIAS_ANTICIPACION_VACACIONES) | PAQ |
| HORAS_SEMANA | Calculada | ≤ JORNADA_MAXIMA del año; topes diarios del art. 61 como máximos | PAQ, RIT, M9 |
| JORNADA_VERSION | Identificador | Versión del turno (M5) | M5, M9, VAC |

### 2.3 Catálogo de clientes REPSE

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| CLIENTE_RAZON_SOCIAL | Texto | Obligatoria | PAQ, M5 |
| CLIENTE_RFC | Texto | Formato RFC | PAQ |
| CLIENTE_INSTALACION_DOMICILIO | Texto | Por instalación | PAQ, M4, M5 |
| SERVICIO_CONTRATO_FECHA | Texto | Fecha y número del contrato de servicios | PAQ |
| CLIENTE_ACTIVIDAD_REPSE | Texto | Actividad registrada que se presta | PAQ |
| CLIENTE_DECLARACION_FECHA | Fecha | — | PAQ |

---

## 3. Organigrama (nivel 2: atributos del puesto)

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| PUESTO | Texto | Del catálogo; igual en carátula, perfil y nómina | Todos |
| AREA | Texto | — | PAQ, PER, M5 |
| CLASIFICACION | Base · Confianza | Confianza exige FUNCIONES_CONFIANZA | PAQ, RIT, PTU, CMR, FIR |
| FUNCIONES_CONFIANZA | Texto largo | Obligatoria con Confianza | PAQ |
| PUESTO_DIRECCION_TECNICO | Sí/No | Lo captura consultoría; independiente de la clasificación | PAQ, M5 |
| TRABAJO_MATERIAL | Sí/No | Con Sí, periodicidad solo semanal | PAQ |
| PERIODICIDAD | Semanal · Quincenal | ◆ P9: atributo del puesto (registro, sección 2), no derivada | PAQ, RIT, PER, M9 |
| PUESTO_SALARIO_BASE ◆ | Moneda | ≥ mínimo de la zona; precarga SALARIO_PERSONA en el alta | PAQ, M5 |
| ESTRUCTURA_SALARIO | Salario fijo · Base + comisión · Comisión | Las dos últimas activan el módulo C | PAQ |
| COMISION_BASE, COMISION_DEVENGO, COMISION_PERIODICIDAD, COMISION_PLAZO_DIAS, COMISION_OBJECION_DIAS, COMISION_RESPUESTA_DIAS, PLAN_AVISO_DIAS, SISTEMA_REGISTRO_CAMPO ⚑ | Varios | Solo con módulo C | PAQ |
| SALARIO_OTROS ⚑ | Texto | «Ninguna» si no hay | PAQ |
| PRESTACIONES_EXTRA | Texto largo | Opcional; vacía omite la fila | PAQ, M4 (como PRESTACIONES_SUPERIORES), VAC |
| NIVEL_ACCESO_INFO | General · Calificado | Obligatoria | PAQ, M4 |
| PUESTO_SISTEMAS | Tabla | Opcional; con filas activa la carta responsiva | PAQ, M4 |
| PUESTO_INFO_CATEGORIAS | Texto largo | Obligatoria con Calificado | PAQ |
| PUESTO_PI | Selección de PI_CATALOGO | — | PAQ |
| PERFIL_CLAVE, PERFIL_FECHA, PERFIL_OBJETIVO, PERFIL_FUNCIONES, PERFIL_CONEXAS, PERFIL_REQUISITOS, PERFIL_INDICADORES, PERFIL_RIESGOS, PERFIL_CAPACITACION | Varios | Lineamientos de perfiles; sin criterios discriminatorios | PAQ |
| PERFIL_APROBADO_POR / PERFIL_APROBADO_FECHA | Texto / fecha | Obligatorias con PERFIL_ORIGEN = Sistema | PAQ |
| ACTIVIDADES_PRINCIPALES (lista del puesto) | Lista | 5 a 10; precarga del alta | PAQ |
| PERSONA_JEFATURA | Puesto | Jefatura inmediata; sustituye a JEFE_INMEDIATO | RIT, PER, VAC, M9 |
| DIRECTOR_AREA | Puesto | Opcional | PER, VAC |
| PTU_EXCLUIDO | Sí/No | Independiente del atributo de dirección | PTU |
| PUESTO_CRITICO_SEGURIDAD ◆ (nombre) | Sí/No | — | RIT (art. 60) |
| PUESTO_RIESGO_EMBARAZO_LACTANCIA ◆ (nombre) | Sí/No | — | RIT (art. 65), PER (INC-2) |
| PUESTO_VEDADO_MENORES ◆ (nombre) | Sí/No | — | RIT (art. 67) |
| PUESTO_TIPO_NOM035 | Operativo · Supervisor · Profesional o técnico · Gerente | — | NOM |
| PUESTO_VERSION, PERFIL_VERSION, PRESTACIONES_VERSION | Identificador | Versionado (M5) | M4, M5, M9, VAC |

---

## 4. Alta y expediente de la persona (nivel 3)

### 4.1 Identificación y contacto

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| TRAB_NOMBRE | Nombre y apellidos por campos | Obligatoria | Todos |
| TRAB_CURP | Texto | 18 caracteres con dígito verificador | Todos |
| TRAB_RFC | Texto | Prellenado con la CURP más la homoclave; 13 caracteres | PAQ, M4, M6 |
| TRAB_NSS | Texto | 11 dígitos; necesaria para la baja, no bloquea el contrato | PAQ, M4 |
| TRAB_EDAD, TRAB_SEXO | Número / texto | ◆ P10: derivadas de la CURP (registro 5.1) | PAQ, M9 (menores), VAC |
| TRAB_NACIONALIDAD | Texto | Obligatoria | PAQ |
| TRAB_ESTADO_CIVIL | Texto | La captura la persona; se guarda en el expediente | PAQ, NOM |
| TRAB_ESCOLARIDAD, TRAB_EXPERIENCIA_LABORAL | Texto | Los captura la persona; precarga en la siguiente captura | NOM |
| TRAB_DOMICILIO | Texto por campos | Obligatoria | PAQ, PER, M4 |
| TRAB_EMAIL | Correo | Obligatoria; medio de notificaciones | Todos |
| TRAB_TELEFONO | Celular, 10 dígitos | Obligatoria con FES y Correo y SMS | PAQ, FIR |
| TRAB_CONTACTO_NOMBRE, TRAB_CONTACTO_PARENTESCO, TRAB_CONTACTO_TELEFONO | Texto / teléfono | Obligatorias | PAQ |
| NUM_EMPLEADO | Texto | Opcional; único por empresa | PTU, M9 |
| CHECADOR_ID | Texto (uno por dispositivo si difiere) | Obligatorio para importar al M9; único por empresa | M9 |

### 4.2 Relación de trabajo, lugar y condiciones

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| FECHA_INICIO | Fecha | Obligatoria; vacía por omisión | Todos |
| TIPO_RELACION | Tiempo indeterminado · Obra determinada · Tiempo determinado · Temporada | Obligatoria | PAQ, PTU, M4, M5 |
| CAUSA_TEMPORALIDAD, CAUSA_TIPO, CAUSA_OBRA, OBRA_DESCRIPCION, FECHA_TERMINO, PERSONA_SUSTITUIDA_PUESTO, TEMPORADA_PERIODOS, TEMPORADA_AVISO_DIAS ⚑ | Varios | Según TIPO_RELACION (PAQ) | PAQ, M4 |
| PRUEBA_OPCION | No aplica · Periodo de prueba · Capacitación inicial | No se repite con la misma persona | PAQ, M4 |
| PERFIL_MODALIDAD | Perfil de puesto · Lista de actividades | Precarga de la empresa | PAQ |
| ACTIVIDADES_PRINCIPALES | Lista | 5 a 10; obligatoria con Lista de actividades | PAQ |
| CT_DOMICILIO ⚑ | Selección del catálogo de centros | El centro de la persona; con REPSE_LUGAR_TIPO = Cliente no aplica | PAQ, todos (centro de la persona) |
| CT_AMBITO, CT_OTROS ⚑ | Selección de centros | — | PAQ, M5 |
| REPSE_LUGAR_TIPO | Empresa · Cliente | Empresa; Cliente solo con instalaciones en el catálogo | PAQ, M5 |
| ASIGNACION_INICIO | Fecha | Solo con Cliente | PAQ, M5 |
| SALARIO_PERSONA | Moneda | Precarga de PUESTO_SALARIO_BASE; ≥ mínimo de CENTRO_ZONA_SM; menor que el vigente solo por MOD-1 | Todos |
| FORMA_PAGO | Efectivo · Depósito o transferencia | Obligatoria | PAQ |
| BANCO, CLABE | Texto | Obligatorias si no es efectivo; CLABE de 18 dígitos | PAQ |
| TELETRABAJO | Sí/No | «¿Trabaja días en casa?» | PAQ, M5 |
| TELE_DIAS | Selección de días | Dentro de los días laborados | PAQ, M5, M9 |
| TELE_DOMICILIO_IGUAL / TELE_DOMICILIO | Casilla / texto | — | PAQ |
| TELE_ORIGEN, TELE_SOLICITUD_FECHA, TELE_AUTORIZACION_ORGANO, TELE_AUTORIZACION_FECHA, TELE_ADAPTACION ⚑, TELE_ADAPTACION_DIAS ⚑ | Varios | Módulo T | PAQ, M5 |
| HIBRIDO_ORIGEN | Solicitud de la Persona Trabajadora · Decisión de la Empresa | — | PAQ, M5 |
| SINDICALIZADO | Sí/No | Solo con SINDICATO = Sí | PTU |

### 4.3 Firma, herramientas y entregas

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| FIRMA_MODALIDAD | Autógrafa · Electrónica | Una sola vez para el contrato y el kit | Todos |
| TIPO_FIRMA | FES · e.firma | Solo con Electrónica; FES | PAQ, FIR |
| MEDIO_IDENTIFICACION | Presencial · INE y video de aceptación · e.firma · Remota sin verificación | Obligatoria con Electrónica | PAQ, FIR |
| BIOMETRICO_FIRMA_CONSENT | Sí/No con fecha, hora y versión del texto | La otorga la persona en la Plataforma; solo en la contratación | PAQ, FIR |
| BIOMETRICO_JORNADA_CONSENT | Sí/No con fecha y hora | La otorga la persona en la casilla del aviso; solo se pide con REGISTRO_BIOMETRICO = Sí | PAQ, M9 |
| FECHA_FIRMA / LUGAR_FIRMA | Fecha / texto | LUGAR_FIRMA: municipio del centro por omisión | Todos |
| INTRANET | Sí/No | Obligatoria | PAQ |
| CORREO_INSTITUCIONAL | Correo | Dominio de la empresa; obligatoria con INTRANET = Sí | PAQ, M4 |
| EQUIPO_DESCRIPCION | Tabla: descripción, marca y modelo, serie o identificador, estado, valor de reposición | Una fila por bien | PAQ, RIT (FD-5), M4 |
| BENEFICIARIOS | Tabla | Hasta 4; suman 100 | PAQ, M4 |
| BENEF_CONFIRMACION_FECHA | Fecha | La actualiza ACT-1 | M4, M5, PER |
| AVISO_ENTREGA, DOCUMENTOS_ENTREGA, DOCUMENTOS_ENTREGADOS, RIT_ENTREGA, CLIENTE_LINEAMIENTOS_ENTREGA ⚑ | Texto (fecha y medio) | Anexo 3 | PAQ |

### 4.4 Créditos, pensión y datos protegidos

| Variable | Tipo | Validación u omisión | La usan |
|---|---|---|---|
| INFONAVIT_CREDITO | Sí/No | Opcional | PAQ, M4, M9 |
| INFONAVIT_DESCUENTO_TIPO ⚑ | Porcentaje · Cuota fija · Veces salario mínimo | Con crédito; opciones por confirmar | PAQ, M4, M9 |
| INFONAVIT_DESCUENTO_VALOR | Número | Con crédito | PAQ, M4, M9 |
| FONACOT_CREDITO | Sí/No | Opcional | PAQ, M4, M8, M9 |
| FONACOT_DESCUENTO_MONTO | Moneda mensual | Valor esperado; prevalece la cédula | PAQ, M4, M8, M9 |
| PENSION_ALIMENTICIA | Sí/No | Opcional | M4, PTU, M9 |
| PENSION_AUTORIDAD, PENSION_EXPEDIENTE | Texto | Obligatorias con PENSION_ALIMENTICIA = Sí | M4 |
| PENSION_PORCENTAJE | Porcentaje | De la resolución | M4, PTU, M9 |
| PENSION_INCLUYE_PTU / PENSION_BASE_PTU | Sí/No / Bruta · Neta de ISR | Sin dato, la PTU no calcula pensión | PTU |
| EMBARAZO_INFORMADO_FECHA | Fecha | Expediente; la captura RH; nunca se imprime; deja de usarse con C3 | M4, M5 |

---

## 5. Tablas globales (las administra AEXIS; vigencia y aprobación humana)

| Tabla | Contenido | La usan |
|---|---|---|
| Parámetros fiscales y de seguridad social (UMA, TARIFA_ISR_96, SUBSIDIO_EMPLEO, CUOTAS_IMSS, EXENCIONES_93) y REF_EXENCION | M4, 5.3 | M4, PTU |
| SALARIO_MINIMO | Año, zona, monto | Todos los que validan salario; M4 |
| JORNADA_MAXIMA / TE_LIMITES | Máximos por año y límites del tiempo extra | M9, catálogo de jornadas, RIT |
| PARAMETROS_LEGALES_VACACIONES / PARAMETROS_LEGALES_PERMISOS | Días, plazos y duraciones | VAC, PER |
| PORCENTAJE_PTU / PTU_COMPUTA / AGUINALDO_COMPUTA | Porcentaje vigente y tablas gemelas de días computables | PTU, VAC, PER |
| FONACOT_PLAZOS / FONACOT_CALENDARIO / PAGO_CLAVES_SAT | Plazos del convenio, calendario de cédulas, claves de percepción | M8, M4, M6, M9 |
| PERMISO_LEY_* | Filas fijas de la tabla I del RIT | RIT, PER |
| Calendario de días inhábiles | Fines de semana y días de descanso obligatorio (global) más los días que marque la empresa | Todos los plazos en días hábiles |

---

## 6. Calculadas o de evento que leen varios módulos

| Variable | Qué es | Dueño | La leen |
|---|---|---|---|
| SALARIO_PERSONA_LETRA | «… pesos NN/100 M.N.» | PAQ / M5 | PAQ, M5 |
| DIA_PAGO | Texto por persona, de PERIODICIDAD y DIA_PAGO_SEMANAL o DIAS_PAGO_QUINCENAL | PAQ | PAQ |
| PERIODICIDADES_PAGO_EMPRESA / DIAS_PAGO_RESUMEN | Periodicidades usadas por los puestos | RIT | RIT, PER |
| TELETRABAJO_ACTIVO / HIBRIDO_ACTIVO / DIAS_EN_CASA_ACTIVO / PORC_TIEMPO_DOMICILIO | Modalidad calculada | PAQ | PAQ, M5, M9, RIT |
| PLANTILLA_NUM | Personas activas | Sistema | RIT, CYA |
| RIT_ESTADO / RIT_DEPOSITADO / RIT_FECHA_DEPOSITO | Estado del RIT | RIT | PAQ, PER |
| Versión de condiciones de la persona | PUESTO, PERFIL, JORNADA y PRESTACIONES vigentes de la persona | M5 | Todos |
| BAJA_FECHA / BAJA_MOTIVO | Baja | M4 | Todos |
| SITUACION_PROTEGIDA / SITUACION_PROTEGIDA_TIPO | Situación protegida | PER | M4, M5 |
| Estado de cada falta (Por confirmar · Confirmada) | Ausencias sin evento | M9 vía PER | PER, VAC, PTU |
| FIRMA_SELLO_TRAB / FIRMA_SELLO_EMPRESA / FIRMA_EMPRESA_NOMBRE / FIRMA_EMPRESA_CARGO | Sello y firmante | FIR | Todos los documentos con firma electrónica |
| CFDI_REGISTRADO / UUID_CFDI | Evidencia del pago | M6 | PTU |
| D4_REUBICACION / D4_REUBICACION_FIN | Reubicación en D4 | M5 | PER, VAC, PTU |
| INCAPACIDAD_PARCIAL / INCAPACIDAD_PARCIAL_FECHA | Al cerrar C2 | PER | M5 |

---

## 7. Equivalencias (nombre en un documento → nombre canónico)

El motor de plantillas resuelve el nombre de la izquierda al campo de la derecha. Las especificaciones no se reescriben por esto; se ajustan cuando su conversación emita otra versión.

| Nombre usado | Dónde | Canónico |
|---|---|---|
| RAZON_SOCIAL | RIT, PTU | PATRON_RAZON_SOCIAL |
| RFC | RIT, PTU | PATRON_RFC |
| DOMICILIO_FISCAL | RIT | PATRON_DOMICILIO |
| ACTIVIDAD_ECONOMICA | RIT | PATRON_ACTIVIDAD |
| NOMBRE_COMERCIAL | RIT | PATRON_NOMBRE_COMERCIAL ◆ |
| REGISTRO_PATRONAL | RIT, PTU | CENTRO_REGISTRO_PATRONAL (◆ P1) |
| EMPRESA_TIPO_PERSONA, TIPO_PATRON | PTU, comisiones | PATRON_TIPO_PERSONA |
| REPRESENTANTE_LEGAL, REPRESENTANTE_LEGAL_NOMBRE | PTU, CMR | REP_NOMBRE |
| NOMBRE_PERSONA, PERSONA_NOMBRE | PTU, RIT | TRAB_NOMBRE |
| CURP, PERSONA_CURP | PTU, M9, CMR | TRAB_CURP |
| PERSONA_PUESTO | RIT | PUESTO |
| PERSONA_CENTRO, CENTRO_TRABAJO, CENTRO_TRABAJO_NOMBRE | RIT, PER, VAC | CENTRO_NOMBRE del centro de la persona (CT_DOMICILIO) |
| PERSONA_CORREO | RIT | TRAB_EMAIL |
| DOMICILIO_CENTRO | PTU | CENTRO_DOMICILIO |
| MUNICIPIO_ESTADO | PTU | CENTRO_MUNICIPIO_ESTADO (derivada) |
| FECHA_BAJA | PTU | BAJA_FECHA |
| BIEN_DESCRIPCION, BIEN_IDENTIFICACION, BIEN_ESTADO_ENTREGA, BIEN_VALOR_REPOSICION | RIT | Columnas de EQUIPO_DESCRIPCION |
| RESGUARDO_FECHA | RIT | FECHA_FIRMA de la carta responsiva |
| TURNO_NOMBRE, TURNO_CENTRO | RIT, M9 | Nombre y centro del turno (JORNADA_ID) |
| TURNO_TIPO_JORNADA | RIT | JORNADA_TIPO |
| TURNO_DIAS_LABORABLES | RIT | DIAS_LABORADOS |
| TURNO_ENTRADA, TURNO_SALIDA | RIT, M9 | Campos de HORARIO |
| TURNO_COMIDA | RIT | DESCANSO_MINUTOS |
| TURNO_DESCANSO_TIPO | RIT | DESCANSO_SEMANAL |
| TURNO_DESCANSO_SEMANAL | RIT | DESCANSO_DIAS |
| TURNO_DIAS_TRABAJO_SEMANA | RIT | DIAS_TRABAJO_SEMANA |
| TURNO_HORAS_SEMANA | RIT | HORAS_SEMANA |
| PUESTOS_CRITICOS_SEGURIDAD, AREAS_RESTRINGIDAS_EMBARAZO_LACTANCIA, AREAS_RESTRINGIDAS_MENORES | RIT (listas calculadas) | Puestos con PUESTO_CRITICO_SEGURIDAD, PUESTO_RIESGO_EMBARAZO_LACTANCIA o PUESTO_VEDADO_MENORES = Sí |
| PRESTACIONES_SUPERIORES | M4 | PRESTACIONES_EXTRA |
| SALARIO_DIARIO | PER (INC-1) | SALARIO_PERSONA (en el layout de importación de PTU, SALARIO_DIARIO solo es el nombre de la columna de cotejo) |
| JEFE_INMEDIATO | Versiones anteriores | PERSONA_JEFATURA |
| PRESTACION_SEGURO_VIDA | Versiones anteriores | SEGURO_VIDA |
| TRAB_EMAIL_INSTITUCIONAL | Versiones anteriores | CORREO_INSTITUCIONAL |
| N_REP, NUM_REP_TRAB, NUM_REP_POR_PARTE | Versiones anteriores | NUM_REPRESENTANTES_POR_PARTE |
| CMRIT_INTEGRACION_MODO | Versiones anteriores | DESIGNACION_OBRERA |
| BIOMETRICO_CONSENTIMIENTO | M9 v1.0 | BIOMETRICO_JORNADA_CONSENT |
| FALTAS_VENTANA_30 | PER v1.8 | FALTAS_VENTANA_30_CONFIRMADAS / _POR_CONFIRMAR |

Nombres que el módulo 4 pidió verificar: TRAB_RFC (confirmado, 4.1), PRIMA_VACACIONAL_PCT (confirmado, 1.7), BENEFICIARIOS (confirmado, 4.3); JORNADA_RESUMEN y CARTA_RESPONSIVA son textos o documentos del propio módulo 4, no datos de captura.

---

## 8. Decisiones pendientes del usuario (propuestas de Cerebro)

| # | Hallazgo | Propuesta | Efecto |
|---|---|---|---|
| P1 | El contrato pide un registro patronal de la empresa (PATRON_REG_PATRONAL), pero el RIT y la PTU lo leen por centro, y la revisión de pantallas (hallazgo 11) pide varios registros patronales | Fuente única: CENTRO_REGISTRO_PATRONAL. PATRON_REG_PATRONAL pasa a derivada: el registro del centro de la persona (CT_DOMICILIO). Con REPSE en instalaciones del cliente queda por definir de qué centro de la Empresa se toma | Sin cambio de texto en el contrato; cambia el origen del dato |
| P2 | COMPETENCIA (Federal · Local, contrato) y AUTORIDAD_INSPECCION («Federal / Local y nombre», PTU y permisos) capturan dos veces el ámbito | COMPETENCIA es la única fuente del ámbito; AUTORIDAD_INSPECCION guarda solo el nombre de la autoridad, prellenado según COMPETENCIA y editable | Un dato menos; evita contradicciones entre el contrato y D-03 o INC-1 |
| P3 | Todos los módulos validan «salario mínimo de la zona del centro», pero ningún documento define la zona del centro | Nueva CENTRO_ZONA_SM en el catálogo de centros (General · Zona Libre de la Frontera Norte), sin valor por omisión. Si el software ya la tiene, se usa su nombre | Validaciones de PAQ, M5 y SALARIO_TOPADO de M4 |
| P4 | El salario base del puesto se usa para precargar SALARIO_PERSONA, pero no tiene nombre | PUESTO_SALARIO_BASE (organigrama, moneda, ≥ mínimo de la zona) | Solo nombre |
| P5 | PI_ACTIVAR está en la configuración de la empresa (paquete), pero el registro (sección 2) dice que la propiedad intelectual es atributo del puesto | La cláusula de propiedad intelectual se activa con PI_ACTIVAR = Sí (la empresa la usa) y el puesto con PUESTO_PI no vacío; sin variable nueva | Encargo al paquete: ajustar la condición de la cláusula décima quinta |
| P6 | El RIT (art. 41) y la comisión de capacitación leen MOD_PRUEBA como «dato del paquete», pero el paquete no la define | MOD_PRUEBA como pregunta de la empresa («¿La Empresa usa periodo de prueba o capacitación inicial?»), sin valor por omisión, con alerta si un alta elige PRUEBA_OPCION ≠ No aplica y aquí dice No. Mismo criterio de DIAS_EN_CASA_EMPRESA: derivarla de las altas cambiaría el RIT sin que nadie lo decida | Variable nueva de empresa; cambiarla con el RIT depositado activa la alerta de depósito |
| P7 | REPSE_APLICA está en la empresa (paquete), pero el registro 5.1 pregunta «Trabajador REPSE» en el alta; el RIT y el M9 usan REPSE_EMPRESA | REPSE_EMPRESA (calculada: folio y vigencia) para la Empresa; REPSE_APLICA en el alta (la persona es trabajadora REPSE), visible solo si REPSE_EMPRESA = Sí | Encargo al paquete: confirmar el nivel en su diccionario |
| P8 | PORTAL_DESCARGA: el paquete la infiere en la empresa (⚑) y la especificación de firma la pone en el alta | En la empresa, prellenada con la intranet | Una sola captura |
| P9 | El paquete calcula PERIODICIDAD (semanal si hay trabajo material; quincenal en los demás casos), pero el registro (sección 2) dice que la define el puesto y que solo el trabajo material obliga a semanal | Atributo del puesto (Semanal · Quincenal) con bloqueo de quincenal si TRABAJO_MATERIAL = Sí | Encargo al paquete: corregir la regla, sin cambio de texto |
| P10 | El paquete captura TRAB_EDAD y TRAB_SEXO; el registro 5.1 dice que se toman de la CURP | Derivadas de la CURP, editables solo si la CURP no los da | Encargo al paquete: anotar el origen |

---

## 9. Variables eliminadas (no programar)

SALARIO, SALARIO_LETRA, CENTAVOS y SALARIO_DIARIO como base de cálculo (sustituidas por SALARIO_PERSONA y SALARIO_PERSONA_LETRA) · PUEDE_SALIR · TELE_APTO · PRESTACIONES_SUPERIORES como variable de empresa · TIPO_PATRON · JEFE_INMEDIATO · TRIBUNAL_COMPETENTE · DIA_PAGO como dato de empresa (sigue como texto derivado por persona) · PERIODICIDAD_PAGO · MODULO_TELETRABAJO · MODULO_PAGO_DIAS_ESPERA · TRATAMIENTO_EXCEDENTE · ANEXO5 · ANEXO_COMITE, INTEGRANTES_COMITE, COMITE_PUESTO, COMITE_CARACTER · RIT_REVISION_FIJACION_MESES · ALERTA_PATRON_VENTANAS · BIOMETRICO_CONSENTIMIENTO · FALTAS_VENTANA_30 · RENUNCIA_*, RATIFICACION*, RECIBE_NOMBRE, RECIBE_CARGO, CONV_PENA_DIARIA · VAC_PROGRAMACION_EMPRESA_DIAS, VAC_VENTANA_PROGRAMACION_DIAS, VAC_AVISO_REPROGRAMACION_DIAS. El detalle de cada eliminación está en la sección de variables eliminadas de cada especificación.

---

## 10. Impacto en el sistema

| Variable | Nivel | Tipo | Validación | Qué activa |
|---|---|---|---|---|
| PATRON_NOMBRE_COMERCIAL (nueva, nombre canónico del NOMBRE_COMERCIAL del RIT) | Empresa | Texto | Opcional | Dictamen y art. 1 del RIT |
| CENTRO_ZONA_SM (◆ P3) | Catálogo de centros | General · Zona Libre de la Frontera Norte | Sin valor por omisión; obligatoria | Validación del salario mínimo; SALARIO_TOPADO |
| PUESTO_SALARIO_BASE (◆ P4) | Organigrama | Moneda | ≥ salario mínimo de la zona | Precarga de SALARIO_PERSONA |
| MOD_PRUEBA (◆ P6) | Empresa | Sí/No | Sin valor por omisión; alerta con PRUEBA_OPCION ≠ No aplica y MOD_PRUEBA = No | Art. 41 del RIT; activación de la comisión de capacitación |
| PUESTO_CRITICO_SEGURIDAD, PUESTO_RIESGO_EMBARAZO_LACTANCIA, PUESTO_VEDADO_MENORES (nombres) | Organigrama | Sí/No | — | Arts. 60, 65 y 67 del RIT; INC-2 |
| PENSION_ALIMENTICIA, PENSION_AUTORIDAD, PENSION_EXPEDIENTE, PENSION_PORCENTAJE, PENSION_INCLUYE_PTU, PENSION_BASE_PTU (alta formal; las pedían M4 y PTU) | Alta | Sección 4.4 | Sección 4.4 | Deducción en el finiquito, la PTU y la prenómina |
| CENTRO_MUNICIPIO_ESTADO | Derivada | Texto | Del catálogo de centros | Documentos de PTU |
| PATRON_REG_PATRONAL (◆ P1) | Pasa a derivada | Texto | Del centro de la persona | Carátula del contrato |
