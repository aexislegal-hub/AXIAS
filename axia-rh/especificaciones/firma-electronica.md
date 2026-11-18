# AXIARH — Firma electrónica — Especificación funcional para programación

Versión 1.4 · 18/11/2026 · Responsable: Damián Torres
Decisiones de origen: «Corte - Firma electrónica» y registro, sección 4.11. Cláusula del contrato: VIGÉSIMA SEGUNDA, «Formalización por medios electrónicos» (CL_FIRMA_ELECTRONICA).

Cambios de la v1.1: se agrega el firmante designado de RH como firmante de la Empresa.
Cambios de la v1.2: todo lo que se firma en el alta lo firma el representante; RH designado firma documentos posteriores.
Cambios de la v1.3: verificación remota de identidad con INE y video de aceptación, opcional para la persona.
Cambios de la v1.4 (encargos del mapa del 13, 17 y 18/11/2026): la verificación con INE y video es **solo para la contratación**; el cambio de correo o teléfono se verifica de forma presencial (secciones 2, 5.7 y 5.9). Se amplía la lista de firma autógrafa obligatoria (sección 1). Se agregan a la sección 11 los documentos de los módulos 5 y 8.

Este documento dice **qué** debe hacer el sistema: pantallas, estados, validaciones y bloqueos. **Cómo** se implementa (librerías, proveedores de correo, SMS y verificación de identidad, conexión con el SAT y con el INE, almacenamiento) lo decide el programador; sus decisiones están listadas en la sección 10.

---

## 1. Alcance

- Firma de los documentos generados por Axia RH con FIRMA_MODALIDAD = Electrónica: contrato y anexos, kit de contratación, FR-1, nuevas versiones del perfil de puesto, recibo de PTU (D-14), documentos de los módulos de permisos y licencias y de modificación de condiciones, comunicados y demás documentos que remiten a la cláusula de formalización por medios electrónicos.
- **Firma autógrafa obligatoria**, sea cual sea FIRMA_MODALIDAD. El sistema los genera para imprimir y no permite enviarlos a firma electrónica:
  - convenio de terminación y finiquito, y recibo de finiquito;
  - acuerdo de descuento;
  - el RIT y el acta de integración de la CMRIT (documentos del depósito ante el CFCRL);
  - formatos disciplinarios FD-1 a FD-5;
  - constancia de difusión del RIT (FR-2);
  - FON-1, aviso sobre el crédito Fonacot (firma autógrafa de recibido).
- La FR-1 sigue FIRMA_MODALIDAD en sus tres momentos (emisión, ingreso y modificación). Es autógrafa solo cuando la persona firma en papel, cuando falla la Plataforma o cuando se niega a firmar.
- Sin firma: los registros que se resuelven en la Plataforma (SP-1 y SUS-3 del módulo de permisos; ACT-1 del módulo 5). Su prueba es la bitácora; se rigen por la especificación de su módulo.
- Firmantes:
  - la Persona Trabajadora (FES o e.firma);
  - por la Empresa, según el momento y el tipo de documento (sección 11): el representante legal (siempre e.firma) o la persona de RH designada (FIRMANTES_EMPRESA).

## 2. Tipos de firma y verificación de identidad

| Tipo | Quién | Cómo se firma | Prueba de identidad | Prueba de integridad |
|---|---|---|---|---|
| FES | Persona Trabajadora (por omisión) | Código de un solo uso al correo personal y, según FES_CANAL_OTP, al celular | Verificación en el alta (MEDIO_IDENTIFICACION) + control del correo y del celular | Hash SHA-256 del PDF final + copia al correo personal + constancia NOM-151 si NOM151_SERVICIO = Sí |
| FES institucional | Firmante designado de RH | Su usuario de la Plataforma + código de un solo uso a su correo institucional y, según FES_CANAL_OTP, a su celular | Designación firmada por el representante con e.firma (5.6) + usuario + control del correo institucional | Igual que la FES |
| e.firma | Persona Trabajadora (opcional), representante legal (siempre) y firmante de RH (opcional, si registra su certificado) | Certificado (.cer) y llave privada (.key) del SAT, firmando en el dispositivo de quien firma | Certificado emitido por el SAT, validado al firmar | La propia firma criptográfica + hash + copia al correo |

Medios de verificación de identidad en la contratación (MEDIO_IDENTIFICACION):

| Medio | Cómo | Cuándo procede |
|---|---|---|
| Presencial | RH revisa la identificación oficial y la persona confirma correo y celular con códigos (5.2) | Siempre |
| INE y video de aceptación | Validación de la credencial para votar con el INE, prueba de vida, cotejo facial y video de aceptación (5.9) | Solo en la contratación, con IDV_SERVICIO = Sí, persona con credencial para votar y consentimiento expreso (BIOMETRICO_FIRMA_CONSENT = Sí) |
| e.firma | El certificado del SAT acredita la identidad | Si la persona firma con e.firma |
| Remota sin verificación | Sin verificación | Con advertencia y alerta permanente |

Reglas absolutas:
- La plataforma **nunca** solicita, recibe, transmite ni almacena el archivo .key ni la contraseña de la e.firma. La firma se genera en el navegador o dispositivo del firmante; al servidor solo llegan la firma resultante y el certificado público (.cer).
- La verificación con INE y video **nunca** es obligatoria y **solo se usa en la contratación**. Quien no otorgue el consentimiento, lo revoque o no tenga credencial para votar se verifica de forma presencial, con e.firma o firma en papel, sin ninguna consecuencia laboral.

## 3. Configuración y datos

### 3.1 Configuración de la empresa (nivel 1)

| Variable | Tipo | Validación |
|---|---|---|
| PLATAFORMA_FIRMA | Texto | Obligatoria si algún alta usa firma electrónica |
| FES_CANAL_OTP | Lista: Correo / Correo y SMS | Por omisión Correo y SMS. Aplica a la Persona Trabajadora y al firmante de RH |
| NOM151_SERVICIO | Sí / No | Por omisión No |
| IDV_SERVICIO | Sí / No | Por omisión No. Con Sí, el alta ofrece la verificación con INE y video. Se cobra aparte por el costo del proveedor |
| FIRMA_ENLACE_DIAS | Entero | Por omisión 5; mínimo 1, máximo 30 |
| Registro del representante con e.firma | Carga del .cer únicamente | Se validan con el SAT: vigencia, no revocación y que el RFC coincida con el del representante registrado. Se guardan REP_EFIRMA_RFC y REP_EFIRMA_VIGENCIA |
| FIRMANTES_EMPRESA | Tabla: persona trabajadora, puesto, correo institucional, celular (obligatorio con Correo y SMS), fecha de inicio, fecha de fin (opcional), folio de designación | Solo personas trabajadoras activas de la Empresa, en puestos con clasificación Confianza. El correo debe ser del dominio institucional de la empresa. Cada fila nace de una designación firmada por el representante (5.6). Si no hay ninguno vigente, ver la sección 11 |
| FIRMA_EMPRESA_DOC | Por tipo de documento y momento (Alta / Posterior): Representante / RH designado | Valores fijos de la sección 11. Todo documento con momento Alta es «Representante» sin excepción. La empresa puede subir un documento posterior de «RH designado» a «Representante», nunca al revés |

Puede haber más de un representante y más de un firmante de RH; la empresa elige quién firma cada documento o lote.

### 3.2 Alta de la persona trabajadora (nivel 3)

| Variable | Tipo | Validación |
|---|---|---|
| FIRMA_MODALIDAD | Autógrafa / Electrónica | Existente |
| TIPO_FIRMA | FES / e.firma | Solo con Electrónica; por omisión FES |
| MEDIO_IDENTIFICACION | Presencial / INE y video de aceptación / e.firma / Remota sin verificación | «INE y video de aceptación» solo aparece con IDV_SERVICIO = Sí. Con TIPO_FIRMA = e.firma, el sistema propone e.firma. «Remota sin verificación» exige confirmar una advertencia y genera alerta permanente en el expediente |
| BIOMETRICO_FIRMA_CONSENT | Sí / No, con fecha y hora | Lo otorga la propia persona en la pantalla de consentimiento (5.9, paso 1); RH no lo captura. Sin «Sí», no se habilita la verificación con INE y video |
| TRAB_EMAIL | Correo | Existente; obligatorio |
| TRAB_TELEFONO | Celular, 10 dígitos | Existente; obligatorio con FES y FES_CANAL_OTP = Correo y SMS |
| PORTAL_DESCARGA | Texto | Existente; prellenado con la intranet |

### 3.3 Datos que se imprimen del firmante de la Empresa

- Con «Representante»: REP_NOMBRE y su carácter.
- Con «RH designado»: FIRMA_EMPRESA_NOMBRE y FIRMA_EMPRESA_CARGO, que el sistema toma del firmante que firmó. No se capturan a mano.
- Los formatos con una fila fija «Recursos Humanos» (por ejemplo, FR-1) imprimen el firmante que corresponda según la sección 11.

## 4. Estados del documento

| Estado | Significa | Pasa a |
|---|---|---|
| Borrador | Generado, aún editable | Listo para firma · Cancelado |
| Listo para firma | Validado por RH; ya no se edita. Se calcula el hash del PDF sin firmas | En firma |
| En firma – Persona Trabajadora | Solicitud enviada; corre el plazo FIRMA_ENLACE_DIAS | En firma – Empresa · Rechazado · Vencido · Firma autógrafa |
| En firma – Empresa | Firmó la Persona Trabajadora; falta el firmante de la Empresa que corresponde (representante o RH designado) | Firmado · Vencido |
| Firmado | Firmaron todos; se generan el PDF final y la hoja de evidencias, se calcula el hash final y se envía la copia | Con constancia (si NOM151_SERVICIO = Sí) |
| Con constancia | Se recibió la constancia NOM-151 | Estado final |
| Rechazado | La Persona Trabajadora rechazó firmar, con motivo obligatorio | Borrador (versión nueva) · Firma autógrafa |
| Vencido | Venció el plazo sin firma | Listo para firma (reenvío) · Firma autógrafa |
| Firma autógrafa | Se imprimió para firma en papel | Firmado en papel (al cargar el escaneo) |
| Cancelado | RH lo canceló antes de que firmaran todos | Estado final; se conserva con su bitácora |

Reglas:
- Un documento en «Listo para firma» o posterior no se puede editar. Cualquier cambio genera una versión nueva, que requiere nuevas firmas; la versión anterior se conserva.
- Orden de firma: primero la Persona Trabajadora y después la Empresa. En los documentos que firma solo la Empresa (por ejemplo, SUS-1 cuando la persona no está disponible), firma la Empresa y el documento se envía a la persona.
- Con MEDIO_IDENTIFICACION = INE y video de aceptación, los documentos del alta no se pueden enviar a firma mientras la verificación (5.9) no esté aprobada.
- El firmante de RH no puede firmar por la Empresa un documento en el que él mismo es la Persona Trabajadora. Ese documento pasa a otro firmante de RH o al representante.
- Si la Persona Trabajadora rechaza el **contrato**: alerta crítica a RH y a consultoría. La relación de trabajo existe aunque no haya contrato firmado, y la falta del escrito se imputa a la Empresa; RH debe resolverlo en papel o documentar la negativa con dos testigos, como en las demás constancias.
- Recordatorios automáticos a la persona a los 2 días y el día anterior al vencimiento.

## 5. Pantallas

### 5.1 RH — Bandeja de firmas
- Lista de documentos por estado, persona, tipo de documento, firmante de la Empresa y fecha.
- Acciones: enviar a firma, reenviar, cancelar, pasar a firma autógrafa, reasignar firmante de la Empresa, descargar paquete probatorio.
- Indicadores: pendientes de la persona, pendientes del representante, pendientes del firmante de RH, verificaciones de identidad pendientes o fallidas, vencidos, rechazados, sin verificación de identidad.

### 5.2 RH — Verificación presencial
Se usa en la primera firma (contratación) y en todo cambio de correo o teléfono (5.7).
1. RH revisa la identificación oficial y marca: tipo de identificación, últimos 4 caracteres del folio y «verifiqué que coincide con la persona». No se guarda imagen de la identificación en este paso.
2. El sistema envía un código al correo y otro al celular; la persona los teclea en ese momento.
3. Si ambos son correctos, se registran en la bitácora: RH que verificó, fecha y hora, medios confirmados. En la contratación, MEDIO_IDENTIFICACION = Presencial.
4. En la contratación, la persona firma después los documentos del alta en la misma sesión.

### 5.3 Persona Trabajadora — Firma con FES
1. Recibe el enlace en su correo personal (y aviso por SMS si aplica).
2. Ve el documento completo; el botón de firmar se habilita después de mostrar todo el documento. Puede descargarlo.
3. Marca la casilla «Leí el documento y acepto firmarlo electrónicamente».
4. Solicita el código; lo recibe por el canal configurado; lo teclea.
5. Confirmación en pantalla y correo con la copia (al terminar todas las firmas).
6. Opción «Rechazar» con motivo obligatorio.

Reglas del código: 6 dígitos, vigencia de 10 minutos, 3 intentos; después, bloqueo de 15 minutos y alerta a RH. Valores propuestos, ajustables por el programador sin cambiar el texto legal.

### 5.4 Persona Trabajadora — Firma con e.firma
1. Igual que 5.3, pasos 1 a 3.
2. Selecciona su .cer y su .key y teclea su contraseña. La firma se genera en su dispositivo.
3. El sistema valida con el SAT el certificado: vigencia, no revocación y que el RFC o la CURP coincidan con los del alta. Si falla, no se acepta la firma y se le ofrece FES (si la empresa lo permite) o firma autógrafa.

### 5.5 Empresa — Firma
**Representante legal (por lote).**
- Ve los documentos que le corresponden en «En firma – Empresa», con filtro y selección múltiple. Los documentos del alta de una misma persona aparecen agrupados.
- Puede revisar cada uno antes de firmar.
- Firma el lote con una sola carga de .cer, .key y contraseña; el sistema genera una firma **por documento**, nunca una firma para el lote.
- Antes de firmar se valida el certificado con el SAT. Vencido o revocado: no se firma.

**Firmante designado de RH (por documento).**
- Entra con su usuario y ve solo los documentos de tipo «RH designado» que tiene asignados.
- Ve el documento completo, marca «Leí el documento y lo firmo en representación de la Empresa» y teclea el código de un solo uso que recibe en su correo institucional (y en su celular, según FES_CANAL_OTP). Si registró su e.firma, puede firmar con ella.
- Antes de firmar, el sistema verifica que la designación esté vigente. Si no lo está, no se firma.

### 5.6 Configuración — Firmantes de la Empresa
**Representantes.**
- Alta del representante con su .cer (solo el certificado público).
- Muestra la vigencia; alerta 30 días antes del vencimiento a consultoría y al contacto de la empresa.
- Certificado vencido o revocado: bloqueo de nuevos envíos a firma electrónica de los documentos que firma el representante (incluidos todos los del alta), hasta que se cargue uno vigente o se registre otro representante. Los documentos en firma se quedan en espera.

**Firmantes designados de RH.**
1. El representante elige a una persona trabajadora activa de la Empresa. El sistema solo muestra puestos con clasificación Confianza.
2. El sistema genera la constancia de designación (texto en 5.8), con folio, y el representante la firma con su e.firma.
3. La persona designada confirma su correo institucional (y su celular, si aplica) con un código.
4. Con los tres pasos completos, la designación queda vigente desde la fecha de inicio.

Revocación: la hace el representante en cualquier momento, también con e.firma. Es automática si la persona designada causa baja, cambia a un puesto que no sea de confianza o llega la fecha de fin. Los documentos que tenía asignados vuelven a «En firma – Empresa» para reasignarlos; alerta a RH. Las designaciones revocadas y su bitácora se conservan.

### 5.7 Persona Trabajadora — Cambio de correo o teléfono
- Lo inicia RH. La identidad se verifica siempre de forma presencial (5.2), sin biometría, aunque en la contratación se haya usado la verificación con INE y video.
- El sistema envía un código al medio nuevo; la persona lo confirma.
- Hasta la confirmación, sigue vigente el medio anterior. Todo queda en la bitácora.

### 5.8 Texto de la constancia de designación

```text
CONSTANCIA DE DESIGNACIÓN DE FIRMANTE · Folio {{DESIGNACION_FOLIO}}

{{PATRON_RAZON_SOCIAL}}, por conducto de su representante {{REP_NOMBRE}}, designa a {{FIRMANTE_NOMBRE}}, quien ocupa el puesto de {{FIRMANTE_PUESTO}} y ejerce en él funciones de dirección o administración, para firmar en representación de la Empresa, por medios electrónicos, los documentos que la Plataforma {{PLATAFORMA_FIRMA}} le asigne conforme a su tipo, a partir del {{DESIGNACION_INICIO}}[SI DESIGNACION_FIN] y hasta el {{DESIGNACION_FIN}}[FIN SI].

{{FIRMANTE_NOMBRE}} firmará con su usuario de la Plataforma y el código de verificación de un solo uso que reciba en su correo institucional {{FIRMANTE_CORREO}}[SI FES_CANAL_OTP = Correo y SMS] y en su teléfono {{FIRMANTE_TELEFONO}}[FIN SI], o con su firma electrónica avanzada. Esos medios están bajo su exclusivo control.

La designación termina al revocarla la Empresa, al concluir la relación de trabajo de la persona designada, al cambiar esta a un puesto sin funciones de dirección o administración o en la fecha de fin señalada.

{{LUGAR_FIRMA}}, a {{FECHA_FIRMA}}.

LA EMPRESA ({{REP_NOMBRE}}, firma electrónica avanzada) · PERSONA DESIGNADA ({{FIRMANTE_NOMBRE}})
```

### 5.9 Persona Trabajadora — Verificación con INE y video de aceptación (solo en la contratación)

Se usa solo en el alta, antes de los documentos de contratación. Los demás documentos se firman con el código, y el cambio de correo o teléfono se verifica de forma presencial (5.7).

1. **Consentimiento.** Antes de cualquier captura, la persona ve una pantalla con la finalidad (verificar su identidad para la firma electrónica de su contratación), los datos que se tratan (imagen de su credencial para votar, imagen y voz del video, cotejo facial), quién los trata (la Empresa y el proveedor de verificación, como encargado), cuánto se conservan y la alternativa sin biometría (verificación presencial, e.firma o papel). Elige entre «Acepto» y «Prefiero verificarme de otra forma», con el mismo peso visual. El «Acepto» se confirma con un código de un solo uso a su correo personal. El sistema guarda BIOMETRICO_FIRMA_CONSENT con fecha y hora y la versión del texto de consentimiento. Si elige la otra forma, RH recibe aviso para la verificación presencial; no hay ninguna consecuencia laboral.
2. **Credencial.** La persona fotografía el anverso y el reverso de su credencial para votar. El proveedor valida con el INE que la credencial esté vigente y que sus datos coincidan; el sistema compara además nombre y CURP con los del alta.
3. **Prueba de vida y cotejo.** El proveedor confirma que hay una persona real frente a la cámara (no foto, pantalla ni máscara) y coteja su rostro con la fotografía de la credencial.
4. **Video de aceptación.** La persona graba un video de máximo 30 segundos leyendo el guion que muestra la pantalla: «Yo, {{TRAB_NOMBRE}}, el {{FECHA_VIDEO}}, acepto firmar por medios electrónicos mi contrato de trabajo con {{PATRON_RAZON_SOCIAL}} y los documentos de mi contratación. Código {{CODIGO_VIDEO}}». CODIGO_VIDEO es un número aleatorio que genera el sistema para esa grabación, para impedir que se reutilice un video anterior.
5. **Resultado.** Aprobada: MEDIO_IDENTIFICACION = INE y video de aceptación y se habilita el envío de los documentos del alta. Fallida: se permite un segundo intento; si vuelve a fallar, RH recibe alerta y la persona se verifica de forma presencial, con e.firma o en papel. Una verificación fallida no impide la contratación.

Conservación y supresión:
- Se conservan, como evidencia de la firma: el resultado de la validación con el INE (sin la imagen de la credencial, si el proveedor lo permite), el resultado de la prueba de vida y del cotejo (aprobado o fallido, con su fecha y hora), el video de aceptación y la bitácora.
- La plantilla biométrica (el modelo matemático del rostro) se borra después del cotejo. El proveedor no conserva imágenes, video ni plantillas una vez entregado el resultado.
- Si la persona revoca el consentimiento, no se hace ningún nuevo tratamiento biométrico; el video ya grabado se conserva solo como prueba del acto que firmó, durante el plazo de conservación del documento.
- Personas sin credencial para votar (por ejemplo, extranjeras): la opción no se ofrece; verificación presencial, e.firma o papel.

## 6. Bitácora y hoja de evidencias

Cada evento se registra con: fecha y hora (hora del servidor sincronizada, en UTC y en hora local), IP, dispositivo y navegador, usuario o firmante, acción y resultado.

Eventos mínimos: generación; paso a «Listo para firma» con su hash; envío de la solicitud; apertura del enlace; visualización completa; aceptación de la casilla; solicitud y envío del código (canal y destino enmascarado, p. ej. c\*\*\*@dominio y \*\*\*\*1234); validación del código (correcta o fallida); consentimiento biométrico (otorgado, negado o revocado, con la versión del texto); validación de la credencial con el INE, prueba de vida, cotejo y video (resultado, intento, proveedor e identificador de la transacción); verificación presencial (RH que verificó); firma con e.firma (número de serie, emisor, vigencia y resultado de la validación del certificado, con fecha y hora); rechazo con motivo; vencimiento; cancelación; reasignación del firmante de la Empresa; firma de la Empresa; hash final; envío de la copia; constancia NOM-151 (folio, PSC, fecha). Para el firmante de RH: verificación de la designación vigente y su folio.

La **hoja de evidencias** es la última página del PDF final y contiene: datos del documento y versión; firmantes con nombre, RFC o CURP, tipo de firma y medio de identificación (con INE y video: resultado y fecha de la verificación, e identificador del video); para el firmante de RH, su puesto y el folio de su designación; la cronología de eventos; el hash del documento sin firmas y el hash final. No contiene imágenes de la credencial ni del rostro. La constancia NOM-151, si existe, se emite sobre el PDF que ya incluye la hoja de evidencias.

## 7. Cierre del documento

Al firmar el último firmante:
1. Se genera el PDF final con las firmas visibles y la hoja de evidencias.
2. Se calcula el hash SHA-256 del PDF final.
3. Si NOM151_SERVICIO = Sí, se solicita la constancia al PSC.
4. Se guarda en almacenamiento que no permita modificar ni borrar el archivo.
5. Se envía el PDF al correo personal de la Persona Trabajadora, con el hash escrito en el cuerpo del correo, y se publica en PORTAL_DESCARGA.
6. Se registra el envío del correo y su resultado (entregado, rebotado). Rebote: alerta a RH.

## 8. Paquete probatorio exportable

Por documento, un archivo comprimido con: el PDF final; la bitácora completa en formato legible por máquina (JSON o XML); en e.firma, los archivos de firma y los certificados públicos; la constancia NOM-151 si existe; si firmó RH, la constancia de designación vigente a la fecha de la firma; si la identidad se verificó con INE y video, el video de aceptación con su hash, el comprobante del consentimiento y los resultados de la verificación; y una hoja de instrucciones para el perito: cómo recalcular los hash y cómo verificar cada firma. Se puede descargar por documento o por persona trabajadora. El acceso al video queda restringido a RH y consultoría y cada descarga se registra.

## 9. Alertas

| Alerta | Cuándo | A quién |
|---|---|---|
| Identidad no verificada | Alta con MEDIO_IDENTIFICACION = Remota sin verificación | RH y consultoría; permanente en el expediente |
| Verificación con INE y video fallida | Al segundo intento fallido | RH; se ofrece verificación presencial |
| Persona prefirió verificación sin biometría | Al elegir «Prefiero verificarme de otra forma» | RH, para agendar la verificación presencial |
| Firma pendiente | 2 días y día anterior al vencimiento | Persona Trabajadora y RH |
| Documento vencido | Al vencer FIRMA_ENLACE_DIAS | RH |
| Contrato rechazado o vencido | Inmediata, crítica | RH y consultoría |
| Código bloqueado | 3 intentos fallidos | RH |
| Correo rebotado | Al fallar el envío de la copia | RH |
| e.firma del representante por vencer | 30 días antes | Consultoría y contacto de la empresa |
| e.firma del representante vencida o revocada | Inmediata; bloquea los envíos que firma el representante | Consultoría y contacto de la empresa |
| Designación de RH revocada o terminada | Inmediata; sus documentos pendientes vuelven a reasignación | RH y representante |
| Sin firmante de RH vigente | Al enviar un documento de tipo «RH designado» | RH; el documento pasa al representante (sección 11) |
| Documento autógrafo obligatorio | Si alguien intenta enviarlo a firma electrónica | Bloqueo con mensaje |

## 10. Decisiones técnicas del programador

1. Validación del certificado del SAT (vigencia, cadena de confianza y revocación) y su registro como evidencia.
2. Firma con e.firma en el navegador o dispositivo del firmante, sin que la llave privada ni la contraseña salgan de él; formato de la firma.
3. Proveedores de correo y SMS: entregabilidad, registro de entrega y rebote.
4. Generación del PDF final y de la hoja de evidencias; cálculo del hash SHA-256.
5. Sincronización de la hora del servidor.
6. Almacenamiento no modificable y respaldos.
7. Integración opcional con un PSC para la constancia NOM-151.
8. Formato del paquete probatorio.
9. Seguridad de los enlaces de firma (de un solo uso, ligados a la persona y con caducidad).
10. Control de acceso del firmante de RH: solo ve y firma los documentos de tipo «RH designado» que tiene asignados.
11. Marcar cada documento con su momento (Alta / Posterior) al generarlo, para asignar el firmante de la Empresa.
12. Proveedor de verificación de identidad: que tenga convenio vigente con el INE para la verificación de datos de la credencial y, si se usa, para el cotejo facial; prueba de vida resistente a fotos, pantallas, máscaras y videos manipulados; borrado de plantillas e imágenes después del resultado; servidores y transferencias conforme a la ley de datos personales. Integración por API y registro del identificador de cada transacción. Solo se invoca en el flujo de contratación.
13. Grabación del video en el navegador o la app: duración máxima, calidad mínima, hash del archivo al cerrarse la grabación y almacenamiento cifrado con acceso restringido.

## 11. Quién firma por la Empresa (FIRMA_EMPRESA_DOC)

**Regla principal (decidida, 12/11/2026):** todo documento que se firma en el alta lo firma por la Empresa el representante legal, sin importar su tipo. Comprende el contrato y sus anexos (perfil de puesto, designación de beneficiarios, Anexo 3 de acuses y aviso de privacidad), el convenio de confidencialidad y su Anexo A, la carta responsiva, la asignación de correo institucional, la FR-1 de ingreso, el oficio de asignación REPSE inicial y los documentos de los módulos activos en el alta.

**Documentos posteriores al alta:**

| Documento | Firma por la Empresa | Estado |
|---|---|---|
| Adenda de confidencialidad | Representante | Decidido (12/11/2026) |
| MOD-1 Convenio modificatorio (módulo 5) | Representante | Decidido (12 y 17/11/2026) |
| Constancia de designación de firmante | Representante | Decidido (12/11/2026) |
| INC-1 Aviso de accidente de trabajo | Representante (o autógrafa) | Decidido (módulo de permisos) |
| LIC-1, LIC-3, INC-2, SUS-1 y SUS-2 | RH designado | Decidido (módulo de permisos) |
| MOD-2 Comunicado de modificación y MOD-4 Oficio de reasignación REPSE (módulo 5) | RH designado | Decidido (12 y 17/11/2026) |
| MOD-5 Constancia de reasignación temporal (módulo 5) | RH designado | Decidido (17/11/2026) |
| FR-1 por emisión o modificación del RIT | RH designado | Decidido (12 y 13/11/2026) |
| Carta responsiva y asignación de correo institucional posteriores (cambio de equipo, de sistemas o de puesto) | RH designado | Decidido (12/11/2026) |
| Nuevas versiones del perfil de puesto | RH designado | Decidido (12/11/2026) |
| Recibo individual de PTU (D-14) | RH designado | Decidido (12/11/2026) |
| Comunicados (por ejemplo, cambio de centro de trabajo) | RH designado | Decidido (12/11/2026) |
| ACT-1 Registro de actualización anual (módulo 5) | Sin firma: registro digital | Decidido (17/11/2026) |

Reglas:
- La empresa puede subir un documento posterior de «RH designado» a «Representante», nunca al revés. Los documentos del alta no se pueden bajar a «RH designado».
- Si no hay firmante de RH vigente, el documento de tipo «RH designado» pasa al representante, con alerta; no se manda a papel.
- Los documentos de firma autógrafa obligatoria (sección 1) quedan fuera de esta tabla.

## 12. Pendientes

- Contrato de encargo con el proveedor de verificación de identidad (confidencialidad, supresión, prohibición de usos propios, ubicación de servidores, convenio con el INE).
- Plazo de conservación de documentos firmados, evidencias, videos y designaciones (tabla de conservación).
- Aplicar al contrato las instrucciones del apartado 9 del corte (encargo 3 del paquete de contratación).
- Aviso de privacidad: finalidad y consentimiento de la verificación con INE y video, y datos de la bitácora de firma (encargos 2 y 6 del paquete de contratación).
