# Designs-

```mermaid

%%{init: {
  'theme': 'dark',
  'themeVariables': {
    'fontFamily': 'monaco',
    'primaryColor': '#BB86FC',
    'primaryTextColor': '#fff',
    'primaryBorderColor': '#BB86FC',
    'lineColor': '#BB86FC',
    'secondaryColor': '#03DAC6',
    'tertiaryColor': '#CF6679'
  }
}}%%
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

    classDef external fill:#BB86FC,stroke:#BB86FC,color:#000000
    classDef orch fill:#03DAC6,stroke:#03DAC6,color:#000000
    classDef core fill:#CF6679,stroke:#CF6679,color:#000000
    classDef infra fill:#FFB86C,stroke:#FFB86C,color:#000000
    classDef storage fill:#50FA7B,stroke:#50FA7B,color:#000000
    classDef monitor fill:#8BE9FD,stroke:#8BE9FD,color:#000000

    class UI,API,DS external
    class LG,QA,DA,RA,MA,MON orch
    class RP,RV,RC,FE,MT,MP core
    class K,R,V,P infra
    class DW,FS,MS,FB storage
    class MM,DM,PM monitor

   
