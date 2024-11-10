# Designs-

```mermaid

%%{init: {
  'theme': 'dark',
  'themeVariables': {
    'fontFamily': 'arial',
    'nodeTextColor': '#FFFFFF',
    'mainBkg': '#1F2937',
    'textColor': '#FFFFFF',
    'lineColor': '#FFFFFF',
    'clusterBkg': '#374151',
    'titleColor': '#FFFFFF'
  }
}}%%
flowchart TB
    subgraph Input["Input System"]
        UI[Clinical Interface]
        API[API Gateway]
    end

    subgraph AgentNetwork["LangGraph Agent Network"]
        direction TB
        OA[Orchestrator Agent]
        
        subgraph UnderstandingAgents["Understanding Layer"]
            QA[Query Understanding Agent]
            SA[Schema Understanding Agent<br>Clinical DB Schema]
            EA[Entity Resolution Agent<br>Medical Terms & Codes]
            DA[Domain Knowledge Agent<br>Clinical Guidelines]
        end

        subgraph ExecutionAgents["Execution Layer"]
            PA[Planning Agent<br>Query Strategy]
            DRA[Data Retrieval Agent<br>Clinical Data Access]
            VA[Validation Agent<br>Clinical Rules]
        end

        subgraph AnalysisAgents["Analysis Layer"]
            AA[Analytics Agent<br>Clinical Metrics]
            MA[ML Agent<br>Risk Models]
            RA[Reporting Agent<br>Clinical Summaries]
        end
    end

    subgraph Tools["Agent Tools & Resources"]
        direction TB
        subgraph DataStores["Data Stores"]
            CDB[(Clinical DB)]
            VDB[(Vector Store)]
            KG[(Medical Knowledge Graph)]
        end
        
        subgraph Resources["Clinical Resources"]
            SNOMED[SNOMED CT]
            ICD[ICD-10 Codes]
            LOINC[LOINC Lab Codes]
        end
        
        subgraph Models["ML Models"]
            ClinicalBERT[ClinicalBERT]
            RiskModels[Risk Models]
        end
    end

    subgraph Learning["Learning System"]
        MA[Memory Agent<br>Case History]
        LA[Learning Agent<br>Pattern Recognition]
        FA[Feedback Agent<br>Clinical Validation]
    end

    Input --> OA
    OA --> UnderstandingAgents
    UnderstandingAgents --> ExecutionAgents
    ExecutionAgents --> AnalysisAgents
    UnderstandingAgents -.-> Tools
    ExecutionAgents -.-> Tools
    AnalysisAgents -.-> Tools
    AnalysisAgents --> Learning
    Learning --> OA

   
