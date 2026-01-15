# AI-EduResearch: A research and learning support platform powered by Artificial Intelligence and Machine Learning models

[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org) [![Django](https://img.shields.io/badge/Django-5.1-092E20?style=for-the-badge&logo=django&logoColor=white)](https://djangoproject.com) [![Angular](https://img.shields.io/badge/Angular-18-DD0031?style=for-the-badge&logo=angular&logoColor=white)](https://angular.io) [![License](https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge)](LICENSE)

This documentation describes the architecture and capabilities of the **AI-EduResearch** platform, a system designed to automate the scientific research lifecycle using advanced Natural Language Processing and Deep Learning models.

> **Project Status:** Active Development - Enterprise Edition
> **Focus:** Automated Surveys, Topic Modeling (ECRTM), and Knowledge Graphs.

---

## 👨‍💻 Engineering Profile

**AI-EduResearch Team | Advanced NLP & Machine Learning**

**Demonstrated expertise:**

- 🏗️ **Scalable Architecture**: Modular Django-based backend with clear separation of concerns.
- 🤖 **Deep Learning**: Custom implementation of ECRTM (Embedded Clustering and Topic Modeling).
- 🧠 **Large Language Models**: Zero-shot labeling and content synthesis using OpenAI GPT-4o.
- 📊 **Scientific Visualization**: Dynamic Knowledge Graph generation via NetworkX and Plotly.
- 📄 **Automated Reporting**: LaTeX-based PDF engine for academic-grade survey generation.
- ⚛️ **Modern Frontend**: Responsive Single Page Application (SPA) built with Angular 18.

---

## 🎯 Problem & Solution

### The Challenge

Scientific researchers face an exponential growth in published literature. Manually searching repositories (DOAJ, PLOS), filtering relevant papers, identifying latent topics, and writing "State of the Art" surveys is a time-consuming and error-prone process that scales poorly.

### The Solution: AI-EduResearch

**An autonomous research assistant** that:

- **Aggregates** literature from multiple open-access repositories (DOAJ, PLOS) and local libraries.
- **Analyzes** semantic content using neural topic models (ECRTM) to discover hidden thematic structures.
- **Synthesizes** findings into structured narratives.
- **Generates** publication-ready PDF reports with proper citations and vector graphics.
- **Visualizes** knowledge landscapes through interactive graphs.

### ✨ Key Features

- **🚀 Automated Literature Review**: Fetches and processes hundreds of papers in minutes.
- **🧠 Zero-Shot Topic Labeling**: Uses GPT-4o to assign meaningful, human-readable labels to abstract topic clusters.
- **🕸️ Dynamic Knowledge Graphs**: Interactive, physics-based visualization of research topics and their relationships.
- **📄 Print-Ready PDFs**: Generates academic-standard surveys using a robust LaTeX engine.
- **🔐 Enterprise Security**: Multi-tenant architecture with Firebase Authentication and JWT validation.
- **📈 Advanced Analytics**: Deep learning-based metrics for topic coherence and distribution.

---

## 🏗️ System Architecture

### High-Level Data Flow

The system follows a linear pipeline architecture, processing raw unstructured data into structured knowledge artifacts.

```
┌──────────────────────────────────────────────────────────┐
│  CLIENT (Angular 18 + Firebase Auth)                     │
└────────────────────┬─────────────────────────────────────┘
                     │ HTTPS / JSON + JWT
┌────────────────────▼─────────────────────────────────────┐
│  AI-EduResearch GATEWAY (Django REST Framework)          │
│  ┌────────────────────────────────────────────────────┐  │
│  │ 1. Data Ingestion (Recoleccion_datos)              │  │
│  │    - DOAJ API Client                               │  │
│  │    - PLOS API Client                               │  │
│  │    - Local PDF Uploads                             │  │
│  └──────────────────────┬─────────────────────────────┘  │
│                         │ Raw Metadata + PDFs            │
│  ┌──────────────────────▼─────────────────────────────┐  │
│  │ 2. Preprocessing Engine (preprocesamiento)         │  │
│  │    - Text Normalization                            │  │
│  │    - Academic Stopword Removal                     │  │
│  │    - Fixed-size Chunking Strategy                  │  │
│  └──────────────────────┬─────────────────────────────┘  │
│                         │ Cleaned Tokenized Text         │
│  ┌──────────────────────▼─────────────────────────────┐  │
│  │ 3. Deep Learning Core (Deep_Learning)              │  │
│  │    - Embedding Generation (FastText)               │  │
│  │    - ECRTM Training (Neural Topic Modeling)        │  │
│  │    - Label Inference (GPT-4o Integration)          │  │
│  └──────────────────────┬─────────────────────────────┘  │
│                         │ Topics, Keywords, Probabilities│
│  ┌──────────────────────▼─────────────────────────────┐  │
│  │ 4. Synthesis & Reporting (creacion_pdf / diagrama) │  │
│  │    - Knowledge Graph Construction (NetworkX)       │  │
│  │    - LaTeX Template Rendering                      │  │
│  │    - PDF Compilation (pdflatex)                    │  │
│  └────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure & File Reference

### 🎯 Core Logic Breakdown (Backend)

The backend is structured into distinct applications, each responsible for a specific stage of the research pipeline.

#### `Backend/Recoleccion_datos/` - Data Ingestion Layer

| File | Purpose |
|------|---------|
| `views.py` | **API Gateway**: Handles `upload_files` and `buscar_articulos_endpoints`. Validates input and delegates to services. |
| `services.py` | **Business Logic**: Manages file storage, duplication checks, and interacts with external APIs (DOAJ/PLOS). |
| `logic.py` | **Search Algorithms**: Implements the search strategy, including query normalization and result aggregation. |

#### `Backend/preprocesamiento/` - NLP Pipeline

| File | Purpose |
|------|---------|
| `logic.py` | **Text Processor**: Implements `dividir_en_secciones` (chunking) and `analyze_and_preprocess` (normalization). Uses Regex for cleaning execution. |
| `views.py` | **Execution Handler**: Endpoint trigger for the preprocessing pipeline. |

#### `Backend/Deep_Learning/` - Neural Topic Modeling (The Brain)

| File | Purpose |
|------|---------|
| `logic.py` | **ECRTM Orchestrator**: Manages the complete training lifecycle: Embedding loading -> Data preparation -> Model training -> Label generation via OpenAI. |
| `models.py` | **Neural Network Architecture**: Defines the `ECRTM` PyTorch model and the `ArgsECRTM` configuration interface. |
| `views.py` | **Training Endpoint**: Accepts hyperparameters (epochs, dropout) and triggers the `realizar_ecrtm_view` training job. |

#### `Backend/creacion_pdf/` & `Backend/diagrama/` - Synthesis Layer

| File | Purpose |
|------|---------|
| `creacion_pdf/Builder.py` | **LaTeX Factory**: Class responsible for assembling LaTeX fragments into a cohesive document structure. |
| `creacion_pdf/logic/orchestrator.py` | **Report Manager**: Coordinates content generation, calling LLMs to write summaries for each topic section. |
| `diagrama/logic.py` | **Graph Generator**: Converts topic distributions into NetworkX graphs and exports visual data structures. |

### 💻 Frontend Architecture (Angular)

The frontend is built with Angular 18, providing a responsive and interactive user experience.

| Directory | Purpose |
|-----------|---------|
| `src/app/` | **Core Application**: Contains the main modules and components. |
| `src/app/components/` | **UI Components**: Reusable UI elements and views. |
| `src/app/services/` | **Data Access**: Services for communicating with the Backend API. |
| `src/environments/` | **Configuration**: Environment variables (API URLs, Firebase config). |

---

## 🛠️ Technology Stack

### Backend Infrastructure

| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| Framework | **Django** | 5.1 | High-level web framework. |
| API | **DRF** | 3.15 | REST API toolkit. |
| Database | **SQLite** | 3.x | Lightweight storage for metadata. |
| Task Queue | **Asyncio** | - | Concurrent API requests. |

### AI & Machine Learning

| Component | Technology | Purpose |
|-----------|------------|---------|
| Framework | **PyTorch** | Implementation of custom ECRTM autoencoder. |
| Embeddings | **FastText** | Pre-trained word vectors (`crawl-300d-2M`). |
| LLM | **OpenAI GPT-4o** | Zero-shot topic labeling and text synthesis. |
| Topic Model | **ECRTM** | Embedded Clustering for short-text analysis. |

### Frontend

| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| Framework | **Angular** | 18.2.8 | Main frontend framework. |
| Styles | **SCSS** | - | Component-level styling. |
| Auth | **Firebase** | 18+ | User authentication and management. |
| UI Libs | **SweetAlert2** | 11.22 | Beautiful replacement for JavaScript's popup boxes. |
| Viz | **Plotly.js** | - | Rendering interactive topic graphs. |

### Data Processing & Visualization

| Component | Technology | Purpose |
|-----------|------------|---------|
| NLP | **NLTK / Regex** | Text tokenization and cleaning. |
| Scraping | **BeautifulSoup4** | Metadata extraction from HTML sources. |
| PDFs | **PyMuPDF** | High-fidelity text extraction from PDFs. |
| Graphs | **NetworkX** | Knowledge graph topology construction. |

---

## 🚀 Installation & Setup

### Prerequisites

- **Python** 3.10+
- **Node.js** 22.9.0+ (and npm)
- **Angular CLI** 18.2.20 (`npm install -g @angular/cli@18.2.20`)
- **Git**

### 1. Backend Setup (Django)

1. **Access the Source Code:**

    > **Note:** This is a private repository. Ensure you have the necessary permissions or have extracted the provided source code.

    ```bash
    cd ai-eduresearch-platform/Backend
    ```

2. **Create and activate a virtual environment:**

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

4. **Download Embedding Vectors:**
    - Create directory: `Backend/resources/files_vec/`
    - Download `crawl-300d-2M.vec` and place it here.

5. **Configure Environment:**
    - Create a `.env` file (or set variables) with your API keys:

        ```bash
        export OPENAI_API_KEY="sk-..."
        ```

    - **Configuration Variables (`.env`)**

        Define the following keys in your `Backend/.env` file:

        | Variable | Description | Example |
        |----------|-------------|---------|
        | `OPENAI_API_KEY` | Required for GPT-4o topic labeling. | `sk-proj...` |
        | `DEBUG` | Django debug mode (True/False). | `True` |
        | `SECRET_KEY` | Django security key. | `django-insecure...` |
        | `ALLOWED_HOSTS` | Comma-separate host list. | `localhost,127.0.0.1` |

6. **Run Migrations & Server:**

    ```bash
    python manage.py migrate
    python manage.py runserver
    ```

### 2. Frontend Setup (Angular)

1. **Navigate to frontend directory:**

    ```bash
    cd ../frontend
    ```

2. **Install dependencies:**

    ```bash
    npm install
    ```

3. **Configure Firebase:**
    - Update `src/environments/environment.ts` with your Firebase credentials (`apiKey`, `authDomain`, etc.).

4. **Start Development Server:**

    ```bash
    ng serve -o
    ```

    - Access the app at `http://localhost:4200/`.

---

## 📝 Usage Examples

### 1. Topic Modeling Request (Deep Learning)

**Endpoint:** `POST /deep_learning/encontrar_temas/`

**Input Payload:**

```json
{
  "ntemas": 5,
  "search_query": "Artificial Intelligence in Education",
  "apikey": "sk-...",
  "epochs": 100,
  "dropout": 0.1,
  "en1_units": 100,
  "beta_temp": 0.2
}
```

**Processing:**

1. Loads pre-processed chunks.
2. Initializes ECRTM with 300-dim embeddings.
3. Trains for 100 epochs.
4. Generates semantic labels via GPT-4o.

**Output Response:**

```json
{
  "ok": "Generacion de conocimiento generada.",
  "temas": [
    "Adaptive Learning Systems",
    "Student Performance Prediction",
    "Intelligent Tutoring Architecture",
    "Gamification Strategies",
    "Natural Language Interaction"
  ]
}
```

### 2. Article Search (Data Ingestion)

**Endpoint:** `POST /recoleccion_datos/buscar_articulos/`

**Input Payload:**

```json
{
  "search_query": "machine learning",
  "repositorios": ["doaj", "plos"],
  "search_query_mejorada": "machine learning classifiers"
}
```

---

## 🎨 Design Patterns

| Pattern | Implementation | Purpose |
|---------|----------------|---------|
| **Gateway** | `Recoleccion_datos/services.py` | Abstracting external API calls (DOAJ/PLOS) behind a uniform interface. |
| **Builder** | `creacion_pdf/Builder.py` | Constructing complex LaTeX documents step-by-step. |
| **Strategy** | `Deep_Learning/logic.py` | Encapsulating the topic modeling algorithm, allowing for future model swaps. |
| **Facade** | `views.py` (in all apps) | Providing a simplified interface to the complex underlying logic layers. |

---

## 🔧 Troubleshooting

### 🛑 Error: "No se encontraron partes de embeddings"

**Context**: The system needs pre-trained vectors to initialize the neural network.
**Fix**:

1. Navigate to `Backend/resources/`.
2. Create folder `files_vec`.
3. Download the `crawl-300d-2M.vec` split files.
4. The system will auto-reconstruct them on first run.

### 🛑 Error: "OpenAI API Key Missing"

**Context**: Label generation requires an external LLM.
**Fix**: Pass `"apikey": "sk-..."` in your request body or configure the environment variable.

---

## 📄 License

**Copyright © 2026 AI-EduResearch Team.** All Rights Reserved.

This project is proprietary and confidential. Unauthorized copying of this file, via any medium, is strictly prohibited.
