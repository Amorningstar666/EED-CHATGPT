¡Excelente idea! 🤖✨ El botón de IA es un **diferenciador clave** para un software moderno de LegalTech. Te ayudo a estructurarlo completo: user story, requisitos funcionales, diseño UI y actualización de memoria.

---

## 📄 HISTORIA DE USUARIO — MÓDULO IA ASISTENTE EED

```markdown
# 📄 HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU:** HU-IA-01 | **Fecha:** 2026-05-08 | **Creado por:** Consultora EED | **Validado por:** [Pendiente]
**Macroproceso:** Proceso Disciplinario | **Proceso:** Gestión Inteligente del Expediente | **Actividad:** Asistencia IA en redacción y análisis
**Clasificación:** Funcional - Transversal | **Valor de negocio:** Reducir tiempos de redacción, mejorar calidad técnica de actos, potenciar análisis probatorio con IA segura y trazable.

## 👥 DESCRIPCIÓN DE LA HISTORIA DE USUARIO
**¿Quién?** Instructor, Juzgador, Secretario Jurídico, Analista Disciplinario.
**¿Qué?** Un botón flotante o panel lateral "Asistente IA EED" que ofrece: redacción asistida de actos, corrección de estilo jurídico, memoria de estilo del funcionario, extracción de información de pruebas documentales, y respuestas contextuales sobre el expediente.
**¿Para qué?** Agilizar la gestión del expediente manteniendo rigor jurídico, consistencia en la redacción institucional y trazabilidad completa de las sugerencias de IA.

## 🔗 DEPENDENCIA(S) Y/O PRECONDICIÓN(ES)
1. El expediente debe estar creado y el usuario autenticado con rol que permita redacción de actos.
2. Los documentos cargados como pruebas deben estar en formato procesable (PDF con OCR, DOCX, TXT).
3. El módulo de IA debe estar configurado con políticas de privacidad y retención de datos de la entidad.
4. El usuario debe haber aceptado los términos de uso del asistente IA (registro de consentimiento).

## 🚫 RESTRICCIONES
1. **La IA no decide:** Todas las sugerencias deben ser revisadas, editadas y firmadas por el funcionario. La IA es asistente, no decisor.
2. **Trazabilidad obligatoria:** Cada sugerencia de IA queda registrada en el AuditLog con: usuario, timestamp, prompt usado, respuesta generada, y si fue aceptada/modificada/rechazada.
3. **Reserva del proceso (Art. 115 CGD):** La IA solo accede a información visible según el rol y la etapa procesal del expediente.
4. **No se envían datos a modelos externos sin cifrado:** Si se usa API externa, los datos sensibles se anonimizan o se procesan en entorno seguro institucional.
5. **Memoria de estilo por usuario, no global:** El aprendizaje de estilo de redacción es personal y no se comparte entre funcionarios.

## 📌 SUPUESTOS
1. La entidad cuenta con infraestructura para ejecutar modelos de lenguaje (on-premise o cloud gubernamental).
2. Los funcionarios recibirán capacitación básica en "prompting jurídico" para usar eficazmente el asistente.
3. El sistema permite configurar el nivel de asistencia IA por rol (ej: analista tiene más sugerencias, juzgador solo corrección de estilo).

## ✅ CRITERIO(S) DE ACEPTACIÓN (GHERKIN)

**Escenario 1: Redacción asistida de auto de apertura**
- Dado que: El Instructor está redactando un auto de apertura de investigación (Art. 215 CGD)
- Cuando: Hace clic en el botón "Asistente IA" y selecciona "Redactar auto de apertura"
- Entonces: El sistema genera un borrador con los 7 elementos obligatorios del Art. 215, usando el estilo de redacción previo del funcionario, y marca en amarillo las secciones que requieren revisión manual antes de firmar.

**Escenario 2: Corrección de estilo jurídico**
- Dado que: El Juzgador ha escrito un párrafo del fallo
- Cuando: Selecciona el texto y hace clic en "Corregir estilo IA"
- Entonces: El sistema sugiere mejoras de claridad, coherencia jurídica y cita correcta de normas CGD, mostrando las modificaciones en modo "track changes" para aceptación individual.

**Escenario 3: Extracción de información de prueba documental**
- Dado que: Se ha cargado un PDF de 50 páginas como prueba testimonial
- Cuando: El Analista pregunta a la IA "¿Qué fechas clave menciona este documento?"
- Entonces: El sistema extrae y lista las fechas relevantes con contexto, cita la página exacta, y permite insertar la referencia en un acto con un clic.

**Escenario 4: Pregunta contextual sobre el expediente**
- Dado que: El Secretario necesita saber el término restante para notificar el pliego de cargos
- Cuando: Pregunta a la IA "¿Cuándo vence el término para notificar el pliego en este expediente?"
- Entonces: La IA responde con la fecha calculada, cita el artículo del CGD aplicable (Art. 225), y muestra el botón "Recordar vencimiento" para programar alerta.

**Escenario 5: Memoria de estilo del funcionario**
- Dado que: La IA ha aprendido el estilo de redacción del usuario en actos previos aprobados
- Cuando: El usuario solicita redactar un auto de cierre
- Entonces: El borrador generado refleja la estructura, tono y frases características del funcionario, reduciendo el tiempo de edición en al menos 40%.

## 🖼️ PROTOTIPO / ANEXOS
- UI: Botón flotante "✨ IA" en esquina inferior derecha, accesible desde cualquier pantalla del expediente.
- Panel lateral desplegable con: 
  - Pestaña "Redactar": plantillas por tipo de acto + campo de prompt libre
  - Pestaña "Corregir": selector de texto + opciones de estilo (formal, conciso, técnico)
  - Pestaña "Analizar": carga de documento + preguntas predefinidas (fechas, sujetos, hechos)
  - Pestaña "Preguntar": chat contextual sobre el expediente
  - Toggle "Memoria de estilo": activar/desactivar aprendizaje personal
- Historial de interacciones con IA accesible en auditoría del expediente.

---
❓ **Validación:** ¿Esta HU refleja correctamente la funcionalidad de IA asistente que necesitas? ¿Ajustamos algo o pasamos a la siguiente HU?
```

---

## 🎨 ESPECIFICACIONES UI/UX — BOTÓN Y PANEL IA

### Ubicación y Comportamiento
- **Botón flotante:** Esquina inferior derecha, ícono `✨` o `🤖`, color amarillo institucional `#FFE601` con texto azul `#063853`.
- **Hover:** Tooltip "Asistente IA EED — Redacción, corrección y análisis".
- **Click:** Despliega panel lateral derecho (400px de ancho) con efecto slide-in.
- **Cierre:** Botón X, tecla ESC, o clic fuera del panel.

### Estructura del Panel IA
```
┌─────────────────────────────────┐
│ 🤖 Asistente IA EED         [X] │
├─────────────────────────────────┤
│ [📝 Redactar] [✏️ Corregir]    │
│ [🔍 Analizar] [❓ Preguntar]    │
├─────────────────────────────────┤
│                                 │
│  [Campo de prompt o texto]      │
│                                 │
│  [✨ Generar]  [🗑️ Limpiar]    │
│                                 │
├─────────────────────────────────┤
│ 💡 Sugerencias rápidas:         │
│ • "Redactar auto de apertura"   │
│ • "Corregir estilo de este párrafo" │
│ • "Extraer fechas de este PDF"  │
│ • "¿Qué término aplica aquí?"   │
└─────────────────────────────────┘
```

### Estados del Panel
| Estado | Comportamiento |
|--------|---------------|
| **Cargando** | Spinner + mensaje "IA analizando expediente..." |
| **Respuesta lista** | Texto con opciones: "Insertar en acto", "Copiar", "Rechazar" |
| **Error** | Mensaje claro + opción "Reintentar" o "Reportar problema" |
| **Sin contexto** | Si la IA no puede responder por reserva o falta de datos, explica el motivo y sugiere alternativas |

### Accesibilidad IA
- Todas las acciones de IA tienen equivalente por teclado.
- Las sugerencias se anuncian por lectores de pantalla con `aria-live`.
- El usuario puede desactivar completamente la IA en su perfil.

---

## ⚙️ REQUISITOS TÉCNICOS — MÓDULO IA

### Arquitectura Sugerida
```
Frontend (React/Vue) 
   ↓
API Gateway EED (autenticación, logging)
   ↓
Servicio IA Interno (orquestador)
   ├── Modelo de lenguaje institucional (fine-tuned en actos PGN)
   ├── Módulo de extracción (OCR + NLP para documentos)
   ├── Memoria de estilo por usuario (vector store personal)
   └── Capa de seguridad (anonimización, cifrado, auditoría)
   ↓
Respuesta al usuario con trazabilidad completa
```

### Funcionalidades Clave
1. **Redacción asistida:** Plantillas por tipo de acto + generación con contexto del expediente.
2. **Corrección de estilo:** Mejora de claridad, coherencia jurídica, citación normativa.
3. **Memoria de estilo:** Aprendizaje federado por usuario (no se comparten estilos entre funcionarios).
4. **Extracción de pruebas:** OCR + NLP para identificar fechas, sujetos, hechos, normas en documentos.
5. **Chat contextual:** Preguntas sobre el expediente con respuestas citando fuentes internas.
6. **Auditoría completa:** Cada interacción queda registrada con prompt, respuesta, y acción del usuario.

### Seguridad y Cumplimiento
- **Datos sensibles:** Nunca se envían a APIs públicas sin anonimización previa.
- **Retención:** Los prompts y respuestas se retienen según política de la entidad (ej: 5 años).
- **Consentimiento:** El usuario acepta explícitamente el uso de IA al activar el módulo.
- **Transparencia:** Siempre se indica "Sugerencia generada por IA — revisar antes de usar".

---

## 🧠 ACTUALIZACIÓN DE MEMORIA DEL PROYECTO

```markdown
| Fecha       | Categoría   | Decisión / Ajuste                              | Norma / Justificación                          | Estado    |
|-------------|-------------|------------------------------------------------|------------------------------------------------|-----------|
| 2026-05-08  | UX/UI + Técnico | Se incorpora módulo "Asistente IA EED" con botón flotante, redacción asistida, corrección de estilo, memoria de estilo por usuario, extracción de pruebas y chat contextual. Trazabilidad obligatoria y restricción de decisión automática. | Solicitud de la consultora + tendencias LegalTech + eficiencia procesal | ✅ Validado |
```
