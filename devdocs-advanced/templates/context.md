# Enhanced Agentic Loop Context Template

## Task Description
[Provide a detailed description of what needs to be accomplished, including specific requirements, constraints, and expected outcomes]

## Repository Configuration
- **Repository Path**: [Absolute path or "None" for generic task]
- **Target Framework**: [e.g., Swift 6.1, Metal 3, Core ML]
- **Platform**: [iOS 17+, macOS 14+, visionOS, etc.]
- **Architecture Focus**: [Apple Silicon, x86_64, Universal]
- **Dependencies**: [List key frameworks and libraries]

## Task Complexity Assessment
- **Estimated Complexity**: [Low|Medium|High|Critical]
- **Domain Expertise Required**: [List specific areas]
- **Performance Requirements**: [Specific metrics if applicable]
- **Security Considerations**: [Any security-critical aspects]
- **Risk Level**: [Low|Medium|High]

## Enhanced Configuration

### Specialist Configuration
```yaml
specialist_config:
  desired_parallelism: 2  # 1-3 specialists
  allocation_strategy: "dynamic"  # static|dynamic|adaptive
  
  domains_required:
    - swift_systems     # Memory management, unsafe code
    - concurrency      # Actors, async/await, Tasks
    - performance      # SIMD, cache optimization
    - metal_gpu        # Compute shaders, GPU programming
    - security         # Cryptography, secure coding

  expertise_level:
    minimum: "senior"   # junior|mid|senior|principal
    preferred: "principal"
```

### Confidence Requirements
```yaml
confidence_config:
  # Overall workflow confidence thresholds
  minimum_acceptable: 75      # Below this, workflow adjusts
  auto_spawn_threshold: 70    # Spawn additional specialist
  human_review_threshold: 60  # Request human intervention
  halt_threshold: 50         # Stop and reassess
  
  # Task-specific confidence weights
  dimension_weights:
    quality: 0.4
    performance: 0.3
    security: 0.2
    confidence_calibration: 0.1
  
  # Critical component thresholds (override defaults)
  critical_components:
    memory_management: 95
    security_functions: 95
    concurrent_code: 90
    public_apis: 90
```

### Checkpoint Configuration
```yaml
checkpoint_config:
  enabled: true
  storage_path: "./outputs/{TASK}/checkpoints"
  
  triggers:
    automatic:
      - phase_complete
      - specialist_complete
      - confidence_drop        # >10 point drop
      - error_encountered
      - decision_made         # Major decisions only
    
  options:
    compression: true
    encryption: false        # Enable for sensitive tasks
    retention_days: 30
    max_size_mb: 100
    
  recovery:
    auto_resume: true
    max_attempts: 3
    fallback_strategy: "previous_checkpoint"
```

### Event System Configuration
```yaml
event_config:
  enabled: true
  storage_path: "./outputs/{TASK}/events"
  
  subscriptions:
    critical:  # Immediate action required
      - "agent.blocked"
      - "confidence.critical_drop"
      - "quality.regression"
      - "security.issue"
    
    monitoring:  # Track progress
      - "agent.confidence.*"
      - "phase.*"
      - "performance.*"
    
    analytics:  # Post-processing
      - "workflow.*"
      - "decision.*"
      - "evaluation.*"
  
  plugins:
    - name: "performance_monitor"
      config:
        sample_rate: 1000ms
        metrics: ["memory", "cpu", "api_calls"]
    
    - name: "slack_notifier"
      enabled: false
      config:
        webhook: "${SLACK_WEBHOOK}"
        events: ["workflow.failed", "quality.regression"]
```

### Quality Requirements
```yaml
quality_config:
  target_score: 90  # Default threshold
  max_iterations: 5
  
  # Dimension-specific minimums
  minimum_scores:
    quality: 85
    performance: 80
    security: 90
    confidence: 75
  
  # Automatic actions based on scores
  score_actions:
    below_50: "halt_and_reassess"
    50_70: "major_iteration_required"
    70_85: "targeted_improvements"
    85_90: "minor_polish"
    above_90: "approve"
  
  # Special requirements
  requirements:
    - "All public APIs must have documentation"
    - "Memory safety must be formally verified"
    - "Performance benchmarks required"
    - "Thread safety analysis mandatory"
```

## Success Criteria
1. **Functional Requirements**
   - [Specific measurable outcome 1]
   - [Specific measurable outcome 2]
   - [Specific measurable outcome 3]

2. **Performance Requirements**
   - [Metric 1: e.g., <1ms latency for core operations]
   - [Metric 2: e.g., Memory usage <50MB]
   - [Metric 3: e.g., 1M+ operations/second]

3. **Quality Requirements**
   - Code coverage: >90%
   - Documentation: Complete API docs
   - Examples: Working sample code
   - Tests: Unit, integration, performance

4. **Security Requirements**
   - Memory safety: Verified
   - Thread safety: Proven
   - Input validation: Complete
   - Error handling: No information leakage

## Workflow Decision Matrix

### Parallelism Strategy
The orchestrator should decide parallelism based on:

| Complexity | Confidence Req. | Risk | Specialists |
|------------|----------------|------|-------------|
| Low        | >85%          | Low  | 1           |
| Medium     | >80%          | Med  | 1-2         |
| High       | >75%          | High | 2-3         |
| Critical   | >70%          | Crit | 2-3 + review|

### Iteration Strategy
- **Fast Iterations**: For exploratory tasks
- **Careful Iterations**: For critical components
- **Progressive Enhancement**: Start simple, add complexity
- **Parallel Exploration**: Multiple approaches simultaneously

## Task-Specific Context
[Add any additional context specific to your task, such as:]
- Existing code patterns to follow
- Performance benchmarks to beat
- Security requirements to meet
- API compatibility constraints
- Platform-specific considerations

## Resource Allocation
```yaml
resources:
  time_budget: "2 hours"     # Estimated completion time
  api_budget: "unlimited"    # API call limits
  
  compute_resources:
    cpu_cores: 8             # For parallel testing
    memory_gb: 16            # For large datasets
    gpu_required: true       # For Metal shaders
  
  external_resources:
    documentation: ["link1", "link2"]
    example_code: ["repo1", "repo2"]
    benchmarks: ["suite1", "suite2"]
```

## Output Specifications
```yaml
outputs:
  code:
    format: "swift"
    style_guide: "apple"
    organization: "feature_modules"
  
  documentation:
    format: "markdown"
    sections: ["overview", "api", "examples", "performance"]
    
  tests:
    framework: "swift-testing"
    coverage_minimum: 90
    types: ["unit", "integration", "performance"]
    
  deliverables:
    - implementation_files/
    - documentation/
    - tests/
    - benchmarks/
    - examples/
```

## Shared Resources
- All agents receive this enhanced context.md file
- Runtime outputs go to `./devdocs-claude/outputs/[TASK]_[TIMESTAMP]/`
- Checkpoints stored in designated checkpoint directory
- Events logged to event storage with configured retention
- Each phase creates separate directories for tracking iteration history

## Notes
- The enhanced configuration supports the checkpoint, confidence, and event systems
- Specialists will self-assess confidence and publish events
- The orchestrator will manage checkpoints and respond to confidence changes
- The evaluator will perform multi-dimensional assessment with confidence validation