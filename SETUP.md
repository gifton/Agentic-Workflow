# 🚀 Agentic Workflow - Setup Guide

## Quick Setup (Recommended)

### 1. Copy the Workflow File
```bash
# For Agentic Natural (recommended)
cp agentic-natural/workflow.md your-project/

# For other variants
cp devdocs-standard/templates/*.md your-project/.agentic/
```

### 2. Update Your CLAUDE.md

Add Agentic Workflow instructions to your project's `CLAUDE.md` file:

```bash
# Option 1: Copy our template (recommended)
cp templates/CLAUDE.md.example your-project/CLAUDE.md
# Then customize for your project

# Option 2: Add minimal version
echo "## Agentic Workflow
This project uses Agentic Natural. Check workflow.md for structured tasks.
Commands: 'agentic natural [for ...] [with ...]'" >> your-project/CLAUDE.md
```

Or manually add:

```markdown
## Agentic Workflow Integration

This project uses the Agentic Workflow system for complex tasks. When I mention "agentic workflow" or you see workflow.md:

1. Look for `workflow.md` in the project root
2. Follow the structured multi-agent approach defined there
3. Use the confidence tracking system (0-100 scale)
4. Update progress inline as you work

### Natural Language Commands
- "agentic natural" - Use the adaptive workflow
- "agentic natural for [type] with [features]" - Customize the workflow
- See workflow.md for the full command syntax

### Workflow Location
Primary: ./workflow.md
Fallback: ./.agentic/workflow.md
```

### 3. First Use

Tell your AI assistant:
```
"Use the agentic natural workflow in workflow.md for this task"
```

## Alternative Setup Options

### Option A: Global CLAUDE.md (For All Projects)

Add to `~/.claude/CLAUDE.md`:

```markdown
## Global Agentic Workflow Support

When working on any project, check for Agentic Workflow files:
- Look for `workflow.md` in project root
- Check `.agentic/` directory for workflow templates
- If found, follow the multi-agent structured approach

Common patterns:
- "agentic natural" → Adaptive workflow
- "use agentic workflow" → Look for workflow files
- Confidence tracking: 0-100 scale
```

### Option B: Project-Specific Directory

Create a dedicated directory:
```bash
mkdir your-project/.agentic
cp agentic-natural/workflow.md your-project/.agentic/
echo "Check .agentic/ for workflow templates" >> your-project/CLAUDE.md
```

### Option C: Inline Reminder

For one-off usage without setup, simply tell the AI:

```
"I have an Agentic Workflow file at workflow.md. Please read it and follow 
the multi-agent structured approach with confidence tracking for this task."
```

## Best Practices

### 1. Large Codebases
For projects with many files, be explicit:

```markdown
# In CLAUDE.md
IMPORTANT: This large codebase uses Agentic Workflow. 
Always check for workflow.md before starting complex tasks.
Priority files:
- workflow.md (Agentic Natural workflow)
- .agentic/*.md (Workflow templates)
```

### 2. Team Projects
Ensure consistency across team:

```bash
# Add to your project's README
## Development Process
We use Agentic Workflow for complex features. 
See workflow.md for our structured approach.

Quick start:
`agentic natural for feature with testing`
```

### 3. CI/CD Integration
Add a check to ensure workflow files exist:

```yaml
# .github/workflows/check-agentic.yml
- name: Verify Agentic Workflow
  run: |
    if [ ! -f "workflow.md" ]; then
      echo "⚠️ workflow.md missing. Copy from agentic-natural/"
      exit 1
    fi
```

## Troubleshooting

### AI Doesn't Recognize Workflow

If the AI doesn't pick up the workflow naturally:

1. **Be explicit first time:**
   ```
   "Read workflow.md and use the agentic natural approach"
   ```

2. **Add context to filename:**
   ```bash
   mv workflow.md AGENTIC-WORKFLOW.md
   ```

3. **Use clear headers:**
   ```markdown
   # AGENTIC NATURAL WORKFLOW - READ THIS FIRST
   <!-- AI Assistant: Follow this structured approach -->
   ```

### Workflow Not Found

If the AI can't find the workflow:

```
"The agentic workflow is in workflow.md in the project root. 
Please read it first, then follow the multi-agent approach."
```

### Confidence Tracking Issues

If confidence isn't being tracked:

```
"Remember to update confidence scores (0-100) as you complete 
each step in the workflow, as defined in workflow.md"
```

## Quick Reference Card

Print and keep handy:

```
┌─────────────────────────────────────────┐
│        AGENTIC WORKFLOW QUICK REF       │
├─────────────────────────────────────────┤
│ Setup:                                  │
│ 1. Copy workflow.md to project          │
│ 2. Add note to CLAUDE.md                │
│ 3. Say "use agentic natural"            │
│                                         │
│ Natural Commands:                       │
│ • agentic natural                       │
│ • for [what] with [features]            │
│ • optimized for [goal]                  │
│                                         │
│ Location Priority:                      │
│ 1. ./workflow.md                        │
│ 2. ./.agentic/workflow.md               │
│ 3. Explicitly tell AI the path          │
└─────────────────────────────────────────┘
```

## Next Steps

1. Choose your setup approach (Quick Setup recommended)
2. Copy the workflow file
3. Update CLAUDE.md
4. Try it: "agentic natural for API with testing"

Remember: The goal is to make the AI aware of the workflow system in your project context. Being explicit initially helps establish the pattern.