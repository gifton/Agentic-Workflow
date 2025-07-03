# Task: Build a Rate Limiter

## Task Description
Build a thread-safe rate limiter that can be used to limit API requests. The rate limiter should support multiple limiting strategies and be easy to integrate into existing web applications.

## Requirements
### Functional Requirements
- Support at least two rate limiting algorithms (Token Bucket and Fixed Window)
- Thread-safe implementation for concurrent requests
- Configurable limits (requests per time window)
- Per-user and per-IP limiting capabilities
- Clear API for easy integration

### Non-Functional Requirements
- Performance: Sub-millisecond overhead per check
- Memory efficient: O(1) memory per user
- Scalability: Handle 10k+ unique users
- Testable: Comprehensive test suite

## Success Criteria
1. All rate limiting algorithms work correctly
2. Thread safety verified with concurrent tests
3. Performance benchmarks show <1ms overhead
4. 90%+ test coverage achieved
5. Clear documentation with usage examples

## Configuration
```yaml
workflow:
  specialists: 2          # One for core logic, one for tests
  max_iterations: 3       
  target_quality: HIGH    

task:
  complexity: medium      
  domain: backend_service
  estimated_time: 3h     

output:
  format: markdown       
  include_tests: true    
  documentation: inline
```

## Constraints
- Must be implemented in Python
- Should not require external services (Redis, etc.)
- Must work with Python 3.8+
- Keep dependencies minimal

## Context and Background
This rate limiter will be used in a production API serving 100k requests per day. It needs to be reliable and performant. The API currently has no rate limiting, leading to occasional abuse.

## Example Usage
```python
# Initialize rate limiter
limiter = RateLimiter(
    algorithm="token_bucket",
    rate=100,  # 100 requests
    period=60  # per 60 seconds
)

# Check if request is allowed
if limiter.allow_request(user_id="user123"):
    # Process request
    return handle_request()
else:
    # Rate limit exceeded
    return error_429_too_many_requests()
```

## Technical Specifications
- Language: Python 3.8+
- Testing: pytest
- No external dependencies for core functionality
- Thread safety using threading primitives

## Notes
- Consider using Python's threading.Lock for thread safety
- Token bucket is preferred for its burst handling
- Fixed window is simpler but has the "thundering herd" problem
- Memory usage is critical as we'll track many users