# CancerLiver AI 🩺🤖

> **Proyecto de Prácticas - Gestión de Proyectos Software (`33681`)**  
> 4º Curso - Grado en Ingeniería en Inteligencia Artificial  
> Escuela Politécnica Superior (EPS) - Universidad de Alicante (Curso 2026/2027)  
> **Grupo de Prácticas:** Grupo B  

---

## 📋 Descripción del Proyecto

**CancerLiver AI** es un sistema de soporte a la decisión clínica (CDSS) basado en Inteligencia Artificial multimodal (modelos de visión computacional y modelos de lenguaje a gran escala - LLMs) diseñado para asistir a profesionales médicos en el cribado, detección y diagnóstico precoz del cáncer de hígado a partir de imágenes médicas (TAC/CT, Resonancia Magnética/MRI y ecografías).

El proyecto se desarrolla bajo el rol de una consultora/empresa tecnológica especializada en IA y software biomédico, abordando todas las fases de gestión, estimación, planificación, aseguramiento de la calidad, cumplimiento regulatorio y arquitectura técnica.

---

## 🚀 Capacidades y Funcionalidades Principales

1. **Ingesta y Preprocesamiento Multiformato:** Compatibilidad con formatos médicos estándar (**DICOM**) y convencionales (PNG, JPEG), incluyendo normalización y realce de contraste de tejidos.
2. **Análisis Automatizado con Visión por Computador:** Redes neuronales convolucionales / Vision Transformers entrenados para la detección, localización y segmentación de lesiones hepáticas.
3. **Estratificación del Riesgo y Explicabilidad:** Clasificación del caso en 4 niveles estandarizados:
   - 🟢 *Riesgo Bajo*
   - 🟡 *Riesgo Moderado*
   - 🟠 *Riesgo Alto*
   - 🔴 *Presencia Confirmada*  
   Acompañado de una justificación clínica textual generada por el agente inteligente.
4. **Módulo Conversacional Asistido por LLM:** Interfaz en lenguaje natural que permite al facultativo realizar preguntas clínicas, contrastar hallazgos y solicitar explicaciones en texto libre.
5. **Historial Clínico y Almacenamiento Estructurado:** Persistencia segura de estudios anteriores, métricas evolutivas y trazabilidad por paciente.
6. **Generación Automática de Informes Clínicos (PDF):** Exportación de reportes detallados con imágenes anotadas, mapas de calor/segmentación y veredicto del sistema.
7. **Control de Accesos y Gestión de Roles:** Panel de administración con segregación de privilegios (médico general, especialista oncológico, radiólogo, administrador de sistemas).
8. **Auditoría, Trazabilidad y Seguridad:** Registro inmutable de cada consulta, inferencia y validación humana para cumplir con la legislación sanitaria vigente.

---

## ⚖️ Marco Regulatorio y Restricciones

- **Protección de Datos:** Cumplimiento estricto del Reglamento General de Protección de Datos (**RGPD**) y de la **LOPDGDD** (Tratamiento de categorías especiales de datos de salud - Art. 9 RGPD).
- **Entorno Hospitalario:** Requisitos no funcionales de alta disponibilidad (99.9%), resiliencia frente a caídas y ciberseguridad avanzada.
- **Normativa de Dispositivos Médicos y Software Sanitario:** Consideración de los estándares **ISO 13485**, **IEC 62304** (ciclo de vida de software médico) y directrices de marcado CE / FDA para software como dispositivo médico (SaMD).

---

## 📁 Estructura del Repositorio

```text
GPS-Proyecto-B/
├── .gitignore
├── README.md
├── docs/                      # Documentación modular del proyecto
│   ├── README.md              # Índice de entregables
│   ├── 01-requisitos/         # Punto 1: Objetivos, Canvas, RF, RNF, Restricciones
│   ├── 02-costes/             # Punto 2: Estimación de costes y esfuerzo
│   ├── 03-riesgos/            # Punto 3: Análisis y gestión de riesgos
│   ├── 04-rrhh/               # Punto 4: Estructura de equipo
│   ├── 05-agenda/             # Punto 5: WBS, precedencias y MS Project
│   └── actas/                 # Registro de reuniones y decisiones
├── res/                       # Materiales y plantillas oficiales del profesorado
│   ├── 1_Funcionalidades.pdf
│   ├── CANVAS SCRUM Y ESTRUCTURA ORGANIZATIVA.pdf
│   ├── Enunciado_Practicas_GP.pdf
│   └── planning.doc
└── src/                       # Prototipos, scripts y pipelines técnicos
```

---

## 📅 Cronograma de Entregas y Evaluación

| Semana | Hito / Entregable | Fecha Límite | Estado |
| :---: | :--- | :---: | :---: |
| **S4** | **Punto 1:** Objetivos, Lean Canvas, Requerimientos Funcionales/No Funcionales y Restricciones | 02/10/2026 | 🟡 En progreso |
| **S6** | Estimación de costes y presupuesto inicial (Parkinson, Pricing to Win, Puntos Objeto) | 16/10/2026 | ⚪ Pendiente |
| **S8** | Plan de proyecto general y detallado (WBS, Gantt en MS Project - 2 iteraciones) | 30/10/2026 | ⚪ Pendiente |
| **S10** | Plan de RRHH (organigrama empresa IA) y Plan de Gestión de Riesgos | 13/11/2026 | ⚪ Pendiente |
| **S12** | Plan de monitorización y control (Métricas y EVM - Valor Ganado) | 27/11/2026 | ⚪ Pendiente |
| **S13** | 🗣️ Presentación y defensa oral del plan de proyecto (15% evaluación) | 01/12/2026 / 03/12/2026 | ⚪ Pendiente |
| **S16** | Análisis normativo legal (RGPD/LOPD, IP) y propuesta de arquitectura | 23/12/2026 | ⚪ Pendiente |

---

## 👥 Equipo de Desarrollo (Grupo B)

- **Equipo:** 5 integrantes (Grado en Ingeniería en Inteligencia Artificial).
- **Metodología:** Ágil (Scrum) con adaptación a entornos biomédicos regulados.

---

## 🛠️ Flujo de Trabajo Git

1. **Ramas principales:**
   - `main`: Versión estable y entregables consolidados.
   - `develop`: Integración continua de trabajo en curso.
   - `feature/<nombre>`: Desarrollo de secciones o funcionalidades específicas.
2. **Convención de Commits:** [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `docs:`, `fix:`, `chore:`).
