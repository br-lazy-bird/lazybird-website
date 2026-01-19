---
title: "Broken System List Update"
date:  2025-10-09 17:14:06
categories: ["Lazy Bird Project"]
tags: []
---

Here's an updated list of broken systems that we can implement on this project. The update is related to the categories. First, we defined it as categories related to domains. Now, they are related to problems domains, but without mentioning the problem itself. 

These are not backlog or roadmap, these are only ideas of broken systems that can be implemented or not. Each of broken system is grouped based on its problem domain and it is rated according to the following criterias:

| 🟢 Easy Systems                       | 🟡 Medium Systems           | 🔴 Hard Systems                      |
| ------------------------------------ | -------------------------- | ----------------------------------- |
| Simple configuration changes         | Multiple component changes | Distributed system concepts         |
| Standard library solutions           | Some infrastructure setup  | Complex infrastructure requirements |
| Clear cause-and-effect relationships | Moderate research required | Advanced debugging needed           |
| Single-file modifications            | Mid-level concepts         | Enterprise-level patterns           |
| Beginner-friendly concepts           | Testing complexity         | Multiple interacting components     |



## 1. Database Performance

### Query Optimization
- 🟢 `01-employee-directory/` - Missing indexes on search columns
- 🟢 `02-customer-lookup/` - Inefficient WHERE clauses with functions
- 🟢 `03-product-catalog/` - Full table scans on large datasets
- 🟡 `04-order-history/` - Missing composite indexes
- 🟡 `05-sales-reports/` - N+1 query problems
- 🔴 `06-user-analytics/` - Inefficient JOINs and subqueries
- 🟡 `07-inventory-tracking/` - Cartesian product issues
- 🔴 `08-audit-logs/` - Query plan optimization

### Connection Management
- 🔴 `09-user-sessions/` - Connection pool exhaustion
- 🟡 `10-batch-processing/` - Transaction timeout issues
- 🔴 `11-reporting-system/` - Long-running query blocking
- 🔴 `12-data-migration/` - Lock contention problems

---

## 2. Asynchronous Patterns

### API Call Patterns
- 🟢 `01-product-catalog/` - Sequential vs parallel API calls
- 🟢 `02-user-profile/` - Synchronous blocking calls
- 🟡 `03-order-processing/` - Nested API dependency chains
- 🟡 `04-inventory-sync/` - Inefficient polling patterns

### Task Processing
- 🟢 `05-email-service/` - Fire-and-forget reliability
- 🟡 `06-file-processing/` - Long-running task handling
- 🔴 `07-batch-jobs/` - Event-driven orchestration

---

## 3. Response Time Optimization

### Caching Strategies
- 🟢 `01-content-delivery/` - Missing application cache
- 🟢 `02-database-queries/` - No query result caching
- 🟢 `03-api-responses/` - Repeated expensive computations
- 🟡 `04-session-management/` - Database-stored sessions
- 🟡 `05-product-prices/` - Cache invalidation problems
- 🟡 `06-user-preferences/` - Cache warming strategies
- 🔴 `07-real-time-data/` - Stale cache issues
- 🔴 `08-distributed-cache/` - Cache consistency problems

### Cache Management
- 🟡 `09-large-datasets/` - Memory cache overflow
- 🟡 `10-image-processing/` - Inefficient cache usage
- 🟡 `11-search-results/` - Cache key collision
- 🔴 `12-multi-tenant/` - Cache isolation issues

---

## 4. System Resilience

### Error Handling
- 🟡 `01-payment-gateway/` - Missing timeout configurations
- 🟡 `02-notification-service/` - No retry mechanisms
- 🔴 `03-third-party-integration/` - Circuit breaker missing
- 🔴 `04-microservice-calls/` - Cascade failure scenarios
- 🔴 `05-circuit-patterns/` - Cascading failure prevention

### System Design
- 🔴 `06-monolith-scaling/` - Single point of failure
- 🔴 `07-service-boundaries/` - Tight coupling issues
- 🔴 `08-data-consistency/` - Distributed transaction problems
- 🟡 `09-service-discovery/` - Hard-coded dependencies

---

## 5. Traffic Management

### Rate Control
- 🟡 `01-search-api/` - No rate limiting implementation
- 🔴 `02-upload-service/` - Missing backpressure handling
- 🔴 `03-analytics-collector/` - Burst traffic overwhelming
- 🟡 `04-webhook-handler/` - Resource exhaustion attacks
- 🟡 `05-rate-limiting/` - DDoS vulnerability

### Load Distribution
- 🟡 `06-traffic-routing/` - Uneven load balancing
- 🟡 `07-session-affinity/` - Sticky session problems
- 🔴 `08-auto-scaling/` - Scale-up delay issues

---

## 6. Data Integrity

### Race Conditions
- 🟡 `01-booking-system/` - Double booking scenarios
- 🟢 `02-counter-service/` - Non-atomic increment operations
- 🟡 `03-resource-allocation/` - Shared resource conflicts
- 🟢 `04-user-registration/` - Duplicate account creation

### Locking & Synchronization
- 🔴 `05-inventory-updates/` - Deadlock scenarios
- 🔴 `06-bank-transfers/` - Transaction isolation issues
- 🟡 `07-voting-system/` - Read-write lock problems
- 🟡 `08-cache-updates/` - Lock contention hotspots

---

## 7. Resource Management

### Compute Resources
- 🟡 `01-batch-processing/` - Thread pool exhaustion
- 🟡 `02-data-analysis/` - CPU-bound task blocking
- 🟡 `03-image-resizing/` - Resource starvation
- 🔴 `04-report-generation/` - Memory sharing issues
- 🟡 `05-memory-leaks/` - Garbage collection issues
- 🟡 `06-thread-management/` - Context switching overhead

### System Resources
- 🟡 `07-connection-pools/` - Resource exhaustion
- 🟡 `08-disk-io/` - File handle limitations

---

## 8. Event-Driven Architecture

### Message Queues
- 🟡 `01-notification-system/` - Backpressure and overflow
- 🟡 `02-order-tracking/` - Event ordering problems
- 🟡 `03-audit-trail/` - Message durability issues
- 🔴 `04-user-actions/` - Dead letter queue handling

### Event Processing
- 🔴 `05-real-time-updates/` - Event storm scenarios
- 🟡 `06-data-synchronization/` - Out-of-order processing
- 🔴 `07-workflow-engine/` - Event replay mechanisms
- 🟡 `08-monitoring-alerts/` - Event deduplication
- 🔴 `09-integration-hub/` - Event transformation issues

---

## 9. Application Security

### Authentication & Authorization
- 🟡 `01-user-login/` - JWT token vulnerabilities
- 🟢 `02-api-access/` - Missing authorization checks
- 🟡 `03-session-management/` - Session fixation attacks
- 🟡 `04-password-reset/` - Insecure token generation

### Data Protection
- 🟢 `05-sensitive-data/` - Information leakage
- 🟢 `06-sql-injection/` - Input validation bypass
- 🟡 `07-file-upload/` - Malicious file execution
- 🟡 `08-data-encryption/` - Weak encryption implementation

### Network Security
- 🟢 `09-api-endpoints/` - CORS misconfiguration
- 🟡 `10-ssl-certificates/` - Certificate validation issues
- 🟢 `11-input-sanitization/` - XSS attack vectors

---

## 10. System Observability

### Monitoring Fundamentals
- 🟢 `01-application-logs/` - Missing critical logging
- 🟢 `02-performance-metrics/` - No monitoring instrumentation
- 🟢 `03-error-tracking/` - Silent failure scenarios
- 🟢 `04-health-checks/` - Inadequate service monitoring

### Alerting Systems
- 🟡 `05-threshold-alerts/` - Alert fatigue problems
- 🔴 `06-anomaly-detection/` - False positive rates
- 🟡 `07-incident-response/` - Alert correlation issues
- 🟡 `08-dependency-monitoring/` - Blind spot identification

### Performance Analysis
- 🟡 `09-profiling-tools/` - Performance bottleneck identification
- 🟡 `10-resource-usage/` - Capacity planning data gaps
- 🔴 `11-user-experience/` - End-to-end tracing missing
- 🟡 `12-business-metrics/` - KPI measurement implementation