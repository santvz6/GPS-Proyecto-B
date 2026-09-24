# 1. Introducción y Especificación de Requisitos

> **Proyecto:** CancerLiver AI  
> **Asignatura:** Gestión de Proyectos Software (`33681`) - Curso 2026/2027  
> **Documento base:** Bloque 1 de `res/planning.doc` y directrices de `res/1_Funcionalidades.pdf`  

---

## 1.1. Objetivos Generales

### Visión General y Contexto
**CancerLiver AI** es un sistema de soporte a la decisión clínica (CDSS - *Clinical Decision Support System*) enfocado en el diagnóstico precoz del carcinoma hepatocelular (cáncer de hígado). Integra modelos de Visión por Computador para la detección y segmentación de lesiones hepáticas a partir de estudios de imagen médica (TAC/CT, MRI y ecografías), junto con un módulo conversacional basado en Modelos de Lenguaje a Gran Escala (LLM) que asiste al especialista médico en la interpretación y emisión de informes clínicos.

### Objetivos desde la Perspectiva del Usuario (Profesional Médico y Hospitales)
1. **Reducción de tiempos de diagnóstico:** Minimizar el tiempo de cribado de estudios radiológicos voluminosos (series TAC multicorte) de horas a segundos.
2. **Disminución de falsos negativos:** Servir como segunda opinión diagnóstica algorítmica para detectar microlesiones hepáticas que pasan inadvertidas en estadios tempranos.
3. **Explicabilidad diagnóstica:** Proporcionar mapas de calor visuales (Grad-CAM) y justificaciones clínicas textuales para fundamentar cada alerta.
4. **Agilidad en la consulta:** Resolver dudas clínicas sobre el caso en tiempo real mediante un asistente conversacional interactivo.
5. **Automatización burocrática:** Generar informes clínicos normalizados en PDF con un solo clic.

### Objetivos desde la Perspectiva de los Desarrolladores (Empresa de Software e IA)
1. **Pipeline de inferencia robusto:** Procesamiento normalizado de volúmenes DICOM, PNG y JPEG con latencia predecible.
2. **Cumplimiento regulatorio estricto:** Diseñar la arquitectura técnica bajo directrices **RGPD/LOPDGDD** (datos especialmente protegidos) y estándares sanitarios (**IEC 62304**, **ISO 13485**).
3. **Trazabilidad y reproducibilidad:** Auditoría inmutable de versiones de modelo, pesos, hiperparámetros e inferencias clínicas emitidas.
4. **Interoperabilidad hospitalaria:** Integración futura con sistemas PACS/RIS vía protocolos DICOM/HL7/FHIR.

### Funcionalidades Diferenciales
- **Explicabilidad Multimodal Bidireccional:** Asociación de la región anatómica segmentada en la imagen con la justificación redactada por el LLM.
- **RAG Clínico (Retrieval-Augmented Generation):** El LLM fundamenta sus respuestas contrastando la analítica del paciente con guías clínicas internacionales de hepatología (EASL, AASLD, NCCN).
- **Semáforo de Riesgo Cuatripartito:** Clasificación directa en cuatro niveles estandarizados con umbrales de incertidumbre explícitos.

---

## 1.2. Lean Canvas (Modelo de Negocio Sanitario)

| Bloque | Descripción |
| :--- | :--- |
| **1. Problema** | • Detección tardía del cáncer hepático (altas tasas de mortalidad).<br>• Sobrecarga laboral extrema de los servicios de radiología y oncología.<br>• Falta de herramientas explicativas que justifiquen las decisiones de IA diagnóstica. |
| **2. Segmento de Clientes** | • **Compradores:** Hospitales privados, mutuas y redes hospitalarias públicas.<br>• **Prescriptores:** Jefes de servicio de Radiología y Oncología Hepática.<br>• **Early Adopters:** Oncólogos y radiólogos jóvenes de clínicas privadas de diagnóstico avanzado. |
| **3. Proposición de Valor Única** | *"Segunda opinión diagnóstica en cáncer de hígado en segundos, con explicabilidad visual y justificación clínica interactiva en lenguaje natural."* |
| **4. Solución** | • Pipeline automático de segmentación y detección de lesiones hepáticas (CV).<br>• Asistente conversacional clínico (LLM) con respaldo documental.<br>• Sistema de alerta de riesgo en 4 niveles con generación de informe PDF. |
| **5. Canales** | • Venta consultiva directa B2B a gerencias hospitalarias.<br>• Congresos médicos y sociedades científicas (SERAM, SEOM, EASL).<br>• Alianzas con proveedores de hardware radiológico (Siemens Healthineers, Philips, GE). |
| **6. Estructura de Costes** | • Ensayos clínicos y validación diagnóstica con comités éticos.<br>• Certificación regulatoria (Marcado CE como Producto Sanitario SaMD, ISO 13485, FDA).<br>• Computación Cloud de GPU (entrenamiento e inferencia segura).<br>• Nóminas de equipo técnico e ingenieros biomédicos. |
| **7. Flujo de Ingresos** | • Licenciamiento SaaS B2B anual por volumen de estaciones de trabajo hospitalarias.<br>• Pago por uso (coste por estudio/TAC analizado en la nube médica).<br>• Servicios profesionales de integración PACS/RIS y soporte 24/7. |
| **8. Métricas Clave** | • Sensibilidad y especificidad diagnóstica (AUC-ROC > 0.95 en microlesiones).<br>• Tiempo medio de análisis por estudio (< 15 segundos).<br>• Tasa de adopción/aceptación médica de las sugerencias del agente (> 85%). |
| **9. Ventaja Diferencial** | • Arquitectura híbrida patentable que enlaza segmentación 3D médica con RAG asistido sobre guías oncológicas actualizadas. |

---

## 1.3. Requerimientos Funcionales (RF)

| Identificador | Bloque Funcional | Subfuncionalidad | Descripción Detallada |
| :---: | :--- | :--- | :--- |
| `ING-DICOM` | Ingesta de Imágenes | Ingesta estándar DICOM | Recepción, validación de cabeceras de metadatos clínicos y lectura de imágenes DICOM multicorte. |
| `ING-CONV` | Ingesta de Imágenes | Ingesta formatos comunes | Carga y preprocesado de imágenes convencionales (PNG, JPEG) preservando resolución nativa. |
| `PRE-NORM` | Preprocesamiento | Normalización y filtrado | Normalización de escala de grises (unidades Hounsfield en TAC), reducción de ruido y realce de contraste de parénquima hepático. |
| `VIS-DETEC` | Visión Artificial | Detección de lesiones | Detección automática y delimitación mediante bounding boxes de áreas sospechosas compatibles con nódulos o tumores. |
| `VIS-SEGM` | Visión Artificial | Segmentación volumétrica | Segmentación píxel a píxel / vóxel a vóxel del contorno de la lesión hepática para cálculo de volumen y geometría. |
| `VIS-HEAT` | Visión Artificial | Mapa de explicabilidad | Generación de mapa de calor (Grad-CAM) superpuesto a la imagen médica para indicar los puntos clave de activación del modelo. |
| `RIE-CLAS` | Estratificación | Clasificación de riesgo | Asignación automática de uno de los 4 niveles: **Riesgo Bajo**, **Riesgo Moderado**, **Riesgo Alto** o **Presencia Confirmada**. |
| `RIE-JUST` | Estratificación | Justificación diagnóstica | Generación automática de texto estructurado justificando la categoría de riesgo en base a parámetros biomédicos y volumétricos. |
| `LLM-CHAT` | Módulo LLM | Consulta en texto libre | Interfaz conversacional para que el facultativo realice preguntas clínicas abiertas sobre el estudio evaluado. |
| `LLM-RAG` | Módulo LLM | Contrastación documental | Recuperación de fragmentos de guías clínicas oficiales para justificar recomendaciones farmacológicas o de seguimiento. |
| `HIS-REG` | Historial Clínico | Registro de pacientes | Almacenamiento estructurado de ficha paciente, histórico de análisis, imágenes previas y evolución temporal de nódulos. |
| `HIS-CONS` | Historial Clínico | Búsqueda y filtrado | Motor de búsqueda de estudios por identificador anonimizado de paciente, fecha, nivel de riesgo o médico evaluador. |
| `INF-GEN` | Generación Informes | Generación informe PDF | Compilación automática en un documento PDF con datos del estudio, imagen anotada, mapa de calor, veredicto y justificación. |
| `INF-DESC` | Generación Informes | Firma y exportación | Descarga digital del informe PDF preparado para inserción en historia clínica electrónica o firma digital médica. |
| `SEC-AUTH` | Seguridad y Accesos | Autenticación y roles | Control de acceso seguro (RBAC) con perfiles diferenciados: Médico General, Oncólogo Especialista, Radiólogo y Administrador. |
| `SEC-ANON` | Seguridad y Accesos | Anonimización previa | Eliminación automática de datos de identificación directa en imágenes antes del procesado por los modelos de IA. |
| `AUD-TRAZ` | Auditoría | Registro inmutable de logs | Trazabilidad completa de cada petición, inferencia devuelta, fecha/hora, usuario emisor y confirmación médica. |

---

## 1.4. Requerimientos No Funcionales (RNF)

| Identificador | Categoría | Subrequerimiento | Descripción Detallada |
| :---: | :--- | :--- | :--- |
| `RNF-PERF-01` | Rendimiento | Tiempo de inferencia | El procesamiento completo de una serie de imágenes (hasta 100 cortes) no superará los **15 segundos** en servidor con aceleración GPU. |
| `RNF-PERF-02` | Rendimiento | Concurrencia | El backend soportará al menos **50 peticiones simultáneas** sin degradación de rendimiento superior al 10%. |
| `RNF-DISP-01` | Disponibilidad | Alta disponibilidad hospitalaria | El sistema garantizará una disponibilidad mínima del **99.9%** (tiempo de inactividad no planificado inferior a 8.7 horas al año). |
| `RNF-SEGU-01` | Seguridad | Cifrado en tránsito y reposo | Comunicaciones securizadas mediante TLS 1.3 y cifrado de base de datos e imágenes en reposo mediante AES-256. |
| `RNF-SEGU-02` | Seguridad | Cumplimiento RGPD/LOPDGDD | Tratamiento estricto de datos de categoría especial (Art. 9 RGPD), con arquitectura *Privacy by Design* y disociación de identificadores. |
| `RNF-USAB-01` | Usabilidad | Diseño intuitivo médico | Interfaz gráfica usable sin formación técnica especializada; navegación y acceso al informe en menos de **3 clics**. |
| `RNF-INTE-01` | Interoperabilidad | Estándares médicos | Cumplimiento del estándar DICOM 3.0 para ingesta de archivos y preparación para intercambio HL7 / FHIR. |
| `RNF-RELI-01` | Fiabilidad | Robustez frente a fallos | En caso de caída de un nodo de procesamiento de IA, las peticiones en cola se redirigirán automáticamente sin pérdida de datos. |
| `RNF-DOCU-01` | Soporte | Manuales y documentación | Disponibilidad de Manual de Usuario Clínico, Guía de Despliegue para TI hospitalario y especificación de API técnica. |

---

## 1.5. Restricciones del Proyecto

1. **Restricción de Recursos Humanos:** Equipo de desarrollo fijado en **5 integrantes** con dedicación correspondiente a la carga lectiva del cuatrimestre.
2. **Restricción Temporal:** Calendario cerrado de entregas académicas, culminando con la presentación final en diciembre de 2026.
3. **Restricción Presupuestaria:** Proyecto inicial modelado bajo entorno de simulación académica, requiriendo estimación formal mediante Ley de Parkinson, Pricing to Win y Puntos Objeto.
4. **Restricción Regulatoria y Legal:** Imposibilidad de salida al mercado sin certificación como Producto Sanitario (Software as a Medical Device - SaMD) bajo Reglamento Europeo de Productos Sanitarios (MDR) y normativas IEC 62304 / ISO 13485.
5. **Restricción de Infraestructura Hospitalaria:** Los hospitales imponen firewalls restrictivos, políticas de almacenamiento *on-premise* o nubes médicas dedicadas (prohibición de enviar datos médicos a APIs públicas de IA sin acuerdo BAA/DPA).
