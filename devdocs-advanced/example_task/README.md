# Example Task: High-Performance Concurrent Cache

This example demonstrates the enhanced Agentic Loop system with checkpoint recovery, confidence metrics, and event-driven coordination.

## Task Overview

Implement a production-grade concurrent cache in Swift that showcases:
- Modern Swift concurrency (actors, async/await)
- High-performance design patterns
- Comprehensive testing and benchmarking
- Self-assessment and confidence tracking

## Why This Example?

This task was chosen because it:
1. **Requires Deep Expertise**: Memory management, concurrency, and performance
2. **Benefits from Parallelism**: Core implementation vs. optimization can be split
3. **Has Clear Metrics**: Performance can be measured objectively
4. **Tests Confidence System**: Complex enough to trigger uncertainty
5. **Showcases Recovery**: Long enough to benefit from checkpoints

## Enhanced Features Demonstrated

### 1. Checkpoint System
- Saves progress after each specialist completes work
- Enables recovery if workflow is interrupted
- Tracks decision rationale for learning

### 2. Confidence Metrics
- Specialists self-assess their implementations
- Low confidence triggers additional specialist
- Evaluator validates confidence claims

### 3. Event System
- Real-time progress monitoring
- Performance metrics collection
- Automatic reactions to issues

## Expected Workflow

### Phase 1: Initial Implementation
- Specialist 1: Actor-based cache core (Confidence: ~85%)
- Specialist 2: Eviction policies (Confidence: ~80%)
- Checkpoint created after completion

### Phase 2: Performance Optimization
- Address evaluator feedback
- Improve confidence through testing
- Event system tracks improvements

### Phase 3: Final Polish
- Achieve target performance metrics
- Complete documentation
- Final confidence validation

## Running the Example

1. **Initialize Workflow**
   ```bash
   # Copy templates to example_task directory
   # Customize context.md as needed
   # Launch orchestrator
   ```

2. **Monitor Progress**
   - Check `outputs/concurrent_cache_*/events/` for real-time updates
   - Review confidence scores in specialist outputs
   - Observe checkpoint creation

3. **Test Recovery**
   - Interrupt workflow mid-execution
   - Restart to see checkpoint recovery
   - Verify no work is lost

## Success Metrics

- **Quality Score**: >92/100
- **Performance**: <1μs read latency
- **Confidence**: Well-calibrated (±5%)
- **Iterations**: Complete in ≤3 iterations

## Learning Outcomes

This example teaches:
1. How confidence metrics improve quality
2. When checkpoints provide value
3. How events enable responsive workflows
4. Benefits of multi-dimensional evaluation

## Customization

To adapt for your use case:
1. Modify performance requirements
2. Adjust confidence thresholds
3. Change eviction policies required
4. Add platform-specific optimizations