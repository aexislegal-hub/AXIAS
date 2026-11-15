# Registro de decisiones — Axia NOMs

Lo escribe solo el Cerebro de Axia NOMs. Creado el 15/11/2026.

La arquitectura general (niveles de captura, atributos de puesto) y las convenciones de redacción **no se repiten aquí**: rigen las de `base-comun/arquitectura-y-convenciones.md`. Este registro solo contiene lo propio de la línea.

Estados: **provisional** (decisión tomada en conversación, sujeta a revisión final), **aprobada** (el usuario la aprobó expresamente; sigue siendo revisable en la revisión final), **propuesta** (planteada por Cerebro, sin decisión del usuario).

---

## 1. Catálogo de documentos y módulos

| Módulo / documento | NOM | Se activa cuando | Estado |
|---|---|---|---|
| Módulo NOM-035: aplicación en línea de las Guías I, II o III y V, calificación, análisis individual y por centro, borrador del programa de intervención, informe y difusión | NOM-035-STPS-2018 | Todo centro de trabajo; la guía depende del tramo del centro (NOM035_TRAMO) | Arquitectura cerrada (provisional). Falta la especificación funcional |
| Aviso de privacidad para la evaluación de factores de riesgo psicosocial | NOM-035-STPS-2018 / LFPDPPP | Cada evaluación | Borrador, pendiente de revisión del usuario |
| Política de prevención de riesgos psicosociales | NOM-035 (5.1) | Todo centro | La desarrolla Axia Compliance en coordinación con esta línea |
| Contrato de prestación de servicios AEXIS–cliente (encargo de datos, respaldo, confidencialidad, devolución) | — | Servicio de acompañamiento | Otra conversación; sin iniciar |
| Módulo NOM-019: comisión de seguridad e higiene | NOM-019-STPS-2011 | Todo centro (la NOM distingue por número de personas trabajadoras; tramos por confirmar en su conversación) | Por diseñar. Salió de Axia RH el 26/10/2026 |
| Módulo NOM-030: responsable de seguridad y salud, diagnóstico y programa | NOM-030-STPS-2009 | Todo centro | Por diseñar. La NOM-035 se integra a su diagnóstico |
| Resto del catálogo | Ver `mapa.md`, apartado 2 | — | Propuesto el 15/11/2026, sin aprobar |

---

## 2. Arquitectura propia de la línea

Remite a la base común para los niveles 1 a 3 y los eventos. Aquí solo lo que agrega Axia NOMs.

- (15/11/2026, propuesta) **Unidad de cumplimiento: el centro de trabajo.** Toda obligación se evalúa por centro (los de la configuración de la empresa de Axia RH, incluidas las instalaciones del catálogo de clientes REPSE cuando ahí se prestan servicios). El sistema solo exige a cada centro lo que su perfil activa.
- (15/11/2026, propuesta) **Matriz de obligaciones.** Cada NOM se carga como filas de una tabla del sistema: NOM y numeral; fuente (NOM, Reglamento Federal de Seguridad y Salud en el Trabajo o LFT); tipo (obligación, buena práctica o medida estratégica); condición de activación; responsable; plazo o periodicidad; evidencia que acredita el cumplimiento; quién puede elaborarla o validarla; alerta. Los plazos y periodicidades viven en la tabla con fecha de vigencia, no en los textos (misma regla que las cifras de la base común).
- (15/11/2026, propuesta) **Motor de aplicabilidad.** Un cuestionario por centro (actividades, procesos, maquinaria, sustancias, agentes físicos, teletrabajo, personas con discapacidad, etc.) determina qué NOMs y qué filas de la matriz aplican. Equivale funcionalmente al ASINOM de la STPS, pero alimenta la matriz. Se diseña junto con el diagnóstico de la NOM-030. Nivel de captura: pendiente de decisión (mapa, contradicción C1).
- (15/11/2026, propuesta) **Estudios técnicos de terceros.** Donde la NOM exige reconocimiento, evaluación o estudios por laboratorio o unidad de verificación (ruido, iluminación, químicos, condiciones térmicas, vibraciones, etc.), el sistema no genera el estudio: registra el estudio, su fecha, vigencia, quién lo hizo y su acreditación, y alerta su renovación.
- (15/11/2026, regla del proyecto) Cada obligación se clasifica como obligación de la NOM (con numeral), del Reglamento o de la LFT, buena práctica o medida estratégica. Ninguna recomendación se presenta como obligación.

---

## 3. Decisiones por NOM

### 3.1 NOM-035-STPS-2018 (factores de riesgo psicosocial)

Fuente del corte: «Corte - Módulo NOM-035», 10/11/2026, actualización 6 (copia en `cortes/`). Fuentes verificadas en el corte: NOM-035, edición impresa del DOF del 23/10/2018; LFPDPPP, última reforma DOF 14-11-2025.

| Fecha | Decisión | Estado |
|---|---|---|
| 10/11/2026 | Tres niveles de acceso: responsable de la evaluación (ficha individual completa); RH (solo lo necesario para actuar); jefaturas y dirección (solo agregados con el mínimo de respuestas) | Provisional |
| 10/11/2026 | Respuestas identificadas por persona, sin modo anónimo. AEXIS acompaña el servicio: recibe todos los resultados, conserva respaldo y decide a qué personas del cliente se envían | Provisional |
| 10/11/2026 | Censo por omisión; muestra como opción solo en centros de más de 50 personas (7.1 a) | Provisional |
| 10/11/2026 | Tamaño mínimo de grupo para reportes agregados: 5 respuestas (NOM035_GRUPO_MIN) | Provisional |
| 10/11/2026 | El programa lo valida AEXIS o un profesional de la salud del cliente, si lo hay. Sin profesional, las acciones de tercer nivel se redactan como canalización (8.5 c y 5.6) | Provisional |
| 10/11/2026 | Bitácora de envíos con destinatarios de nombre y correo abiertos; envíos externos con medio «Externo» y evidencia opcional | Provisional |
| 10/11/2026 | Guía I positiva: aviso «requiere valoración clínica» (sin respuestas) al contacto de canalización del cliente y al correo de alertas de AEXIS; el cliente marca «canalizado» con fecha y destino; recordatorio a los NOM035_DIAS_CANALIZACION días | Provisional |
| 10/11/2026 | Programa de intervención obligatorio si al menos un cuestionario del centro resulta medio, alto o muy alto (lectura literal de II.4 y III.4); su alcance puede limitarse a las áreas o personas afectadas (8.4 a) | Provisional |
| 10/11/2026 | Resultado del centro con dos indicadores: distribución por nivel (principal) y promedio calificado con los mismos puntos de corte (complementario); el informe declara el método (7.7 d) | Provisional |
| 10/11/2026 | Preguntas condicionadas: con «No» en la pregunta filtro se saltan y valen 0; se declara en el método | Provisional |
| 10/11/2026 | Se retira la alerta de incongruencia entre la pregunta filtro y el organigrama | Provisional |
| 10/11/2026 | Uso exclusivo de los resultados individuales para la mejora del ambiente de trabajo; nunca para selección, desempeño, disciplina ni terminación | Provisional |
| 10/11/2026 | Datos de la Guía V que no tiene el sistema: los llena la persona trabajadora, se guardan en su expediente y se precargan en la siguiente evaluación (encargo a Axia RH) | Provisional |
| 10/11/2026 | Aviso de privacidad específico de la evaluación, separado del aviso de personas trabajadoras (que no se modifica). Lo emite el cliente como responsable; AEXIS es persona encargada y no se nombra. Consentimiento expreso con casilla al inicio (art. 8 LFPDPPP); funda además el tratamiento en la NOM-035 y la relación de trabajo (art. 9, fr. I y IV). Negativa: no avanza, constancia de negativa y alerta a AEXIS; la aceptación posterior, con acceso vigente, deja sin efecto la negativa. Sin abrir el acceso: registro «no contestó», sin constancia | **Aprobada** |
| 10/11/2026 | El contrato de prestación de servicios AEXIS–cliente se trabaja en otra conversación | Provisional |
| 10/11/2026 | Resuelta la contradicción sobre el acceso del psicólogo del cliente | Provisional |

### 3.2 NOM-019-STPS-2011 (comisiones de seguridad e higiene)

| Fecha | Decisión | Estado |
|---|---|---|
| 26/10/2026 | La comisión de seguridad e higiene y su alerta salen de Axia RH (registro de Axia RH, sección 2) y pasan a esta línea | Aprobada (en Axia RH) |
| 15/11/2026 | La NOM-035 menciona la comisión en 6.4 y 6.5; se resuelve en el módulo NOM-019, no en el de la NOM-035 | Provisional |

### 3.3 NOM-030-STPS-2009 (servicios preventivos)

| Fecha | Decisión | Estado |
|---|---|---|
| 10/11/2026 | La NOM-035 se integra al diagnóstico de la NOM-030 (7.6 del corte de la NOM-035) | Provisional |

---

## 4. Reglas del sistema

- (10/11/2026, provisional) NOM035_TRAMO se calcula por centro: ≤15 / 16-50 / >50. Determina la guía aplicable y si se permite muestra.
- (10/11/2026, provisional) Muestra (solo TRAMO >50): n = 0.9604·N / (0.0025·(N−1) + 0.9604), redondeo hacia arriba; selección aleatoria proporcional por sexo.
- (10/11/2026, provisional) NOM035_PERIODO_MESES no puede ser mayor de 24. NOM035_GRUPO_MIN no puede ser menor de 5.
- (10/11/2026, provisional) Sin aceptación del aviso (NOM035_AVISO_ACEPTADO = Sí) no se habilita el cuestionario.
- (10/11/2026, provisional) NOM035_CONSERVACION_ANOS es obligatoria y no tiene valor por omisión hasta que exista la tabla de conservación de documentos.

---

## 5. Variables de la línea

Nivel según la base común. Las marcadas «encargo» pertenecen a Axia RH y están pedidas en `encargos-para-axia-rh.md`; las marcadas «nivel en revisión» dependen de la contradicción C1 del mapa.

| Variable | Nivel | Tipo y validación | Uso | Situación |
|---|---|---|---|---|
| NOM035_RESPONSABLE | Empresa | Tabla: nombre, cédula profesional (opcional), tipo (AEXIS / Profesional de la salud del cliente); obligatoria | Validación del programa | Nivel en revisión |
| NOM035_CANALIZACION_DESTINO | Empresa | Lista: institución de seguridad social / institución privada / médico o psicólogo del centro o de la empresa; obligatoria | Canalización | Nivel en revisión |
| NOM035_CONTACTO_CANALIZACION | Empresa | Tabla: nombre y correo, mínimo 1; obligatoria | Aviso de Guía I positiva | Nivel en revisión |
| NOM035_DIAS_CANALIZACION | Empresa | Entero | Recordatorio | Nivel en revisión |
| NOM035_GRUPO_MIN | Empresa | Entero; 5 por omisión, mínimo 5 | Reportes agregados | Nivel en revisión |
| NOM035_PERIODO_MESES | Empresa | Entero, máximo 24 | Periodicidad | Nivel en revisión |
| NOM035_CONSERVACION_ANOS | Empresa | Entero, obligatoria, sin valor por omisión | Apartado 8 del aviso | Nivel en revisión |
| AEXIS_CORREO_ALERTAS | Plataforma | Correo, obligatoria | Alertas | — |
| NOM035_AVISO_VERSION | Plataforma | Texto | Apartado 11 del aviso, casilla, constancias | — |
| NOM035_TRAMO | Sistema, por centro | ≤15 / 16-50 / >50 | Guía y muestra | — |
| NOM035_AVISO_FECHA_HORA | Sistema, por persona | Fecha y hora | Constancias | — |
| NOM035_INVITACION_FECHAS | Sistema, por persona | Fechas de invitación y recordatorios | Constancia de negativa y «no contestó» | — |
| NOM035_FECHA_CORTE, NOM035_VENTANA_INICIO, NOM035_VENTANA_FIN | Evento | Fechas | Evaluación | — |
| NOM035_MODALIDAD | Evento | Censo / Muestra (solo TRAMO >50) | Evaluación | — |
| NOM035_ACCESO_DIAS | Evento | Entero | Vigencia del acceso | — |
| NOM035_CANALIZADO | Evento, por persona con Guía I positiva | Sí/No, fecha, destino, evidencia opcional | Seguimiento | — |
| NOM035_ENVIOS | Evento | Tabla por envío: fecha, contenido, persona evaluada, medio (Sistema / Externo, obligatorio), evidencia opcional | Bitácora | — |
| NOM035_ENVIO_DESTINATARIOS | Evento, filas por envío (mínimo 1) | Nombre y correo obligatorios; cargo opcional | Bitácora | — |
| NOM035_AVISO_ACEPTADO | Evento, por persona | Sí/No; la aceptación posterior deja sin efecto la negativa | Habilita el cuestionario | — |
| PUESTO_TIPO_NOM035 | Organigrama | Operativo / Supervisor / Profesional o técnico / Gerente | Guía y análisis por tipo de puesto | Encargo pendiente (10/11/2026) |
| TRAB_ESTADO_CIVIL, TRAB_ESCOLARIDAD, TRAB_EXPERIENCIA_LABORAL | Alta (nivel 3), capturados por la persona trabajadora | — | Guía V | Encargo pendiente (10/11/2026) |
| CENTRO_TRABAJO_NOMBRE | Empresa | Nombre por confirmar en el diccionario único | Constancias | Encargo pendiente (10/11/2026) |
| Reutilizadas de Axia RH: PATRON_RAZON_SOCIAL, PATRON_DOMICILIO, AVISO_CORREO_DATOS, TRAB_NOMBRE | — | — | Aviso de la NOM-035 | Existentes |

---

## 6. Fuentes verificadas

| Instrumento | Estado | Dato verificado | Fuente | Verificado |
|---|---|---|---|---|
| NOM-035-STPS-2018 | Vigente | DOF 23/10/2018 | Catálogo de la Secretaría de Economía (PLATIICA); edición impresa del DOF (corte) | 10 y 15/11/2026 |
| NOM-019-STPS-2011 | Vigente | Aplica en todos los centros de trabajo (num. 2) | PLATIICA; texto en el DOF | 15/11/2026 |
| NOM-030-STPS-2009 | Vigente | DOF 22/12/2009; vigor 22/03/2010 | PLATIICA | 15/11/2026 |
| NOM-001-STPS-2008 | Vigente | Aplica en todos los centros de trabajo | Texto publicado en PLATIICA | 15/11/2026 |
| NOM-002-STPS-2010 | Vigente; **en modificación** | Inscrita como NOM vigente a ser modificada en el Suplemento del PNIC 2026 (DOF 26/08/2026), con desarrollo estimado de agosto a diciembre de 2026 | Suplemento del PNIC 2026 (PLATIICA) | 15/11/2026 |
| NOM-017-STPS-2024 | Vigente | DOF 28/03/2025; vigor 28/09/2025; sustituyó a la NOM-017-STPS-2008; aplica donde se requiera EPP | PLATIICA; DOF | 15/11/2026 |
| NOM-006-STPS-2023 | Vigente | DOF 07/03/2024; vigor 03/09/2024; solo manejo con maquinaria | PLATIICA | 15/11/2026 |
| NOM-037-STPS-2023 | Vigente | DOF 08/06/2023 | PLATIICA y fuentes secundarias | 15/11/2026. El umbral del 40% y cómo se mide quedan por confirmar en el texto del DOF |
| Reglamento Federal de Seguridad y Salud en el Trabajo | Vigente según las fuentes consultadas | DOF 13/11/2014 | DOF | 15/11/2026. No encontré reglamento nuevo; confirmar en la conversación de la NOM-030 |

---

## 7. Pendientes

- [ ] Decisión del usuario sobre el nivel de captura de la configuración propia de la línea (mapa, C1).
- [ ] Aprobación del catálogo y del orden de trabajo (mapa, apartados 2 y 7).
- [ ] NOM-035: especificación funcional; revisión del usuario al aviso; verificar en la LFPDPPP las excepciones para comunicar datos a la institución de canalización y a la autoridad; confirmar si la excepción del art. 9 alcanza a los datos sensibles del art. 8 (el reglamento de la ley nueva no se ha publicado); decidir si la persona encargada se nombra en el aviso; revisar la política de prevención del usuario.
- [ ] Tabla de conservación de documentos (transversal): fija NOM035_CONSERVACION_ANOS y las de las demás NOMs.
