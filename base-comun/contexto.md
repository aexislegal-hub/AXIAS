# Contexto del sistema Axia

Desarrollo documentos maestros para AXIARH, un software de cumplimiento laboral de la familia Axia que genera documentos de forma automatizada. Los documentos son modelos genéricos con variables y módulos condicionales que el sistema llena con los datos de cada empresa y de cada persona trabajadora; si aparece un dato residual de una empresa real, es un error, no un cliente.

Los documentos tienen tres lectores: Recursos Humanos del cliente, que llena el formulario y no debe tomar decisiones jurídicas; consultoría, que configura la empresa y el organigrama; y el ingeniero que programa el sistema, que necesita variables y reglas sin ambigüedad.

Los datos vienen de tres niveles y cada uno se captura una sola vez: (1) configuración de la empresa; (2) organigrama, con los atributos de cada puesto y su perfil; (3) alta de la persona trabajadora, solo con sus datos personales, el puesto, el centro de trabajo, la fecha de inicio y las modalidades. Las condiciones de trabajo vienen preestablecidas por la empresa y el puesto; a RH no se le pregunta nada que pueda definirse en los niveles 1 o 2.

## Familia Axia

- **Axia RH:** cumplimiento laboral (contratación, RIT, PTU, terminación, modificaciones, permisos y licencias, vacaciones y aguinaldo, capacitación en lo que toca a SIRCE y la comisión mixta, Fonacot y análisis de jornada).
- **Axia NOMs:** normas oficiales mexicanas de seguridad y salud en el trabajo (NOM-035, NOM-019, NOM-030 y demás). Usa los niveles 1 a 3 de Axia RH.
- **Axia CYA:** capacitación y adiestramiento (DNC, planes y programas, cursos y DC-3). Axia RH conserva la Comisión Mixta, el SIRCE y el DC-1.
- **Axia Compliance:** anticorrupción, ética, Comité de Integridad y Disciplina, políticas legales (trabajo híbrido y teletrabajo, prevención de la violencia y el acoso) y políticas organizacionales a las que remite el RIT.
- **Axia Corporativa:** línea posterior.

## Especificaciones transversales

La especificación de firma electrónica («AXIARH - Firma electrónica - Especificación para programación», v1.2; decisiones en el registro de Axia RH, 4.11) rige la firma de todos los documentos de la familia. Hoy vive en el proyecto de Axia RH.
