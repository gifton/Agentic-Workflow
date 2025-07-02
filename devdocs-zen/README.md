# Zen-Enhanced Agentic Workflow

A streamlined, zen-integrated version of the Agentic Loop focused on simplicity and developer experience.

## Philosophy
- **Simple > Complex**: 80% value with 20% complexity
- **Zen-First**: Use zen-mcp analysis to boost confidence
- **Interactive**: Real-time feedback and debugging
- **Practical**: Remove theoretical features, focus on what works

## Quick Start

```bash
# One-line setup
echo "mode: swift\nzen: auto" > .agentic

# Run with zen analysis
agentic run "implement rate limiter" --zen

# Watch mode with live updates
agentic watch --confidence-view
```

## Core Features (Simplified)

### 1. Single Confidence Score
```yaml
confidence: 75/100
reason: "Uncertain about thread safety"
action: "Spawning concurrency expert"
```

### 2. Smart Checkpoints
- Auto-save on phase completion
- Simple JSON format
- One-command recovery

### 3. Zen Integration
```python
# Automatic zen analysis
def enhance_confidence(code):
    zen_report = zen.analyze(code)
    if zen_report.quality == "A":
        return confidence + 15
    return confidence
```

### 4. Visual Progress
```
Task: Auth System
█████████░░░░░░ 65% [🔍 Analyzing with Zen]

P: ✓ Planning (90%)
I: ⚠ Implementation (65%)
R: ○ Review (0%)
```

## Removed Complexity

❌ Multi-dimensional scoring
❌ Event pub/sub system  
❌ Checkpoint encryption
❌ Mythological names
❌ 200+ line configs
❌ Experimental features

## Enhanced Developer Experience

### Interactive Commands
```bash
agentic repl          # Interactive task mode
agentic explain       # Explain decisions
agentic optimize      # Run zen optimization
agentic shortcuts     # Show all shortcuts
```

### Zen-Powered Workflows
```yaml
workflows:
  secure_implementation:
    - zen: "analyze --security"
    - implement: "with security focus"
    - zen: "verify --no-vulnerabilities"
    
  performance_critical:
    - zen: "profile --baseline"
    - implement: "with benchmarks"
    - zen: "analyze --performance"
```

### Auto-Context Detection
```python
# Automatically detects and configures
project_context = {
    'language': 'Swift',
    'frameworks': ['SwiftUI', 'Combine'],
    'patterns': ['MVVM', 'Repository'],
    'focus': 'iOS app development'
}
```

## Integration Examples

### With GitHub
```bash
agentic pr "fix memory leak" --auto-commit --zen-review
```

### With VS Code
```json
{
  "agentic.showConfidence": true,
  "agentic.zenIntegration": "auto",
  "agentic.liveMode": true
}
```

### With CI/CD
```yaml
- name: Agentic Review
  run: |
    agentic review ${{ github.event.pull_request.head.sha }}
    agentic zen-check --fail-below 80
```

## Simple Configuration

```yaml
# .agentic (complete config)
mode: swift-systems
confidence: 
  min: 75
  auto_help: true
  
zen:
  pre_analyze: true
  validate: true
  
output:
  format: clean
  progress: visual
```

## Benefits

1. **Faster Start**: < 1 minute setup
2. **Less Cognitive Load**: Simple mental model
3. **Better Integration**: Works with existing tools
4. **Real Feedback**: See confidence in real-time
5. **Practical Focus**: Only features that developers actually use

## Getting Started

1. Install: `brew install agentic-zen`
2. Configure: `echo "mode: swift" > .agentic`
3. Run: `agentic run "your task"`

That's it! The system handles the complexity behind the scenes.