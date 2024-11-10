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
        DS[(Data Sources)]
    end

    subgraph SchemaLayer["Schema Management Layer"]
        direction TB
        subgraph TableManager["Table Management"]
            TM[Table Mapper]
            RM[Relationship Manager]
            CM[Column Manager]
            DT[Data Type Handler]
        end
        
        subgraph EntityManager["Entity Management"]
            ER[Entity Registry]
            AM[Alias Manager]
            SM[Standardization Manager]
            VM[Validation Manager]
        end

        subgraph DomainManager["Domain Knowledge"]
            DK[Domain Rules]
            BL[Business Logic]
            KM[KPI Manager]
            TH[Term Handler]
        end
    end

    subgraph Orchestration["Processing Orchestration"]
        direction TB
        OE[Orchestration Engine]
        
        subgraph DataProcessing["Data Processing"]
            DP[Data Processor]
            QV[Quality Validator]
            TR[Type Resolver]
            JE[Join Engine]
        end

        subgraph QueryProcessing["Query Processing"]
            QP[Query Parser]
            QA[Query Analyzer]
            QO[Query Optimizer]
            QE[Query Executor]
        end
    end

    subgraph Storage["Storage Layer"]
        direction LR
        RD[(Relational DB)]
        VD[(Vector Store)]
        CD[(Cache Layer)]
        KG[(Knowledge Graph)]
    end

    subgraph Analytics["Analytics Layer"]
        direction TB
        subgraph Basic["Basic Analytics"]
            SA[Statistical Analysis]
            AG[Aggregation Engine]
            FT[Filter Engine]
        end

        subgraph Advanced["Advanced Analytics"]
            ML[ML Pipeline]
            PP[Pattern Processor]
            PA[Predictive Analytics]
        end
    end

    subgraph Monitor["Monitoring Layer"]
        direction TB
        PM[Performance Monitor]
        QM[Quality Monitor]
        UM[Usage Monitor]
        AM[Analytics Monitor]
    end

    External --> SchemaLayer
    SchemaLayer --> Orchestration
    Orchestration --> Storage
    Storage --> Analytics
    Analytics --> Monitor
    Monitor --> Orchestration

    classDef external fill:#3498DB,stroke:#2980B9,color:#E8F0F8
    classDef schema fill:#2ECC71,stroke:#27AE60,color:#E8F0F8
    classDef orch fill:#E74C3C,stroke:#C0392B,color:#E8F0F8
    classDef storage fill:#9B59B6,stroke:#8E44AD,color:#E8F0F8
    classDef analytics fill:#F1C40F,stroke:#F39C12,color:#2C3E50
    classDef monitor fill:#1ABC9C,stroke:#16A085,color:#E8F0F8

    class External external
    class SchemaLayer,TableManager,EntityManager,DomainManager schema
    class Orchestration,DataProcessing,QueryProcessing orch
    class Storage storage
    class Analytics,Basic,Advanced analytics
    class Monitor monitor
        
       
    
