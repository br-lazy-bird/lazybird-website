---
title: "Broken System List"
date:  2025-09-17 17:01:55
categories: ["Lazy Bird Project"]
tags: []
---

Here's a list of broken systems that we can implement on this project. These are not backlog or roadmap, these are only ideas of broken systems that can be implemented or not. Each of broken system is grouped based on its problem domain and it is rated according to the following criterias:

| 🟢 Easy Systems                       | 🟡 Medium Systems           | 🔴 Hard Systems                      |
| ------------------------------------ | -------------------------- | ----------------------------------- |
| Simple configuration changes         | Multiple component changes | Distributed system concepts         |
| Standard library solutions           | Some infrastructure setup  | Complex infrastructure requirements |
| Clear cause-and-effect relationships | Moderate research required | Advanced debugging needed           |
| Single-file modifications            | Mid-level concepts         | Enterprise-level patterns           |
| Beginner-friendly concepts           | Testing complexity         | Multiple interacting components     |

### Database

- Query Performance
    - 🟢 `01-employee-directory/` - Missing indexes on search columns
    - 🟢 `02-customer-lookup/` - Inefficient WHERE clauses with functions
    - 🟢 `03-product-catalog/` - Full table scans on large datasets
    - 🟡 `04-order-history/` - Missing composite indexes

- Query Optimization
    - 🟡 `05-sales-reports/` - N+1 query problems
    - 🔴 `06-user-analytics/` - Inefficient JOINs and subqueries
    - 🟡 `07-inventory-tracking/` - Cartesian product issues
    - 🔴 `08-audit-logs/` - Query plan optimization

- Connection & Resource Management
    - 🔴 `09-user-sessions/` - Connection pool exhaustion
    - 🟡 `10-batch-processing/` - Transaction timeout issues
    - 🔴 `11-reporting-system/` - Long-running query blocking
    - 🔴 `12-data-migration/` - Lock contention problems

### APIs

- Call Patterns
    - 🟢 `01-product-catalog/` - Sequential vs parallel API calls
    - 🟢 `02-user-profile/` - Synchronous blocking calls
    - 🟡 `03-order-processing/` - Nested API dependency chains
    - 🟡 `04-inventory-sync/` - Inefficient polling patterns

- Error Handling & Resilience
    - 🟡 `05-payment-gateway/` - Missing timeout configurations
    - 🟡 `06-notification-service/` - No retry mechanisms
    - 🔴 `07-third-party-integration/` - Circuit breaker missing
    - 🔴 `08-microservice-calls/` - Cascade failure scenarios

- Rate Limiting & Throttling
    - 🟡 `09-search-api/` - No rate limiting implementation
    - 🔴 `10-upload-service/` - Missing backpressure handling
    - 🔴 `11-analytics-collector/` - Burst traffic overwhelming
    - 🟡 `12-webhook-handler/` - Resource exhaustion attacks

### Caching

- Cache Layers
    - 🟢 `01-content-delivery/` - Missing application cache
    - 🟢 `02-database-queries/` - No query result caching
    - 🟢 `03-api-responses/` - Repeated expensive computations
    - 🟡 `04-session-management/` - Database-stored sessions

- Cache Strategies
    - 🟡 `05-product-prices/` - Cache invalidation problems
    - 🟡 `06-user-preferences/` - Cache warming strategies
    - 🔴 `07-real-time-data/` - Stale cache issues
    - 🔴 `08-distributed-cache/` - Cache consistency problems

- Memory Management
    - 🟡 `09-large-datasets/` - Memory cache overflow
    - 🟡 `10-image-processing/` - Inefficient cache usage
    - 🟡 `11-search-results/` - Cache key collision
    - 🔴 `12-multi-tenant/` - Cache isolation issues

### Events

- Message Queues
    - 🟡 `01-notification-system/` - Backpressure and overflow
    - 🟡 `02-order-tracking/` - Event ordering problems
    - 🟡 `03-audit-trail/` - Message durability issues
    - 🔴 `04-user-actions/` - Dead letter queue handling

- Event Processing
    - 🔴 `05-real-time-updates/` - Event storm scenarios
    - 🟡 `06-data-synchronization/` - Out-of-order processing
    - 🔴 `07-workflow-engine/` - Event replay mechanisms
    - 🟡 `08-monitoring-alerts/` - Event deduplication

- Async Patterns
    - 🟢 `09-email-service/` - Fire-and-forget reliability
    - 🟡 `10-file-processing/` - Long-running task handling
    - 🔴 `11-batch-jobs/` - Event-driven orchestration
    - 🔴 `12-integration-hub/` - Event transformation issues

### Concurrency

- Race Conditions
    - 🟡 `01-booking-system/` - Double booking scenarios
    - 🟢 `02-counter-service/` - Non-atomic increment operations
    - 🟡 `03-resource-allocation/` - Shared resource conflicts
    - 🟢 `04-user-registration/` - Duplicate account creation

- Locking & Synchronization
    - 🔴 `05-inventory-updates/` - Deadlock scenarios
    - 🔴 `06-bank-transfers/` - Transaction isolation issues
    - 🟡 `07-voting-system/` - Read-write lock problems
    - 🟡 `08-cache-updates/` - Lock contention hotspots

- Parallel Processing
    - 🟡 `09-batch-processing/` - Thread pool exhaustion
    - 🟡 `10-data-analysis/` - CPU-bound task blocking
    - 🟡 `11-image-resizing/` - Resource starvation
    - 🔴 `12-report-generation/` - Memory sharing issues

### Architecture

- System Design
    - 🔴 `01-monolith-scaling/` - Single point of failure
    - 🔴 `02-service-boundaries/` - Tight coupling issues
    - 🔴 `03-data-consistency/` - Distributed transaction problems
    - 🟡 `04-service-discovery/` - Hard-coded dependencies

- Load Distribution
    - 🟡 `05-traffic-routing/` - Uneven load balancing
    - 🟡 `06-session-affinity/` - Sticky session problems
    - 🔴 `07-auto-scaling/` - Scale-up delay issues
    - 🔴 `08-circuit-patterns/` - Cascading failure prevention

- Resource Management
    - 🟡 `09-memory-leaks/` - Garbage collection issues
    - 🟡 `10-connection-pools/` - Resource exhaustion
    - 🟡 `11-thread-management/` - Context switching overhead
    - 🟡 `12-disk-io/` - File handle limitations

### Security

- Authentication & Authorization
    - 🟡 `01-user-login/` - JWT token vulnerabilities
    - 🟢 `02-api-access/` - Missing authorization checks
    - 🟡 `03-session-management/` - Session fixation attacks
    - 🟡 `04-password-reset/` - Insecure token generation

- Data Protection
    - 🟢 `05-sensitive-data/` - Information leakage
    - 🟢 `06-sql-injection/` - Input validation bypass
    - 🟡 `07-file-upload/` - Malicious file execution
    - 🟡 `08-data-encryption/` - Weak encryption implementation

- Network Security
    - 🟢 `09-api-endpoints/` - CORS misconfiguration
    - 🟡 `10-rate-limiting/` - DDoS vulnerability
    - 🟡 `11-ssl-certificates/` - Certificate validation issues
    - 🟢 `12-input-sanitization/` - XSS attack vectors

### Monitoring

- Observability
    - 🟢 `01-application-logs/` - Missing critical logging
    - 🟢 `02-performance-metrics/` - No monitoring instrumentation
    - 🟢 `03-error-tracking/` - Silent failure scenarios
    - 🟢 `04-health-checks/` - Inadequate service monitoring

- Alerting Systems
    - 🟡 `05-threshold-alerts/` - Alert fatigue problems
    - 🔴 `06-anomaly-detection/` - False positive rates
    - 🟡 `07-incident-response/` - Alert correlation issues
    - 🟡 `08-dependency-monitoring/` - Blind spot identification

- Performance Analysis
    - 🟡 `09-profiling-tools/` - Performance bottleneck identification
    - 🟡 `10-resource-usage/` - Capacity planning data gaps
    - 🔴 `11-user-experience/` - End-to-end tracing missing
    - 🟡 `12-business-metrics/` - KPI measurement implementation

