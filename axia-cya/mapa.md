# AXIA CYA — Mapa (Capacitación y adiestramiento)

Creado el 27/11/2026 por el Cerebro de Axia RH como arranque de la línea. **Desde esta fecha lo escribe solo el Cerebro de Axia CYA.** En el conocimiento del proyecto se llama «AXIA CYA - Mapa». Las decisiones viven en `registro-de-decisiones.md`; aquí solo alcance, avance, dependencias, contradicciones, encargos y orden de trabajo.

Prioridad: **A** = sin esto el módulo no funciona o queda expuesto en una inspección · **B** = necesario para el PMV de la línea · **C** = puede esperar.

---

## 1. Alcance de la línea

**Entra:** Comisión Mixta de Capacitación, Adiestramiento y Productividad (integración, Bases, sesiones, opinión sobre los periodos, informe anual); diagnóstico de necesidades de capacitación (DNC); planes y programas; gestión de cursos, instructores y evidencias; constancias DC-3; DC-1 y reporte al SIRCE (por omisión, por confirmar); módulo opcional de productividad.

**Se queda en Axia RH:** cláusula de prueba o capacitación inicial del contrato; art. 41 del RIT; comunicado de respaldo del módulo 4; exigencia de evidencia para terminar la capacitación inicial; D-01 y D-02 (elección común), que viven en el kit de PTU.

**No entra por ahora:** impartir los cursos en la plataforma (etapa futura); los estudios técnicos y la matriz de NOM (Axia NOMs); las políticas (Axia Compliance).

---

## 2. Catálogo y avance

| # | Módulo | Documentos y funciones | Estado | Prioridad |
|---|---|---|---|---|
| 1 | Comisión mixta | Oficio al sindicato o designación; acta de integración e instalación con Bases; F-1 a F-5 | Redactados; en revisión por el usuario; falta aplicar el criterio común del 02/11/2026 y hacer corte nuevo | A |
| 2 | Constancias y reporte | DC-3 con su autentificación; lista de constancias y exportación al SIRCE; DC-1 | DC-3: flujo definido. SIRCE: falta. DC-1: confirmar | A |
| 3 | DNC | Diagnóstico por puesto, área o centro; liga con perfiles de puesto, NOM y evaluaciones | Por diseñar | B |
| 4 | Planes y programas | Plan y programa (DC-2 si sigue vigente), calendario, presupuesto | Por diseñar | B |
| 5 | Gestión de cursos | Catálogo de cursos, instructores o agentes capacitadores, convocatoria, asistencia, evaluación, evidencias | Por diseñar | B |
| 6 | Productividad | Base 3.11 y Base 17 de la comisión | Provisional | C |
| 7 | Cursos en la plataforma | — | Etapa futura | C |

**Dónde están los documentos de la comisión:** se redactaron en la conversación de la comisión de capacitación del proyecto de Axia RH; su último corte es del 26/10/2026 y no está en el conocimiento de ese proyecto. Hay que traer el modelo maestro y su corte a este proyecto (paso 1 del orden de trabajo).

---

## 3. Dependencias

| Con | Qué | Dirección |
|---|---|---|
| Axia RH, módulo 4 | F2_EMITIDA, F2_FECHA, F2_SENTIDO, F2_SOLICITUD_FECHA | Axia CYA entrega; Axia RH lee |
| Axia RH, módulo 4 | Evidencia de la capacitación impartida (DC-3 u otra) para terminar la capacitación inicial | Axia CYA entrega; Axia RH lee |
| Axia RH, configuración de la empresa | MOD_PRUEBA, SINDICATO, SINDICATO_NOMBRE, DESIGNACION_OBRERA, NUM_REPRESENTANTES_POR_PARTE, REPRESENTANTES_SUPLENTES; PLANTILLA_NUM (calculada) | Axia RH entrega; Axia CYA lee |
| Axia RH, organigrama y alta | Puestos, CLASIFICACION (confianza no puede ser representante obrero), perfiles de puesto (requisitos y capacitación del puesto, PERFIL_CAPACITACION), centros, TRAB_ESCOLARIDAD | Axia RH entrega; Axia CYA lee |
| Axia RH, kit de PTU | D-01 y D-02 para la elección común | Axia RH mantiene |
| Axia RH, RIT | Art. 41 remite a la opinión de la Comisión | Axia RH mantiene |
| Axia NOMs | Qué capacitación exige cada NOM; DNC de la NOM-035 | Axia NOMs indica; Axia CYA programa y acredita |
| Axia Compliance | Capacitación o difusión que exijan las políticas | Por encargo |
| Firma electrónica (Axia RH, especificación v1.5) | Firma de actas y constancias; la autentificación de la DC-3 con firma digitalizada (F-3) | Verificar compatibilidad |

---

## 4. Contradicciones y decisiones que necesita el usuario

| # | Asunto | Propuesta del Cerebro de Axia RH |
|---|---|---|
| 1 | **PERIODICIDAD.** Los pendientes de la comisión usan PERIODICIDAD (sesiones de la comisión); en Axia RH, PERIODICIDAD es la periodicidad de pago, atributo del puesto (decisión P9 del 21/11/2026) | Renombrar en esta línea (por ejemplo, CMCAP_SESIONES_PERIODICIDAD). Revisar igual PERIODO_CARGO, ANOS_CONSERVACION, DIAS_OBJECION y DIAS_RESOLUCION contra el diccionario único antes de darlas de alta |
| 2 | **SIRCE y DC-1.** Pasaron a esta línea «por omisión» el 15/11/2026, sin confirmación expresa | Confirmar que quedan en Axia CYA |
| 3 | **DC-3 de la capacitación inicial.** Axia RH la exige como evidencia, pero no la genera | Que esta línea la genere cuando la capacitación inicial la imparta la Empresa, y que admita cargar constancias externas |
| 4 | **Configuración propia de la línea** | Aprobar el mismo criterio que Axia NOMs: configuración por empresa y por centro, ligada a Axia RH, sin duplicar sus datos |
| 5 | **Normalización de los documentos de la comisión** (términos, marcas y referencia a la «Cláusula Cuarta») | Aplicarla al traer el modelo, en la misma conversación de la comisión |

---

## 5. Encargos por conversación

**Comisión mixta** (conversación por abrir en este proyecto, con el modelo traído de Axia RH)
1. Aplicar el criterio común del 02/11/2026 (registro, sección 3): designación por omisión, sin votación secreta, CONFORMIDAD_FIRMAS opcional, elección solo con D-01 y D-02 del kit de PTU; quitar convocatoria, constancia y acta de elección propias.
2. Normalizar «la Empresa» y «las personas trabajadoras», `{{VARIABLES}}` y `[SI …] … [FIN SI]`.
3. Corregir la referencia a la «Cláusula Cuarta» del contrato (hoy cláusula tercera, apartados 3.1 a 3.4) y retirar la dependencia del aviso de privacidad sobre SIRCE.
4. Resolver la contradicción 1 (nombres de variables) contra el diccionario único.
5. Verificar los formatos y plazos de la sección 6.
6. Guardar «Corte - Comisión mixta de capacitación».

**Constancias y SIRCE** (conversación por abrir)
1. Verificar los formatos DC-1, DC-2 y DC-3 vigentes y sus campos; listar los datos que exige cada uno y cuáles ya existen en el diccionario único. Los que falten de empresa, organigrama o alta se piden en `encargos-para-axia-rh.md`.
2. Diseñar el flujo DC-3: emisión, autentificación (sección 3 del registro), entrega, carga de constancias externas y salida hacia Axia RH.
3. Diseñar la exportación al SIRCE con su calendario de alertas.

---

## 6. Vigilancia normativa

- Capítulo de productividad, formación y capacitación de la LFT y arts. 39-A a 39-F.
- Acuerdo de la STPS sobre criterios, requisitos y formatos de capacitación (DC-1, DC-2, DC-3) y sus reformas; eliminación del DC-4 en abril de 2025 (por verificar).
- Lineamientos del SIRCE y sus plazos (por verificar).
- NOM-035 y NOM que exigen capacitación (vía Axia NOMs).
- LFPDPPP 2025 y su reglamento (datos de las personas capacitadas).

---

## 7. Orden de trabajo sugerido (27/11/2026)

1. Traer al proyecto el modelo maestro de la comisión y su corte del 26/10/2026; abrir la conversación «Comisión mixta» y cumplir sus encargos.
2. Constancias y SIRCE: es lo que Axia RH necesita para cerrar la terminación de la capacitación inicial y lo que más se revisa en una inspección.
3. Resolver las decisiones 2 a 4 de la sección 4.
4. DNC, después planes y programas, después gestión de cursos.
5. Productividad y, en una etapa posterior, cursos en la plataforma.
