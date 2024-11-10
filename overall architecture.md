# Designs-

```mermaid

flowchart TB
    subgraph External["External Layer"]
        UI[Web UI - Next.js 14]
        API[FastAPI/LangServe]
        DS[(Clinical Sources)]
    end

    subgraph Orchestration["LangGraph Orchestration"]
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

    subgraph Core["Core Processing"]
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

    subgraph Infrastructure["Modern Stack"]
        direction LR
        K[Kafka/Redpanda]
        R[(Redis Enterprise)]
        V[(Vectorize)]
        P[(PGVector)]
    end

    subgraph Storage["Storage Layer"]
        direction LR
        DW[(MongoDB Atlas)]
        FS[(Milvus)]
        MS[(MinIO)]
        FB[(LangKit Store)]
    end

    subgraph Monitor["Observability"]
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

    classDef external fill:#e1f5fe,stroke:#01579b
    classDef orch fill:#fff3e0,stroke:#e65100
    classDef core fill:#e8f5e9,stroke:#2e7d32
    classDef infra fill:#f3e5f5,stroke:#4a148c
    classDef storage fill:#fce4ec,stroke:#880e4f
    classDef monitor fill:#fff8e1,stroke:#ff6f00

    class UI,API,DS external
    class LG,QA,DA,RA,MA,MON orch
    class RP,RV,RC,FE,MT,MP core
    class K,R,V,P infra
    class DW,FS,MS,FB storage
    class MM,DM,PM monitor
