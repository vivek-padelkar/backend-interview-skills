# Question Bank — Backend Engineering Interviews

This reference provides scenario-based questions organized by topic × difficulty × experience level. Questions are pulled dynamically based on user selections; use this as a comprehensive source.

---

## Topic: Node.js Core

### Easy (Junior)

**Q1: Understand the Event Loop**
- **Scenario:** You have a function that uses `setTimeout(callback, 0)`, a Promise, and synchronous code. In what order do they execute?
- **Probe:** Write pseudocode or explain the order. What's the difference between the call stack and callback queue?
- **Key Concepts:** Event loop, call stack, callback queue, microtask queue, event loop phases

**Q2: Streams Basics**
- **Scenario:** Your API receives a large file upload. Would you load the entire file into memory or use streams? Why?
- **Probe:** How do streams help with memory usage and backpressure?
- **Key Concepts:** Readable/writable streams, backpressure, memory efficiency, `.pipe()`

**Q3: Callbacks, Promises, Async/Await**
- **Scenario:** You have callback-based code (`fs.readFile(path, (err, data) => {...})`). How would you convert it to Promises? Then to async/await?
- **Probe:** What's the difference? When would you use each?
- **Key Concepts:** Callback hell, Promise chaining, async/await, error handling

**Q4: Module System**
- **Scenario:** Your app has a `config.js` that exports an object. You modify it in one module. Is that change visible to other modules?
- **Probe:** Why or why not? How does Node.js caching work?
- **Key Concepts:** CommonJS modules, caching, module.exports, require()

### Medium (Mid)

**Q1: Worker Threads**
- **Scenario:** You have a CPU-intensive calculation (hash cracking, matrix math) blocking your event loop. Would you use Worker Threads, child processes, or offload to a queue? Trade-offs?
- **Probe:** When would you pick each? Memory cost? Communication overhead?
- **Key Concepts:** Worker threads vs child processes, shared memory, message passing, CPU-bound vs I/O-bound

**Q2: Understanding the Event Loop Under Pressure**
- **Scenario:** You notice one endpoint is slow, blocking other requests. You profile it and see the event loop is backed up. Is it a CPU issue or I/O issue? How do you tell?
- **Probe:** What tools would you use? How do you fix each case differently?
- **Key Concepts:** Event loop blocking, microbenchmarks, CPU profiling, I/O analysis, flame graphs

**Q3: Clusters and Process Management**
- **Scenario:** You want to use all 8 CPU cores in your Node.js app. How? Trade-offs vs single process?
- **Probe:** How does clustering affect memory, debugging, session management?
- **Key Concepts:** Cluster module, master/worker pattern, load balancing, memory overhead

**Q4: Memory Leaks**
- **Scenario:** Your app's memory grows over time even under steady load. What could cause this? How do you debug?
- **Probe:** Give me a specific example (circular references, event listeners, caches). How do you find it?
- **Key Concepts:** Garbage collection, heap snapshots, detached DOM nodes, event listener cleanup, unreferenced objects

### Hard (Senior/Staff)

**Q1: Event Loop Internals and Scheduling**
- **Scenario:** You need sub-millisecond timing precision. You experiment with `setImmediate()` vs `process.nextTick()` vs `queueMicrotask()`. What are the guarantees? When would you use each in a performance-critical system?
- **Probe:** What about `setInterval()` and `setTimeout()` jitter under load?
- **Key Concepts:** Event loop phases (timers, pending callbacks, idle/prepare, poll, check, close), microtask queues, macrotask queues, scheduling precision

**Q2: Module Loading and Circular Dependencies**
- **Scenario:** You have modules A → B → A (circular). Node.js doesn't crash; what gets exported in each case? How would you restructure to avoid the issue at scale?
- **Probe:** Show a concrete code example. What about ES modules vs CommonJS?
- **Key Concepts:** Circular dependency resolution, partial exports, module initialization order, ES modules vs CommonJS semantics

**Q3: Stream Internals and Backpressure**
- **Scenario:** You're piping a large file to a slow destination. Without proper backpressure handling, memory spikes. Explain the mechanism and how `pipe()` or manual pausing prevents it. What's the invariant?
- **Probe:** How do you implement backpressure in custom streams?
- **Key Concepts:** highWaterMark, drain event, pause/resume, write() return value, stream composition

**Q4: Async/Await Error Handling at Scale**
- **Scenario:** You have 100 concurrent requests using async/await. One throws an unhandled rejection. Your server crashes. Design a system-wide error boundary without try-catch on every function.
- **Probe:** How do you categorize errors (retriable, fatal)? How does this scale to microservices?
- **Key Concepts:** Promise rejection handling, uncaughtException listeners, graceful shutdown, error categorization, observability

---

## Topic: Express/Fastify

### Easy (Junior)

**Q1: Middleware Order**
- **Scenario:** You have middleware for logging, auth, and error handling. In what order should you register them? Why?
- **Probe:** What happens if you put error handling first?
- **Key Concepts:** Middleware chaining, order matters, next() flow, error-handling middleware signature

**Q2: Routing**
- **Scenario:** You need a `/users/:id` route that retrieves a user. How do you extract the `:id` parameter? How do you handle invalid IDs (e.g., non-numeric)?
- **Probe:** When would you validate in the route vs in a middleware?
- **Key Concepts:** Route parameters, req.params, validation, status codes (400 vs 404)

**Q3: Request/Response Cycle**
- **Scenario:** You send a response with `res.json(data)`. Can you send another response after that? What happens?
- **Probe:** How do you prevent double-sending?
- **Key Concepts:** Response lifecycle, headers sent, single response rule, error prevention

**Q4: Error Handling**
- **Scenario:** An async route handler throws an error. Does Express catch it automatically?
- **Probe:** How do you ensure errors are caught? What's the best pattern?
- **Key Concepts:** Try-catch in async routes, error-handling middleware, explicit error passing

### Medium (Mid)

**Q1: Middleware and Context Passing**
- **Scenario:** You need to pass user data from auth middleware to your route handler. How? (req.user = {...})? Is this safe? What if you need it in multiple places?
- **Probe:** Trade-offs of different approaches? How do you type this in TypeScript?
- **Key Concepts:** Middleware context, req object mutation, type safety, middleware composition

**Q2: Performance—Request Body Parsing**
- **Scenario:** Your API receives large JSON payloads (10MB+). You use `express.json()`. What could go wrong? How do you optimize?
- **Probe:** What's the difference between `express.json()` and `express.raw()`? When would you use each?
- **Key Concepts:** Body parser limits, streaming bodies, multipart uploads, memory efficiency

**Q3: Session Management**
- **Scenario:** You have a session-based auth system (Express with redis sessions). A user logs in on server A, then hits server B (load balanced). What happens?
- **Probe:** How do you ensure sessions work across instances? What about JWTs instead?
- **Key Concepts:** Session store, shared state, load balancing, JWT vs sessions trade-offs

**Q4: Rate Limiting and Throttling**
- **Scenario:** You need to rate-limit an endpoint to 100 requests/min per IP. How? What if users are behind a proxy?
- **Probe:** In-memory vs Redis? What about distributed systems?
- **Key Concepts:** Rate limiting strategies, IP detection (X-Forwarded-For), sliding windows, distributed coordination

### Hard (Senior/Staff)

**Q1: Custom Middleware Composition**
- **Scenario:** Design a middleware that authenticates, logs, and handles errors, but can be composed at different granularities (global, per-route, per-param). How do you handle nested async operations and error propagation?
- **Probe:** Show how you'd compose auth + logging + error handling without callback hell.
- **Key Concepts:** Higher-order functions, middleware factories, error propagation, async composition

**Q2: Request Timeout and Cancellation**
- **Scenario:** A request to an external API hangs. Your Express server is stuck waiting. Design a timeout + cancellation strategy (hint: AbortController). What about cleanup?
- **Probe:** How do you handle partial failures? What about cascading timeouts?
- **Key Concepts:** AbortController, timeout patterns, graceful degradation, resource cleanup

**Q3: Streaming Responses**
- **Scenario:** You need to return a large dataset (1GB) to the client. You can't load it all into memory. Design a streaming response using Express/Fastify.
- **Probe:** How do you handle backpressure? What about error handling mid-stream?
- **Key Concepts:** res.write(), pipe(), backpressure, chunked encoding, error recovery

**Q4: Production Hardening**
- **Scenario:** Your Express app went to production. List 5 security issues and how you'd address them (CORS, helmet, input validation, rate limiting, secret management).
- **Probe:** How do you test these? What monitoring would you add?
- **Key Concepts:** CORS, CSP, rate limiting, input validation, secret rotation, observability

---

## Topic: Databases

### Easy (Junior)

**Q1: Basic Queries**
- **Scenario:** You need to fetch a user by ID from a SQL database. Write pseudocode. What's a `SELECT` statement? What's different from a NoSQL query?
- **Probe:** When would you use SQL vs NoSQL?
- **Key Concepts:** SQL basics, indexes, NoSQL trade-offs, query structure

**Q2: Connection Pooling Concept**
- **Scenario:** Your app connects to a database. Should you create a new connection per request or reuse connections? Why?
- **Probe:** What's a connection pool? Why is it better?
- **Key Concepts:** Connection pooling, resource reuse, latency, pool size tuning

**Q3: Transactions**
- **Scenario:** You transfer money between two accounts (debit one, credit another). If the app crashes mid-operation, what happens? How do you prevent inconsistency?
- **Probe:** What's a transaction? Why does it matter?
- **Key Concepts:** ACID properties, atomic operations, rollback, consistency

**Q4: N+1 Problem**
- **Scenario:** You query 100 users and their posts. Naive code does: 1 query for users + 100 queries for posts (N+1). How do you fix it?
- **Probe:** Name the techniques (JOIN, eager loading, batching).
- **Key Concepts:** N+1 query problem, JOINs, eager loading, query optimization

### Medium (Mid)

**Q1: Indexing Strategy**
- **Scenario:** Your `SELECT * FROM users WHERE email = ?` query is slow (scanning 1M rows). How do you speed it up? What's the trade-off?
- **Probe:** What type of index? When do indexes hurt?
- **Key Concepts:** B-tree indexes, index selectivity, insertion cost, storage overhead

**Q2: Database Design—Normalization vs Denormalization**
- **Scenario:** You design a schema with Users, Posts, Comments. Normalized: 3 tables with FKs. Denormalized: flatten everything. Trade-offs?
- **Probe:** When would you denormalize? What about read/write patterns?
- **Key Concepts:** Normal forms (1NF, 2NF, 3NF), denormalization, read/write amplification, consistency risk

**Q3: Replication and Consistency**
- **Scenario:** You have 1 primary + 2 replicas. After a write, a read from a replica might see stale data. How do you handle this? Can you avoid it?
- **Probe:** What's eventual consistency? When is it acceptable?
- **Key Concepts:** Primary-replica setup, read-after-write consistency, eventual consistency, consistency models

**Q4: Migration at Scale**
- **Scenario:** You need to add a NOT NULL column to a 100M-row table without downtime. How?
- **Probe:** What about concurrent writes during migration?
- **Key Concepts:** Online migrations, dual-write patterns, feature flags, backfill safety

### Hard (Senior/Staff)

**Q1: Sharding Design**
- **Scenario:** Your 1TB user table is too big for a single node. Design a sharding strategy (by user ID, region, etc.). How do you handle hot shards? Resharding?
- **Probe:** How do you query across shards? What about transactions?
- **Key Concepts:** Sharding keys, shard balancing, hot shard mitigation, distributed transactions

**Q2: Query Optimization Deep Dive**
- **Scenario:** A complex JOIN query with 5 tables, subqueries, and aggregations is slow. Walk through your optimization process (EXPLAIN, statistics, rewrites).
- **Probe:** How do you identify bottlenecks? What's the cost model?
- **Key Concepts:** Query plans, cardinality estimation, statistics, rewrite rules, cost-based optimization

**Q3: Backup and Disaster Recovery**
- **Scenario:** Your production database fails. You have hourly backups. Design a recovery strategy: RTO (recovery time), RPO (data loss tolerance), validation, failover automation.
- **Probe:** How do you test recovery? What about compliance (GDPR, etc.)?
- **Key Concepts:** RTO/RPO, backup strategies (full, incremental, WAL), PITR (point-in-time recovery), failover automation

**Q4: ACID vs BASE Trade-offs**
- **Scenario:** You're building a distributed system (shopping cart, inventory). ACID transactions are too slow. Design a BASE (eventual consistency) system. How do you handle anomalies (overselling inventory, double-charging)?
- **Probe:** What compensating actions do you need?
- **Key Concepts:** BASE model, eventual consistency, compensation, idempotency, conflict resolution

---

## Topic: System Design

### Easy (Junior)

**Q1: Simple API Architecture**
- **Scenario:** Design a basic blogging API: users create posts, view them. How do you organize the backend? What components do you need?
- **Probe:** Database, caching, API layer?
- **Key Concepts:** Layered architecture, separation of concerns, basic scalability concepts

**Q2: Caching Basics**
- **Scenario:** You have a frequently accessed static page (10K requests/min). Queries are slow. How do you speed it up?
- **Probe:** Where do you cache? (CDN, Redis, memory)
- **Key Concepts:** Caching layers, TTL, invalidation, cache misses

**Q3: Load Balancing**
- **Scenario:** You have 3 servers. How do you distribute traffic evenly?
- **Probe:** Round-robin, least connections? What if a server fails?
- **Key Concepts:** Load balancing strategies, failover, health checks

**Q4: Databases at Scale**
- **Scenario:** Your single database server is overloaded (reads + writes). How do you scale?
- **Probe:** Read replicas, caching, sharding?
- **Key Concepts:** Scaling strategies, read/write separation, eventual consistency

### Medium (Mid)

**Q1: Designing a URL Shortener (1M requests/day)**
- **Scenario:** Design `short.url/abc` → redirect to long URL. 1M redirects/day, 100K unique URLs created/day. How do you architect it?
- **Probe:** Database schema, caching strategy, URL generation (sequential vs random), hot URLs.
- **Key Concepts:** Traffic estimation, caching strategy, database design, collision handling

**Q2: Message Queues for Async Processing**
- **Scenario:** Users upload photos. Image processing (resize, optimize) is slow. How do you decouple upload from processing?
- **Probe:** Use a queue (RabbitMQ, Kafka)? What about failures and retries?
- **Key Concepts:** Async processing, message queues, idempotency, failure handling, monitoring

**Q3: Rate Limiting at Scale**
- **Scenario:** Implement rate limiting: 100 req/min per user, 10K req/min per IP. 100K concurrent users. How?
- **Probe:** In-memory vs distributed (Redis)? Sliding windows vs token bucket?
- **Key Concepts:** Rate limiting algorithms, distributed state, precision, fairness

**Q4: Designing a Notification System**
- **Scenario:** Users get notifications (email, SMS, push). 1M users, some preferences are per-user. How do you scale notification delivery?
- **Probe:** Batch vs real-time? Channels? Storage?
- **Key Concepts:** Fan-out, batching, channel management, preference system, delivery guarantees

### Hard (Senior/Staff)

**Q1: Design a 1M QPS Real-Time Analytics System**
- **Scenario:** Ingest 1M events/sec (user clicks, purchases, etc.), store, query in <100ms. Petabyte-scale data. How do you architect?
- **Probe:** Ingestion, time-series DB, aggregation, hot/cold storage, query language.
- **Key Concepts:** Stream processing, OLAP vs OLTP, data partitioning, real-time aggregation, cost optimization

**Q2: Consistency Under Failure**
- **Scenario:** You have 3 data centers. Network partition splits them (A, B vs C). How do you maintain consistency? Availability? What trade-offs?
- **Probe:** CAP theorem. Which do you sacrifice?
- **Key Concepts:** CAP theorem, quorum-based consistency, multi-datacenter strategies, Byzantine failures

**Q3: Distributed Tracing at Scale**
- **Scenario:** A user request spans 10 microservices; latency is high. How do you trace it? 1M requests/sec, can't trace all (sampling cost). Design a sampling strategy.
- **Probe:** Trace sampling, tail latency, cost-aware sampling.
- **Key Concepts:** Distributed tracing, sampling, tail percentiles, cost, instrumentation

**Q4: Global Load Balancing**
- **Scenario:** You have data centers in 3 regions. Route user requests to the nearest DC, but handle region failure. How?
- **Probe:** DNS, BGP, geolocation, fallback, consistency.
- **Key Concepts:** Geographic routing, DNS-based LB, failover, consistency across regions, cost optimization

---

## Topic: Microservices

### Easy (Junior)

**Q1: Monolith vs Microservices**
- **Scenario:** You have a monolith with Users, Orders, Payments. Should you split into microservices? Why or why not?
- **Probe:** When are microservices beneficial?
- **Key Concepts:** Monolith, microservices, service boundaries, deployment independence

**Q2: Service Communication**
- **Scenario:** Service A (Orders) needs data from Service B (Inventory). How do they communicate?
- **Probe:** Sync (HTTP/gRPC) vs async (message queue)? Trade-offs?
- **Key Concepts:** RPC, message passing, coupling, latency

**Q3: API Gateway**
- **Scenario:** You have 5 microservices. Should clients talk directly to each or through a gateway?
- **Probe:** What does the gateway do?
- **Key Concepts:** API gateway, routing, cross-cutting concerns, single entry point

**Q4: Deployment**
- **Scenario:** Each microservice has its own DB. One service is slow. Can you restart just that service without affecting others?
- **Probe:** How is this different from a monolith?
- **Key Concepts:** Independent deployment, service isolation, database per service

### Medium (Mid)

**Q1: Distributed Transactions**
- **Scenario:** Order service calls Inventory to reserve stock, then Payment to charge. What if Inventory succeeds but Payment fails?
- **Probe:** How do you keep consistency? (Saga pattern, compensating actions)
- **Key Concepts:** Saga pattern, compensating transactions, eventual consistency, failure handling

**Q2: Service Discovery**
- **Scenario:** You have 100 instances of a service (auto-scaling). How does another service find them?
- **Probe:** Service registry, DNS, load balancer?
- **Key Concepts:** Service discovery, health checks, dynamic scaling, routing

**Q3: Circuit Breaker**
- **Scenario:** Service A calls Service B. Service B is slow/failing. How do you prevent cascading failures?
- **Probe:** Circuit breaker pattern. States?
- **Key Concepts:** Circuit breaker, open/half-open/closed states, fallback, resilience

**Q4: Versioning and Backward Compatibility**
- **Scenario:** You deploy a new Orders service API with a breaking change. Old clients break. How do you handle this?
- **Probe:** API versioning strategies. How do you retire old versions?
- **Key Concepts:** API versioning, backward compatibility, deprecation, migration

### Hard (Senior/Staff)

**Q1: Data Consistency in a Distributed System**
- **Scenario:** 5 microservices, each with its own DB. A business transaction involves all 5. How do you achieve consistency (eventual, strong, causal)?
- **Probe:** What's the weakest consistency model you can use?
- **Key Concepts:** Consistency models, eventual consistency, causal consistency, compensation, tradeoffs

**Q2: Failure Isolation and Resilience**
- **Scenario:** Service A fails; design the system so it doesn't cascade to B, C, D. Timeouts, retries, fallbacks, bulkheads. How do you orchestrate these?
- **Probe:** How do you test resilience (chaos engineering)?
- **Key Concepts:** Bulkheads, timeouts, retries, exponential backoff, chaos engineering, test strategies

**Q3: Cross-Service Authorization**
- **Scenario:** User service issues JWTs. Order service validates them. Inventory service also needs to validate. How do you distribute trust without repeating work?
- **Probe:** Token validation, caching, revocation.
- **Key Concepts:** Distributed auth, token validation, revocation lists, token caching, trust models

**Q4: Observability in Microservices**
- **Scenario:** A request spans 10 services; latency is bad. You have logs, metrics, traces from each service. How do you correlate them and debug the issue?
- **Probe:** Correlation IDs, structured logging, metrics tags, tracing.
- **Key Concepts:** Distributed logging, metrics correlation, distributed tracing, debugging strategies, cost optimization

---

## Topic: Security

### Easy (Junior)

**Q1: SQL Injection**
- **Scenario:** You write `SELECT * FROM users WHERE email = '` + userInput + `'`. A hacker sends `' OR '1'='1`. What happens? How do you prevent it?
- **Probe:** Parameterized queries?
- **Key Concepts:** SQL injection, parameterized queries, prepared statements, input validation

**Q2: Password Storage**
- **Scenario:** You store user passwords in your database. How should you store them? Plain text? Encrypted?
- **Probe:** Hashing vs encryption? Salt?
- **Key Concepts:** Password hashing, salt, bcrypt/scrypt, salting, slow hashing

**Q3: HTTPS and Certificates**
- **Scenario:** Your API is accessed over HTTP. A hacker intercepts traffic and steals session tokens. How do you prevent this?
- **Probe:** HTTPS, certificates?
- **Key Concepts:** TLS/SSL, certificates, MITM prevention, encryption in transit

**Q4: CORS**
- **Scenario:** Your frontend (example.com) calls your API (api.example.com). The browser blocks it. Why? How do you fix it?
- **Probe:** CORS headers?
- **Key Concepts:** CORS, same-origin policy, preflight, credentials, allowed origins

### Medium (Mid)

**Q1: Authentication vs Authorization**
- **Scenario:** User logs in (authentication). They request `/admin` endpoint. You need to check if they're an admin (authorization). Design both.
- **Probe:** JWT, sessions, roles, permissions.
- **Key Concepts:** Authentication, authorization, JWT, RBAC, permissions, claims

**Q2: JWT Vulnerabilities**
- **Scenario:** You use JWTs for auth. A hacker claims they're the admin (`{"role": "admin"}`), signs it with the wrong key, but you accept it. Why? How do you prevent?
- **Probe:** Key management, signature verification.
- **Key Concepts:** JWT structure, signing, key management, signature verification, algorithm selection

**Q3: API Key Management**
- **Scenario:** Your mobile app uses an API key (hard-coded). A hacker decompiles the app, finds the key, makes requests as your app. How do you prevent this?
- **Probe:** Key rotation, rate limiting, pinning?
- **Key Concepts:** API key rotation, rate limiting, certificate pinning, key leakage prevention

**Q4: Dependency Vulnerabilities**
- **Scenario:** Your app uses npm packages. One has a known RCE vulnerability. How do you find it? Fix it?
- **Probe:** Vulnerability scanning (npm audit, Snyk)?
- **Key Concepts:** Dependency scanning, CVE, updates, version pinning, supply chain security

### Hard (Senior/Staff)

**Q1: OAuth 2.0 and OpenID Connect**
- **Scenario:** Design a multi-tenant SaaS. Users log in with Google, Microsoft, custom OIDC. How do you implement OAuth flow? Token refresh?
- **Probe:** Authorization code flow, refresh tokens, token expiry, scope management.
- **Key Concepts:** OAuth 2.0, OpenID Connect, authorization code flow, refresh tokens, scopes, audience

**Q2: Encryption Key Rotation at Scale**
- **Scenario:** You encrypt user data with a master key. You need to rotate the key (compromise, compliance). 1B encrypted records. How do you rotate without re-encrypting everything?
- **Probe:** Envelope encryption, key derivation, versioning.
- **Key Concepts:** Envelope encryption, key versioning, derivation keys, zero-downtime rotation, audit

**Q3: CSRF Protection**
- **Scenario:** A hacker's site tricks your logged-in user into submitting a form to your bank API. You transfer money without knowing. How do you prevent?
- **Probe:** CSRF tokens, SameSite cookies?
- **Key Concepts:** CSRF, origin checking, CSRF tokens, SameSite attribute, double-submit cookies

**Q4: Zero-Trust Security Architecture**
- **Scenario:** Design a system where no entity is trusted by default. Every request must be authenticated and authorized. How do you implement this for 1000 internal services?
- **Probe:** mTLS, service mesh, PAM, audit logging.
- **Key Concepts:** Zero-trust, mutual TLS, service mesh, privileged access management, audit logging, least privilege

---

## Topic: Performance

### Easy (Junior)

**Q1: Profiling Basics**
- **Scenario:** Your endpoint is slow (1 second response time). How do you figure out why? (Database query? CPU? Network?)
- **Probe:** Logging, timing, tools?
- **Key Concepts:** Profiling, bottleneck identification, timing, basic measurements

**Q2: Database Query Optimization**
- **Scenario:** A query that fetches 100K rows is slow. You log it and see 1 second. Would you optimize the query or add caching?
- **Probe:** EXPLAIN, indexes, query rewriting.
- **Key Concepts:** Query plans, indexes, slow query logs, optimization techniques

**Q3: Caching Strategy**
- **Scenario:** A popular endpoint (10K req/min) queries the database every time. Caching could help. What should you cache? How long?
- **Probe:** TTL, invalidation, stale data.
- **Key Concepts:** Cache hit rate, TTL, invalidation, freshness, trade-offs

**Q4: Async Processing**
- **Scenario:** An endpoint sends an email, uploads a file, and logs an event—all in series (3 seconds). How do you speed it up?
- **Probe:** Async, parallel, queue?
- **Key Concepts:** Async I/O, parallelization, queueing, non-blocking

### Medium (Mid)

**Q1: Memory Profiling and Leaks**
- **Scenario:** Your app's memory grows from 100MB to 1GB over a week. You suspect a leak. How do you find it? Tools?
- **Probe:** Heap snapshots, diff, retained objects.
- **Key Concepts:** Heap dumps, memory analysis, retained objects, DOM nodes, event listeners

**Q2: Network Optimization**
- **Scenario:** Your API returns a 1MB JSON response. Frontend receives it in 2 seconds. How do you optimize?
- **Probe:** Compression (gzip), pagination, payload reduction?
- **Key Concepts:** Gzip compression, payload optimization, pagination, delta sync, bandwidth

**Q3: Database Connection Pooling**
- **Scenario:** You have 1000 concurrent requests, each opening a DB connection. Max connections = 100. What happens? How do you fix?
- **Probe:** Connection pool size, queue, wait times.
- **Key Concepts:** Connection pooling, queue depth, pool size tuning, connection timeout, backpressure

**Q4: Load Testing**
- **Scenario:** You claim your API can handle 10K req/sec. How do you test this? What should you measure?
- **Probe:** Tools (k6, JMeter), metrics (latency, throughput, error rate).
- **Key Concepts:** Load testing, throughput, latency percentiles, error rate, stress testing

### Hard (Senior/Staff)

**Q1: Distributed Systems Performance Tuning**
- **Scenario:** A global e-commerce system has p99 latency of 5 seconds (unacceptable). Request spans 5 services, multiple DBs. Design a profiling + optimization strategy.
- **Probe:** Bottleneck identification, trace analysis, optimization priorities.
- **Key Concepts:** Tail latency, distributed tracing, bottleneck identification, optimization ROI, cost-aware optimization

**Q2: Database Indexing at Scale**
- **Scenario:** You have a 10TB table with complex queries. You add an index; query is faster but writes slow down. Another index for a different query. Trade-offs?
- **Probe:** Index selectivity, write amplification, storage cost, multi-column indexes.
- **Key Concepts:** B-tree indexes, selectivity, write cost, storage, partial indexes, composite indexes

**Q3: Cache Coherence**
- **Scenario:** You cache in memory, Redis, and a CDN. Data updates in the DB. How do you ensure all caches are fresh? Consistency?
- **Probe:** Invalidation strategy, versioning, eventual consistency.
- **Key Concepts:** Cache invalidation, versioning, eventual consistency, cache coherence, conflict resolution

**Q4: Capacity Planning**
- **Scenario:** You forecast 100M users next year, 10x traffic. Estimate cost and infrastructure. How do you validate assumptions?
- **Probe:** Growth modeling, bottlenecks, cost simulation.
- **Key Concepts:** Capacity forecasting, bottleneck analysis, cost modeling, infrastructure planning, risk scenarios

---

## Topic: Testing

### Easy (Junior)

**Q1: Unit Testing Basics**
- **Scenario:** You write a function `add(a, b)`. How do you test it? What's a unit test?
- **Probe:** Test structure, assertions, edge cases.
- **Key Concepts:** Unit tests, test structure, assertions, AAA (Arrange-Act-Assert)

**Q2: Mocking and Stubbing**
- **Scenario:** Your function calls a database. In tests, you don't want to hit the real DB. How do you fake it?
- **Probe:** Mocks, stubs, spies.
- **Key Concepts:** Mocking, stubbing, test isolation, dependencies

**Q3: Integration Testing**
- **Scenario:** You test a full flow: API request → database → response. Is this a unit test or integration test?
- **Probe:** Differences, speed, what to test where.
- **Key Concepts:** Integration tests, end-to-end, speed, coverage trade-offs

**Q4: Test Coverage**
- **Scenario:** Your test coverage is 80%. Is that good? What should you focus on?
- **Probe:** Coverage metrics, critical paths, diminishing returns.
- **Key Concepts:** Code coverage, critical path testing, coverage goals, diminishing returns

### Medium (Mid)

**Q1: Async Test Handling**
- **Scenario:** You test an async function that returns a Promise. How do you write the test? What if it times out?
- **Probe:** done() callback, async/await, timeout.
- **Key Concepts:** Testing Promises, async/await in tests, timeouts, error handling

**Q2: Mocking External APIs**
- **Scenario:** Your function calls Stripe API. You don't want to hit the real API in tests. How do you mock it?
- **Probe:** Mock libraries (sinon, jest.mock), request matching.
- **Key Concepts:** API mocking, request matching, fixtures, realistic mocks

**Q3: Database Testing**
- **Scenario:** You test database queries. Do you use a real DB, in-memory, or mock? Trade-offs?
- **Probe:** Test database, fixtures, transactions, rollback.
- **Key Concepts:** Test database, fixtures, transaction rollback, test isolation, speed vs realism

**Q4: Flaky Tests**
- **Scenario:** A test passes 90% of the time, fails 10%. How do you debug and fix it?
- **Probe:** Timing issues, concurrency, environment dependencies.
- **Key Concepts:** Flaky tests, timing-dependent code, concurrency issues, test determinism

### Hard (Senior/Staff)

**Q1: Test Strategy at Scale**
- **Scenario:** You have 100K tests. They take 2 hours to run. Design a test strategy that's fast and covers critical paths.
- **Probe:** Test pyramid, priorities, parallelization, CI/CD.
- **Key Concepts:** Test pyramid, test priorities, parallelization, critical path testing, cost-aware testing

**Q2: Contract Testing for Microservices**
- **Scenario:** Service A calls Service B with a specific JSON schema. Service B changes the schema; A breaks. How do you detect this early?
- **Probe:** Contract testing, schema validation, compatibility.
- **Key Concepts:** Contract testing, schema versioning, API compatibility, pact testing

**Q3: Chaos Engineering**
- **Scenario:** You want to test if your system survives failures (network partition, disk full, service crash). Design a chaos engineering strategy.
- **Probe:** Fault injection, chaos experiments, hypotheses, learning.
- **Key Concepts:** Chaos engineering, failure injection, experiment design, observability, incident learnings

**Q4: Test Performance Analysis**
- **Scenario:** A test that takes 10 seconds to run blocks your CI pipeline. How do you optimize?
- **Probe:** Profiling, parallelization, fixtures, caching.
- **Key Concepts:** Test profiling, bottleneck identification, parallelization, fixture optimization, cost-benefit analysis
