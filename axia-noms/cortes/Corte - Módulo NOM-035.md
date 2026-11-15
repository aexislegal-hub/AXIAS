# Corte - Módulo NOM-035 (10/11/2026, actualización 6)

Copia trasladada desde el proyecto de Axia RH el 15/11/2026.

1. DOCUMENTO: Diseño del módulo de la NOM-035-STPS-2018 (aplicación en línea de las Guías I, II o III y V, calificación, análisis individual y por centro de trabajo, borrador del programa de intervención, informe y difusión). Línea Axia NOMs; fuera del alcance del PMV de Axia RH (módulos 1 a 9), pero usa los niveles 1 a 3 de Axia RH. El servicio incluye acompañamiento de AEXIS. Documento del módulo: «Aviso de privacidad para la evaluación de factores de riesgo psicosocial (NOM-035)», borrador, https://claude.ai/artifact/Xmhmi2wAPudwpEe1XjHHnT.

2. ESTADO: Decisiones de arquitectura cerradas (provisionales); aviso específico redactado en borrador, pendiente de revisión del usuario. Fuentes: NOM-035, edición impresa del DOF del 23/10/2018 (vigente según el catálogo de la Secretaría de Economía); LFPDPPP, texto de la Cámara de Diputados con última reforma DOF 14-11-2025 (arts. 2, fr. XII y XX; 7; 8; 9; 15).

3. DECISIONES NUEVAS (no están en el registro; provisionales)
- (10/11/2026) Tres niveles de acceso: responsable de la evaluación (ficha individual completa); RH (solo lo necesario para actuar); jefaturas y dirección (solo agregados con el mínimo de respuestas).
- (10/11/2026) Respuestas identificadas por persona, sin modo anónimo. AEXIS acompaña el servicio: recibe todos los resultados, conserva respaldo y decide a qué personas de la organización cliente se envían, para que el cliente tenga su propio respaldo.
- (10/11/2026) Censo por omisión y muestra como opción, solo en centros de más de 50 personas (num. 7.1 a).
- (10/11/2026) Tamaño mínimo de grupo para reportes agregados: 5 respuestas, donde aplique.
- (10/11/2026) El programa lo valida AEXIS o un profesional de la salud del cliente, si lo hay. Sin profesional, las acciones de tercer nivel se redactan como canalización (8.5 c y 5.6).
- (10/11/2026) Bitácora de envíos con destinatarios de nombre y correo abiertos (uno o varios; cargo opcional). Envíos externos: registro manual con medio «Externo» y evidencia opcional.
- (10/11/2026) Guía I positiva: aviso automático «requiere valoración clínica» (sin respuestas) al contacto de canalización del cliente y al correo de alertas de AEXIS; tablero de AEXIS; el cliente marca «canalizado» con fecha y destino; recordatorio si no lo marca en NOM035_DIAS_CANALIZACION días.
- (10/11/2026) Programa de intervención obligatorio si al menos un cuestionario del centro resulta medio, alto o muy alto (lectura literal de II.4 y III.4); su alcance puede limitarse a las áreas o personas afectadas (8.4 a).
- (10/11/2026) Resultado del centro con dos indicadores: distribución de personas por nivel (principal) y promedio calificado con los mismos puntos de corte (complementario). El informe declara el método (7.7 d).
- (10/11/2026) Preguntas condicionadas: si la persona contesta «No» al filtro, se saltan y valen 0 puntos; se declara en el método.
- (10/11/2026) Se retira la alerta de incongruencia entre la pregunta filtro y el organigrama.
- (10/11/2026) Uso exclusivo de los resultados individuales para la mejora del ambiente de trabajo; no se usan para selección, desempeño, disciplina ni terminación.
- (10/11/2026) Datos de la Guía V que no tiene el sistema: los llena la persona trabajadora y se guardan en su expediente; precarga en la siguiente evaluación.
- (10/11/2026, aprobada) Aviso de privacidad específico de la evaluación, separado del aviso de personas trabajadoras (que no se modifica). Lo emite el cliente como responsable; AEXIS es persona encargada y no se nombra en el texto. Casilla de consentimiento expreso al inicio, dentro del acceso individual (art. 8). Funda además el tratamiento en la NOM-035 y la relación de trabajo (art. 9, fr. I y IV). Si la persona no acepta: no avanza, constancia de negativa y alerta a AEXIS; si después acepta mientras su acceso está vigente, la aceptación deja sin efecto la negativa. Si nunca abre su acceso: registro «no contestó», sin constancia de negativa.
- (10/11/2026) El contrato de prestación de servicios AEXIS–cliente (encargo, respaldo, confidencialidad, devolución) se trabaja en otra conversación.

4. DECISIONES QUE CAMBIAN EL REGISTRO
- Catálogo: agregar el módulo NOM-035 (línea Axia NOMs) y el «Aviso de privacidad para la evaluación de factores de riesgo psicosocial» (borrador).
- Sección 2 (atributos del puesto): agregar PUESTO_TIPO_NOM035.
- Sección 2 (nivel 3): el expediente recibe datos capturados por la persona trabajadora (TRAB_ESTADO_CIVIL, TRAB_ESCOLARIDAD, TRAB_EXPERIENCIA_LABORAL).
- Registro 2 (26/10): «la comisión de seguridad e higiene sale de Axia RH». La NOM-035 la menciona en 6.4 y 6.5; resolver en Axia NOMs (NOM-019).

5. VARIABLES (propuestas)
- NOM035_RESPONSABLE · empresa · tabla: nombre, cédula profesional (opcional), tipo (AEXIS / Profesional de la salud del cliente) · obligatoria.
- NOM035_CANALIZACION_DESTINO · empresa · lista: Institución de seguridad social / Institución privada / Médico o psicólogo del centro o de la empresa · obligatoria.
- NOM035_CONTACTO_CANALIZACION · empresa · tabla: nombre y correo abiertos, mínimo 1 · obligatoria.
- AEXIS_CORREO_ALERTAS · plataforma · correo · obligatoria.
- NOM035_CANALIZADO · evento, por persona con Guía I positiva · Sí/No, fecha, destino, evidencia opcional.
- NOM035_DIAS_CANALIZACION · empresa · entero.
- NOM035_ENVIOS · evento · tabla por envío: fecha, contenido, persona evaluada, medio (Sistema / Externo, obligatorio), evidencia (opcional).
- NOM035_ENVIO_DESTINATARIOS · evento, filas por envío (mínimo 1) · nombre y correo abiertos y obligatorios, cargo opcional.
- NOM035_AVISO_VERSION · plataforma · texto · apartado 11 del aviso, casilla y constancias.
- NOM035_AVISO_ACEPTADO · evento, por persona · Sí/No; la aceptación posterior deja sin efecto la negativa · habilita el cuestionario.
- NOM035_AVISO_FECHA_HORA · sistema, por persona · fecha y hora · constancias. Nueva.
- NOM035_INVITACION_FECHAS · sistema, por persona · fechas de invitación y recordatorios · constancia de negativa y registro «no contestó». Nueva.
- NOM035_CONSERVACION_ANOS · empresa · entero, obligatoria; sin valor por omisión hasta la tabla de conservación · apartado 8 del aviso. Nueva.
- CENTRO_TRABAJO_NOMBRE · empresa · confirmar el nombre en el diccionario · constancias.
- Reutilizadas en el aviso: PATRON_RAZON_SOCIAL, PATRON_DOMICILIO, AVISO_CORREO_DATOS, TRAB_NOMBRE, NOM035_TRAMO, NOM035_GRUPO_MIN, NOM035_FECHA_CORTE.
- NOM035_GRUPO_MIN · empresa · entero, 5 por omisión, mínimo 5.
- NOM035_PERIODO_MESES · empresa · entero, máximo 24.
- NOM035_TRAMO · sistema, por centro · ≤15 / 16-50 / >50.
- NOM035_FECHA_CORTE, NOM035_VENTANA_INICIO, NOM035_VENTANA_FIN · evento · fechas.
- NOM035_MODALIDAD · evento · Censo / Muestra (solo TRAMO >50); n = 0.9604·N / (0.0025·(N−1) + 0.9604), redondeo hacia arriba; selección aleatoria proporcional por sexo.
- NOM035_ACCESO_DIAS · evento · entero.
- PUESTO_TIPO_NOM035 · organigrama · Operativo / Supervisor / Profesional o técnico / Gerente.
- TRAB_ESTADO_CIVIL, TRAB_ESCOLARIDAD, TRAB_EXPERIENCIA_LABORAL · nivel 3, capturados por la persona trabajadora.

6. DEPENDENCIAS
- Aviso de privacidad para personas trabajadoras: sin cambios.
- Contrato de prestación de servicios AEXIS–cliente (otra conversación): encargo, respaldo, confidencialidad, devolución.
- Política de prevención de riesgos psicosociales (documento aparte; 5.1).
- Axia Compliance: mecanismo de quejas (8.1 b) y protocolo de violencia laboral (8.2 g).
- NOM-030 (Axia NOMs): integración al diagnóstico (7.6).
- RIT, arts. 11 y 72.
- Axia Capacitación: DNC al menos cada dos años (8.2 i) 3).
- Tabla de conservación de documentos (pendiente transversal del mapa): NOM035_CONSERVACION_ANOS.

7. PENDIENTES
- [x] Tabla 3 de la Guía II, Ecuación 1 y rangos confirmados en la edición oficial.
- Revisión del usuario al aviso específico.
- Verificar en la LFPDPPP las excepciones para comunicar datos a la institución de canalización y a la autoridad (apartado 7 del aviso).
- Confirmar si la excepción del art. 9 alcanza a los datos sensibles del art. 8 (se recaba la casilla de todos modos). El reglamento de la ley nueva no se ha publicado.
- Decidir si la persona encargada se nombra en el aviso (hoy no, por la regla de documentos sin marca).
- Revisar la política de prevención del usuario en su propia conversación.
- Redactar la especificación funcional.

8. CONTRADICCIONES
- Resuelta (10/11/2026): acceso del psicólogo del cliente.
- Política del usuario: atribuye la investigación de quejas a las «Comisiones Mixtas»; el RIT la asigna al Comité de Integridad y Disciplina.
