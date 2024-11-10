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
    participant A as Analytics Agent

    C->>O: "Show me top 5 patients with highest HbA1c levels in diabetes clinic"
    
    O->>Q: Process clinical query
    activate Q
    Note over Q: Identifies:<br/>1. Query type: Ranking<br/>2. Measure: HbA1c<br/>3. Limit: 5<br/>4. Context: Diabetes clinic
    Q-->>O: Structured query requirements
    deactivate Q

    par Schema & Entity Resolution
        O->>S: Resolve schema context
        activate S
        Note over S: Maps required tables:<br/>1. patient_records<br/>2. lab_results<br/>3. clinic_assignments
        S-->>O: Table relationships
        deactivate S

        O->>E: Resolve clinical entities
        activate E
        Note over E: Resolves:<br/>1. HbA1c to LOINC: 4548-4<br/>2. Diabetes clinic ID
        E-->>O: Resolved entities
        deactivate E

        O->>D: Get clinical context
        activate D
        Note over D: Validates:<br/>1. HbA1c normal ranges<br/>2. Clinical relevance<br/>3. Time validity
        D-->>O: Clinical rules
        deactivate D
    end

    O->>R: Execute data retrieval
    activate R
    Note over R: SQL Generation:<br/>SELECT p.id, p.name, l.value<br/>FROM patients p<br/>JOIN lab_results l<br/>WHERE l.loinc = '4548-4'<br/>ORDER BY l.value DESC<br/>LIMIT 5
    R-->>O: Raw results
    deactivate R

    O->>A: Process analytics
    activate A
    Note over A: Analysis:<br/>1. Validate ranges<br/>2. Format values<br/>3. Add clinical context<br/>4. Generate alerts
    A-->>O: Analyzed results
    deactivate A

    O-->>C: Clinical report with top 5 HbA1c values
