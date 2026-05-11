# HU-10 — Módulo Compulsa de Copias (EED)

## MATRIZ MAESTRA DE HISTORIAS
- HU-10-01: Proyectar auto de compulsa transversal.
- HU-10-02: Seleccionar y validar piezas/folios a compulsar.
- HU-10-03: Seleccionar autoridad destinataria externa (patrón traslado).
- HU-10-04: Seleccionar dependencia destinataria interna PGN.
- HU-10-05: Gestionar remisión múltiple en un mismo auto.
- HU-10-06: Flujo Instructor → Revisor → Aprobador → Jefe.
- HU-10-07: Firma electrónica y generación automática de oficio(s).
- HU-10-08: Registro de auditoría, reserva y continuidad del proceso principal.

---

TASK CONTEXT
- Objective: Definir requisitos funcionales completos para la pantalla de Compulsa de Copias.
- CGD Stage: Actuación transversal (aplicable a inhibitorio, indagación, investigación, archivo y pliegos).
- Target Role: instructor (primario), revisor, aprobador y jefe de dependencia (secundarios).
- Linked Prototype: `Pantallas VEED/10_compulsa.html` y patrón de autoridad de `Pantallas VEED/09_traslado_competencia.html`.

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-01 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: instructor
- Que: proyectar auto de compulsa de copias desde cualquier estado procesal habilitado
- Para que: remitir hallazgos o piezas a autoridad competente sin suspender el trámite disciplinario principal

### DEPENDENCIAS Y PRECONDICIONES
1. Expediente activo con número IUS/IUC y metadatos completos.
2. Permiso RBAC del rol instructor sobre acción "Proyectar auto".
3. Trazabilidad habilitada para evento de creación (bitácora auditable).

### RESTRICCIONES
1. La compulsa es acto de trámite y no debe alterar etapa procesal principal.
2. Debe conservar separación funcional entre instructor y roles aprobadores.
3. Toda creación debe dejar huella de auditoría (usuario, fecha, IP/sesión).

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Creación de borrador de auto**
- Dado que: el instructor está dentro de un expediente habilitado
- Cuando: selecciona la acción "Compulsa de copias"
- Entonces: el sistema crea borrador con radicado interno, plantilla oficial y metadatos del expediente

**Escenario 2: Persistencia de borrador**
- Dado que: existe un borrador de compulsa
- Cuando: el instructor guarda y reingresa
- Entonces: el sistema restaura contenido, secciones y estado exacto del borrador

**Escenario 3: No alteración del proceso principal**
- Dado que: se crea el auto de compulsa
- Cuando: se consulta línea de tiempo del expediente
- Entonces: la etapa principal permanece inalterada y se registra evento independiente de compulsa

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html`

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-02 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: instructor
- Que: seleccionar piezas procesales y validar folios obligatorios
- Para que: asegurar integridad documental de la remisión

### DEPENDENCIAS Y PRECONDICIONES
1. Índice documental del expediente cargado y accesible.
2. Piezas con numeración/folio o metadatos de rango.
3. Regla de negocio de preselección por defecto activada.

### RESTRICCIONES
1. La selección inicial debe marcar todas las piezas disponibles (configurable).
2. No se puede enviar a aprobación si hay piezas sin folio/rango válido.
3. Toda modificación de selección debe quedar auditada.

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Preselección por defecto**
- Dado que: el instructor abre "Documentos a compulsar"
- Cuando: el bloque termina de cargar
- Entonces: todas las piezas aparecen seleccionadas y el contador refleja total real

**Escenario 2: Recalcular resumen documental**
- Dado que: el instructor marca/desmarca piezas
- Cuando: cambia cualquier selección
- Entonces: el sistema actualiza cantidad de piezas, total de folios y estado visual de selección

**Escenario 3: Bloqueo por folios inválidos**
- Dado que: una pieza carece de folio/rango
- Cuando: el usuario intenta enviar a revisión
- Entonces: el sistema bloquea la transición y muestra mensaje de validación obligatoria

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html` (bloque documentos a compulsar)

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-03 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: instructor
- Que: seleccionar autoridad externa con patrón de traslado por competencia
- Para que: dirigir la compulsa a autoridad disciplinaria externa jurídicamente competente

### DEPENDENCIAS Y PRECONDICIONES
1. Componente de destinatario externo con subtipos: autoridades, personerías, OCDI.
2. Catálogo de autoridades con ámbito y base normativa.
3. Campos de dependencia receptora y dirección/correo habilitados.

### RESTRICCIONES
1. Debe permitir selección múltiple de destinatarios externos.
2. Debe mantener trazabilidad de subtipo elegido y motivo normativo.
3. No habilitar firma si no existe al menos un destinatario válido.

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Navegación por subtipos externos**
- Dado que: el instructor está en "Autoridad externa"
- Cuando: alterna entre Autoridades/Personerías/OCDI
- Entonces: el sistema muestra subpanel correspondiente y conserva datos previamente diligenciados

**Escenario 2: Selección múltiple en tabla de autoridades**
- Dado que: el instructor consulta el catálogo
- Cuando: marca varias filas de autoridad
- Entonces: el sistema incrementa contador de destinatarios y registra cada selección

**Escenario 3: Captura de contacto para remisión**
- Dado que: existe al menos una autoridad seleccionada
- Cuando: el instructor diligencia dependencia y dirección/correo
- Entonces: los datos quedan asociados al destinatario para generación automática de oficio

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html`
- `Pantallas VEED/09_traslado_competencia.html`

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-04 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: instructor
- Que: seleccionar dependencia interna PGN como destinataria
- Para que: compulsar internamente cuando la competencia está en otra dependencia

### DEPENDENCIAS Y PRECONDICIONES
1. Catálogo interno PGN por tipo, ciudad y dependencia.
2. Permiso funcional para remisión interdependencias.
3. Reglas de reserva activas por perfil y despacho.

### RESTRICCIONES
1. Debe separar claramente destinatario interno vs externo.
2. No se permite destinatario interno incompleto (tipo/ciudad/dependencia vacíos).
3. Debe registrar traza de origen y destino institucional.

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Diligenciamiento de destinatario interno**
- Dado que: el instructor selecciona "Otra dependencia PGN"
- Cuando: completa tipo, ciudad y dependencia
- Entonces: el sistema valida y agrega destinatario interno a la compulsa

**Escenario 2: Coexistencia interno + externo**
- Dado que: el caso exige múltiple remisión
- Cuando: el instructor agrega destinatarios de ambos tipos
- Entonces: el sistema permite coexistencia en el mismo auto sin pérdida de datos

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html` (panel interna PGN)

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-05 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: instructor
- Que: gestionar lista de múltiples destinatarios en una sola decisión
- Para que: evitar duplicar autos y mantener coherencia de actuación

### DEPENDENCIAS Y PRECONDICIONES
1. Modelo de datos que soporte destinatarios N por auto.
2. Resumen visible de cantidad de destinatarios seleccionados.
3. Eventos de agregar/quitar/editar destinatario auditables.

### RESTRICCIONES
1. Cada destinatario debe tener canal y contacto de envío.
2. Eliminar destinatario debe requerir confirmación explícita.
3. El resumen de destinatarios debe sincronizarse en tiempo real.

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Contador dinámico de destinatarios**
- Dado que: existen destinatarios seleccionados
- Cuando: el instructor agrega o quita uno
- Entonces: el contador se actualiza inmediatamente con el valor correcto

**Escenario 2: Persistencia de lista múltiple**
- Dado que: el auto tiene varios destinatarios
- Cuando: se guarda borrador y se reabre
- Entonces: se conserva listado completo y metadatos por destinatario

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html` (indicador de destinatarios)

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-06 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: revisor y aprobador
- Que: validar legal/técnicamente la compulsa antes de firma
- Para que: prevenir errores de remisión y reprocesos

### DEPENDENCIAS Y PRECONDICIONES
1. Auto en estado "En revisión" o "En aprobación".
2. Checklist mínimo de completitud (destinatarios, folios, resuelve, soporte).
3. Canal de devolución con observaciones obligatorias.

### RESTRICCIONES
1. Revisor/aprobador no pueden suplantar rol instructor en autoría original.
2. Toda devolución exige motivo y registro de observación.
3. No se habilita pase a jefe con validaciones pendientes.

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Devolución con observaciones**
- Dado que: el revisor detecta inconsistencia
- Cuando: selecciona "Devolver"
- Entonces: el sistema exige observación obligatoria y retorna al instructor

**Escenario 2: Aprobación condicionada a completitud**
- Dado que: el aprobador revisa el auto
- Cuando: todos los requisitos están completos
- Entonces: el estado cambia a "Listo para firma" y se registra decisión

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html` (flujo de rol y panel de acciones)

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-07 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: jefe de dependencia
- Que: firmar electrónicamente auto de compulsa y disparar oficios automáticos
- Para que: formalizar la remisión con validez institucional

### DEPENDENCIAS Y PRECONDICIONES
1. Auto en estado "Listo para firma".
2. Integración con firma electrónica institucional.
3. Plantilla de oficio y motor de generación por destinatario.

### RESTRICCIONES
1. Tras firma, el auto queda inmutable (versión final).
2. Debe generar un oficio por cada destinatario registrado.
3. Debe capturar evidencia de firma y hash documental.

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Firma exitosa**
- Dado que: el jefe abre un auto listo para firma
- Cuando: confirma firma electrónica
- Entonces: el sistema aplica firma, cierra edición y cambia estado a "Firmado"

**Escenario 2: Generación automática de oficios**
- Dado que: el auto firmado tiene N destinatarios
- Cuando: finaliza la firma
- Entonces: el sistema genera N oficios con trazabilidad individual de remisión

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html` (acción firmar)

---

## HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU: HU-10-08 | Fecha: 11-05-2026 | Creado por: Consultora EED**

### DESCRIPCION
- Quien: analista y superior_jerarquico
- Que: auditar la actuación de compulsa y verificar continuidad del proceso principal
- Para que: garantizar trazabilidad, reserva y control posterior

### DEPENDENCIAS Y PRECONDICIONES
1. Bitácora de auditoría activa en cada transición de estado.
2. Registro de destinatarios, piezas remitidas y oficio(s) generados.
3. Políticas de visibilidad por reserva y rol.

### RESTRICCIONES
1. Acceso a datos sensibles limitado por perfil y necesidad funcional.
2. Toda consulta de trazabilidad debe registrarse.
3. Compulsa no puede suspender automáticamente términos del proceso principal.

### CRITERIOS DE ACEPTACION (GHERKIN)
**Escenario 1: Consulta integral de trazabilidad**
- Dado que: existe una compulsa emitida
- Cuando: un analista autorizado consulta auditoría
- Entonces: visualiza línea de tiempo completa (creación, revisiones, firma, oficios y envíos)

**Escenario 2: Control de continuidad procesal**
- Dado que: la compulsa fue remitida
- Cuando: se revisa estado del expediente principal
- Entonces: se evidencia continuidad en su etapa vigente sin alteración automática por la compulsa

### PROTOTIPO / ANEXOS
- `Pantallas VEED/10_compulsa.html`

---

## NORMATIVE AND TECHNICAL ALIGNMENT
- CGD articles cited: Deben validarse y anexarse por Jurídica PGN en versión DOCX final (matriz normativa por HU).
- Reservation controls: Aplican controles de visibilidad y trazabilidad por rol para actuaciones con reserva.
- procuradurIA boundaries: Cualquier sugerencia automatizada requiere validación humana expresa y registro en auditoría.
- Term calculation rules: Si se incorporan términos, usar lógica de días hábiles con calendario oficial.
- Interoperability requirements: Preparado para integración con firma electrónica y remisión interoperable.

## VALIDATION NOTES
- Format compliance: Confirmado contra plantilla HU Architect (estructura PGN completa por HU).
- Gherkin testability: Confirmado (escenarios verificables por estado/acción/resultado).
- Legal traceability: Requiere cierre de citas normativas específicas por mesa jurídica.
- Next review focus: matriz de artículos CGD por escenario y reglas de reserva por perfil.
