

# Decision Log — EED Procuraduría

Archivo: `.claude/memory/decision_log.md`
Última actualización: 2026-05-11T00:00:00Z
Responsable: Consultora EED + Orquestador
Propósito: Registro trazable, inmutable y consultable de decisiones de diseño, normativa, técnica y ética del proyecto Expediente Electrónico Disciplinario.

---

## Instrucciones de uso

1. Cada decisión se registra como entrada YAML estructurada
2. No editar entradas existentes; solo agregar nuevas al final del archivo
3. Citar norma CGD cuando la decisión tenga fundamento jurídico
4. Estado de validación: validado | observado | bloqueado | pendiente
5. Mantener orden cronológico ascendente por fecha
6. Usar ISO 8601 para timestamps (ej: 2026-05-11T14:30:00Z)

---

## Esquema de entrada

```yaml
- fecha: "YYYY-MM-DDTHH:MM:SSZ"
  categoria: legal | ux | technical | ia_ethics | workflow | security | interoperability
  decision: "Descripción concisa y accionable de la decisión"
  justificacion: "Rationale incluyendo normas, estándares, requisitos de usuario o restricciones técnicas"
  norma_aplicada: "Art. XXX Ley 1952/2019 (CGD) o STI-XXX si aplica"
  validated_by: human | orchestrator
  related_tasks: ["HU-XXX", "screen-YYY", "module-ZZZ"]
  impacto: "Breve descripción del impacto en arquitectura, UX, flujo o cumplimiento"
  alternativas_descartadas: ["Opción A: razón de descarte", "Opción B: razón de descarte"]
  estado: validado | observado | bloqueado | pendiente
```

---

## Registro de decisiones

- fecha: "2026-04-18T00:00:00Z"
  categoria: legal
  decision: "El expediente se crea siempre al radicarse la noticia disciplinaria, independientemente del resultado posterior. Lo que varía es el tipo y estado del expediente (Inhibido, Trasladado, Con actuación). No existen dos entidades raíz separadas."
  justificacion: "Garantizar trazabilidad completa desde el primer contacto con la noticia, coherencia con el principio de unidad del expediente y facilitación de auditoría. Corrige ambigüedad en modelo de datos inicial."
  norma_aplicada: "Art. 69-73 Ley 1952/2019 (CGD) — Radicación y numeración"
  validated_by: human
  related_tasks: ["modelo-datos-v1", "screen-radicacion-v1"]
  impacto: "Unificación del identificador único de expediente desde la radicación; simplificación de consultas y reportes; trazabilidad completa incluso para expedientes inhibidos."
  alternativas_descartadas: ["Crear expediente solo si hay apertura de actuación: pierde trazabilidad de noticias no procedentes", "Dos entidades raíz (Noticia/Expediente): complejidad innecesaria en consultas y auditoría"]
  estado: validado

- fecha: "2026-04-18T00:00:00Z"
  categoria: legal
  decision: "La inhibición (Art. 209 CGD) genera radicado y expediente. No genera investigado vinculado ni actuación disciplinaria. El expediente queda cerrado en estado 'Inhibido'. Contra esta decisión no procede recurso; solo se comunica al quejoso."
  justificacion: "Diferenciar claramente entre decisión inhibitoria y archivo definitivo. La inhibición opera en etapa de evaluación de procedibilidad, antes de vincular investigado. El expediente debe existir para efectos de trazabilidad y estadística."
  norma_aplicada: "Art. 209 Ley 1952/2019 (CGD)"
  validated_by: human
  related_tasks: ["flujo-evaluacion-v1", "screen-inhibitorio-v1"]
  impacto: "El sistema debe permitir cerrar expedientes en estado 'Inhibido' sin activar módulos de términos procesales ni notificación formal al disciplinado. Vista limitada para quejoso."
  alternativas_descartadas: ["No crear expediente para inhibitorios: pierde trazabilidad y capacidad de reporte", "Tratar inhibición como archivo: confunde efectos jurídicos y recursos procedentes"]
  estado: validado

- fecha: "2026-04-18T00:00:00Z"
  categoria: technical
  decision: "La separación funcional instructor/juzgador (Art. 12 CGD mod. Ley 2094/2021) debe reforzarse a nivel de permisos del sistema (RBAC/ABAC), no solo de procedimiento. El sistema bloqueará automáticamente que un usuario actúe como instructor y juzgador en el mismo expediente."
  justificacion: "Garantizar cumplimiento automático del principio de separación de funciones, prevenir errores humanos y facilitar auditoría. Requisito de validez procesal."
  norma_aplicada: "Art. 12 Ley 1952/2019 mod. Ley 2094/2021 (CGD)"
  validated_by: human
  related_tasks: ["rbac-design-v1", "screen-permisos-v1"]
  impacto: "Implementación de control de acceso a nivel de backend y frontend. Registro en audit log de intentos de acceso cruzado. Mensaje explicativo al usuario cuando se bloquee una acción por este motivo."
  alternativas_descartadas: ["Validación solo procedural (manual): riesgo de error humano y nulidad", "Separación por dependencia física: no escalable ni auditable"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: workflow
  decision: "Se incorpora el flujo oficial completo del CGD en el sistema: evaluación de noticia, traslado por competencia, impedimentos, indagación previa, investigación, juicio ordinario/verbal, segunda instancia, doble conformidad, revocatoria directa y mecanismos extraprocesales."
  justificacion: "Alinear el sistema con el procedimiento real de la Procuraduría, garantizando cobertura total del ciclo disciplinario y evitando gaps funcionales que requieran procesos paralelos manuales."
  norma_aplicada: "Ley 1952/2019 y Ley 2094/2021 (CGD completo)"
  validated_by: human
  related_tasks: ["flujo-completo-v1", "matriz-hu-v1"]
  impacto: "Arquitectura modular que permite activar/desactivar módulos según competencia de la dependencia. Timeline procesal dinámico que refleja la etapa actual del expediente."
  alternativas_descartadas: ["Flujo mínimo viable (solo indagación/investigación): deja por fuera actuaciones transversales críticas", "Flujo genérico de proceso administrativo: no cubre particularidades del CGD"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: technical
  decision: "Control automático de reserva de la actuación por etapa procesal (Art. 115 CGD) y módulo de gestión de derechos de petición con alertas de vencimiento."
  justificacion: "Cumplir con el deber legal de reserva sin depender de criterio manual del funcionario, y garantizar respuesta oportuna a derechos de petición so pena de sanción disciplinaria."
  norma_aplicada: "Art. 115 Ley 1952/2019 (CGD) + Ley 1755 de 2015"
  validated_by: human
  related_tasks: ["controls-reserva-v1", "modulo-peticiones-v1"]
  impacto: "Motor de reglas que ajusta visibilidad de datos y acciones según etapa + rol. Alertas automáticas de vencimiento de términos de respuesta a peticiones. Registro de accesos para auditoría."
  alternativas_descartadas: ["Reserva manual por funcionario: riesgo de vulneración y nulidad", "Alertas de peticiones en sistema externo: duplicidad y riesgo de omisión"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: ux
  decision: "Sistema de color completo del Manual de Marca PGN con usos definidos por contexto. Alertas progresivas de términos en 4 niveles: >30 días (verde), 15-30 (amarillo), 5-14 (naranja), <5 o vencido (rojo)."
  justificacion: "Garantizar identidad institucional y facilitar la percepción rápida del estado crítico de los expedientes. El semáforo permite priorización visual sin saturación cognitiva."
  norma_aplicada: "Manual de Marca PGN + Instrucciones de diseño"
  validated_by: human
  related_tasks: ["design-system-v1", "widget-terminos-v1"]
  impacto: "Variables CSS centralizadas para colores. Componente de semáforo reutilizable. Notificaciones push alineadas con niveles de alerta."
  alternativas_descartadas: ["Semáforo de 3 niveles: no distingue entre alerta temprana y crítica", "Colores personalizados fuera de marca: riesgo de rechazo institucional"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: ux
  decision: "Tipografía: Montserrat (títulos, labels, botones) + Poppins (cuerpo, tablas, ayuda). Escala tipográfica completa. CSS de botones (primario, secundario, acento, peligro, deshabilitado). Card de expediente con estados visuales. Widget de términos con barra de progreso."
  justificacion: "Mejorar legibilidad, jerarquía visual y consistencia en interfaces de alta densidad informativa. Los componentes estandarizados aceleran desarrollo y reducen errores de implementación."
  norma_aplicada: "Manual de Marca PGN + WCAG 2.1 AA"
  validated_by: human
  related_tasks: ["design-system-v1", "component-library-v1"]
  impacto: "Biblioteca de componentes reutilizables. Tokens de diseño centralizados. Documentación de patrones para equipo de desarrollo."
  alternativas_descartadas: ["Una sola familia tipográfica: menor jerarquía visual", "Botones genéricos sin estados: confusión en acciones disponibles"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: ux
  decision: "7 principios UX con aplicación concreta: revelación progresiva, estado siempre visible, prevención de errores, consistencia, eficiencia para experto, accesibilidad AA, diseño institucional usable. Estructura de 3 zonas para vista de expediente. Sistema de notificaciones por nivel de criticidad. Dashboard. Responsive. Portal externo ciudadano."
  justificacion: "Balancear rigor jurídico con eficiencia operativa para funcionarios, y claridad para usuarios externos. La accesibilidad es requisito legal, no opcional."
  norma_aplicada: "Manual de Marca PGN + WCAG 2.1 AA + Ley 1712/2014"
  validated_by: human
  related_tasks: ["ux-principles-v1", "portal-ciudadano-v1"]
  impacto: "Guía de diseño con ejemplos aplicados al contexto disciplinario. Plantillas de pantalla que aceleran prototipado. Checklist de accesibilidad por componente."
  alternativas_descartadas: ["Diseño genérico de sistema documental: no cubre particularidades del proceso disciplinario", "Accesibilidad como fase posterior: riesgo de retrabajo y nulidad por barreras"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: technical
  decision: "Se definen 9 roles del sistema con sus acciones específicas y la matriz de permisos completa. Control RBAC automático para separación funcional instructor/juzgador."
  justificacion: "Traducir la estructura organizacional y legal de la Procuraduría a controles de acceso técnicos, garantizando que cada usuario vea y ejecute solo lo permitido por su rol y la etapa procesal."
  norma_aplicada: "Art. 12 Ley 1952/2019 mod. Ley 2094/2021 (CGD)"
  validated_by: human
  related_tasks: ["rbac-design-v1", "matriz-permisos-v1"]
  impacto: "Motor de autorización centralizado. Validación en backend y frontend. Auditoría de intentos de acceso no autorizado."
  alternativas_descartadas: ["Roles genéricos (admin/user): no cubre matices del proceso disciplinario", "Validación solo en frontend: riesgo de elusión y vulnerabilidad"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: technical
  decision: "Stack técnico definido: OAuth 2.0 + JWT, AES-256, TLS 1.3. 7 módulos funcionales del sistema. Plan de implementación en 6 fases (32 semanas)."
  justificacion: "Alinear con estándares de Gobierno Digital (STI) y capacidades del equipo de TI de la entidad. Planificación por fases permite entrega incremental de valor y ajuste basado en feedback."
  norma_aplicada: "Decreto 1081 de 2015 (Gobierno Digital) + STI"
  validated_by: human
  related_tasks: ["arquitectura-v1", "plan-implantacion-v1"]
  impacto: "Documentación técnica para equipo de desarrollo. Criterios de aceptación por fase. Métricas de avance y riesgo."
  alternativas_descartadas: ["Stack no estándar: riesgo de incompatibilidad con sistemas legacy", "Implementación big-bang: alto riesgo de fallo y dificultad de ajuste"]
  estado: validado

- fecha: "2026-04-20T00:00:00Z"
  categoria: legal
  decision: "Se incorpora glosario completo de términos disciplinarios y técnicos del sistema para coherencia en diseño y desarrollo."
  justificacion: "Evitar ambigüedades entre equipos jurídicos, de diseño y técnicos. Unificar lenguaje para documentación, prototipos y código."
  norma_aplicada: "Consolidación del proyecto + CGD"
  validated_by: human
  related_tasks: ["glosario-v1", "documentacion-v1"]
  impacto: "Referencia única para definición de términos. Integración con tooltips y ayuda contextual en la interfaz."
  alternativas_descartadas: ["Glosario externo no vinculado: riesgo de desactualización", "Definiciones implícitas en documentos: ambigüedad y retrabajo"]
  estado: validado

- fecha: "2026-04-29T00:00:00Z"
  categoria: ux
  decision: "Preferencia de diseño: Azul institucional (#063853) como color primario dominante. Amarillo (#FFE601) como acento estratégico (no fondo extenso). Bordes redondeados (12px cards, 8px botones). Iconos Lucide vía CDN. Selectores con búsqueda. Carga masiva con drag & drop. Links contextuales en vez de botones saturados. Microinteracciones tipo SaaS moderno."
  justificacion: "Modernizar la experiencia sin sacrificar identidad institucional. Patrones SaaS mejoran eficiencia de funcionarios expertos. La accesibilidad se mantiene como requisito no negociable."
  norma_aplicada: "Manual de Marca PGN + WCAG 2.1 AA"
  validated_by: human
  related_tasks: ["ux-moderno-v1", "componentes-avanzados-v1"]
  impacto: "Actualización de biblioteca de componentes con patrones modernos. Documentación de microinteracciones. Validación de contraste para nuevos estados."
  alternativas_descartadas: ["Diseño institucional tradicional (sin modernización): menor eficiencia para usuarios expertos", "Adopción plena de patrones SaaS sin adaptación: riesgo de rechazo por identidad institucional"]
  estado: validado

- fecha: "2026-04-29T00:00:00Z"
  categoria: workflow
  decision: "Enfoque de trabajo: una pantalla por respuesta, validación explícita antes de avanzar, coherencia visual entre pantallas, preguntas concretas antes de diseñar."
  justificacion: "Garantizar calidad iterativa, evitar retrabajo por desalineación temprana y mantener trazabilidad de decisiones de diseño. Alineado con metodología ágil y revisión jurídica paso a paso."
  norma_aplicada: "Instrucciones de comportamiento para el asistente + Buenas prácticas ágiles"
  validated_by: human
  related_tasks: ["metodologia-v1", "validacion-iterativa-v1"]
  impacto: "Protocolo de entrega por pantalla con checkpoint de validación. Registro de feedback por iteración. Ajuste de prioridades basado en validación temprana."
  alternativas_descartadas: ["Diseño de múltiples pantallas por respuesta: mayor riesgo de desalineación y retrabajo", "Validación al final del flujo: dificultad para ajustar decisiones tempranas"]
  estado: validado

- fecha: "2026-05-11T00:00:00Z"
  categoria: ia_ethics
  decision: "procuradurIA debe registrar cada sugerencia en audit log con usuario, timestamp, contexto y acción. La IA nunca decide, solo asiste. El usuario debe activar explícitamente el módulo y aceptar términos de uso."
  justificacion: "Garantizar trazabilidad, transparencia y control humano sobre decisiones procesales. Cumplir con principios éticos de IA en administración pública y prevenir responsabilidad por actos automatizados."
  norma_aplicada: "Principios de IA responsable + Art. 115 CGD (reserva) + Ley 1581/2012 (datos)"
  validated_by: human
  related_tasks: ["ia-ethics-v1", "consentimiento-ia-v1"]
  impacto: "Implementación de middleware de registro para interacciones con IA. Flujo de consentimiento previo a activación. Mensajes de advertencia en UI sobre límite no-decisivo de la IA."
  alternativas_descartadas: ["Registro opcional de sugerencias: pierde trazabilidad para auditoría", "Activación automática de IA: vulnera principio de consentimiento y control humano"]
  estado: validado

---

## Espacio para nuevas decisiones

(Agregar nuevas entradas aquí siguiendo el esquema definido. Mantener orden cronológico.)

```yaml
- fecha: "YYYY-MM-DDTHH:MM:SSZ"
  categoria: legal | ux | technical | ia_ethics | workflow | security | interoperability
  decision: ""
  justificacion: ""
  norma_aplicada: ""
  validated_by: human | orchestrator
  related_tasks: []
  impacto: ""
  alternativas_descartadas: []
  estado: validado | observado | bloqueado | pendiente
```

---

## Índice rápido por categoría

### legal
- Creación de expediente desde radicación de noticia
- Inhibición genera expediente cerrado sin investigación
- Separación funcional instructor/juzgador en permisos
- Reserva por etapa procesal (Art. 115 CGD)
- procuradurIA: trazabilidad y límite no-decisivo

### ux
- Paleta PGN con usos definidos
- Semáforo de términos en 4 niveles
- Tipografía Montserrat + Poppins con escala
- Componentes: card de expediente, widget de términos
- Principios UX aplicados al contexto disciplinario
- Diseño moderno SaaS con identidad institucional

### technical
- RBAC/ABAC con separación funcional automática
- Stack: OAuth 2.0+JWT, AES-256, TLS 1.3
- 7 módulos funcionales del sistema
- Integración con DOKUS, firma digital, SIRI/SCC
- Control de reserva dinámica por etapa + rol

### ia_ethics
- procuradurIA: consentimiento explícito, trazabilidad obligatoria, cero capacidad decisoria
- Anonimización o entorno seguro para procesamiento de datos sensibles
- Registro de auditoría para cada interacción con IA

### workflow
- Flujo CGD completo incorporado
- Metodología: una pantalla por respuesta, validación explícita
- Glosario unificado para coherencia entre equipos

---

## Notas de mantenimiento

1. Este archivo se actualiza automáticamente por el Orquestador EED cuando se valida una nueva decisión.
2. Para consultas, usar búsqueda por categoría, norma_aplicada o related_tasks.
3. No eliminar entradas; si una decisión se revoca, agregar nueva entrada con estado "bloqueado" y referencia a la entrada original en justificacion.
4. Exportar periódicamente a formato JSON para integración con herramientas de auditoría externa si se requiere.

---

Fin del archivo decision_log.md. Listo para guardar en `.claude/memory/decision_log.md`.