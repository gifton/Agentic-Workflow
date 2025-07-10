# Agent Interaction Flow Diagrams

Visual representations of how the three agents (Orchestrator/Atlas, Specialist/Mercury, and Evaluator/Apollo) interact in the Agentic Workflow system.

## Basic Agent Interaction Flow

```mermaid
graph TD
    subgraph "User Input"
        U[User Task]
    end
    
    subgraph "Orchestrator (Atlas)"
        O1[Analyze Task]
        O2[Create Plan]
        O3[Assign Work]
        O4[Monitor Progress]
    end
    
    subgraph "Specialist (Mercury)"
        S1[Receive Assignment]
        S2[Implement Solution]
        S3[Track Confidence]
        S4[Report Progress]
    end
    
    subgraph "Evaluator (Apollo)"
        E1[Review Work]
        E2[Test Solution]
        E3[Assess Quality]
        E4[Provide Feedback]
    end
    
    subgraph "Output"
        R[Final Result]
    end
    
    U --> O1
    O1 --> O2
    O2 --> O3
    O3 --> S1
    S1 --> S2
    S2 --> S3
    S3 --> S4
    S4 --> E1
    E1 --> E2
    E2 --> E3
    E3 --> E4
    E4 --> O4
    O4 -->|If incomplete| O3
    O4 -->|If complete| R
```

## Detailed Workflow with Checkpointing

```mermaid
sequenceDiagram
    participant User
    participant Atlas as Orchestrator<br/>(Atlas)
    participant Mercury as Specialist<br/>(Mercury)
    participant Apollo as Evaluator<br/>(Apollo)
    participant CP as Checkpoint<br/>System
    
    User->>Atlas: Submit task
    Atlas->>Atlas: Analyze requirements
    Atlas->>CP: Save initial state
    
    loop For each subtask
        Atlas->>Mercury: Assign subtask
        Mercury->>Mercury: Implement
        Mercury->>Mercury: Self-test
        Mercury->>CP: Save progress
        Mercury->>Apollo: Submit for review
        Apollo->>Apollo: Test & evaluate
        
        alt Quality passed
            Apollo->>Atlas: Approve ✓
            Atlas->>CP: Mark milestone
        else Quality failed
            Apollo->>Mercury: Request fixes
            Mercury->>Mercury: Iterate
        end
    end
    
    Atlas->>User: Deliver final result
```

## Confidence Tracking Flow

```mermaid
graph LR
    subgraph "Confidence Evolution"
        C1[Initial: 60%]
        C2[After Research: 75%]
        C3[After Implementation: 85%]
        C4[After Testing: 92%]
        C5[Final: 95%]
    end
    
    subgraph "Actions"
        A1[Task Start]
        A2[Complete Research]
        A3[Build Solution]
        A4[Pass Tests]
        A5[Final Review]
    end
    
    A1 --> C1
    C1 --> A2
    A2 --> C2
    C2 --> A3
    A3 --> C3
    C3 --> A4
    A4 --> C4
    C4 --> A5
    A5 --> C5
    
    style C1 fill:#ff9999
    style C2 fill:#ffcc99
    style C3 fill:#ffff99
    style C4 fill:#99ff99
    style C5 fill:#66ff66
```

## Error Recovery Flow

```mermaid
stateDiagram-v2
    [*] --> Planning
    Planning --> Implementation
    Implementation --> Testing
    Testing --> Evaluation
    
    Implementation --> ErrorDetected
    Testing --> ErrorDetected
    
    ErrorDetected --> CheckpointRestore
    CheckpointRestore --> Implementation
    
    Evaluation --> Approved
    Evaluation --> NeedsRevision
    
    NeedsRevision --> Implementation
    Approved --> [*]
    
    note right of CheckpointRestore
        Restore to last
        known good state
    end note
    
    note right of NeedsRevision
        Apollo requests
        improvements
    end note
```

## Multi-Agent Communication Pattern

```mermaid
graph TB
    subgraph "Communication Hub"
        H[Event Bus]
    end
    
    subgraph "Agents"
        O[Orchestrator<br/>Plans & Coordinates]
        S[Specialist<br/>Implements & Builds]
        E[Evaluator<br/>Tests & Validates]
    end
    
    O <-->|Status Updates| H
    S <-->|Progress Reports| H
    E <-->|Quality Metrics| H
    
    O -->|Assignments| S
    S -->|Work Products| E
    E -->|Feedback| O
    
    style O fill:#9cf,stroke:#333,stroke-width:2px
    style S fill:#f9c,stroke:#333,stroke-width:2px
    style E fill:#fc9,stroke:#333,stroke-width:2px
```

## Agentic Natural Adaptive Flow

```mermaid
graph TD
    subgraph "Natural Language Input"
        NL["agentic natural for web API<br/>with testing optimized for quality"]
    end
    
    subgraph "Adaptation Layer"
        A1[Parse Modifiers]
        A2[Infer Requirements]
        A3[Configure Workflow]
    end
    
    subgraph "Dynamic Workflow"
        W1[Basic Structure]
        W2[+ Testing Phase]
        W3[+ Quality Gates]
        W4[+ Extra Review]
    end
    
    NL --> A1
    A1 -->|"for web API"| A2
    A1 -->|"with testing"| A2
    A1 -->|"optimized for quality"| A2
    
    A2 --> A3
    A3 --> W1
    A3 -->|Testing modifier| W2
    A3 -->|Quality optimization| W3
    A3 -->|Quality optimization| W4
    
    style NL fill:#e6f2ff,stroke:#0066cc,stroke-width:2px
    style A3 fill:#ffe6e6,stroke:#cc0000,stroke-width:2px
```

## Implementation Comparison Flow

```mermaid
graph TD
    subgraph "User Decision"
        START[Choose Implementation]
    end
    
    subgraph "Implementations"
        NAT[Natural<br/>Adaptive & Smart]
        STD[Standard<br/>Balanced]
        ADV[Advanced<br/>Full Featured]
        ZEN[Zen<br/>Ultra Simple]
        ZPY[Zen-Python<br/>ML Focused]
    end
    
    START -->|"I want flexibility"| NAT
    START -->|"I want balance"| STD
    START -->|"I need everything"| ADV
    START -->|"Keep it simple"| ZEN
    START -->|"ML/Python project"| ZPY
    
    NAT --> RESULT[One workflow<br/>adapts to all needs]
    STD --> RESULT2[Fixed 3-agent<br/>workflow]
    ADV --> RESULT3[Complex multi-agent<br/>system]
    ZEN --> RESULT4[Single file<br/>workflow]
    ZPY --> RESULT5[ML-optimized<br/>workflow]
    
    style NAT fill:#ffd700,stroke:#333,stroke-width:3px
    style RESULT fill:#90ee90,stroke:#333,stroke-width:2px
```

## Workflow State Machine

```mermaid
stateDiagram-v2
    [*] --> Initialization
    
    Initialization --> Planning
    
    state Planning {
        [*] --> AnalyzeTask
        AnalyzeTask --> CreateSteps
        CreateSteps --> AssignConfidence
        AssignConfidence --> [*]
    }
    
    Planning --> Implementation
    
    state Implementation {
        [*] --> BuildSolution
        BuildSolution --> SelfTest
        SelfTest --> UpdateConfidence
        UpdateConfidence --> [*]
    }
    
    Implementation --> Evaluation
    
    state Evaluation {
        [*] --> ReviewCode
        ReviewCode --> RunTests
        RunTests --> AssessQuality
        AssessQuality --> [*]
    }
    
    Evaluation --> Decision
    
    state Decision {
        [*] --> CheckConfidence
        CheckConfidence --> Ship: confidence >= 80
        CheckConfidence --> Iterate: confidence < 80
    }
    
    Decision --> [*]: Ship
    Decision --> Implementation: Iterate
```

## Agent Responsibility Matrix

```mermaid
graph LR
    subgraph "Orchestrator (Atlas)"
        O1[Task Decomposition]
        O2[Resource Allocation]
        O3[Timeline Management]
        O4[Integration]
    end
    
    subgraph "Specialist (Mercury)"
        S1[Implementation]
        S2[Problem Solving]
        S3[Technical Decisions]
        S4[Code Writing]
    end
    
    subgraph "Evaluator (Apollo)"
        E1[Quality Assurance]
        E2[Testing]
        E3[Performance Review]
        E4[Security Check]
    end
    
    subgraph "Shared Responsibilities"
        SR1[Confidence Tracking]
        SR2[Progress Reporting]
        SR3[Risk Assessment]
    end
    
    O1 -.-> SR1
    S1 -.-> SR1
    E1 -.-> SR1
    
    O2 -.-> SR2
    S2 -.-> SR2
    E2 -.-> SR2
    
    O3 -.-> SR3
    S3 -.-> SR3
    E3 -.-> SR3
```

## Rendering These Diagrams

These diagrams use Mermaid syntax and can be rendered in:
- GitHub markdown files (automatic rendering)
- VS Code with Mermaid preview extensions
- Online at [mermaid.live](https://mermaid.live)
- Any markdown viewer that supports Mermaid

To use in other tools, copy the mermaid code blocks and paste into any Mermaid-compatible renderer.