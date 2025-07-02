# Checkpoint System Design

## Overview
The checkpoint system provides state persistence, crash recovery, and workflow resumption capabilities for the Agentic Loop framework. It ensures no work is lost and enables time-travel debugging.

## Architecture

### Checkpoint Structure
```swift
struct WorkflowCheckpoint {
    let id: UUID
    let timestamp: Date
    let phase: Int
    let agentStates: [AgentID: AgentState]
    let decisions: [Decision]
    let outputs: [Output]
    let metrics: WorkflowMetrics
    let confidence: ConfidenceSnapshot
}

struct AgentState {
    let agentType: AgentType
    let status: AgentStatus
    let internalState: Data  // Serialized agent-specific state
    let confidence: Double
    let blockers: [String]
}

struct Decision {
    let timestamp: Date
    let agent: AgentID
    let description: String
    let rationale: String
    let confidence: Double
    let alternatives: [String]
}
```

## Implementation

### Checkpoint Manager
```markdown
## Checkpoint Manager Responsibilities

1. **State Serialization**
   - Capture complete workflow state
   - Compress large data structures
   - Encrypt sensitive information
   - Version checkpoint format

2. **Storage Strategy**
   - File-based storage in `outputs/[TASK]/checkpoints/`
   - Naming: `checkpoint_phase{N}_{timestamp}.json`
   - Automatic cleanup of old checkpoints
   - Configurable retention policy

3. **Recovery Protocol**
   - Scan for latest valid checkpoint
   - Validate checkpoint integrity
   - Restore agent states
   - Resume workflow execution
   - Replay decisions if needed

4. **Performance Optimization**
   - Asynchronous checkpoint writing
   - Incremental checkpointing
   - Memory-mapped files for large states
   - Checkpoint compression
```

### Checkpoint Triggers
```yaml
automatic_triggers:
  - phase_completed
  - specialist_finished
  - evaluation_completed
  - confidence_threshold_crossed
  - error_encountered
  - memory_pressure_high

manual_triggers:
  - user_requested
  - debug_breakpoint
  - before_risky_operation
```

### Recovery Scenarios

#### Scenario 1: Clean Shutdown
```markdown
1. Save final checkpoint with status: "completed"
2. Include all outputs and metrics
3. Mark workflow as resumable: false
```

#### Scenario 2: Crash Recovery
```markdown
1. On startup, check for incomplete workflows
2. Load most recent checkpoint
3. Validate checkpoint integrity
4. Resume from last known good state
5. Log recovery event
```

#### Scenario 3: Partial Failure
```markdown
1. Detect specialist failure
2. Save checkpoint with failure context
3. Attempt specialist restart
4. If recovery fails, rollback to previous checkpoint
5. Adjust confidence scores
```

## Checkpoint File Format

### JSON Structure
```json
{
  "version": "1.0",
  "checkpoint_id": "550e8400-e29b-41d4-a716-446655440000",
  "workflow_id": "task_20240102_143022",
  "timestamp": "2024-01-02T14:35:22Z",
  "phase": 2,
  "status": "in_progress",
  "agents": {
    "atlas": {
      "status": "active",
      "confidence": 0.92,
      "last_decision": "spawn_additional_specialist",
      "state": "base64_encoded_state"
    },
    "mercury_1": {
      "status": "completed",
      "confidence": 0.87,
      "output_ref": "phase2/specialist_1_output.md",
      "state": "base64_encoded_state"
    }
  },
  "decisions": [
    {
      "timestamp": "2024-01-02T14:33:10Z",
      "agent": "atlas",
      "type": "workflow_adjustment",
      "description": "Spawned additional specialist due to low confidence",
      "rationale": "Mercury_1 confidence (0.73) below threshold (0.75)",
      "alternatives_considered": ["request_human_review", "proceed_with_low_confidence"]
    }
  ],
  "metrics": {
    "elapsed_time": 185.4,
    "api_calls": 42,
    "tokens_used": 18500,
    "memory_peak": 512.3
  }
}
```

## Integration Points

### Orchestrator Integration
```markdown
## Atlas Checkpoint Hooks

1. **Before Phase Start**
   ```
   checkpoint_manager.create_checkpoint(phase: current_phase, type: .phase_start)
   ```

2. **After Specialist Launch**
   ```
   checkpoint_manager.update_agent_state(agent: specialist_id, state: .launched)
   ```

3. **On Decision Made**
   ```
   checkpoint_manager.record_decision(
     decision: Decision(
       description: "Allocated sub-task to specialist",
       rationale: "Task complexity requires parallel processing",
       confidence: 0.88
     )
   )
   ```

4. **On Recovery**
   ```
   if let checkpoint = checkpoint_manager.load_latest() {
     restore_workflow_state(from: checkpoint)
     resume_from_phase(checkpoint.phase)
   }
   ```
```

### Specialist Integration
```markdown
## Mercury Checkpoint Support

1. **State Serialization**
   - Export current task progress
   - Include partial outputs
   - Save confidence history
   - Record encountered blockers

2. **State Restoration**
   - Load previous progress
   - Resume from last milestone
   - Restore confidence metrics
   - Continue with assigned task
```

### Evaluator Integration
```markdown
## Apollo Checkpoint Awareness

1. **Evaluation State**
   - Save partial scores
   - Record identified issues
   - Checkpoint feedback generation
   - Track iteration history

2. **Recovery Behavior**
   - Resume evaluation from checkpoint
   - Recalculate scores if needed
   - Maintain evaluation consistency
```

## Configuration

### Checkpoint Settings
```yaml
checkpoint_config:
  enabled: true
  storage_path: "./outputs/{TASK}/checkpoints"
  compression: true
  encryption: true
  retention_days: 30
  max_checkpoints_per_phase: 5
  checkpoint_size_limit_mb: 100
  
recovery_config:
  auto_recovery: true
  max_recovery_attempts: 3
  recovery_timeout_seconds: 300
  fallback_to_previous: true
  
performance_config:
  async_writes: true
  batch_decisions: true
  compression_level: 6
  memory_mapped_threshold_mb: 10
```

## Best Practices

1. **Checkpoint Frequency**
   - Balance between safety and performance
   - More frequent for critical operations
   - Less frequent for stable workflows

2. **State Minimization**
   - Only checkpoint essential state
   - Use references for large outputs
   - Compress repetitive data

3. **Integrity Verification**
   - Checksum validation
   - Version compatibility checks
   - Corruption detection

4. **Privacy & Security**
   - Encrypt sensitive data
   - Sanitize credentials
   - Audit checkpoint access

## Monitoring & Debugging

### Checkpoint Metrics
```yaml
metrics_to_track:
  - checkpoint_write_duration
  - checkpoint_size
  - recovery_success_rate
  - checkpoint_frequency
  - storage_usage
```

### Debug Commands
```bash
# List all checkpoints
./debug.sh list-checkpoints --task=example_task

# Validate checkpoint
./debug.sh validate-checkpoint --file=checkpoint_phase2_20240102.json

# Replay from checkpoint
./debug.sh replay --checkpoint=550e8400-e29b-41d4-a716-446655440000

# Compare checkpoints
./debug.sh diff-checkpoints --from=phase1 --to=phase2
```

## Future Enhancements

1. **Distributed Checkpointing**
   - Cloud storage integration
   - Multi-region replication
   - Checkpoint streaming

2. **Smart Checkpointing**
   - ML-based checkpoint timing
   - Predictive state capture
   - Anomaly detection

3. **Checkpoint Analytics**
   - Workflow pattern analysis
   - Performance optimization
   - Failure prediction