# Microservices Patterns Study Guide

## 1. Service Decomposition

**Goal:** Split a system into independently deployable services.

### Study
- Decompose by business capability
- Decompose by subdomain / bounded context
- Avoid splitting by technical layers

### Know
- Good services own behavior and data.
- Bad services are thin CRUD wrappers around shared tables.

---

## 2. Database per Service

**Goal:** Each service owns its data.

### Use When
- Teams need independent schema changes.
- Services need independent deployability.
- You want loose coupling.

### Tradeoff
- Cross-service queries and transactions become harder.

### Avoid
- Direct table access across services.
- Shared databases as the default.

---

## 3. API Gateway

**Goal:** One entry point for clients.

### Responsibilities
- Routing
- Authentication
- Rate limiting
- Request aggregation
- Protocol translation

### Risk
- Gateway becomes a bottleneck or mini-monolith.

---

## 4. Backend for Frontend (BFF)

**Goal:** Separate API layer per client type.

### Examples
- Web BFF
- Mobile BFF
- Partner API BFF

### Use When
- Different clients need different payloads or workflows.

---

## 5. Saga

**Goal:** Manage business transactions across services without distributed transactions.

### Styles
#### Choreography
Services publish and consume events.

#### Orchestration
A coordinator directs workflow execution.

### Key Idea
Each step has a compensating action.

---

## 6. Event-Driven Messaging

**Goal:** Services communicate asynchronously using events.

### Benefits
- Loose coupling
- Scalability
- Auditability
- Integration between domains

### Watch For
- Duplicate events
- Out-of-order delivery
- Event versioning
- Idempotency

---

## 7. CQRS

**Goal:** Separate write models from read models.

### Use When
- Reads are complex
- Read volume is high
- Read and write models differ significantly

### Tradeoff
- Increased complexity
- Eventual consistency

---

## 8. Event Sourcing

**Goal:** Store state as a sequence of events.

### Benefits
- Complete audit history
- Replay capability
- Temporal debugging

### Avoid When
- CRUD requirements are simple

---

## 9. Circuit Breaker

**Goal:** Prevent repeated calls to failing dependencies.

### States
- Closed
- Open
- Half-Open

### Common Companions
- Timeouts
- Retries
- Fallbacks

---

## 10. Bulkhead

**Goal:** Isolate failures and resource consumption.

### Examples
- Separate thread pools
- Separate connection pools
- Separate worker queues

---

## 11. Sidecar

**Goal:** Run supporting functionality beside a service.

### Common Uses
- Logging
- Metrics
- Security
- Service mesh proxies
- Configuration management

---

## 12. Ambassador

**Goal:** Externalize outbound network communication.

### Uses
- Service discovery
- Retries
- TLS
- Tracing
- Circuit breaking

---

## 13. Strangler Fig

**Goal:** Incrementally replace a legacy system.

### Process
1. Add a facade.
2. Route selected functionality to new services.
3. Gradually migrate capabilities.
4. Retire legacy components.

---

## 14. Anti-Corruption Layer

**Goal:** Protect modern domain models from legacy systems.

### Benefits
- Translation between models
- Reduced coupling
- Cleaner architecture

---

## 15. Service Discovery

**Goal:** Locate service instances dynamically.

### Types
- Client-side discovery
- Server-side discovery
- Platform-managed discovery

---

# Pattern Selection Cheat Sheet

| Problem | Pattern |
|----------|----------|
| Clients call too many services | API Gateway |
| Different clients need different APIs | BFF |
| Independent data ownership | Database per Service |
| Transactions span services | Saga |
| Loose coupling | Event-Driven Messaging |
| Complex reads | CQRS |
| Full audit history | Event Sourcing |
| Unreliable dependency | Circuit Breaker |
| Failure isolation | Bulkhead |
| Shared operational concerns | Sidecar |
| Outbound proxy behavior | Ambassador |
| Legacy migration | Strangler Fig |
| Legacy integration | Anti-Corruption Layer |

---

# Review Questions

1. Why is a shared database usually a bad default in microservices?
2. When would you choose Saga over distributed transactions?
3. What is the difference between API Gateway and BFF?
4. How do Circuit Breaker and Bulkhead differ?
5. What are the risks of Event Sourcing?
6. When is CQRS overkill?
7. Why must event consumers be idempotent?
8. What defines a good service boundary?
9. How does Strangler Fig reduce migration risk?
10. What belongs in a Sidecar instead of application code?
