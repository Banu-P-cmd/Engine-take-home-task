# Designs-

```mermaid

%%{init: {
  'theme': 'dark',
  'themeVariables': {
    'fontFamily': 'arial',
    'primaryColor': '#2C3E50',
    'primaryTextColor': '#E8F0F8',
    'primaryBorderColor': '#445E7C',
    'lineColor': '#445E7C',
    'secondaryColor': '#34495E',
    'tertiaryColor': '#1C2833'
  }
}}%%
flowchart TB
    subgraph External["External Integration Layer"]
        UI[Web UI - Next.js 14]
        API[FastAPI/LangServe]
        DS[(Clinical Sources)]
    end

    subgraph Orchestration["LangGraph Orchestrator"]
        direction TB
        LG[LangGraph Controller]
        subgraph Agents["Agent Network"]
            QA[Query Agent w/Claude 3]
            DA[Data Agent]
            RA[Rules Agent]
            MA[ML Agent]
            MON[Monitor Agent]
        end
    end

    subgraph Core["Core Processing Layer"]
        direction TB
        subgraph Rules["Rules Engine"]
            RP[RAG Pipeline]
            RV[Vector Store - Qdrant]
            RC[(ChromaDB)]
        end

        subgraph ML["ML Pipeline"]
            FE[Vector Database]
            MT[LlamaIndex]
            MP[Model Registry]
        end
    end

    subgraph Infrastructure["Infrastructure Layer"]
        direction LR
        K[Kafka/Redpanda]
        R[(Redis Enterprise)]
        V[(Vectorize)]
        P[(PGVector)]
    end

    subgraph Storage["Persistence Layer"]
        direction LR
        DW[(MongoDB Atlas)]
        FS[(Milvus)]
        MS[(MinIO)]
        FB[(LangKit Store)]
    end

    subgraph Monitor["Observability Layer"]
        direction TB
        MM[LangSmith]
        DM[Weights & Biases]
        PM[Prometheus/Grafana]
    end

    External --> Orchestration
    Orchestration --> Infrastructure
    Infrastructure --> Core
    Core --> Storage
    Storage --> Monitor
    Monitor --> Orchestration

    classDef external fill:#3498DB,stroke:#2980B9,color:#E8F0F8
    classDef orch fill:#2ECC71,stroke:#27AE60,color:#E8F0F8
    classDef core fill:#E74C3C,stroke:#C0392B,color:#E8F0F8
    classDef infra fill:#9B59B6,stroke:#8E44AD,color:#E8F0F8
    classDef storage fill:#F1C40F,stroke:#F39C12,color:#2C3E50
    classDef monitor fill:#1ABC9C,stroke:#16A085,color:#E8F0F8

    class UI,API,DS external
    class LG,QA,DA,RA,MA,MON orch
    class RP,RV,RC,FE,MT,MP core
    class K,R,V,P infra
    class DW,FS,MS,FB storage
    class MM,DM,PM monitor

    %% Add professional styling
    style External fill:#2C3E50,stroke:#445E7C,color:#E8F0F8
    style Orchestration fill:#2C3E50,stroke:#445E7C,color:#E8F0F8
    style Core fill:#2C3E50,stroke:#445E7C,color:#E8F0F8
    style Infrastructure fill:#2C3E50,stroke:#445E7C,color:#E8F0F8
    style Storage fill:#2C3E50,stroke:#445E7C,color:#E8F0F8
    style Monitor fill:#2C3E50,stroke:#445E7C,color:#E8F0F8
            
    
