# Agentic Natural - Complete Command Reference

> The natural language system that adapts to how you think and work.

## Core Concept

Agentic Natural uses conversational commands that read like English. Instead of memorizing syntax, just describe what you want naturally.

## Basic Syntax

```
agentic natural
  [for {what}]           # What you're building
  [with {features}]      # What capabilities you need
  [using {how}]          # Your approach or technology
  [in {when/mode}]       # Time constraints or style
  [optimized for {why}] # Your main goal
  [by {who}]            # Your team structure
```

## Command Building Blocks

### 🎯 FOR - What You're Building

The `for` modifier tells the system what type of project you're creating. This fundamentally shapes the workflow structure.

**Web & API Development**
- `for web API` → RESTful service with endpoints, error handling, validation
- `for GraphQL API` → Schema-first development, resolvers, subscriptions
- `for microservice` → Service boundaries, health checks, service discovery
- `for webhook handler` → Event processing, retry logic, idempotency

**Frontend Development**
- `for web app` → Component structure, state management, routing
- `for mobile app` → Platform considerations, offline support, push notifications
- `for dashboard` → Data visualization, real-time updates, responsive design
- `for landing page` → SEO optimization, performance, conversion tracking

**CLI & Tools**
- `for CLI tool` → Argument parsing, help system, error messages
- `for script` → Simple automation, minimal structure
- `for developer tool` → Plugin architecture, extensibility
- `for automation` → Scheduled tasks, error recovery

**Data & ML**
- `for data pipeline` → ETL processes, data validation, monitoring
- `for ML model` → Training pipeline, evaluation, deployment
- `for analytics` → Data aggregation, reporting, visualization
- `for scraper` → Rate limiting, data extraction, storage

**Infrastructure**
- `for deployment pipeline` → CI/CD, testing stages, rollback
- `for monitoring system` → Metrics collection, alerting, dashboards
- `for backup system` → Scheduled backups, retention, recovery

**Special Types**
- `for prototype` → Quick validation, minimal polish
- `for MVP` → Core features only, basic documentation
- `for hackathon` → Maximum speed, technical debt acceptable
- `for production` → Full testing, monitoring, documentation
- `for enterprise` → Compliance, audit trails, extensive docs

### 🛠️ WITH - Features & Capabilities

The `with` modifier adds specific features to your workflow. Chain multiple features with "and".

**Zen-MCP Integration**
- `with zen` → Enables intelligent zen-mcp tool usage throughout
- `with zen debug` → Uses zen debug tool for troubleshooting
- `with zen analysis` → Deep code analysis with zen analyze
- `with zen planning` → Uses zen planner for complex tasks
- `with zen review` → Comprehensive code review with zen
- `with zen testing` → Test generation using zen testgen
- `with zen consensus` → Multi-model validation for decisions

**Quality & Testing**
- `with testing` → Unit tests, integration tests, coverage
- `with TDD` → Test-first development cycle
- `with automated testing` → CI integration, test generation
- `with performance testing` → Load tests, benchmarks

**Observability**
- `with monitoring` → Metrics, dashboards, alerts (see [example](example-monitoring.md))
- `with logging` → Structured logs, log aggregation
- `with tracing` → Distributed tracing, request tracking
- `with debugging` → Debug endpoints, detailed errors

**Reliability**
- `with checkpoints` → Save states, resume capability
- `with rollback` → Version control, deployment rollback
- `with error handling` → Graceful failures, recovery
- `with retry logic` → Exponential backoff, circuit breakers

**Security**
- `with security` → Security best practices, OWASP
- `with authentication` → User auth, JWT, OAuth
- `with encryption` → Data encryption, key management
- `with security scanning` → Vulnerability detection

**Documentation**
- `with documentation` → Code docs, API docs, README
- `with API docs` → OpenAPI/Swagger specs
- `with examples` → Usage examples, tutorials
- `with diagrams` → Architecture diagrams, flow charts

**Development Features**
- `with hot reload` → Development server, live updates
- `with debugging tools` → Debugger integration
- `with linting` → Code style enforcement
- `with formatting` → Auto-formatting setup

### 🔧 USING - Approach & Technology

The `using` modifier specifies your technical approach or stack.

**Development Methodologies**
- `using TDD` → Test-driven development
- `using BDD` → Behavior-driven development
- `using DDD` → Domain-driven design
- `using agile` → Sprint-based, iterative
- `using waterfall` → Sequential phases

**Architecture Patterns**
- `using microservices` → Service-oriented
- `using serverless` → Function-based
- `using monolith` → Single application
- `using event-driven` → Message-based
- `using CQRS` → Command/Query separation

**Languages & Frameworks**
- `using Python` → Python-specific patterns
- `using TypeScript` → Type-safe JavaScript
- `using React` → Component-based UI
- `using FastAPI` → Modern Python API
- `using Next.js` → Full-stack React

**Protocols & Standards**
- `using REST` → RESTful principles
- `using GraphQL` → Query language
- `using WebSocket` → Real-time communication
- `using gRPC` → High-performance RPC

### ⏱️ IN - Time & Mode

The `in` modifier sets constraints or working style.

**Time Constraints**
- `in 2 hours` → Extreme simplification
- `in 1 day` → Focus on essentials
- `in 1 week` → Balanced approach
- `in 1 sprint` → Sprint-sized work
- `in phases` → Incremental delivery

**Development Modes**
- `in exploratory mode` → Heavy experimentation
- `in careful mode` → Extra validation
- `in learning mode` → Educational focus
- `in teaching mode` → Documentation heavy
- `in debug mode` → Diagnostic features

**Working Styles**
- `in iterative mode` → Small increments
- `in sprint mode` → Time-boxed work
- `in maintenance mode` → Minimal changes
- `in migration mode` → Gradual transition

### 🎯 OPTIMIZED FOR - Primary Goal

The `optimized for` modifier sets the primary optimization target.

**Performance Goals**
- `optimized for speed` → Ship ASAP
- `optimized for performance` → Runtime efficiency
- `optimized for scalability` → Handle growth
- `optimized for latency` → Response time

**Quality Goals**
- `optimized for quality` → Code excellence
- `optimized for maintainability` → Long-term health
- `optimized for readability` → Clear code
- `optimized for simplicity` → Minimal complexity

**Business Goals**
- `optimized for cost` → Resource efficiency
- `optimized for user experience` → UX focus
- `optimized for conversion` → Business metrics
- `optimized for engagement` → User retention

**Development Goals**
- `optimized for learning` → Educational value
- `optimized for experimentation` → Try new things
- `optimized for collaboration` → Team work
- `optimized for iteration` → Quick cycles

### 👥 BY - Team Structure

The `by` modifier adapts the workflow for your team.

**Team Sizes**
- `by solo developer` → No coordination overhead
- `by pair` → Pair programming flow
- `by small team` → 3-5 people coordination
- `by large team` → 10+ people, more process
- `by distributed team` → Async communication

**Team Types**
- `by startup team` → Fast, flexible
- `by enterprise team` → Process-heavy
- `by open source contributors` → Public collaboration
- `by cross-functional team` → Multiple disciplines

## Preset Commands

Quick shortcuts for common scenarios:

### ⚡ Express Presets
- `agentic natural express` → Ship in 2 hours
- `agentic natural prototype` → Quick validation
- `agentic natural hackathon` → 24-hour sprint

### 📊 Balanced Presets
- `agentic natural standard` → Default balanced approach
- `agentic natural professional` → Production-ready
- `agentic natural startup` → Move fast, iterate

### 🏢 Enterprise Presets
- `agentic natural enterprise` → Full compliance
- `agentic natural regulated` → Audit trails
- `agentic natural government` → Maximum documentation

### 🔬 Specialized Presets
- `agentic natural research` → Heavy experimentation
- `agentic natural scientific` → Reproducibility focus
- `agentic natural academic` → Citations and rigor

## Real-World Command Examples

### Startup Building MVP
```
agentic natural for MVP with metrics and deployment 
using React and Node.js in 1 week 
optimized for user feedback by small team
```

### Enterprise Microservice
```
agentic natural for microservice with monitoring and security scanning 
using Java and Spring Boot 
optimized for maintainability by enterprise team
```

### Data Science Project
```
agentic natural for ML model with experimentation tracking 
using Python and TensorFlow in research mode 
optimized for accuracy
```

### Hackathon Project
```
agentic natural for web app with real-time features 
using Next.js in 24 hours 
optimized for demo impact by pair programming
```

### Migration Project
```
agentic natural for database migration with rollback 
using PostgreSQL in careful mode 
optimized for zero downtime by platform team
```

## Advanced Combinations

### Multiple "For" Targets
```
agentic natural for web API and admin dashboard
```
Creates workflow covering both backend API and frontend admin panel.

### Multiple "With" Features
```
agentic natural with testing and monitoring and documentation and deployment
```
Adds all specified features to the workflow.

### Complex Constraints
```
agentic natural for MVP in 3 days but optimized for quality
```
AI will balance speed vs quality tradeoff.

### Conditional Features
```
agentic natural for API with caching if high traffic expected
```
Adds features based on conditions.

## Interactive Commands

### Minimal Start
```
agentic natural
```
Triggers interactive mode with guided questions.

### Partial Commands
```
agentic natural for web API
```
AI will ask about missing aspects (timeline, team, goals).

### Clarification Requests
```
agentic natural for something with AI
```
AI will ask for specifics about "something" and "AI" usage.

## Smart Inference

The system intelligently infers requirements:

### Project Type Inference
- `for e-commerce` → Implies payment processing, cart, user accounts
- `for SaaS` → Implies subscriptions, multi-tenancy, billing
- `for game` → Implies real-time updates, state management, physics

### Technology Stack Inference
- `using React` → Implies modern JavaScript, component patterns
- `using Django` → Implies Python, MVC pattern, ORM
- `using Kubernetes` → Implies containerization, orchestration

### Team Inference
- `by startup` → Implies moving fast, some technical debt OK
- `by agency` → Implies client deliverables, documentation
- `by consultancy` → Implies knowledge transfer, best practices

## Command Aliases

Create your own shortcuts:

### Define Alias
```
agentic natural alias "my-stack" = "for web API with testing and monitoring using Python optimized for maintainability"
```

### Use Alias
```
agentic natural my-stack by small team
```

## Natural Variations

All these are equivalent:
- `agentic natural for API with tests`
- `agentic natural with tests for API`
- `agentic natural for API including tests`
- `agentic natural to build API with testing`

The system understands natural variations in phrasing.

## Tips for Effective Commands

1. **Start Simple** - Add modifiers as needed
2. **Be Specific About Constraints** - Time and resources matter most
3. **State Your Real Goal** - The system optimizes for what you specify
4. **Use Presets for Common Cases** - Don't reinvent the wheel
5. **Trust the Inference** - The system is smart about implications

## Getting Help

If unsure about commands:
- Just start with `agentic natural` for interactive mode
- Describe your needs in plain English
- The AI will help construct the right command
- You can always refine after starting

Remember: The goal is to make workflows feel natural, not to memorize syntax. Just describe what you need!