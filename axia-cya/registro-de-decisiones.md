# AXIA CYA — Registro de decisiones (Capacitación y adiestramiento)

Creado el 27/11/2026 por el Cerebro de Axia RH como arranque de la línea, con las decisiones que Axia CYA hereda del registro de Axia RH (secciones 4.5, 4.6, 5.2 y 6). **Desde esta fecha lo escribe solo el Cerebro de Axia CYA.** En el conocimiento del proyecto se llama «AXIA CYA - Registro de decisiones».

La arquitectura general (niveles de captura, atributos de puesto, pantallas de eventos) y las convenciones de redacción **no se repiten aquí**: rigen `base-comun/arquitectura-y-convenciones.md` y el diccionario único `base-comun/diccionario-variables.md`. Este registro solo contiene lo propio de la línea.

Estados: **provisional** (decisión tomada en conversación, sujeta a revisión final), **aprobada** (el usuario la aprobó expresamente; sigue siendo revisable en la revisión final), **propuesta** (planteada por un Cerebro, sin decisión del usuario).

---

## 1. Catálogo de documentos y módulos

| Módulo / documento | Se activa cuando | Estado |
|---|---|---|
| Comisión Mixta de Capacitación, Adiestramiento y Productividad: oficio al sindicato (con sindicato) o designación por las personas trabajadoras; acta de integración e instalación con Bases de Funcionamiento | PLANTILLA_NUM > 50, o la Empresa usa periodo de prueba o capacitación inicial (MOD_PRUEBA = Sí) | En revisión por el usuario. Último corte: 26/10/2026 (conversación de la comisión en el proyecto de Axia RH). Falta aplicar el criterio común (sección 3) |
| F-1 acta de sesión · F-2 opinión sobre el periodo de prueba o de capacitación inicial · F-3 firma digitalizada · F-4 sustitución · F-5 informe anual | Según el evento | F-2 redactado (prioridad A); F-1, F-3, F-4 y F-5 redactados (B) |
| Elección opcional de representantes: D-01 y D-02 del kit de PTU (Axia RH), comunes a las comisiones de PTU y de capacitación, con boleta separada por comisión | DESIGNACION_OBRERA = Elección | Redactados en Axia RH; esta línea solo los usa |
| Módulo opcional de productividad (Base 3.11 y Base 17) | A elección de la Empresa | Provisional (24/10/2026) |
| Constancia de competencias o de habilidades laborales (DC-3) | Cada curso concluido | Formato oficial; flujo de autentificación definido (sección 3) |
| Lista de constancias y exportación para el SIRCE | Cada periodo de reporte | **Falta**; plazos identificados (por verificar) |
| DC-1 | Por definir | Pasa a esta línea por omisión; **confirmar** (sección 4) |
| Diagnóstico de necesidades de capacitación (DNC) | Por definir | Por diseñar |
| Planes y programas (DC-2) | Por definir | Por diseñar; verificar el formato vigente |
| Gestión de cursos: instructores o agentes capacitadores, asistencia, evaluación y evidencias | Cada curso | Por diseñar |
| Cursos tomados en la plataforma | — | Etapa futura (idea del usuario, 26/10/2026) |

---

## 2. Arquitectura propia de la línea y puntos de contacto

- (27/11/2026, regla heredada) **Datos compartidos.** Personas, puestos, centros, plantilla, sindicato y demás datos de empresa, organigrama y alta se leen de Axia RH con su nombre canónico (`base-comun/diccionario-variables.md`). Esta línea no los captura de nuevo; lo que le falte lo pide en `encargos-para-axia-rh.md`.
- (27/11/2026, **propuesta** del Cerebro de Axia RH, igual que la aprobada en Axia NOMs) **Configuración propia de Axia CYA**, por empresa y por centro, ligada a la empresa y a los centros de Axia RH, para los datos que solo usa esta línea (catálogo de cursos e instructores, parámetros de la comisión, plazos de reporte). Pendiente de decisión del usuario.
- **Variables comunes de las comisiones** (nivel empresa en Axia RH, diccionario 1.8): SINDICATO, SINDICATO_NOMBRE, DESIGNACION_OBRERA, NUM_REPRESENTANTES_POR_PARTE, REPRESENTANTES_SUPLENTES. CONFORMIDAD_FIRMAS es dato del acta (evento). MOD_PRUEBA es pregunta de la configuración de la empresa en Axia RH (decisión P6 del 21/11/2026), sin valor por omisión; esta línea la lee para activar la comisión. PLANTILLA_NUM es calculada por el sistema.
- **Lo que Axia RH lee de esta línea** (no cambiar sin avisar al Cerebro de Axia RH):
  - F2_EMITIDA, F2_FECHA, F2_SENTIDO y F2_SOLICITUD_FECHA, que usa el comunicado de respaldo del módulo 4 al terminar el periodo de prueba o de capacitación inicial.
  - La evidencia de la capacitación impartida (DC-3 u otra constancia), que Axia RH exige cargar para terminar la capacitación inicial.
- **Lo que se queda en Axia RH:** la cláusula de prueba o capacitación inicial del contrato (cláusula tercera); la remisión del art. 41 del RIT a la opinión de la Comisión; el comunicado de respaldo del módulo 4; la exigencia de evidencia para terminar la capacitación inicial.
- **Axia NOMs:** indica qué capacitación exige cada NOM; esta línea la programa y la acredita. La NOM-035 pide el diagnóstico de necesidades al menos cada dos años (según el README de esta carpeta, numeral 8.2 i) 3; por verificar).
- **Axia Compliance:** si una política exige capacitación o difusión, se coordina por encargo.

---

## 3. Decisiones heredadas — Comisión Mixta de Capacitación, Adiestramiento y Productividad

Fuente: registro de Axia RH, 4.6 y 4.5 (corte de la comisión del 26/10/2026 y criterio común del 02/11/2026).

**Criterio común de las tres comisiones (RIT, capacitación y PTU)**
- (02/11/2026, aprobada; sustituye el criterio del 26/10, que proponía votación secreta en capacitación y PTU) **En ninguna comisión hay votación secreta.** Por omisión, las personas trabajadoras designan a su representación; el documento hace constar la designación, la aceptación de los representantes y que la Empresa no intervino. Refuerzo opcional: relación de conformidad firmada (CONFORMIDAD_FIRMAS). Elección formal opcional (DESIGNACION_OBRERA = Elección), sin voto secreto, en una jornada común con D-01 y D-02 del kit de PTU. Con sindicato, la designa el sindicato. El usuario no obliga al cliente a celebrar elecciones ni a conservar sus evidencias; riesgo explicado una vez, se mantiene.
- (02/11/2026) Variables comunes: DESIGNACION_OBRERA (sustituye a CMRIT_INTEGRACION_MODO), NUM_REPRESENTANTES_POR_PARTE (mínimo 1) y REPRESENTANTES_SUPLENTES (Sí por omisión). El personal de confianza participa pero no puede ser representante. Una persona puede representar en más de una comisión.
- (26/10/2026, aprobada) El tiempo dedicado a cualquier comisión mixta es tiempo de trabajo con goce de salario.
- (26/10/2026) Representantes obreros: no pueden tener clasificación Confianza en el organigrama y deben pertenecer a uno de los centros.

**Objeto y funcionamiento**
- Objeto reducido a las funciones legales. (24/10/2026) La Base 2 excluye expresamente la disciplina, las sanciones, la terminación, el salario y la nómina.
- Coordinación fija patronal y secretaría obrera. (26/10/2026, aprobada) La secretaría puede suplir a la coordinación solo para convocar y conducir una sesión, sin cambiar su titularidad.
- (24/10/2026, provisional) Variante con sindicato (oficio de designación; sin convocatoria, constancia ni acta de elección) y variante sin sindicato.
- (02/11/2026) Instrumento base: acta de integración e instalación con Bases de Funcionamiento. La convocatoria, la constancia y el acta de elección propias se sustituyen por D-01 y D-02 del kit de PTU, solo si se elige el módulo de elección.
- (02/11/2026) Solo con el módulo opcional de elección: mesa de personas trabajadoras, votación sin voto secreto, publicación al menos 5 días hábiles en cada centro y por medio digital, válida con más del 50 % del padrón y segunda jornada dentro de 10 días hábiles sin umbral.
- (24/10/2026, provisional) Requisitos de candidatura: prestar servicios en el centro, no ocupar puesto de confianza y no formar parte de la representación patronal. Los representantes patronales se designan por nombramiento escrito.
- (24/10/2026, provisional) Quórum: mitad más uno de los propietarios y al menos uno de cada representación. Acuerdos por mayoría de cada representación, sin voto de calidad; sin acuerdo, el acta registra la posición de cada parte. Duración del cargo, cinco causas de sustitución y procedimiento para cubrir vacantes.
- (24/10/2026, provisional) Se usa la denominación legal de la comisión, con la aclaración de que es la misma de los periodos de prueba y capacitación inicial.

**Opinión sobre el periodo de prueba y la capacitación inicial**
- (24/10/2026, aprobada) La cláusula del periodo se trabaja en el contrato (Axia RH); la terminación va al kit; la comisión solo conserva la Base 14 y el formato F-2.
- (24/10/2026, provisional) La comisión emite **opinión, no dictamen**. Sin acuerdo, se registra la opinión de cada representación. Si no se emite a tiempo, se levanta constancia de que se solicitó oportunamente.
- (26/10/2026, aprobada) Sin alerta automática de solicitud de opinión ni variable de días de aviso: el F-2 se genera e imprime junto con los documentos de terminación al vencer el periodo.
- (10/11/2026, Axia RH) Los requisitos ya no bloquean la terminación en Axia RH: sin F-2 ni evidencia, «Continuar sin requisitos» permite la baja con convenio y solo deja de generarse el comunicado de respaldo.

**Constancias y reporte**
- (24/10/2026, provisional) La DC-3 se autentifica con al menos una firma de cada representación. La firma digitalizada solo procede por acuerdo unánime (F-3) y se revoca al sustituir al firmante. Con plantilla de 50 o menos, la Empresa autentifica la DC-3.
- (24/10/2026, provisional) La Empresa firma y conserva el DC-1. La lista de constancias se presenta por SIRCE (según el corte, el DC-4 se eliminó en abril de 2025). Plazos: DC-3 dentro de 20 días hábiles y presentación en SIRCE dentro de 60 días hábiles. **Por verificar** en la fuente oficial vigente.

---

## 4. Decisiones de alcance

- (15/11/2026, decisión del usuario; sustituye la del 26/10) La Comisión Mixta de Capacitación, Adiestramiento y Productividad sale de Axia RH y pasa a Axia CYA, con sus formatos F-1 a F-5, junto con DNC, plan y programa, cursos y DC-3. **Por omisión se van también el SIRCE y el DC-1, salvo que el usuario indique otra cosa** (pendiente de confirmar).
- (15/11/2026, decisión del usuario) Cada línea Axia tiene su propio proyecto y su propio Cerebro, con la misma estructura de trabajo que Axia RH (registro, mapa, cortes).
- (26/10/2026, idea del usuario) Etapas: primero DNC, comisión mixta, plan y programa, gestión de capacitaciones y exportación para SIRCE; a futuro, tomar los cursos en la plataforma.
- (26/10/2026) La capacitación inicial es solo una cláusula del contrato (Axia RH), no un contrato autónomo.
- (27/11/2026) Proyecto de claude.ai «AXIA CAPACITACIÓN» y su Cerebro configurados por el Cerebro de Axia RH (instrucciones en `instrucciones-del-proyecto.md`).
- (27/11/2026) El Cerebro de Axia CYA asume este registro y el mapa. Copias en el conocimiento del proyecto («AXIA CYA - Registro de decisiones» y «AXIA CYA - Mapa»), con el mismo contenido que estos archivos.

---

## 5. Pendientes heredados

- [ ] Confirmar que el SIRCE y el DC-1 quedan en Axia CYA (por omisión desde el 15/11/2026).
- [ ] Confirmar si las constancias DC-3 de la capacitación inicial se generan en esta línea (Axia RH solo exige cargarlas como evidencia).
- [ ] Verificar en la fuente oficial los arts. 39-A, 39-B, 153-D y 183 LFT y el capítulo de productividad, formación y capacitación.
- [ ] Confirmar que no haya un acuerdo de la STPS posterior a abril de 2025 que modifique los formatos DC-1, DC-2 o DC-3; verificar la eliminación del DC-4 y los plazos de DC-3 y SIRCE.
- [ ] Buscar criterios judiciales sobre procedimientos internos autoimpuestos (riesgo de que la Empresa quede obligada por un procedimiento que no siga).
- [ ] Fijar valores por omisión de PERIODO_CARGO, ANOS_CONSERVACION, DIAS_OBJECION, DIAS_RESOLUCION y de la periodicidad de las sesiones (ver contradicción 1 del mapa: no puede llamarse PERIODICIDAD).
- [ ] Normalizar términos y marcas en los documentos de la comisión: «la Empresa», «las personas trabajadoras», `{{VARIABLES}}` y `[SI …] … [FIN SI]`.
- [ ] Corregir la referencia a la «Cláusula Cuarta» del contrato (hoy cláusula tercera, temporalidad, apartados 3.1 a 3.4) y retirar la dependencia del aviso de privacidad sobre SIRCE.
- [ ] Tabla de conservación de documentos: alinear los plazos de la comisión con la tabla transversal que prepara Axia RH.
