# Event-Driven Architecture

## Overview
The event system provides real-time workflow monitoring, asynchronous agent communication, and extensible integration points for the Agentic Loop framework. It enables reactive workflows that adapt to changing conditions.

## Event Architecture

### Core Event Types
```swift
enum WorkflowEvent {
    // Lifecycle Events
    case workflowStarted(id: String, context: Context)
    case workflowCompleted(id: String, result: Result)
    case workflowFailed(id: String, error: Error)
    case workflowPaused(id: String, reason: String)
    case workflowResumed(id: String)
    
    // Phase Events
    case phaseStarted(phase: Int, description: String)
    case phaseCompleted(phase: Int, outputs: [Output])
    case phaseIteration(phase: Int, iteration: Int)
    
    // Agent Events
    case agentSpawned(id: String, type: AgentType)
    case agentStatusChanged(id: String, status: AgentStatus)
    case agentConfidenceUpdated(id: String, confidence: Double)
    case agentOutputGenerated(id: String, output: Output)
    case agentBlocked(id: String, blockers: [String])
    
    // Decision Events
    case decisionMade(agent: String, decision: Decision)
    case decisionReverted(agent: String, reason: String)
    
    // Performance Events
    case performanceMetric(name: String, value: Double)
    case memoryPressure(level: MemoryPressureLevel)
    case apiRateLimitApproaching(remaining: Int)
    
    // Quality Events
    case qualityScoreCalculated(score: Double, details: QualityDetails)
    case qualityThresholdMet(score: Double)
    case qualityRegressionDetected(current: Double, previous: Double)
    
    // Custom Events
    case custom(name: String, data: [String: Any])
}
```

### Event Bus Implementation
```swift
actor EventBus {
    private var subscribers: [EventPattern: [EventHandler]] = [:]
    private var eventHistory: CircularBuffer<EventRecord> = CircularBuffer(capacity: 10000)
    private var filters: [EventFilter] = []
    
    func publish(_ event: WorkflowEvent) async {
        // Record event
        let record = EventRecord(
            id: UUID(),
            timestamp: Date(),
            event: event,
            metadata: captureMetadata()
        )
        eventHistory.append(record)
        
        // Apply filters
        guard passesFilters(event) else { return }
        
        // Notify subscribers
        await notifySubscribers(event)
        
        // Trigger reactions
        await processReactions(event)
    }
    
    func subscribe(pattern: EventPattern, handler: @escaping EventHandler) {
        subscribers[pattern, default: []].append(handler)
    }
    
    func query(predicate: EventPredicate, limit: Int = 100) -> [EventRecord] {
        eventHistory.filter(predicate).prefix(limit).map { $0 }
    }
}
```

## Event Patterns & Subscriptions

### Pattern Matching
```swift
enum EventPattern {
    case exact(WorkflowEvent)
    case type(String)                    // "agent.*"
    case regex(String)                   // "specialist.*.completed"
    case predicate((WorkflowEvent) -> Bool)
    case compound([EventPattern])        // AND/OR combinations
}

// Subscription Examples
eventBus.subscribe(pattern: .type("agent.*")) { event in
    logger.log("Agent event: \(event)")
}

eventBus.subscribe(pattern: .predicate({ event in
    if case .agentConfidenceUpdated(_, let confidence) = event {
        return confidence < 70
    }
    return false
})) { event in
    orchestrator.handleLowConfidence(event)
}
```

### Event Handlers
```markdown
## Handler Types

1. **Synchronous Handlers**
   - Logging and metrics collection
   - State updates
   - Quick validations

2. **Asynchronous Handlers**  
   - Checkpoint creation
   - External notifications
   - Heavy computations

3. **Reactive Handlers**
   - Workflow adjustments
   - Agent spawning
   - Error recovery

4. **Plugin Handlers**
   - Custom integrations
   - External tool triggers
   - Webhook notifications
```

## Integration Examples

### Orchestrator Event Integration
```swift
// Atlas event publishing
extension Orchestrator {
    func startWorkflow() async {
        await eventBus.publish(.workflowStarted(
            id: workflowId,
            context: context
        ))
        
        await eventBus.subscribe(pattern: .type("agent.blocked")) { [weak self] event in
            await self?.handleAgentBlocked(event)
        }
        
        await eventBus.subscribe(pattern: .type("quality.regression")) { [weak self] event in
            await self?.handleQualityRegression(event)
        }
    }
    
    func makeDecision(_ decision: Decision) async {
        await eventBus.publish(.decisionMade(
            agent: "atlas",
            decision: decision
        ))
        
        // Create checkpoint on important decisions
        if decision.importance == .critical {
            await checkpointManager.createCheckpoint(
                trigger: .importantDecision(decision)
            )
        }
    }
}
```

### Specialist Event Publishing
```swift
// Mercury event integration
extension Specialist {
    func updateConfidence(_ newConfidence: Double) async {
        await eventBus.publish(.agentConfidenceUpdated(
            id: agentId,
            confidence: newConfidence
        ))
        
        // Auto-spawn if confidence drops
        if newConfidence < config.autoSpawnThreshold {
            await eventBus.publish(.custom(
                name: "specialist.needs.assistance",
                data: [
                    "specialist": agentId,
                    "confidence": newConfidence,
                    "uncertainties": currentUncertainties
                ]
            ))
        }
    }
    
    func reportBlocker(_ blockers: [String]) async {
        await eventBus.publish(.agentBlocked(
            id: agentId,
            blockers: blockers
        ))
    }
}
```

### Evaluator Event Reactions
```swift
// Apollo event subscriptions
extension Evaluator {
    func setupEventHandlers() async {
        // React to specialist outputs
        await eventBus.subscribe(pattern: .type("agent.output")) { [weak self] event in
            if case .agentOutputGenerated(let id, let output) = event {
                await self?.queueForEvaluation(agentId: id, output: output)
            }
        }
        
        // Monitor confidence trends
        await eventBus.subscribe(pattern: .type("agent.confidence")) { [weak self] event in
            await self?.updateConfidenceTrends(event)
        }
    }
    
    func publishEvaluation(_ result: EvaluationResult) async {
        await eventBus.publish(.qualityScoreCalculated(
            score: result.score,
            details: result.details
        ))
        
        if result.score >= config.targetScore {
            await eventBus.publish(.qualityThresholdMet(score: result.score))
        }
    }
}
```

## Event-Driven Workflows

### Reactive Patterns
```yaml
reactive_rules:
  - trigger: agent.confidence.updated
    condition: confidence < 70
    action: spawn_support_specialist
    
  - trigger: phase.completed
    condition: always
    action: create_checkpoint
    
  - trigger: memory.pressure.high
    condition: level > 0.8
    action: pause_workflow_and_gc
    
  - trigger: quality.regression.detected
    condition: regression > 10
    action: rollback_to_checkpoint
    
  - trigger: agent.blocked
    condition: duration > 5_minutes
    action: escalate_to_human
```

### Event Correlation
```swift
// Complex event processing
class EventCorrelator {
    func detectPatterns() async {
        // Detect cascading failures
        let recentFailures = await eventBus.query(
            predicate: { event in
                if case .agentStatusChanged(_, .failed) = event {
                    return true
                }
                return false
            },
            limit: 10
        )
        
        if recentFailures.count > 3 {
            await eventBus.publish(.custom(
                name: "workflow.cascading.failure",
                data: ["failure_count": recentFailures.count]
            ))
        }
        
        // Detect performance degradation
        let perfEvents = await eventBus.query(
            predicate: { event in
                if case .performanceMetric = event {
                    return true
                }
                return false
            }
        )
        
        if detectDegradation(in: perfEvents) {
            await eventBus.publish(.custom(
                name: "performance.degradation.detected",
                data: ["metrics": perfEvents]
            ))
        }
    }
}
```

## Event Storage & Querying

### Event Persistence
```swift
struct EventRecord: Codable {
    let id: UUID
    let timestamp: Date
    let event: WorkflowEvent
    let metadata: EventMetadata
}

struct EventMetadata: Codable {
    let workflowId: String
    let phase: Int
    let memoryUsage: Double
    let apiCalls: Int
    let customData: [String: String]
}

// Storage Strategy
class EventStore {
    func persist(_ record: EventRecord) async {
        // Write to append-only log
        await logFile.append(record)
        
        // Index for fast queries
        await index.add(record)
        
        // Archive old events
        if shouldArchive() {
            await archiveOldEvents()
        }
    }
}
```

### Query Interface
```swift
// Event query DSL
let query = EventQuery.builder()
    .type("agent.confidence.updated")
    .where("confidence", .lessThan, 75)
    .timeRange(from: .now.addingHours(-1), to: .now)
    .limit(50)
    .build()

let results = await eventStore.execute(query)
```

## Event Analytics

### Real-time Dashboard
```yaml
dashboard_widgets:
  - name: "Workflow Progress"
    events: ["phase.*", "workflow.*"]
    visualization: timeline
    
  - name: "Agent Confidence"
    events: ["agent.confidence.*"]
    visualization: line_chart
    
  - name: "Quality Trends"
    events: ["quality.*"]
    visualization: gauge
    
  - name: "Performance Metrics"
    events: ["performance.*"]
    visualization: heatmap
    
  - name: "Error Rate"
    events: ["*.failed", "*.error"]
    visualization: counter
```

### Event Stream Processing
```swift
// Real-time event analytics
class EventAnalyzer {
    func analyzeStream() -> AsyncStream<EventInsight> {
        AsyncStream { continuation in
            Task {
                await eventBus.subscribe(pattern: .type("*")) { event in
                    let insight = analyze(event)
                    continuation.yield(insight)
                }
            }
        }
    }
    
    func analyze(_ event: WorkflowEvent) -> EventInsight {
        // Pattern detection
        // Anomaly detection
        // Trend analysis
        // Performance impact
    }
}
```

## Plugin System

### Plugin Interface
```swift
protocol EventPlugin {
    var name: String { get }
    var version: String { get }
    var subscribedPatterns: [EventPattern] { get }
    
    func initialize(eventBus: EventBus) async
    func handleEvent(_ event: WorkflowEvent) async
    func shutdown() async
}

// Example Plugin
class SlackNotificationPlugin: EventPlugin {
    let name = "slack_notifier"
    let version = "1.0.0"
    let subscribedPatterns: [EventPattern] = [
        .type("workflow.failed"),
        .type("quality.regression.detected"),
        .predicate { event in
            if case .agentConfidenceUpdated(_, let conf) = event {
                return conf < 50
            }
            return false
        }
    ]
    
    func handleEvent(_ event: WorkflowEvent) async {
        let message = formatEventMessage(event)
        await slackClient.send(message)
    }
}
```

### Plugin Management
```yaml
plugins:
  enabled:
    - slack_notifier
    - datadog_metrics
    - github_integration
    - opentelemetry_exporter
    
  config:
    slack_notifier:
      webhook_url: "${SLACK_WEBHOOK}"
      channel: "#agentic-alerts"
      
    datadog_metrics:
      api_key: "${DD_API_KEY}"
      tags: ["env:prod", "service:agentic"]
```

## Performance Considerations

### Event Bus Optimization
```yaml
performance_config:
  event_buffer_size: 10000
  async_handlers: true
  batch_notifications: true
  compression: true
  
  rate_limiting:
    enabled: true
    max_events_per_second: 1000
    burst_capacity: 5000
    
  filtering:
    early_filtering: true
    compiled_patterns: true
    pattern_cache_size: 100
```

### Best Practices
1. **Event Naming**: Use hierarchical names (agent.confidence.updated)
2. **Event Size**: Keep event payloads small, use references for large data
3. **Handler Performance**: Keep synchronous handlers fast (<1ms)
4. **Error Handling**: Never let handler errors crash the event bus
5. **Testing**: Use event replay for integration testing

## Monitoring & Debugging

### Event Bus Metrics
```yaml
metrics_to_track:
  - events_published_per_second
  - event_processing_latency
  - handler_execution_time
  - event_queue_depth
  - pattern_match_performance
  - plugin_error_rate
```

### Debug Tools
```bash
# Tail events in real-time
./debug.sh tail-events --pattern="agent.*"

# Replay events
./debug.sh replay-events --from="2024-01-02T10:00:00" --speed=2x

# Analyze event patterns
./debug.sh analyze-events --window=1h --report=patterns

# Test event handling
./debug.sh simulate-event --type="agent.blocked" --data='{"id":"test","blockers":["API"]}'
```