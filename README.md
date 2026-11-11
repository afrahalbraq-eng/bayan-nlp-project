Project Overview

Bayan is an enterprise-grade natural language processing (NLP) service designed to automatically parse, classify, extract entities from, and index bilingual (Arabic and English) citizen feedback and complaints. It provides a streamlined interface for automated grievance analysis and semantic similarity matching.

🛑 Problem Description

Public agencies and corporate service providers handle thousands of diverse citizen feedback messages and complaints daily. Manually reading, categorizing, extracting critical entities (like locations and service types), and cross-referencing historical cases is time-consuming, prone to bottlenecks, and lacks real-time operational insights.

📊 Dataset & Model Used

Dataset: Bilingual citizen complaints dataset containing structured feedback, titles, and descriptions, indexed across historical case records.

Models Used:

Classification: Fine-tuned Arabic/English classification model optimized via ONNX Runtime (INT8 Quantization).

Named Entity Recognition (NER): Hugging Face token-classification pipeline for extracting operational entities.

Embeddings: sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2 for dense vector representations.

🏗️ Workflow / Architecture

[ Incoming Complaint ] 
          │
          ▼
 [ 1. Preprocessing & PII Masking ] ── (Sanitizes Phones & Emails)
          │
          ▼
 ┌────────┴─────────────────────────┬──────────────────────────┐
 │                                  │                          │
 ▼                                  ▼                          ▼
[ 2. Text Classification ]   [ 3. Named Entity Recognition ]   [ 4. Semantic Search ]
(ONNX INT8 Optimized Model)   (Fine-tuned Transformer/NER)     (FAISS Vector Index)
 │                                  │                          │
 └────────┴─────────────────────────┴──────────────────────────┘
          │
          ▼
 [ 5. FastAPI Unified REST API & Interactive UI ]


📈 Results & Evaluation

Model Optimization: Evaluated FP32 vs. INT8 quantization; INT8 achieved a 97% agreement score with FP32 while significantly reducing latency and memory footprint.

Vector Indexing: Successfully indexed historical records using FAISS (IndexFlatIP) for rapid semantic similarity search.

💻 Technologies Used

Language: Python 3.10+

Frameworks & Libraries: FastAPI, Hugging Face Transformers, Sentence-Transformers, ONNX Runtime

Vector Search Engine: FAISS (CPU)

Data Manipulation: Pandas, NumPy, Regex

🚀 How to Run the Project

Clone the Repository:

git clone https://github.com/afrahalbraq-eng/bayan-nlp-project.git
cd bayan-nlp-project


Install Dependencies:

pip install -r requirements.txt


Run the Server:

make serve
# Alternatively using uvicorn directly:
uvicorn main:app --host 127.0.0.1 --port 8000


🔮 Future Improvements

Integrating automated dialect detection (Gulf, Levantine, Egyptian).

Implementing two-stage neural re-ranking for enhanced FAISS retrieval accuracy.

Containerizing the application using Docker for scalable cloud deployment.

🔗 SDAIA Academy GitHub Repository Link

Repository URL: [GitHub Repository Link](https://github.com/SDAIAAcademy)
