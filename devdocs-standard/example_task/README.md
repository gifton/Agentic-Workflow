# Example Task: Rate Limiter Implementation

This example demonstrates the Standard Agentic Workflow in action with a practical backend task.

## Why This Example?

The rate limiter task is perfect because it:
- Has clear requirements but multiple implementation approaches
- Requires both algorithmic thinking and practical engineering
- Needs thread safety considerations
- Is complex enough to show iteration but simple enough to understand

## Expected Workflow

### Phase 1: Planning
Orchestrator will:
- Analyze the requirements
- Decide on 2 specialists (implementation + testing)
- Create clear work allocation

### Phase 2: Implementation
- Specialist 1: Implements core rate limiting algorithms
- Specialist 2: Creates comprehensive test suite
- Both report confidence levels

### Phase 3: Evaluation
Evaluator will likely find:
- Core functionality works (good!)
- May need better thread safety validation
- Performance benchmarks needed

### Phase 4: Iteration
Specialists address:
- Add concurrent stress tests
- Include performance benchmarks
- Improve documentation

### Phase 5: Completion
Final output includes:
- Working rate limiter implementation
- Comprehensive test suite
- Performance validation
- Usage documentation

## File Structure During Execution
```
outputs/rate_limiter_20240102/
├── phase_plan.json           # Orchestrator's plan
├── progress.json             # Workflow state
├── implementation_1.md       # Core rate limiter code
├── implementation_2.md       # Test suite
├── evaluation_1.json         # First evaluation
├── implementation_1_v2.md    # Updated after feedback
├── implementation_2_v2.md    # Updated tests
├── evaluation_2.json         # Second evaluation
└── final_output.md          # Consolidated result
```

## Key Learning Points

1. **Clear Requirements Help**: The specific requirements lead to better implementation
2. **Confidence Matters**: Specialists honestly report uncertainties
3. **Iteration Improves**: First attempt rarely perfect, iteration addresses specific issues
4. **Tests Are Critical**: Dedicated test specialist ensures quality

## Running This Example

1. Copy `context.md` to your working directory
2. Use the templates to guide each agent
3. Follow the standard workflow phases
4. Expect 1-2 iterations for HIGH quality

## Success Metrics
- Implementation works correctly ✓
- Thread safety proven ✓
- Performance validated ✓
- Well-tested (90%+ coverage) ✓
- Clear documentation ✓

This example shows how Standard workflow handles real-world tasks efficiently without unnecessary complexity.