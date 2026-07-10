# UT-AI Lab Platform

## Plataforma de Modelado, Simulación e Inteligencia Artificial para Procesos Químicos y Mantenimiento 4.0

**UT-AI Lab Platform** es una plataforma modular orientada a docencia, investigación aplicada y desarrollo tecnológico en Universidades Tecnológicas y Politécnicas. Su primera versión se enfoca en el modelado y simulación de procesos químicos, con una arquitectura preparada para integrar posteriormente mantenimiento 4.0, análisis de sensores, asistentes RAG, generación de reportes técnicos, HMIs didácticas y aplicaciones especializadas con inteligencia artificial.

El objetivo inicial no es construir una plataforma masiva desde el primer día, sino un sistema funcional, documentado y reproducible que permita demostrar el ciclo:

```text
Proyecto académico-industrial
→ Modelo de proceso químico
→ Simulación
→ Resultados
→ Reporte técnico
→ Consulta inteligente de documentación
```

---

## 1. Propósito del proyecto

El proyecto busca crear una plataforma institucional de bajo costo para que profesores y alumnos puedan:

- crear proyectos de modelado y simulación;
- registrar modelos de procesos químicos;
- ejecutar simulaciones numéricas;
- visualizar resultados;
- generar reportes técnicos;
- documentar prácticas, antologías, manuales y resultados;
- consultar la documentación del proyecto mediante un asistente RAG;
- extender la plataforma hacia mantenimiento predictivo, gemelos digitales, HMIs didácticas y aplicaciones con IA.

---

## 2. Alcance del MVP 1

El **MVP 1** se enfoca exclusivamente en procesos químicos y simulación.

### Incluido en el MVP 1

- Backend con FastAPI.
- Base de datos PostgreSQL.
- Modelado de entidades con SQLModel.
- Creación y consulta de proyectos.
- Registro de modelos de proceso.
- Simulación inicial de un CSTR isotérmico con reacción de primer orden.
- Almacenamiento local de resultados.
- Generación inicial de reportes técnicos en Markdown.
- Estructura preparada para RAG, mantenimiento 4.0 y HMI.

### No incluido todavía

- Visión artificial.
- YOLO.
- Etiquetado de imágenes.
- Anotadores visuales.
- Gemelos digitales 3D.
- Integración real con PLC o SCADA.
- Usuarios y permisos avanzados.
- MinIO o almacenamiento institucional.
- Kubernetes.
- Entrenamiento de modelos pesados.

---

## 3. Caso de uso inicial

El caso de uso inicial es un **reactor continuo de tanque agitado isotérmico** o CSTR, usado ampliamente en cursos de modelado, simulación y control de procesos.

Modelo base:

```text
A → B

 dCA/dt = (F/V)(CAin - CA) - k CA
 dCB/dt = -(F/V)CB + k CA
```

Donde:

- `CA` es la concentración del reactivo A;
- `CB` es la concentración del producto B;
- `CAin` es la concentración de entrada;
- `F` es el flujo volumétrico;
- `V` es el volumen del reactor;
- `k` es la constante de reacción;
- `t` es el tiempo de simulación.

---

## 4. Arquitectura inicial

```text
[Frontend Streamlit - futuro inmediato]
          |
          v
[FastAPI Backend]
          |
          ├── PostgreSQL
          |
          ├── Local Storage
          |     └── data/projects/{project_id}/...
          |
          ├── Process Modeling Module
          |     ├── CSTR model
          |     ├── tank model
          |     └── future process units
          |
          ├── Simulation Module
          |     ├── numerical solver
          |     ├── result storage
          |     └── plots/exports
          |
          ├── Reports Module
          |     └── Markdown/HTML reports
          |
          ├── RAG Module - planned
          |     ├── document loading
          |     ├── embeddings
          |     └── semantic search
          |
          └── Maintenance 4.0 Module - planned
                ├── CSV sensor upload
                ├── signal features
                └── fault diagnosis
```

---

## 5. Tecnologías

### Backend

- Python
- FastAPI
- SQLModel
- PostgreSQL
- Uvicorn

### Simulación y datos

- NumPy
- Pandas
- SciPy, en fases posteriores
- Matplotlib, para reportes y gráficas

### Frontend

- Streamlit en la primera etapa
- React opcional en versiones posteriores

### IA y RAG, en fases posteriores

- Ollama local
- Gemini API opcional
- OpenAI API opcional
- pgvector o Qdrant
- LangChain o LlamaIndex

### Despliegue

- Docker
- Docker Compose
- GitHub
- GitHub Actions

---

## 6. Estructura del repositorio

```text
ut-ai-lab-platform/
│
├── app/
│   ├── api/
│   │   ├── projects.py
│   │   ├── process_models.py
│   │   ├── simulations.py
│   │   ├── reports.py
│   │   └── documents.py
│   │
│   ├── core/
│   │   ├── config.py
│   │   └── paths.py
│   │
│   ├── database/
│   │   ├── session.py
│   │   └── models.py
│   │
│   ├── modeling/
│   │   ├── cstr.py
│   │   └── tank.py
│   │
│   ├── simulation/
│   │   └── simulation_service.py
│   │
│   ├── reports/
│   │   └── report_service.py
│   │
│   ├── rag/
│   │   ├── loader.py
│   │   ├── indexer.py
│   │   └── query_engine.py
│   │
│   ├── maintenance/
│   │   ├── csv_loader.py
│   │   ├── signal_features.py
│   │   └── diagnosis.py
│   │
│   └── main.py
│
├── frontend/
│   └── streamlit_app.py
│
├── data/
│   ├── projects/
│   ├── simulations/
│   ├── reports/
│   └── documents/
│
├── docs/
│   ├── informe_tecnico.md
│   ├── architecture.md
│   ├── roadmap.md
│   ├── bitacora_desarrollo.md
│   └── manual_usuario.md
│
├── examples/
│   ├── cstr/
│   ├── tank_level/
│   └── maintenance_motor_ac/
│
├── tests/
│   └── test_health.py
│
├── docker-compose.yml
├── Dockerfile
├── requirements.txt
├── README.md
└── .github/
    └── workflows/
        └── python-ci.yml
```

---

## 7. Endpoints iniciales

### Salud del sistema

```text
GET /health
```

### Proyectos

```text
POST /api/projects
GET  /api/projects
GET  /api/projects/{project_id}
```

### Modelos de proceso

```text
POST /api/projects/{project_id}/process-models
GET  /api/projects/{project_id}/process-models
```

### Simulación

```text
POST /api/projects/{project_id}/simulations/cstr
GET  /api/projects/{project_id}/simulations
GET  /api/projects/{project_id}/simulations/{simulation_id}
```

### Reportes

```text
POST /api/projects/{project_id}/reports/generate
GET  /api/projects/{project_id}/reports
```

### Documentos y RAG, planeado

```text
POST /api/projects/{project_id}/documents/upload
POST /api/projects/{project_id}/rag/index
POST /api/projects/{project_id}/rag/query
```

---

## 8. Roadmap

### Fase 1: Base de plataforma

- Crear estructura del repositorio.
- Configurar FastAPI.
- Configurar PostgreSQL.
- Crear modelos de base de datos.
- Crear endpoints de proyectos.
- Crear endpoint de simulación CSTR.
- Guardar resultados en JSON.

### Fase 2: Reportes técnicos

- Generar reportes Markdown.
- Agregar gráficas.
- Exportar resultados.
- Documentar simulaciones.

### Fase 3: Frontend didáctico

- Crear interfaz con Streamlit.
- Permitir creación de proyectos desde frontend.
- Permitir edición de parámetros.
- Visualizar curvas de concentración.

### Fase 4: RAG académico-técnico

- Subir documentos.
- Indexar prácticas, manuales, antologías y reportes.
- Consultar documentación mediante asistente.
- Responder con fuentes.

### Fase 5: Mantenimiento 4.0

- Subir CSV de vibración, corriente o temperatura.
- Extraer características.
- Clasificar condiciones.
- Generar diagnóstico técnico.

### Fase 6: Generación de aplicaciones

- Generar HMIs didácticas.
- Crear apps especializadas por proyecto.
- Crear asistentes de práctica.
- Integrar LLM provider layer.

---

## 9. Ejecución local

### 1. Clonar el repositorio

```bash
git clone https://github.com/usuario/ut-ai-lab-platform.git
cd ut-ai-lab-platform
```

### 2. Crear entorno virtual

```bash
python -m venv .venv
```

En Windows:

```powershell
.\.venv\Scripts\activate
```

En Linux/Mac:

```bash
source .venv/bin/activate
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

### 4. Levantar PostgreSQL

```bash
docker compose up -d
```

### 5. Ejecutar API

```bash
uvicorn app.main:app --reload
```

### 6. Abrir documentación automática

```text
http://127.0.0.1:8000/docs
```

---

## 10. Estado actual

```text
Versión: 0.1.0
Estado: diseño e implementación inicial del MVP 1
Módulo principal: modelado y simulación de procesos químicos
Caso inicial: CSTR isotérmico con reacción de primer orden
```

---

## 11. Valor académico y profesional

Este proyecto puede documentarse como:

- desarrollo tecnológico;
- plataforma institucional;
- evidencia de arquitectura de software;
- evidencia de integración de IA aplicada;
- herramienta de apoyo docente;
- base para proyectos de investigación aplicada;
- evidencia profesional para perfiles AI Software Engineer.

El desarrollo se documenta mediante:

- README;
- informe técnico;
- arquitectura;
- bitácora;
- manual de usuario;
- pruebas funcionales;
- ejemplos reproducibles;
- reportes generados por la plataforma.

---

## 12. Licencia

Pendiente de definir.

Opciones sugeridas:

- MIT, para apertura y reutilización amplia.
- Apache 2.0, si se busca una licencia abierta con protección explícita de patentes.
- Licencia institucional, si la universidad requiere control formal del desarrollo.
