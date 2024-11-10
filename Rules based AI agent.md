sequenceDiagram
    participant C as Clinician
    participant L as LangGraph
    participant Q as Query Agent
    participant D as Data Agent
    participant R as RAG Agent
    participant M as Monitor

    C->>L: Query: "Find high-risk diabetes patients"
    
    L->>Q: Process query
    activate Q
    Note over Q: Using Claude 3:<br/>1. Intent classification<br/>2. Entity extraction<br/>3. Query planning
    Q-->>L: Structured query plan
    deactivate Q
    
    par Parallel Processing
        L->>D: Retrieve patient data
        Note over D: Sources:<br/>1. PGVector<br/>2. Redis Enterprise
        
        L->>R: Prepare RAG context
        Note over R: Using:<br/>1. ChromaDB<br/>2. LlamaIndex
    end
    
    D-->>L: Vector-enriched data
    R-->>L: Retrieved context
    
    L->>R: Execute RAG pipeline
    activate R
    Note over R: Processing:<br/>1. Semantic search<br/>2. Context injection<br/>3. Rule application
    R-->>L: Risk assessment
    deactivate R
    
    L->>M: Log with LangSmith
    Note over M: Track:<br/>1. RAG performance<br/>2. Query patterns
    
    L-->>C: Enhanced Risk Report
