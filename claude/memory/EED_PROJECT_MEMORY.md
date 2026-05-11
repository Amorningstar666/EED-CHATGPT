# 🧠 EED_PROJECT_MEMORY.md
## Registro de Decisiones y Ajustes — Expediente Electrónico Disciplinario
**Entidad:** Procuraduría General de la Nación — Oficina de Control Interno Disciplinario (Veeduría)  
**Última actualización:** 2026-04-29  
**Responsable de actualización:** Consultora de diseño + Asistente IA

---

## 📋 Instrucciones de Uso

1. **Actualización automática:** Cada vez que se valide un ajuste, corrección o nueva decisión de diseño/flujo/técnica, agregar una nueva fila a la tabla.
2. **Categorías disponibles:** `Flujo`, `UX/UI`, `Técnico`, `Jurídico`, `Roles`, `Seguridad`, `Interoperabilidad`, `Accesibilidad`.
3. **Estados:** 
   - ✅ Validado: Aprobado por la consultora o entidad
   - ⏳ Pendiente: Por revisar o validar
   - 🔄 En ajuste: Modificado tras feedback
   - ❌ Descartado: No se implementará
4. **Citar siempre la norma** cuando la decisión tenga fundamento en el CGD o marco jurídico.

---
Excelente. He analizado la estructura de tus archivos. Tienes una base muy sólida en los **Módulos 1 y 2** (Radicación hasta Apertura de Investigación).

Aquí tienes el bloque actualizado para tu archivo `EED_PROJECT_MEMORY.md`. Esto le dice al sistema exactamente qué prototipos existen y cuáles son la "fuente de verdad" para no rediseñarlos desde cero.

Copia y pega esto en tu archivo de memoria:

---

### 📦 2. INVENTARIO DE ENTREGABLES Y PROTOTIPOS (Estado Actual)

#### Prototipos HTML Validados (Carpeta `prototypes/`)
| ID | Archivo | Módulo | Estado | Notas |
|----|---------|--------|--------|-------|
| 01 | `01_login.html` | Acceso | ✅ Base | Autenticación institucional |
| 02 | `02_shell_navegacion.html` | Estructura | ✅ Base | Navbar, Sidebar, Estructura global |
| 03 | `03_radicacion.html` | Radicación | ✅ Validado | Formulario de queja |
| 04 | `04_reparto_asignacion.html` | Reparto | ✅ Validado | Asignación a despacho |
| 05 | `05_evaluacion_noticia_V2.html` | Evaluación | ✅ **Final** | Usar V2 como referencia. V1 descartada. |
| 06 | `06_decision_inhibitoria.html` | Decisión | ✅ Validado | Actuación inhibitoria (Art. 209) |
| 07 | `07_auto_indagacion_previa.html` | Indagación | ✅ Validado | Auto de apertura de indagación |
| 08 | `08_auto_apertura_investigacion.html` | Investigación | ✅ **Final** | Usar versión sin "copia". Referente visual principal. |
| 09 | `09_traslado_competencia.html` | Traslado | ✅ Validado | Actuación por competencia |

#### Historias de Usuario (Carpeta `user_stories/`)
| Carpeta | Contenido | Estado |
|---------|-----------|--------|
| `HU-01_Login_EED` | Acceso y roles | ✅ Archivada |
| `HU-02-Shell` | Desglose por 6 roles (Secretaría, Instrucción, etc.) | ✅ Archivada |
| `HU-03-Radicacion` | Radicación de noticia | ✅ Archivada |
| `HU-04-REPARTO` | Reparto y asignación | ✅ Archivada |
| `HU-05-Evaluacion` | Evaluación preliminar | ✅ Archivada |
| `HU-06-Inhibitoria` | Decisión inhibitoria | ✅ Archivada |
| `HU-07-INDAGACION` | Indagación previa | ✅ Archivada |

---

### 🚀 PLAN DE CONTINUIDAD

**Próximo Entregable Sugerido:**
Dado que ya tienes la **Apertura de Investigación (Pantalla 08)**, el siguiente paso lógico en el flujo del Instructor es la **Gestión de la Investigación Activa**.

**Pantalla 10: Dashboard de Gestión de Investigación (Instructor)**
- **Objetivo:** Permitir al instructor ver el tiempo restante (semáforo), decretar/practicar pruebas y ver el estado del disciplinado.
- **Componentes a reutilizar:**
  - `Widget de términos` (del Pantalla 08).
  - `Shell de navegación` (Pantalla 02).
  - `Botón flotante procuradurIA`.
- **Normativa:** Art. 211-216 CGD (Términos, Pruebas, Medidas Preventivas).

**¿Quieres que proceda con el diseño de la Pantalla 10 o prefieres ajustar alguno de los prototipos existentes (01-09) antes de avanzar?**

## 📜 Registro de Decisiones Validadas

| Fecha       | Categoría   | Decisión / Ajuste                                                                                                                                 | Norma / Justificación                                                                 | Estado    |
|-------------|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|-----------|
| 2026-04-18  | Modelo de datos | El expediente se crea SIEMPRE al radicarse la noticia disciplinaria. Lo que varía es el tipo/estado (Inhibido, Trasladado, Con actuación). No hay dos entidades raíz. | Corrección validada por consultora — coherencia con Art. 69-73 CGD                   | ✅ Validado |
| 2026-04-18  | Jurídico/Flujo | La inhibición (Art. 209 CGD) genera radicado y expediente. No genera investigado vinculado ni actuación disciplinaria. El expediente queda cerrado en estado "Inhibido". Contra esta decisión no procede recurso. | Art. 209 Ley 1952 de 2019                                                             | ✅ Validado |
| 2026-04-18  | Técnico/Jurídico | La separación funcional instructor/juzgador (Art. 12 CGD mod. Ley 2094/2021) debe reforzarse a nivel de permisos del sistema (RBAC), no solo de procedimiento. | Art. 12 CGD mod. Ley 2094 de 2021                                                    | ✅ Validado |
| 2026-04-20  | Flujo       | Se incorpora el flujo oficial completo del CGD: evaluación de noticia, traslado por competencia, impedimentos, indagación previa, investigación, juicio ordinario/verbal, segunda instancia, doble conformidad, revocatoria directa. | Flujo oficial PGN — Ley 1952/2019 y Ley 2094/2021                                    | ✅ Validado |
| 2026-04-20  | Técnico     | Control automático de reserva de la actuación por etapa procesal (Art. 115 CGD) y módulo de gestión de derechos de petición con alertas de vencimiento. | Art. 115 CGD + Ley 1755 de 2015                                                      | ✅ Validado |
| 2026-04-20  | UX/UI       | Sistema de color completo del Manual de Marca PGN con usos definidos por contexto. Alertas progresivas de términos en 4 niveles: >30 días (verde), 15-30 (amarillo), 5-14 (naranja), <5 o vencido (rojo). | Manual de Marca PGN + Instrucciones de diseño                                        | ✅ Validado |
| 2026-04-20  | UX/UI       | Tipografía: Montserrat (títulos, labels, botones) + Poppins (cuerpo, tablas, ayuda). Escala tipográfica completa. CSS de botones (primario, secundario, acento, peligro, deshabilitado). Card de expediente con estados visuales. Widget de términos con barra de progreso. | Manual de Marca PGN + buenas prácticas UX                                            | ✅ Validado |
| 2026-04-20  | UX/UI       | 7 principios UX con aplicación concreta: revelación progresiva, estado siempre visible, prevención de errores, consistencia, eficiencia para experto, accesibilidad AA, diseño institucional usable. Estructura de 3 zonas para vista de expediente. Sistema de notificaciones por nivel de criticidad. Dashboard. Responsive. Portal externo ciudadano. | Manual de Marca PGN + WCAG 2.1 AA + Instrucciones.md                                 | ✅ Validado |
| 2026-04-20  | Técnico/Roles | Se definen 9 roles del sistema con sus acciones específicas y la matriz de permisos completa. Control RBAC automático para separación funcional instructor/juzgador. | Art. 12 CGD mod. Ley 2094/2021 + Instrucciones.md                                    | ✅ Validado |
| 2026-04-20  | Técnico     | Stack técnico definido: OAuth 2.0 + JWT, AES-256, TLS 1.3. 7 módulos funcionales del sistema. Plan de implementación en 6 fases (32 semanas). | Instrucciones.md — Oficina Control Interno Disciplinario                             | ✅ Validado |
| 2026-04-20  | Jurídico    | Se incorpora glosario completo de términos disciplinarios y técnicos del sistema para coherencia en diseño y desarrollo. | Consolidación del proyecto                                                           | ✅ Validado |
| 2026-04-29  | UX/UI       | Preferencia de diseño: Azul institucional (#063853) como color primario dominante. Amarillo (#FFE601) como acento estratégico (no fondo extenso). Bordes redondeados (12px cards, 8px botones). Iconos Lucide vía CDN. Selectores con búsqueda. Carga masiva con drag&drop. Links contextuales en vez de botones saturados. Microinteracciones tipo SaaS moderno. | Preferencia consultora + Manual de Marca PGN                                         | ✅ Validado |
| 2026-04-29  | Metodología | Enfoque de trabajo: una pantalla por respuesta, validación explícita antes de avanzar, coherencia visual entre pantallas, preguntas concretas antes de diseñar. | Instrucciones de comportamiento para el asistente                                    | ✅ Validado |

---

## 🆕 Espacio para Nuevas Decisiones

*(Agregar nuevas filas aquí a medida que se validen ajustes)*

| Fecha | Categoría | Decisión / Ajuste | Norma / Justificación | Estado |
|-------|-----------|-------------------|----------------------|--------|
|       |           |                   |                      |        |
|       |           |                   |                      |        |
|       |           |                   |                      |        |

---

## 🔍 Búsqueda Rápida por Categoría

<details>
<summary>✅ Flujo Procesal</summary>

- El expediente existe desde la radicación de la noticia, independientemente del resultado posterior.
- La inhibición cierra el expediente sin vincular investigado ni activar términos procesales.
- Separación funcional instructor/juzgador reforzada a nivel de permisos del sistema.

</details>

<details>
<summary>🎨 UX/UI & Diseño</summary>

- Paleta de colores PGN estricta: Azul #063853 (primario), Amarillo #FFE601 (acento), Rojo #E3201B (crítico).
- Tipografía: Montserrat + Poppins.
- Bordes redondeados, sombras suaves, microinteracciones tipo SaaS moderno.
- Semáforo de términos en 4 niveles con días específicos.
- 7 principios UX con aplicación concreta al contexto disciplinario.

</details>

<details>
<summary>⚙️ Técnico & Seguridad</summary>

- Arquitectura modular, API-first, preparada para integración con ORFEO.
- OAuth 2.0 + JWT, AES-256, TLS 1.3, logs inmutables.
- RBAC/ABAC con separación funcional automática instructor/juzgador.
- 7 módulos funcionales: gestión de expedientes, control de términos, generación de actos, notificaciones, pruebas, recursos, dashboard.

</details>

<details>
<summary>⚖️ Jurídico & Normativo</summary>

- Citar siempre el artículo del CGD al mencionar etapas, plazos o garantías.
- Reserva de la actuación por etapa (Art. 115 CGD) con controles de acceso diferenciados.
- Glosario de términos para coherencia en diseño y desarrollo.

</details>

---

> 💡 **Nota:** Este archivo debe mantenerse actualizado en cada iteración del proyecto. Antes de proponer una nueva pantalla o funcionalidad, el asistente consultará este registro para garantizar coherencia con las decisiones previas.

---

**Documento vivo — Última sincronización:** 2026-04-29  
**Próxima revisión programada:** Al validar la primera pantalla prototipada