# Designs-

```mermaid

%%{init: {
  'theme': 'dark',
  'themeVariables': {
    'fontFamily': 'arial',
    'primaryColor': '#2C3E50',
    'primaryTextColor': '#E8F0F8',
    'primaryBorderColor': '#445E7C',
    'lineColor': '#445E7C'
  }
}}%%
flowchart TB
    subgraph External["External Integration Layer"]
        UI[Web UI - Next.js 14]
        API[FastAPI/LangServe]
        DS[(Clinical Sources)]
    end

    subgraph Schema["Schema & Knowledge Layer"]
        direction TB
        subgraph SchemaProcess["Schema Processing"]
            SM[Schema Manager]
            DQ[Data Quality Engine]
            EM[Entity Mapper]
        end
        
        subgraph Knowledge["Domain Knowledge"]
            KG[Knowledge Graph]
            DR[Domain Rules]
            AM[Alias Manager]
        end
    end

    subgraph Orchestration["LangGraph Orchestration"]
        direction TB
        LG[LangGraph Controller]
        subgraph Agents["Agent Network"]
            QA[Query Agent]
            DA[Data Agent]
            RA[Rules Agent]
            EA[Entity Agent]
            MA[ML Agent]
            MON[Monitor Agent]
        end
    end

    subgraph Core["Enhanced Processing Layer"]
        direction TB
        subgraph Rules["Rules Engine"]
            RP[RAG Pipeline]
            RV[Vector Store]
            RC[Context Engine]
        end

        subgraph ML["ML Pipeline"]
            FE[Feature Engineering]
            MT[Model Training]
            MP[Prediction Engine]
        end

        subgraph Entity["Entity Resolution"]
            ER[Entity Recognition]
            VM[Vector Matching]
            NM[Name Normalizer]
        end
    end

    subgraph Infrastructure["Infrastructure Layer"]
        direction LR
        K[Kafka/Redpanda]
        R[(Redis Enterprise)]
        V[Vectorize]
        P[PGVector]
    end

    subgraph Storage["Persistence Layer"]
        direction LR
        DW[(Data Warehouse)]
        FS[(Feature Store)]
        MS[(Model Store)]
        ES[(Entity Store)]
    end

    subgraph Monitor["Observability Layer"]
        direction TB
        MM[Model Monitor]
        DM[Data Quality Monitor]
        PM[Performance Monitor]
        EM[Entity Monitor]
    end

    External --> Schema
    Schema --> Orchestration
    Orchestration --> Core
    Core --> Infrastructure
    Infrastructure --> Storage
    Storage --> Monitor
    Monitor --> Orchestration

    classDef external fill:#3498DB,stroke:#2980B9,color:#E8F0F8
    classDef schema fill:#2ECC71,stroke:#27AE60,color:#E8F0F8
    classDef orch fill:#E74C3C,stroke:#C0392B,color:#E8F0F8
    classDef core fill:#9B59B6,stroke:#8E44AD,color:#E8F0F8
    classDef infra fill:#F1C40F,stroke:#F39C12,color:#2C3E50
    classDef storage fill:#1ABC9C,stroke:#16A085,color:#E8F0F8
    classDef monitor fill:#34495E,stroke:#2C3E50,color:#E8F0F8

    class External external
    class Schema,SchemaProcess,Knowledge schema
    class Orchestration,Agents orch
    class Core,Rules,ML,Entity core
    class Infrastructure infra
    class Storage storage
    class Monitor monitor
           
    
