# Zen Agentic Template (Simplified)

## Task
[What needs to be built]

## Config
```yaml
mode: [swift|python|typescript|auto]
confidence_min: 75
zen_integration: true
```

## Agents (Simple Names)

### Planner
- Analyzes task with zen-mcp
- Creates simple plan
- Identifies uncertainties

### Implementer  
- Writes code
- Reports confidence (0-100)
- Asks for help if needed

### Reviewer
- Checks quality
- Runs zen analysis
- Simple PASS/RETRY decision

## Workflow

1. **Zen Pre-Analysis**
   ```bash
   zen analyze . --suggest-patterns
   ```

2. **Implementation**
   - Start with high-confidence parts
   - Flag uncertainties
   - Get help when confidence < 75

3. **Zen Validation**
   ```bash
   zen analyze output/ --verify
   ```

4. **Iterate if needed**
   - Focus on zen-identified issues
   - Boost confidence with evidence
   - Stop when quality > 90

## Checkpoints
- Simple JSON files
- Auto-save after each phase
- One command recovery

## Interactive Mode
```bash
agentic> run "implement cache"
Planning... [████████░░] 80%
Confidence: 72% ⚠️ 
Action: Getting help with thread safety

agentic> explain
The confidence dropped because the thread safety 
requirements are complex and I found conflicting 
patterns in the codebase.

agentic> zen-analyze
Running zen analysis...
Found: Race condition risk in proposed design
Suggestion: Use actor pattern instead

agentic> continue
Applying zen suggestions...
Confidence: 88% ✓
```

## Output Structure
```
output/
├── implementation.swift
├── tests.swift
├── confidence.json
├── zen-report.md
└── decisions.log
```

## Success Criteria
- Code works: ✓
- Tests pass: ✓
- Zen score: B+ or higher
- Confidence: 80+ sustained

That's it. No mythology, no complex scoring, just practical development assistance.