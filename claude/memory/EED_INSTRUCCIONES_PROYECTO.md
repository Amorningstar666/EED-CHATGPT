# EED — EXPEDIENTE ELECTRONICO DISCIPLINARIO
## Procuraduria General de la Nacion — Documento de Proyecto

**Version:** 6.0  
**Fecha de ultima actualizacion:** 2026-04-29  
**Elaborado por:** Nathalia Carvajal  
**Fuentes de referencia:** Flujo oficial PGN (Ley 1952/2019 mod. Ley 2094/2021) — Manual de Marca PGN — Instrucciones complementarias Oficina Control Interno Disciplinario Veeduria  
**Estado:** En construccion — documento vivo

---

## 1. RESUMEN EJECUTIVO

El Expediente Electronico Disciplinario (EED) es un sistema de informacion institucional destinado a digitalizar, orquestar y garantizar la validez juridica del proceso disciplinario adelantado por la Procuraduria General de la Nacion de Colombia.

El sistema cubre el ciclo completo: desde la evaluacion de la noticia disciplinaria hasta la ejecutoria del fallo, segunda instancia, doble conformidad, ejecucion de la sancion y reporte a los sistemas de informacion estatales. Incluye ademas los mecanismos transversales al proceso: impedimentos y recusaciones, nulidades, acumulacion, revocatoria directa y mecanismos extraprocesales (derecho de peticion, accion de tutela).

Cada etapa queda con trazabilidad auditada, terminos calculados automaticamente y separacion funcional reforzada entre instructor y juzgador conforme a la Ley 2094 de 2021.

**Objetivo principal:** reemplazar el expediente fisico por un expediente electrónico juridicamente valido, seguro, interoperable y usable por perfiles tecnicos y no tecnicos.

---

## 2. CONTEXTO INSTITUCIONAL

| Campo | Descripcion |
|---|---|
| Entidad | Procuraduria General de la Nacion de Colombia |
| Ambito | Proceso disciplinario — Ley 1952 de 2019 y Ley 2094 de 2021 |
| Usuarios internos | jefe de dependencia, funcionarios de instruccion, funcionarios de secretaria, funcionario de juzgamiento, revisor, aprobador| 
| Usuarios externos | Quejosos, disciplinados, defensores, victimas, ciudadanos |
---

## 3. MARCO JURIDICO DE REFERENCIA

Toda decision de diseno — funcional, tecnico o de UX — debe validarse contra el siguiente marco. Citar siempre el articulo especifico.

| Norma | Contenido relevante |
|---|---|
| Ley 1952 de 2019 | Codigo General Disciplinario (CGD) — norma base |
| Ley 2094 de 2021 | Modificaciones al CGD: separacion instructor/juzgador, doble conformidad, terminos, confesion, juicio verbal |
| Decreto 1081 de 2015 | Gobierno Digital |
| Decreto 1083 de 2015 | Firma y notificaciones electronicas |
| Ley 1581 de 2012 | Proteccion de datos personales |
| Ley 1755 de 2015 | Derecho de Peticion y transparencia |
| Ley 1712 de 2014 | Acceso a informacion publica — reserva del proceso |
| Decreto Ley 262 de 2000 mod. Decreto Ley 1851 de 2021 | Competencias del Procurador General (revocatoria directa) |
| Sentencia C-030 de 2023 y Auto de Unificacion Consejo de Estado 03/12/2024 | Servidores electos popularmente — remision a Consejo de Estado para recurso de revision |

**Principios rectores:** debido proceso, presuncion de inocencia, derecho a la defensa, contradiccion, celeridad, transparencia, eficacia, reserva de la informacion, eficiencia.

---

## 4. MODELO DE ENTIDADES DEL SISTEMA

El sistema maneja una unica entidad raiz — el Expediente — que existe desde el momento de la radicacion de cualquier noticia disciplinaria. Lo que varia segun el resultado del analisis de procedibilidad es el **estado y tipo del expediente**, no su existencia.

| Entidad | Descripcion | Se crea cuando |
|---|---|---|
| Expediente | Contenedor unico de toda actuacion, desde la radicacion de la noticia hasta su finalizacion. Tiene numero de radicado desde el primer momento. | Siempre, al radicarse cualquier noticia disciplinaria |
| ActoProcesal | Cualquier auto, decision, comunicacion o notificacion dentro del expediente | Cada paso del flujo |
| Termino | Plazo legal por etapa con fecha de inicio, vencimiento y estado | Automatico por etapa cuando aplica |
| Prueba | Documento, testimonio, peritacion, informe tecnico, confesion, inspeccion disciplinaria vinculados al expediente | Instruccion y juzgamiento |
| Sancion | Resultado ejecutoriado con tipo, duracion y estado de ejecucion | Fallo ejecutoriado |
| AuditLog | Registro inmutable de toda accion sobre cualquier entidad | Continuo |

**Tipos de expediente segun resultado del analisis de procedibilidad:**

| Tipo | Descripcion | Investigado vinculado | Actuacion disciplinaria |
|---|---|---|---|
| Inhibido (Art. 209 CGD) | Noticia que resulta en decision inhibitoria. Tiene radicado y expediente. El expediente queda cerrado con el acto inhibitorio y la comunicacion al quejoso. | No | No |
| Trasladado | Noticia remitida por competencia a otra entidad. Tiene radicado. Queda cerrado con el auto de traslado. | No | No — continua en otra entidad |
| Con actuacion (indagacion, investigacion, juzgamiento) | Expediente con proceso disciplinario activo. | Si, desde la apertura | Si |

**Regla de diseno critica:** el numero de radicado se asigna **siempre** al momento de recibir la noticia, independientemente del resultado posterior. Lo que cambia es el tipo y estado del expediente. La inhibicion (Art. 209) cierra el expediente sin vincular investigado ni abrir actuacion disciplinaria, pero el expediente y su radicado existen y son trazables. Contra la decision inhibitoria no procede recurso, pero el quejoso recibe comunicacion y el expediente queda en el sistema con acceso restringido segun el perfil.

---

## 5. FLUJO PROCESAL

### BLOQUE 0 — EVALUACION DE LA NOTICIA DISCIPLINARIA

**Tipos de noticia disciplinaria (Art. 86 CGD):**
- Queja formulada por cualquier persona natural o juridica
- Informacion de servidor publico
- De oficio
- Anonimo 
- Otro medio que amerite credibilidad (redes sociales, paginas web, medios de comunicacion, etc.)

**Decisiones posibles al evaluar la noticia — pueden ser conjuntas o por cada hecho:**

| Decision | Norma | Descripcion |
|---|---|---|
| Inhibitorio | Art. 209 CGD | Ver desarrollo abajo |
| Indagacion previa | Art. 208 CGD | Ver desarrollo abajo |
| Investigacion disciplinaria | Art. 211 CGD | Cuando el autor es identificado desde la noticia |
Acumulacion | Art. 98 CGD | Ver desarrollo abajo
Compulsa de copias | Art. 87 y 99 CGD |Ver desarrollo abajo
Conflicto de Competencias |Art. 99 CGD | Ver desarrollo abajo
| Traslado por competencia | Art. 76, 91-103 CGD | Ver desarrollo abajo |
| Remision por poder preferente | Art. 3, 93 CGD | Ver desarrollo abajo |
| Impedimento y recusacion | Art. 104-108 CGD | Ver desarrollo abajo |
| Devolucion | | Ver desarrollo abajo
| Incorporacion de noticia||Ver desarrollo abajo
---

### BLOQUE 1 — DECISION INHIBITORIA
**Norma:** Art. 209 CGD  
**Naturaleza:** Decision de plano que impide el inicio de actuacion disciplinaria. No equivale al archivo del Art. 90 CGD.

**Importante:** la decision inhibitoria **si genera radicado y expediente**. El expediente existe desde la radicacion de la noticia. Lo que la inhibicion impide es la apertura de actuacion disciplinaria, la vinculacion de un investigado y el inicio de terminos procesales. El expediente queda cerrado en estado "Inhibido" con trazabilidad completa.

**Causales (Art. 209 CGD):**
- Queja manifiestamente temeraria
- Hechos disciplinariamente irrelevantes
- Hechos de imposible ocurrencia
- Hechos absolutamente inconcretos o difusos
- La accion disciplinaria no puede iniciarse


**Efectos en el sistema:**
- El expediente existe con su numero de radicado desde la radicacion de la noticia
- El expediente cambia de estado a "Inhibido"
- No se vincula investigado al expediente
- No se activan modulos de terminos procesales ni de notificacion al disciplinado
- Se genera comunicacion al quejoso (no notificacion formal)
- Contra esta decision no procede recurso alguno (Art. 209 CGD)
- El expediente queda cerrado y auditable
- No hace transito a cosa juzgada

**Diferencia con el archivo (Art. 90/152 CGD):** el archivo supone que ya habia actuacion disciplinaria iniciada, se notifica formalmente a los sujetos procesales y la decision puede hacer transito a cosa juzgada formal. Son estados distintos del expediente con efectos juridicos distintos.
**Por extincion de la accion (Art. 32 CGD):**
- Muerte del disciplinable
- Prescripcion (Art. 33 CGD)

**Terminos de prescripcion:**

| Tipo de falta | Termino | Contado desde |
|---|---|---|
| Faltas instantaneas | 5 anos | Dia de consumacion |
| Faltas permanentes o continuadas | 5 anos | Realizacion del ultimo acto |
| Faltas omisivas | 5 anos | Cuando ceso el deber de actuar |
| Renuncia a la prescripcion (Art. 34) | 2 anos adicionales | Presentacion personal de la solicitud |

**Por cosa juzgada (Art. 16 CGD):**
- Mismo sujeto investigado + misma conducta + mismo fundamento normativo
- El sistema debe verificar estas tres identidades antes de admitir una nueva noticia

---

### BLOQUE 2 — TRASLADO POR COMPETENCIA Y REMISIONES
**Norma:** Art. 76, 91-101 CGD — Actuacion transversal a todo el proceso

**Factores determinantes de competencia (Art. 91):**
- Factor subjetivo: calidad del sujeto disciplinable
- Factor objetivo: naturaleza del hecho
- Factor territorial: lugar donde se cometio la falta
- Factor funcional: distribucion de competencias entre dependencias
- Conexidad (Art. 98): mismo disciplinado, mismo contexto, sin auto de cierre

**Nota:** cuando resulte incompatible la aplicacion de los factores territorial y funcional, prevalece el factor funcional.

**Organos receptores por tipo de remision:**

| Tipo | Organo | Ambito |
|---|---|---|
| Poder preferente | Oficina Control Disciplinario Interno (Art. 93) | Servidores de la entidad |
| Poder preferente | Personeria municipal o distrital (Art. 3) | Servidores nivel municipal |
| Poder preferente | Superintendencia de Notariado | Notarios (Art. 76) |
| Incompetencia PGN | Comision Nacional de Disciplina Judicial o Seccionales | Rama Judicial |
| Incompetencia PGN | Corte Suprema de Justicia | Procurador General (Art. 100) |
| Incompetencia PGN | Congreso — Comision de Etica | Congresistas (Par. 2 Art. 101) |
| Incompetencia PGN | Comision de Investigacion y Acusacion — Camara | Altos funcionarios del Estado |
| Competencia Interna PGN| Dependencias PGN

**Conflicto de competencia:** puede proponerlo quien se considere incompetente. Si no hay acuerdo entre iguales niveles, lo dirime el superior inmediato.

---

### BLOQUE 3 — IMPEDIMENTOS Y RECUSACIONES
**Norma:** Art. 104-108 CGD — Actuacion transversal a todo el proceso

**Causales:** las establecidas en el Art. 104 CGD.

**Impedimento (Art. 105):**
- El funcionario se declara impedido
- Se suspende la actuacion y se envia al superior
- El superior decide dentro de 3 dias

**Recusacion:**
- El recusado manifiesta si acepta o no dentro de 2 dias
- Se suspende la actuacion y se envia al superior
- Si acepta: se determina quien conoce el proceso
- Si no acepta: continua quien estaba conociendo

**Procurador General (Art. 108):**
- Si acepta la causal: asume el Viceprocurador General
- Si no acepta: se envia a la Sala de Consulta y Servicio Civil del Consejo de Estado (5 dias para decidir)
  - Si acepta la causal: envia al Viceprocurador
  - Si declara infundada: devuelve al Despacho del Procurador

**Efecto en el sistema:** el modulo de impedimentos debe suspender automaticamente los terminos del expediente afectado y registrar el cambio de funcionario en el log de auditoria. Semaforo alerta de tres dias para decidir

---

### BLOQUE 4 — INCORPORACION DE NOTICIA
Cuando existe un expediente disciplinario en tramite por los mismos hechos, la nueva noticia se incorpora a ese expediente. Condiciones:
- Identidad del sujeto disciplinable
- Mismos hechos objeto de investigacion
- Misma naturaleza de la conducta investigada
- la misma queja noticia radicada en otras dependencias
---
### BLOQUE ACUMULACION
**Norma:** Art. 98 CGD — Actuacion transversal a todo el proceso
Cuando existe una actuacion disciplinaria en tramite por los mismos hechos, la nueva noticia se incorpora a ese expediente. 
Requisitos:
- Identidad del sujeto disciplinable
- Mismos hechos objeto de investigacion
- Misma naturaleza de la conducta investigada
- no se haya proferido el cierre
- no se haya vencido el termino de la investigacioN
Efecto en el sistema: Verificar que no se encuentre en etapa procesal de cierre o investigacion vencida. solo queda activo al expediente que se acumulo y los archivos del expediente acumulado se pueden ver en el expediente al que se acumulo.
---
### BLOQUE DEVOLUCION
Cuando falte realizar analisis de la directiva 007 de 2026
Para dar cumplimiento  a una solicitud
Efecto en el sistema: SE DEVUELVE A LA DEPENDCIA DE LA PGN, O SE DEVUELVE A LA OFICINA DE RELACIONAMIENTO CIUDADANO.
## 6. INSTRUCCION

### 6.1 INDAGACION PREVIA
**Norma:** Art. 208 CGD

**Procedencia y finalidad:**
- Cuando hay duda sobre la identificacion o individualizacion del posible autor (en averiguacion de responsables)
- Para practica de pruebas con medios de prueba legalmente reconocidos

**Terminos:**

| Conducta | Termino |
|---|---|
| Todas las conductas | 6 meses |
| Violacion de DDHH o DIH | 6 meses adicionales |

**Recursos:** no proceden.

**Decisiones posibles:**

| Decision | Condicion | Efectos |
|---|---|---|
| Archivo | No se logro identificar al autor o no procede investigacion | No hace transito a cosa juzgada |
| Prescripcion | Vencimiento del termino (Art. 33 CGD) | Ver tabla de prescripcion |
| Apertura de investigacion | Se identifico al posible autor | Continua el flujo |

**Notificacion del archivo en indagacion previa:**
- A sujetos procesales: notificacion de decisiones interlocutorias (Art. 123 CGD)
- Al quejoso: comunicacion (Art. 129 CGD)

**Recurso de apelacion contra el archivo (Art. 224 CGD):**
- No se interpuso: fin
- Se interpuso:
  - Superior confirma: fin
  - Superior revoca: devuelve para abrir investigacion
  - No concede el recurso: recurso de queja (2 dias para resolver)
    - Superior concede apelacion
    - Superior no concede apelacion

**Ruptura de la unidad procesal en indagacion previa (Art. 214 CGD):**
- Cuando no se identifican todos los investigados
- Cuando uno tiene fuero constitucional o legal que implique cambio de competencia
- Cuando se decrete nulidad parcial de la actuacion

---

### 6.2 INVESTIGACION DISCIPLINARIA
**Norma:** Art. 211-216 CGD

**Procedencia (Art. 211):** de la queja, la informacion recibida o la indagacion previa cuando se identifica al posible autor.

**Finalidad (Art. 212):** verificar la ocurrencia de la conducta, determinar si es constitutiva de falta o si hay causal de exclusion de responsabilidad.

**Terminos (Art. 213):**

| Supuesto | Termino |
|---|---|
| Regla general | 6 meses |
| Varias faltas o 2 o mas sujetos | Prorrogable 6 meses mas |
| Infracciones DDHH o DIH | No puede exceder 18 meses |
| Pruebas pendientes que modifiquen situacion juridica | Prorroga 3 meses adicionales |

**Contenido del auto de apertura de investigacion (Art. 215):**
- Identidad del autor o posibles autores
- Hechos disciplinariamente relevantes
- Pruebas a decretar
- Orden de incorporar antecedentes disciplinarios, certificacion laboral y de salarios, ultima direccion conocida
- Beneficios de la confesion o aceptacion de cargos

**Notificacion:** personal (Art. 121). Si no se logra: por edicto (Art. 127) o electronica con previa autorizacion escrita (Art. 122).

**Recursos contra el auto de apertura:** no proceden.

**Medidas preventivas que pueden proferirse durante la investigacion:**

**Suspension provisional (Art. 127 CGD):**

| Termino | Condicion |
|---|---|
| 3 meses | Regla general |
| + 3 meses | Prorrogable |
| + 3 meses | Una vez proferido el fallo de primera instancia |

- Consulta de la declaratoria y sus prorrogas ante el superior, sin perjuicio de cumplimiento inmediato
- El superior corre traslado de 3 dias al disciplinado para alegaciones
- Se decide dentro de los 10 dias siguientes
- Revocatoria: cuando desaparezcan los motivos, por archivo o terminacion del proceso, o si expira el termino sin fallo de primera instancia

**Suspension del procedimiento administrativo (Art. 219 CGD):**
- Para que cesen los efectos y se eviten perjuicios
- Cuando se evidencien circunstancias de vulneracion del ordenamiento juridico o fraude al patrimonio publico
- Revocatoria cuando hayan cesado los efectos y las circunstancias

**Actuaciones sobre pruebas durante la investigacion:**

Autos sobre practica de pruebas:
- Auto que decreta pruebas de oficio: comunicar a sujetos procesales (Art. 129 CGD)
- Auto que niega practica de pruebas: notificacion interlocutoria (Art. 123 CGD) — recurso de reposicion hasta 5 dias

Prueba pericial:
- Auto que ordena devolver al perito para correccion o complementacion
- Auto de traslado a sujetos procesales por 3 dias para solicitar aclaracion, complementacion o adicion
  - Si se acepta: perito tiene 5 dias (prorrogable una vez) para aclarar o complementar
  - Si se niega: recurso de reposicion hasta 5 dias
- Objecion del dictamen por error grave:
  - Se acepta: nuevo perito emite dictamen
  - Se declara improcedente: recurso de reposicion hasta 5 dias

Testigo renuente (Art. 165 CGD):
- Auto que ordena seguir el procedimiento: notificacion interlocutoria (Art. 123)
- Auto que impone multa: notificacion interlocutoria — recurso de reposicion hasta 5 dias
- Auto que ordena conduccion del testigo: comunicacion (Art. 129)

**Confesion durante la investigacion (Art. 161 CGD):**
- Desde la apertura de investigacion hasta antes de la ejecutoria del auto de cierre
- En 10 dias se evalua la manifestacion
- Se suscribe acta con los terminos de la confesion (equivale al pliego de cargos)
- Se remite a juzgamiento para fallo en 45 dias. No hay retractacion salvo violacion de derechos fundamentales

| Tipo | Beneficio | Excepcion |
|---|---|---|
| Total | Sanciones (inhabilidad, suspension o multa) disminuidas a la mitad | No aplica para faltas gravisimas del Art. 52 CGD |
| Parcial | Ruptura de la unidad procesal | — |

**Nulidades durante la investigacion (Art. 204 CGD):**
- De oficio: auto que la declara — no procede recurso — notificacion interlocutoria
- A solicitud de parte (dentro de 5 dias):
  - Declara nulidad: recurso de reposicion hasta 5 dias
  - Niega nulidad: recurso de reposicion hasta 5 dias

**Acumulacion (Art. 98 CGD):**
Procede cuando:
1. Se adelanta contra el mismo disciplinado
2. Conductas en el mismo contexto de hechos o de la misma naturaleza
3. No se haya proferido auto de cierre ni vencido el termino de investigacion

- De oficio: no procede recurso
- A solicitud de parte — acepta: competencia para juzgar al de mayor jerarquia
- A solicitud de parte — niega: recurso de reposicion hasta 5 dias

---

### 6.3 CIERRE DE LA INVESTIGACION DISCIPLINARIA
**Norma:** Art. 220 CGD  
**Naturaleza:** auto de sustanciacion que declara cerrada la investigacion.  
**Procedencia:** cuando se hayan recaudado las pruebas ordenadas o este vencido el termino.  
**Finalidad:** presentar alegatos precalificatorios.  
**Traslado:** a sujetos procesales por 10 dias.  
**Notificacion:** decisiones interlocutorias (Art. 213).  
**Recursos:** no proceden.

---

### 6.4 EVALUACION DE LA INVESTIGACION Y CALIFICACION PROVISIONAL

**Decisiones (Art. 222-223 CGD):**

**A — Pliego de cargos (Art. 222-223 CGD):**

Contenido obligatorio:
1. Identificacion del autor o autores
2. Denominacion del cargo o funcion en la epoca de comision
3. Descripcion de la conducta con circunstancias de tiempo, modo y lugar
4. Normas presuntamente violadas y concepto de la violacion
5. Analisis de la ilicitud sustancial
6. Analisis de la culpabilidad
7. Analisis de las pruebas que fundamentan cada cargo
8. Exposicion fundada de criterios de gravedad o levedad (Art. 47 CGD)
9. Analisis de argumentos de los sujetos procesales

Notificacion: personal (Art. 121 y 225) y por edicto (Art. 127) o electronica (Art. 122 CGD).

Defensor de oficio: si el procesado o su defensor no se presentan dentro de los 5 dias siguientes a la entrega de la comunicacion, se designa defensor publico o estudiante de consultorio juridico (Art. 225, Art. 72 Ley 2094/21).

Recursos: no proceden.

Remision a juzgamiento: dentro de los 3 dias siguientes a la notificacion.

**B — Terminacion del proceso y archivo definitivo (Art. 90 y 213 CGD):**

Causales (Art. 90):
- El hecho no existio
- La conducta no esta prevista como falta
- El disciplinado no la cometio
- Existe causal de exclusion de responsabilidad
- La actuacion no podia iniciarse o proseguirse (muerte, no identificacion del autor)

Notificacion: a sujetos procesales (Art. 123 CGD) y comunicacion al quejoso (Art. 129 Inc. 2 CGD).

Recurso de apelacion (Art. 224 CGD):
- Sujetos procesales: hasta 5 dias desde la notificacion
- Quejoso: hasta 5 dias desde la comunicacion (Art. 110 paragrafo)
- Superior confirma: fin
- Superior revoca: devuelve para continuar
- No se concede: recurso de queja

---

## 7. JUZGAMIENTO

### 7.1 FIJACION DEL JUZGAMIENTO
**Norma:** Art. 225A CGD

Auto de sustanciacion motivado que:
- Avoca el conocimiento del juzgador
- Informa beneficios de la confesion o aceptacion de cargos
- Fija el procedimiento: juicio ordinario o juicio verbal
- Recursos: no proceden

**Criterios para elegir el tipo de juicio:**

| Juicio verbal | Juicio ordinario |
|---|---|
| Disciplinable sorprendido en la comision | Faltas graves y gravisimas no incluidas en verbal |
| Faltas leves | Complejidad del asunto, numero de disciplinables o cargos |
| Faltas gravisimas especificas (Art. 54 nums. 4 y 5; 55 nums. 1,2,4,5,6,7,8,10; 56 nums. 1,2,3,5; 57 nums. 1,2,3,5,11; 58, 60, 61 y 62 num. 6) | Carencia de recursos humanos, fisicos o dotacionales |

---

### 7.2 JUICIO ORDINARIO

**Traslado a sujetos procesales — 15 dias (Art. 225B CGD):**
Se ordena en el mismo auto que fija el juzgamiento. La renuencia a presentar descargos no interrumpe el tramite. Vencido el termino el competente resuelve sobre:
- Nulidades propuestas
- Practica de pruebas solicitadas
- Pruebas de oficio

**Auto que resuelve nulidades (Art. 225C):**
- Declara nulidad: ordena reponer la actuacion — recurso de reposicion hasta 5 dias
- Niega nulidad: recurso de reposicion hasta 5 dias

**Auto sobre pruebas (Art. 225 CGD):**
- Criterios: conducencia, pertinencia y necesidad (Art. 151 CGD)
- Decreta pruebas solicitadas: comunicacion (Art. 129) — termino 90 dias
- Niega pruebas: recurso de apelacion hasta 5 dias — se envia al superior
- Pruebas de oficio: comunicacion (Art. 129) — termino 90 dias

**Variacion de cargos en juicio ordinario (Art. 225D CGD):**

Por error en la calificacion:
- Devolucion al instructor por auto de sustanciacion motivado — plazo maximo 15 dias para nueva calificacion — no procede recurso
- Instructor varia el pliego: notificacion personal — remite a juzgamiento — juzgamiento aplica Art. 225A
- Instructor no varia: comunica a juzgamiento — juzgamiento puede decretar nulidad del pliego

Por prueba sobreviniente:
- El funcionario de juzgamiento varia el pliego (no implica juicio previo de responsabilidad)
- Notificacion personal (Arts. 121 y 127)
- Termino para descargos, solicitar y aportar pruebas: 10 dias
- Periodo probatorio: maximo 2 meses

**Confesion o aceptacion de cargos en juzgamiento (Art. 161 y 162 CGD):**
Hasta la ejecutoria del auto que concede el traslado para alegar de conclusion:

| Tipo | Beneficio | Excepcion |
|---|---|---|
| Total | Sanciones disminuidas en una tercera parte | No aplica para faltas gravisimas Art. 52 CGD |
| Parcial | Ruptura de la unidad procesal | — |

Se profiere el fallo dentro de los 15 dias siguientes.

**Traslado para alegatos de conclusion (Art. 225E):**
- Si no hay pruebas que practicar, o si ya se practicaron las decretadas
- Traslado comun por 10 dias a los sujetos procesales

---

### 7.3 JUICIO VERBAL
**Norma:** Art. 225H - 231 CGD

**Auto que decide adelantar el juicio verbal (Art. 225H):**
- Fija fecha y hora para audiencia: no menor a 10 dias ni mayor a 20 dias desde el auto de citacion
- Recursos: no proceden

**Instalacion de la audiencia (Art. 227):**

Si el disciplinable acude con defensor:
- Se pregunta si acepta la responsabilidad imputada en el pliego de cargos
  - Acepta total: tramite Art. 162 CGD (beneficios de confesion)
  - Acepta parcial: ruptura de la unidad procesal
  - No acepta: version libre, descargos y solicitud de pruebas por el disciplinable y el defensor. Interviene el Ministerio Publico, victimas o perjudicados si concurren.

Si el disciplinable acude sin defensor:
- Se pregunta si se acoge al beneficio de confesion o aceptacion de cargos
  - Si acepta: se suspende la audiencia 5 dias para designar defensor publico o que asista con uno de confianza
  - No acepta: continua el juicio verbal

Se presentan los hechos en forma sucinta y se leen los cargos.

**Continuacion de la audiencia:**
- Descargos y solicitud de pruebas en descargos (Art. 227)
- Resolucion de nulidades solicitadas: notificacion en estrados — recurso de reposicion en el curso de la audiencia
- Pruebas: se decreta en audiencia fijando fecha y hora para la sesion en que se practicaran
  - Niega pruebas: recurso de apelacion ante el superior — interposicion y sustentacion en el curso de la audiencia

**Variacion de cargos en juicio verbal (Art. 229):**

Por error en la calificacion: igual al juicio ordinario con plazos adaptados al verbal.

Por prueba sobreviniente:
- Notificacion en estrados — suspension de audiencia
- Reanuda en termino no menor a 5 ni mayor a 10 dias
- Descargos, solicitar y aportar pruebas: a cargo del disciplinable o defensor
- Periodo probatorio maximo: 1 mes

**Traslado para alegatos previos al fallo (Art. 230):**
- Suspension de audiencia por 10 dias para preparar alegatos
- Reanuda: presentan alegatos en orden — Ministerio Publico, victima, disciplinable, defensor
- Se cita para el fallo dentro de los 15 dias siguientes

**Fallo de primera instancia en juicio verbal (Art. 231):**
- Debe constar por escrito
- Notificacion en estrados
- Recurso de apelacion:
  - No se interpuso: el fallo queda ejecutoriado al terminar la audiencia
  - Se interpone en la misma diligencia y puede sustentarse verbalmente de inmediato, o por escrito dentro de los 5 dias siguientes ante la Secretaria del Despacho
  - Se concede en audiencia: remision al superior
  - No se concede: recurso de queja

---

### 7.4 FALLO DE PRIMERA INSTANCIA — CONTENIDO Y TRAMITE GENERAL

**Termino:** 30 dias habiles.

**Notificacion:** personal (Art. 121 y 127).

**Recurso de apelacion:**
- Interposicion y sustentacion: 10 dias siguientes a la notificacion
- No se interpuso: fin
- Si se interpuso: continua

**Contenido del fallo sancionatorio:**
- Nombres de los sancionados
- Cargo o funcion y entidad
- Calificacion definitiva de la falta
- Culpabilidad y grado
- Sancion y termino

**Contenido del fallo absolutorio:**
- Nombres de los absueltos
- Cargo o funcion y entidad
- Motivo de la decision

**Correccion, aclaracion y adicion del fallo (Art. 140 CGD):**
- De oficio o a peticion de parte
- Causales: error aritmetico, nombre o identidad del investigado, entidad, denominacion del cargo, omision sustancial en la parte resolutiva
- Competencia: mismo funcionario que lo profirio
- Notificacion: personal (Art. 121, 122 y 127)
- No procede: se rechaza mediante auto que no afecta la ejecutoria

**Auto que concede el recurso de apelacion:** envio al superior.  
**Auto que no concede:** recurso de queja.

---

## 8. SEGUNDA INSTANCIA Y DOBLE CONFORMIDAD

**Norma:** Art. 235 CGD y Art. 12 CGD

### 8.1 TRAMITE EN SEGUNDA INSTANCIA

**Pruebas de oficio (Art. 235 CGD):**
- Excepcionalmente, cuando puedan modificar sustancial y favorablemente la situacion juridica del disciplinado
- Traslado de 5 dias a sujetos procesales una vez practicadas

**Terminos para decidir:**

| Supuesto | Termino |
|---|---|
| Sin decreto de pruebas | 45 dias desde recibido el expediente |
| Con decreto de pruebas | 40 dias desde vencido el traslado |

**Prescripcion en segunda instancia (Art. 33 CGD):**

| Tipo de falta | Termino | Contado desde |
|---|---|---|
| Todas las faltas (excepto Art. 52 DDHH/DIH) | 2 anos | Notificacion del fallo de primera instancia |
| Faltas gravisimas Art. 52 DDHH/DIH | 3 anos | Notificacion del fallo de primera instancia |

### 8.2 FALLO DE SEGUNDA INSTANCIA

**Notificacion:** personal (Art. 121, 122 y 127 CGD).

**Confirma fallo sancionatorio:**

| Tipo de servidor | Efecto |
|---|---|
| Servidores electos popularmente cuya sancion afecte derechos politicos (destitucion, inhabilidad general, suspension con inhabilidad especial) — Sentencia C-030/23 y Auto Consejo de Estado 03/12/24 | Se remite al Consejo de Estado para recurso de revision, previo traslado de 30 dias al sancionado y su defensor |
| Demas servidores y particulares disciplinables | Ejecutoriado en la fecha en que culmine la notificacion. Registro de la sancion y comunicacion a quien deba ejecutarlo |

**Revoca — fallo absolutorio:** fin del proceso.

**Declara nulidad:** se devuelve al competente de instruccion o juzgamiento segun la etapa hasta la cual se declaro la nulidad.

### 8.3 DOBLE CONFORMIDAD (Art. 12 CGD)

**Procedencia:**
- En todos los casos en que el fallo de primera instancia es absolutorio y el de segunda instancia es sancionatorio
- El disciplinable tiene derecho a que el fallo sancionatorio sea revisado por una autoridad diferente
- El tramite es el previsto para el recurso de apelacion

**Primer fallo sancionatorio del Procurador General:**
- Sera resuelto por una Sala de tres personas que reunan los requisitos del Art. 232 de la Constitucion
- Sorteada de lista de 12 nombres elaborada por la comision de servicio (concurso de meritos para la Sala Disciplinaria)

---

## 9. ACTUACIONES TRANSVERSALES AL PROCESO

### 9.1 TERMINACION Y ARCHIVO DEFINITIVO (Art. 90 CGD)

Puede proferirse en cualquier etapa de la actuacion.

**Causales:**
- El hecho no existio
- La conducta no esta prevista en la ley como falta
- El disciplinado no la cometio
- Existe causal de exclusion de responsabilidad
- La actuacion no podia iniciarse o proseguirse

**Notificacion:** a sujetos procesales (Art. 123 CGD) y comunicacion al quejoso (Art. 129 CGD).

**Recurso de apelacion (Art. 224 CGD):** misma estructura que el archivo en evaluacion.

### 9.2 RECURSO DE QUEJA

**Procedencia:** cuando no se concede el recurso de apelacion.  
**Termino para interponer:** 2 dias.  
**Tramite:** se envia al superior.
- Superior concede: da tramite al recurso de apelacion
- Superior no concede: devuelve a primera instancia

### 9.3 NULIDADES (Art. 202-207 CGD)

- De oficio (Art. 204): no procede recurso
- A solicitud de parte (dentro de 5 dias): recurso de reposicion hasta 5 dias tanto si se acepta como si se niega

### 9.4 ACUMULACION (Art. 98 CGD)

Mismas reglas que en instruccion. En juzgamiento tambien aplica cuando surge prueba sobreviniente que determina nueva falta o vinculacion de nueva persona.

### 9.5 SOLICITUD DE COPIAS

- Auto que autoriza: comunicacion
- Auto que niega: notificacion interlocutoria — recurso de reposicion hasta 5 dias

### 9.6 RESERVA DE LA ACTUACION (Art. 115 CGD)

Las actuaciones disciplinarias son reservadas hasta cuando se cite a audiencia y se formule pliego de cargos, o se emita auto de archivo definitivo. La reserva no es oponible a autoridades que soliciten informacion para el ejercicio de sus funciones (Art. 27 Ley 1437 de 2011).

El sistema debe implementar controles de acceso diferenciados por etapa procesal.

---

## 10. REVOCATORIA DIRECTA

**Norma:** Art. 141-146 CGD  
**Competencia unica:** Procurador General de la Nacion (Art. 142 y Decreto Ley 262/2000 mod. Decreto Ley 1851/2021).

**Regimen aplicable:** norma vigente al momento de la radicacion de la solicitud de revocatoria.

**Sobre fallos sancionatorios (Procuraduria, Personerias, Oficinas de Control Interno):**
- De oficio o a solicitud de parte
- Causal: infraccion manifiesta de normas constitucionales, legales o reglamentarias, o vulneracion de derechos fundamentales
- Solicitud formulada dentro de los 5 anos siguientes a la ejecutoria del fallo
- El sancionado puede solicitar por una unica vez, siempre que no hubiere interpuesto recursos ordinarios
- Procede aun cuando se haya acudido a la jurisdiccion contenciosa, siempre que no haya sentencia definitiva
- Termino para resolver: 6 meses

**Sobre fallos absolutorios o archivos por infracciones al DDHH y DIH:**
- De oficio o a peticion del quejoso, las victimas o perjudicados
- Solicitud dentro de los 4 meses siguientes al conocimiento de la decision
- Se informa al disciplinable para que se pronuncie dentro de los 10 dias siguientes
- Termino para resolver: 6 meses

**Efectos (Art. 146 CGD):** ni la peticion de revocatoria ni la decision que la resuelve reviven los terminos para ejercer medios de control contencioso administrativo. No da lugar a recurso ni a silencio administrativo.

---

## 11. MECANISMOS EXTRAPROCESALES

### 11.1 DERECHO DE PETICION
**Norma:** Art. 23 C.P. y Ley 1755 de 2015

Aplica para peticiones de quienes no son sujetos procesales. Las solicitudes de disciplinables y defensores se tramitan conforme al CGD dentro del proceso.

La respuesta debe observar:
- Los terminos de la Ley 1755 de 2015
- La reserva del Art. 115 CGD hasta la citacion a audiencia o pliego de cargos
- La proteccion de informacion reservada: defensa y seguridad nacional, privacidad, secretos comerciales, secreto profesional (Art. 24 Ley 1437/2011 y Ley 1712/2014)

**Implicacion de diseno:** el sistema debe generar alertas de vencimiento de terminos de respuesta a derechos de peticion y controlar automaticamente el nivel de reserva aplicable segun la etapa procesal del expediente.

### 11.2 ACCION DE TUTELA
**Norma:** Art. 86 C.P. y normas concordantes

Puede interponerse contra acciones u omisiones en relacion con el tramite disciplinario. El funcionario debe facilitar oportunamente los insumos necesarios a la Oficina Juridica de la Procuraduria para dar respuesta al juez que admitio la accion.

**Implicacion de diseno:** el sistema debe permitir la extraccion urgente de actuaciones especificas del expediente para respuesta a tutelas, con trazabilidad del acceso.

---

## 12. REQUISITOS TECNICOS

### 12.1 Arquitectura
- Modular y escalable: microservicios o serverless
- API-first: cada modulo expone servicios consumibles por otros sistemas
- Preparada para integracion con sistemas legacy de la entidad (DOKUS entre otros)

### 12.2 Seguridad
- Cifrado en transito y en reposo
- Logs inmutables de todas las acciones sobre el expediente
- Firma digital avanzada con sello de tiempo
- Control de acceso por roles y atributos (RBAC/ABAC)
- Principio de minimo privilegio
- Auditoria continua
- La separacion funcional instructor/juzgador reforzada a nivel de permisos: el sistema no puede permitir que el mismo usuario sea instructor y juzgador en el mismo expediente

### 12.3 Diseno UI/UX — Especificaciones Completas

#### 12.3.1 Sistema de color — Manual de Marca PGN (fuente oficial)

Los colores del sistema deben respetar estrictamente la composicion cromatica del Manual de Marca de la Procuraduria General de la Nacion. No se permite el uso de colores fuera de esta paleta salvo para estados semanticos de sistema (error, exito, advertencia) que deben derivarse de los colores institucionales.

**Colores principales:**

| Nombre | HEX | RGB | Pantone | Uso principal |
|---|---|---|---|---|
| Amarillo institucional | #FFE601 | R:255 G:230 B:0 | 803 C | Fondos de cabecera, acentos primarios, botones de accion principal, badges de estado activo |
| Azul marino institucional | #063853 | R:6 G:56 B:83 | 302 C | Texto principal sobre fondos claros, barras de navegacion, encabezados de seccion, iconos |

**Color secundario:**

| Nombre | HEX | RGB | Pantone | Uso |
|---|---|---|---|---|
| Rojo institucional | #E3201B | R:227 G:32 B:27 | 485 C | Alertas criticas, vencimiento de terminos, acciones destructivas, estados de error procesal |

**Colores terciarios:**

| Nombre | HEX | RGB | Pantone | Uso |
|---|---|---|---|---|
| Negro neutro | #131313 | R:19 G:19 B:19 | Negro neutro C | Texto de cuerpo, contenido de expedientes, documentos |
| Gris claro | #EDEDED | R:237 G:237 B:237 | P 169-3 U | Fondos de paneles secundarios, separadores, fondos de tabla |
| Gris medio | #949494 | R:148 G:148 B:148 | P 179-8 U | Texto deshabilitado, placeholders, metadatos secundarios |

**Colores complementarios:**

| Nombre | HEX | RGB | Pantone | Uso |
|---|---|---|---|---|
| Amarillo dorado | #FFC300 | R:255 G:195 B:0 | 7548 C | Iconos de advertencia, terminos proximos a vencer, estados intermedios |
| Azul medio | #074C84 | R:7 G:76 B:132 | 301 C | Links, acciones secundarias, estados informativos |
| Azul claro | #4DBFE2 | R:77 G:191 B:226 | 2985 C | Indicadores de progreso, estados de etapa activa, tooltips |
| Verde menta digital | #33FFCC | R:51 G:255 B:204 | — (solo digital) | Confirmaciones de exito, notificaciones enviadas, estados completados |

**Regla de contraste obligatoria (WCAG 2.1 AA):**
- Texto sobre amarillo #FFE601: usar azul marino #063853 (nunca negro puro ni blanco)
- Texto sobre azul marino #063853: usar blanco #FFFFFF o amarillo #FFE601
- Texto sobre rojo #E3201B: usar blanco #FFFFFF
- Texto sobre fondos blancos o grises claros: usar negro neutro #131313 o azul marino #063853
- Ratio minimo de contraste: 4.5:1 para texto normal, 3:1 para texto grande (18px+ o 14px bold)

---

#### 12.3.2 Tipografia — Manual de Marca PGN

**Fuentes institucionales principales (obligatorias):**

| Fuente | Variantes | Uso en el sistema |
|---|---|---|
| Montserrat | Regular, Bold, Black | Titulos de pagina, encabezados de seccion, etiquetas de campo, nombres de etapa procesal, botones |
| Poppins | Regular, Bold, Black | Texto de cuerpo, contenido de expedientes, descripciones, textos de ayuda contextual, tablas |

Ambas fuentes son de libre descarga (Google Fonts). El sistema debe cargarlas de forma local o desde CDN confiable para garantizar disponibilidad sin dependencia de internet externo.

**Escala tipografica del sistema:**

| Nivel | Fuente | Peso | Tamano | Uso |
|---|---|---|---|---|
| Display | Montserrat | Black | 32px | Titulos de modulo principal (ej: "Expediente #2024-001") |
| H1 | Montserrat | Bold | 24px | Titulos de pagina y seccion principal |
| H2 | Montserrat | Bold | 20px | Subtitulos de seccion, nombres de etapa |
| H3 | Montserrat | Bold | 16px | Encabezados de card, encabezados de tabla |
| Body | Poppins | Regular | 16px | Texto de contenido general |
| Body small | Poppins | Regular | 14px | Metadatos, fechas, numero de radicado, texto de tabla |
| Label | Montserrat | Bold | 12px | Etiquetas de campo de formulario, badges de estado |
| Caption | Poppins | Regular | 12px | Notas al pie, textos de ayuda contextual, timestamps |

**Interlineado:** 1.5 para cuerpo, 1.2 para titulos.  
**Espaciado de letras:** 0.02em para labels en mayusculas.

---

#### 12.3.3 Principios de diseno UI/UX

El sistema debe diseñarse para tres perfiles de usuario con necesidades muy distintas: el funcionario experto que usa el sistema diariamente y valora la velocidad, el usuario ocasional (disciplinado, quejoso, defensor) que puede no tener formacion tecnica, y el operador de segunda instancia que revisa expedientes completos. El diseno debe servir a los tres sin sacrificar a ninguno.

**Principio 1 — Revelacion progresiva (progressive disclosure)**

Mostrar solo la informacion necesaria para la accion inmediata. Los detalles adicionales se revelan bajo demanda. Aplicacion concreta:
- La vista de expediente muestra la etapa actual y las acciones disponibles. Los demas actos procesales se colapsan en un historial expandible.
- Los formularios de actos administrativos muestran primero los campos obligatorios. Los campos opcionales o de configuracion avanzada aparecen bajo un enlace "ver mas opciones".
- Las alertas de terminos muestran el vencimiento mas critico. El detalle completo de todos los terminos del expediente esta disponible en una vista secundaria.

**Principio 2 — Estado siempre visible**

El usuario debe saber en todo momento en que etapa esta el expediente, que acciones estan disponibles para su rol, y cuales son los proximos vencimientos. Aplicacion concreta:
- Indicador de etapa procesal fijo en la cabecera del expediente: nombre de la etapa, fecha de inicio, dias restantes del termino.
- Semaforo de terminos en cuatro niveles:

| Nivel | Dias restantes | Color | Comportamiento en UI |
|---|---|---|---|
| Normal | Mas de 30 dias | Verde — #33FFCC | Sin alerta activa. Solo visible en widget de terminos. |
| Advertencia | 15 a 30 dias | Amarillo — #FFE601 | Badge amarillo en la card del expediente. |
| Alerta | 5 a 14 dias | Naranja — #FFC300 | Banner en cabecera del expediente. Notificacion push al funcionario. |
| Critico | Menos de 5 dias o vencido | Rojo — #E3201B | Banner persistente. Correo automatico al funcionario y al superior. |

- El rol del usuario en ese expediente especifico debe ser explicito: "Estas actuando como INSTRUCTOR en este expediente". Nunca asumir que el usuario lo sabe.

**Principio 3 — Prevencion de errores sobre correccion de errores**

Es preferible que el sistema impida un error procesal antes que permitirlo y corregirlo despues. Aplicacion concreta:
- Deshabilitar visualmente (no ocultar) las acciones que no estan disponibles en la etapa actual o para el rol actual, con tooltip explicativo del motivo.
- Antes de actos irreversibles (cierre de instruccion, formulacion de pliego de cargos), mostrar un dialogo de confirmacion que enumere las consecuencias procesales: "Esta accion notificara a los sujetos procesales e iniciara el termino de 10 dias para alegatos precalificatorios. Esta accion no puede deshacerse. Confirmar?"
- Validacion en tiempo real de los campos de formulario con mensajes de error especificos: no "campo requerido" sino "debe ingresar la descripcion de la conducta segun Art. 222 num. 3 CGD".
- Controles de separacion funcional: si el usuario que intenta acceder a una accion de juzgamiento ya actuo como instructor en ese expediente, el sistema bloquea el acceso y muestra el motivo legal (Art. 12 CGD).

**Principio 4 — Consistencia y estandares**

Los mismos patrones visuales y de interaccion deben usarse para las mismas situaciones en todo el sistema. Aplicacion concreta:
- Los autos de sustanciacion siempre tienen el mismo formato de tarjeta: icono de tipo, numero de auto, fecha, funcionario que lo profirió, y boton de descarga.
- Las notificaciones electronicas siempre muestran: destinatario, fecha de envio, fecha de entendida (5 dias), y estado (pendiente / surtida).
- Los terminos siempre se expresan en dias habiles, con la fecha de vencimiento en calendario explicitamente, no solo el numero de dias.
- Las decisiones que admiten recurso siempre muestran el tipo de recurso disponible, el termino para interponerlo y el organo ante quien se interpone, inmediatamente despues de la notificacion.

**Principio 5 — Eficiencia para el usuario experto**

Los funcionarios que usan el sistema todos los dias no deben verse forzados a navegar multiples pantallas para completar acciones frecuentes. Aplicacion concreta:
- Accesos directos de teclado para las acciones mas comunes: nueva actuacion, buscar expediente, crear auto.
- Vista de bandeja de trabajo personalizada: lista de expedientes a cargo del funcionario ordenados por urgencia de termino, con acciones rapidas desde la lista sin necesidad de abrir el expediente.
- Plantillas reutilizables para actos administrativos frecuentes (auto de apertura, auto de cierre, pliego de cargos) con campos pre-llenados segun el expediente.
- Busqueda global rapida por numero de radicado, nombre del disciplinado o numero de expediente accesible desde cualquier pantalla con atajo de teclado.
- Historial de expedientes recientes en la barra lateral.

**Principio 6 — Accesibilidad como requisito, no como optativo**

El sistema debe cumplir WCAG 2.1 nivel AA sin excepcion. Aplicacion concreta:
- Todos los campos de formulario tienen etiqueta visible asociada mediante `<label>`. No usar solo placeholder como etiqueta.
- Todos los iconos funcionales tienen texto alternativo o aria-label descriptivo.
- El sistema es completamente operable con teclado: Tab para navegar, Enter para confirmar, Escape para cancelar dialogos.
- Los mensajes de error y de estado son anunciados por lectores de pantalla mediante aria-live regions.
- El semaforo de terminos nunca comunica el estado solo mediante color: incluye siempre un icono y texto descriptivo.
- Tamano minimo de area tactil en movil: 44x44 px.

**Principio 7 — Diseno institucional sin sacrificar usabilidad**

La identidad visual de la Procuraduria debe ser reconocible en toda interfaz del sistema, pero sin que el cumplimiento de la marca deteriore la experiencia de uso. Aplicacion concreta:
- El amarillo #FFE601 se usa para acentos, cabeceras y acciones principales, no como fondo de areas de contenido extenso (dificulta la lectura).
- El azul marino #063853 es el color dominante en barras de navegacion, encabezados y texto, generando la percepcion institucional sobria y seria.
- El logotipo de la PGN aparece en la barra de navegacion superior izquierda y en los documentos generados por el sistema, en su version horizontal sobre fondo blanco o sobre fondo amarillo segun el contexto.
- El rojo #E3201B se reserva exclusivamente para estados criticos y alertas. No usarlo como color decorativo ni en botones de accion positiva.

---

#### 12.3.4 Patrones de interaccion especificos del EED

**Card de expediente — estructura y estados:**

Cada expediente en la bandeja de trabajo se representa como una card con la siguiente estructura:

```
+--------------------------------------------------+
| EXP-2026-001234                      [campana]   |  <- Header azul #063853, texto blanco
+--------------------------------------------------+
| Quejoso:      [Nombre del quejoso]               |
| Disciplinado: [Cargo y entidad]                  |
| Etapa:        [Badge color segun estado]         |
| Termino:      [Barra de progreso] 67%            |
| Vence:        [Indicador de dias con semaforo]   |
|                                                  |
| [Ver expediente]          [Actuar]               |  <- Botones
+--------------------------------------------------+
```

**Estados visuales de la card:**

| Estado | Tratamiento visual |
|---|---|
| Pendiente de evaluacion | Borde izquierdo amarillo #FFE601 |
| En curso — en termino | Borde izquierdo azul medio #074C84 |
| Proximo a vencer | Borde izquierdo naranja #FFC300 + badge de alerta |
| Vencido | Fondo rojo muy suave (10% opacidad #E3201B) + icono critico |
| Completado / archivado | Opacidad 60%, sin acciones activas |
| Inhibido | Gris claro #EDEDED, etiqueta "Inhibido" |

**Widget de control de terminos:**

```
+----------------------------------------------+
|  Termino de Investigacion                    |
|  [=============================-------] 67%  |  <- Barra de progreso
|                                              |
|  Inicio:      15-Mar-2026                    |
|  Vencimiento: 15-Sep-2026                    |
|  Faltan:      45 dias habiles                |
|                                              |
|  [Solicitar prorroga]                        |
+----------------------------------------------+
```

La barra de progreso usa el color del nivel de semaforo activo. El boton "Solicitar prorroga" solo aparece cuando el tipo de termino admite prorroga segun el CGD y cuando el usuario tiene el rol para solicitarla.

**Modales de confirmacion — estructura:**

- Overlay semi-transparente con blur sobre el contenido
- Header azul #063853 con titulo del acto y articulo del CGD
- Cuerpo: resumen claro de las consecuencias procesales en lenguaje preciso
- Dos botones: cancelar (secundario) y confirmar (acento o peligro segun la accion)
- Cierre: boton X, tecla ESC, o clic fuera del modal
- Animacion: slide-in desde arriba, 200ms

**Selectores y controles especializados:**

- Date picker con logica de dias habiles colombianos integrada. No permite seleccionar sabados, domingos ni festivos nacionales. Muestra automaticamente la fecha de vencimiento calculada al seleccionar la fecha de inicio.
- Dropdown de funcionarios con buscador integrado y filtro por rol y dependencia.
- Multi-select con chips visuales para seleccion de sujetos procesales a notificar.
- Toggle switches para activar/desactivar notificaciones por canal (electronica, correo, push).

**Vista de expediente — estructura recomendada:**

La pantalla principal del expediente se divide en tres zonas:
- Zona superior fija: identificador del expediente, nombre del disciplinado (con mascara si aplica reserva), etapa actual, semaforo de terminos, rol del usuario en el expediente.
- Zona lateral izquierda: indice de etapas del proceso como linea de tiempo vertical. La etapa activa esta resaltada en azul medio #074C84. Las etapas completadas en gris medio. Las futuras en gris claro.
- Zona central de contenido: actos procesales de la etapa activa, acciones disponibles para el rol, documentos vinculados. Esta zona es la unica con scroll.

**Formulario de acto procesal:**

- Titulo del auto en la parte superior con el articulo del CGD que lo fundamenta.
- Campos agrupados por tematica, no listados uno detras de otro.
- Panel lateral derecho fijo con el resumen de datos del expediente (numero, disciplinado, etapa, funcionario) para que el usuario no pierda contexto mientras llena el formulario.
- Boton de guardar borrador siempre visible. El sistema guarda automaticamente cada 30 segundos con indicador visual discreto.
- El boton de "firmar y notificar" solo se activa cuando todos los campos obligatorios estan completos y validados. Su color es amarillo #FFE601 con texto azul marino #063853.

**Notificaciones del sistema:**

- Notificaciones criticas (vencimiento de termino en menos de 3 dias, accion requerida urgente): banner rojo persistente en la parte superior de la pantalla. No desaparece hasta que el usuario lo cierra o resuelve la accion.
- Notificaciones de advertencia (termino entre 3 y 10 dias): banner amarillo temporal de 8 segundos, con enlace al expediente correspondiente.
- Notificaciones de confirmacion (acto guardado, notificacion enviada): toast verde menta #33FFCC en esquina inferior derecha, 4 segundos.
- Notificaciones informativas (nuevo acto en expediente a cargo): icono de campana en navbar con contador. No interrumpe el flujo de trabajo.

**Dashboard de trabajo del funcionario:**

- Panel principal: expedientes a cargo ordenados por urgencia de termino (los mas criticos primero).
- Cada fila de expediente muestra: numero, disciplinado (con reserva si aplica), etapa actual, dias restantes del termino activo con semaforo, y dos acciones rapidas.
- Filtros persistentes: por etapa, por tipo de proceso, por urgencia, por fecha de asignacion.
- Indicadores de carga de trabajo: numero de expedientes activos, promedio de dias de termino restante, expedientes con termino vencido.

---

#### 12.3.5 Responsive y dispositivos

El sistema debe funcionar correctamente en los siguientes contextos, en orden de prioridad:

| Contexto | Resolucion | Consideraciones |
|---|---|---|
| Escritorio institucional | 1366x768 a 1920x1080 | Pantalla principal de uso diario. Layout de tres columnas. |
| Tablet | 768px a 1024px | Consulta de expedientes en sala de audiencia. Layout de dos columnas. |
| Movil | 360px a 767px | Consulta y firma en campo. Layout de una columna. Solo funciones criticas. |

En movil, las acciones de creacion de actos administrativos complejos quedan deshabilitadas con mensaje explicativo. Solo se habilitan: consulta de expediente, consulta de terminos, firma de documentos pendientes, y notificaciones.

---

#### 12.3.6 Modo de acceso para usuarios externos (disciplinados, quejosos, defensores)

El portal externo tiene un diseno distinto al panel interno pero comparte la misma identidad visual. Sus principios especificos:
- Lenguaje ciudadano, no juridico. Donde se use terminologia legal, incluir definicion en tooltip o glosa.
- Flujo de consulta en maximo 3 pasos desde la pagina de inicio hasta la informacion del proceso.
- El estado del proceso se muestra como una linea de tiempo visual en lenguaje simple: "Su queja fue recibida", "Su queja esta siendo evaluada", "Se abrio investigacion", etc.
- Indicar claramente que informacion esta disponible segun la etapa de reserva del Art. 115 CGD, con explicacion del motivo en lenguaje comprensible.
- Descarga de documentos notificados en un solo clic, sin necesidad de navegar a subsecciones.

### 12.4 Interoperabilidad
- Cumplimiento de estandares de Gobierno Digital (STI)
- Exportacion en PDF/A y XML
- Integracion con DOKUS
- Integracion con plataforma de firma digital
- Notificaciones electronicas validas juridicamente (Art. 122 CGD)
- Reporte a SIRI, SCC y SECOP II cuando aplique

### 12.5 Funcionalidades clave
- Calculo automatico de terminos procesales con alertas de vencimiento, caducidad y prescripcion
- Control de reserva de la actuacion por etapa procesal (Art. 115 CGD)
- Generacion inteligente de actos administrativos (autos, resoluciones, fallos)
- Control de procedencia de recursos por tipo de auto y etapa
- Gestion de impedimentos y recusaciones con suspension automatica de terminos
- Busqueda avanzada con OCR sobre documentos digitalizados y metadatos
- Dashboard de indicadores de gestion: tiempos por etapa, carga de trabajo, tipos de falta, estado de expedientes
- Modulo de gestion de derechos de peticion con alertas de vencimiento
- Registro de revocatorias directas como proceso separado vinculado al expediente original

---

## 13. ROLES DEL SISTEMA Y MATRIZ DE PERMISOS

### 13.1 Roles definidos

**1. Administrador del sistema**
- Gestion de usuarios, roles y perfiles
- Configuracion de parametros del sistema (calendario de dias habiles, plantillas)
- Acceso a auditoria completa del sistema
- Backup, restauracion y monitoreo

**2. Procurador Delegado — Instructor**
- Evaluar noticias disciplinarias
- Proferir decision inhibitoria, apertura de indagacion o investigacion
- Decretar y practicar pruebas en instruccion
- Formular pliego de cargos
- Archivar investigaciones
- No puede actuar como juzgador en el mismo expediente (control RBAC automatico)

**3. Procurador Delegado — Juzgador**
- Avocar conocimiento del expediente para juzgamiento
- Fijar tipo de juicio (ordinario o verbal) y audiencias
- Decretar pruebas en juzgamiento
- Proferir fallo de primera instancia
- Resolver nulidades en juzgamiento
- No puede actuar como instructor en el mismo expediente (control RBAC automatico)

**4. Secretario Juridico**
- Radicar noticias disciplinarias y asignar numero de expediente
- Notificar actos administrativos y registrar trazabilidad
- Gestionar comunicaciones al quejoso
- Expedir copias autorizadas
- Controlar y alertar sobre vencimientos de terminos

**5. Analista Disciplinario**
- Apoyar en practica de pruebas
- Elaborar proyectos de actos administrativos
- Seguimiento y actualizacion de estado de expedientes
- No tiene facultad de decision

**6. Superior Jerarquico**
- Resolver recursos de apelacion y queja de sus subordinados
- Decidir impedimentos y recusaciones
- Consultar expedientes de las dependencias a cargo
- Revisar y confirmar o revocar decisiones

**7. Disciplinado**
- Consultar su expediente (vista limitada segun etapa y reserva del Art. 115 CGD)
- Presentar descargos y version libre
- Solicitar y aportar pruebas
- Interponer recursos (reposicion, apelacion, queja)
- Aceptar cargos o confesar con beneficios
- Recibir notificaciones electronicas

**8. Defensor**
- Acceder al expediente completo del disciplinado que representa
- Presentar descargos y solicitar pruebas
- Interponer recursos en nombre del disciplinado
- Recibir notificaciones

**9. Quejoso**
- Radicar la noticia disciplinaria
- Consultar estado del expediente (vista muy limitada — solo estado y etapa, sujeta a reserva)
- Recibir comunicaciones del Art. 129 CGD
- Interponer recurso de apelacion contra archivos cuando corresponda (Art. 110 paragrafo CGD)
- Solicitar revocatoria en casos DDHH/DIH cuando aplique

### 13.2 Matriz de permisos

| Funcion | Admin | Instructor | Juzgador | Secretario | Analista | Superior | Disciplinado | Defensor | Quejoso |
|---|---|---|---|---|---|---|---|---|---|
| Radicar noticia | S | S | S | S | N | N | N | N | S |
| Asignar expediente | S | N | N | S | N | N | N | N | N |
| Evaluar noticia | N | S | N | N | S (apoyo) | N | N | N | N |
| Proferir inhibitorio | N | S | N | N | N | N | N | N | N |
| Abrir indagacion / investigacion | N | S | N | N | N | N | N | N | N |
| Decretar pruebas instruccion | N | S | N | N | N | N | N | N | N |
| Presentar descargos | N | N | N | N | N | N | S | S | N |
| Aportar pruebas | N | N | N | N | N | N | S | S | N |
| Formular pliego de cargos | N | S | N | N | N | N | N | N | N |
| Avocar juzgamiento | N | N | S | N | N | N | N | N | N |
| Decretar pruebas juzgamiento | N | N | S | N | N | N | N | N | N |
| Proferir fallo | N | N | S | N | N | N | N | N | N |
| Notificar actos | N | N | N | S | S (apoyo) | N | N | N | N |
| Interponer recursos | N | N | N | N | N | N | S | S | S (limitado) |
| Resolver apelacion / queja | N | N | N | N | N | S | N | N | N |
| Resolver impedimento / recusacion | N | N | N | N | N | S | N | N | N |
| Consultar expediente completo | S | S (propio) | S (propio) | S | S | S (dependencia) | Limitado | Completo del representado | Limitado |
| Expedir copias | S | S | S | S | S | S | S (autorizadas) | S | N |
| Archivar definitivo | N | S | N | N | N | N | N | N | N |
| Configurar sistema | S | N | N | N | N | N | N | N | N |
| Ver auditoria | S | N | N | N | N | S (parcial) | N | N | N |

**Regla critica de separacion funcional (Art. 12 CGD):** el sistema verifica automaticamente que el usuario que intenta asumir el rol de juzgador en un expediente no haya actuado previamente como instructor en ese mismo expediente. Si hay conflicto, el acceso se bloquea con mensaje explicativo del fundamento legal y se registra el intento en el log de auditoria.

---

## 14. ESPECIFICACIONES TECNICAS

### 14.1 Arquitectura

- Arquitectura modular de microservicios o serverless
- API RESTful — API-first: cada modulo expone servicios consumibles por otros sistemas
- Preparada para integracion con sistemas legacy de la entidad (ORFEO entre otros)
- Frontend: framework moderno (React, Vue o Angular — definir segun capacidad del equipo de TI de la entidad)
- Backend: Node.js, Python o Java — con soporte transaccional robusto
- Base de datos: relacional con soporte transaccional (PostgreSQL recomendado)

### 14.2 Autenticacion y seguridad

- Autenticacion: OAuth 2.0 con tokens JWT
- Cifrado en reposo: AES-256
- Cifrado en transito: TLS 1.3
- Firma digital avanzada con sello de tiempo certificado
- Logs inmutables de auditoria — toda accion sobre un expediente queda registrada con usuario, fecha, hora y IP
- Control de acceso RBAC/ABAC con separacion funcional reforzada a nivel de sistema
- Principio de minimo privilegio: cada rol solo accede a lo estrictamente necesario
- Backup automatico y plan de recuperacion ante desastres

### 14.3 Interoperabilidad

- Cumplimiento de estandares de Gobierno Digital colombiano (STI)
- Exportacion en PDF/A y XML con firma digital embebida
- Integracion con ORFEO (sistema de gestion documental)
- Integracion con plataforma de firma digital institucional
- Notificaciones electronicas validas juridicamente (Art. 122 CGD) con acuse de recibo certificado
- Reporte a SIRI y SCC para registro de sanciones ejecutoriadas
- SECOP II cuando aplique

### 14.4 Funcionalidades tecnicas clave

**Modulo 1 — Gestion de expedientes:**
- Creacion automatica de expediente y asignacion de numero de radicado desde la radicacion de la noticia
- Numeracion consecutiva institucional configurable por dependencia y anio
- Clasificacion por tipo de falta, etapa, competencia y estado
- Busqueda avanzada con OCR sobre documentos digitalizados y metadatos
- Historial completo e inmutable de actuaciones

**Modulo 2 — Control de terminos:**
- Calculo automatico de terminos procesales en dias habiles (calendario colombiano con festivos actualizables)
- Alertas progresivas en cuatro niveles (ver seccion 12.3.3)
- Gestion de prorrogas con validacion de procedencia segun el CGD
- Suspension automatica de terminos al proferir impedimento o recusacion
- Notificaciones automaticas por vencimiento al funcionario y al superior
- Alertas de caducidad y prescripcion

**Modulo 3 — Generacion de actos administrativos:**
- Plantillas predefinidas por tipo de acto (auto de apertura, auto de cierre, pliego de cargos, fallo, entre otros)
- Autocompletado de datos del expediente en la plantilla
- Validacion de requisitos legales del acto antes de permitir la firma (ej: verificar que el pliego contenga los 9 elementos del Art. 222 CGD)
- Numeracion automatica de autos
- Firma digital integrada con sello de tiempo

**Modulo 4 — Notificaciones:**
- Notificacion personal con acuse de recibo (Art. 121 CGD)
- Notificacion electronica con autorizacion previa escrita (Art. 122 CGD)
- Notificacion por edicto con publicacion digital (Art. 127 CGD)
- Notificacion en estrados con registro de audiencia
- Comunicacion al quejoso (Art. 129 CGD)
- Trazabilidad completa de cada notificacion: envio, entrega y fecha de entendida

**Modulo 5 — Pruebas:**
- Gestion del decreto y practica de pruebas por tipo (testimonial, documental, pericial, inspeccion)
- Control de traslado de dictamenes periciales con plazos automaticos
- Procedimiento de testigo renuente con generacion automatica del auto de multa
- Objecion del dictamen pericial con flujo de decision
- Registro de cadena de custodia de pruebas documentales

**Modulo 6 — Recursos:**
- Registro de interposicion de recursos (reposicion, apelacion, queja) con control de termino para interponerlos
- Flujo automatico de traslado al superior cuando el recurso se concede
- Seguimiento del tramite del recurso con alertas de termino para decidir
- Registro de la decision del superior y sus efectos sobre el expediente

**Modulo 7 — Dashboard e indicadores de gestion:**
- Expedientes activos por etapa, funcionario y dependencia
- Tiempos promedio de resolucion por etapa y tipo de proceso
- Expedientes proximos a vencer (por nivel de alerta)
- Expedientes con termino vencido sin decision
- Tipos de faltas mas frecuentes
- Tasa de confirmacion y revocacion en segunda instancia
- Carga de trabajo por funcionario
- Exportacion de estadisticas en Excel y PDF

---

## 15. PROMPT DE DISENO ITERATIVO — INSTRUCCIONES PARA IA DE DISENO

Esta seccion es un prompt listo para pasarle a una IA de diseno (como Claude, Figma AI, v0, o similar) para que construya el sistema pantalla por pantalla de forma iterativa. La IA debe trabajar un paso a la vez, mostrar el resultado, preguntar antes de continuar y nunca asumir decisiones de diseno sin validacion.

---

### PROMPT BASE — PEGAR AL INICIO DE CADA SESION DE DISENO


Eres un disenador UI/UX senior especializado en sistemas de gestion documental institucional para entidades del Estado colombiano.

Vas a disenar el Expediente Electronico Disciplinario (EED) de la Procuraduria General de la Nacion, paso a paso, una pantalla o componente a la vez.

REGLAS DE TRABAJO OBLIGATORIAS:
1. Disenamos un elemento a la vez. Nunca avances al siguiente sin que yo lo apruebe.
2. Antes de disenar cualquier pantalla, hazme las preguntas necesarias para entender exactamente que necesito. Maximo 2 o 3 preguntas por ronda.
3. Cuando presentes un diseno, explica brevemente las decisiones que tomaste y por que.
4. Despues de cada entrega pregunta: "Que quieres ajustar antes de continuar?"
5. No uses colores, tipografias ni componentes fuera de las especificaciones de marca que te doy a continuacion.
6. Si algo del requerimiento es ambiguo desde el punto de vista juridico-procesal, señalalo antes de disenar, no despues.
7. Nunca uses datos reales de personas o procesos. Usa siempre datos ficticios de ejemplo.

IDENTIDAD VISUAL — OBLIGATORIA:
Colores principales:
- Azul marino institucional: #063853 — navegacion, encabezados, botones primarios
- Amarillo institucional: #FFE601 — acentos, boton de accion positiva (firmar, confirmar), badges activos
- Rojo: #E3201B — alertas criticas, vencimientos, acciones destructivas

Colores de soporte:
- Negro texto: #131313
- Gris claro fondos: #EDEDED
- Gris medio deshabilitado: #949494
- Azul medio links: #074C84
- Azul claro informativo: #4DBFE2
- Naranja advertencia: #FFC300
- Verde exito: #33FFCC

Tipografia:
- Montserrat: titulos, encabezados, labels, botones
- Poppins: cuerpo de texto, tablas, descripciones, ayuda contextual

Semaforo de terminos procesales (4 niveles):
- Verde #33FFCC: mas de 30 dias restantes
- Amarillo #FFE601: 15 a 30 dias
- Naranja #FFC300: 5 a 14 dias
- Rojo #E3201B: menos de 5 dias o vencido

Botones:
- Primario: fondo #063853, texto blanco, borde-radius 6px, Montserrat 600
- Secundario: borde 2px #063853, fondo transparente, texto #063853
- Acento (firmar/confirmar): fondo #FFE601, texto #063853, Montserrat 700
- Peligro: fondo #E3201B, texto blanco
- Deshabilitado: fondo #EDEDED, texto #949494, cursor not-allowed

Accesibilidad obligatoria: WCAG 2.1 AA — contraste minimo 4.5:1, navegacion por teclado, labels ARIA, no comunicar estado solo con color.

CONTEXTO DEL SISTEMA:
El EED gestiona el proceso disciplinario de la Procuraduria bajo la Ley 1952 de 2019 modificada por la Ley 2094 de 2021. Tiene 9 roles de usuario: Administrador, Instructor, Juzgador, Secretario Juridico, Analista, Superior Jerarquico, Disciplinado, Defensor y Quejoso. La separacion funcional entre Instructor y Juzgador es un requisito legal (Art. 12 CGD) que debe reforzarse a nivel de interfaz — un usuario no puede ver ni ejecutar acciones del otro rol en el mismo expediente.

Cuando estes listo, dime: "Listo. Por donde empezamos?" y yo te dire que pantalla o componente disenar primero.
```

---

### ORDEN SUGERIDO DE PANTALLAS Y COMPONENTES

Seguir este orden garantiza que cada pantalla construya sobre la anterior. Sin embargo, la consultora puede alterar el orden segun prioridad del proyecto. La IA nunca debe avanzar sin instruccion explicita.

**Bloque 1 — Estructura base y navegacion**

Paso 1.1 — Login institucional
- Campos: usuario, contrasena, entidad
- Logo PGN, fondo azul marino, formulario centrado
- Manejo de error de credenciales
- Preguntar: que metodo de autenticacion usa la entidad actualmente?

Paso 1.2 — Shell de la aplicacion (estructura fija)
- Barra de navegacion superior: logo, nombre del sistema, nombre del usuario, rol activo, notificaciones, cerrar sesion
- Barra lateral izquierda: menu de modulos segun rol
- Zona de contenido principal
- Preguntar: la barra lateral debe estar siempre visible o colapsa en algunas vistas?

Paso 1.3 — Sistema de notificaciones (campana)
- Panel desplegable con lista de alertas por nivel (critico primero)
- Badge con contador en el icono
- Tipos: vencimiento critico, accion requerida, nuevo acto en expediente propio, asignacion de expediente

**Bloque 2 — Dashboard del funcionario interno**

Paso 2.1 — Bandeja de trabajo (vista principal del funcionario)
- Lista de expedientes a cargo ordenados por urgencia de termino
- Semaforo de terminos en cada fila
- Filtros: por etapa, por urgencia, por tipo de proceso, por fecha de asignacion
- Acciones rapidas desde la lista sin abrir el expediente
- Preguntar: cuantos expedientes maneja en promedio un funcionario?

Paso 2.2 — Indicadores de gestion (panel superior del dashboard)
- Expedientes activos totales
- Con termino vencido
- Proximos a vencer (menos de 5 dias)
- Promedio de dias de resolucion por etapa
- Preguntar: quieres que estos indicadores sean globales o solo del funcionario que inicio sesion?

Paso 2.3 — Card de expediente (componente reutilizable)
- Numero de radicado, nombre del disciplinado (con mascara si hay reserva), etapa, semaforo de termino, acciones rapidas
- Estados visuales: pendiente, en curso, proximo a vencer, vencido, archivado, inhibido

**Bloque 3 — Radicacion de la noticia disciplinaria**

Paso 3.1 — Formulario de radicacion
- Tipo de noticia (queja, informe, oficio, otro)
- Datos del quejoso (con opcion de anonimo con soporte)
- Descripcion de los hechos
- Datos del posible disciplinado (si se conocen)
- Carga de documentos adjuntos
- Preguntar: el quejoso puede radicar en linea directamente o solo lo hace el secretario en nombre del quejoso?

Paso 3.2 — Confirmacion de radicacion y asignacion de numero
- Resumen del expediente creado
- Numero de radicado asignado
- Instrucciones al quejoso sobre seguimiento
- Generacion automatica del acuse de recibo

**Bloque 4 — Vista del expediente**

Paso 4.1 — Cabecera del expediente (zona fija superior)
- Identificador, estado, etapa actual, semaforo de termino, rol del usuario en este expediente
- Acciones disponibles segun rol y etapa (visibles y deshabilitadas si no aplican)

Paso 4.2 — Linea de tiempo procesal (zona lateral izquierda)
- Etapas del proceso como timeline vertical
- Etapa activa resaltada, completadas en gris, futuras en gris claro
- Clic en etapa completada muestra sus actos en la zona central

Paso 4.3 — Panel de actos procesales (zona central de contenido)
- Lista de actos de la etapa activa con tipo, fecha, funcionario y estado
- Boton para crear nuevo acto segun tipo de etapa y rol
- Descarga de cada acto en PDF

Paso 4.4 — Widget de control de terminos
- Barra de progreso del termino activo
- Fecha de inicio, fecha de vencimiento, dias habiles restantes
- Boton de solicitud de prorroga (visible solo si el termino la admite y el rol puede solicitarla)

**Bloque 5 — Formularios de actos procesales**

Paso 5.1 — Auto de apertura de investigacion (Art. 215 CGD)
- Campos: identidad del autor, hechos relevantes, pruebas a decretar, beneficios de la confesion
- Validacion de los 7 elementos obligatorios del Art. 215 antes de habilitar la firma
- Panel lateral con resumen del expediente siempre visible

Paso 5.2 — Pliego de cargos (Arts. 222-223 CGD)
- Campos para los 9 elementos obligatorios del Art. 222
- Checklist de validacion: el boton de firmar no se activa hasta que los 9 elementos esten completos
- Vista previa del documento antes de firmar

Paso 5.3 — Auto de cierre de investigacion (Art. 220 CGD)
- Dialogo de confirmacion con las consecuencias procesales explicadas
- Calculo automatico del termino de traslado de 10 dias para alegatos precalificatorios
- Preguntar: el sistema debe generar automaticamente la comunicacion de traslado o el secretario la gestiona manualmente?

Paso 5.4 — Fallo de primera instancia
- Tipo (sancionatorio / absolutorio)
- Contenido diferenciado segun tipo
- Vista previa antes de firmar
- Calculo automatico del termino para interponer recurso de apelacion (10 dias)

**Bloque 6 — Modulo de notificaciones**

Paso 6.1 — Panel de notificaciones pendientes
- Lista de actos pendientes de notificar por secretario
- Tipo de notificacion requerida segun el acto (personal, electronica, edicto, estrados)
- Estado: pendiente, enviada, surtida (con fecha de entendida)

Paso 6.2 — Flujo de notificacion electronica
- Seleccion de destinatarios
- Confirmacion de canal autorizado previamente por escrito
- Envio y registro del acuse de recibo
- Calculo automatico de la fecha de entendida (5 dias habiles)

Paso 6.3 — Registro de edicto
- Formulario de publicacion digital
- Fecha de fijacion y fecha de desfijacion
- Generacion del acta de notificacion por edicto

**Bloque 7 — Portal externo (disciplinados, defensores, quejosos)**

Paso 7.1 — Pagina de inicio del portal ciudadano
- Lenguaje simple, sin jerga juridica
- Opciones: consultar expediente, radicar queja, ver estado de mi proceso
- Preguntar: el portal externo requiere registro previo o solo numero de radicado?

Paso 7.2 — Vista de estado del proceso (ciudadano)
- Linea de tiempo en lenguaje simple: "Su queja fue recibida", "Esta siendo evaluada", etc.
- Indicacion clara de que informacion no esta disponible por reserva (Art. 115 CGD) con explicacion en lenguaje comprensible
- Documentos notificados disponibles para descarga

Paso 7.3 — Presentacion de descargos (disciplinado / defensor)
- Formulario de texto libre con carga de documentos adjuntos
- Control del termino disponible para presentar
- Confirmacion de radicacion con numero de registro

**Bloque 8 — Componentes transversales**

Paso 8.1 — Modal de confirmacion de actos irreversibles
- Estructura estandar para cualquier accion sin retorno
- Titulo del acto, articulo del CGD que lo fundamenta
- Lista de consecuencias procesales en lenguaje claro
- Botones: cancelar (secundario) y confirmar (acento o peligro)

Paso 8.2 — Widget de impedimentos y recusaciones
- Formulario de declaracion de impedimento
- Suspension automatica del termino del expediente afectado
- Flujo de remision al superior

Paso 8.3 — Buscador global
- Busqueda por numero de radicado, nombre, cedula del disciplinado
- Accesible desde cualquier pantalla con atajo de teclado
- Resultados con preview de estado y etapa

---


## 16. GLOSARIO DE TERMINOS

| Termino | Definicion |
|---|---|
| Auto | Decision interlocutoria proferida durante el proceso que no pone fin a la instancia |
| Fallo | Decision de fondo que pone fin al proceso en una instancia |
| Pliego de cargos | Acto que formula cargos concretos contra el disciplinado — equivale a la acusacion |
| Descargos | Defensa presentada por el disciplinado frente a los cargos formulados |
| Ejecutoria | Momento en que el fallo queda en firme por no haberse interpuesto recursos o por haberse agotado |
| Ruptura de unidad procesal | Separacion del expediente en dos o mas procesos independientes por confesion parcial, prueba sobreviniente o fuero |
| Termino procesal | Plazo legal establecido en el CGD para realizar una actuacion o proferir una decision |
| Sujetos procesales | El investigado, su defensor, el quejoso (en algunos casos) y el Ministerio Publico cuando actua como sujeto procesal |
| Cosa juzgada | Efectos que impiden juzgar a una persona dos veces por el mismo hecho con identidad de sujeto, conducta y fundamento normativo |
| DDHH | Derechos Humanos |
| DIH | Derecho Internacional Humanitario |
| DIDH | Derecho Internacional de los Derechos Humanos |
| Notificacion personal | Forma de poner en conocimiento una decision mediante contacto directo con el sujeto procesal (Art. 121 CGD) |
| Notificacion electronica | Notificacion enviada al correo o canal electronico autorizado previamente por escrito (Art. 122 CGD) |
| Notificacion por edicto | Forma de notificacion publica cuando no se logra la notificacion personal (Art. 127 CGD) |
| Comunicacion | Acto mediante el cual se informa al quejoso de las decisiones sin que sea sujeto procesal formal (Art. 129 CGD) |
| Notificacion en estrados | Notificacion que se surte en la misma audiencia, con efectos inmediatos |
| Poder preferente | Facultad de la PGN o la Personeria de asumir el conocimiento de asuntos de otras entidades disciplinarias |
| Confesion | Manifestacion expresa del disciplinado de su responsabilidad que genera beneficios de reduccion de sancion |
| Doble conformidad | Derecho del disciplinado a que un fallo sancionatorio de segunda instancia sea revisado por una autoridad diferente |
| Revocatoria directa | Mecanismo extraordinario de competencia exclusiva del Procurador General para revocar fallos sancionatorios o absolutorios |
| Ruptura de termino de prescripcion | Interrupcion del termino de prescripcion que ocurre con la notificacion del fallo de primera instancia |
| SIRI | Sistema de Informacion de Registro de Sanciones e Inhabilidades |
| SCC | Sistema de Control y Comunicacion de la Procuraduria |
| ORFEO | Sistema de Gestion Documental utilizado por la Procuraduria |
| RBAC | Control de Acceso Basado en Roles (Role-Based Access Control) |
| ABAC | Control de Acceso Basado en Atributos (Attribute-Based Access Control) |

---

## 17. REGLAS DEL ASISTENTE

El asistente actua como co-disenador tecnico-juridico senior. Las siguientes reglas son de obligatorio cumplimiento:

### Comportamiento

- Priorizar la validez procesal, la seguridad juridica y el cumplimiento normativo sobre la innovacion tecnologica
- Trabajar paso a paso sin saltar etapas. Validar cada propuesta antes de asumir que es definitiva
- Si hay ambiguedad, hacer preguntas concretas antes de proponer soluciones
- Citar siempre el articulo del CGD o la norma aplicable cuando se mencionen etapas, plazos, garantias o actos procesales
- Verificar con el texto oficial vigente antes de afirmar un requisito procesal
- Proponer alternativas tecnicas con pros y contras, nunca una unica opcion rigida
- Equilibrar precision legal con factibilidad de implementacion
- Las propuestas deben estar listas para presentarse a equipos tecnicos y juridicos de la entidad

### Formato de respuesta
- Sin emojis en respuestas tecnicas
- Si se propone codigo o arquitectura, indicar nivel de madurez: POC, prototipo o produccion
- Mantener ejemplos con datos ficticios. Nunca solicitar ni usar informacion real de procesos

### Limites
- No emitir dictamenes juridicos vinculantes. Indicar cuando se requiere revision del area juridica de la Procuraduria o de la Oficina de Control Interno
- No asumir requisitos de seguridad sin validar con las politicas de TI de la entidad
- Evitar jerga tecnica innecesaria; si se usa, explicar brevemente
- Mantener confidencialidad absoluta. No almacenar ni simular datos reales de procesos disciplinarios

---

## 18. REGISTRO DE DECISIONES VALIDADAS

| Fecha | Categoria | Decision | Norma / Justificacion | Estado |
|---|---|---|---|---|
| 2026-04-18 | Modelo de datos | El expediente se crea siempre al radicarse la noticia, independientemente del resultado posterior. Lo que varia es el tipo y estado del expediente (Inhibido, Trasladado, Con actuacion). No existen dos entidades raiz separadas. | Correccion validada por consultora — 2026-04-20 | Validado |
| 2026-04-18 | Juridico / Flujo | La inhibicion (Art. 209) si genera radicado y expediente. Lo que no genera es investigado vinculado ni actuacion disciplinaria. El expediente queda cerrado en estado Inhibido. Contra la decision no procede recurso; solo se comunica al quejoso. | Art. 209 Ley 1952 de 2019 — correccion validada 2026-04-20 | Validado |
| 2026-04-18 | Tecnico / Juridico | La separacion funcional instructor/juzgador debe reforzarse a nivel de permisos del sistema (RBAC), no solo de procedimiento. | Art. 12 CGD mod. Ley 2094 de 2021 | Validado |
| 2026-04-20 | Flujo | Se incorpora el flujo oficial completo del CGD: evaluacion de la noticia, traslado por competencia, impedimentos, indagacion previa con sus terminos y recursos, investigacion con terminos y medidas preventivas, juicio ordinario y verbal con sus diferencias, segunda instancia, doble conformidad, revocatoria directa y mecanismos extraprocesales. | Flujo oficial PGN — Ley 1952/2019 y Ley 2094/2021 | Validado |
| 2026-04-20 | Tecnico | Se agrega control automatico de reserva de la actuacion por etapa procesal y modulo de gestion de derechos de peticion con alertas de vencimiento. | Art. 115 CGD y Ley 1755 de 2015 | Validado |
| 2026-04-20 | UX/UI | Sistema de color completo del Manual de Marca PGN con usos definidos por contexto. Alertas progresivas de terminos en 4 niveles con dias especificos: >30 normal, 15-30 advertencia, 5-14 alerta, <5 critico. | Manual de Marca PGN + Instrucciones.md | Validado |
| 2026-04-20 | UX/UI | Tipografia: Montserrat + Poppins. Escala tipografica completa. CSS de botones (primario, secundario, acento, peligro, deshabilitado). Card de expediente con estados visuales. Widget de terminos con barra de progreso. | Manual de Marca PGN + Instrucciones.md | Validado |
| 2026-04-20 | UX/UI | 7 principios UX con aplicacion concreta. Estructura de 3 zonas para vista de expediente. Sistema de notificaciones por nivel de criticidad. Dashboard. Responsive. Portal externo ciudadano. | Manual de Marca PGN + buenas practicas UX | Validado |
| 2026-04-20 | Tecnico / Roles | Se definen 9 roles del sistema con sus acciones especificas y la matriz de permisos completa. Se confirma el control RBAC automatico para separacion funcional instructor/juzgador. | Art. 12 CGD mod. Ley 2094/2021 + Instrucciones.md | Validado |
| 2026-04-20 | Tecnico | Se incorpora stack tecnico: OAuth 2.0 + JWT, AES-256, TLS 1.3. Se detallan 7 modulos funcionales del sistema. Plan de implementacion en 6 fases de 32 semanas. | Instrucciones.md — Oficina Control Interno Disciplinario | Validado |
| 2026-04-20 | Juridico | Se incorpora glosario completo de terminos disciplinarios y tecnicos del sistema. | Consolidacion del proyecto | Validado |

---

## 19. PROXIMOS TEMAS A DESARROLLAR

- Modelo de datos completo: entidad Expediente con todos sus atributos, relaciones y estados posibles
- Motor de calculo de terminos: logica de dias habiles, festivos, prorrogas y suspension por impedimentos
- Plantillas de actos administrativos: estructura y campos requeridos por tipo de auto con validacion legal
- Integracion con DOKUS: protocolo de intercambio, campos mapeados, flujo de sincronizacion
- Integracion con SIRI y SCC: estructura del reporte, frecuencia, campos obligatorios de la sancion
- Diseno del portal externo para disciplinados, defensores y quejosos: flujos por rol
- Modelo de auditoria e inmutabilidad de logs: estructura del log, politica de retencion, acceso
- Control de reserva dinamica (Art. 115 CGD): reglas de visibilidad por etapa y perfil
- Definicion del numero de radicado: serie unica o diferenciada para expedientes inhibidos
- Especificaciones de accesibilidad WCAG 2.1 AA: checklist por componente

