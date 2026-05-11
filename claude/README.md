
Sistema de información institucional diseñado para digitalizar, orquestar y garantizar la validez jurídica del proceso disciplinario colombiano, desde la radicación de la noticia hasta la ejecutoria del fallo, con trazabilidad auditada, cálculo automático de términos y separación funcional reforzada.

---

##  Características Principales

- **Flujo CGD Completo:** Evaluación de noticia, indagación previa, investigación, juzgamiento (ordinario/verbal), segunda instancia, doble conformidad y revocatoria directa.
- **Control Jurídico Automático:** Reserva por etapa (Art. 115 CGD), cálculo de términos en días hábiles colombianos, validación de elementos obligatorios en autos y pliegos.
- **Separación Funcional:** Bloqueo RBAC/ABAC que impide que un mismo usuario actúe como instructor y juzgador en el mismo expediente (Art. 12 CGD mod. Ley 2094/2021).
- **Asistente `procuradurIA`:** Módulo de IA con trazabilidad obligatoria, cero capacidad decisoria, consentimiento explícito y procesamiento seguro de datos sensibles.
- **UX/UI Institucional:** Manual de Marca PGN, principios de revelación progresiva, semáforo de términos en 4 niveles, accesibilidad WCAG 2.1 AA y patrones SaaS modernos.
- **Interoperabilidad:** Estándares Gobierno Digital (STI), integración con ORFEO, firma digital avanzada con sello de tiempo, exportación PDF/A+XML y reporte a SIRI/SCC.

---

## 📂 Estructura del Repositorio

```
EED/
├── .claude/
│   ├── instructions.md          # 🤖 Orquestador EED (System Prompt principal)
│   ├── memory/
│   │   ├── EED_PROJECT_MEMORY.md # 🧠 Decisiones validadas y estado actual
│   │   ├── decision_log.md       # 📜 Registro trazable de decisiones
│   │   └── EED_INSTRUCCIONES_PROYECTO.md # 📖 Documento maestro normativo/técnico
│   └── agents/
│       ├── ux-designer.md        # 🎨 Diseñador UI/UX & Prototipador
│       ├── legal-compliance.md   # ⚖️ Validador normativo CGD
│       ├── hu-architect.md       # 📝 Arquitecto de Historias de Usuario (Gherkin)
│       ├── qa-critic.md          # 🔍 Revisor crítico independiente
│       └── tech-architect.md     # ️ Arquitecto técnico & STI

├── prototypes/                   # 🖼️ Prototipos HTML/CSS validados (01 a 09+)
── user_stories/                 # 📄 Historias de usuario por módulo (HU-XX.md)
├── docs/                         # 📚 Documentación técnica, flujos, glosario
├── src/                          #  Código fuente (frontend/backend/shared)
└── README.md                     # 📘 Este archivo
```

---

## 🛠️ Stack Tecnológico

| Capa          | Tecnología                                                                 |
|---------------|----------------------------------------------------------------------------|
| **Frontend**  | React / Vue / Angular (por definir con TI PGN)                             |
| **Backend**   | Node.js / Python / Java (API-first, modular)                               |
| **Base de Datos** | PostgreSQL (transaccional, RLS, logs inmutables)                        |
| **Seguridad** | OAuth 2.0 + JWT, AES-256, TLS 1.3, firma digital con sello de tiempo       |
| **Integraciones** | ORFEO, Plataforma de Firma Digital, SIRI, SCC, SECOP II                  |
| **Cumplimiento** | Estándares Gobierno Digital (STI), WCAG 2.1 AA, Ley 1581/2012 (Habeas Data) |

---

## 🤖 Sistema de Agentes IA (Orquestación)

El proyecto utiliza un modelo de **orquestación por contexto** nativo en Claude Code. No requiere instalación de servicios externos. El archivo `.claude/instructions.md` actúa como cerebro y coordina internamente 6 modos especializados según palabras clave:

| Agente (Modo)          | Trigger de Activación                          | Función Principal                                  |
|------------------------|-----------------------------------------------|----------------------------------------------------|
| `ux_designer`          | `diseñar pantalla`, `prototipo`, `componente` | Genera HTML/CSS autocontenido con tokens PGN       |
| `legal_compliance`     | `validar`, `norma`, `CGD`, `artículo`         | Verifica alineación normativa y riesgos de nulidad |
| `hu_architect`         | `historia de usuario`, `HU`, `Gherkin`        | Documenta requisitos en formato PGN                |
| `qa_critic`            | `revisar`, `crítica`, `gap`, `riesgo`         | Auditoría independiente de coherencia y calidad    |
| `tech_architect`       | `arquitectura`, `integración`, `ORFEO`, `STI` | Define contratos técnicos y seguridad              |


### 🔄 Flujo de Trabajo Recomendado
1. **Activación:** Pegar prompt inicial en Claude Code: `Inicializar proyecto EED. Leer .claude/instructions.md y memoria. Confirmar modos activos.`
2. **Desarrollo:** Solicitar pantalla o HU. El orquestador detecta el modo, aplica validaciones cruzadas y entrega estructura estandarizada.
3. **Validación:** Revisar secciones `VALIDATION RESULTS` y `QA OBSERVATIONS`. Responder `✅ Aprobado` o `️ Observaciones: [texto]`.
4. **Persistencia:** El sistema actualiza automáticamente `EED_PROJECT_MEMORY.md` y `decision_log.md`.

---

## 📖 Documentación Normativa & Técnica

- `docs/EED_INSTRUCCIONES_PROYECTO.md`: Marco jurídico CGD, flujo procesal completo, matriz de permisos, glosario y especificaciones UI/UX.
- `.claude/memory/EED_PROJECT_MEMORY.md`: Estado actual del proyecto, entregables validados y preferencias de diseño.
- `.claude/memory/decision_log.md`: Registro cronológico e inmutable de decisiones de diseño, jurídicas y técnicas.

> ⚖️ **Nota Legal:** Toda decisión de diseño se valida contra la Ley 1952 de 2019 modificada por la Ley 2094 de 2021. El sistema prioriza la validez procesal sobre la estética. `procuradurIA` asiste pero **nunca decide, firma ni notifica**.

---

## 🚀 Primeros Pasos (Desarrollo)

1. **Clonar & Vincular:** Conectar repositorio a Claude Code Web (`claude code init` o Projects > Connect GitHub).
2. **Cargar Contexto:** Asegurar que `.claude/instructions.md` esté en la raíz.
3. **Prompt de Inicio:**
   ```
   Inicializar proyecto EED. Leer memoria de contexto. Confirmar límites no negociables y modos activos. Estado listo para primera tarea.
   ```
4. **Solicitar Entregable:** Ej. `Diseñar pantalla 10: Dashboard de Gestión de Investigación (Instructor). Reutilizar componentes de prototipos 02 y 08. Validar con legal_compliance.`
5. **Iterar:** Revisar entregable, aprobar o solicitar ajustes. El sistema registra la versión en `iteration_history`.

---

## 🤝 Contribución & Gobierno del Proyecto

- **Metodología:** Una pantalla/HU por iteración. Validación explícita obligatoria antes de avanzar.
- **Ramas:** `main` (validado), `dev` (en progreso), `feature/[modulo]-[pantalla]`.
- **Commits:** `feat: HU-10 dashboard investigación v1`, `fix: validación art. 215 auto apertura`, `docs: actualizar decision_log`.
- **Revisión:** Todo cambio requiere aprobación de la Consultora EED y/o Veeduría PGN antes de merge.

---

## 👩‍⚖️ Mantenedor & Contacto

**Elaborado por:** Nathalia Carvajal — Consultora EED / LegalTech  
**Entidad:** Procuraduría General de la Nación — Oficina de Control Interno Disciplinario (Veeduría)  
**Marco:** Ley 1952 de 2019 + Ley 2094 de 2021 (CGD)  
**Última actualización:** Mayo 2026  

> 📌 *Este repositorio contiene prototipos, documentación y prompts de orquestación. El código fuente de producción se desarrollará en `src/` bajo los estándares STI de Gobierno Digital y políticas de seguridad de la entidad.*
```
