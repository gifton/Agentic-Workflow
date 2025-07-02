# Confidence Metrics Framework

## Overview
The confidence metrics system enables agents to self-assess their outputs, triggering dynamic workflow adjustments based on uncertainty levels. This creates a more intelligent and adaptive system that knows when to ask for help.

## Core Concepts

### Confidence Scale
```markdown
0-100 Scale Definition:
- 95-100: Absolute certainty, proven correct
- 85-94: High confidence, minimal uncertainty  
- 75-84: Good confidence, some assumptions made
- 65-74: Moderate confidence, several unknowns
- 50-64: Low confidence, significant uncertainty
- 0-49: Very low confidence, mostly guessing

Calibration Rule: Agents should be neither overconfident nor underconfident.
```

### Multi-Dimensional Confidence
```swift
struct ConfidenceMetrics {
    let overall: Double              // 0-100 aggregate score
    let dimensions: [String: Double] // Component scores
    let factors: [ConfidenceFactor]  // What influenced the score
    let uncertainty: [String]        // Specific areas of doubt
}

struct ConfidenceFactor {
    let description: String
    let impact: Double    // -50 to +50
    let category: FactorCategory
}

enum FactorCategory {
    case knowledge      // Domain expertise
    case information   // Available data
    case complexity    // Task difficulty
    case ambiguity     // Requirement clarity
    case risk          // Potential for errors
}
```

## Agent-Specific Implementation

### Specialist (Mercury) Confidence

#### Self-Assessment Protocol
```markdown
## How Mercury Calculates Confidence

1. **Knowledge Assessment** (0-25 points)
   - Do I have expertise in this domain? (+25)
   - Is this a familiar pattern/problem? (+20)
   - Am I using well-tested solutions? (+15)
   - Am I extrapolating beyond my training? (-20)

2. **Information Completeness** (0-25 points)
   - Are all requirements clear? (+25)
   - Do I have all necessary context? (+20)
   - Are there missing dependencies? (-15)
   - Am I making assumptions? (-10 per assumption)

3. **Implementation Quality** (0-25 points)
   - Is my solution elegant and simple? (+25)
   - Have I handled edge cases? (+20)
   - Are there potential bugs? (-15)
   - Did I use hacky workarounds? (-20)

4. **Testing & Validation** (0-25 points)
   - Do I have comprehensive tests? (+25)
   - Did all tests pass? (+20)
   - Can I prove correctness? (+15)
   - Are there untested paths? (-20)
```

#### Confidence Output Format
```markdown
## Confidence Report

### Overall Confidence: 78/100

### Dimension Breakdown:
- Knowledge: 22/25 (Swift concurrency expertise)
- Information: 18/25 (Some API details assumed)
- Implementation: 20/25 (Clean but one complex section)
- Validation: 18/25 (Good tests, missing edge cases)

### Confidence Factors:
- [+20] Strong expertise in actor isolation
- [+15] Used proven concurrent patterns
- [-10] Uncertain about memory pressure behavior
- [-8] Missing performance benchmarks
- [-5] Assumed thread pool configuration

### Specific Uncertainties:
1. How does the system behave under extreme load?
2. Are there race conditions in the error path?
3. What's the actual memory overhead?

### Recommendation:
Confidence is MODERATE-HIGH. Suggest specialist review of:
- Memory pressure handling
- Performance under load
- Error path thread safety
```

### Orchestrator (Atlas) Confidence Aggregation

#### Aggregation Strategy
```swift
func aggregateConfidence(specialists: [SpecialistReport]) -> WorkflowConfidence {
    // Weighted average based on task criticality
    let weights = specialists.map { report in
        switch report.taskCriticality {
        case .critical: return 2.0
        case .high: return 1.5
        case .standard: return 1.0
        case .low: return 0.7
        }
    }
    
    // Calculate weighted confidence
    let weightedSum = zip(specialists, weights).reduce(0.0) { sum, pair in
        sum + (pair.0.confidence.overall * pair.1)
    }
    let totalWeight = weights.reduce(0, +)
    let aggregated = weightedSum / totalWeight
    
    // Apply uncertainty propagation
    let uncertaintyPenalty = calculateUncertaintyPenalty(specialists)
    let final = max(0, aggregated - uncertaintyPenalty)
    
    return WorkflowConfidence(
        overall: final,
        specialistScores: specialists.map { ($0.id, $0.confidence.overall) },
        criticalIssues: identifyCriticalIssues(specialists),
        recommendation: determineAction(final)
    )
}
```

#### Dynamic Response to Low Confidence
```markdown
## Orchestrator Confidence Actions

### Confidence >= 85: Proceed Normally
- Continue to evaluation phase
- No additional specialists needed

### Confidence 75-84: Minor Adjustments  
- Flag for careful evaluation
- Consider targeted review
- Document assumptions

### Confidence 65-74: Spawn Support Specialist
- Launch additional specialist for uncertain areas
- Focus on specific uncertainty points
- Require consensus between specialists

### Confidence 50-64: Major Intervention
- Spawn multiple specialists
- Request human review option
- Implement defensive strategies
- Increase test coverage requirements

### Confidence < 50: Workflow Halt
- Stop current approach
- Analyze why confidence is low
- Consider alternative strategies
- Escalate to human operator
```

### Evaluator (Apollo) Confidence Validation

#### Confidence Calibration Check
```markdown
## Apollo Confidence Validation

1. **Historical Calibration**
   - Compare claimed confidence with actual outcomes
   - Track over/under confidence patterns
   - Adjust for agent biases

2. **Cross-Validation**
   - Compare confidence with complexity metrics
   - Validate against similar past tasks
   - Check for confidence/quality correlation

3. **Red Flag Detection**
   - High confidence + high complexity = suspicious
   - Low confidence + simple task = needs investigation  
   - Sudden confidence changes = potential issue

4. **Feedback Integration**
   ```
   if specialist.confidence >= 90 && quality_score < 80:
       feedback.append("Overconfidence detected - calibration needed")
       adjusted_confidence = specialist.confidence * 0.8
   ```
```

## Integration with Workflow

### Pre-Task Confidence
```yaml
# In context.md
confidence_requirements:
  minimum_acceptable: 75
  auto_spawn_threshold: 70
  human_review_threshold: 60
  halt_threshold: 50
  
confidence_weights:
  security_critical: 2.0
  performance_critical: 1.5
  functional: 1.0
  cosmetic: 0.5
```

### Runtime Confidence Tracking
```json
{
  "phase": 2,
  "timestamp": "2024-01-02T15:45:00Z",
  "specialist_confidence": {
    "mercury_1": {
      "overall": 82,
      "trend": "increasing",
      "dimensions": {
        "knowledge": 90,
        "information": 75,
        "implementation": 85,
        "validation": 78
      }
    },
    "mercury_2": {
      "overall": 71,
      "trend": "stable",
      "dimensions": {
        "knowledge": 68,
        "information": 70,
        "implementation": 75,
        "validation": 72
      }
    }
  },
  "workflow_confidence": 78.5,
  "action_taken": "continue_with_monitoring"
}
```

## Confidence Improvement Strategies

### For Specialists
1. **Ask Specific Questions**
   ```markdown
   I need clarification on:
   - Expected behavior under memory pressure
   - Preferred error handling strategy
   - Performance requirements (specific numbers)
   ```

2. **Incremental Validation**
   ```markdown
   Building confidence through:
   - Unit test: confidence +5
   - Integration test: confidence +8
   - Benchmark passes: confidence +10
   - Peer review: confidence +7
   ```

3. **Documentation as Confidence**
   ```markdown
   Confidence boosters:
   - Found official docs: +15
   - Verified with example: +10
   - Confirmed with test: +12
   ```

### For Orchestrators
1. **Specialist Pairing**
   - Pair low-confidence specialist with high-confidence one
   - Cross-validate outputs
   - Learn from confidence patterns

2. **Iterative Refinement**
   - Start with low-confidence prototype
   - Incrementally improve with feedback
   - Track confidence growth

3. **Domain Expert Consultation**
   - Identify low-confidence domains
   - Request specialized expertise
   - Build confidence through knowledge

## Monitoring & Analytics

### Confidence Metrics Dashboard
```yaml
real_time_metrics:
  - current_workflow_confidence
  - specialist_confidence_distribution
  - confidence_trend_analysis
  - uncertainty_hotspots
  
historical_analytics:
  - confidence_calibration_accuracy
  - confidence_outcome_correlation  
  - per_agent_confidence_bias
  - domain_confidence_patterns
```

### Confidence Report Generation
```markdown
## Weekly Confidence Analytics Report

### Summary Statistics
- Average Specialist Confidence: 79.3%
- Confidence Calibration Error: ±5.2%
- Workflows Halted (Low Confidence): 2
- Additional Specialists Spawned: 7

### Key Insights
1. Cryptography tasks show 15% lower confidence
2. Mercury_1 tends to be overconfident (+8%)
3. Confidence improves 12% after first iteration

### Recommendations
1. Additional training on cryptographic patterns
2. Adjust Mercury_1 confidence by -8% factor
3. Consider two-phase approach for complex tasks
```

## Best Practices

1. **Honest Assessment**
   - Better to underestimate than overestimate
   - Document all assumptions
   - Flag uncertainties early

2. **Confidence Building**
   - Start with what you know
   - Build incrementally
   - Validate assumptions

3. **Confidence Communication**
   - Be specific about uncertainties
   - Explain confidence factors
   - Suggest mitigation strategies

4. **Continuous Calibration**
   - Track prediction accuracy
   - Adjust for biases
   - Learn from mistakes