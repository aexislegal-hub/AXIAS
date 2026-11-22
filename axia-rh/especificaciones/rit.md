# AXIA RH — MÓDULO 2: REGLAMENTO INTERIOR DE TRABAJO Y FORMATOS DISCIPLINARIOS

Especificación para programación · Versión 1.7 · 18/11/2026
Fuente: «Modelo maestro — Reglamento Interior de Trabajo» (pestaña principal, rev. 1388, y pestaña «Formatos», rev. 39), «Modelo maestro — Acta de integración de la CMRIT» (rev. 36), «AXIARH - Registro de decisiones» (actualizado al 02/11/2026), «Corte - RIT» y «Corte - Módulo de permisos y licencias» y «Corte - Firma electrónica» (12/11/2026), y encargos del mapa del 13/11/2026.

> **Nota de Cerebro (21/11/2026, decisiones P1 a P10 del diccionario único, aplicadas por Cerebro con autorización del usuario).** `MOD_PRUEBA` es una pregunta de la configuración de la empresa, no un dato del paquete (decisión P6). `REGISTRO_PATRONAL` es el `CENTRO_REGISTRO_PATRONAL` del catálogo de centros (decisión P1). Los textos del RIT no cambian.

## Cambios respecto de la versión 1.6 (encargo 18 del mapa, 18/11/2026)

Si la 1.6 ya se cargó, aplicar solo estos cambios.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 0; 4.1; 4.3; 6.1, arts. 80 y 81 y conducta 43; 6.3; 6.5; 8.3 | **Plazos del expediente disciplinario en días naturales** (decisión del usuario): reporte de la jefatura (a más tardar al día siguiente), audiencia (1 a 5 días naturales después de FD-1), notificación de FD-3 (5 días naturales después de la audiencia), inicio de la suspensión (a más tardar 10 días naturales después de la notificación) y revisión de la falta leve (3 días naturales). El art. 83 ya estaba en días naturales. Los demás plazos del RIT siguen en días hábiles (art. 5) |
| 2 | 4.3; 6.1, art. 81 | Reglas complementarias: si la audiencia o el inicio de la suspensión caen en día de descanso de la persona, pasan a su siguiente día laborable; si el plazo de revisión vence en su día de descanso, se extiende a su siguiente día laborable; la duración de la suspensión (1 a 8 días) se cuenta en días laborables del turno. El sistema propone las fechas y RH puede cambiarlas, con las validaciones de 4.3. Párrafo nuevo al final del art. 81 |

## Cambios respecto de la versión 1.5 (encargos del mapa del 18/11/2026)

Si la 1.5 ya se cargó, aplicar solo estos cambios.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 6.1, art. 36 | Última frase del párrafo de días sin vacaciones: «Esas medidas no modifican, sin la conformidad de la persona trabajadora, las vacaciones que haya solicitado o que se le hayan autorizado antes de que la Empresa las dé a conocer.» Prevalece lo que se registra primero |
| 2 | 0.1, regla 4; 8.2 | `VAC_PROGRAMACION_MODO` es un solo campo: si la pantalla del RIT lo pregunta, lee y escribe el mismo campo que el módulo de vacaciones |
| 3 | 2.1; 8.1; 8.2 | `DIAS_EN_CASA_EMPRESA` deja de derivarse de `TELE_APTO` (eliminada): pasa a pregunta de empresa Sí/No, sin valor por omisión. Alerta si un alta tiene `DIAS_EN_CASA_ACTIVO` = Sí y la empresa dice No |
| 4 | 6.1, art. 12 y anexo de horarios; 2.4; 8.1 | Descanso rotativo: con `TURNO_DESCANSO_TIPO` = Rotativo, el anexo imprime «N días por semana» y «Rotativo», sin tabla de días. El tipo de jornada es el calculado (Diurna, Nocturna o Mixta), nunca «Rotativa». Frase nueva en el art. 12 con `TURNOS_ROTATIVOS` = Sí. Ya no existe PUEDE_SALIR |

## Cambios respecto de la versión 1.4 (encargos del mapa del 17/11/2026)

Si la 1.4 ya se cargó, aplicar solo estos cambios.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 6.1, art. 36; 2.1; 8.2 | `VAC_PROGRAMACION_MODO` con tres valores: Calendario anual · Periodos de solicitud por antigüedad · A solicitud. La primera frase del art. 36 tiene un texto por valor. Párrafo nuevo, siempre impreso, sobre días en que no se programan vacaciones y número de personas por área (fundamento de los bloqueos y cupos del módulo de vacaciones) |
| 2 | 3.2 | Cambiar `VAC_PROGRAMACION_MODO` con el RIT depositado activa la alerta «RIT modificado: pendiente de depósito» |
| 3 | 2.6 | El comunicado de horarios ajustados es MOD-2 «Ajuste legal de jornada» del módulo 5. Las personas afectadas se identifican por la jornada de su versión de condiciones, solo para el resumen del lote; el anexo de horarios no cambia condiciones individuales |
| 4 | 10 | El documento del Comité de Integridad y Disciplina se redacta en Axia Compliance; el RIT solo conserva la remisión del art. 79 y `COMITE_INTEGRANTES` |

## Cambios respecto de la versión 1.3 (retroalimentación del segundo corte, 15/11/2026)

La 1.3 se corrió en el software. Aplicar estos cambios; ante cualquier duda rige el texto completo.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 0.1, regla 6 | **Sin candados por fecha.** El sistema permite capturar, guardar, generar, imprimir y marcar como firmado cualquier documento con fecha futura (sesión, emisión, conformidad). Se elimina el bloqueo «La sesión aún no ocurre». Solo se conservan las validaciones de orden entre fechas del propio expediente |
| 2 | 0.1, regla 7; 8.2 | **Campos que dependen de una opción.** Primero se pregunta la opción y solo después aparecen sus campos. Si la opción los excluye, no se muestran, no se piden y no aparecen en «Faltan datos». Aplica a `LACTARIO` (sin valor por omisión: con No no se piden ubicación ni equipamiento) y a `VAC_PROGRAMACION_MODO` |
| 3 | 6.1, art. 36; 8.2 | **Vacaciones sin calendario anual.** Nueva opción `VAC_PROGRAMACION_MODO`: Calendario anual · A solicitud. Con A solicitud no se pide `MES_CALENDARIO_VACACIONES` y el art. 36 imprime el texto de solicitud. El segundo párrafo del art. 36 remite al art. 30 |
| 4 | 1; 2.2; 2.3; 2.4; 2.5; 6.1; 8.1 | **Nuevo orden de anexos:** A. Centros de trabajo (solo con más de un centro), B. Horarios, C. Catálogo de conductas y escala de medidas disciplinarias. El Anexo A lista nombre, domicilio, estado y registro patronal IMSS de cada centro. Arts. 3 y 88 y dictamen ajustados. Con un solo centro no hay Anexo A y las letras se recorren (2.3) |
| 5 | 6.2 a 6.8; 8.3 | Los formatos nombran el catálogo de conductas por su contenido, no por su letra. Se renombran `EXP_CONDUCTAS_ANEXO_A` → `EXP_CONDUCTAS_CATALOGO` y `FD3_CONDUCTA_ANEXO_A` → `FD3_CONDUCTA_CATALOGO`. FR-1 enumera los anexos por contenido |
| 6 | 6.1, Anexo B | La introducción del anexo de horarios deja de imprimir la nota de diseño («Se genera del catálogo…») |
| 7 | 0.1, regla 8; 6.9 | **Concordancia de número:** con valor 1 se imprime en singular la palabra que sigue al número («1 año», «1 representante propietario»). Nunca se imprimen «(s)» ni «(a)». El acta dice «Propietario» en el Anexo 1 |
| 8 | 6.9, regla 10 | La CMRIT es permanente «mientras la Empresa tenga centros de trabajo en operación» (antes: «mientras subsista el centro de trabajo») |
| 9 | 2.5; 6.9 | **Un solo catálogo de centros.** El dictamen, el Anexo A, la carátula del acta y las hojas del Anexo 1 del acta toman los centros del mismo catálogo. Toda persona activa y todo turno deben pertenecer a un centro de ese catálogo (bloqueo). CURP repetida entre integrantes o personas: bloqueo |

## Cambios respecto de la versión 1.2 (retroalimentación del primer corte, 13/11/2026)

La 1.2 se corrió una vez en el software. Aplicar estos cambios; ante cualquier duda rige el texto completo.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 0 | **Arial en todos los documentos del sistema** (no solo este módulo). Sin encabezado ni pie del navegador: el PDF se genera en el servidor (ver 0, «Impresión») |
| 2 | 0.1 (nueva) | Reglas de pantalla: campos faltantes resaltados, tablas con botón de guardar, casilla de documento firmado con archivo opcional, flujo de datos del acta al RIT |
| 3 | 6.9; 8.5 | Acta de la CMRIT: CURP en las firmas de todos los integrantes (propietarios y suplentes) y en el Anexo 1 |
| 4 | 3.1; 0.1 | La casilla «firmado por todos los integrantes» basta para avanzar; el archivo firmado es opcional y su falta solo genera alerta |
| 5 | 6.1, art. 25; 8.2 | Días de pago por periodicidad (`DIAS_PAGO_RESUMEN`), en lugar de un solo `DIA_PAGO` |
| 6 | 6.1, art. 66; 8.2 | Lactario opcional (`LACTARIO`); sin lactario, reducción de una hora de la jornada |
| 7 | 6.1, art. 58 | Ubicación del procedimiento de primeros auxilios opcional |
| 8 | 6.4 | FD-3 ya no nombra al puesto que decide la rescisión: «turna el expediente a la Empresa». `RESCISION_RESPONSABLE` queda solo para la notificación interna |
| 9 | 3.2; 3.4; 6.8 | Se elimina por completo la verificación periódica de la fijación (`RIT_REVISION_FIJACION_MESES`, su alerta y el punto 3 de FR-2). FR-2 conserva solo la fijación y la entrega individual |
| 10 | 6.1, art. 79; Anexo C; 2.x; 8.2 | Se quita del RIT la integración del Comité: el art. 79 remite a un documento propio y desaparece el anexo del Comité |
| 11 | 6.1, art. 74; 2.1 | Canal de denuncias opcional: sin `CANAL_DENUNCIAS` se omite el art. 74 y se renumera |
| 12 | 6.1, art. 47 | Limpieza general de instalaciones opcional |
| 13 | 6.1, arts. 4 y 88; Anexo C; 6.7; 2.x; 8.2 | **Se quita del RIT el anexo de ubicación de las políticas** (la Ley no lo pide y puede ser motivo de observación en el depósito). El RIT queda con los Anexos A y B. El art. 4 solo remite al registro de políticas de RH; el art. 88 solo menciona el Anexo B; FR-1 solo menciona los Anexos A y B |
| 14 | 0; 3.3; 4.6; 6.7 | **Firma (decisión del 13/11/2026, registro 4.4):** el RIT y el acta de la CMRIT se firman de forma autógrafa (depósito). **FR-1 sigue `FIRMA_MODALIDAD` de cada persona** en sus tres momentos; autógrafa solo por firma en papel, falla de la Plataforma o negativa. Por la Empresa firma el representante al ingreso y RH designado en la emisión y la modificación. FD-1 a FD-5 y FR-2 siguen siendo autógrafos. Sustituye el cambio 10 de la 1.2 en lo que toca a FR-1 |
| 15 | 6.1, arts. 16 y 30; 5 | Art. 30: en los permisos legales la solicitud puede devolverse para corrección; si llega la fecha sin autorización completa, RH los registra y la ausencia no es falta. Art. 16 y tabla II (asuntos personales): remiten a la cadena del art. 30; la jefatura es el primer nivel |

## Cambios respecto de la versión 1.0

Ni la 1.0 ni la 1.1 se cargaron al software; esta versión las sustituye completas.

| # | Sección | Cambio |
| --- | --- | --- |
| 1 | 6.1, art. 31, tabla I | La fila de voto incluye los procesos de revocación de mandato. Fila fija nueva: comisión accidental o permanente del sindicato o del Estado |
| 2 | 6.1, art. 31 | Párrafo nuevo: un permiso de la tabla II sin evidencia en plazo puede tenerse por otorgado sin goce, con reversión si la evidencia llega después; los de la tabla I conservan su salario. Regla de sistema en 5 |
| 3 | 6.1, art. 31 | Párrafo nuevo: días que se computan y no se computan para la PTU (registro, 4.7) |
| 4 | 6.1, Anexo A; 4.2; 9 | Conducta muy grave 60, ausentismo reiterado, ligada a la fr. XV en la tabla de correspondencia. Regla de sistema en 4.2 |
| 5 | 10 | Dependencia con el módulo de permisos y licencias |
| 6 | 6.1, art. 77 | La fracción 4 aclara que la rescisión la decide la Empresa conforme al art. 84 y no requiere resolución del Comité |
| 7 | 6.1, art. 46; 4.5 | La investigación por daño o pérdida se sigue por los arts. 80 y 81, y el descuento solo procede con reconocimiento o determinación de responsabilidad, conforme al art. 27 |
| 8 | 6.1, art. 30; 5 | Cadena de autorización para todo permiso (jefatura, RH y dirección del área), con plazo por nivel. En los permisos legales la cadena verifica y programa, pero no puede negar, salvo donde la Ley lo permite |
| 9 | Alcance; 6.9; 8.5 | Se agrega el acta de integración de la CMRIT, ya con el criterio común de las comisiones (DESIGNACION_OBRERA, REPRESENTANTES_SUPLENTES y CONFORMIDAD_FIRMAS opcional) |
| 10 | 0; 3.3; 4.6; 6.7; 6.9 | **Todo el módulo se firma de forma autógrafa** (decisión del usuario, 12/11/2026): RIT, acta de la CMRIT y su Anexo 1, actas de sesión, FD-1 a FD-5, FR-1 y FR-2, aunque `FIRMA_MODALIDAD` = Electrónica. Se quita de FR-1 el bloque de firma electrónica (revertido para FR-1 por el cambio 14 de la 1.3) |

## Alcance

| Se programa con esta especificación | Queda fuera |
| --- | --- |
| Acta de integración de la CMRIT (6.9) | Jornada común de elección (D-01 y D-02 del kit de PTU) |
| Dictamen de emisión y Reglamento Interior de Trabajo (89 artículos en 13 capítulos, transitorios y firmas) | Mecánica de la firma electrónica de FR-1: «AXIARH - Firma electrónica - Especificación para programación» |
| Anexos A (centros de trabajo, solo con varios centros), B (horarios) y C (conductas y escala) | Políticas internas a las que remite el RIT (se generan en otro módulo) |
| Expediente disciplinario y formatos FD-1 a FD-5 | Aviso de rescisión: servicio aparte (módulo 4, v1.3) |
| Constancias FR-1 (recibo) y FR-2 (difusión) | Acuerdo de descuento (otro documento del kit) |
| Control de versiones, depósito y alertas del RIT | |

---

## 0. Convenciones

- Variables: `{{MAYÚSCULAS_CON_GUION_BAJO}}`. Se sustituyen por el dato; nunca se imprime la marca.
- Condiciones: `[SI condición] … [FIN SI]`. Si la condición es falsa, se omite todo el bloque. Las marcas nunca se imprimen. Se permiten condiciones anidadas; cada `[SI]` cierra con su `[FIN SI]`.
- `[RECUADRO_MANUSCRITO]`: marca de los formatos. El sistema imprime en su lugar un recuadro de 15 renglones en blanco con la leyenda «Si el espacio no es suficiente, continúe en hojas adicionales, que firmará y se agregarán al expediente» y una línea de firma de la persona trabajadora. No se captura texto.
- Términos fijos: «la Empresa» y, por ser instrumento colectivo, «las personas trabajadoras» (plural, minúscula).
- Niveles de captura:
  - **E** = configuración de la empresa.
  - **O** = organigrama o puesto (atributos).
  - **K** = catálogo de jornadas y turnos.
  - **A** = alta de la persona trabajadora.
  - **C** = acta de integración de la CMRIT.
  - **V** = evento (pantalla del RIT, del expediente disciplinario o de difusión).
  - **S** = calculada o derivada por el sistema.
  - **X** = sistema, solo consultoría AEXIS (bloqueada para el cliente).
- Fechas: formato largo («12 de noviembre de 2026»). Montos: MXN con dos decimales.
- **Días hábiles del RIT:** el art. 5 los define como los días laborables del centro de trabajo de que se trate. Se usan en los plazos que no son del expediente disciplinario (justificación de ausencias, aclaraciones, nómina, denuncias, permisos). El conteo empieza el día hábil siguiente al evento. Es distinto del calendario del módulo 4.
- **Plazos del expediente disciplinario (arts. 80, 81 y 83):** en días naturales, contados desde el día siguiente al evento. Reglas: (a) si la audiencia o el inicio de la suspensión caen en un día de descanso de la persona según su turno, pasan a su siguiente día laborable; (b) si el plazo de revisión de una falta leve vence en un día de descanso de la persona, se extiende a su siguiente día laborable; (c) la duración de la suspensión (1 a 8 días) se cuenta en días laborables del turno. Los días de descanso obligatorio cuentan como días de descanso. El sistema propone las fechas con estas reglas; RH puede cambiarlas, sujeto a las validaciones de 4.3.
- **Tipo de letra:** todos los documentos que genera el sistema, de este y de los demás módulos, se imprimen en Arial (12 puntos en el cuerpo; títulos en negrita, del mismo tamaño o un punto mayor). Incluye tablas y bloques de firma.
- **Impresión:** el PDF se genera en el servidor (por ejemplo, Chromium sin interfaz con `displayHeaderFooter: false`), no con la función imprimir del navegador. Así no aparecen la fecha, el título de la página, la URL ni el número de página que agrega el navegador. Márgenes con `@page { size: letter; margin: 2.5cm 2cm; }`. Si el usuario imprime desde el navegador, la vista de impresión lleva `@page { margin: 0 }` y el margen se da con relleno del cuerpo, lo que suprime el encabezado y pie del navegador. Aplica a todos los módulos.
- **Firma:** el RIT, el acta de la CMRIT (con su Anexo 1), las actas de sesión, FD-1 a FD-5 y FR-2 se firman siempre de forma autógrafa, sea cual sea `FIRMA_MODALIDAD`; el sistema genera el PDF para imprimir y la casilla «firmado» basta para avanzar (0.1). **FR-1 es la excepción:** sigue `FIRMA_MODALIDAD` de cada persona (3.3).
- Ningún texto fija cifras que cambian por reforma (jornada máxima, salario mínimo). Esas cifras viven en tablas del sistema.
- El RIT no cita artículos de la Ley. Las referencias a la LFT de esta especificación son internas y no se imprimen.

### 0.1 Reglas de pantalla (aplican a todos los formularios del sistema)

1. **Datos faltantes:** al intentar generar con datos obligatorios vacíos, el sistema no solo muestra una alerta: resalta en rojo cada campo faltante, muestra junto a él «Dato obligatorio», lista los faltantes arriba del formulario con enlace a cada uno y lleva la pantalla al primero.
2. **Tablas editables** (permisos de la Empresa, otros devengados, deducciones, etc.): cada renglón tiene botones visibles «Guardar» y «Quitar»; el renglón nuevo queda marcado «Sin guardar» hasta que se guarda; al salir con renglones sin guardar, el sistema pregunta si se guardan. El botón «+ Agregar» solo agrega un renglón vacío.
3. **Documento firmado:** la casilla «El documento está firmado por todos» basta para avanzar el estado (acta de la CMRIT, RIT firmado, constancias). La carga del archivo firmado es opcional; sin archivo queda una alerta «Falta cargar el documento firmado», que no bloquea.
4. **Un dato, una captura:** lo que se captura en el acta de la CMRIT (fecha, lugar, representantes con su CURP) llena en automático el dictamen y las firmas del RIT; no se vuelve a pedir ni se deja vacío. Lo mismo para cualquier dato que ya exista en otro nivel. Si dos pantallas preguntan el mismo dato (por ejemplo, `VAC_PROGRAMACION_MODO` en el RIT y en vacaciones), ambas leen y escriben el mismo campo.
5. Los campos opcionales dicen «Opcional» y explican qué pasa si se dejan vacíos (por ejemplo: «Si lo deja vacío, se omite el artículo 74»).
6. **Sin candados por fecha:** ningún documento se bloquea porque su fecha (sesión, emisión, conformidad, firma) sea futura. El usuario puede capturar, guardar, generar, imprimir y marcar como firmado un documento fechado después de hoy; los documentos se preparan antes del acto. Guardar nunca se bloquea por validaciones: estas solo impiden emitir la versión definitiva (sin marca de agua). Se conservan las validaciones de orden entre fechas (por ejemplo, `CMRIT_FECHA` ≤ `FECHA_EMISION`).
7. **Campos que dependen de una opción:** la pregunta de opción va primero y, si la ley no fija un valor, no tiene valor por omisión («Selecciona…»). Los campos que dependen de ella solo aparecen cuando aplican; si no aplican, no se piden ni se listan como faltantes. Ejemplos: `LACTARIO` = No oculta ubicación y equipamiento; `VAC_PROGRAMACION_MODO` = A solicitud oculta el mes del calendario.
8. **Concordancia de número:** cuando un número vale 1, la palabra que lo acompaña se imprime en singular («1 año», «1 representante propietario»); con 2 o más, en plural. Las plantillas nunca imprimen «(s)» ni «(a)».

---

## 1. Qué se imprime y qué no

El documento maestro tiene partes de diseño que **nunca** se imprimen:

| Parte del maestro | ¿Se imprime? |
| --- | --- |
| Nota de uso y matriz de cambios | No |
| Diccionario de variables | No (está en la sección 8 de esta especificación) |
| Correspondencia del catálogo de conductas con las causas legales de rescisión | No (sección 9; uso interno) |
| Dictamen de emisión | Sí, como primera hoja |
| Reglamento: capítulos I a XIII, transitorios y firmas | Sí |
| Anexo A, centros de trabajo | Solo con `NUM_CENTROS_TRABAJO` > 1 |
| Anexos de horarios y de conductas | Sí, siempre |
| Pendientes de validación y documentos por generar | No |
| Pestaña «Formatos»: reglas comunes y tabla de variables | No |

Orden de impresión: dictamen, Reglamento, firmas, Anexo A (centros de trabajo, si aplica), Anexo B (horarios) y Anexo C (catálogo de conductas). No hay más anexos.

---

## 2. Reglas de generación del RIT

### 2.1 Artículos y bloques condicionales

| Bloque | Se genera cuando | Si no se genera |
| --- | --- | --- |
| Art. 1, nombre comercial; dictamen, nombre comercial | `NOMBRE_COMERCIAL` no está vacío | Se omite la frase |
| Art. 9, bloque REPSE (5 puntos) | `REPSE_EMPRESA` = Sí | Se omite el bloque; el artículo se conserva |
| **Art. 22 completo** (días en casa) | `DIAS_EN_CASA_EMPRESA` = Sí | Se omite el artículo y se renumera |
| Art. 31, tabla I, última fila | `PERMISO_LEY_NUEVO` no está vacío (una fila por permiso legal que agregue consultoría) | No se imprime la fila |
| Art. 31, tabla II | Una fila por cada registro de `PERMISOS_EMPRESA` | — |
| **Art. 32 completo** (días por fallecimiento) | `PERMISO_FALLECIMIENTO` = Sí | Se omite el artículo y se renumera |
| Art. 36, primera frase | `VAC_PROGRAMACION_MODO` = Calendario anual: calendario anual en `MES_CALENDARIO_VACACIONES`. = Periodos de solicitud por antigüedad: periodos por grupos de antigüedad y asignación por antigüedad. = A solicitud: solicitud de cada persona por la Plataforma | Se imprime solo el texto del valor elegido. El párrafo de días sin vacaciones y personas por área se imprime siempre |
| Art. 12, descanso rotativo | `TURNOS_ROTATIVOS` = Sí (algún turno del catálogo con descanso rotativo) | Se omite la frase |
| Art. 34, pago de los días de espera | `PAGO_DIAS_ESPERA` = Sí | Se omite la frase |
| Art. 41, opinión de la Comisión Mixta de Capacitación | `MOD_PRUEBA` = Sí | Se omite la frase |
| **Art. 50 completo** (vehículos) | `VEHICULOS_ASIGNADOS` = Sí | Se omite el artículo y se renumera |
| Art. 47, limpieza general | `HORARIO_LIMPIEZA_GENERAL` no vacío | Se omite la frase |
| Art. 58, ubicación del procedimiento | `UBICACION_PROCEDIMIENTO_PRIMEROS_AUXILIOS` no vacío | Imprime «lo conserva la persona responsable designada» |
| Art. 66, lactancia | `LACTARIO` = Sí: espacio de lactancia. `LACTARIO` = No: reducción de una hora de la jornada | — |
| **Art. 74 completo** (canal de denuncias) | `CANAL_DENUNCIAS` no vacío | Se omite el artículo y se renumera |
| Dictamen, centros; art. 3, segunda frase; art. 88, Anexo A; **Anexo A completo** | `NUM_CENTROS_TRABAJO` > 1 | Con un centro, el dictamen imprime su domicilio y se omiten las frases y el Anexo A |
| Transitorio segundo, abrogación | `RIT_ANTERIOR` = Sí | Se omite la frase |

### 2.2 Renumeración de artículos

- Cada artículo tiene un identificador fijo igual a su número en el maestro (`ART_1` a `ART_89`). El identificador no se imprime.
- Al generar, el sistema numera de forma consecutiva solo los artículos que se generan. Sin «Bis» y sin huecos.
- Toda remisión a un artículo se resuelve por su identificador y se imprime con el número final. Tabla de remisiones del maestro:

| Dónde está la remisión | Remite a |
| --- | --- |
| Art. 9 (bloque REPSE) | `ART_17` y `ART_18` |
| Art. 11 | `ART_54`, `ART_72`; «artículo anterior» = `ART_10` |
| Art. 22 | `ART_17` |
| Art. 16 | `ART_30` |
| Art. 27 | `ART_46` |
| Art. 46 | `ART_80`, `ART_81`, `ART_27` |
| Art. 77 | `ART_84` |
| Art. 28 («artículo anterior») | `ART_27` |
| Art. 31, tabla II, filas de fallecimiento y de asuntos personales | `ART_32`, `ART_30` |
| Art. 34 | `ART_15` |
| Art. 39 | `ART_69` |
| Art. 63 y art. 65 | `ART_61` |
| Art. 81, párrafo final | `ART_83` |
| Art. 84 | `ART_81` |
| Art. 85 | `ART_71` |
| Art. 36 | `ART_30` |
| Art. 88 | `ART_6`, `ART_8` |
| Transitorios cuarto y quinto | `ART_13`, `ART_4` |
| Anexo de centros, introducción | `ART_3` |
| Anexo de horarios, introducción | `ART_8`, `ART_12` |
| Anexo de conductas, introducción | `ART_84` |
| Anexo de conductas, conductas 2, 5 y 33 | `ART_15`, `ART_17`, `ART_60` |
| FD-3 y FD-5 («artículo 27 del Reglamento») | `ART_27` |
| Reglas de FD («artículo 83 del Reglamento») | `ART_83` |

- Las remisiones a capítulos (I a XIII) no cambian: ningún capítulo es condicional.
- Las conductas del catálogo conservan siempre su número (1 a 60); no se renumeran.

### 2.3 Letras de los anexos

- Cada anexo tiene un identificador fijo: `ANX_CENTROS`, `ANX_HORARIOS`, `ANX_CONDUCTAS`. El identificador no se imprime.
- Con `NUM_CENTROS_TRABAJO` > 1: A = centros, B = horarios, C = conductas.
- Con un solo centro no hay anexo de centros y las letras se recorren: A = horarios, B = conductas.
- Toda mención de un anexo en el dictamen, el Reglamento y los transitorios («Anexo A», «Anexo B», «Anexo C» en la plantilla 6.1) se resuelve por su identificador y se imprime con la letra final, igual que las remisiones a artículos (2.2). En la plantilla, «Anexo A» = `ANX_CENTROS`, «Anexo B» = `ANX_HORARIOS`, «Anexo C» = `ANX_CONDUCTAS`.
- Los formatos FD y FR nombran los anexos por su contenido, no por su letra.
- La letra queda fija en cada versión depositada; si se abre o cierra un centro y cambia el número de anexos, es una nueva versión (3.1).

### 2.4 Filas repetibles

| Tabla | Fuente | Regla |
| --- | --- | --- |
| Firmas | Acta CMRIT: una fila por representante de cada parte (`REP_EMPRESA_*`, `REP_TRABAJADORES_*`) | Tantas filas como `NUM_REPRESENTANTES_POR_PARTE`, mínimo 1 por parte. Columna «Firma» vacía |
| Art. 31, tabla II | `PERMISOS_EMPRESA` | Una fila por registro, en el orden del catálogo |
| Art. 31, tabla I, última fila | `PERMISO_LEY_*` | Una fila por permiso que agregue consultoría; vacía no se imprime |
| Anexo de centros | Catálogo de centros de trabajo (`CENTRO_*`) | Una fila por centro activo, numerada con `N`; solo con más de un centro |
| Anexo de horarios | Catálogo de jornadas (`TURNO_*`) | Una fila por turno activo de los centros de la Empresa. Con `TURNO_DESCANSO_TIPO` = Fijo: días laborables y días de descanso de la tabla. Con Rotativo: «`TURNO_DIAS_TRABAJO_SEMANA` días por semana» y «Rotativo». Tipo de jornada: el calculado con los horarios, nunca «Rotativa» |

### 2.5 Validaciones de los datos del RIT

| Validación | Efecto |
| --- | --- |
| `FECHA_ACTA_INTEGRACION` ≤ `FECHA_EMISION` | Bloqueo |
| `PRIMA_VACACIONAL_PCT` ≥ 25 | Bloqueo |
| `MESES_CANCELACION_ANTECEDENTES` ≥ `MESES_REINCIDENCIA` | Bloqueo |
| `PERMISOS_EMPRESA`: nombre, duración y salario obligatorios; ninguna fila duplica ni reduce un permiso de la tabla I | Bloqueo |
| Filas de la tabla I (permisos legales) | No editables ni eliminables por el cliente |
| Turnos del anexo de horarios: horas semanales ≤ jornada máxima legal vigente (tabla del sistema) | Bloqueo |
| Con más de un centro: cada centro con nombre, domicilio, estado y registro patronal IMSS | Bloqueo (resaltar el centro incompleto, 0.1) |
| Toda persona activa y todo turno pertenecen a un centro del catálogo de centros | Bloqueo |
| CURP repetida entre los integrantes de la CMRIT o entre las personas del Anexo 1 del acta | Bloqueo |
| Representante de las personas trabajadoras con clasificación Confianza en el organigrama | Bloqueo |
| `RIT_ANTERIOR` = Sí sin `FECHA_DEPOSITO_RIT_ANTERIOR` | Bloqueo |

### 2.6 Ajuste por reducción legal de la jornada (art. 8)

- Cuando entra en vigor una reducción de la jornada máxima (tabla del sistema: 48 h en 2026, 46 en 2027, 44 en 2028, 42 en 2029, 40 en 2030, cada cambio el 1 de enero), el sistema identifica los turnos del catálogo que la exceden.
- Calcula el horario ajustado con `REGLA_AJUSTE_JORNADA` (anticipar la salida del último día laborable de la semana, o anticipar en proporción la salida diaria) y genera, para las personas afectadas, el comunicado MOD-2 «Ajuste legal de jornada» del módulo 5 (es el «comunicado de horarios ajustados»), con alerta `DIAS_AVISO_AJUSTE_HORARIO` días naturales antes de la entrada en vigor.
- Las personas afectadas se identifican por la jornada de su versión de condiciones (registro, sección 2, versión de condiciones por persona). El lote lee esa jornada solo para armar su resumen; el anexo de horarios no cambia condiciones individuales.
- Este ajuste **no** crea una versión nueva del RIT ni genera la alerta de depósito.
- Si ningún turno excede la nueva jornada, no se genera nada.

---

## 3. Versiones, depósito y difusión

### 3.1 Estados del RIT

| Estado | Cómo se llega | Efecto |
| --- | --- | --- |
| Borrador | Al crear o modificar | Se imprime con marca de agua «BORRADOR» |
| Firmado | Se capturan `FECHA_EMISION` y `LUGAR_EMISION` y se marca la casilla «firmado por todos»; el archivo firmado es opcional (alerta si falta) | Alerta de depósito: «Deposite el Reglamento ante el CFCRL a más tardar el [`FECHA_EMISION` + 8 días]» |
| Depositado y vigente | Se capturan `RIT_FECHA_DEPOSITO` y `RIT_ACUSE_DEPOSITO` (archivo) | Se habilitan FR-1 y FR-2; esta versión pasa a ser la vigente y la anterior queda como histórica |

- Solo puede haber una versión vigente. Mientras una versión nueva no se deposita, el sistema sigue usando la vigente para todo (FR-1, FR-2, expedientes).
- Cada versión guarda: número de versión, fecha de emisión, fecha y acuse de depósito, archivo firmado y los datos con que se generó.

### 3.2 Alertas

| Alerta | Se activa | Bloquea |
| --- | --- | --- |
| Depósito pendiente | Versión firmada sin acuse; desde `FECHA_EMISION`, con vencimiento a los 8 días | No |
| «RIT modificado: pendiente de depósito» | Cambio en el catálogo de jornadas (alta o cambio de turno), en el catálogo de centros (con más de un centro), en `VAC_PROGRAMACION_MODO` o en `DIAS_EN_CASA_EMPRESA` | No. FR-1 y FR-2 siguen entregando la versión vigente |
| Revisión anual | 12 meses después de `RIT_FECHA_DEPOSITO` de la versión vigente (art. 87) | No |
| Constancias FR-1 pendientes | Personas activas sin FR-1 de la versión vigente | No |

- La integración del Comité no forma parte del RIT: cambiarla no genera alerta ni versión.
- Un cambio en el catálogo de jornadas aplica de inmediato a las altas nuevas. Para el personal vigente se genera el comunicado o convenio del módulo 5; nunca cambia en silencio sus condiciones.

### 3.3 FR-1, constancia de recibo

- Se genera en tres momentos (`FR1_MOMENTO`):
  - **Emisión:** al depositar la primera versión, una por persona activa.
  - **Ingreso:** en cada alta, con el kit de contratación.
  - **Modificación:** al depositar una versión nueva, una por persona activa.
- No se genera sin `RIT_ACUSE_DEPOSITO`. Siempre entrega la versión depositada vigente.
- `FR1_MEDIO` = Electrónico: imprime `RIT_ENLACE`, enlace al PDF de la versión vigente.
- Se firma con la modalidad de la persona (`FIRMA_MODALIDAD`) en sus tres momentos. Es autógrafa solo si la persona firma en papel, si falla la Plataforma o si se niega a firmar (dos testigos y envío al correo personal).
- Firma por la Empresa (`FIRMA_EMPRESA_NOMBRE`, `FIRMA_EMPRESA_CARGO`): el representante en el momento Ingreso (dentro del paquete de contratación); la persona de RH designada en `FIRMANTES_EMPRESA` en Emisión y Modificación; sin firmante de RH vigente, el representante, con alerta (especificación de firma electrónica, sección 11).
- `FR1_MEDIO` (Papel · Electrónico) solo indica cómo se entrega el ejemplar del RIT; no determina la firma.
- Con el RIT depositado, la FR-1 de ingreso sustituye a la fila `RIT_ENTREGA` del Anexo 3 del contrato.
- Cada FR-1 firmada se archiva en el expediente individual y alimenta el balance de FR-2.

### 3.4 FR-2, constancia de difusión

- Una por cada versión depositada, con una fila por centro de trabajo (`FIJACION_*`). La evidencia fotográfica es obligatoria por fila.
- `FR1_RECABADAS`, `FR1_NEGATIVAS` y `FR1_PENDIENTES` se calculan del registro de FR-1 de esa versión.
- No se genera sin `RIT_ACUSE_DEPOSITO`.

---

## 4. Expediente disciplinario

### 4.1 Rutas

| Tipo (`EXP_TIPO`) y nivel (`EXP_NIVEL`) | Formatos, en orden |
| --- | --- |
| Disciplinario, falta leve | FD-4. Revisión opcional ante el Comité dentro de 3 días naturales (regla b de 0) |
| Disciplinario, falta grave o muy grave | FD-1 → FD-2 → FD-3 |
| Daño o pérdida de bienes | FD-5. Si `FD5_RECONOCE` = No (o hay negativa a firmar): FD-1 → FD-2 → FD-3 con el bloque de daño |

Un expediente tiene un solo folio (`EXP_FOLIO`) para todos sus formatos.

### 4.2 Nivel de la falta

- `EXP_NIVEL` se deriva de la conducta más grave seleccionada en `EXP_CONDUCTAS_CATALOGO`: 1 a 21 leve, 22 a 43 grave, 44 a 60 muy grave.
- Excepciones que el sistema ofrece al seleccionar la conducta:
  - 20 y 21: casilla «daño considerable» (20) o «causó daño o riesgo» (21). Marcada, el nivel sube a grave.
  - 25: si el puesto de la persona tiene el atributo «crítico para la seguridad», el nivel es muy grave.
- 60 (ausentismo reiterado): solo se puede seleccionar si existe una alerta de patrón de ausentismo del módulo de permisos y licencias (indicadores `ALERTA_PATRON_*`). El expediente adjunta el historial de la alerta como evidencia. Las faltas del patrón que ya tienen medida firme no se vuelven a sancionar: sirven de antecedente y de evidencia (confirmado por el usuario el 12/11/2026).
- **Conducta intentada** (art. 78): casilla `EXP_TENTATIVA`. Marcada, el nivel baja uno (muy grave a grave, grave a leve). Variable nueva; ver la sección 8.
- La persona que captura no puede cambiar el nivel de otra forma.

### 4.3 Fechas y plazos

| Dato | Regla |
| --- | --- |
| `EXP_FECHA_CONOCIMIENTO_JEFATURA` | Obligatoria; no posterior a la fecha de captura |
| `EXP_FECHA_AVISO_COMITE` | Obligatoria; igual o posterior a la anterior. Si pasa del día siguiente a `EXP_FECHA_CONOCIMIENTO_JEFATURA`: alerta «Reporte tardío de la jefatura (conducta 43)» y botón «Abrir expediente a la jefatura», que crea un expediente nuevo con la conducta 43 precargada |
| `EXP_FECHA_LIMITE_NOTIFICACION` | La menor entre (a) `EXP_FECHA_CONOCIMIENTO_JEFATURA` + 30 días naturales y (b) el mismo día del mes siguiente a `EXP_FECHA_CONOCIMIENTO_JEFATURA` (prescripción de un mes; si ese día no existe, el último día del mes). Se imprime en FD-3 |
| Alertas del plazo | A 10, 5 y 2 días naturales del vencimiento. Vencido, FD-3 solo admite «Sin responsabilidad» y el expediente se cierra |
| `FD1_FECHA_AUDIENCIA` | Entre 1 y 5 días naturales después de `FD1_FECHA`; si cae en día de descanso de la persona, su siguiente día laborable (regla a). El sistema la propone; RH puede cambiarla dentro del plazo. Fuera de plazo: alerta y confirmación de RH |
| Reprogramación | Una sola vez, con causa justificada acreditada; la nueva fecha debe respetar `EXP_FECHA_LIMITE_NOTIFICACION` |
| `FD3_FECHA_NOTIFICACION` | Dentro de 5 días naturales después de `FD2_FECHA` y ≤ `EXP_FECHA_LIMITE_NOTIFICACION`. Si no cabe, alerta crítica |
| `FD3_SUSPENSION_INICIO` | A más tardar 10 días naturales después de `FD3_FECHA_NOTIFICACION`; si cae en día de descanso, el siguiente día laborable (regla a). `FD3_SUSPENSION_FIN` y `FD3_REINCORPORACION` se calculan contando los días de suspensión en días laborables del turno (regla c). Propuestas por el sistema, editables por RH |
| Revisión de falta leve | Dentro de 3 días naturales después de `FD4_FECHA`; si vence en día de descanso de la persona, se extiende a su siguiente día laborable (regla b) |

### 4.4 Medidas que admite cada nivel (escala del catálogo de conductas)

`FD3_REINCIDENCIA` = Sí cuando la persona tiene un expediente concluido con medida, del mismo nivel, con `FD3_FECHA_NOTIFICACION` dentro de los `MESES_REINCIDENCIA` meses anteriores. Las medidas con más de `MESES_CANCELACION_ANTECEDENTES` meses sin falta nueva no cuentan.

| Nivel | Sin reincidencia | Con reincidencia |
| --- | --- | --- |
| Leve (FD-4) | Sin medida · Amonestación verbal registrada · Amonestación escrita | Suspensión de 1 a 2 días: FD-4 no la admite; el sistema cambia la ruta a FD-1 → FD-3 |
| Grave (FD-3) | Sin responsabilidad · Amonestación escrita · Suspensión de 1 a 3 días | Sin responsabilidad · Suspensión de 4 a 8 días |
| Muy grave (FD-3) | Sin responsabilidad · Suspensión de 4 a 8 días | Sin responsabilidad · Suspensión de 8 días |

- «Propuesta de rescisión» se ofrece en FD-3, en cualquier nivel, solo si alguna conducta del expediente está en la tabla de correspondencia (sección 9).
- `EXP_POSIBLE_RESCISION` (párrafo de FD-1) se marca en automático con la misma regla; RH puede desmarcarla.
- Con «Propuesta de rescisión», el sistema notifica internamente a `RESCISION_RESPONSABLE` con la fecha límite; el formato no lo nombra. El aviso de rescisión no se genera en este módulo.

### 4.5 Daño o pérdida de bienes

- Los datos del bien (`BIEN_*`, `RESGUARDO_FECHA`) se toman del resguardo o de la carta responsiva del alta. Sin resguardo con valor de reposición: aviso «Sin resguardo con valor de reposición no procede descuento» y se ocultan los campos de descuento.
- `DESCUENTO_MONTO` ≤ `BIEN_VALOR_REPOSICION`, y el descuento por pago dentro de los límites legales de descuento por deudas (tabla del sistema). Bloqueo si se excede.
- `FD5_RECONOCE` = Sí: se genera el acuerdo de descuento con origen «Reconocimiento FD-5».
- `FD3_NEGLIGENCIA` = Sí: se genera el acuerdo de descuento con origen «Resolución FD-3».
- Regla del art. 27 (decisión del 31/10/2026): el descuento puede registrarse y la evidencia (FD-5 o FD-3) cargarse después; sin evidencia solo hay alertas, no bloqueo.
- Para el finiquito (módulo 4), una deducción por pérdida o daño solo se descuenta con expediente concluido.
- Art. 46: la investigación es la ruta de 4.1 (FD-5 y, sin reconocimiento, FD-1 → FD-3). Sin FD-5 con reconocimiento ni FD-3 con negligencia, el descuento queda en alerta (regla del art. 27).

### 4.6 Firmas, negativas y declaraciones

- Toda versión o manifestación de la persona trabajadora se escribe a mano en `[RECUADRO_MANUSCRITO]`. Si no sabe o no puede escribir, dicta a quien ella elija, se le lee, firma o pone su huella y firman dos testigos. Si se niega a escribir, se asienta la negativa con dos testigos y el procedimiento continúa.
- En cada formato, la bandera `FDx_NEGATIVA` (o `FR1_NEGATIVA`) muestra el bloque de negativa y hace obligatorios `TESTIGO_1_NOMBRE` y `TESTIGO_2_NOMBRE`, distintos de la persona y de la jefatura. En FD-1, FD-3 y FR-1 el sistema envía el documento a `PERSONA_CORREO` y registra la fecha de envío.
- **FD-1 a FD-5 se firman siempre de forma autógrafa**, aunque `FIRMA_MODALIDAD` = Electrónica. Se imprimen, se firman y se digitalizan al expediente; la casilla «firmado» basta para avanzar y la falta del archivo genera alerta (0.1).

### 4.7 Conservación

- El expediente se conserva durante la relación y `ANIOS_CONSERVACION_DISCIPLINARIOS` años después de la baja. Después, alerta de depuración (no se borra en automático).
- La persona trabajadora puede consultar su propio expediente (art. 86).

---

## 5. Otras reglas del sistema

| Regla | Detalle |
| --- | --- |
| Aclaraciones del registro de jornada (art. 13) | La persona solicita por la Plataforma dentro de `DIAS_ACLARACION_REGISTRO` días hábiles desde el cierre del periodo de pago; RH responde dentro de `DIAS_RESPUESTA_NOMINA` días hábiles. Sin solicitud, el registro se marca «conforme para nómina» |
| Correcciones del registro | Solo RH; obligatorio el soporte; se guarda quién, cuándo y por qué |
| Aclaraciones de nómina (art. 26) | Dentro de `DIAS_ACLARACION_NOMINA` días hábiles desde el pago; respuesta en `DIAS_RESPUESTA_NOMINA` |
| Horas extra (art. 17) | Orden previa de la jefatura por la Plataforma, con horas autorizadas. Tiempo registrado sin orden: se paga y alerta a RH (conducta 5) |
| Denuncias (art. 74) | Acuse dentro de `DIAS_ACUSE_DENUNCIA` días hábiles; opción anónima |
| Políticas (transitorio quinto) | Alerta si a `DIAS_EMISION_POLITICAS` días de la vigencia no están emitidas y acusadas las políticas del registro |
| Conducta 21 | Solo seleccionable si la política incumplida tiene acuse de la persona |
| Evidencia de permisos (art. 31) | La regla vive en el módulo de permisos y licencias: con un permiso de la tabla II sin evidencia a los 10 días hábiles, RH decide con `EVIDENCIA_DESCUENTO` si pasa a sin goce (precarga `EVIDENCIA_VENCIDA_EFECTO`); el sistema nunca descuenta solo y revierte en la nómina siguiente si la evidencia llega. Los permisos de la tabla I conservan el goce; alertas en los días 5 y 9 |
| Días computables para PTU (art. 31) | El módulo de PTU toma los días de los eventos del módulo de permisos y licencias con el criterio del art. 31 |
| Autorización de permisos (art. 30) | La ejecuta el módulo de permisos y licencias: cadena `CADENA_AUTORIZACION` (jefatura inmediata, RH y `DIRECTOR_AREA` si existe), plazo `AUTORIZACION_PLAZO_DIAS` por paso (1 por omisión), suplente, nadie autoriza su propio permiso. Los eventos de origen Ley también pasan por la cadena (decisión del usuario, 12/11/2026), con estas reglas: cada paso solo puede «Autorizar» o «Devolver para corrección» (aviso, fechas o evidencia); no existe «Negar». Única excepción: en la comisión del sindicato o del Estado, la cadena puede negar con motivo si el número de personas comisionadas perjudica la operación. Si llega la fecha sin autorización completa, RH registra el permiso legal y la ausencia no se marca como falta (registro 4.9) |
| Comisiones del sindicato o del Estado (art. 31, tabla I) | RH elige con o sin goce al otorgar cada una (`COMISION_GOCE`, módulo de permisos). Con contrato colectivo, manda lo que este disponga |

---

## 6. Plantillas

### 6.1 Dictamen, Reglamento y anexos

Texto completo para imprimir, tal como está en el maestro. Las tablas se imprimen como tablas; las filas repetibles siguen la sección 2.4. Los números de artículo y las remisiones se ajustan con la sección 2.2, y las letras de los anexos con la 2.3. Los títulos de capítulo, de anexo y de cada artículo («Artículo 1. Objeto.») van en negrita.

```text
DICTAMEN DE EMISIÓN DEL REGLAMENTO INTERIOR DE TRABAJO

| Dato | Contenido |
| --- | --- |
| Empresa | {{RAZON_SOCIAL}}[SI NOMBRE_COMERCIAL ≠ vacío] ({{NOMBRE_COMERCIAL}})[FIN SI] |
| RFC / Registro patronal | {{RFC}} / {{REGISTRO_PATRONAL}} |
| Domicilio | {{DOMICILIO_FISCAL}} |
| Actividad | {{ACTIVIDAD_ECONOMICA}} |
| Centros de trabajo | [SI NUM_CENTROS_TRABAJO = 1]{{DOMICILIOS_CENTROS_TRABAJO}}[FIN SI][SI NUM_CENTROS_TRABAJO > 1]{{NUM_CENTROS_TRABAJO}}, relacionados en el Anexo A[FIN SI] |
| Acta de integración de la Comisión | {{FECHA_ACTA_INTEGRACION}} |
| Sesión de aprobación | {{LUGAR_EMISION}}, {{FECHA_EMISION}} |

Considerando. La Comisión Mixta del Reglamento Interior de Trabajo (la «Comisión»), integrada conforme a la Ley Federal del Trabajo, elaboró el presente Reglamento con base en las propuestas de ambas representaciones y en la operación real del centro de trabajo.

Dictamen. Las dos representaciones de la Comisión aprueban el Reglamento Interior de Trabajo que se transcribe a continuación, con sus anexos, que forman parte integrante de él. La Coordinación lo depositará ante el Centro Federal de Conciliación y Registro Laboral dentro de los ocho días siguientes a su firma, y la Empresa lo difundirá en los términos de la misma Ley.

REGLAMENTO INTERIOR DE TRABAJO DE {{RAZON_SOCIAL}}

CAPÍTULO I. Disposiciones generales

Artículo 1. Objeto. Este Reglamento contiene las disposiciones obligatorias para {{RAZON_SOCIAL}}[SI NOMBRE_COMERCIAL ≠ vacío], conocida comercialmente como {{NOMBRE_COMERCIAL}},[FIN SI] (la «Empresa») y para las personas trabajadoras en el desarrollo de los trabajos de la Empresa, conforme a la Ley Federal del Trabajo (la «Ley»).

Artículo 2. A quién aplica. Aplica a todas las personas trabajadoras de la Empresa, de base o de confianza, cualquiera que sea la modalidad o duración de su contratación, y a quienes laboren en teletrabajo en lo que resulte compatible con esa modalidad.

No aplica al personal de contratistas, prestadores de servicios especializados, proveedores ni visitantes, que no tienen relación de trabajo con la Empresa. Su conducta dentro de las instalaciones se regula mediante los contratos respectivos y las reglas de acceso y seguridad, cuyo incumplimiento autoriza a la Empresa a negar o retirar el acceso.

Artículo 3. Dónde aplica. Rige en todos los centros de trabajo de la Empresa, actuales y futuros, y en los lugares donde las personas trabajadoras realicen comisiones o actividades encomendadas por ella.[SI NUM_CENTROS_TRABAJO > 1] Los centros de trabajo en operación se relacionan en el Anexo A; los que se abran después quedan sujetos a este Reglamento desde su apertura y se incorporan al Anexo A en su siguiente actualización.[FIN SI]

Artículo 4. Relación con otros instrumentos. Las relaciones de trabajo se rigen, en este orden, por la Ley y las normas oficiales aplicables, el contrato colectivo si existe, el contrato individual, este Reglamento y las políticas internas. En caso de contradicción prevalece la disposición más favorable a la persona trabajadora.

Las políticas internas desarrollan este Reglamento y no pueden contradecirlo. Son obligatorias una vez comunicadas con acuse de recibo. Las vigentes a la fecha se enlistan en el registro de políticas que Recursos Humanos mantiene a disposición de las personas trabajadoras.

Artículo 5. Definiciones. Para efectos de este Reglamento:

- Comisión: la Comisión Mixta del Reglamento Interior de Trabajo.
- Comité: el Comité de Integridad y Disciplina previsto en el Capítulo XII.
- Jefatura inmediata: la persona a quien la persona trabajadora reporta directamente, o quien la sustituya.
- Recursos Humanos: el área o persona designada por la Empresa para administrar personal.
- Plataforma: el sistema, correo institucional o aplicación que la Empresa designe por escrito para solicitudes, avisos y registros.
- Días hábiles: los días laborables del centro de trabajo de que se trate.

Artículo 6. Difusión. La Empresa entregará un ejemplar de este Reglamento a cada persona trabajadora, en papel o por medio electrónico, con constancia de recibo (formato FR-1); lo fijará en los lugares más visibles de cada centro de trabajo, y lo entregará a quien ingrese en lo sucesivo como parte de su inducción. Las constancias se integrarán al expediente de cada persona, y la fijación se acreditará con la constancia de difusión (formato FR-2).

Artículo 7. Comunicaciones. Son medios válidos de comunicación entre las partes el escrito con acuse y la Plataforma. Las personas trabajadoras deben mantener actualizados su domicilio, teléfono y correo de contacto ante Recursos Humanos.

CAPÍTULO II. Jornada, horarios y asistencia

Artículo 8. Horarios. Las horas de entrada y salida, el tiempo para comidas, los periodos de reposo y los días de descanso de cada centro de trabajo y turno son los del Anexo B. El horario individual se precisa en el contrato de cada persona trabajadora.

Los horarios nunca excederán la jornada máxima que establezca la Ley en cada momento. Cuando una reforma legal reduzca la jornada máxima, los horarios del Anexo B se entenderán reducidos de pleno derecho desde la entrada en vigor de la reducción, {{REGLA_AJUSTE_JORNADA}}, sin disminución del salario ni de las prestaciones. La Empresa comunicará los horarios ajustados con al menos {{DIAS_AVISO_AJUSTE_HORARIO}} días naturales de anticipación, sin que ello requiera modificar este Reglamento.

Artículo 9. Inicio y término de la jornada. La jornada inicia con el registro de entrada y termina con el de salida, en el centro de trabajo asignado o en el lugar de la comisión encomendada. El tiempo que la persona trabajadora destine dentro de las instalaciones a colocarse o retirarse uniforme o equipo de protección obligatorio forma parte de la jornada.

[SI REPSE_EMPRESA = Sí]

Para las personas trabajadoras que prestan servicios especializados a clientes de la Empresa:

1. Si su centro de trabajo es el de la Empresa, la jornada inicia y termina en el lugar que indique la orden de servicio del día, sea la Empresa o la instalación de un cliente.
2. Si su centro de trabajo es la instalación de un cliente conforme al oficio de asignación, la jornada inicia y termina en ella.
3. El tiempo de traslado entre la Empresa y un cliente, o entre clientes, durante la jornada es tiempo de trabajo. Cada llegada a una instalación y cada salida de ella se registran en el sistema de registro de jornada.
4. Si un traslado ordenado obliga a prolongar la jornada, el tiempo excedente se rige por los artículos 17 y 18 de este Reglamento.
5. La Empresa cubre o reembolsa los gastos de los traslados que ordene durante la jornada, conforme a la política de viáticos y traslados.

[FIN SI]

Artículo 10. Comida y reposo. En jornada continua se concede un reposo de por lo menos media hora. Las condiciones específicas de cada persona trabajadora son las pactadas al contratarla. Sin excepción, todas las personas trabajadoras registran el inicio y el término de estos reposos por los medios que designe la Empresa.

Artículo 11. Pausas y prevención de la fatiga. Además del reposo del artículo anterior, la Empresa podrá establecer pausas para prevenir la fatiga y los riesgos asociados a ella. Las pausas son tiempo de trabajo, no se descuentan de la jornada y no pueden acumularse ni usarse para salir antes. Se aplican así:

1. Trabajo de pie: los descansos y el uso de asientos del artículo 54.
2. Tareas repetitivas, manejo manual de cargas o posturas forzadas: pausas activas conforme a la política de ergonomía y pausas activas.
3. Conducción de vehículos, operación de maquinaria, puestos críticos para la seguridad o jornadas con horas extra: las medidas de la política de prevención de la fatiga, como límites de conducción continua, descanso mínimo entre jornadas y rotación de tareas.
4. Factores psicosociales: la política del artículo 72.

La frecuencia y duración de las pausas se fijan en esas políticas con base en el diagnóstico de la Comisión de Seguridad e Higiene. Quien advierta en sí o en otra persona una fatiga que comprometa la seguridad avisará a la jefatura, que concederá una pausa o reasignará la tarea; el aviso nunca es motivo de sanción.

Artículo 12. Descanso semanal. Los días de descanso son los del Anexo B.[SI TURNOS_ROTATIVOS = Sí] En los turnos con descanso rotativo, el día de descanso se asigna conforme al contrato de cada persona trabajadora, sin que transcurran más de seis días consecutivos de trabajo.[FIN SI] El trabajo en domingo o en el día de descanso se paga en los términos de la Ley.

Artículo 13. Registro de jornada. Cada persona trabajadora registrará personalmente su entrada y su salida en el sistema electrónico que designe la Empresa, conforme a la Ley y a las disposiciones de la STPS. Además:

1. Nadie puede registrar la asistencia de otra persona ni alterar registros.
2. Quien no otorgue o revoque su consentimiento para el uso de datos biométricos registra su asistencia por el medio alterno que designe la Empresa, sin consecuencia alguna. El mismo medio se usa cuando el sistema falla.
3. Si tampoco es posible usar el medio alterno, la persona avisará a su jefatura el mismo día y ambas firmarán un registro manual que Recursos Humanos capturará.
4. Solo Recursos Humanos puede corregir un registro, con el soporte que lo justifique, dejando constancia de quién y por qué lo corrigió.
5. La persona trabajadora puede consultar sus registros y solicitar su aclaración por la Plataforma dentro de los {{DIAS_ACLARACION_REGISTRO}} días hábiles siguientes al cierre de cada periodo de pago. Recursos Humanos responde dentro de los {{DIAS_RESPUESTA_NOMINA}} días hábiles siguientes. Sin aclaración en ese plazo, el registro se tiene por conforme para el cálculo de la nómina, sin perjuicio de los derechos de la persona trabajadora.

Artículo 14. Puntualidad y tolerancia. Se concede una tolerancia de {{TOLERANCIA_MIN}} minutos a la hora de entrada. Después de ella, la llegada es retardo. La acumulación de retardos tiene las consecuencias disciplinarias del Anexo C.

Artículo 15. Aviso y justificación de ausencias. Quien no pueda asistir avisará a su jefatura por la Plataforma o por teléfono antes del inicio de su turno o, si la causa es imprevisible, dentro de los 60 minutos siguientes. Lo hará personalmente o por medio de un tercero cuando esté impedida. La ausencia se justificará dentro de los 2 días hábiles siguientes al regreso, con la incapacidad del IMSS o el documento que acredite la causa. La ausencia sin aviso ni justificación es falta injustificada.

El aviso no implica por sí solo la justificación de la ausencia, pues esta deberá ser valorada por Recursos Humanos en conjunto con la dirección y la opinión de la jefatura inmediata.

Artículo 16. Salidas durante la jornada. Ninguna persona puede ausentarse durante su jornada sin autorización previa, que se tramita conforme al artículo 30, por la Plataforma o por escrito; la jefatura inmediata es el primer nivel de autorización. La salida y el regreso se registran en los medios designados.

Artículo 17. Horas extra. Solo se labora tiempo extraordinario por orden previa de la jefatura, por escrito o por la Plataforma, con indicación de las horas autorizadas. La orden respetará los límites diarios, semanales y de jornada total que establezca la Ley, y las horas se pagan en los términos de esta, en la nómina del periodo en que se laboraron. Las personas menores de 18 años no laboran horas extra; las personas embarazadas o en lactancia, conforme al Capítulo X.

Artículo 18. Tiempo laborado sin orden. La jefatura debe impedir que se labore tiempo extraordinario sin orden. El tiempo efectivamente laborado y registrado se paga siempre; la falta de orden previa se atiende por vía disciplinaria respecto de quien la omitió.

Artículo 19. Prolongación por siniestro. En caso de siniestro o riesgo inminente que ponga en peligro la vida de las personas o la existencia de la Empresa, la jornada podrá prolongarse por el tiempo estrictamente indispensable, y esas horas se pagarán en los términos de la Ley.

Artículo 20. Interrupción de labores por emergencia. Ante una evacuación, falla de suministros, contingencia ambiental u otra emergencia que impida trabajar con seguridad, la jefatura podrá interrumpir las labores. Las personas trabajadoras permanecerán a disposición de la Empresa, el tiempo se computa como laborado y podrán asignárseles otras tareas compatibles con su puesto.

Artículo 21. Suspensión colectiva. La suspensión de las relaciones de trabajo por causas no imputables a las partes, incluida la contingencia sanitaria declarada por la autoridad, solo procede en los supuestos y con el procedimiento que establece la Ley.

[SI DIAS_EN_CASA_EMPRESA = Sí]

Artículo 22. Días en casa. Este artículo aplica a quienes laboren parte o toda su jornada desde su domicilio, en teletrabajo o en trabajo híbrido, conforme a su contrato.

1. Política aplicable. La solicitud, la autorización, las obligaciones, el cambio y la revocación de los días en casa y de los horarios flexibles se rigen por la política de trabajo híbrido y jornada flexible de la Empresa. Sin autorización conforme a esa política, no se labora en casa ni con horario distinto al pactado.
2. Registro de jornada. En días en casa, la entrada y la salida se registran en el sistema electrónico de la Empresa, sin captura de ubicación. Las horas extra requieren la orden previa del artículo 17.
3. Contacto y desconexión. La persona trabajadora atiende los medios de contacto designados durante su jornada y, fuera de ella, tiene derecho a la desconexión, conforme a su contrato.
4. Herramientas e información. Usa el equipo y las cuentas asignados conforme a la carta responsiva y a la política de uso de tecnologías, y protege la información de la Empresa en su domicilio.
5. Regreso a la modalidad presencial. El regreso no disminuye el salario ni las condiciones de trabajo.
6. Teletrabajo. En teletrabajo, el cambio de modalidad y el regreso a la modalidad presencial se pactan por escrito, y la Empresa cumple además las obligaciones especiales que establecen la Ley y la norma oficial aplicable.

[FIN SI]

CAPÍTULO III. Salario y pago

Artículo 23. Salario. El salario de cada persona trabajadora es el pactado en su contrato, nunca inferior al mínimo que corresponda, y se fija con criterios objetivos: a trabajo igual, en puesto, jornada y condiciones de eficiencia iguales, salario igual. Sus modificaciones constan por escrito.

Artículo 24. Periodicidad y forma de pago. El salario se paga con la periodicidad que corresponde a su puesto, según el contrato y dentro de los plazos máximos de la Ley. Se paga en moneda nacional, por depósito o transferencia a la cuenta que designe la persona trabajadora con su consentimiento, o en efectivo. Las periodicidades de pago que usa la Empresa son: {{PERIODICIDADES_PAGO_EMPRESA}}.

Artículo 25. Día y lugar de pago. Los días de pago son: {{DIAS_PAGO_RESUMEN}}. Si un día de pago es inhábil, el pago se hará el día hábil anterior. El pago en efectivo se hace en el centro de trabajo, durante la jornada o inmediatamente después de su terminación.

Artículo 26. Recibos y aclaraciones. Cada pago se documenta con el comprobante fiscal correspondiente, que detalla percepciones y deducciones. La persona trabajadora puede pedir aclaraciones a Recursos Humanos dentro de los {{DIAS_ACLARACION_NOMINA}} días hábiles siguientes al pago. Recursos Humanos responderá en {{DIAS_RESPUESTA_NOMINA}} días hábiles y las diferencias a su favor se pagarán en la nómina siguiente.

Artículo 27. Descuentos. Solo se hacen los descuentos que permite la Ley. Los descuentos por deudas con la Empresa (anticipos, pagos en exceso, errores, pérdidas, averías o compra de productos de la Empresa) requieren:

1. Reconocimiento de la deuda por la persona trabajadora, con su monto y número de pagos, o, tratándose de pérdidas o averías, la determinación de responsabilidad del artículo 46.
2. Que la deuda y cada descuento respeten los límites que fija la Ley.
3. Que no genere intereses.

Artículo 28. Pagos en exceso. Si se detecta un pago en exceso, Recursos Humanos lo notificará por escrito y propondrá un plan de recuperación conforme al artículo anterior. La Empresa no retendrá salario de forma unilateral.

Artículo 29. Constancias. La Empresa expedirá, en los casos y plazos que establece la Ley, las constancias de días trabajados y salario percibido, de servicios al terminar la relación y de antigüedad y periodo vacacional. Las solicitudes se presentan a Recursos Humanos por la Plataforma o el medio asignado para ello.

CAPÍTULO IV. Ausencias, permisos y licencias

Artículo 30. Cómo se solicita un permiso. Todo permiso se solicita por la Plataforma o en el formato de la Empresa, indicando tipo, fechas y horario. Todo permiso lo autorizan, en este orden, la jefatura inmediata, Recursos Humanos y, cuando exista, la dirección del área. Cada nivel resuelve dentro del plazo que fije la Empresa en la Plataforma, que a falta de otro es el día hábil siguiente a que recibe la solicitud. En los permisos que otorga la Ley, la autorización se limita a verificar el aviso, las fechas y la evidencia, y a programar la ausencia; la solicitud puede devolverse para su corrección, pero no negarse, salvo en los casos en que la Ley lo permite. Si llega la fecha del permiso legal sin que concluya la autorización, Recursos Humanos lo registra y la ausencia no se considera falta. Cuando la causa sea urgente, el aviso puede darse por teléfono y la solicitud formal se completa al regreso.

Artículo 31. Permisos y licencias.

I. Permisos y licencias que otorga la Ley. Se otorgan siempre, en los términos de la Ley, y no pueden suprimirse ni reducirse:

| Permiso | Aviso previo | Duración | Salario | Evidencia (entregar dentro de 10 días hábiles) |
| --- | --- | --- | --- | --- |
| Paternidad o adopción | 8 días antes de la fecha probable, o en cuanto se conozca | La que establezca la Ley | Con goce | Acta de nacimiento o constancia de adopción |
| Maternidad y adopción (madres) | Al obtener el certificado del IMSS | La que establezca la Ley | Conforme a la Ley y a la Ley del Seguro Social | Certificado de incapacidad del IMSS |
| Hijos menores con cáncer | Al obtener la licencia del IMSS | La que expida el IMSS | Conforme a la Ley del Seguro Social | Licencia del IMSS |
| Votar en elecciones populares o en procesos de revocación de mandato; servicios de jurado, electorales o censales | En cuanto se conozca | El tiempo necesario | Con goce | Constancia, cuando exista |
| Comisión accidental o permanente del sindicato o del Estado | Con la oportunidad debida. Procede siempre que el número de personas comisionadas no perjudique la operación | La de la comisión. En la permanente, la persona conserva su puesto y sus derechos si regresa dentro del plazo que fija la Ley | Con o sin goce, según lo determine la Empresa al otorgarla. Sin goce, no se descuenta el tiempo que la persona compense con un tiempo igual de trabajo efectivo | Oficio o nombramiento de la comisión |
| {{PERMISO_LEY_NUEVO}} | {{PERMISO_LEY_AVISO}} | {{PERMISO_LEY_DURACION}} | {{PERMISO_LEY_SALARIO}} | {{PERMISO_LEY_EVIDENCIA}} |

II. Permisos que otorga la Empresa. Además, la Empresa otorga los permisos siguientes:

| Permiso | Aviso previo | Duración | Salario | Evidencia (entregar dentro de 10 días hábiles) |
| --- | --- | --- | --- | --- |
| Fallecimiento de familiar | Por cualquier medio, el mismo día | Según el artículo 32 | Con goce | Acta de defunción |
| Matrimonio | 15 días naturales | {{DIAS_PERMISO_MATRIMONIO}} días, por una sola ocasión | Con goce | Acta de matrimonio |
| Accidente grave u hospitalización de cónyuge, hijos o padres | Inmediato | Hasta {{DIAS_PERMISO_HOSPITALIZACION}} días por evento | {{GOCE_PERMISO_HOSPITALIZACION}} | Constancia médica u hospitalaria |
| Adaptación en guardería | 5 días hábiles | Días y horario que indique la guardería, hasta {{DIAS_ADAPTACION_GUARDERIA}} días | Con goce | Constancia de la guardería |
| Readaptación en guardería | 5 días hábiles | La necesaria | Sin goce, o a cuenta de vacaciones si la persona lo pide por escrito | Constancia de la guardería |
| Citas médicas propias o de hijos menores | 2 días hábiles, salvo urgencia | Hasta {{HORAS_CITA_MEDICA}} horas, {{CITAS_MEDICAS_AL_MES}} veces al mes | Con goce | Comprobante de asistencia |
| Asuntos personales | 5 días hábiles | Hasta {{DIAS_ASUNTOS_PERSONALES}} días al año; adicionales a criterio de quienes autorizan conforme al artículo 30 | Con goce los primeros {{DIAS_ASUNTOS_PERSONALES}}; sin goce los adicionales | No requiere |
| Permiso por horas | 1 día hábil | Menos de 4 horas | Con goce, hasta {{PERMISOS_HORAS_AL_MES}} veces al mes; después, sin goce | No requiere |
| Permiso por horas | 1 día hábil | 4 horas o más | Sin goce | No requiere |

Los permisos con goce no se acumulan de un año a otro ni se pagan si no se usan. Los permisos de medio tiempo se otorgan en proporción a la jornada.

Si la evidencia de un permiso de la tabla II no se entrega en el plazo, la Empresa puede tenerlo por otorgado sin goce de salario; si la persona trabajadora la entrega después, la diferencia se le paga en la nómina siguiente. Los permisos de la tabla I conservan el salario que les corresponde aunque la evidencia se entregue tarde.

Para la participación en las utilidades se computan como días trabajados los laborados, los de vacaciones, los de permisos con goce de salario y los de incapacidad por riesgo de trabajo o por maternidad. No se computan las faltas, los permisos sin goce, las suspensiones ni las incapacidades por enfermedad general.

[SI PERMISO_FALLECIMIENTO = Sí]

Artículo 32. Días por fallecimiento.

| Familiar | Días con goce |
| --- | --- |
| Cónyuge, concubina o concubinario, hijas o hijos | {{DIAS_FALLECIMIENTO_GRADO_1}} |
| Madre, padre, hermanas o hermanos | {{DIAS_FALLECIMIENTO_GRADO_2}} |
| Abuelas o abuelos, nietas o nietos, suegra o suegro | {{DIAS_FALLECIMIENTO_GRADO_3}} |

Si el funeral es en otra ciudad a más de {{KM_FUNERAL_FORANEO}} km, se agrega {{DIAS_FUNERAL_FORANEO}} día sin goce a solicitud de la persona trabajadora.

[FIN SI]

Artículo 33. Negativa. Los permisos que otorga la Ley no pueden negarse. Los demás solo pueden negarse por escrito y con motivo: falta de requisitos subsanables, o una necesidad operativa concreta que se expresará en la respuesta, proponiendo otra fecha cuando sea posible. La falta de respuesta no equivale a autorización; la persona podrá acudir a Recursos Humanos, que resolverá el mismo día.

Artículo 34. Enfermedad general. Quien enferme avisará conforme al artículo 15 y entregará la incapacidad del IMSS, física o digital, dentro de los 2 días hábiles siguientes a su expedición. [SI PAGO_DIAS_ESPERA = Sí] La Empresa pagará al 100% los tres días de espera que no subsidia el IMSS. [FIN SI] Los riesgos de trabajo se rigen por el Capítulo IX.

CAPÍTULO V. Vacaciones

Artículo 35. Días de vacaciones. Las personas trabajadoras disfrutan cada año de los días de vacaciones pagadas que establezca la Ley según su antigüedad.

Artículo 36. Programación y disfrute. [SI VAC_PROGRAMACION_MODO = Calendario anual]Recursos Humanos elaborará en {{MES_CALENDARIO_VACACIONES}} el calendario anual de vacaciones, considerando las preferencias de las personas trabajadoras y las necesidades operativas.[FIN SI][SI VAC_PROGRAMACION_MODO = Periodos de solicitud por antigüedad]La Empresa establece cada año los periodos en que las personas trabajadoras solicitan sus vacaciones, por grupos según su antigüedad, comenzando por el de mayor antigüedad, y los da a conocer con anticipación. Cuando en un área las solicitudes para las mismas fechas excedan el número de personas que pueden estar de vacaciones al mismo tiempo, las fechas se asignan por orden de antigüedad y a quien no alcance lugar se le proponen otras. Concluidos los periodos de solicitud, las vacaciones pendientes se solicitan en fechas libres.[FIN SI][SI VAC_PROGRAMACION_MODO = A solicitud]Cada persona trabajadora solicita sus vacaciones por la Plataforma dentro del periodo que la Ley fija para concederlas, considerando las necesidades operativas.[FIN SI] Las vacaciones se conceden dentro del plazo que fija la Ley. La persona trabajadora disfrutará en forma continua el periodo mínimo que establezca la Ley y podrá distribuir el resto como lo requiera, solicitándolo por la Plataforma con {{DIAS_ANTICIPACION_VACACIONES}} días naturales de anticipación. Las vacaciones no pueden compensarse con dinero, salvo en los casos que permite la Ley.

La Empresa puede señalar, por escrito y con su motivo, los días en que no se programan vacaciones por necesidades operativas o de capacitación, y el número de personas de cada área que pueden estar de vacaciones al mismo tiempo, siempre que cada persona trabajadora pueda disfrutar sus vacaciones dentro del plazo que fija la Ley. Esas medidas no modifican, sin la conformidad de la persona trabajadora, las vacaciones que haya solicitado o que se le hayan autorizado antes de que la Empresa las dé a conocer.

La solicitud no implica autorización automática: se valida y se autoriza conforme al artículo 30.

Artículo 37. Prima vacacional. La prima vacacional es del {{PRIMA_VACACIONAL_PCT}}% del salario de los días de vacaciones, sin ser inferior a la mínima legal, y se paga {{MOMENTO_PAGO_PRIMA}}.

CAPÍTULO VI. Derechos y obligaciones de las partes

Artículo 38. Obligaciones de la Empresa. Además de las que establece la Ley, la Empresa:

1. Pondrá a disposición de las personas trabajadoras la Plataforma y los formatos para solicitudes, avisos y acuses.
2. Proporcionará los útiles, herramientas, equipo y asientos necesarios conforme a los Capítulos VII y VIII.
3. Llevará el registro de jornada y expedirá las constancias previstas en este Reglamento.
4. Tratará con respeto a las personas trabajadoras, incluso al señalar faltas, y no tomará represalias por el ejercicio de derechos, la presentación de denuncias de buena fe o la participación en comisiones mixtas.
5. Impartirá la capacitación que corresponda y la inducción sobre este Reglamento.

Artículo 39. Obligaciones de las personas trabajadoras. Además de las que establece la Ley, las personas trabajadoras deben:

1. Cumplir este Reglamento y las políticas internas que se les hayan comunicado.
2. Desempeñar el trabajo con la intensidad, cuidado y esmero apropiados, conforme a las instrucciones de la Empresa relacionadas con el trabajo contratado.
3. Tratar con respeto a compañeros, jefaturas, clientes, proveedores y visitantes.
4. Asistir a las capacitaciones programadas y presentar las evaluaciones correspondientes.
5. Cuidar los bienes de la Empresa y guardar reserva sobre la información confidencial a que tengan acceso.
6. Declarar a Recursos Humanos cualquier conflicto de interés, conforme al artículo 69.
7. Avisar de inmediato los riesgos, fallas y accidentes que adviertan, conforme al Capítulo IX.
8. Someterse a los exámenes médicos previstos en el Capítulo IX.

Artículo 40. Facultad de dirección. La Empresa organiza y dirige el trabajo: asigna las funciones propias de cada puesto, define métodos y procedimientos, emite políticas y supervisa su cumplimiento. Las condiciones pactadas en el contrato individual solo se modifican por acuerdo de las partes o en los casos que prevé la Ley.

Artículo 41. Comisiones mixtas. La Empresa integrará y facilitará el funcionamiento de las comisiones mixtas que exige la Ley. La participación de las personas trabajadoras es un derecho y sus representantes son designados o elegidos por ellas. El personal de confianza participa en la designación o en la elección, pero no puede ser representante de las personas trabajadoras. El tiempo dedicado a cualquier comisión mixta es tiempo de trabajo con goce de salario. [SI MOD_PRUEBA = Sí]Antes de dar por terminada una relación al vencer el periodo de prueba o de capacitación inicial, la Empresa solicita la opinión de la Comisión Mixta de Capacitación, Adiestramiento y Productividad.[FIN SI]

Artículo 42. Capacitación. La capacitación se imparte preferentemente dentro de la jornada. Si se imparte fuera de ella por acuerdo con la persona trabajadora, el tiempo se paga como tiempo de trabajo. La asistencia se acredita con lista firmada o registro electrónico, y las constancias de habilidades se integran al expediente.

Artículo 43. Conservación de documentos. La Empresa conservará contratos, nóminas, recibos de salario, controles de asistencia, registros de jornada y comprobantes de pago de prestaciones durante los plazos que establecen la Ley y las disposiciones de la STPS. Los expedientes disciplinarios se conservarán durante la relación de trabajo y {{ANIOS_CONSERVACION_DISCIPLINARIOS}} años después.

CAPÍTULO VII. Herramientas, equipo, uniformes y limpieza

Artículo 44. Entrega y resguardo. La Empresa entrega a cada persona trabajadora, en buen estado, las herramientas, equipo, uniformes y equipo de protección personal que requiere su puesto. La entrega consta en un resguardo firmado que describe cada bien, su estado y su valor de reposición, y que se actualiza en cada cambio o reposición.

Artículo 45. Uso y cuidado. Los bienes se usan solo para el trabajo, se conservan en buen estado y se guardan en el lugar que designe la Empresa. Cualquier falla, daño o pérdida se reporta a la jefatura el mismo día. La reposición por desgaste normal se solicita entregando el bien desgastado.

Artículo 46. Daño o pérdida. La persona trabajadora no responde del deterioro por el uso normal, caso fortuito, fuerza mayor o mala calidad del bien. Si el daño o la pérdida obedece a su negligencia se iniciará una investigación para la determinación o deslinde de responsabilidad. La investigación se sigue conforme a los artículos 80 y 81. El descuento solo procede si la persona trabajadora reconoce su responsabilidad o esta se determina en la investigación, y conforme al artículo 27.

Artículo 47. Limpieza. Cada persona trabajadora deja limpios y ordenados su área, herramientas y equipo durante los últimos {{MINUTOS_LIMPIEZA}} minutos de su jornada, tiempo que forma parte de ella. [SI HORARIO_LIMPIEZA_GENERAL ≠ vacío]La limpieza general de las instalaciones a cargo de las personas trabajadoras se realiza {{HORARIO_LIMPIEZA_GENERAL}}, y la de maquinaria conforme al programa de mantenimiento.[FIN SI]

Artículo 48. Mantenimiento. La Empresa mantendrá un programa {{PERIODICIDAD_MANTENIMIENTO}} de revisión y mantenimiento de herramientas, equipo y maquinaria, con bitácora de revisiones, reparaciones y sustituciones.

Artículo 49. Uniformes y vestimenta. El uso del uniforme y la vestimenta se rige por el código de vestimenta. Cuando el uniforme o el equipo sea necesario por seguridad, su uso es obligatorio durante toda la jornada.

[SI VEHICULOS_ASIGNADOS = Sí]

Artículo 50. Vehículos. Quien tenga asignado un vehículo tendrá las obligaciones siguientes:

- Lo utilizará solo para fines de trabajo;
- Debe contar con licencia de conducir vigente;
- Debe respetar la legislación en materia de vialidad aplicable a la zona geográfica;
- Observar de manera estricta lo establecido en la política de vehículos.

[FIN SI]

Artículo 51. Herramientas digitales. Las cuentas, equipos y sistemas de la Empresa son de uso laboral, personal e intransferible. Cada usuario es responsable del correcto uso de sus cuentas digitales. La Empresa puede supervisar su uso conforme a la política de tecnologías comunicada previamente y a la legislación de protección de datos personales. Al terminar la relación, la persona trabajadora devuelve equipos e información y no conserva copias.

CAPÍTULO VIII. Instalaciones, áreas comunes y asientos

Artículo 52. Acceso a áreas. Cada persona trabajadora accede a su área de trabajo y a las áreas comunes. Las áreas restringidas, señaladas como tales, requieren autorización. Fuera de su horario, solo se permanece en las instalaciones con autorización de la jefatura. El ingreso de personas ajenas requiere el registro y la autorización que fijen las reglas de acceso.

Artículo 53. Áreas comunes. El comedor, los sanitarios y las áreas de descanso se usan para su fin, se mantienen limpios, sin obstruir accesos ni salidas, y los utensilios comunes se dejan en su lugar. Los alimentos se consumen en el comedor o en las áreas autorizadas, no en las áreas de producción donde la Empresa lo prohíba por seguridad o higiene.

Artículo 54. Asientos y descansos para quienes trabajan de pie. Conforme a la Ley y a las disposiciones de la STPS sobre factores de riesgo por bipedestación:

1. La Empresa provee asientos o sillas con respaldo suficientes, en el puesto de trabajo cuando la tarea lo permite o, si no, en áreas de descanso señalizadas cercanas.
2. Quien trabaje de pie puede usar el asiento durante sus funciones cuando la tarea lo permita, y tiene además descansos de {{MINUTOS_DESCANSO_BIPEDESTACION}} minutos cada {{HORAS_ENTRE_DESCANSOS_BIPEDESTACION}} horas, que no se descuentan de la jornada, en tanto la Comisión de Seguridad e Higiene determine otra frecuencia con base en el diagnóstico de riesgos.
3. Las personas trabajadoras usan y cuidan los asientos, reportan sus fallas a la Comisión de Seguridad e Higiene y participan en la capacitación sobre su uso.
4. Quien presente molestias relacionadas con la postura será canalizado a atención médica.

Ninguna persona trabajadora será obligada a permanecer de pie durante toda su jornada.

CAPÍTULO IX. Seguridad y salud en el trabajo

Artículo 55. Marco preventivo. La Empresa aplica el Reglamento Federal de Seguridad y Salud en el Trabajo y las normas oficiales que corresponden a su actividad. La Comisión de Seguridad e Higiene realiza los recorridos de verificación y propone medidas, y la Empresa mantiene el diagnóstico y el programa de seguridad y salud.

Artículo 56. Medidas preventivas obligatorias. Las personas trabajadoras deben:

1. Usar durante toda la tarea el equipo de protección personal que su puesto requiera, conforme a la capacitación recibida.
2. Seguir los procedimientos seguros de trabajo, sin retirar guardas ni inhabilitar dispositivos de seguridad.
3. Llevar el cabello recogido y no portar cadenas, anillos, pulseras ni ropa suelta cerca de maquinaria en movimiento.
4. Respetar la señalización y las áreas restringidas.
5. No fumar ni vapear fuera de las áreas designadas, que estarán al aire libre y lejos de materiales inflamables.
6. Mantener ordenada su área y depositar los residuos en los contenedores clasificados.

Ante un peligro grave e inminente, la persona trabajadora puede detener la tarea y avisar de inmediato a su jefatura, sin que ello sea motivo de sanción.

Artículo 57. Emergencias. La Empresa cuenta con brigadas de emergencia integradas por personas capacitadas, y realiza al menos {{SIMULACROS_AL_ANIO}} simulacros al año. Todas las personas trabajadoras participan en los simulacros. Los equipos contra incendio, rutas de evacuación, señales y planos no se obstruyen ni se alteran.

Artículo 58. Primeros auxilios. Cada centro de trabajo tiene al menos un botiquín señalizado y de fácil acceso, cuyo contenido se define según la evaluación de riesgos. La persona responsable designada revisa su contenido cada mes, lo repone y lleva el registro. El procedimiento de primeros auxilios[SI UBICACION_PROCEDIMIENTO_PRIMEROS_AUXILIOS ≠ vacío] está disponible en {{UBICACION_PROCEDIMIENTO_PRIMEROS_AUXILIOS}} y[FIN SI][SI UBICACION_PROCEDIMIENTO_PRIMEROS_AUXILIOS = vacío] lo conserva la persona responsable designada y[FIN SI] se difunde en la capacitación.

Artículo 59. Exámenes médicos. La Empresa tiene la obligación de practicar exámenes médicos a las personas trabajadoras, por lo que estas estarán sujetas a la aplicación de exámenes médicos de manera periódica.

Los exámenes se practican por el médico o la institución que esta designe. Los resultados serán tratados de manera confidencial y no podrán usarse para ningún acto de discriminación. Su uso será para verificar la capacidad física y mental para ejecutar las labores.

Artículo 60. Pruebas de detección de alcohol y drogas.

1. Cuándo: (a) aleatoriamente, en los puestos críticos para la seguridad: {{PUESTOS_CRITICOS_SEGURIDAD}}; (b) ante sospecha razonable, documentada por dos personas con signos observables; (c) después de un accidente o incidente grave.
2. Cómo: las practica personal médico o un laboratorio, en un lugar privado. Antes de la prueba, la persona puede declarar los medicamentos que toma con receta.
3. Confirmación: un resultado preliminar positivo se confirma en laboratorio. Mientras tanto, si hay signos de intoxicación, la persona no labora ese día y se le retira con seguridad. Si la confirmación es negativa, ese día se paga. Recursos Humanos recibe solo el resultado confirmado, positivo o negativo; el detalle clínico lo conserva el servicio médico.
4. Consecuencias: un positivo confirmado sin prescripción médica implica el retiro de funciones críticas hasta una valoración médica de aptitud, y se ofrecerá canalización a atención especializada. La medida disciplinaria se determina por los hechos conforme al Anexo C.

Artículo 61. Datos de salud. Los datos de salud son confidenciales y se tratan conforme a la legislación de protección de datos personales y al aviso de privacidad para personas trabajadoras y serán conservados durante la relación laboral y hasta 2 años terminada esta.

Artículo 62. Riesgos de trabajo. Ante un accidente, incluido el de trayecto:

1. La persona trabajadora, o un tercero si está impedida, avisa de inmediato a su jefatura, que informa a Recursos Humanos el mismo día.
2. La Empresa presta los primeros auxilios, gestiona la atención en el IMSS y da a las autoridades los avisos que exige la Ley, en los plazos que esta señala.
3. La Comisión de Seguridad e Higiene investiga las causas y propone medidas correctivas.
4. La persona trabajadora entrega a Recursos Humanos copia de los documentos que le expida el IMSS dentro de los 2 días hábiles siguientes. La omisión se atiende por vía disciplinaria y no traslada a la persona trabajadora las obligaciones de la Empresa.

Artículo 63. Enfermedades contagiosas. Quien padezca una enfermedad contagiosa lo comunicará a la Empresa en cuanto lo sepa, para adoptar medidas de protección. La información se trata con la confidencialidad del artículo 61.

CAPÍTULO X. Protección reforzada

Artículo 64. Principio. La Empresa aplica las protecciones que la Ley establece para las personas embarazadas o en lactancia, las personas menores de 18 años y las personas con discapacidad. Este capítulo precisa cómo se aplican en la Empresa. Las medidas protegen la salud y los derechos de esas personas y no pueden usarse para excluirlas, reducir su salario ni limitar su desarrollo; se basan en la evaluación del puesto y, cuando se requiera, en una valoración médica individual.

Artículo 65. Embarazo y lactancia. Las personas trabajadoras embarazadas o en periodo de lactancia no realizarán, sin perjuicio de su salario, prestaciones y derechos:

1. Labores insalubres o peligrosas, trabajo nocturno industrial, trabajo en establecimientos comerciales o de servicio después de las 22:00 horas, ni horas extra, cuando se ponga en peligro su salud o la del producto.
2. Durante el embarazo, trabajos que exijan esfuerzos considerables y signifiquen un peligro para su salud en relación con la gestación, como levantar, tirar o empujar grandes pesos, los que produzcan trepidación, impliquen estar de pie durante largo tiempo o puedan alterar su estado psíquico y nervioso.
3. Durante el embarazo, trabajos en los que exista:
   - exposición a ruido o vibraciones que rebasen los límites de exposición;
   - exposición a radiaciones ionizantes o no ionizantes infrarrojas o ultravioletas;
   - presiones ambientales anormales o condiciones térmicas elevadas o abatidas;
   - exposición a contaminantes del ambiente laboral que puedan afectar su salud o la del producto;
   - manejo, transporte, almacenamiento o proceso de sustancias tóxicas, cancerígenas, teratogénicas o mutagénicas;
   - exposición a residuos peligrosos, agentes biológicos o enfermedades infectocontagiosas;
   - esfuerzo físico moderado o pesado, cargas superiores a 10 kilogramos, posturas forzadas o movimientos repetitivos prolongados que impliquen esfuerzo abdominal o de miembros inferiores;
   - labores de rescate, salvamento y brigadas contra siniestros;
   - trabajo en altura o en espacios confinados;
   - soldadura y corte;
   - condiciones climáticas extremas en campo abierto que las expongan a deshidratación, golpe de calor, hipotermia o congelación;
   - actividades productivas de las industrias gasera, del cemento, minera, del hierro y el acero, petrolera, nuclear y eléctrica, torres de perforación o plataformas marítimas, y trabajos submarinos o subterráneos;
   - las demás que las leyes, reglamentos y normas aplicables establezcan como peligrosas o insalubres.
4. Durante la lactancia, labores con exposición a sustancias químicas peligrosas capaces de actuar sobre la vida y la salud del lactante o de interrumpir la lactancia.
5. Cualquier labor, cuando la autoridad competente emita una declaratoria de contingencia sanitaria que así lo determine.

En los centros de trabajo de la Empresa, las áreas y puestos en que se presentan estas condiciones son: {{AREAS_RESTRINGIDAS_EMBARAZO_LACTANCIA}}. La persona trabajadora que ocupe alguno de ellos informará a Recursos Humanos de su embarazo en cuanto lo sepa, para que se le reasigne temporalmente a otra actividad sin reducción de salario. La información se trata con la confidencialidad del artículo 61.

Artículo 66. Descansos por maternidad, adopción y lactancia. Se otorgan en los términos de la Ley. Durante los descansos se percibe el salario a través del subsidio del IMSS; si el IMSS no lo cubre, la Empresa pagará el salario íntegro. [SI LACTARIO = Sí]Para la lactancia, la Empresa dispone de un espacio privado, higiénico y accesible en {{UBICACION_LACTARIO}}, con {{LACTARIO_EQUIPAMIENTO}} para conservar la leche.[FIN SI][SI LACTARIO = No]Como la Empresa no dispone de un lugar adecuado e higiénico para los reposos de lactancia, la jornada de la persona trabajadora se reduce en una hora durante el periodo de lactancia, en el horario que acuerde con la Empresa.[FIN SI]

Artículo 67. Personas menores de 18 años. La Empresa no contrata a personas menores de 15 años, ni a personas de 15 a 17 años que no hayan concluido su educación básica obligatoria, salvo autorización de la autoridad laboral. A las personas de 15 a 17 años que contrate les aplica lo siguiente:

1. Requisitos: certificado médico de aptitud para el trabajo antes de iniciar labores y exámenes médicos periódicos; la Empresa lleva el registro de su nombre, fecha de nacimiento, clase de trabajo, horario, salario y demás condiciones, y distribuye el trabajo para que cumplan sus programas escolares.
2. Jornada: las menores de 16 años laboran como máximo 6 horas diarias, en periodos de no más de 3 horas con reposos de al menos 1 hora entre ellos. Ninguna persona menor de 18 años labora horas extra, en domingo ni en días de descanso obligatorio.
3. Vacaciones: al menos 18 días laborables pagados al año.
4. Lugares y horarios prohibidos: establecimientos no industriales después de las 22:00 horas; expendios de bebidas embriagantes de consumo inmediato, cantinas, tabernas y centros de vicio; y trabajos susceptibles de afectar su moralidad o buenas costumbres.
5. Labores peligrosas o insalubres prohibidas, entre ellas las que impliquen:
   - exposición a ruido, vibraciones, radiaciones, condiciones térmicas elevadas o abatidas, presiones ambientales anormales, agentes químicos contaminantes, residuos peligrosos, agentes biológicos, enfermedades infectocontagiosas, fauna peligrosa o flora nociva;
   - trabajo nocturno industrial o después de las 22:00 horas;
   - rescate, salvamento y brigadas contra siniestros;
   - trabajo en altura o en espacios confinados;
   - operación de equipos y procesos críticos con sustancias químicas peligrosas, y manejo, transporte, almacenamiento o despacho de sustancias químicas peligrosas;
   - soldadura y corte;
   - condiciones climáticas extremas en campo abierto o vialidades con amplio volumen de tránsito vehicular;
   - labores agrícolas, forestales, de aserrado, silvícolas, de caza y pesca que impliquen uso de químicos, maquinaria o vehículos pesados;
   - actividades productivas de las industrias gasera, del cemento, minera, del hierro y el acero, petrolera, nuclear, ladrillera, vidriera, cerámica, cerera y tabacalera;
   - generación, transmisión y distribución de electricidad y mantenimiento de instalaciones eléctricas;
   - obras de construcción;
   - responsabilidad directa sobre el cuidado de personas o la custodia de bienes y valores;
   - alto grado de dificultad, apremio de tiempo, alta responsabilidad o concentración y atención sostenidas;
   - recipientes sujetos a presión, recipientes criogénicos, generadores de vapor o calderas;
   - trabajo en buques, minas, o submarino o subterráneo, y trabajo ambulante sin autorización de la Inspección del Trabajo;
   - esfuerzo físico moderado o pesado, cargas superiores a 7 kilogramos, posturas forzadas o movimientos repetitivos prolongados;
   - manejo, operación o mantenimiento de maquinaria, equipo o herramientas mecánicas, eléctricas, neumáticas o motorizadas que puedan causar amputaciones, fracturas o lesiones graves;
   - manejo o mantenimiento de vehículos motorizados, y uso de herramientas manuales punzocortantes;
   - las demás que las leyes, reglamentos y normas aplicables establezcan.
6. Contingencia sanitaria: no laborarán cuando la autoridad competente así lo determine, sin perjuicio de su salario, prestaciones y derechos.

En los centros de trabajo de la Empresa, las áreas y puestos vedados a personas menores de 18 años son: {{AREAS_RESTRINGIDAS_MENORES}}.

Artículo 68. Discapacidad y condiciones de salud. La Empresa realiza los ajustes razonables que requiera una persona con discapacidad para desempeñar su puesto. La información sobre condiciones de salud es voluntaria y confidencial. Si sobreviene una condición incompatible con el puesto, previa valoración médica, la Empresa buscará con la persona trabajadora una reasignación temporal o definitiva antes de cualquier otra medida, y le dará preferencia en las opciones de flexibilidad o teletrabajo que la operación permita.

CAPÍTULO XI. Integridad, igualdad y denuncias

Artículo 69. Conflictos de interés y relaciones personales. La Empresa no interviene en la vida privada de las personas trabajadoras. Sin embargo, deben declararse por escrito a Recursos Humanos, para que se adopten medidas de organización: (a) las relaciones de pareja o de parentesco entre personas con relación jerárquica directa o que se supervisen entre sí; y (b) los intereses económicos o personales en clientes, proveedores o competidores. La medida típica es la reasignación de la supervisión, sin efectos en salario ni categoría.

Artículo 70. Igualdad y no discriminación. Queda prohibida toda distinción, exclusión o restricción que atente contra la dignidad de las personas por cualquiera de los motivos que prohíbe la Ley. El salario, los ascensos y la capacitación se determinan con criterios objetivos.

Artículo 71. Violencia, acoso y hostigamiento sexual. La Empresa cuenta con un protocolo para prevenir la discriminación por razones de género y atender los casos de violencia, acoso u hostigamiento sexual. Las quejas en esas materias se tramitan por ese protocolo, que prevé medidas de protección inmediatas para la persona afectada, y no por el procedimiento ordinario del Capítulo XII, salvo en lo relativo a la imposición de la medida.

Artículo 72. Entorno organizacional. La Empresa aplica su política de prevención de riesgos psicosociales y promueve un entorno organizacional favorable conforme a la norma oficial aplicable.

Artículo 73. Código de ética, regalos y vestimenta. El código de ética, la política de regalos y el código de vestimenta desarrollan las conductas esperadas en esas materias. Son obligatorios una vez comunicados con acuse.

[SI CANAL_DENUNCIAS ≠ vacío]

Artículo 74. Canal de denuncias. Cualquier persona puede denunciar incumplimientos de este Reglamento, de las políticas o de la ley por {{CANAL_DENUNCIAS}}, incluso de forma anónima. La Empresa garantiza confidencialidad, prohíbe represalias contra quien denuncie de buena fe o colabore en una investigación, y acusa recibo en {{DIAS_ACUSE_DENUNCIA}} días hábiles.

[FIN SI]

Artículo 75. Información y redes sociales. Las personas trabajadoras pueden expresarse libremente en sus redes personales. No pueden publicar información confidencial de la Empresa, incluyendo la operativa o laboral, datos personales de compañeros o clientes, ni imágenes de áreas restringidas, ni hablar a nombre de la Empresa sin autorización.

CAPÍTULO XII. Medidas disciplinarias y procedimiento

Artículo 76. Propósito. Las medidas disciplinarias buscan corregir conductas mediante retroalimentación. Se aplican con proporcionalidad, confidencialidad y respeto, y ninguna se impone sin escuchar antes a la persona trabajadora.

Artículo 77. Medidas disciplinarias. Las únicas medidas disciplinarias son:

1. Amonestación verbal, con registro en el expediente.
2. Amonestación escrita.
3. Suspensión en el trabajo sin goce de salario de 1 a 8 días.
4. Rescisión de la relación de trabajo, cuando los hechos constituyan una causa legal. La decide la Empresa conforme al artículo 84 y no requiere resolución del Comité.

Artículo 78. Cómo se gradúa la medida. El Anexo C clasifica cada conducta como leve, grave o muy grave y fija el rango de medidas aplicable. Dentro del rango se consideran: la intención o la negligencia; el daño o riesgo causado; los antecedentes de la persona; las circunstancias, como provocación previa o causas personales acreditadas; y su colaboración para aclarar los hechos. La reincidencia en una conducta del mismo nivel dentro de {{MESES_REINCIDENCIA}} meses permite aplicar el rango previsto para la reincidencia. La conducta intentada y no consumada se califica en el nivel inferior al de la consumada.

Artículo 79. Comité de Integridad y Disciplina. El Comité conoce de las faltas graves y muy graves y de las revisiones de faltas leves. La Empresa lo integra y regula su funcionamiento en un documento propio, que da a conocer a las personas trabajadoras. Quien tenga relación directa con los hechos o con las personas involucradas se excusa y es sustituido por quien designe la Empresa.

Artículo 80. Ruta para faltas leves.

1. La jefatura y/o Recursos Humanos conversa en privado con la persona trabajadora, le expone el hecho y escucha su versión.
2. Registra en el formato de falta leve (FD-4) el hecho, la versión de la persona y lo acordado.
3. Si procede, aplica una amonestación verbal registrada o una amonestación escrita. La persona firma de enterada; si se niega, lo hacen constar dos testigos.
4. La persona afectada puede pedir al Comité, dentro de los 3 días naturales siguientes, que revise la medida. Si el plazo vence en un día de descanso de la persona, se extiende a su siguiente día laborable.

Artículo 81. Ruta para faltas graves y muy graves.

1. Reporte. La jefatura inmediata, o quien conozca los hechos, los reporta de inmediato a Recursos Humanos y al Comité, a más tardar al día siguiente de conocerlos, con la evidencia disponible. El reporte tardío de la jefatura es una falta conforme al Anexo C.
2. Aviso de hechos. Recursos Humanos entrega a la persona trabajadora el aviso de hechos (formato FD-1), con los hechos, las conductas del Anexo C que podrían actualizarse, la fecha de la audiencia (entre 1 y 5 días naturales después de la entrega del aviso) y su derecho a presentar pruebas y testigos y a acompañarse de una persona trabajadora de su confianza.
3. Audiencia. El Comité escucha a la persona, recibe sus pruebas y levanta el acta de audiencia (formato FD-2), que firman los asistentes. Si la persona se niega a firmar, lo hacen constar dos testigos. Si no asiste sin causa justificada, habiendo recibido el aviso, el Comité resuelve con lo que obre en el expediente.
4. Resolución. El Comité resuelve por escrito, en el formato FD-3, indicando hechos, pruebas, conducta, medida y razones, y la notifica dentro de los 5 días naturales siguientes a la audiencia. Si impone una suspensión, señala su duración, que se cuenta en días laborables del turno de la persona, y la suspensión inicia a más tardar 10 días naturales después de la notificación.

Recursos Humanos fija la fecha de la audiencia y las del inicio y el término de la suspensión dentro de los plazos de este artículo y del artículo 83. Si la audiencia o el inicio de la suspensión caen en un día de descanso de la persona trabajadora, se trasladan a su siguiente día laborable.

Artículo 82. Medidas provisionales. Cuando sea necesario para proteger a personas o pruebas, durante el procedimiento la Empresa puede reasignar temporalmente a la persona trabajadora de área, turno o funciones, o separarla del centro de trabajo con goce de salario. Ninguna medida provisional es sin goce de salario.

Artículo 83. Plazo. La medida disciplinaria se notifica en un plazo de 30 días naturales contados a partir de la fecha en que la jefatura inmediata, o cualquier persona con mando sobre la persona trabajadora, tuvo conocimiento de la falta, sin exceder en ningún caso el plazo de prescripción que establece la Ley.

Artículo 84. Relación con la rescisión. Si la conducta puede constituir una causa de rescisión conforme a la Ley, la Empresa puede seguir el procedimiento del artículo 81 para documentar los hechos y escuchar a la persona trabajadora. La rescisión se comunica mediante el aviso correspondiente, entregado personalmente o por conducto de la autoridad jurisdiccional, dentro del plazo legal.

Artículo 85. Casos de acoso y violencia. Se investigan conforme al protocolo del artículo 71. El Comité solo interviene para imponer la medida que corresponda con base en el resultado de esa investigación.

Artículo 86. Expediente. Cada medida se integra al expediente de la persona trabajadora, que puede consultarlo. Las amonestaciones no se consideran para la reincidencia después de {{MESES_CANCELACION_ANTECEDENTES}} meses sin una nueva falta.

CAPÍTULO XIII. Revisión y modificación del Reglamento

Artículo 87. Revisión. La Comisión revisa este Reglamento al menos una vez al año y cuando se publique una reforma legal que lo afecte, conforme a las reglas de su acta de integración. Las personas trabajadoras y la Empresa pueden presentar propuestas por conducto de sus representantes.

Artículo 88. Modificaciones. Las modificaciones aprobadas por la Comisión se depositan ante el Centro Federal de Conciliación y Registro Laboral en el plazo legal, surten efectos desde su depósito y se difunden en los términos del artículo 6. El Anexo B se actualiza cuando cambia el catálogo de jornadas[SI NUM_CENTROS_TRABAJO > 1], y el Anexo A cuando se abre o se cierra un centro de trabajo o cambian sus datos[FIN SI]; la versión actualizada se aprueba y deposita en los mismos términos. El ajuste de horarios por reducción legal de la jornada del artículo 8 no constituye una modificación de este Reglamento ni requiere depósito.

Artículo 89. Omisiones. Las personas trabajadoras o la Empresa pueden solicitar a la autoridad competente, en los términos de la Ley, que se subsanen las omisiones de este Reglamento o se revisen las disposiciones contrarias a ella.

TRANSITORIOS

PRIMERO. Este Reglamento surte efectos a partir de la fecha de su depósito ante el Centro Federal de Conciliación y Registro Laboral.

SEGUNDO. Se dejan sin efecto las disposiciones internas que se opongan a este Reglamento. [SI RIT_ANTERIOR = Sí] Se abroga el Reglamento Interior de Trabajo depositado el {{FECHA_DEPOSITO_RIT_ANTERIOR}}. [FIN SI]

TERCERO. Los procedimientos disciplinarios iniciados antes de su vigencia concluyen conforme a la norma con que se iniciaron, aplicando este Reglamento en lo que favorezca a la persona trabajadora.

CUARTO. El registro de jornada del artículo 13 se ajustará a las disposiciones que emita la STPS, sin necesidad de modificar este Reglamento.

QUINTO. Las políticas del artículo 4 se emitirán o actualizarán y comunicarán dentro de los {{DIAS_EMISION_POLITICAS}} días naturales siguientes a la vigencia de este Reglamento. Mientras tanto, solo son sancionables las conductas descritas expresamente en el Anexo C.

FIRMAS

La Comisión aprueba y firma este Reglamento y sus anexos en {{LUGAR_EMISION}}, el {{FECHA_EMISION}}, en {{NUM_EJEMPLARES}} ejemplares.

| Representación | Nombre | Cargo | CURP | Firma |
| --- | --- | --- | --- | --- |
| Empresa | {{REP_EMPRESA_NOMBRE}} | {{REP_EMPRESA_CARGO}} | {{REP_EMPRESA_CURP}} |  |
| Personas trabajadoras | {{REP_TRABAJADORES_NOMBRE}} | {{REP_TRABAJADORES_CARGO}} | {{REP_TRABAJADORES_CURP}} |  |

[SI NUM_CENTROS_TRABAJO > 1]

ANEXO A. Centros de trabajo

Centros de trabajo de la Empresa en los que rige este Reglamento, conforme al artículo 3.

| # | Centro de trabajo | Domicilio | Estado | Registro patronal IMSS |
| --- | --- | --- | --- | --- |
| {{N}} | {{CENTRO_NOMBRE}} | {{CENTRO_DOMICILIO}} | {{CENTRO_ESTADO}} | {{CENTRO_REGISTRO_PATRONAL}} |

[FIN SI]

ANEXO B. Horarios

Horarios de cada centro de trabajo y turno, conforme a los artículos 8 y 12. Se ajusta conforme al artículo 8 cuando la Ley reduzca la jornada máxima.

| Centro / área | Turno | Tipo de jornada | Días laborables | Entrada | Salida | Comida o reposo | Descanso semanal | Horas semanales |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| {{TURNO_CENTRO}} | {{TURNO_NOMBRE}} | {{TURNO_TIPO_JORNADA}} | [SI TURNO_DESCANSO_TIPO = Fijo]{{TURNO_DIAS_LABORABLES}}[FIN SI][SI TURNO_DESCANSO_TIPO = Rotativo]{{TURNO_DIAS_TRABAJO_SEMANA}} días por semana[FIN SI] | {{TURNO_ENTRADA}} | {{TURNO_SALIDA}} | {{TURNO_COMIDA}} | [SI TURNO_DESCANSO_TIPO = Fijo]{{TURNO_DESCANSO_SEMANAL}}[FIN SI][SI TURNO_DESCANSO_TIPO = Rotativo]Rotativo[FIN SI] | {{TURNO_HORAS_SEMANA}} |

ANEXO C. Catálogo de conductas y escala de medidas disciplinarias

Este anexo forma parte del Reglamento y se deposita con él. Las conductas están ordenadas de menor a mayor gravedad. Las conductas que corresponden a una causa legal de rescisión pueden constituir, además, causa de rescisión en los términos de la Ley, conforme al artículo 84.

Escala

| Nivel | Medida aplicable | Con reincidencia en {{MESES_REINCIDENCIA}} meses |
| --- | --- | --- |
| Leve | Amonestación verbal registrada o amonestación escrita | Suspensión de 1 a 2 días |
| Grave | Amonestación escrita o suspensión de 1 a 3 días | Suspensión de 4 a 8 días |
| Muy grave | Suspensión de 4 a 8 días | Suspensión de 8 días |

Faltas leves

| # | Conducta |
| --- | --- |
| 1 | Llegar después de la tolerancia |
| 2 | No avisar una ausencia conforme al artículo 15, aunque después se justifique |
| 3 | No registrar la entrada o la salida |
| 4 | Exceder sin autorización el tiempo de comida o reposo |
| 5 | Laborar u ordenar tiempo extra sin la orden previa del artículo 17 |
| 6 | Recibir visitas personales en áreas de trabajo sin autorización |
| 7 | Atender asuntos personales o actividades ajenas al trabajo durante la jornada |
| 8 | Usar dispositivos personales con fines no laborales fuera de lo que permite la política |
| 9 | Usar en exceso equipos, correo o internet de la Empresa para asuntos personales |
| 10 | Vender productos o hacer colectas sin autorización |
| 11 | Comer en áreas donde esté prohibido |
| 12 | Hacer mal uso de sanitarios, comedor o áreas comunes |
| 13 | No portar el uniforme o la vestimenta conforme al código |
| 14 | Incumplir por descuido procedimientos o instrucciones de trabajo |
| 15 | Faltar sin causa a una capacitación programada |
| 16 | No participar en un simulacro |
| 17 | No mantener el orden y la limpieza del área o no clasificar residuos |
| 18 | No entregar en plazo los documentos del IMSS sobre un riesgo de trabajo |
| 19 | No reportar fallas, daños o pérdidas de los bienes asignados |
| 20 | Dañar o extraviar por negligencia herramientas, equipo o uniformes (grave si el daño es considerable) |
| 21 | Incumplir una política comunicada con acuse, cuando la conducta no esté prevista en otro punto (grave si causa daño o riesgo) |

Faltas graves

| # | Conducta |
| --- | --- |
| 22 | Acumular {{RETARDOS_FALTA_GRAVE}} o más retardos en 30 días |
| 23 | Faltar un día sin causa justificada |
| 24 | Ausentarse o retirarse antes de terminar la jornada sin autorización |
| 25 | Dormir durante la jornada (muy grave en puestos críticos para la seguridad) |
| 26 | Desobedecer sin causa justificada instrucciones relacionadas con el trabajo contratado |
| 27 | Usar lenguaje ofensivo, apodos o expresiones despectivas hacia cualquier persona |
| 28 | Difundir rumores o comentarios que dañen la reputación de una persona |
| 29 | No usar el equipo de protección personal o usarlo incompleto |
| 30 | Llevar cabello suelto, joyas o ropa suelta cerca de maquinaria en movimiento |
| 31 | No reportar condiciones peligrosas, fallas de equipo o accidentes |
| 32 | Fumar o vapear fuera de las áreas designadas |
| 33 | Negarse sin causa justificada a un examen médico o a una prueba del artículo 60 |
| 34 | Obtener un resultado positivo confirmado sin prescripción en un puesto crítico para la seguridad |
| 35 | Usar herramientas, vehículos o equipo para fines ajenos al trabajo |
| 36 | Tomar fotografías o grabaciones de instalaciones, información o personas sin autorización |
| 37 | Acceder a áreas restringidas o permitir el acceso de terceros sin autorización |
| 38 | Compartir contraseñas o usar cuentas de otra persona |
| 39 | Publicar información confidencial, datos personales o imágenes de áreas restringidas |
| 40 | Omitir la declaración de un conflicto de interés |
| 41 | Dar, recibir u ofrecer regalos o atenciones contrarios a la política |
| 42 | Presentar una denuncia falsa a sabiendas |
| 43 | Siendo jefatura, no reportar a Recursos Humanos y al Comité una falta grave o muy grave de inmediato, a más tardar al día siguiente de conocerla |

Faltas muy graves

| # | Conducta |
| --- | --- |
| 44 | Faltar dos o tres días sin causa justificada en 30 días |
| 45 | Registrar la asistencia de otra persona, permitir que otra registre la propia o alterar registros |
| 46 | Retirar guardas, inhabilitar dispositivos de seguridad o incumplir procedimientos seguros |
| 47 | Comprometer por imprudencia o descuido inexcusable la seguridad del centro o de las personas |
| 48 | Bloquear, dañar o usar indebidamente equipos de emergencia, señales o rutas de evacuación |
| 49 | Introducir o consumir en el centro de trabajo bebidas alcohólicas o drogas |
| 50 | Presentarse o laborar en estado de embriaguez o bajo los efectos de un narcótico sin prescripción médica |
| 51 | Portar armas sin que el trabajo lo requiera |
| 52 | Cometer actos de discriminación |
| 53 | Cometer actos de violencia, amenazas, injurias o malos tratos |
| 54 | Cometer hostigamiento o acoso sexual |
| 55 | Tomar represalias contra quien denuncie o colabore en una investigación |
| 56 | Extraer bienes, documentos o información sin autorización |
| 57 | Dañar intencionalmente bienes de la Empresa o de terceros |
| 58 | Revelar información confidencial o secretos de la Empresa |
| 59 | Incurrir en faltas de probidad u honradez, incluida la alteración de documentos |
| 60 | Incurrir en ausentismo reiterado: faltas injustificadas recurrentes que, aunque no sumen más de tres en 30 días, muestren un patrón sistemático, como su repetición en varios periodos o su coincidencia frecuente con días de descanso, festivos o de pago |
```

### 6.2 FD-1. Aviso de hechos y citatorio a audiencia

```text
FD-1. AVISO DE HECHOS Y CITATORIO A AUDIENCIA

| Folio                        | {{EXP_FOLIO}}                            |
| Fecha de entrega             | {{FD1_FECHA}}                            |
| Persona trabajadora          | {{PERSONA_NOMBRE}}                       |
| Puesto y centro de trabajo   | {{PERSONA_PUESTO}}, {{PERSONA_CENTRO}}   |
| Jefatura inmediata           | {{PERSONA_JEFATURA}}                     |

1. Hechos. El {{EXP_FECHA_HECHOS}}, aproximadamente a las {{EXP_HORA_HECHOS}} horas, en {{EXP_LUGAR_HECHOS}}, ocurrieron los hechos siguientes: {{EXP_HECHOS}}. La jefatura inmediata tuvo conocimiento de los hechos el {{EXP_FECHA_CONOCIMIENTO_JEFATURA}}, y {{EXP_REPORTA}} los reportó a Recursos Humanos y al Comité el {{EXP_FECHA_AVISO_COMITE}}.

2. Evidencia disponible. {{EXP_EVIDENCIA_LISTA}}. Usted puede consultarla antes de la audiencia en {{EXP_LUGAR_CONSULTA}}.

3. Conductas que podrían actualizarse. Conforme al catálogo de conductas y escala de medidas disciplinarias del Reglamento Interior de Trabajo, los hechos podrían constituir: {{EXP_CONDUCTAS_CATALOGO}}, clasificadas como falta {{EXP_NIVEL}}.

[SI EXP_POSIBLE_RESCISION = Sí]Los hechos también podrían constituir una causa de rescisión de la relación de trabajo en los términos de la Ley. Este aviso no es un aviso de rescisión: si la Empresa decide rescindir, se lo comunicará por separado y por escrito.[FIN SI]

4. Citatorio. Se le cita a una audiencia ante el Comité de Integridad y Disciplina el {{FD1_FECHA_AUDIENCIA}}, a las {{FD1_HORA_AUDIENCIA}} horas, en {{FD1_LUGAR_AUDIENCIA}}. La audiencia se celebra dentro de su jornada y el tiempo que dure es tiempo de trabajo.

5. Sus derechos en la audiencia.
   1. Ser escuchado y dar su versión de los hechos, de forma oral o por escrito.
   2. Presentar las pruebas y los testigos que considere convenientes.
   3. Acompañarse de una persona trabajadora de su confianza.
   4. Recibir copia del acta de la audiencia.

Si no puede asistir por una causa justificada, avíselo a Recursos Humanos antes de la hora señalada y acredite la causa; la audiencia se reprogramará una sola vez. Si no asiste sin causa justificada, el Comité resolverá con lo que obre en el expediente.

[SI EXP_MEDIDA_PROVISIONAL = Sí]6. Medida provisional. Mientras concluye el procedimiento, se aplica la medida siguiente: {{EXP_MEDIDA_PROVISIONAL_DESCRIPCION}}, del {{EXP_MEDIDA_INICIO}} al {{EXP_MEDIDA_FIN}}. La medida no es una sanción y no afecta su salario.[FIN SI]

| Entrega              | Nombre                       | Firma |
| Recursos Humanos     | {{RH_RESPONSABLE_NOMBRE}}    |       |
| Recibí este aviso    | {{PERSONA_NOMBRE}}           |       |

[SI FD1_NEGATIVA = Sí]
La persona trabajadora se negó a firmar de recibido. El aviso se le leyó y se le ofreció copia en presencia de los testigos que firman, y se envió a su correo personal {{PERSONA_CORREO}} el {{FD1_FECHA_ENVIO}}.

| Testigo | Nombre                  | Firma |
| 1       | {{TESTIGO_1_NOMBRE}}    |       |
| 2       | {{TESTIGO_2_NOMBRE}}    |       |
[FIN SI]
```

### 6.3 FD-2. Acta de audiencia

```text
FD-2. ACTA DE AUDIENCIA

| Folio                                    | {{EXP_FOLIO}}                                                         |
| Lugar, fecha y hora                      | {{FD2_LUGAR}}, {{FD2_FECHA}}, de {{FD2_HORA_INICIO}} a {{FD2_HORA_CIERRE}} horas |
| Persona trabajadora                      | {{PERSONA_NOMBRE}}, {{PERSONA_PUESTO}}                                |
| Aviso de hechos (FD-1)                   | Entregado el {{FD1_FECHA}}                                            |
| Integrantes del Comité                   | {{COMITE_ASISTENTES}}                                                 |
| Acompañante de la persona trabajadora    | {{FD2_ACOMPANANTE}}                                                   |

[SI FD2_INASISTENCIA = No]
1. Apertura. El Comité leyó a la persona trabajadora los hechos, la evidencia y las conductas del catálogo señaladas en el aviso de hechos, y le explicó sus derechos en la audiencia.

2. Versión de la persona trabajadora. La persona trabajadora escribe de su puño y letra su versión de los hechos:
[RECUADRO_MANUSCRITO]
[SI FD2_ESCRITO = Sí]Presentó además un escrito de {{FD2_ESCRITO_FOJAS}} fojas, que se agrega al expediente.[FIN SI]

3. Pruebas.

| Prueba                       | Ofrecida por           | Admitida               | Observaciones                |
| {{PRUEBA_DESCRIPCION}}       | {{PRUEBA_OFERENTE}}    | {{PRUEBA_ADMITIDA}}    | {{PRUEBA_OBSERVACIONES}}     |

Las pruebas no admitidas se registran con la razón de su rechazo.

4. Testigos. {{FD2_TESTIGOS_DECLARACIONES}}

5. Preguntas y aclaraciones. {{FD2_PREGUNTAS}}

6. Manifestaciones finales. La persona trabajadora escribe de su puño y letra lo que desee manifestar:
[RECUADRO_MANUSCRITO]
[FIN SI]

[SI FD2_INASISTENCIA = Sí]
Inasistencia. La persona trabajadora no se presentó, habiendo recibido el aviso de hechos el {{FD1_FECHA}}, y no comunicó ni acreditó una causa justificada hasta la hora señalada. El Comité resolverá con lo que obre en el expediente.
[FIN SI]

Cierre. El Comité resolverá y notificará su resolución dentro de los 5 días naturales siguientes. Leída el acta, la firman quienes intervinieron. La persona trabajadora recibe copia.

| Intervino como           | Nombre                          | Firma |
| Integrante del Comité    | {{COMITE_INTEGRANTE_NOMBRE}}    |       |
| Persona trabajadora      | {{PERSONA_NOMBRE}}              |       |
| Acompañante              | {{FD2_ACOMPANANTE}}             |       |

[SI FD2_NEGATIVA = Sí]
La persona trabajadora se negó a firmar. Lo hacen constar los testigos {{TESTIGO_1_NOMBRE}} y {{TESTIGO_2_NOMBRE}}, que firman al margen.
[FIN SI]
```

- Tabla de pruebas: una fila por prueba (`PRUEBA_*`).
- Firmas del Comité: una fila por integrante asistente (`COMITE_ASISTENTES`). Fila de acompañante solo si `FD2_ACOMPANANTE` no está vacío.

### 6.4 FD-3. Resolución del Comité de Integridad y Disciplina

```text
FD-3. RESOLUCIÓN DEL COMITÉ DE INTEGRIDAD Y DISCIPLINA

| Folio                          | {{EXP_FOLIO}}                                                                        |
| Fecha de la resolución         | {{FD3_FECHA}}                                                                        |
| Persona trabajadora            | {{PERSONA_NOMBRE}}, {{PERSONA_PUESTO}}                                               |
| Conocimiento de la falta       | {{EXP_FECHA_CONOCIMIENTO_JEFATURA}} (aviso al Comité: {{EXP_FECHA_AVISO_COMITE}})    |
| Fecha límite para notificar    | {{EXP_FECHA_LIMITE_NOTIFICACION}}                                                    |

1. Antecedentes. El {{FD1_FECHA}} se entregó el aviso de hechos y el {{FD2_FECHA}} se celebró la audiencia, cuya acta forma parte de esta resolución.

2. Hechos acreditados. {{FD3_HECHOS_ACREDITADOS}}

3. Valoración de las pruebas y de la versión de la persona trabajadora. {{FD3_VALORACION}}

4. Calificación. Los hechos acreditados constituyen la conducta {{FD3_CONDUCTA_CATALOGO}} del catálogo de conductas del Reglamento, falta {{FD3_NIVEL}}. Para graduar la medida se consideraron: {{FD3_CIRCUNSTANCIAS}}.[SI FD3_REINCIDENCIA = Sí] Existe reincidencia: antecedente {{FD3_ANTECEDENTE_FOLIO}} del {{FD3_ANTECEDENTE_FECHA}}.[FIN SI]

5. Resolución.

[SI FD3_RESULTADO = Sin responsabilidad]
No se acreditó la conducta. El expediente se archiva y no se considera antecedente.
[FIN SI]
[SI FD3_RESULTADO = Amonestación escrita]
Se impone amonestación escrita, que se integra a su expediente.
[FIN SI]
[SI FD3_RESULTADO = Suspensión]
Se impone suspensión en el trabajo sin goce de salario por {{FD3_DIAS_SUSPENSION}} días, del {{FD3_SUSPENSION_INICIO}} al {{FD3_SUSPENSION_FIN}}. Debe reincorporarse el {{FD3_REINCORPORACION}}.
[FIN SI]
[SI EXP_TIPO = Daño Y FD3_NEGLIGENCIA = Sí]
Se determina que la pérdida o el daño del bien {{BIEN_DESCRIPCION}} obedeció a negligencia de la persona trabajadora. Con la autorización otorgada en el resguardo del {{RESGUARDO_FECHA}}, procede el descuento de {{DESCUENTO_MONTO}} en {{DESCUENTO_PAGOS}} pagos de {{DESCUENTO_POR_PAGO}}, dentro de los límites del artículo {{REF_ART_27}} del Reglamento.
[FIN SI]
[SI EXP_TIPO = Daño Y FD3_NEGLIGENCIA = No]
No se acreditó negligencia: el daño o la pérdida del bien {{BIEN_DESCRIPCION}} se atribuye al uso normal, a caso fortuito o fuerza mayor, o a la calidad del bien. No procede descuento alguno.
[FIN SI]
[SI FD3_RESULTADO = Propuesta de rescisión]
Los hechos acreditados pueden constituir una causa de rescisión en los términos de la Ley. El Comité turna el expediente a la Empresa para que decida antes de {{EXP_FECHA_LIMITE_NOTIFICACION}}. Esta resolución no es el aviso de rescisión.
[FIN SI]

6. Derechos. Esta resolución no limita el derecho de la persona trabajadora a acudir ante la autoridad laboral.

| Firma                                                           | Nombre                            |
| Integrante del Comité                                           | {{COMITE_INTEGRANTE_NOMBRE}}      |
| Integrante del Comité                                           | {{COMITE_INTEGRANTE_2_NOMBRE}}    |
| Notificada a la persona trabajadora el {{FD3_FECHA_NOTIFICACION}} | {{PERSONA_NOMBRE}}              |

[SI FD3_NEGATIVA = Sí]
La persona trabajadora se negó a firmar de recibido. Lo hacen constar {{TESTIGO_1_NOMBRE}} y {{TESTIGO_2_NOMBRE}}, y la resolución se envió a su correo personal {{PERSONA_CORREO}}.
[FIN SI]
```

- `{{REF_ART_27}}`: número final del artículo `ART_27` tras la renumeración (sección 2.2). En el maestro se lee «artículo 27».
- Con `EXP_TIPO` = Daño, el bloque de daño se imprime además del resultado disciplinario elegido, si lo hay.

### 6.5 FD-4. Registro de falta leve

```text
FD-4. REGISTRO DE FALTA LEVE

| Folio                       | {{EXP_FOLIO}}                            |
| Fecha de la conversación    | {{FD4_FECHA}}                            |
| Persona trabajadora         | {{PERSONA_NOMBRE}}, {{PERSONA_PUESTO}}   |
| Jefatura que registra       | {{PERSONA_JEFATURA}}                     |

1. Hecho. El {{EXP_FECHA_HECHOS}}: {{EXP_HECHOS}}.

2. Conducta del catálogo. {{EXP_CONDUCTAS_CATALOGO}} (falta leve).

3. Versión de la persona trabajadora. La persona trabajadora escribe de su puño y letra su versión de los hechos:
[RECUADRO_MANUSCRITO]

4. Acuerdo. {{FD4_ACUERDO}}

5. Medida. {{FD4_MEDIDA}}.

6. Revisión. La persona trabajadora puede pedir al Comité de Integridad y Disciplina que revise esta medida dentro de los 3 días naturales siguientes (si el último es su día de descanso, hasta su siguiente día laborable), por la Plataforma o por escrito ante Recursos Humanos.

| Firma                 | Nombre                  |
| Jefatura inmediata    | {{PERSONA_JEFATURA}}    |
| De enterado           | {{PERSONA_NOMBRE}}      |

[SI FD4_NEGATIVA = Sí]
La persona trabajadora se negó a firmar de enterado. Lo hacen constar {{TESTIGO_1_NOMBRE}} y {{TESTIGO_2_NOMBRE}}.
[FIN SI]
```

- `FD4_MEDIDA`: Sin medida · Amonestación verbal registrada · Amonestación escrita. En el maestro las opciones aparecen entre paréntesis como guía; **no se imprimen**: se imprime solo la opción elegida.

### 6.6 FD-5. Acta de hechos por daño o pérdida de bienes

```text
FD-5. ACTA DE HECHOS POR DAÑO O PÉRDIDA DE BIENES

| Folio                            | {{EXP_FOLIO}}                                  |
| Lugar, fecha y hora              | {{FD5_LUGAR}}, {{FD5_FECHA}}, {{FD5_HORA}} horas |
| Persona trabajadora              | {{PERSONA_NOMBRE}}, {{PERSONA_PUESTO}}         |
| Jefatura que levanta el acta     | {{PERSONA_JEFATURA}}                           |

1. Bien afectado. Los datos se toman del resguardo firmado por la persona trabajadora.

| Descripción            | Marca, modelo y serie       | Fecha del resguardo   | Estado al entregarse       | Valor de reposición          |
| {{BIEN_DESCRIPCION}}   | {{BIEN_IDENTIFICACION}}     | {{RESGUARDO_FECHA}}   | {{BIEN_ESTADO_ENTREGA}}    | {{BIEN_VALOR_REPOSICION}}    |

2. Hechos. {{FD5_TIPO}} detectado el {{FD5_FECHA_DETECCION}}: {{FD5_HECHOS}}. Estado actual del bien: {{BIEN_ESTADO_ACTUAL}}.

3. Evidencia. {{FD5_EVIDENCIA}}

4. Versión de la persona trabajadora. La persona trabajadora escribe de su puño y letra su versión de los hechos:
[RECUADRO_MANUSCRITO]

5. Responsabilidad. La persona trabajadora no responde del deterioro por el uso normal, por caso fortuito o fuerza mayor, ni por la mala calidad del bien.

[SI FD5_RECONOCE = Sí]
La persona trabajadora reconoce que el {{FD5_TIPO_MINUSCULA}} obedeció a su negligencia y reconoce un adeudo de {{DESCUENTO_MONTO}}, que acepta cubrir mediante descuento en {{DESCUENTO_PAGOS}} pagos de {{DESCUENTO_POR_PAGO}}, sin intereses y dentro de los límites del artículo {{REF_ART_27}} del Reglamento. Este reconocimiento se formaliza con el acuerdo de descuento.
[FIN SI]
[SI FD5_RECONOCE = No]
La persona trabajadora no reconoce responsabilidad. El expediente se turna al Comité de Integridad y Disciplina para que determine si hubo negligencia, con el aviso de hechos (FD-1) y la audiencia (FD-2). No se aplica descuento alguno mientras el Comité no resuelva.
[FIN SI]

| Firma                  | Nombre                  |
| Jefatura inmediata     | {{PERSONA_JEFATURA}}    |
| Persona trabajadora    | {{PERSONA_NOMBRE}}      |

[SI FD5_NEGATIVA = Sí]
La persona trabajadora se negó a firmar. Lo hacen constar {{TESTIGO_1_NOMBRE}} y {{TESTIGO_2_NOMBRE}}. La negativa equivale a falta de reconocimiento.
[FIN SI]
```

- `FD5_TIPO`: Daño · Pérdida (se imprime solo la opción elegida). `FD5_TIPO_MINUSCULA` es la misma opción en minúscula («daño», «pérdida»), para que la frase lea bien; en el maestro se usa `FD5_TIPO`.
- Una fila por bien afectado.
- `FD5_NEGATIVA` = Sí equivale a `FD5_RECONOCE` = No y abre FD-1.

### 6.7 FR-1. Constancia de recibo del Reglamento Interior de Trabajo

```text
CONSTANCIA DE RECIBO DEL REGLAMENTO INTERIOR DE TRABAJO

| Persona trabajadora           | {{PERSONA_NOMBRE}}                                                                                  |
| Puesto y centro de trabajo    | {{PERSONA_PUESTO}}, {{PERSONA_CENTRO}}                                                              |
| Momento de la entrega         | {{FR1_MOMENTO}}                                                                                     |
| Reglamento entregado          | Versión depositada ante el Centro Federal de Conciliación y Registro Laboral el {{RIT_FECHA_DEPOSITO}} |
| Medio de entrega              | {{FR1_MEDIO}}[SI FR1_MEDIO = Electrónico], enlace {{RIT_ENLACE}}[FIN SI]                            |
| Fecha                         | {{FR1_FECHA}}                                                                                       |

Recibí un ejemplar del Reglamento Interior de Trabajo de {{RAZON_SOCIAL}} y de sus anexos: [SI NUM_CENTROS_TRABAJO > 1]centros de trabajo, [FIN SI]horarios, y catálogo de conductas y escala de medidas disciplinarias. Tuve oportunidad de leerlo y de plantear mis dudas a Recursos Humanos. Sé que también está fijado en los lugares visibles de mi centro de trabajo y que puedo consultarlo en cualquier momento.

| Firma                  | Nombre                        |
| Persona trabajadora    | {{PERSONA_NOMBRE}}                                   |
| Por la Empresa         | {{FIRMA_EMPRESA_NOMBRE}}, {{FIRMA_EMPRESA_CARGO}}    |

[SI FIRMA_MODALIDAD = Electrónica]
Esta constancia se firma por medios electrónicos en los términos de la cláusula de formalización por medios electrónicos del contrato individual de trabajo.
[FIN SI]

[SI FR1_NEGATIVA = Sí]
La persona trabajadora recibió el ejemplar y se negó a firmar. Lo hacen constar {{TESTIGO_1_NOMBRE}} y {{TESTIGO_2_NOMBRE}}, y el Reglamento se envió a su correo personal {{PERSONA_CORREO}} el {{FR1_FECHA_ENVIO}}.
[FIN SI]
```

- `FR1_MOMENTO`: Emisión del Reglamento · Ingreso · Modificación. `FR1_MEDIO`: Papel · Electrónico. Se imprime solo la opción elegida.

### 6.8 FR-2. Constancia de difusión del Reglamento Interior de Trabajo

```text
CONSTANCIA DE DIFUSIÓN DEL REGLAMENTO INTERIOR DE TRABAJO

| Empresa                      | {{RAZON_SOCIAL}}                                       |
| Firma del Reglamento         | {{FECHA_EMISION}}                                      |
| Depósito                     | {{RIT_FECHA_DEPOSITO}}, acuse {{RIT_ACUSE_DEPOSITO}}   |
| Fecha de esta constancia     | {{FR2_FECHA}}                                          |

1. Fijación en lugares visibles.

| Centro de trabajo     | Lugares donde se fijó    | Fecha                | Responsable                | Evidencia fotográfica      |
| {{FIJACION_CENTRO}}   | {{FIJACION_LUGARES}}     | {{FIJACION_FECHA}}   | {{FIJACION_RESPONSABLE}}   | {{FIJACION_EVIDENCIA}}     |

2. Entrega individual.

| Concepto                                                      | Dato                  |
| Personas trabajadoras a la fecha                              | {{PLANTILLA_NUM}}     |
| Constancias de recibo (FR-1) recabadas                        | {{FR1_RECABADAS}}     |
| Entregas con negativa a firmar documentada                    | {{FR1_NEGATIVAS}}     |
| Pendientes y causa (incapacidad, vacaciones, licencia)        | {{FR1_PENDIENTES}}    |

Las entregas pendientes se completan al reincorporarse cada persona. El sistema registra cada constancia en el expediente individual.


| Firma                             | Nombre                       |
| Recursos Humanos                  | {{RH_RESPONSABLE_NOMBRE}}    |
| Testigo, persona trabajadora      | {{TESTIGO_1_NOMBRE}}         |
```

- Tabla de fijación: una fila por centro de trabajo. `FIJACION_EVIDENCIA` es la fotografía, impresa en miniatura.
- La fijación física en cada centro es requisito legal. No hay verificación periódica ni alerta posterior.

### 6.9 Acta de integración de la Comisión Mixta del Reglamento Interior de Trabajo

Se genera antes que el RIT. La «Nota de uso» y los «Pendientes de validación» del maestro no se imprimen.

```text
ACTA DE INTEGRACIÓN DE LA COMISIÓN MIXTA DEL REGLAMENTO INTERIOR DE TRABAJO

Carátula

| Razón social                          | {{RAZON_SOCIAL}}                                                                         |
| RFC                                   | {{RFC}}                                                                                  |
| Registro patronal IMSS                | {{REGISTRO_PATRONAL}}                                                                    |
| Domicilio                             | {{DOMICILIO_FISCAL}}                                                                     |
| Actividad económica                   | {{ACTIVIDAD_ECONOMICA}}                                                                  |
| Centros de trabajo comprendidos       | {{NUM_CENTROS_TRABAJO}}: {{DOMICILIOS_CENTROS_TRABAJO}}                                  |
| Personas trabajadoras a la fecha      | {{PLANTILLA_NUM}}, manifestado bajo protesta de decir verdad por la representación de la Empresa |
| Turnos                                | {{TURNOS_RESUMEN}}                                                                       |
| Forma de integración                  | {{DESIGNACION_OBRERA}}                                                                   |
| Representantes por cada parte         | {{NUM_REPRESENTANTES_POR_PARTE}}                                                         |
| Lugar, fecha y hora de la sesión      | {{CMRIT_LUGAR}}, {{CMRIT_FECHA}}, de {{CMRIT_HORA_INICIO}} a {{CMRIT_HORA_CIERRE}} horas |

Las personas firmantes, en su calidad de representantes de {{RAZON_SOCIAL}} (la «Empresa») y de las personas trabajadoras, con fundamento en la Ley Federal del Trabajo, hacen constar la integración de la Comisión Mixta del Reglamento Interior de Trabajo (la «Comisión») conforme a lo siguiente.

Antecedentes

[SI SINDICATO = No]
[SI DESIGNACION_OBRERA = Designación]
Primero. Representación de las personas trabajadoras. Las personas trabajadoras designaron como sus representantes, sin intervención de la Empresa, a las personas señaladas en el Acuerdo Primero, quienes aceptaron el cargo.[SI CONFORMIDAD_FIRMAS = Sí] Las personas trabajadoras manifestaron su conformidad con la integración de la Comisión el {{CMRIT_FECHA_CONFORMIDAD}}, como consta en el Anexo 1.[FIN SI]
[FIN SI]
[SI DESIGNACION_OBRERA = Elección]
Primero. Representación de las personas trabajadoras. Las personas trabajadoras eligieron a sus representantes en la jornada de elección celebrada el {{FECHA_JORNADA_ELECCION}}, común a las comisiones mixtas de capacitación y de participación de utilidades, como consta en el acta de esa jornada, que se adjunta.
[FIN SI]
[FIN SI]
[SI SINDICATO = Sí]
Primero. Representación de las personas trabajadoras. La representación de las personas trabajadoras fue designada por {{SINDICATO_NOMBRE}}, titular del contrato colectivo de trabajo, como consta en la constancia de designación que se adjunta.
[FIN SI]

Segundo. Representación de la Empresa. La Empresa designó a sus representantes por conducto de {{REPRESENTANTE_LEGAL_NOMBRE}}, quien cuenta con las facultades necesarias para ello.

Acuerdos

PRIMERO. Integración. La Comisión queda integrada en forma paritaria, con {{NUM_REPRESENTANTES_POR_PARTE}} [SI NUM_REPRESENTANTES_POR_PARTE = 1]representante propietario[FIN SI][SI NUM_REPRESENTANTES_POR_PARTE > 1]representantes propietarios[FIN SI] por cada parte, como sigue:

| Nombre                          | Representación          | Cargo                          | Carácter     |
| {{REP_EMPRESA_NOMBRE}}          | Empresa                 | {{REP_EMPRESA_CARGO}}          | Propietario  |
| {{REP_TRABAJADORES_NOMBRE}}     | Personas trabajadoras   | {{REP_TRABAJADORES_CARGO}}     | Propietario  |

[SI REPRESENTANTES_SUPLENTES = Sí]
| Nombre                              | Representación          | Carácter   |
| {{SUPLENTE_EMPRESA_NOMBRE}}         | Empresa                 | Suplente   |
| {{SUPLENTE_TRABAJADORES_NOMBRE}}    | Personas trabajadoras   | Suplente   |
[FIN SI]

SEGUNDO. Aceptación y garantías del cargo. Cada integrante acepta su cargo y se compromete a desempeñarlo de buena fe. La Empresa reconoce que el desempeño del cargo, las opiniones expresadas y los votos emitidos en la Comisión no serán motivo de represalia, sanción ni trato diferenciado. Las sesiones se celebran dentro de la jornada de trabajo y el tiempo dedicado a ellas es tiempo de trabajo con goce de salario.

TERCERO. Reglas de funcionamiento. La Comisión se rige por las reglas contenidas en esta acta, que sustituyen a cualquier estatuto anterior.

CUARTO. Elaboración del Reglamento. La Comisión formulará el Reglamento Interior de Trabajo dentro de los {{CMRIT_PLAZO_RIT_DIAS}} días naturales siguientes a la firma de esta acta. El plazo podrá ampliarse una sola vez por acuerdo de ambas representaciones, asentado en acta.

QUINTO. Depósito. Firmado el Reglamento, la Coordinación lo depositará ante el Centro Federal de Conciliación y Registro Laboral dentro de los ocho días siguientes a su firma. Si la Coordinación no lo hace, cualquier integrante podrá realizar el depósito. El acuse se integrará al archivo de la Comisión.

SEXTO. Difusión. Dentro de los {{DIAS_DIFUSION_RIT}} días hábiles siguientes al depósito, la Empresa: (a) entregará un ejemplar a cada persona trabajadora, en papel o por medio electrónico, con la constancia de recibo; (b) fijará el Reglamento en los lugares más visibles de cada centro de trabajo y lo acreditará con la constancia de difusión; y (c) entregará un ejemplar, con constancia de recibo, a cada persona de nuevo ingreso. Las tres medidas son concurrentes, no alternativas.

Reglas de funcionamiento de la Comisión

Regla 1. Objeto. La Comisión formula el Reglamento Interior de Trabajo, lo revisa y dictamina sus modificaciones. No investiga conductas, no impone sanciones ni interviene en procedimientos disciplinarios, que corresponden a la Empresa conforme al propio Reglamento.

Regla 2. Cargos. La Coordinación corresponde a la representación de la Empresa: convoca y conduce las sesiones, custodia el archivo y realiza el depósito del Reglamento y de sus modificaciones. La Secretaría corresponde a la representación de las personas trabajadoras: levanta las actas de sesión, verifica el quórum y puede convocar y conducir una sesión cuando la Coordinación no lo haga, sin que cambie la titularidad de esta.[SI NUM_REPRESENTANTES_POR_PARTE > 1] Los demás integrantes participan con voz y voto y canalizan las propuestas de las personas a quienes representan.[FIN SI]

Regla 3. Sesiones. La Comisión sesiona en forma ordinaria al menos una vez al año para revisar la vigencia del Reglamento, y en forma extraordinaria cuando lo solicite cualquiera de las representaciones o se publique una reforma legal que lo afecte. La convocatoria se hace por escrito o por medio electrónico con {{CMRIT_DIAS_CONVOCATORIA}} días hábiles de anticipación, indicando los asuntos a tratar. Las sesiones pueden ser presenciales o a distancia.

Regla 4. Quórum y decisiones. Hay quórum cuando asiste al menos una persona de cada representación. Los acuerdos requieren el voto favorable de la mayoría de las personas presentes de cada representación; ninguna representación puede aprobar un acuerdo por sí sola.

Regla 5. Falta de acuerdo. Si un asunto no se aprueba en dos sesiones consecutivas, se asienta en acta la postura de cada representación y el texto vigente del Reglamento sigue aplicándose, sin perjuicio del derecho de las partes de acudir ante la autoridad laboral en los términos de la Ley.

Regla 6. Personal de confianza. El personal de confianza participa en la designación o en la elección, pero no puede ser representante de las personas trabajadoras.

Regla 7. Sustitución de integrantes. El cargo concluye por terminación de la relación de trabajo, renuncia al cargo comunicada por escrito, ausencia injustificada a dos sesiones consecutivas o, en la representación de las personas trabajadoras, por pasar a ocupar un puesto de confianza. La vacante la cubre el suplente de la misma representación. Sin suplente, la Empresa designa a su representante y las personas trabajadoras designan al suyo[SI CONFORMIDAD_FIRMAS = Sí], con constancia de conformidad,[FIN SI] o lo eligen en la siguiente jornada de elección común, dentro de los {{CMRIT_DIAS_VACANTE}} días naturales siguientes.

Regla 8. Actas y archivo. De cada sesión se levanta un acta con asistencia, asuntos tratados, votación y acuerdos. El archivo comprende esta acta y sus anexos, las actas de sesión, los dictámenes, las versiones del Reglamento y las constancias de depósito, recibo y difusión. Se conserva, en papel o en formato digital, mientras el Reglamento esté vigente y {{CMRIT_ANIOS_CONSERVACION}} años después.

Regla 9. Firma. Esta acta, las actas de sesión, el Reglamento y sus modificaciones se firman de forma autógrafa.

Regla 10. Vigencia. La Comisión es permanente mientras la Empresa tenga centros de trabajo en operación. Sus integrantes duran en el cargo {{CMRIT_DURACION_CARGO_ANIOS}} años y pueden ser designados o elegidos nuevamente.

Firmas

Leída esta acta, sus integrantes la firman de conformidad en {{CMRIT_LUGAR}}, el {{CMRIT_FECHA}}.

| Representación          | Nombre                          | CURP                          | Cargo                          | Firma |
| Empresa                 | {{REP_EMPRESA_NOMBRE}}          | {{REP_EMPRESA_CURP}}          | {{REP_EMPRESA_CARGO}}          |       |
| Personas trabajadoras   | {{REP_TRABAJADORES_NOMBRE}}     | {{REP_TRABAJADORES_CURP}}     | {{REP_TRABAJADORES_CARGO}}     |       |

[SI REPRESENTANTES_SUPLENTES = Sí]
| Representación          | Nombre                              | CURP                              | Cargo      | Firma |
| Empresa                 | {{SUPLENTE_EMPRESA_NOMBRE}}         | {{SUPLENTE_EMPRESA_CURP}}         | Suplente   |       |
| Personas trabajadoras   | {{SUPLENTE_TRABAJADORES_NOMBRE}}    | {{SUPLENTE_TRABAJADORES_CURP}}    | Suplente   |       |
[FIN SI]

[SI DESIGNACION_OBRERA = Designación Y SINDICATO = No Y CONFORMIDAD_FIRMAS = Sí]
ANEXO 1. CONSTANCIA DE DESIGNACIÓN Y CONFORMIDAD DE LAS PERSONAS TRABAJADORAS

Las personas trabajadoras de {{RAZON_SOCIAL}} que firman esta constancia manifiestan que designaron como sus representantes ante la Comisión Mixta del Reglamento Interior de Trabajo a las personas siguientes, y que están de acuerdo con la integración de la Comisión en los términos del acta de la que esta constancia forma parte. Declaran que conocen el objeto de la Comisión y que firman libremente.

| Persona designada                   | Carácter        |
| {{REP_TRABAJADORES_NOMBRE}}         | Propietario  |
[SI REPRESENTANTES_SUPLENTES = Sí]| {{SUPLENTE_TRABAJADORES_NOMBRE}}    | Suplente        |[FIN SI]

| #       | Nombre                | CURP                  | Puesto                | Firma |
| {{N}}   | {{PERSONA_NOMBRE}}    | {{PERSONA_CURP}}      | {{PERSONA_PUESTO}}    |       |

{{CMRIT_LUGAR}}, {{CMRIT_FECHA_CONFORMIDAD}}. Las firmas se recaban de forma autógrafa.
[FIN SI]
```

Reglas del acta:

- Filas repetibles: una por representante (propietario y, con `REPRESENTANTES_SUPLENTES` = Sí, suplente) según `NUM_REPRESENTANTES_POR_PARTE`, en los Acuerdos, las firmas y el Anexo 1.
- Anexo 1: una fila por persona activa del centro o turno (`{{N}}` consecutivo). Con varios turnos o centros, una hoja por turno o centro. Las firmas se recaban de forma autógrafa.
- `DESIGNACION_OBRERA` = Elección: se adjunta el acta de la jornada común (D-02 del kit de PTU). En ninguna variante hay votación secreta.
- `SINDICATO` = Sí: se adjunta la constancia de designación del sindicato; no hay Anexo 1.
- Validaciones: representantes de las personas trabajadoras sin clasificación Confianza; `NUM_REPRESENTANTES_POR_PARTE` ≥ 1; una persona puede representar en más de una comisión.
- `FECHA_ACTA_INTEGRACION` del dictamen del RIT = `CMRIT_FECHA`, y las filas de firmas del RIT (`REP_*`, con CURP) salen del acta: se llenan solas (0.1, regla 4). El RIT no se puede pasar a Firmado sin el acta marcada como firmada.
- CURP obligatoria de 18 caracteres con dígito verificador en cada integrante y en cada persona del Anexo 1 (la del Anexo 1 se toma del alta).

---

## 7. Diferencias de esta especificación respecto del texto del maestro

Son ajustes de impresión, no de contenido. El maestro conserva su redacción.

| # | Dónde | Maestro | Especificación |
| --- | --- | --- | --- |
| 1 | FD-2, FD-4, FD-5 | «… su versión de los hechos: Declaración manuscrita.» | «… su versión de los hechos:» seguido de `[RECUADRO_MANUSCRITO]` |
| 2 | FD-4 punto 5, FD-5 punto 2, FR-1 | Las opciones aparecen entre paréntesis | Se imprime solo la opción elegida |
| 3 | FD-5, bloque de reconocimiento | `{{FD5_TIPO}}` | `{{FD5_TIPO_MINUSCULA}}` |
| 4 | FR-1, medio de entrega | «(Papel · Electrónico, enlace {{RIT_ENLACE}})» | El enlace solo se imprime con `FR1_MEDIO` = Electrónico |
| 5 | FD-3 y FD-5 | «artículo 27 del Reglamento» | «artículo {{REF_ART_27}} del Reglamento» (renumeración, 2.2) |

---

## 8. Diccionario de variables

### 8.1 Variables que vienen de otros módulos (no se capturan aquí)

| Variable | Nivel | De dónde viene | Uso |
| --- | --- | --- | --- |
| RAZON_SOCIAL, NOMBRE_COMERCIAL, RFC, REGISTRO_PATRONAL, DOMICILIO_FISCAL, ACTIVIDAD_ECONOMICA | E | Configuración de la empresa | Dictamen, art. 1, FR-1, FR-2 |
| NUM_CENTROS_TRABAJO, DOMICILIOS_CENTROS_TRABAJO | S | Catálogo de centros de trabajo | Dictamen; arts. 3 y 88; letras de los anexos (2.3); carátula del acta |
| CENTRO_NOMBRE, CENTRO_DOMICILIO, CENTRO_ESTADO, CENTRO_REGISTRO_PATRONAL | O | Catálogo de centros de trabajo (domicilio: calle, número, colonia, código postal y municipio) | Anexo A; hojas del Anexo 1 del acta (nombre) |
| REPSE_EMPRESA | S | Sí si la Empresa tiene folio REPSE vigente | Art. 9 |
| PERIODICIDADES_PAGO_EMPRESA | S | Periodicidades de los puestos del organigrama | Art. 24 |
| PUESTOS_CRITICOS_SEGURIDAD, AREAS_RESTRINGIDAS_EMBARAZO_LACTANCIA, AREAS_RESTRINGIDAS_MENORES | S | Puestos con el atributo correspondiente del organigrama | Arts. 60, 65 y 67; conducta 25 |
| MOD_PRUEBA | E | Configuración de la empresa: «¿La Empresa usa periodo de prueba o capacitación inicial?», Sí/No, sin valor por omisión (diccionario único, decisión P6). Cambiarla con el RIT depositado activa la alerta de depósito | Art. 41 |
| FIRMA_MODALIDAD | A | Paquete de contratación | Solo FR-1; los demás documentos del módulo son autógrafos |
| FIRMANTES_EMPRESA, FIRMA_EMPRESA_NOMBRE, FIRMA_EMPRESA_CARGO | E / S | Especificación de firma electrónica | Firma por la Empresa en FR-1 |
| PLANTILLA_NUM | S | Personas activas a la fecha | FR-2 |
| TURNO_CENTRO, _NOMBRE, _TIPO_JORNADA, _DIAS_LABORABLES, _ENTRADA, _SALIDA, _COMIDA, _DESCANSO_SEMANAL, _HORAS_SEMANA | K | Catálogo de jornadas. TURNO_TIPO_JORNADA = JORNADA_TIPO calculada (Diurna, Nocturna o Mixta; nunca «Rotativa»); TURNO_DESCANSO_SEMANAL = DESCANSO_DIAS (solo Fijo); TURNO_HORAS_SEMANA calculada | Anexo de horarios; días hábiles del expediente |
| TURNO_DESCANSO_TIPO, TURNO_DIAS_TRABAJO_SEMANA | K | Catálogo de jornadas: DESCANSO_SEMANAL (Fijo / Rotativo) y DIAS_TRABAJO_SEMANA (1 a 6, solo Rotativo) | Anexo de horarios |
| TURNOS_ROTATIVOS | S | Sí si algún turno activo tiene descanso Rotativo | Art. 12 |
| FECHA_ACTA_INTEGRACION | C | Acta de la CMRIT | Dictamen |
| REP_EMPRESA_NOMBRE / _CARGO / _CURP, REP_TRABAJADORES_NOMBRE / _CARGO / _CURP, NUM_REPRESENTANTES_POR_PARTE | C | Acta de la CMRIT | Firmas |
| PERSONA_NOMBRE, PERSONA_PUESTO, PERSONA_CENTRO, PERSONA_JEFATURA, PERSONA_CORREO | A | Alta (correo personal) | Todos los formatos |
| BIEN_DESCRIPCION, BIEN_IDENTIFICACION, BIEN_ESTADO_ENTREGA, BIEN_VALOR_REPOSICION, RESGUARDO_FECHA | A | Tabla EQUIPO_DESCRIPCION y resguardo o carta responsiva | FD-3, FD-5 |

### 8.2 Variables del RIT

| Variable | Nivel | Tipo | Valor por omisión o validación | Activa o imprime |
| --- | --- | --- | --- | --- |
| LUGAR_EMISION / FECHA_EMISION | V | Texto / fecha | Obligatorias para pasar a Firmado | Dictamen, firmas, FR-2 |
| REGLA_AJUSTE_JORNADA | E | Opción | anticipando la hora de salida del último día laborable de la semana · anticipando en proporción la hora de salida diaria | Art. 8 y cálculo del ajuste (2.6) |
| DIAS_AVISO_AJUSTE_HORARIO | E | Número | 15 | Art. 8; alerta del ajuste |
| DIAS_ACLARACION_REGISTRO | E | Número | 5 | Art. 13 |
| TOLERANCIA_MIN | E | Número | 10 | Art. 14; conducta 1 |
| DIA_PAGO_SEMANAL | E | Día de la semana | Obligatorio si algún puesto paga semanal | DIAS_PAGO_RESUMEN |
| DIAS_PAGO_QUINCENAL | E | Opción | «15 y último día de cada mes» · «14 y 28 de cada mes» · Otro (texto). Obligatorio si algún puesto paga quincenal | DIAS_PAGO_RESUMEN |
| DIAS_PAGO_RESUMEN | S | Texto | Una parte por periodicidad de PERIODICIDADES_PAGO_EMPRESA: «pago semanal, cada viernes» · «pago quincenal, los días 15 y último de cada mes». Con las dos, separadas por punto y coma | Art. 25 |
| DIAS_ACLARACION_NOMINA / DIAS_RESPUESTA_NOMINA | E | Número | 10 / 5 | Arts. 13 y 26 |
| PERMISO_LEY_NUEVO, _AVISO, _DURACION, _SALARIO, _EVIDENCIA | X | Fila repetible | Vacía por omisión; bloqueada para el cliente | Art. 31, tabla I |
| PERMISOS_EMPRESA (permiso, aviso previo, duración, salario, evidencia) | E | Catálogo editable | Precargado con las 9 filas del maestro; el cliente edita, quita o agrega filas | Art. 31, tabla II |
| DIAS_PERMISO_MATRIMONIO, DIAS_PERMISO_HOSPITALIZACION, DIAS_ADAPTACION_GUARDERIA, HORAS_CITA_MEDICA, CITAS_MEDICAS_AL_MES, DIAS_ASUNTOS_PERSONALES, PERMISOS_HORAS_AL_MES | E | Número | 2, 2, 5, 4, 2, 2, 2 | Filas precargadas de la tabla II |
| GOCE_PERMISO_HOSPITALIZACION | E | Opción | Con goce · Sin goce | Tabla II |
| PERMISO_FALLECIMIENTO | S | Bandera | Sí si la fila «Fallecimiento de familiar» sigue en PERMISOS_EMPRESA | Art. 32 |
| DIAS_FALLECIMIENTO_GRADO_1 / _2 / _3 | E | Número | 3, 2, 1 | Art. 32 |
| KM_FUNERAL_FORANEO / DIAS_FUNERAL_FORANEO | E | Número | 200 / 1 | Art. 32 |
| DIAS_EN_CASA_EMPRESA | E | Sí/No | Sin valor por omisión: «¿La Empresa admite días en casa (teletrabajo o trabajo híbrido)?». Alerta, sin bloqueo, si un alta tiene DIAS_EN_CASA_ACTIVO = Sí y aquí dice No (el RIT no regularía esos días; cambiarla con el RIT depositado exige nuevo depósito). Es distinta de DIAS_EN_CASA_ACTIVO (alta, contrato) | Art. 22 |
| PAGO_DIAS_ESPERA | E | Sí/No | No | Art. 34 |
| VAC_PROGRAMACION_MODO | E | Opción | Calendario anual · Periodos de solicitud por antigüedad · A solicitud; sin valor por omisión. Una sola captura, compartida con el módulo de vacaciones (que configura periodos, bloqueos y cupos) | Art. 36; alerta de depósito si cambia con el RIT depositado |
| MES_CALENDARIO_VACACIONES / DIAS_ANTICIPACION_VACACIONES | E | Mes / número | Mes solo con Calendario anual; sin valor por omisión / 15 | Art. 36 |
| PRIMA_VACACIONAL_PCT | E | Número | 25; ≥ 25 | Art. 37 |
| MOMENTO_PAGO_PRIMA | E | Opción | al inicio del periodo · en la nómina inmediata anterior | Art. 37 |
| ANIOS_CONSERVACION_DISCIPLINARIOS | E | Número | 5 | Art. 43; depuración del expediente |
| MINUTOS_LIMPIEZA / HORARIO_LIMPIEZA_GENERAL | E | Número / texto | 15 / opcional (vacío omite la frase) | Art. 47 |
| PERIODICIDAD_MANTENIMIENTO | E | Opción | mensual · bimestral · trimestral | Art. 48 |
| VEHICULOS_ASIGNADOS | E | Sí/No | No | Art. 50 |
| MINUTOS_DESCANSO_BIPEDESTACION / HORAS_ENTRE_DESCANSOS_BIPEDESTACION | E | Número | 10 / 2 | Art. 54 |
| SIMULACROS_AL_ANIO / UBICACION_PROCEDIMIENTO_PRIMEROS_AUXILIOS | E | Número / texto | 2 / opcional | Arts. 57 y 58 |
| UBICACION_LACTARIO / LACTARIO_EQUIPAMIENTO | E | Texto | Solo con LACTARIO = Sí; — / refrigeración | Art. 66 |
| CANAL_DENUNCIAS / DIAS_ACUSE_DENUNCIA | E | Texto / número | Opcional; vacío omite el art. 74 / 5 | Art. 74 |
| MESES_REINCIDENCIA | E | Número | 12 | Art. 78; catálogo de conductas; FD-3 |
| MESES_CANCELACION_ANTECEDENTES | E | Número | 12; ≥ MESES_REINCIDENCIA | Art. 86; FD-3 |
| RIT_ANTERIOR / FECHA_DEPOSITO_RIT_ANTERIOR | E | Sí/No / fecha | No / — | Transitorio segundo |
| DIAS_EMISION_POLITICAS | E | Número | 60 | Transitorio quinto; alerta |
| NUM_EJEMPLARES | V | Texto | tres | Firmas |
| RETARDOS_FALTA_GRAVE | E | Número | 4 | Conducta 22 |
| RIT_ESTADO / RIT_VERSION | S | Opción / número | Borrador · Firmado · Depositado y vigente | Control de versiones (3.1) |
| RIT_FECHA_DEPOSITO / RIT_ACUSE_DEPOSITO (archivo) | V | Fecha / archivo | Sin acuse no se generan FR-1 ni FR-2 | FR-1, FR-2, alertas |
| RIT_ENLACE | S | URL | PDF de la versión vigente | FR-1 |
| RH_RESPONSABLE_NOMBRE | E | Texto | — | FD-1, FR-2 |
| RESCISION_RESPONSABLE | E | Puesto | No se imprime | Notificación interna de la propuesta de rescisión (4.4) |
| COMITE_INTEGRANTES | E | Catálogo interno (personas o puestos, titular o suplente) | Lo alimenta el documento propio del Comité; no se imprime en el RIT | Selección de COMITE_ASISTENTES en FD-2 y FD-3 |
| LACTARIO | E | Sí/No | Sin valor por omisión; se pregunta antes que la ubicación. Con No, UBICACION_LACTARIO y LACTARIO_EQUIPAMIENTO no se muestran ni se piden | Art. 66 |

### 8.3 Variables del expediente y de los formatos

| Variable | Nivel | Tipo | Validación | Activa o imprime |
| --- | --- | --- | --- | --- |
| EXP_FOLIO | S | Texto | Único por expediente | Todos los FD |
| EXP_TIPO | V | Opción | Disciplinario · Daño | Ruta (4.1); bloque de daño de FD-3 |
| EXP_CONDUCTAS_CATALOGO | V | Selección múltiple del catálogo de conductas | Al menos una | FD-1, FD-4; deriva EXP_NIVEL |
| EXP_NIVEL | S | Opción | Leve · Grave · Muy grave; reglas de 4.2 | Ruta; medidas admitidas (4.4) |
| EXP_TENTATIVA (nueva) | V | Sí/No | No por omisión; Sí baja un nivel | EXP_NIVEL |
| EXP_FECHA_HECHOS, EXP_HORA_HECHOS, EXP_LUGAR_HECHOS, EXP_HECHOS, EXP_REPORTA | V | Fecha, hora, texto | Obligatorios | FD-1, FD-4 |
| EXP_FECHA_CONOCIMIENTO_JEFATURA | V | Fecha | No posterior a la captura | FD-1, FD-3; base de la fecha límite |
| EXP_FECHA_AVISO_COMITE | V | Fecha | ≥ EXP_FECHA_CONOCIMIENTO_JEFATURA; alerta si pasa del día siguiente | FD-1, FD-3; alerta de conducta 43 |
| EXP_FECHA_LIMITE_NOTIFICACION | S | Fecha | Regla de 4.3 | FD-3; alertas y cierre |
| EXP_EVIDENCIA_LISTA, EXP_LUGAR_CONSULTA | V | Lista / texto | Alerta si no hay evidencia | FD-1 |
| EXP_POSIBLE_RESCISION | S/V | Sí/No | Sí en automático si alguna conducta está en la tabla de la sección 9; editable | Párrafo de FD-1 |
| EXP_MEDIDA_PROVISIONAL, _DESCRIPCION, EXP_MEDIDA_INICIO, EXP_MEDIDA_FIN | V | Sí/No, texto, fechas | Siempre con goce de salario | FD-1, punto 6 |
| FD1_FECHA, FD1_FECHA_AUDIENCIA, FD1_HORA_AUDIENCIA, FD1_LUGAR_AUDIENCIA | V | Fecha, hora, texto | Audiencia entre 1 y 5 días naturales después de FD1_FECHA (reglas de 0 y 4.3) | FD-1 |
| FD1_NEGATIVA / FD1_FECHA_ENVIO (y sus equivalentes FD2_, FD3_, FD4_, FD5_, FR1_) | V | Sí/No / fecha | Con Sí: dos testigos obligatorios | Bloques de negativa |
| FD2_LUGAR, FD2_FECHA, FD2_HORA_INICIO, FD2_HORA_CIERRE, FD2_ACOMPANANTE | V | Texto, fecha, hora | — | FD-2 |
| FD2_INASISTENCIA | V | Sí/No | — | Variante de FD-2 |
| FD2_ESCRITO / FD2_ESCRITO_FOJAS | V | Sí/No / número | — | FD-2 |
| FD2_TESTIGOS_DECLARACIONES, FD2_PREGUNTAS | V | Texto | — | FD-2 |
| PRUEBA_DESCRIPCION, PRUEBA_OFERENTE, PRUEBA_ADMITIDA, PRUEBA_OBSERVACIONES | V | Fila repetible | Las no admitidas exigen observación | FD-2 |
| COMITE_ASISTENTES, COMITE_INTEGRANTE_NOMBRE, COMITE_INTEGRANTE_2_NOMBRE | V | Texto | Al menos 2 integrantes; ninguno con relación con los hechos (excusa) | FD-2, FD-3 |
| FD3_FECHA, FD3_HECHOS_ACREDITADOS, FD3_VALORACION, FD3_CONDUCTA_CATALOGO, FD3_NIVEL, FD3_CIRCUNSTANCIAS | V | Fecha, texto, selección | FD3_FECHA ≤ EXP_FECHA_LIMITE_NOTIFICACION | FD-3 |
| FD3_REINCIDENCIA, FD3_ANTECEDENTE_FOLIO, FD3_ANTECEDENTE_FECHA | S | Derivadas del historial | Regla de 4.4 | FD-3; medidas admitidas |
| FD3_RESULTADO | V | Opción | Solo las de la tabla de 4.4 | FD-3, punto 5 |
| FD3_DIAS_SUSPENSION, FD3_SUSPENSION_INICIO, FD3_SUSPENSION_FIN, FD3_REINCORPORACION | V/S | Número, fechas | Días según 4.4, en días laborables del turno; inicio ≤ 10 días naturales después de la notificación (reglas de 0 y 4.3); fin y reincorporación calculados con los días laborables del turno | FD-3 |
| FD3_NEGLIGENCIA | V | Sí/No | Solo con EXP_TIPO = Daño | Bloque de daño de FD-3 |
| FD3_FECHA_NOTIFICACION | V | Fecha | ≤ EXP_FECHA_LIMITE_NOTIFICACION | FD-3; inicio del cómputo de reincidencia |
| FD4_FECHA, FD4_ACUERDO, FD4_MEDIDA | V | Fecha, texto, opción | Solo medidas leves sin reincidencia | FD-4 |
| FD5_LUGAR, FD5_FECHA, FD5_HORA, FD5_TIPO, FD5_FECHA_DETECCION, FD5_HECHOS, FD5_EVIDENCIA | V | Texto, fecha, opción | FD5_TIPO: Daño · Pérdida | FD-5 |
| FD5_TIPO_MINUSCULA (nueva) | S | Texto | Minúscula de FD5_TIPO | FD-5 |
| FD5_RECONOCE | V | Sí/No | No abre FD-1 | FD-5; acuerdo de descuento |
| BIEN_ESTADO_ACTUAL | V | Texto | — | FD-5 |
| DESCUENTO_MONTO, DESCUENTO_PAGOS, DESCUENTO_POR_PAGO | V/S | Moneda, número | Monto ≤ BIEN_VALOR_REPOSICION; límites legales por pago y por deuda; DESCUENTO_POR_PAGO = monto ÷ pagos | FD-3, FD-5, acuerdo de descuento |
| TESTIGO_1_NOMBRE, TESTIGO_2_NOMBRE | V | Texto | Distintos de la persona y de la jefatura | Bloques de negativa; FR-2 |
| FR1_MOMENTO, FR1_MEDIO, FR1_FECHA | V/S | Opción, fecha | Reglas de 3.3 | FR-1 |
| FR2_FECHA | V | Fecha | — | FR-2 |
| FIJACION_CENTRO, FIJACION_LUGARES, FIJACION_FECHA, FIJACION_RESPONSABLE, FIJACION_EVIDENCIA | V | Fila repetible por centro | Una por centro; evidencia obligatoria | FR-2 |
| FR1_RECABADAS, FR1_NEGATIVAS, FR1_PENDIENTES | S | Número / lista | Del registro de FR-1 de la versión | FR-2 |
| REF_ART_27 (y en general REF_ART_n) (nueva) | S | Número | Número final del artículo tras la renumeración | Formatos que remiten al RIT |

### 8.5 Variables del acta de la CMRIT

| Variable | Nivel | Tipo | Validación o valor por omisión | Activa o imprime |
| --- | --- | --- | --- | --- |
| DESIGNACION_OBRERA | E | Opción | Designación (por omisión) · Elección. Común a las tres comisiones | Antecedente primero; Anexo 1 |
| CONFORMIDAD_FIRMAS | E | Sí/No | No por omisión. Común a las tres comisiones | Frase del antecedente; Anexo 1; regla 7 |
| REPRESENTANTES_SUPLENTES | E | Sí/No | Sí por omisión. Común a las tres comisiones | Tablas de suplentes |
| NUM_REPRESENTANTES_POR_PARTE | E | Número | ≥ 1. Común a las tres comisiones | Filas de representantes; regla 2 |
| SINDICATO / SINDICATO_NOMBRE | E | Sí/No / texto | — | Variante sindical |
| REPRESENTANTE_LEGAL_NOMBRE | E | Texto | — | Antecedente segundo |
| TURNOS_RESUMEN | S | Texto | Del catálogo de jornadas | Carátula |
| CMRIT_LUGAR, CMRIT_FECHA, CMRIT_HORA_INICIO, CMRIT_HORA_CIERRE | V | Texto, fecha, hora | Admite fecha futura (0.1, regla 6). CMRIT_FECHA ≤ FECHA_EMISION del RIT | Carátula; firmas; dictamen del RIT |
| CMRIT_FECHA_CONFORMIDAD | V | Fecha | Solo con CONFORMIDAD_FIRMAS = Sí; ≤ CMRIT_FECHA | Antecedente; Anexo 1 |
| FECHA_JORNADA_ELECCION | V | Fecha | Solo con Elección; de D-02 | Antecedente |
| SUPLENTE_EMPRESA_NOMBRE / _CURP, SUPLENTE_TRABAJADORES_NOMBRE / _CURP | C | Fila repetible | Solo con REPRESENTANTES_SUPLENTES = Sí; CURP obligatoria | Acuerdos; firmas; Anexo 1 |
| REP_EMPRESA_CURP, REP_TRABAJADORES_CURP | C | Texto | Obligatoria, 18 caracteres con dígito verificador | Firmas del acta y del RIT |
| PERSONA_CURP | A | Texto | Del alta | Anexo 1 |
| CMRIT_PLAZO_RIT_DIAS / DIAS_DIFUSION_RIT / CMRIT_DIAS_CONVOCATORIA / CMRIT_DIAS_VACANTE / CMRIT_ANIOS_CONSERVACION / CMRIT_DURACION_CARGO_ANIOS | E | Número | 60 / 10 / 5 / 30 / 5 / 2 | Acuerdos cuarto y sexto; reglas 3, 7, 8 y 10 |
| N | S | Número | Consecutivo | Anexo 1 |

### 8.4 Variables eliminadas (no programar)

| Variable | Motivo |
| --- | --- |
| EXP_CONDUCTAS_ANEXO_A, FD3_CONDUCTA_ANEXO_A | Renombradas EXP_CONDUCTAS_CATALOGO y FD3_CONDUCTA_CATALOGO (v1.4) |
| PERIODICIDAD_PAGO | Sustituida por PERIODICIDADES_PAGO_EMPRESA |
| MODULO_TELETRABAJO | Sustituida por DIAS_EN_CASA_EMPRESA |
| MODULO_PAGO_DIAS_ESPERA | Sustituida por PAGO_DIAS_ESPERA |
| REP_PATRONAL_1/2, REP_TRABAJADORES_1/2 | Sustituidas por las filas repetibles REP_EMPRESA_* y REP_TRABAJADORES_* |
| TURNO_1_*, TURNO_2_*, TURNO_3_* | Sustituidas por las filas TURNO_* del catálogo de jornadas |
| DIAS_RESPUESTA_DIAS_EN_CASA, TELE_AVISO_DIAS | Pasan a la política de trabajo híbrido y jornada flexible; el RIT no las imprime |
| EXP_FECHA_CONOCIMIENTO | Sustituida por EXP_FECHA_CONOCIMIENTO_JEFATURA |
| DIA_PAGO | Sustituida por DIA_PAGO_SEMANAL, DIAS_PAGO_QUINCENAL y DIAS_PAGO_RESUMEN |
| ANEXO_COMITE, INTEGRANTES_COMITE, COMITE_PUESTO, COMITE_CARACTER | La integración del Comité sale del RIT (documento propio) |
| RIT_REVISION_FIJACION_MESES | Se elimina la verificación periódica de la fijación |
| ANEXO_POLITICAS, POLITICAS_URL, POLITICAS_RUTA_MENU, POLITICAS_ACCESO, POLITICAS_RESPONSABLE_PUESTO, POLITICAS_CAPTURA, POLITICAS_CAPTURA_FECHA, POLITICAS_UBICACION_FISICA | Se quita del RIT el anexo de ubicación de las políticas |
| CMRIT_INTEGRACION_MODO, CMRIT_SUPLENTES | Sustituidas por DESIGNACION_OBRERA y REPRESENTANTES_SUPLENTES (criterio común, 02/11/2026) |
| FD2_VERSION, FD2_MANIFESTACIONES_FINALES, FD4_VERSION, FD5_VERSION | Las declaraciones son manuscritas (`[RECUADRO_MANUSCRITO]`) |
| PERIODICIDAD_EXAMEN_MEDICO, DIAS_INCAPACIDAD_EXAMEN_RETORNO, DIAS_AVISO_EXAMEN_MEDICO | El art. 59 vigente ya no las usa |
| ANIOS_CONSERVACION_EXPEDIENTE_CLINICO | El art. 61 vigente fija el plazo en el texto |

---

## 9. Tabla de correspondencia del catálogo de conductas con el art. 47 LFT (uso interno; no se imprime)

Uso en este módulo: marcar `EXP_POSIBLE_RESCISION` y habilitar «Propuesta de rescisión» en FD-3. Se muestra a RH y al Comité como referencia, nunca en un documento. Desde la v1.3 del módulo 4 el aviso de rescisión es servicio aparte, así que la tabla ya no alimenta ningún documento.

| Conducta | Fracción del art. 47 LFT |
| --- | --- |
| 23, 44 | X, solo si se acumulan más de tres faltas injustificadas en 30 días |
| 26 | XI |
| 29, 30, 46 | XII |
| 36, 39 | IX, solo si la información es un secreto o asunto reservado |
| 45, 59 | II |
| 47 | VII |
| 48 | V si hay dolo; VI si hay negligencia grave; VII si compromete la seguridad |
| 49 | XIII si se presenta o labora en ese estado; en otro caso, XV (valorar) |
| 50 | XIII |
| 51, 52, 55, 60 | XV (valorar) |
| 53 | II si es contra la Empresa, sus familiares o su personal directivo o administrativo; III si es contra compañeros y altera la disciplina; IV si es fuera del servicio |
| 54 | VIII |
| 56 | II; IX si son secretos o asuntos reservados |
| 57 | V |
| 58 | IX |

Para las conductas 23 y 44, el sistema solo marca la posible rescisión si el historial de asistencia registra más de tres faltas injustificadas en 30 días.

---

## 10. Dependencias con otros módulos

| Módulo | Qué necesita este módulo | Qué le da este módulo |
| --- | --- | --- |
| Paquete de contratación (módulo 1) | FIRMA_MODALIDAD, correo personal, resguardo o carta responsiva con valor de reposición | FR-1 en cada alta |
| Organigrama | Atributos de puesto: crítico para la seguridad, riesgo para embarazo o lactancia, vedado a menores, clasificación | — |
| Catálogo de jornadas | Turnos para el anexo de horarios y días laborables para los plazos | Alerta de depósito al cambiar un turno |
| Acta de la CMRIT (6.9) | FECHA_ACTA_INTEGRACION y representantes | — |
| Kit de PTU (D-01, D-02) | Acta de la jornada común si DESIGNACION_OBRERA = Elección | — |
| Firma electrónica | FIRMANTES_EMPRESA, FIRMA_EMPRESA_DOC (FR-1: representante al ingreso, RH designado después) | El RIT y el acta de la CMRIT en la lista de firma autógrafa obligatoria |
| Acuerdo de descuento | — | Origen del descuento: FD-5 (reconocimiento) o FD-3 (resolución) |
| Módulo 4 (terminación) | — | Expediente concluido para una deducción por pérdida o daño en el finiquito |
| Módulo 5 (modificaciones) | Versión de condiciones de cada persona (jornada) | Cambio de turno del catálogo: comunicado o convenio al personal vigente; lote de 2.6: MOD-2 «Ajuste legal de jornada» |
| Módulo de vacaciones y aguinaldo | Periodos de solicitud, bloqueos y cupos (`VAC_PERIODOS_SOLICITUD`, `VAC_BLOQUEOS`, `VAC_CUPOS`) | Art. 36, con `VAC_PROGRAMACION_MODO` |
| Políticas internas | Registro de políticas y acuses | Alerta del transitorio quinto |
| Documento de integración del Comité de Integridad y Disciplina (Axia Compliance, por redactar) | COMITE_INTEGRANTES | Art. 79 |
| Módulo de permisos y licencias | Eventos de ausencia, alerta de patrón de ausentismo (conducta 60), regla de evidencia vencida, COMISION_GOCE | Reglas de los arts. 30 a 34 y tablas I y II |
| Kit de PTU | — | Criterio de días computables (art. 31) |

---

## 11. Pendientes

### 11.1 Propuestas de programación que debe confirmar el usuario

No están en el maestro ni en el registro; se incluyen para que el programa no quede sin regla.

1. Alertas del plazo a 10, 5 y 2 días naturales, y cierre del expediente al vencer (4.3).
2. Falta leve con reincidencia: como FD-4 no admite suspensión, el sistema cambia la ruta a FD-1 → FD-3 (4.4).
3. Variable `EXP_TENTATIVA` para la conducta intentada (4.2).
4. Conducta 21 seleccionable solo si la política tiene acuse (sección 5).
5. `[RECUADRO_MANUSCRITO]` de 15 renglones (sección 0).

### 11.2 Puntos del maestro que conviene revisar antes de congelar la versión

Detectados al preparar esta especificación. No se cambiaron en el maestro porque son de fondo.

| Artículo | Situación | Riesgo o efecto |
| --- | --- | --- |
| 59 | Se quitaron los tipos de examen y la regla de que RH solo recibe el dictamen de aptitud | Tres variables quedan sin uso (8.4). El registro (4.4) y el aviso de privacidad del kit siguen diciendo que RH solo recibe el dictamen |
| 61 | Fija «2 años» después de la terminación | Sustituye a ANIOS_CONSERVACION_EXPEDIENTE_CLINICO (5) y sigue pendiente verificar el plazo de las normas sanitarias |
| Catálogo de conductas, conductas 20, 21 y 25 | Nivel variable dentro del texto («grave si…», «muy grave en…») | Se programó con casillas (4.2); confirmar |

### 11.3 Verificaciones legales que no bloquean la programación

- Fracciones del art. 47 de la tabla de la sección 9 contra el texto oficial vigente de la LFT.
- Disposiciones de la STPS del registro electrónico de jornada (vigencia 1/01/2027): pueden cambiar el art. 13, el medio alterno y el plazo de aclaración.
- Frecuencia de descansos por bipedestación (art. 54).
- Plazo de conservación del expediente clínico (art. 61).
- Requisitos vigentes del depósito ante el CFCRL.
- Límites legales de descuento por deudas para la tabla del sistema (4.5).

Si cambian, afectan valores por omisión y textos, no la estructura.
