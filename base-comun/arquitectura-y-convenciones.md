# Base común de la familia Axia

Generado automáticamente a partir de `axia-rh/registro-de-decisiones.md` (versión del 13 de noviembre de 2026). **No se edita a mano**: cualquier cambio se hace en el registro de Axia RH y Cerebro vuelve a generar este archivo.

Contiene la arquitectura del sistema (niveles de captura y atributos de puesto) y las convenciones de redacción que comparten todos los productos Axia. Un proyecto distinto de Axia RH que necesite una variable nueva de empresa, organigrama o alta la pide como encargo a Cerebro.

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
