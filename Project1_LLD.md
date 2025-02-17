sequenceDiagram
    participant User
    participant Streamlit as Frontend (Streamlit)
    participant Flask as Backend (Flask)
    participant ChromaDB as Vector Search (Chroma DB)
    participant Gemini as Gemini Pro LLM
    participant GCP as GCP Buckets & Preprocessing
    participant Azure as Azure DevOps
    participant Embeddings as Embeddings Storage

    User->>Streamlit: Submit Query (COBOL/Java)
    Streamlit->>Flask: Forward Query
    Flask->>ChromaDB: Perform Vector Search
    ChromaDB->>Embeddings: Fetch Relevant Embeddings
    Embeddings-->>ChromaDB: Return Embeddings
    ChromaDB->>Gemini: Send Retrieved Data & Query
    Gemini-->>Flask: Generate Response
    Flask-->>Streamlit: Send Generated Response
    Streamlit-->>User: Display Response

    Flask->>GCP: Request Data Preprocessing
    GCP->>Azure: Trigger Batch Jobs for Data Extraction
    Azure-->>GCP: Provide Extracted Data
    GCP->>GCP: Preprocess Data
    GCP->>Gemini: Generate Embeddings
    Gemini-->>Embeddings: Store Embeddings

    Flask->>GCP: Send Logs/Monitor Metrics
    GCP-->>Flask: Confirm Monitoring
    Flask->>GCP: Authenticate via IAM
    Flask->>Docker: Deploy on Kubernetes (GKE)
    Docker-->>Azure: CI/CD Pipeline Execution
