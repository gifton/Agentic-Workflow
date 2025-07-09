# Agentic Workflow - Example: Web API with Monitoring

This example demonstrates how "with monitoring" adapts the workflow to include comprehensive observability.

## Command Used
```
agentic workflow for web API with monitoring and metrics optimized for reliability
```

## Task: Build User Management API

Create a RESTful API for user management with full observability, including request tracking, performance metrics, error monitoring, and health checks.

---

## Plan 
*Time: 10 minutes*

**Break down the task:**
- [x] Step 1: Design API endpoints and data model
- [x] Step 2: Set up monitoring infrastructure
- [x] Step 3: Implement core API functionality
- [x] Step 4: Add comprehensive instrumentation
- [x] Step 5: Create monitoring dashboards
- [x] Step 6: Implement health checks and alerts

**Identify risks:**
- [x] Main technical risk: Performance under load
- [x] Main complexity: Distributed tracing setup
- [x] Key dependency: Monitoring stack (Prometheus/Grafana/OpenTelemetry)

**Initial confidence:** 75/100

*Why this confidence level?* Monitoring adds complexity but is well-documented pattern

---

## Monitoring Setup
*Added by "with monitoring" modifier*

### Metrics to Track
- **Request Metrics**
  - [ ] Request rate (req/sec)
  - [ ] Response time (p50, p95, p99)
  - [ ] Error rate (4xx, 5xx)
  - [ ] Request size/response size

- **Resource Metrics**
  - [ ] CPU usage
  - [ ] Memory consumption
  - [ ] Database connection pool
  - [ ] Cache hit rate

- **Business Metrics**
  - [ ] User registrations/hour
  - [ ] Authentication failures
  - [ ] API usage by endpoint
  - [ ] Rate limit violations

### Monitoring Tools
- [ ] OpenTelemetry for instrumentation
- [ ] Prometheus for metrics storage
- [ ] Grafana for visualization
- [ ] AlertManager for alerting

---

## Build
*Time: 1 day*

### Step 1: Design API endpoints and data model
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: None
- **Step confidence:** 95/100

**Monitoring Points Added:**
- Endpoint design includes metric labels
- Structured logging format defined
- Trace context propagation planned

### Step 2: Set up monitoring infrastructure
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Local setup only, need cloud config
- **Step confidence:** 85/100

**Components Configured:**
```yaml
# docker-compose.monitoring.yml
services:
  prometheus:
    image: prom/prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"
  
  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
  
  jaeger:
    image: jaegertracing/all-in-one
    ports:
      - "16686:16686"
      - "14268:14268"
```

### Step 3: Implement core API functionality
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: None
- **Step confidence:** 90/100

**Monitoring Instrumentation Added:**
```python
# Automatic instrumentation with decorators
@monitor_endpoint(name="create_user")
@trace_operation
async def create_user(request: Request, user: UserCreate):
    with metrics.timer("api.user.create.duration"):
        # Record custom metrics
        metrics.increment("api.user.create.attempts")
        
        try:
            result = await user_service.create(user)
            metrics.increment("api.user.create.success")
            return result
        except Exception as e:
            metrics.increment("api.user.create.errors", tags={"error_type": type(e).__name__})
            raise
```

### Step 4: Add comprehensive instrumentation
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Need to tune sampling rate
- **Step confidence:** 88/100

**Instrumentation Coverage:**
- ✅ HTTP middleware for automatic request tracking
- ✅ Database query monitoring
- ✅ External API call tracking
- ✅ Background job monitoring
- ✅ Custom business metrics

**Sample Metrics Output:**
```
# TYPE http_request_duration_seconds histogram
http_request_duration_seconds_bucket{method="POST",endpoint="/users",status="200",le="0.005"} 24
http_request_duration_seconds_bucket{method="POST",endpoint="/users",status="200",le="0.01"} 45
http_request_duration_seconds_bucket{method="POST",endpoint="/users",status="200",le="0.025"} 120

# TYPE api_user_registrations_total counter
api_user_registrations_total{status="success"} 156
api_user_registrations_total{status="failed"} 12
```

### Step 5: Create monitoring dashboards
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Need mobile-responsive views
- **Step confidence:** 82/100

**Dashboards Created:**
1. **Service Overview**
   - Request rate graph
   - Error rate graph
   - Response time heatmap
   - Current active users

2. **Performance Dashboard**
   - Response time percentiles
   - Database query performance
   - Cache hit rates
   - Resource utilization

3. **Business Metrics**
   - User growth chart
   - API usage by endpoint
   - Authentication success rate
   - Feature adoption metrics

### Step 6: Implement health checks and alerts
- [x] Implemented
- [x] Self-tested
- [x] Issues noted: Need to calibrate alert thresholds
- **Step confidence:** 85/100

**Health Check Endpoints:**
```python
@app.get("/health")
async def health():
    return {
        "status": "healthy",
        "timestamp": datetime.utcnow(),
        "version": "1.0.0"
    }

@app.get("/health/ready")
async def readiness():
    checks = {
        "database": await check_database(),
        "cache": await check_cache(),
        "external_api": await check_external_api()
    }
    
    status = "ready" if all(checks.values()) else "not_ready"
    return {"status": status, "checks": checks}
```

**Alert Rules Configured:**
```yaml
alerts:
  - name: HighErrorRate
    expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.05
    severity: critical
    
  - name: SlowResponseTime
    expr: histogram_quantile(0.95, http_request_duration_seconds) > 1
    severity: warning
    
  - name: DatabaseConnectionPoolExhausted
    expr: db_connection_pool_available == 0
    severity: critical
```

**Overall build confidence:** 86/100

---

## Monitoring Validation
*Added by "with monitoring" modifier*

### Load Testing with Monitoring
- [x] Run load test with 1000 concurrent users
- [x] Monitor all metrics during test
- [x] Verify dashboards update correctly
- [x] Confirm alerts trigger appropriately

**Load Test Results:**
- p50 response time: 45ms ✅
- p95 response time: 128ms ✅
- p99 response time: 245ms ✅
- Error rate: 0.02% ✅
- CPU usage: 65% peak ✅
- Memory stable at 512MB ✅

### Observability Coverage Check
- [x] All endpoints instrumented?
- [x] Error tracking complete?
- [x] Distributed traces working?
- [x] Logs properly structured?
- [x] Metrics exportable?
- [x] Alerts tested?

---

## Review
*Time: 30 minutes*

**Functionality Check:**
- [x] All requirements met?
- [x] Core functionality works?
- [x] Edge cases handled?
- [x] Tests passing?

**Monitoring Check:**
- [x] All critical paths instrumented?
- [x] Dashboards provide actionable insights?
- [x] Alerts cover failure scenarios?
- [x] Performance baselines established?
- [x] Debugging information sufficient?

**Issues Found:**
1. Alert thresholds need tuning based on real traffic
2. Dashboard mobile views need improvement
3. Sampling rate might be too high for production

**Final confidence:** 87/100

---

## Decision

✅ **Ready to ship!** (87/100)

Comprehensive monitoring is in place. The system has excellent observability and the team can confidently deploy and operate the service.

**Next action:** Deploy to staging for real-world monitoring validation

---

## Monitoring Artifacts

### Key Dashboards
1. [Service Overview](http://localhost:3000/d/service-overview)
2. [Performance Metrics](http://localhost:3000/d/performance)
3. [Business KPIs](http://localhost:3000/d/business-kpis)

### Alert Runbook
1. **HighErrorRate**: Check logs, review recent deployments, rollback if needed
2. **SlowResponseTime**: Check database queries, cache misses, external API latency
3. **DatabaseConnectionPoolExhausted**: Scale connection pool, investigate query leaks

### Monitoring Queries
```promql
# Useful PromQL queries for debugging

# Request rate by endpoint
sum(rate(http_requests_total[5m])) by (endpoint)

# Error rate percentage
sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m])) * 100

# p95 latency by endpoint
histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (endpoint, le))

# Active users
sum(increase(api_user_activity_total[1h]))
```

---

## How "with monitoring" Transformed This Workflow

1. **Added Monitoring Setup Phase** - Infrastructure before implementation
2. **Instrumentation Throughout** - Every step includes monitoring code
3. **Extra Validation Phase** - Load testing with metric verification
4. **Monitoring-Specific Artifacts** - Dashboards, alerts, runbooks
5. **Observability Review Criteria** - Beyond just functionality
6. **Operational Readiness Focus** - Not just working, but observable

This ensures the application isn't just built, but is ready for production operation with full visibility into its behavior.