# Agentic Loop Context: High-Performance Concurrent Cache

## Task Description
Implement a high-performance, thread-safe cache system in Swift that leverages modern concurrency features (actors, async/await) while maintaining excellent performance characteristics. The cache should support various eviction policies, provide strong consistency guarantees, and be optimized for Apple Silicon processors.

## Repository Configuration
- **Repository Path**: None (Generic implementation)
- **Target Framework**: Swift 6.1, Foundation, Dispatch
- **Platform**: macOS 14+, iOS 17+
- **Architecture Focus**: Apple Silicon (M1/M2/M3)
- **Dependencies**: None (Pure Swift implementation)

## Task Complexity Assessment
- **Estimated Complexity**: High
- **Domain Expertise Required**: 
  - Swift concurrency (actors, async/await, Sendable)
  - Memory management and optimization
  - Lock-free algorithms
  - Performance profiling
  - Cache algorithms (LRU, LFU, FIFO)
- **Performance Requirements**: 
  - Sub-microsecond read latency
  - 1M+ operations/second
  - Memory efficient with large datasets
- **Security Considerations**: 
  - Thread-safe operations
  - No memory leaks
  - Secure key hashing
- **Risk Level**: Medium-High

## Enhanced Configuration

### Specialist Configuration
```yaml
specialist_config:
  desired_parallelism: 2
  allocation_strategy: "dynamic"
  
  domains_required:
    - swift_systems     # Custom allocators, unsafe operations
    - concurrency      # Actor design, async sequences
    - performance      # SIMD for batch operations
    - algorithms       # Cache eviction strategies
    - testing          # Comprehensive test coverage

  expertise_level:
    minimum: "senior"
    preferred: "principal"
```

### Confidence Requirements
```yaml
confidence_config:
  minimum_acceptable: 80
  auto_spawn_threshold: 75
  human_review_threshold: 65
  halt_threshold: 50
  
  dimension_weights:
    quality: 0.35
    performance: 0.35
    security: 0.20
    confidence_calibration: 0.10
  
  critical_components:
    memory_management: 95
    thread_safety: 95
    actor_isolation: 90
    public_apis: 85
```

### Checkpoint Configuration
```yaml
checkpoint_config:
  enabled: true
  storage_path: "./outputs/concurrent_cache/checkpoints"
  
  triggers:
    automatic:
      - phase_complete
      - specialist_complete
      - confidence_drop
      - error_encountered
      - decision_made
    
  options:
    compression: true
    encryption: false
    retention_days: 30
    max_size_mb: 50
    
  recovery:
    auto_resume: true
    max_attempts: 3
    fallback_strategy: "previous_checkpoint"
```

### Event System Configuration
```yaml
event_config:
  enabled: true
  storage_path: "./outputs/concurrent_cache/events"
  
  subscriptions:
    critical:
      - "agent.blocked"
      - "confidence.critical_drop"
      - "quality.regression"
      - "performance.degradation"
    
    monitoring:
      - "agent.confidence.*"
      - "phase.*"
      - "performance.*"
      - "test.results"
    
    analytics:
      - "workflow.*"
      - "decision.*"
      - "evaluation.*"
  
  plugins:
    - name: "performance_monitor"
      config:
        sample_rate: 500ms
        metrics: ["memory", "cpu", "cache_hits"]
```

### Quality Requirements
```yaml
quality_config:
  target_score: 92
  max_iterations: 4
  
  minimum_scores:
    quality: 90
    performance: 88
    security: 92
    confidence: 80
  
  requirements:
    - "All public APIs must have comprehensive documentation"
    - "Thread safety must be proven with tests"
    - "Performance benchmarks must show sub-microsecond latency"
    - "Memory usage must be predictable and bounded"
    - "Support for at least 3 eviction policies"
```

## Success Criteria

1. **Functional Requirements**
   - Thread-safe cache with actor-based implementation
   - Support for LRU, LFU, and FIFO eviction policies
   - Async/await API with proper back-pressure handling
   - Batch operations for efficiency
   - Statistics and monitoring capabilities

2. **Performance Requirements**
   - Read latency: <1 microsecond (p99)
   - Write latency: <5 microseconds (p99)
   - Throughput: >1M operations/second
   - Memory overhead: <20% of stored data
   - CPU usage: Efficient use of available cores

3. **Quality Requirements**
   - Code coverage: >95%
   - Documentation: Complete API documentation with examples
   - Examples: Performance comparison demos
   - Tests: Unit, integration, stress, performance

4. **Security Requirements**
   - Memory safety: No unsafe operations without validation
   - Thread safety: Proven with concurrent stress tests
   - No memory leaks: Validated with instruments
   - Proper error handling: No panics or crashes

## Workflow Decision Matrix

Given the high complexity and performance requirements:
- Start with 2 specialists working on complementary aspects
- Specialist 1: Core cache implementation and actor design
- Specialist 2: Eviction policies and performance optimization
- Dynamic spawning if confidence drops below 75%

## Task-Specific Context

### Implementation Considerations
- Leverage Swift's actor model for thread safety
- Use copy-on-write for value semantics where appropriate
- Consider memory-mapped files for large caches
- Implement proper Sendable conformance
- Use continuation-based APIs for integration

### Performance Optimization Strategies
- SIMD operations for batch key comparisons
- Lock-free algorithms where possible
- Cache-line aware data structures
- Minimal allocations in hot paths
- Profile-guided optimization

### Testing Requirements
- Concurrent stress tests with 100+ threads
- Memory leak detection
- Performance regression tests
- Chaos testing for edge cases
- Benchmark against popular alternatives

## Resource Allocation
```yaml
resources:
  time_budget: "3 hours"
  api_budget: "unlimited"
  
  compute_resources:
    cpu_cores: 8
    memory_gb: 16
    gpu_required: false
  
  external_resources:
    documentation:
      - "https://developer.apple.com/documentation/swift/concurrency"
      - "https://github.com/apple/swift-evolution/blob/main/proposals/0306-actors.md"
    example_code:
      - "https://github.com/apple/swift-async-algorithms"
    benchmarks:
      - "https://github.com/apple/swift-collections-benchmark"
```

## Output Specifications
```yaml
outputs:
  code:
    format: "swift"
    style_guide: "swift.org"
    organization: "single_package"
  
  documentation:
    format: "markdown"
    sections: ["overview", "api_reference", "examples", "performance", "implementation_notes"]
    
  tests:
    framework: "swift-testing"
    coverage_minimum: 95
    types: ["unit", "integration", "performance", "stress"]
    
  deliverables:
    - Sources/ConcurrentCache/
    - Tests/ConcurrentCacheTests/
    - Documentation/
    - Benchmarks/
    - Examples/
```

## Shared Resources
- All agents receive this context.md file
- Runtime outputs go to `./devdocs-claude/outputs/concurrent_cache_[TIMESTAMP]/`
- Checkpoints enable recovery from any phase
- Events provide real-time progress monitoring
- Confidence tracking ensures quality outcomes