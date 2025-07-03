# Standard Agentic Workflow System

A practical, production-ready implementation of the Agentic Loop framework that balances power with simplicity.

## Philosophy
"Everything you need, nothing you don't" - Focused on getting real work done without unnecessary complexity.

## What's Different from Advanced?

### Simplified ✨
- **Progress Tracking**: Simple JSON files instead of complex checkpoints
- **Confidence**: Three levels (HIGH/MEDIUM/LOW) instead of 0-100 scores
- **Communication**: Direct file-based instead of event bus
- **Configuration**: ~50 lines instead of 200+

### Removed 🚫
- Checkpoint encryption/compression
- Time-travel debugging
- Event system with plugins
- Dynamic agent spawning
- Swarm mode
- Multi-dimensional confidence scoring

### Kept ✅
- Three-agent architecture (Orchestrator, Specialist, Evaluator)
- Phased workflow with iterations
- Quality-based approval
- Clear task context
- Proven patterns

## Core Components

### 1. Simple Progress Tracking
```json
{
  "current_phase": 2,
  "phases_completed": ["planning", "implementation"],
  "current_status": "evaluating",
  "iteration": 1,
  "can_resume": true
}
```

### 2. Three-Level Confidence
- **HIGH**: Ready to proceed (80%+ equivalent)
- **MEDIUM**: Works but needs review (60-79% equivalent)
- **LOW**: Major issues, need help (<60% equivalent)

### 3. Phased Workflow
```
Plan → Implement → Evaluate → (Iterate if needed) → Complete
```

### 4. Direct Communication
Agents communicate through well-defined JSON files:
- `phase_plan.json` - Orchestrator's plan
- `implementation.md` - Specialist's output
- `evaluation.json` - Evaluator's assessment

## When to Use Standard vs Advanced

### Use Standard When:
- Building typical software projects
- Need reliable, predictable workflow
- Value simplicity over features
- Working with small-medium teams
- Don't need real-time monitoring

### Use Advanced When:
- Building mission-critical systems
- Need audit trails and recovery
- Require real-time event monitoring
- Managing complex multi-agent workflows
- Need enterprise features

## Directory Structure
```
devdocs-standard/
├── README.md              # This file
├── templates/             # Agent templates
│   ├── orchestrator.md    # Atlas - simplified
│   ├── specialist.md      # Mercury - focused
│   ├── evaluator.md       # Apollo - practical
│   └── context.md         # Task configuration
└── example_task/          # Example implementation
    ├── context.md         # Task definition
    └── README.md          # Task documentation
```

## Quick Start

### 1. Define Your Task
Create a `context.md` with:
- Clear task description
- Success criteria
- Any constraints

### 2. Run the Workflow
- Orchestrator reads context and creates plan
- Specialists implement based on plan
- Evaluator assesses quality
- Iterate until quality target met

### 3. Configuration Example
```yaml
# Simple, focused configuration
task:
  name: "Build Authentication System"
  complexity: "medium"
  specialists: 2

quality:
  target: "HIGH"
  max_iterations: 3

workflow:
  save_progress: true
  verbose_output: false
```

## Key Principles

1. **Clarity Over Cleverness**: Easy to understand beats sophisticated
2. **Files Over Streams**: Simple file I/O instead of event systems
3. **Explicit Over Implicit**: Clear phase transitions
4. **Progress Over Perfection**: Ship working code, iterate as needed

## Migration Path

### From Zen (Too Simple)?
- Add phased workflow structure
- Implement basic evaluation loop
- Keep the simplicity philosophy

### From Advanced (Too Complex)?
- Remove event system
- Simplify to 3-level confidence
- Use basic JSON for state
- Eliminate dynamic features

### To Advanced (Need More)?
- Standard provides a solid foundation
- Add features incrementally
- Event system can be added later
- Checkpoint system is modular

## Example Workflow

```
1. Task: "Build rate limiter"
   
2. Orchestrator analyzes → Creates plan
   Output: phase_plan.json
   
3. Specialist implements → Writes code
   Output: implementation.md
   Confidence: MEDIUM
   
4. Evaluator reviews → Finds issues
   Output: evaluation.json
   Result: "Fix thread safety"
   
5. Specialist iterates → Fixes issues
   Confidence: HIGH
   
6. Evaluator approves → Task complete
```

## Benefits

- **Predictable**: Same workflow every time
- **Debuggable**: Clear file outputs at each step
- **Resumable**: Simple progress tracking
- **Understandable**: Can explain in 5 minutes
- **Reliable**: Fewer moving parts = fewer failures

The Standard implementation is the "Goldilocks" choice - not too simple, not too complex, just right for most development tasks!