# AXIARH — Registro de decisiones de los documentos maestros

Actualizado: 13 de noviembre de 2026 · Responsable: Damián Torres

Este documento es la base de todas las conversaciones del proyecto. Reúne el catálogo de documentos maestros, la arquitectura del sistema, las decisiones tomadas por documento y las reglas que el sistema debe aplicar. Todas las aprobaciones son **provisionales** hasta la revisión final de cada documento. Cuando una conversación tome una decisión nueva, se agrega aquí con su fecha. Las contradicciones entre conversaciones y su propuesta de solución están en «Axia RH - Mapa del PMV».

---

## 1. Catálogo de documentos maestros

| Documento | Grupo | Se genera | Estado |
|---|---|---|---|
| Paquete de contratación: contrato con carátula (tipos A indeterminado, B obra, C tiempo determinado, D temporada), biblioteca de módulos y kit integrado | Contratación | Siempre | **Cerrado por el usuario (26/10/2026)**; ajustes del 28/10 aplicados. Contrato rev. 473, biblioteca rev. 80, visor del paquete integrado v9; versión para programación (actualizada el 31/10 con el ajuste del aviso) y diccionario de variables generados |
| Perfil de puesto (Anexo 1 del contrato) | Contratación | Según PERFIL_MODALIDAD: solo con «Perfil de puesto»; lo genera la IA del sistema con los lineamientos y lo valida una persona | Cerrado con el paquete |
| Lineamientos para generar perfiles de puesto | Sistema | Base de la IA que genera los perfiles | Borrador |
| Aviso de privacidad para personas trabajadoras (Anexo 4) | Contratación | Siempre | Cerrado con el paquete; ajuste del 31/10 aplicado (pruebas y exámenes) |
| Aviso de privacidad para candidatos | Reclutamiento | En reclutamiento | Borrador (en el visor del kit; el documento de Claude Docs ya no es vigente) |
| Convenio de confidencialidad (+ Anexo A de información, activos y accesos) | Contratación (módulo) | Nivel de acceso «Calificado» | Borrador |
| Adenda de confidencialidad | Contratación | Personal contratado antes de adoptar el kit | Por redactar |
| Carta responsiva de herramientas físicas y digitales (+ anexo de inventario) | Contratación | Hay equipo asignado, días en casa (teletrabajo o híbrido), correo institucional o sistemas asignados al puesto | Borrador |
| Designación de beneficiarios | Contratación | Siempre | Borrador |
| Acuerdo de descuento | Contratación | Hay descuento capturado | Borrador; se trabaja en otra conversación |
| Constancia de recibo del RIT (FR-1) | Contratación | En la emisión, en cada alta y en cada modificación; no se genera sin acuse de depósito. (13/11/2026) Se firma con la modalidad de los documentos de contratación de cada persona (FIRMA_MODALIDAD); al ingreso, dentro del paquete | Borrador (pestaña «Formatos» del RIT); incluida en la especificación del RIT |
| Documento de asignación de correo institucional | Contratación | INTRANET = Sí; se entrega con el contrato | Por redactar |
| Documento de designación del sistema de registro de jornada | Contratación | Siempre | Existe como sección B del Anexo 3 del contrato; falta unificarlo con el kit |
| Oficio de asignación REPSE | Operación | Cada asignación de un trabajador REPSE a un cliente, solo si el lugar de trabajo es el del cliente | Modelo propuesto |
| Comunicado de cambio de centro de trabajo | Operación | Cada cambio de centro | Propuesto |
| Convenio de terminación de la relación de trabajo y finiquito (módulos A mutuo consentimiento, B voluntad de la Persona Trabajadora, C vencimiento de plazo u obra, D fin del periodo de prueba o capacitación, E liquidación de rescisión, E-bis rescisión por la Persona Trabajadora) | Terminación | Siempre, en toda baja salvo fallecimiento | Redactado; especificación del módulo 4 v1.0 (27/10/2026) |
| Recibo de finiquito con desglose de conceptos | Terminación | Siempre, en toda baja (anexo del convenio) | Redactado; especificación v1.0 |
| Aviso de rescisión (con constancia de negativa) | Terminación | Rescisión por causa imputable a la Persona Trabajadora | Redactado; especificación v1.0 |
| Documento de terminación al vencer el periodo de prueba o de capacitación | Terminación | Al vencer el periodo, con evaluación, F-2 y, en capacitación, evidencia de la capacitación | Redactado; especificación v1.0 |
| Comunicado de terminación por vencimiento del plazo o terminación de la obra | Terminación | Contratos por tiempo u obra determinada | Redactado; especificación v1.0 |
| Convenio de pago a beneficiarios | Terminación | Fallecimiento | Redactado; especificación v1.0 |
| Comunicado de suspensión por fin de temporada | Terminación / Modificaciones | Contratos de temporada | Por redactar |
| Documento de terminación por incapacidad (art. 54) | Terminación | Incapacidad por riesgo no profesional | Por redactar (prioridad C) |
| Hoja interna del escenario de negociación | Terminación (uso interno) | Solo en pantalla o para la Empresa; nunca se entrega | Por redactar |
| Constancia de salida | Terminación | Al terminar la relación | Borrador; se trabaja en otra conversación |
| Acta de devolución y entrega de herramientas | Terminación | Al terminar la relación, siempre que haya habido entrega de herramientas, cuentas, accesos o información | Plantilla en el paquete integrado; reglas de cierre en el módulo 4; falta su cláusula de cierre |
| Reglamento Interior de Trabajo (89 artículos en 13 capítulos; Anexo A conductas y escala; Anexo B generado del catálogo de jornadas; Anexos C Comité por puestos y D ubicación de políticas, ambos opcionales) — https://claude.ai/artifact/1zoJd9K6M4EVpEuKdcisvW (rev. 1340) | Colectivo | Precargado; ajustes mínimos; depósito ante el CFCRL | **Cerrado para programación (12/11/2026)**; especificación v1.1 |
| Especificación para programación del RIT y sus formatos v1.1 («AXIARH - RIT - Especificacion para programacion», 12/11/2026; sustituye a la 1.0, que no se cargó) | Sistema | — | Entregada; el usuario la correrá y dará retroalimentación |
| Acta de integración y estatutos de la CMRIT (un solo instrumento) — https://claude.ai/artifact/XNGvnyBsNnkJ7fHZxy9Sqy | Colectivo | Con el RIT | En revisión |
| Formatos disciplinarios FD-1 aviso de hechos, FD-2 acta de audiencia, FD-3 resolución, FD-4 falta leve, FD-5 daño o pérdida | Colectivo / Terminación | Cada expediente disciplinario (folio EXP_FOLIO); FD-1 a FD-3 documentan los hechos previos a una rescisión | Borrador (pestaña «Formatos» del RIT, rev. 11); incluidos en la especificación del RIT |
| Constancia de difusión del RIT (FR-2) | Colectivo | Por centro, con fotografía; verificación cada RIT_REVISION_FIJACION_MESES meses; no se genera sin acuse de depósito | Borrador; incluida en la especificación del RIT |
| Juego de la Comisión Mixta de Capacitación, Adiestramiento y Productividad: oficio al sindicato o designación por las personas trabajadoras, acta de integración e instalación con Bases de Funcionamiento, y formatos F-1 a F-5; elección opcional con D-01 y D-02 del kit de PTU | Colectivo | Plantilla de más de 50 personas, o uso de periodo de prueba o capacitación inicial | En revisión por el usuario |
| Kit de PTU (D-01 a D-14 y reglas R-1 a R-3), con y sin sindicato; dictamen con módulos A, B y C — https://claude.ai/artifact/Us8yMoYr6pkYNNBs5RjwdH (rev. 45) | Colectivo | Anual | Borrador completo, pendiente de revisión final |
| Recibo individual de PTU (D-14) | Colectivo | Cada pago de PTU, salvo si se pagó con el finiquito; sigue FIRMA_MODALIDAD | Borrador |
| Registros digitales del módulo de permisos y licencias: SP-1 registro de permiso y SUS-3 lista de reincorporación (la persona confirma en la Plataforma y RH valida) | Eventos | En cada evento resuelto en la Plataforma; formato en papel de respaldo (SALIDA = Respaldo) y constancia exportable (SALIDA = Constancia) | **Terminado (12/11/2026)** |
| Documentos del módulo de permisos y licencias: LIC-1 acuerdo de lactancia, LIC-2 notificación de comisión permanente (con acuse), LIC-3 convenio de licencia sin goce, INC-1 aviso de accidente de trabajo, INC-2 solicitud de transferencia de semanas prenatales, SUS-1 constancia de suspensión, SUS-2 aviso de suspensión por falta de documentos | Eventos | Según el tipo de evento; siguen FIRMA_MODALIDAD | **Terminado (12/11/2026)** |
| Especificación para programación del módulo de permisos y licencias v1.4 («AXIARH - Módulo de permisos y licencias - Especificación para programación», 12/11/2026, lógica y textos; armonizada con el registro, el mapa y el RIT v1.1) | Sistema | — | Entregada |
| Políticas internas (código de ética, vestimenta, TIC, vehículos, regalos y conflictos de interés, protocolo de acoso, riesgo psicosocial, exámenes médicos y pruebas, prevención de la fatiga, ergonomía y pausas activas, trabajo híbrido y jornada flexible, viáticos y traslados) y registro de políticas vigentes | Políticas | Documentos aparte; el RIT remite al registro de políticas. (12/11/2026) La política de vehículos solo se genera con VEHICULOS_ASIGNADOS = Sí; los arts. 9 y 22 del RIT remiten a las de viáticos y traslados y de trabajo híbrido y jornada flexible | Para después (el código de ética figura como hecho en el RIT) |

Kit de contratación del nivel básico: contrato, perfil de puesto, constancia de entrega de herramientas físicas o digitales, aviso de privacidad, convenio de confidencialidad si aplica y constancia de recibo del RIT.

---

## 2. Arquitectura del sistema

Cada dato se captura una sola vez, en el nivel que le corresponde.

| Nivel | Quién lo captura | Qué contiene |
|---|---|---|
| 1. Configuración de la empresa | Consultoría | (31/10/2026) PERFIL_MODALIDAD (Perfil de puesto / Lista de actividades). Datos generales, representante, centros de trabajo con domicilio completo, folio, vigencia y actividades REPSE registradas (cada una con su número y descripción), forma de pago, día de pago semanal, dominio de correo institucional, prestaciones extralegales por puesto (PRESTACIONES_EXTRA), apoyo de gastos y medios de contacto de teletrabajo, sistema de registro de jornada y si usa geolocalización, apoyo para los gastos del domicilio en la modalidad híbrida (HIBRIDO_APOYO_MODO y HIBRIDO_APOYO_MONTO), días de aviso de cambios al perfil de puesto (PERFIL_AVISO_DIAS), correo para asuntos de datos personales (AVISO_CORREO_DATOS), catálogo de propiedad intelectual (PI_CATALOGO), pena del convenio de confidencialidad (CONV_PENA y sus datos), parámetros del RIT (tolerancias, permisos, plazos, conservación, reincidencia) y datos colectivos (sindicato, número de personas trabajadoras, turnos) |
| 2. Organigrama | Consultoría | (31/10/2026) ACTIVIDADES_PRINCIPALES (de 5 a 10; obligatoria con Lista de actividades). Puestos con sus atributos legales, condiciones de trabajo, perfil de puesto versionado y, por puesto, sistemas y plataformas (PUESTO_SISTEMAS), información confidencial a la que accede (PUESTO_INFO_CATEGORIAS) y propiedad intelectual a la que accede (PUESTO_PI) |
| 3. Alta de la persona trabajadora | RH del cliente | Datos personales, puesto, centro de trabajo, ámbito geográfico, fecha de inicio, modalidad de inicio, salario, días en casa, trabajador REPSE y lugar de trabajo REPSE (Empresa o Cliente), origen de la modalidad híbrida (HIBRIDO_ORIGEN), equipo (tabla EQUIPO_DESCRIPCION: descripción, marca y modelo, serie, estado), beneficiarios, descuento, firma |

Regla general: las condiciones de trabajo vienen preestablecidas por la empresa y el puesto. A RH no se le pregunta nada que pueda definirse en los niveles 1 o 2.

(26/10/2026) Los eventos (baja, permisos y licencias, contratos y vencimientos, PTU, vacaciones y aguinaldo) ya tienen su propia pantalla en el software, separada del alta. Con eso queda cubierta la necesidad del cuarto nivel: cada evento captura sus datos en su pantalla y toma los de los niveles 1 a 3.

(26/10/2026) El software ya tiene un catálogo de horarios o turnos. El Anexo B del RIT y la cláusula de jornada deben generarse desde ese catálogo, sin capturar el horario dos veces.

(26/10/2026, aprobada) **Cambios al catálogo con personas ya contratadas.** Cuando cambia el perfil de puesto, el sistema genera una alerta y una nueva versión para firma de quienes ya firmaron la anterior, con el aviso de PERFIL_AVISO_DIAS días de la cláusula 1.4. (26/10/2026, aprobada) La misma lógica se extiende a jornada, salario y prestaciones del puesto: el cambio aplica de inmediato a las altas nuevas y, para las personas ya contratadas, genera el comunicado o el convenio que corresponda según la matriz del módulo 5; nunca cambia en silencio sus condiciones.

(26/10/2026) La comisión de seguridad e higiene y su alerta salen de Axia RH por ahora.

(26/10/2026, aprobada) **Catálogo de clientes REPSE** en la configuración de la empresa: razón social, RFC, domicilio de cada instalación, fecha y número del contrato de servicios y actividad REPSE que se presta. Se elimina el centro genérico «Instalaciones del beneficiario». Con REPSE = Sí y lugar Cliente, el centro de trabajo se elige de las instalaciones del catálogo, su domicilio se imprime en el contrato y se genera el oficio de asignación; cada reasignación es un nuevo oficio desde el módulo de modificaciones. El catálogo sirve también como expediente por cliente.

### Atributos de cada puesto (organigrama)

| Atributo | Valores | Efecto |
|---|---|---|
| Clasificación | Base / Confianza | Contrato, RIT y elegibilidad como representante obrero en las comisiones |
| Puesto de dirección o administración, o técnico o profesional especializado | Sí / No | 180 días de prueba o 6 meses de capacitación. Es independiente de la clasificación base/confianza |
| Trabajo material | Sí / No | Solo pago semanal |
| (26/10/2026, aprobada) Periodicidad de pago | Semanal / Quincenal | Se define en el perfil de puestos, no en el alta; en trabajo material solo semanal. El RIT lista las periodicidades que usa la empresa |
| (26/10/2026, aprobada) Salario | Monto fijo por puesto | Se define en el puesto y se muestra en el alta sin edición. Por ahora el tabulador no maneja rangos: un solo salario por puesto |
| Nivel de acceso a la información | General / Calificado | Calificado activa el convenio de confidencialidad |
| Jornada, horario, días laborables, descanso (fijo o rotativo) | — | Cláusula de jornada |
| Tiempo de comida y si puede salir del centro | — | Variante de la cláusula de jornada |
| Teletrabajo permitido | Sí / No | Muestra las casillas de días en casa |
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
- (28/10/2026, aprobada) **PERFIL_MODALIDAD.** Con «Lista de actividades», la cláusula 1.1 enlista ACTIVIDADES_PRINCIPALES y no se genera el Anexo 1 ni el perfil del kit; las cláusulas de clasificación, labores conexas, actualización, prueba, capacitación inicial y confidencialidad y la Declaración II b) usan su variante; con prueba o capacitación inicial, la Empresa comunica por escrito los criterios de evaluación o el programa. Opción menos recomendable, permitida por decisión del usuario; riesgo explicado una vez.
- (26/10/2026, aprobada) Sin remisiones numéricas entre cláusulas: 25 identificadores estables (CL_*) como código interno, que no se imprimen.
- (26/10/2026, aprobada) Se elimina el Anexo 5. Anexos: 1 perfil de puesto, 2 beneficiarios, 3 acuses (incluye la carta responsiva), 4 aviso de privacidad.
- (26/10/2026, aprobada) No se cambia el título de la cláusula de formalización por medios electrónicos sin actualizar los documentos del kit que la citan.
- (26/10/2026) Sin acuse de recepción al final del contrato. El Anexo 3 es el único acuse: su primera fila acredita la entrega del ejemplar del contrato, la carátula y los anexos que le corresponden (variable ANEXOS_LISTA, la misma de la fila «Anexos» de la carátula).
- (26/10/2026, propuesta tomada de los contratos anteriores; provisional) Declaración II d): la Persona Trabajadora conoce que su patrón es la Empresa y que clientes, proveedores, empresas relacionadas o titulares de licencias, marcas o instalaciones no son su patrón por ese solo hecho, sin limitar las responsabilidades que la ley imponga a terceros.
- (26/10/2026, ídem) Cláusula 1.4: toda modificación al perfil de puesto se comunica por escrito con PERFIL_AVISO_DIAS días naturales de anticipación (variable de la empresa, por omisión 15) y con constancia; las modificaciones a funciones de distinta naturaleza o categoría superior, o a las condiciones de trabajo, requieren acuerdo previo y por escrito.
- (26/10/2026) Cláusula 1.2, labores conexas: se quita la frase «sin derecho a una compensación adicional». (Actualizado 26/10/2026, decisión del usuario) La estrategia es que las labores conexas o complementarias son parte de las actividades del puesto. La cláusula 1.2 dice que forman parte de las actividades del puesto y que la Persona Trabajadora las desempeña sin que implique cambio de puesto; ya no afirma que estén comprendidas en el salario. Aplicado al contrato (rev. 312). Riesgo explicado una vez (ver pendiente).
- (26/10/2026, ídem) Cláusula 10: la Persona Trabajadora entrega el aviso de retención de su crédito INFONAVIT dentro de 3 días hábiles; la Empresa aplica la retención desde que lo recibe. No se traslada a la Persona Trabajadora el pago de recargos u omisiones de la Empresa (el contrato anterior lo hacía por descuento vía nómina).

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
- Descanso semanal fijo (uno o varios días) o rotativo.
- Dos variantes según si la persona puede salir del centro durante la comida; el dato viene del puesto.
- Cláusula 6.5: registro electrónico de jornada con aceptación expresa del sistema que designe la empresa. La ubicación se registra solo si la empresa lo tiene preestablecido (variable REGISTRO_GEOLOC). Hay un documento de designación del sistema. (26/10/2026, aprobada) La ubicación no requiere consentimiento. Los biométricos requieren consentimiento expreso, libre e independiente, recabado en una casilla propia del apartado 10 del aviso de privacidad; el medio alterno (PIN o tarjeta, SISTEMA_REGISTRO_ALTERNO) opera para quien no lo otorgue o lo revoque, sin consecuencia laboral, y también si el sistema falla. El Anexo 3 y la cláusula de jornada solo lo hacen constar. PUEDE_SALIR_B pasa a PUEDE_SALIR, dato del puesto.
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
- Reglas del sistema: exigir carta responsiva con inventario si hay equipo asignado; alertar si la Empresa no tiene la política de uso de TIC; (31/10/2026) alertar si la Empresa no tiene la política de trabajo híbrido y jornada flexible, que regula la solicitud, la autorización y el cambio de los días en casa; el perfil de puesto debe admitir días en casa (TELE_APTO).

### 4.2 Confidencialidad
1. Cláusula base reforzada en el contrato para todas las personas trabajadoras.
2. Conductas y consecuencias en el RIT (conductas 36, 39, 56 y 58 del Anexo A del RIT, corregido el 12/11/2026; deben coincidir con el contrato y con la definición de reproducción y extracción del convenio).
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

**Aviso de privacidad para personas trabajadoras**
- Formato fijo que lista todos los datos que la Empresa puede tratar, con la mención «cuando se utilicen» (documento migratorio, biométricos, ubicación, audio y registros de uso de las herramientas de trabajo). Sin módulos ni versiones distintas por cliente.
- Comunicación de datos a terceros genérica, remitida a las excepciones de la ley; sin destinatarios específicos. Por eso no se agrega una remisión específica a la STPS vía SIRCE.
- Variables mínimas: datos de la Empresa, AVISO_CORREO_DATOS y datos de firma. Se eliminaron las de puestos con acceso a grabaciones, áreas con cámara y plazos de conservación.
- Una sola firma de acuse y consentimiento expreso para datos sensibles y financieros, y una sola finalidad voluntaria (uso de imagen).
- (26/10/2026, aprobada; sustituye la decisión anterior del kit) La **ubicación** se trata sin opción de negarse, con fundamento en la relación de trabajo y el registro de jornada. Los **biométricos** requieren consentimiento expreso, libre e independiente, con casilla propia en el apartado 10 del aviso, y medio alterno (PIN o tarjeta) también por falla del sistema. El aviso de privacidad y el Anexo 3 del contrato deben decir lo mismo.
- (26/10/2026, provisional) El aviso de candidatos es un documento propio del reclutamiento, separado del aviso de personas trabajadoras. Formato fijo, sin módulos ni listas de puestos: psicométricos, antecedentes y estudio socioeconómico solo «cuando la naturaleza del puesto lo justifique»; comunicación de datos genérica; tres casillas (salud, datos patrimoniales y bolsa de trabajo); aviso simplificado para vacantes en línea; nombre y fecha del candidato a mano. Variables nuevas: AVISO_URL, CAND_PLAZO_CONSERVACION y CAND_PLAZO_BOLSA.
- (31/10/2026) **La versión vigente del kit es la del paquete integrado (visor v9), no el visor v6**, que conserva tres diferencias: casilla de biométricos del aviso, condición del acta de devolución y omisión del perfil con Lista de actividades. Versión anterior: visor v6 (https://claude.ai/artifact/3EDzdAW3oyfGXoTXDjrvh3). Variables y dependencias en «Kit de contratación - Variables y dependencias» (55 variables, extraídas del texto). La carta responsiva, inciso d), remite al documento de asignación de correo institucional.

**Carta responsiva**
- (26/10/2026) Se genera también cuando solo hay herramientas digitales: correo institucional o sistemas asignados al puesto, y cuando hay días en casa (teletrabajo o híbrido).
- (26/10/2026) El correo institucional se menciona como «asignado por la Empresa», sin remitir al Anexo 3 del contrato. El Anexo 3 solo contiene el acuse de políticas y la aceptación del registro de asistencia; el usuario lo unificará con el kit.
- Cubre herramientas físicas y digitales: titularidad de cuentas y contenidos, uso exclusivamente laboral, credenciales (lo realizado con ellas se presume hecho por la Persona Trabajadora, salvo prueba en contrario o reporte previo de pérdida o compromiso), prohibiciones de extracción, registros de actividad como prueba, dispositivos personales, entrega de contraseñas y prohibición de borrar información antes de la salida.
- (26/10/2026, provisional) La responsabilidad por dolo o negligencia se acredita mediante el procedimiento del RIT (art. 46). (12/11/2026) El art. 46 ya no menciona la autorización previa: la carta responsiva debe contenerla, junto con el valor de reposición de cada bien (ver 4.4).
- (26/10/2026, aprobada; sustituye la prohibición de compensar) Una sola regla de descuento por pérdida o daño: procede solo si el Comité determina la negligencia con audiencia, existe la autorización previa firmada en el resguardo y se respetan los límites legales. La carta responsiva remite al art. 46 del RIT.
- (26/10/2026, provisional) El mantenimiento y la reposición de las herramientas corresponden a la Empresa.

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
- (31/10/2026, aprobada) Art. 79 y Anexo C: el Comité de Integridad y Disciplina se integra por puestos (titular o suplente). Art. 4 y Anexo D: ubicación de las políticas internas. Ambos anexos opcionales.
- (31/10/2026, aprobada) Art. 75: la prohibición de publicar información confidencial incluye la operativa y la laboral. Riesgo (libertad sindical y de expresión) explicado una vez; se mantiene.
- (31/10/2026, provisional) Art. 9: con REPSE_EMPRESA = Sí, el traslado durante la jornada es tiempo de trabajo; si la prolonga, aplican los arts. 17 y 18; la Empresa cubre los gastos de los traslados que ordene.
- (31/10/2026, provisional) Formatos FD-1 a FD-5: citatorio de 1 a 5 días hábiles; reprogramación una sola vez; medida provisional con goce de salario; FD-3 puede proponer la rescisión a RESCISION_RESPONSABLE; FD-5 toma el bien del resguardo y sin resguardo con valor de reposición no hay descuento; negativa a firmar con dos testigos y envío al correo personal. El aviso de rescisión es documento aparte del módulo 4.

- (31/10/2026, aprobada) Crear o cambiar una jornada del catálogo obliga a depositar de nuevo el Anexo B. El cambio aplica a las altas nuevas; al personal vigente se le genera comunicado o convenio (módulo 5). La reducción legal de jornada no requiere depósito (art. 8).
- (31/10/2026, aprobada) Cambiar los puestos del Comité (Anexo C), la ubicación de las políticas (Anexo D) o el catálogo de jornadas genera la alerta «RIT modificado: pendiente de depósito». No se bloquea la constancia FR-1: mientras no se deposite la versión nueva, se sigue entregando la del RIT vigente. Cambiar a la persona que ocupa un puesto no modifica el RIT.
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

**Firma del RIT y de la FR-1 (13/11/2026, decisión del usuario; resuelve la contradicción entre la especificación del RIT, el paquete de contratación y firma electrónica)**
- Los documentos necesarios para el depósito del RIT ante el CFCRL (el RIT firmado por la Comisión Mixta y el acta de integración de la CMRIT) se firman de forma autógrafa.
- La FR-1, que se genera ya con el RIT depositado y acredita la entrega a cada persona, se firma en sus tres momentos (emisión, ingreso y modificación) con la misma modalidad que los documentos de contratación de esa persona (FIRMA_MODALIDAD). Es autógrafa solo cuando la persona firma en papel, cuando falla la Plataforma o cuando se niega a firmar (dos testigos y envío al correo personal).
- Por la Empresa firma el representante al ingreso, dentro del paquete de contratación, y la persona de RH designada (FIRMANTES_EMPRESA) en la emisión y en la modificación.
- FR1_MEDIO (papel o enlace) solo indica cómo se entrega el ejemplar del RIT; no determina la forma de firma.
- Con el RIT depositado, la FR-1 sustituye a la fila RIT_ENTREGA del Anexo 3 del contrato, que solo se genera si el RIT no está depositado (decisión del paquete de contratación, 13/11/2026).

### 4.5 Comisión Mixta del RIT
- Acta de integración y estatutos fusionados en un solo instrumento.
- (31/10/2026) Número de representantes: NUM_REPRESENTANTES_POR_PARTE (mínimo 1). La falta de acuerdo se asienta y sigue aplicándose el texto vigente.
- Se redacta como designación de integrantes, sin documentar elecciones ni votaciones, con la conformidad de las personas trabajadoras.
- (02/11/2026, aprobada; sustituye el criterio del 26/10) **Criterio común de las tres comisiones (RIT, capacitación y PTU): en ninguna hay votación secreta.** Por omisión, las personas trabajadoras designan a su representación; el documento hace constar la designación, la aceptación de los representantes y que la Empresa no intervino. Refuerzo opcional: relación de conformidad firmada (CONFORMIDAD_FIRMAS). Elección formal opcional (DESIGNACION_OBRERA = Elección), sin voto secreto, en una jornada común con D-01 y D-02 del kit de PTU. Con sindicato, la designa el sindicato. El usuario no obliga al cliente a celebrar elecciones ni a conservar sus evidencias; riesgo explicado una vez, se mantiene.
- (02/11/2026) Variables comunes de las tres: DESIGNACION_OBRERA (sustituye a CMRIT_INTEGRACION_MODO), NUM_REPRESENTANTES_POR_PARTE (mínimo 1) y REPRESENTANTES_SUPLENTES (Sí por omisión). El personal de confianza participa pero no puede ser representante. Una persona puede representar en más de una comisión.
- Los firmantes alimentan la tabla de firmas del RIT. El RIT solo toma del acta FECHA_ACTA_INTEGRACION y los representantes.
- (12/11/2026) El acta de la CMRIT todavía no aplica el criterio común: sigue con CMRIT_INTEGRACION_MODO en lugar de DESIGNACION_OBRERA (encargo 7 del mapa, abierto).

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

### 4.8 Terminación y precálculo de finiquito (26 y 27/10/2026)

Documento de referencia: «AXIARH - Modulo 4 - Especificacion para programacion» (v1.0, 27/10/2026), en el proyecto. Texto legal verificado en la LFT vigente (última reforma DOF 14-05-2026); los arts. 162, 486, 501, 503 y 517 se cotejaron en compilación no oficial y quedan por confirmar.

**Paquete documental**
- (26/10/2026, decisión del usuario) En toda terminación se generan el convenio de terminación y finiquito y el recibo de finiquito con desglose, además del documento propio de la causa. El convenio es un solo modelo con módulos A, B, C, D, E y E-bis; el pago a beneficiarios es su variante por fallecimiento.
- (26/10/2026, aprobada) No se genera formato de renuncia: la salida voluntaria se documenta con el convenio, módulo B. Si la Persona Trabajadora entrega carta propia, se carga como evidencia (CARTA_PROPIA). Fundamento: 2a./J. 14/2023 (11a.).
- (26/10/2026) Del convenio de referencia se eliminaron la renuncia a acciones penales, administrativas y de seguridad social, el deslinde total, la cláusula que impedía reclamar diferencias por fecha, la jurisdicción convencional, la vigencia indefinida y la mención del embarazo. Se conserva la divisibilidad.
- (27/10/2026, decisión del usuario) Sin pena por retraso en pago diferido ni obligación de ratificar en un plazo. Con el servicio de ratificación contratado, el sistema solo genera una hoja de datos para la solicitud.
- (26/10/2026) El recibo se firma siempre de forma autógrafa, aun con FIRMA_MODALIDAD = Electrónica, y remite al CFDI de nómina; contiene solo el «recibí» de los conceptos desglosados.
- (26/10/2026) El escenario de negociación nunca se imprime en los documentos de la baja; solo en pantalla y en una hoja interna con la leyenda «Escenario interno para la toma de decisiones. No constituye reconocimiento de adeudo ni de despido».

**Motivos de baja**
- (26/10/2026, provisional) La pantalla pregunta primero quién decide la salida (BAJA_DECIDE) y solo muestra motivos legales: voluntad de la Persona Trabajadora, rescisión por causa imputable a la Empresa (arts. 51 y 52), mutuo consentimiento, rescisión por causa imputable a la Persona Trabajadora (art. 47), fin del periodo de prueba o capacitación, vencimiento de plazo u obra, fallecimiento e incapacidad (art. 54). No existe «despido injustificado».
- (26/10/2026, provisional) Si decide la Empresa sin causa del art. 47 ni vencimiento, solo se ofrece el mutuo consentimiento.
- (26/10/2026, provisional) Situaciones protegidas (embarazo o lactancia informados, incapacidad temporal en curso, Declaración Especial de Ausencia, representante obrero en funciones) bloquean rescisión, fin del periodo y mutuo consentimiento hasta la revisión de consultoría. El dato nunca se imprime.
- (12/11/2026, provisional; del módulo de permisos) Se agrega a las situaciones protegidas la licencia del IMSS por hijo con cáncer vigente (evento B3).
- (12/11/2026, provisional) Con una comisión permanente vigente (evento B4) la baja no se bloquea: el sistema avisa del derecho a regresar dentro del plazo legal y pide doble confirmación, con registro de quién confirma (BAJA_CONFIRMACION_B4, evento de baja, Sí/No).
- (12/11/2026, provisional) Suspensión por falta de documentos (evento D4): vencido el plazo legal sin regularizar, se actualiza la causa del art. 47, fr. XIV Bis; consultoría decide y prepara el aviso de rescisión con SUS-2 como antecedente. El sistema no termina la relación.
- (26/10/2026) Temporada: el fin de temporada suspende la relación (arts. 39-F y 42, fr. VIII); no se ofrece el motivo de vencimiento.

**Precálculo**
- (26/10/2026) Escenario de negociación en capas: finiquito; indemnización de 90 días de salario integrado; 20 días por año (o art. 50, fr. I) solo con un supuesto del art. 49 o en la rescisión del art. 52; y como riesgo informativo, salarios vencidos hasta 12 meses e intereses.
- (26/10/2026) En los documentos, el excedente sobre el finiquito se llama «gratificación por terminación» (CONV_GRATIFICACION), salvo en la rescisión del art. 51.
- (26/10/2026, aprobada) Prima de antigüedad obligatoria y bloqueada donde la ley la impone (voluntad con 15 años o más, rescisión por cualquiera de las partes, fallecimiento, art. 54). En mutuo consentimiento, voluntad con menos de 15 años, fin del periodo y vencimiento es opcional (PA_INCLUIR), con registro de quién la marcó. Salario topado al doble del mínimo del área (art. 486).
- (26/10/2026, aprobada) El precálculo es previsualización con umbrales que no bloquean; admite cifras propias con registro. Ningún convenio ni recibo sale en versión final sin la validación del contador (CALCULO_VALIDADO); un cambio de monto revierte la validación. Único bloqueo: neto negativo.
- (26/10/2026) La PTU pendiente no se suma al finiquito; el recibo informa el ejercicio y la fecha estimada. La PTU ya determinada y no pagada sí se suma.
- (26/10/2026) Descuento por daño en el finiquito solo con expediente del Comité concluido (art. 46 del RIT) y dentro del art. 110, fr. I; si no concluye antes del pago, el finiquito se paga completo.

**Servicios que se cobran aparte**
- (26/10/2026, aprobada) Ratificación ante el Centro de Conciliación (RATIFICACION_SERVICIO) y depósito paraprocesal (PARAPROCESAL_SERVICIO). El sistema solo los recomienda con alertas; no bloquean la baja.

**Baja sin firma**
- (26/10/2026, aprobada) Secuencia de alertas desde BAJA_FECHA: día 0 informativa, día 2 preventiva, día 4 crítica y, desde el día 5, cada ALERTA_BAJA_INTERVALO días hábiles con escalamiento a consultoría. Cesan con BAJA_FIRMA_EVIDENCIA o PARAPROCESAL_ACUSE.
- (26/10/2026, aprobada) Rescisión: plazo de 5 días hábiles del art. 47; vencido sin acuse, la alerta cambia a «aviso extemporáneo: se presume el despido injustificado».
- (26/10/2026, aprobada) Mutuo consentimiento sin firma: la relación sigue vigente. Voluntad sin firma ni carta propia: no se registra baja voluntaria; las inasistencias se documentan para la vía del art. 47, fr. X.
- (26/10/2026, aprobada) El finiquito nunca se retiene por falta de firma: se paga por transferencia y el CFDI es la prueba.

**Aviso de rescisión**
- (26/10/2026) Los hechos se toman del expediente disciplinario del RIT. Bloqueo si pasa más de un mes desde el conocimiento (art. 517); solo consultoría desbloquea. Hecho sin evidencia: alerta crítica.
- (26/10/2026) Vigilar la contradicción de criterios 165/2025 de la SCJN (proyecto retirado en enero de 2026).

**Pago a beneficiarios**
- (26/10/2026, provisional) Ruta por designación (vigente, confirmada en los últimos 12 meses, sin controversia y total menor que BENEF_UMBRAL) o ruta Tribunal. Solo el pago por resolución del Tribunal libera a la Empresa frente a terceros (art. 503, fr. VII). El pago por designación nunca en efectivo.

**Acta de devolución**
- (26/10/2026) No condiciona el pago; faltantes y daños van al Comité del RIT; cierre de accesos a más tardar el día hábil siguiente a la baja (en rescisión, al entregar el aviso); requerimiento por correo si la persona no se presenta; el acta se levanta en la fecha del convenio o dentro de 3 días hábiles.

### 4.9 Permisos y licencias (12/11/2026)

Documento de referencia: «AXIARH - Módulo de permisos y licencias - Especificación para programación» (v1.4). Las decisiones del módulo están en «Corte - Módulo de permisos y licencias»; aquí solo se registran las que tocan otros documentos.
- (12/11/2026) Conversación propia, separada del RIT. El RIT es la fuente de las reglas; el módulo las ejecuta.
- (12/11/2026) Fuente única: el evento es la única fuente de ausencias para nómina, IMSS, PTU, vacaciones, finiquito y análisis de jornada; ningún otro módulo captura ausencias.
- (12/11/2026) Catálogo de 18 eventos en cuatro familias: A permisos, B licencias, C incapacidades del IMSS y D suspensiones del art. 42. Lo que no encaja es falta y va por la vía disciplinaria del RIT.
- (12/11/2026) Los registros digitales SP-1, SUS-3 y el acuse de LIC-2 se apoyan en el «Corte - Firma electrónica» y en la cláusula de formalización por medios electrónicos del contrato.
- (12/11/2026, decisión del usuario) No se crea TRIBUNAL_COMPETENTE en el alta de la empresa. El art. 504, fr. V LFT (cotejado con el texto vigente) exige dar el aviso de accidente también al Tribunal, por lo que INC-1 lo menciona con texto fijo, sin variable. (12/11/2026) Aplicado en la especificación v1.4; TRIBUNAL_COMPETENTE eliminada.
- (12/11/2026, decisión del usuario) **Cadena de autorización.** Los permisos que otorga la Ley (A1, A2, A3, B2), los permisos de la Empresa (A4) y la licencia sin goce (B5) se autorizan por jefatura inmediata (PERSONA_JEFATURA), RH y dirección del área (DIRECTOR_AREA) si existe. El representante legal no interviene. Cadena por omisión en CADENA_AUTORIZACION (empresa); cada concepto de PERMISOS_EMPRESA puede tener una más corta, con RH siempre como paso (B5, siempre completa). Nadie autoriza su propio permiso; quien ocupa dos pasos autoriza una vez. Cada paso tiene AUTORIZACION_PLAZO_DIAS días hábiles (1 por omisión); la falta de respuesta no es autorización y RH puede reasignar a un suplente. Si llega la fecha sin resolución y la solicitud se hizo a tiempo, RH resuelve ese día y la ausencia no es falta.
- (12/11/2026, decisión del usuario) **Permisos que otorga la Ley:** pasan por la cadena, pero no pueden negarse (art. 132, frs. IX, X y XXVII Bis, y art. 170 LFT). La cadena solo verifica datos, aviso y evidencia y puede «Devolver para corrección» (DEVOLUCION_MOTIVO); en A3 solo puede limitar el número de comisionados. Si llega la fecha sin autorización completa, RH lo registra y la ausencia nunca es falta. Licencias, incapacidades y suspensiones (B1, B3, B4, C y D) no pasan por la cadena: RH registra y la jefatura y la dirección reciben aviso.
- (12/11/2026) Negativa de permisos de la Empresa: solo por las causas del art. 33 del RIT (NEGATIVA_CAUSA: requisitos no subsanados o necesidad operativa concreta).
- (12/11/2026, decisión del usuario) **Firma de la Empresa:** en LIC-1, LIC-3, INC-2, SUS-1 y SUS-2 firma la persona de RH que la Empresa designe (FIRMANTES_EMPRESA, configuración de la empresa), solo entre puestos con funciones de dirección o administración, con usuario y código de un solo uso. El representante legal solo firma INC-1, con e.firma o de forma autógrafa. FIRMA_EMPRESA_NOMBRE y FIRMA_EMPRESA_CARGO pasan a derivarse del firmante designado. Mientras la especificación de firma electrónica no prevea este firmante, RH firma esos documentos de forma autógrafa.
- (12/11/2026) Contradicción abierta con el RIT: el art. 30 dice que los permisos legales no requieren autorización y RH los registra; el art. 16 y la fila de asuntos personales de la tabla II dependen solo de la jefatura. Mientras el RIT depositado no cambie, la cadena de los permisos legales opera como verificación interna y nunca como condición del permiso (encargo en el mapa).

---

## 5. Reglas del formulario y del sistema

### 5.1 Alta de la persona trabajadora
- Nombre y domicilio por campos separados.
- CURP de 18 caracteres con dígito verificador. Edad y sexo se toman de la CURP.
- RFC prellenado con la CURP; el usuario agrega la homoclave.
- Correo personal obligatorio. El correo institucional es una casilla que genera su documento de asignación.
- Sin jefe inmediato, clasificación, atributo de dirección, trabajo material, lugar de pago, forma de pago, propiedad intelectual ni campos editables del perfil de puesto: todo eso viene de la empresa o del organigrama.
- Fecha de inicio vacía y obligatoria.
- (Actualizado 26/10/2026) La periodicidad de pago no se captura en el alta: viene del perfil de puestos. Días de pago calculados.
- (26/10/2026) El salario tampoco se captura en el alta: es un monto fijo por puesto.
- Días en casa con casillas de días de la semana; el sistema calcula el porcentaje y el módulo: T (TELETRABAJO_ACTIVO, más de 40%) o H (HIBRIDO_ACTIVO, de 1 a 40%). (26/10/2026) La casilla se rotula «¿Trabaja días en casa?».
- La pregunta REPSE solo aparece si la empresa tiene folio. Sin datos de supervisores. (26/10/2026) Con REPSE = Sí, el alta captura el lugar de trabajo (Empresa o Cliente); solo con Cliente se capturan los datos del cliente y de la asignación (los del oficio de asignación). El contrato no lleva los datos del servicio especializado por persona: la declaración lista todas las actividades registradas de la Empresa.
- (26/10/2026) El equipo asignado se captura como tabla (EQUIPO_DESCRIPCION: descripción, marca y modelo, serie o identificador, estado), una fila por bien.
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
| Variante de comida dentro del centro | El puesto no permite salir a comer |
| Cláusula de firma electrónica en cada documento del kit | FIRMA_MODALIDAD = Electrónica |
| Juego de la Comisión Mixta de Capacitación | PLANTILLA_NUM > 50, o se usa periodo de prueba o capacitación inicial (MOD_PRUEBA) |
| Variante sindical (oficio de designación) de las comisiones de capacitación y PTU | SINDICATO = Sí |
| Módulo A, B o C del dictamen de PTU | RESULTADO, derivado de la renta gravable y de la excepción legal |

### 5.5 Baja de la persona trabajadora (27/10/2026)

| Alerta | Plazo | Fundamento |
|---|---|---|
| Baja ante el IMSS | No más de 5 días hábiles | Art. 15, fr. I LSS |
| Aviso al juzgado y a acreedores alimentarios | 5 días hábiles siguientes a la terminación | Art. 110, fr. V LFT |
| Aviso de rescisión por el Tribunal | 5 días hábiles | Art. 47 LFT |
| Prescripción para rescindir | Un mes desde el día siguiente al conocimiento | Art. 517, fr. I LFT |
| Constancia de servicios | 3 días, si se solicita | Art. 132, fr. VIII LFT |
| Baja ante Fonacot e Infonavit | Configurable mientras se verifica | Pendiente |
| Alta ante el IMSS desde el primer día del periodo de prueba o capacitación | Al inicio de la relación | Art. 39-C LFT |
| Vencimiento de contrato determinado | 15 días naturales antes; contador de renovaciones desde la segunda | Política |
| Secuencia de baja sin firma | Ver 4.8 | Decisión del usuario |

Datos que faltan en el alta para la baja: TRAB_NSS (necesario para la baja, no bloquea el contrato); pensión alimenticia (PENSION_ALIMENTICIA, PENSION_AUTORIDAD, PENSION_PORCENTAJE, PENSION_EXPEDIENTE); INFONAVIT_CREDITO y FONACOT_CREDITO; BENEF_CONFIRMACION_FECHA. Variables eliminadas por el módulo 4: RENUNCIA_*, RECIBE_NOMBRE, RECIBE_CARGO, RATIFICACION, RATIFICACION_UMBRAL, RATIF_DIAS y CONV_PENA_DIARIA.

### 5.3 Alertas del periodo (no configurables)

| Modalidad | Evaluaciones | Vencimiento |
|---|---|---|
| Capacitación inicial de 3 meses | Días 30, 60 y 75 | Alertas desde 3 semanas antes, cada vez más críticas |
| Capacitación inicial de 6 meses | Mensuales | Alerta 15 días antes del vencimiento |
| Periodo de prueba | Solo evaluación final | Alertas desde 3 semanas antes, cada vez más críticas |

Candados: el documento de terminación solo se habilita con la evaluación final, la opinión de la Comisión Mixta (formato F-2) o la constancia de que se solicitó oportunamente, y, en capacitación, las constancias de la capacitación impartida. Pasado el vencimiento, queda bloqueado.

### 5.4 Validaciones legales del sistema
- La jornada no puede exceder el máximo del año de la fecha de inicio. Tabla de máximos: 48 horas en 2026, 46 en 2027, 44 en 2028, 42 en 2029 y 40 en 2030, cada cambio el 1 de enero. Falta confirmar con el DOF los máximos de las jornadas nocturna y mixta.
- Si no se puede salir a comer, ese tiempo cuenta como jornada.
- En jornada continua, mínimo 30 minutos de descanso.
- Salario no menor al mínimo de la zona del centro de trabajo.
- No se puede repetir el periodo de prueba ni la capacitación inicial con la misma persona. (31/10/2026) Se amplía a lo que prohíbe el art. 39-D: simultáneo o sucesivo, más de una ocasión, puestos distintos, ascensos y nueva relación con la misma Empresa.
- (26/10/2026) Módulo H: 1 ≤ PORC_TIEMPO_DOMICILIO ≤ 40; con HIBRIDO_ORIGEN = Decisión de la Empresa no se permite HIBRIDO_APOYO_MODO = Sin apoyo (bloqueo).
- (26/10/2026) REPSE: sin folio y vigencia cargados en el perfil de la empresa el módulo R se bloquea. Con REPSE_LUGAR_TIPO = Cliente no se genera el contrato sin el oficio de asignación completo.
- (26/10/2026) Representantes obreros de las comisiones: no pueden tener clasificación Confianza en el organigrama y deben pertenecer a uno de los centros.
- (26/10/2026) PTU: alerta si la copia de la declaración no se entrega dentro de 10 días hábiles; fechas límite de consulta, objeciones, observaciones, resolución y pago calculadas desde FECHA_PRESENTACION; límite de pago según el tipo de persona de la Empresa.

---

## 6. Alcance del PMV de Axia RH (26/10/2026)

- Módulos: kit de contratación; RIT y su comisión mixta; PTU y su procedimiento; terminación y precálculo de finiquito; modificación de condiciones de trabajo; validación de pago de PTU y aguinaldo; comisión mixta de capacitación y SIRCE; Fonacot; análisis de jornada.
- La Comisión Mixta de Capacitación, Adiestramiento y Productividad entra al PMV.
- El PMV genera todo tipo de contratos laborales, no solo por tiempo indeterminado.
- La PTU se calcula importando la nómina o capturando datos por persona (días trabajados y salario devengado).
- El finiquito se precalcula bruto, antes de impuestos y deducciones.
- (26/10/2026) La capacitación inicial es solo una cláusula del contrato, no un contrato autónomo.
- (26/10/2026) De capacitación, Axia RH solo cubre el SIRCE, la Comisión Mixta de Capacitación, Adiestramiento y Productividad y el DC-1. Lo demás (DNC, plan y programa, cursos) queda para Axia Capacitación.
- (26/10/2026) La constancia DC-3 no entra a Axia RH. Para terminar la capacitación inicial, el sistema exige que se cargue la evidencia de la capacitación impartida (DC-3 u otra constancia generada fuera de Axia RH).
- (26/10/2026) Fonacot: el PMV solo alerta y guarda evidencia; no calcula retenciones.
- (26/10/2026) Análisis de jornada: los datos salen del archivo del reloj checador del cliente.
- (26/10/2026) Acta formal de devolución y entrega de herramientas a la salida, como documento propio del módulo de terminación.
- (26/10/2026) Los documentos que recibe el cliente no llevan «AEXIS» ni «AXIARH». El logo del cliente se ofrece en otro nivel de servicio.
- El detalle de faltantes, dependencias y contradicciones está en «Axia RH - Mapa del PMV».

---

## 7. Pendientes

- [ ] Confirmar si la cláusula base de confidencialidad incluye el pacto de titularidad de obras (art. 84 LFDA).
- [ ] Confirmar con el texto del DOF los máximos de las jornadas nocturna y mixta en la reducción gradual.
- [ ] Definir con cada cliente el apoyo para gastos de teletrabajo y los medios de contacto.
- [ ] Decidir si las prestaciones superiores se configuran por empresa o por puesto o nivel.
- [ ] Redactar: adenda de confidencialidad, constancia de recibo del RIT, asignación de correo institucional. (Constancias del RIT, formatos disciplinarios, terminación al vencer el periodo y recibo de PTU ya están en borrador.)
- [ ] Integrar al contrato maestro las cláusulas ajustadas por el layout (notificaciones, jornada, lugar de trabajo, REPSE, teletrabajo, prestaciones, perfil de puesto). La integración de jornada, teletrabajo y REPSE ya se hizo el 26/10/2026; falta la revisión final.
- [x] (26/10/2026) Cerrado: variantes B, C y D incorporadas; paquete de contratación cerrado y diccionario de variables generado.
- [ ] (31/10/2026) Paquete de contratación: dar de alta en el formulario las 12 variables sin estructura (CANAL_AVISO_AUSENCIA, MEDIO_ENTREGA_RECIBOS, JORNADA_ID, CLIENTE_ACTIVIDAD_REPSE, REPSE_ACT_DESCRIPCION, REPSE_ACT_NUMERO, MODULO_REVISION_FECHA, MODULO_REVISION_MESES, TELE_APTO, TELE_AUTORIZACION_FECHA, TELE_AUTORIZACION_ORGANO, TELE_SOLICITUD_FECHA); verificar la LFPDPPP 2025; quitar la nota «por verificar» del módulo R; corregir formato de encabezados 3.1 y 3.3; diseñar el paquete de prestaciones extralegales.
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
- [ ] (12/11/2026) Diccionario único: distinguir DIAS_EN_CASA_EMPRESA (empresa, RIT) de DIAS_EN_CASA_ACTIVO (alta, contrato); PERSONA_JEFATURA es la jefatura inmediata y DIRECTOR_AREA la dirección del área, ambas por puesto (se elimina JEFE_INMEDIATO); FIRMANTES_EMPRESA va en la configuración de la empresa; CENTRO_TRABAJO (módulo de permisos) equivale a PERSONA_CENTRO (RIT) y debe quedar un solo nombre.
- [ ] (26/10/2026) Comisión de capacitación: verificar en la fuente oficial los arts. 39-A, 39-B, 153-D y 183 LFT; confirmar que no haya un acuerdo de la STPS posterior a abril de 2025 que modifique los formatos DC-1, DC-2 o DC-3; buscar criterios judiciales sobre procedimientos disciplinarios internos autoimpuestos; fijar valores por defecto de PERIODO_CARGO, PERIODICIDAD, ANOS_CONSERVACION, DIAS_OBJECION y DIAS_RESOLUCION.
- [ ] (02/11/2026) PTU: verificar el tratamiento del excedente por el tope individual (art. 127, fr. VIII) y el art. 122 LFT; agregar AUTORIDAD_INSPECCION al alta de la empresa. Recibo individual y control de PTU no cobrada: redactados.
- [ ] (26/10/2026) Kit: comprobar que el aviso cumple el contenido mínimo del art. 15 de la LFPDPPP 2025 (el reglamento nuevo no se ha publicado); revisar el aviso para candidatos con los mismos criterios; unificar el Anexo 3 del contrato con el kit.
