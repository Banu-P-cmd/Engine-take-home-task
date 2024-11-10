# Designs-


```mermaid

sequenceDiagram
    participant C as Clinician
    participant O as Orchestrator Agent
    participant Q as Query Agent
    participant S as Schema Agent
    participant E as Entity Agent
    participant D as Domain Agent
    participant R as Data Retrieval Agent
    participant M as ML Agent
    participant A as Analytics Agent

    C->>O: "Predict risk of diabetes for patients based on last 6 months data"
    
    O->>Q: Process prediction query
    activate Q
    Note over Q: Identifies:<br/>1. Task: Risk prediction<br/>2. Timeframe: 6 months<br/>3. Condition: Diabetes<br/>4. Scope: All patients
    Q-->>O: Prediction requirements
    deactivate Q

    par Data Preparation
        O->>S: Get temporal schema
        activate S
        Note over S: Maps required data:<br/>1. Demographics<br/>2. Lab results<br/>3. Vital signs<br/>4. Medications<br/>5. Family history
        S-->>O: Data schema
        deactivate S

        O->>E: Resolve clinical markers
        activate E
        Note over E: Maps indicators:<br/>1. HbA1c<br/>2. Fasting glucose<br/>3. BMI<br/>4. Blood pressure<br/>5. Family history
        E-->>O: Clinical markers
        deactivate E

        O->>D: Get risk factors
        activate D
        Note over D: Defines:<br/>1. Risk thresholds<br/>2. Clinical criteria<br/>3. Intervention points<br/>4. Risk categories
        D-->>O: Risk criteria
        deactivate D
    end

    O->>R: Retrieve historical data
    activate R
    Note over R: Collects:<br/>1. Time-series data<br/>2. Patient history<br/>3. Related conditions<br/>4. Treatment history
    R-->>O: Patient datasets
    deactivate R

    O->>M: Execute prediction
    activate M
    Note over M: ML Pipeline:<br/>1. Feature engineering<br/>2. Model selection<br/>3. Risk calculation<br/>4. Confidence scoring
    M-->>O: Risk predictions
    deactivate M

    O->>A: Generate insights
    activate A
    Note over A: Analysis:<br/>1. Risk stratification<br/>2. Key factors<br/>3. Trend analysis<br/>4. Recommendations
    A-->>O: Clinical insights
    deactivate A

    O-->>C: Comprehensive risk report with recommendations
