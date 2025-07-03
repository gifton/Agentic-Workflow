# Standard Context Template

## Task Description
[Provide a clear, concise description of what needs to be built]

## Requirements
### Functional Requirements
- [Specific requirement 1]
- [Specific requirement 2]
- [Specific requirement 3]

### Non-Functional Requirements
- Performance: [e.g., Handle 1000 requests/second]
- Security: [e.g., Use secure authentication]
- Scalability: [e.g., Support 10k concurrent users]

## Success Criteria
1. [Measurable outcome 1]
2. [Measurable outcome 2]
3. [Measurable outcome 3]

## Configuration
```yaml
# Simple, focused configuration
workflow:
  specialists: 2          # Usually 1-2 for standard tasks
  max_iterations: 3       # Default: 3
  target_quality: HIGH    # HIGH/MEDIUM minimum acceptable

task:
  complexity: medium      # low/medium/high
  domain: web_app        # Category for context
  estimated_time: 2h     # Rough estimate

output:
  format: markdown       # How to format deliverables
  include_tests: true    # Whether to include tests
  documentation: inline  # inline/separate
```

## Constraints
- [Technical constraint 1]
- [Business constraint 2]
- [Time/resource constraint 3]

## Context and Background
[Any additional context that helps understand the task better]

## Example Usage (Optional)
```python
# Example of how the feature should work
result = feature.process(input)
assert result == expected_output
```

## Technical Specifications (Optional)
- Language: [e.g., Python 3.9+]
- Framework: [e.g., Django 4.0]
- Database: [e.g., PostgreSQL]
- Dependencies: [List key dependencies]

## Notes
- [Any special considerations]
- [Known challenges]
- [Preferred approaches]