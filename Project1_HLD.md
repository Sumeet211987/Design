sequenceDiagram
    participant User
    participant Frontend as Frontend (Streamlit)
    participant Backend as Backend (Flask)
    participant Search as Vector Search (Chroma DB)
    participant LLM as Gemini Pro LLM
    participant Data as Data Layer (GCP Buckets, Azure DevOps)

    User->>Frontend: Submit Query
    Frontend->>Backend: Forward Query
    Backend->>Search: Retrieve Relevant Data
    Search->>LLM: Augment Query with Retrieved Data
    LLM-->>Backend: Generate Response
    Backend-->>Frontend: Return Response
    Frontend-->>User: Display Response

    Backend->>Data: Preprocess, Store, and Monitor Data
    Data-->>Backend: Confirm Operations
    Backend->>Data: Deploy and Authenticate Services