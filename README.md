# 🧠 AI Prompt Pack for Developers — 120 Battle-Tested Prompts

> **For senior developers who use AI as a force multiplier, not a crutch.**
> Every prompt includes placeholders `[LIKE THIS]`, a "when to use" guide, and is designed for real production work — not toy examples.

### How to get the most out of this pack:

1. **Fill in every placeholder.** The more context you give, the better the output. "Write a REST endpoint" gives you garbage. The prompts below force you to provide what matters.
2. **Iterate.** First output is a draft. Say "add error handling for X edge case" or "use Y pattern instead."
3. **Combine prompts.** Use #2 (Data Model) → #1 (REST API) → #12 (Repository) → #54 (Unit Tests) for a complete feature.
4. **Customize and save.** Once you've tuned a prompt for your stack, save it. Your version > the template.

### Quick Reference — Prompt Categories:

| Category | Prompts | Best For |
|----------|---------|----------|
| Code Generation | #1–16 | Scaffolding features, patterns, and infrastructure |
| Debugging | #17–31 | Root-cause analysis, systematic troubleshooting |
| Code Review | #32–42 | Security, performance, and quality audits |
| Architecture | #43–53 | System design, tech decisions, scaling |
| Testing | #54–64 | Unit tests, integration tests, edge cases |
| Documentation | #65–75 | READMEs, API docs, ADRs, runbooks |
| Refactoring | #76–86 | Cleanup, modernization, pattern application |
| DevOps | #87–97 | Docker, CI/CD, K8s, monitoring, IaC |
| Database | #98–108 | Schema design, query optimization, migrations |
| AI/ML Integration | #109–120 | RAG, embeddings, LLM APIs, eval frameworks |

---

## 1. Code Generation

### 1. Full REST API Endpoint
**When to use:** You need a complete CRUD endpoint with validation and error handling.
```
Write a complete [METHOD] endpoint for [RESOURCE] in [LANGUAGE/FRAMEWORK].

Requirements:
- Input validation with clear error messages
- Proper HTTP status codes (200, 201, 400, 404, 500)
- Error handling with try/catch
- TypeScript types / type hints for all parameters and return values
- Comments explaining non-obvious logic

Request body: [DESCRIBE FIELDS AND TYPES]
Database: [DATABASE TYPE, e.g., PostgreSQL with Prisma / MongoDB with Mongoose]
Auth: [AUTH METHOD, e.g., JWT bearer token / API key / none]

Return the endpoint code, the data model/schema, and an example curl request.
```

### 2. Data Model / Schema Design
**When to use:** You need to define a data model from business requirements.
```
Design a data model for [ENTITY] in [ORM/DATABASE].

Business rules:
[LIST 3-5 BUSINESS RULES, e.g., "A user can have multiple orders", "Orders must have at least one item"]

Include:
- All fields with types, defaults, and constraints (required, unique, etc.)
- Relationships / foreign keys
- Indexes for common query patterns
- Created/updated timestamps
- Soft delete support if appropriate

Also suggest 3 queries that will be common for this model and show how to write them efficiently.
```

### 3. CLI Tool Scaffold
**When to use:** You need a command-line tool with argument parsing and help text.
```
Build a CLI tool in [LANGUAGE] that [DESCRIBE PURPOSE].

Commands:
[LIST COMMANDS AND WHAT THEY DO]

Requirements:
- Argument parsing with --help for each command
- Colored output for errors (red) and success (green)
- Exit codes (0 for success, 1 for error)
- Config file support (read from ~/.config/[TOOL_NAME]/config.[json/yaml])
- Verbose mode with --verbose flag

Use [LIBRARY, e.g., argparse / commander / clap] for argument parsing.
```

### 4. Middleware / Interceptor
**When to use:** You need request/response middleware for an API.
```
Write [FRAMEWORK] middleware that [DESCRIBE PURPOSE, e.g., "rate limits requests per API key"].

Behavior:
- [DESCRIBE TRIGGER CONDITIONS]
- [DESCRIBE WHAT IT SHOULD DO WHEN TRIGGERED]
- [DESCRIBE WHAT HEADERS/CONTEXT IT SHOULD ADD]

It should:
- Be configurable (not hardcoded values)
- Log actions at appropriate levels (debug for normal, warn for blocked)
- Not break if [EDGE CASE, e.g., "the header is missing"]
- Include TypeScript types / type annotations
- Have clear inline comments

Show how to register/use it in the app, plus a test case.
```

### 5. Webhook Handler
**When to use:** You need to receive and process webhooks from an external service.
```
Write a webhook handler in [FRAMEWORK] for [SERVICE, e.g., Stripe / GitHub / Twilio].

Events to handle:
[LIST EVENTS, e.g., "payment.succeeded", "payment.failed", "subscription.cancelled"]

Requirements:
- Signature verification using [SIGNING SECRET METHOD]
- Idempotency check (don't process the same event twice)
- Async processing (acknowledge immediately, process in background)
- Error handling that doesn't return 500 to the sender
- Logging of all received events
- Dead letter queue / retry logic for failed processing

Show the complete handler plus the signature verification helper function.
```

### 6. State Machine Implementation
**When to use:** You have an entity with defined states and transitions.
```
Implement a state machine in [LANGUAGE] for [ENTITY, e.g., "an order"] with these states and transitions:

States: [LIST STATES, e.g., draft → submitted → approved → fulfilled → completed]
Transitions:
- [STATE] → [STATE]: triggered by [EVENT], requires [CONDITIONS]
- [STATE] → [STATE]: triggered by [EVENT], requires [CONDITIONS]
[ADD MORE]

Invalid transitions should throw descriptive errors.
Include:
- A transition history log
- Guards/validators that run before each transition
- Hooks/callbacks that run after each transition
- Current state query method
- Serialization (to/from JSON for persistence)
```

### 7. Batch Processor
**When to use:** You need to process large datasets in chunks with progress tracking.
```
Write a batch processor in [LANGUAGE] that [DESCRIBE TASK, e.g., "migrates user records from old schema to new schema"].

Input: [DESCRIBE INPUT SOURCE, e.g., "PostgreSQL table with ~500K rows"]
Output: [DESCRIBE OUTPUT, e.g., "transformed records written to new table"]

Requirements:
- Process in configurable batch sizes (default 100)
- Progress bar / logging showing N/total processed
- Error handling: log failed items, continue processing
- Resume capability (track last processed ID)
- Configurable concurrency (default 5 parallel batches)
- Dry run mode that validates without writing
- Summary report at the end (processed, failed, skipped, duration)
```

### 8. Type-Safe API Client
**When to use:** You need a typed client for consuming a REST/GraphQL API.
```
Generate a type-safe API client in [LANGUAGE] for this API:

Base URL: [URL]
Auth: [AUTH METHOD]

Endpoints:
[LIST ENDPOINTS WITH METHOD, PATH, REQUEST BODY, RESPONSE BODY]

Requirements:
- Full type definitions for all request/response bodies
- Error type with status code, message, and optional details
- Automatic retry with exponential backoff (max 3 retries)
- Request/response logging in debug mode
- Timeout configuration (default 30s)
- Interceptor support for adding auth headers
```

### 9. Event Emitter / Pub-Sub System
**When to use:** You need decoupled components communicating through events.
```
Implement a typed event emitter / pub-sub system in [LANGUAGE].

Events:
[LIST EVENT NAMES AND THEIR PAYLOAD TYPES]

Features:
- Type-safe event names and payloads (no stringly-typed events)
- Subscribe / unsubscribe / once (single-fire)
- Wildcard subscribers (listen to all events)
- Async handler support
- Error handling (one failed handler shouldn't break others)
- Event history / replay for debugging
```

### 10. Configuration Parser
**When to use:** You need to load config from multiple sources with validation.
```
Build a configuration loader in [LANGUAGE] that:

1. Loads defaults from a hardcoded object
2. Overrides with values from [CONFIG FILE FORMAT, e.g., YAML / TOML / JSON]
3. Overrides with environment variables (prefixed with [PREFIX]_)
4. Validates the final config against a schema

Config shape:
[DESCRIBE YOUR CONFIG FIELDS AND TYPES]

Requirements:
- Type-safe access (no config["unknown_key"])
- Helpful error messages for invalid values
- Support for nested keys via env vars (e.g., PREFIX_DATABASE_HOST)
- .env file support
- Frozen/immutable after loading
```

### 11. Error Handling Pattern
**When to use:** You need a consistent error handling strategy across your app.
```
Design an error handling pattern for a [LANGUAGE/FRAMEWORK] application.

Error categories I need:
- Validation errors (user input problems)
- Authentication/Authorization errors
- Not found errors
- External service errors (API calls, database)
- Internal/unexpected errors

For each category, provide:
- A custom error class/type with appropriate fields
- How to throw/create it
- How it maps to HTTP status codes (if web app)
- How it should be logged (level, what to include)
- How it appears in API responses (user-safe message vs internal details)

Also provide a global error handler middleware that catches everything and formats responses consistently.
```

### 12. Database Repository Pattern
**When to use:** You want a clean data access layer with separation from business logic.
```
Implement the repository pattern in [LANGUAGE] for [ENTITY] using [DATABASE/ORM].

Model fields:
[LIST FIELDS WITH TYPES]

Methods needed:
- findById(id) → Entity | null
- findMany(filters, pagination, sorting) → { data: Entity[], total: number }
- create(data) → Entity
- update(id, partial data) → Entity
- delete(id) → void (soft delete)
- [ANY CUSTOM QUERIES, e.g., "findByEmail", "findActiveSubscriptions"]

Include:
- Input validation before database calls
- Proper error wrapping (don't leak ORM errors)
- Transaction support for multi-step operations
- Query builder for dynamic filters
```

### 13. Authentication Flow
**When to use:** You need a complete auth implementation.
```
Implement [AUTH TYPE, e.g., JWT / OAuth2 / session-based] authentication in [FRAMEWORK].

Features:
- Sign up with [FIELDS, e.g., email + password]
- Login → return tokens
- Token refresh
- Logout (invalidate tokens)
- Password reset flow
- [OPTIONAL: social login, MFA]

Security requirements:
- Password hashing with [bcrypt/argon2]
- Token expiry: access [15min], refresh [7 days]
- Rate limiting on login endpoint
- Account lockout after [N] failed attempts

Provide all route handlers, middleware, and helper functions.
```

### 14. Caching Layer
**When to use:** You need to add caching to reduce database/API load.
```
Implement a caching layer in [LANGUAGE] using [CACHE BACKEND, e.g., Redis / in-memory].

Patterns needed:
- Cache-aside (read-through) for [DESCRIBE READ-HEAVY ENDPOINT]
- Write-through for [DESCRIBE WRITE ENDPOINT]
- Cache invalidation when [DESCRIBE TRIGGER]

Requirements:
- Configurable TTL per cache key pattern
- Cache key generation that handles object parameters (deterministic serialization)
- Stampede protection (only one request populates cache on miss)
- Fallback to source on cache failure (don't break if Redis is down)
- Metrics: hit rate, miss rate, eviction count
- Clear/flush capability for debugging

Show the caching decorator/wrapper and how to apply it to existing functions.
```

### 15. Worker Queue / Background Jobs
**When to use:** You need to offload long-running tasks from request handlers.
```
Implement a background job system in [LANGUAGE] using [QUEUE BACKEND, e.g., Redis/BullMQ / RabbitMQ / SQS / in-memory].

Job types:
[LIST JOB NAMES AND WHAT THEY DO]

Requirements:
- Job scheduling (immediate, delayed, recurring/cron)
- Retry with exponential backoff (max [N] retries)
- Dead letter queue for permanently failed jobs
- Concurrency control (max [N] workers)
- Job priority levels
- Progress tracking and status queries
- Graceful shutdown (finish current job before stopping)

Show: job producer (enqueue), job consumer (worker), and a monitoring endpoint to check queue health.
```

### 16. Decorator / Wrapper Functions
**When to use:** You need reusable cross-cutting logic (logging, timing, caching, auth).
```
Write the following decorator/wrapper functions in [LANGUAGE]:

1. @timed / withTiming — logs execution duration
2. @retry(maxAttempts, backoffMs) — retries on failure
3. @cached(ttlSeconds) — memoizes with TTL
4. @rateLimit(maxCalls, windowMs) — throttles invocations
5. @validate(schema) — validates input before execution
6. @deprecated(message) — logs a deprecation warning on use

Each should:
- Preserve the original function's types/signature
- Be composable (can stack multiple decorators)
- Handle async functions properly
- Include a usage example
```

---

## 2. Debugging & Error Fixing

### 17. Stack Trace Analysis
**When to use:** You have an error stack trace and need to understand the root cause.
```
Analyze this error and stack trace. Identify the root cause, explain the chain of events that led to it, and provide a fix.

Error:
[PASTE THE FULL ERROR MESSAGE AND STACK TRACE]

Context:
- Language/framework: [LANGUAGE/FRAMEWORK]
- This happens when: [DESCRIBE WHEN THE ERROR OCCURS]
- It started after: [RECENT CHANGE, if known]

Please:
1. Identify the exact line/function where the error originates
2. Explain WHY this error occurs (not just what it means)
3. Provide the fix with code
4. Suggest how to prevent similar errors in the future
```

### 18. Systematic Debugging
**When to use:** Something is broken and you don't know where to start.
```
Help me systematically debug this issue:

What should happen: [EXPECTED BEHAVIOR]
What actually happens: [ACTUAL BEHAVIOR]
Environment: [LANGUAGE, FRAMEWORK, OS, relevant versions]

What I've already tried:
[LIST THINGS YOU'VE TRIED]

Relevant code:
[PASTE THE CODE YOU SUSPECT]

Please give me a systematic debugging plan:
1. What to check first (most likely causes)
2. How to isolate the problem (specific tests/logs to add)
3. What to look for in each step
4. Common gotchas for this type of issue in [FRAMEWORK]
```

### 19. Memory Leak Detection
**When to use:** Your app's memory usage grows over time.
```
Help me find a memory leak in my [LANGUAGE/FRAMEWORK] application.

Symptoms:
- Memory usage: [DESCRIBE PATTERN, e.g., "grows ~50MB/hour under normal load"]
- When it started: [DATE/CHANGE]
- What triggers it: [DESCRIBE TRIGGERS, e.g., "worse under high request volume"]

Suspected areas:
[PASTE CODE SECTIONS YOU SUSPECT]

Please:
1. Identify likely leak sources in this code
2. Explain the memory lifecycle issue for each
3. Provide fixes
4. Give me a checklist of common [LANGUAGE] memory leak patterns to audit
5. Suggest monitoring/profiling tools to confirm the fix
```

### 20. Race Condition Diagnosis
**When to use:** You have intermittent bugs that seem timing-dependent.
```
I suspect a race condition in this code. The bug occurs intermittently (~[FREQUENCY]).

Code:
[PASTE THE CONCURRENT/ASYNC CODE]

Symptoms:
- [DESCRIBE WHAT GOES WRONG, e.g., "duplicate records created", "stale data returned"]
- Happens more under: [HIGH LOAD / SPECIFIC TIMING / etc.]

Please:
1. Identify all possible race conditions in this code
2. Explain the exact interleaving of operations that causes each bug
3. Provide thread-safe / concurrency-safe fixes
4. Suggest how to write a test that reliably reproduces this
```

### 21. Performance Profiling
**When to use:** An endpoint or function is slow and you need to find the bottleneck.
```
This [FUNCTION/ENDPOINT] is too slow. Help me profile and optimize it.

Current performance: [CURRENT LATENCY, e.g., "~2.5s average response time"]
Target: [TARGET, e.g., "<200ms"]
Traffic: [REQUESTS/SEC]

Code:
[PASTE THE SLOW CODE]

Please:
1. Identify the likely bottlenecks (rank by impact)
2. For each bottleneck, explain WHY it's slow
3. Provide an optimized version with comments explaining each improvement
4. Estimate the expected improvement for each change
5. Suggest what to measure/profile to validate improvements
```

### 22. Dependency Conflict Resolution
**When to use:** You have version conflicts or incompatible dependencies.
```
I'm getting dependency conflicts in my [LANGUAGE] project:

Error:
[PASTE THE DEPENDENCY ERROR]

My dependencies:
[PASTE package.json / requirements.txt / Cargo.toml / etc.]

Please:
1. Explain what's conflicting and why
2. Provide the minimum changes to resolve it
3. Flag any security concerns with the resolved versions
4. Suggest if any dependencies should be replaced with alternatives
```

### 23. Silent Failure Investigation
**When to use:** Something isn't working but there are no errors.
```
My code runs without errors but produces wrong results.

Expected output: [WHAT SHOULD HAPPEN]
Actual output: [WHAT ACTUALLY HAPPENS]

Code:
[PASTE YOUR CODE]

Input data sample:
[PASTE SAMPLE INPUT]

Please:
1. Trace through the code step-by-step with my input data
2. Identify where the logic diverges from expectations
3. Explain the bug
4. Provide the fix
5. Suggest assertions/checks I should add to catch this class of bug
```

### 24. API Error Diagnosis
**When to use:** You're getting unexpected errors from an API you're calling.
```
I'm getting [STATUS CODE] errors from [API/SERVICE]:

Request:
[METHOD] [URL]
Headers: [HEADERS]
Body: [BODY]

Response:
Status: [STATUS CODE]
Body: [RESPONSE BODY]

My code:
[PASTE THE CODE MAKING THE REQUEST]

This worked before and broke [WHEN/AFTER WHAT CHANGE].

Please:
1. Diagnose the likely cause based on the status code and response
2. Check my request for common mistakes
3. Suggest fixes
4. Provide a working curl command I can use to test independently
```

### 25. Log Analysis
**When to use:** You have logs but need help finding the relevant signal.
```
Help me analyze these logs to find the issue:

Problem: [DESCRIBE THE ISSUE YOU'RE INVESTIGATING]
Timeframe: [WHEN THE ISSUE OCCURRED]

Logs:
[PASTE RELEVANT LOG SECTION]

Please:
1. Identify the key events/errors in this log
2. Build a timeline of what happened
3. Highlight the root cause entry
4. Suggest what additional logging would help next time
5. Provide a grep/jq command to filter for this issue in the future
```

### 26. Regression Hunting
**When to use:** Something that used to work is now broken.
```
A feature that was working is now broken. Help me find the regression.

What broke: [DESCRIBE THE BROKEN BEHAVIOR]
When it last worked: [DATE/VERSION/COMMIT]
Recent changes since then:
[LIST RECENT CHANGES, or paste git log --oneline]

Relevant code (current):
[PASTE CURRENT CODE]

Please:
1. Based on the symptom and recent changes, rank which changes most likely caused it
2. For each suspect change, explain how it could cause this specific regression
3. Suggest a git bisect strategy or specific commits to test
4. Provide a targeted test case that would catch this regression
```

### 27. Flaky Test Diagnosis
**When to use:** Tests pass sometimes and fail sometimes.
```
This test is flaky — it passes ~[N]% of the time.

Test code:
[PASTE THE FLAKY TEST]

Code being tested:
[PASTE THE SOURCE CODE]

Error when it fails:
[PASTE THE FAILURE OUTPUT]

Please:
1. Identify why this test is non-deterministic
2. List all sources of flakiness (timing, ordering, shared state, external dependencies)
3. Rewrite the test to be deterministic
4. Suggest what testing patterns to avoid to prevent flaky tests
```

### 28. Timeout Debugging
**When to use:** Operations are timing out unexpectedly.
```
[OPERATION, e.g., "Database queries" / "API calls" / "Websocket connections"] are timing out.

Error: [PASTE TIMEOUT ERROR]
Timeout setting: [CURRENT TIMEOUT VALUE]
Frequency: [HOW OFTEN, e.g., "~5% of requests"]

Environment:
- [LANGUAGE/FRAMEWORK]
- [DATABASE/SERVICE DETAILS]
- [INFRASTRUCTURE, e.g., "running in Docker on AWS ECS"]

Code:
[PASTE THE CODE THAT TIMES OUT]

Please:
1. List all possible causes for these timeouts (ranked by likelihood)
2. For each cause, provide a diagnostic step to confirm/rule out
3. Suggest both quick fixes (increase timeout) and proper fixes (address root cause)
4. Provide monitoring queries/commands to track timeout patterns
```

### 29. Data Corruption Investigation
**When to use:** Data in your database/store doesn't match what it should be.
```
I'm finding corrupted/inconsistent data in my [DATABASE]:

Expected state: [WHAT THE DATA SHOULD LOOK LIKE]
Actual state: [WHAT IT LOOKS LIKE]
Affected records: [SCOPE, e.g., "~200 user records created after Jan 15"]

Suspected code paths that write to this data:
[PASTE RELEVANT CODE]

Please:
1. Identify which code path could produce this corruption
2. Explain the sequence of events that leads to bad data
3. Provide a SQL/query to identify all affected records
4. Provide a fix for the code
5. Provide a migration/script to repair the corrupted data
6. Suggest a data integrity check to run periodically
```

### 30. Concurrency Bug Analysis
**When to use:** You have issues with concurrent access to shared resources.
```
I have a concurrency issue in my [LANGUAGE] application:

Symptom: [DESCRIBE, e.g., "counter is inaccurate under high load", "duplicate records"]
Architecture: [DESCRIBE, e.g., "3 API server instances behind a load balancer"]

Code:
[PASTE THE CODE WITH SHARED STATE]

Please:
1. Identify the critical section(s) and shared resources
2. Explain exactly how concurrent access breaks this
3. Provide a fix using appropriate concurrency primitives ([LANGUAGE]-specific)
4. Compare approaches: locks vs optimistic concurrency vs atomic operations
5. Show how to test this with concurrent load
```

### 31. Environment Issue Diagnosis
**When to use:** Code works in one environment but not another.
```
My code works in [WORKING ENV, e.g., "local dev"] but fails in [BROKEN ENV, e.g., "production"].

Error in [BROKEN ENV]:
[PASTE ERROR]

Differences between environments:
[LIST KNOWN DIFFERENCES — OS, runtime version, env vars, network, permissions]

Code:
[PASTE RELEVANT CODE]

Please:
1. Based on the error, identify likely environment-specific causes
2. Provide diagnostic commands to run in both environments to compare
3. Suggest fixes that work across both environments
4. Recommend practices to prevent "works on my machine" issues
```

---

## 3. Code Review

### 32. Full Security Audit
**When to use:** You want to check code for security vulnerabilities before deploying.
```
Perform a security audit of this code. Treat this as a pre-production review.

Code:
[PASTE YOUR CODE]

Context: This is a [DESCRIBE — web API, CLI tool, data pipeline, etc.] in [LANGUAGE/FRAMEWORK].
Auth method: [HOW USERS AUTHENTICATE]
Data sensitivity: [DESCRIBE — PII, financial, public, etc.]

Check for:
- Injection vulnerabilities (SQL, XSS, command injection, SSRF)
- Authentication/authorization bypasses
- Data exposure (sensitive data in logs, responses, errors)
- Insecure defaults or configurations
- Missing input validation/sanitization
- Cryptographic issues (weak hashing, hardcoded secrets)
- Dependency vulnerabilities

For each finding:
1. Severity (Critical / High / Medium / Low)
2. Exact location in the code
3. Exploitation scenario
4. Fix with code
```

### 33. Performance Review
**When to use:** You want to identify performance bottlenecks in code.
```
Review this code for performance issues:

Code:
[PASTE YOUR CODE]

Context:
- Expected load: [REQUESTS/SEC or RECORDS/BATCH]
- Current performance: [IF KNOWN]
- Database: [TYPE]
- Infrastructure: [DESCRIBE]

Identify:
1. N+1 queries or unnecessary database calls
2. Missing indexes (based on query patterns)
3. Unbounded operations (loading everything into memory)
4. Blocking operations that should be async
5. Missing caching opportunities
6. Inefficient algorithms or data structures
7. Resource leaks (connections, file handles)

For each issue, provide the optimized version and expected improvement.
```

### 34. Error Handling Review
**When to use:** You want to ensure your error handling is robust and consistent.
```
Review the error handling in this code:

Code:
[PASTE YOUR CODE]

Check for:
1. Swallowed errors (catch blocks that don't log or rethrow)
2. Generic catch-all handlers that hide specific errors
3. Missing error handling on async operations
4. User-facing messages that leak internal details
5. Missing cleanup/finally blocks for resources
6. Inconsistent error response formats
7. Errors that should be retried vs. reported
8. Missing error boundaries / circuit breakers

For each issue, show the current problematic code and the improved version.
```

### 35. API Design Review
**When to use:** You want feedback on your API design before implementing.
```
Review this API design for best practices:

Endpoints:
[LIST YOUR ENDPOINTS — METHOD, PATH, REQUEST/RESPONSE BODIES]

Check against:
1. RESTful conventions (resource naming, HTTP methods, status codes)
2. Consistency across endpoints
3. Pagination for list endpoints
4. Filtering, sorting, and searching patterns
5. Versioning strategy
6. Error response format
7. Authentication/authorization granularity
8. Rate limiting considerations
9. Backward compatibility concerns
10. Missing endpoints that clients will likely need

Provide a revised API spec with improvements and reasoning for each change.
```

### 36. Database Query Review
**When to use:** You want to optimize your database queries.
```
Review these database queries for correctness and performance:

Queries:
[PASTE YOUR QUERIES]

Schema:
[PASTE RELEVANT SCHEMA / CREATE TABLE STATEMENTS]

Expected data volume: [ROW COUNTS FOR RELEVANT TABLES]

Check for:
1. Missing indexes for WHERE/JOIN/ORDER BY columns
2. Full table scans
3. Cartesian joins
4. SELECT * when specific columns would suffice
5. N+1 patterns (in application code calling these)
6. Subqueries that should be JOINs (or vice versa)
7. Missing LIMIT on potentially large result sets
8. Lock contention risks

Provide EXPLAIN analysis predictions and optimized queries.
```

### 37. Test Coverage Gap Analysis
**When to use:** You want to find what's missing from your test suite.
```
Analyze the test coverage gaps for this code:

Source code:
[PASTE THE SOURCE CODE]

Current tests:
[PASTE EXISTING TESTS]

Identify:
1. Code paths not covered by any test
2. Edge cases not tested (null, empty, boundary values, overflow)
3. Error paths not tested (what happens when things fail?)
4. Integration points not tested
5. Race conditions or timing-dependent behavior not tested

For each gap, write the missing test with clear assertions.
```

### 38. Code Smell Detection
**When to use:** You want a general quality review to improve maintainability.
```
Review this code for code smells and maintainability issues:

Code:
[PASTE YOUR CODE]

Identify:
1. Functions/methods that are too long (>30 lines)
2. High cyclomatic complexity (deeply nested conditionals)
3. God objects / classes with too many responsibilities
4. Magic numbers / hardcoded values that should be constants
5. Dead code or unreachable branches
6. Inconsistent naming conventions
7. Missing abstractions (repeated patterns that should be extracted)
8. Tight coupling between components
9. Violations of [PRINCIPLE, e.g., SOLID / DRY / KISS]

For each smell, rate the severity and provide a refactored version.
```

### 39. Dependency Risk Review
**When to use:** You want to audit your project's dependencies.
```
Review my project's dependencies for risk:

Dependencies:
[PASTE package.json / requirements.txt / go.mod / etc.]

For each dependency, assess:
1. Is it actively maintained? (Last commit, open issues, bus factor)
2. Are there known security vulnerabilities?
3. Is it the right choice vs. alternatives?
4. Could this be replaced with built-in language features?
5. License compatibility with [YOUR LICENSE, e.g., MIT / commercial]

Flag any dependencies that are:
- Abandoned (no updates in 12+ months)
- Have known CVEs
- Are unnecessarily heavy for what they do
- Have problematic licenses

Suggest replacements where appropriate.
```

### 40. Naming and Readability Review
**When to use:** You want to improve code clarity for your team.
```
Review this code purely for naming and readability:

Code:
[PASTE YOUR CODE]

Check:
1. Variable/function names: Are they descriptive? Could a new team member understand them?
2. Abbreviations: Are any confusing or inconsistent?
3. Boolean names: Do they read naturally? (e.g., isReady, hasPermission, shouldRetry)
4. Function names: Do they describe what the function DOES, not HOW?
5. Consistency: Same concept = same name throughout?
6. Comments: Are they necessary? Do any explain WHAT (bad) vs WHY (good)?
7. Code structure: Is the reading flow logical? (setup → action → result)

Provide renamed versions with reasoning. Don't change logic — only names and structure.
```

### 41. Architecture Compliance Review
**When to use:** You want to ensure code follows your team's architectural patterns.
```
Review this code for compliance with our architectural standards:

Our architecture:
[DESCRIBE YOUR ARCHITECTURE PATTERN — layered, hexagonal, CQRS, microservices, etc.]

Our rules:
[LIST KEY RULES, e.g.:
- Controllers should not contain business logic
- Database access only through repositories
- All external calls go through adapters
- Events for cross-service communication]

Code to review:
[PASTE YOUR CODE]

For each violation:
1. What rule is broken
2. Why this matters (what goes wrong if we allow it)
3. How to refactor to comply
```

### 42. Accessibility Review
**When to use:** You need to check frontend code for accessibility compliance.
```
Review this [HTML/React/Vue] code for accessibility (WCAG 2.1 AA compliance):

Code:
[PASTE YOUR FRONTEND CODE]

Check for:
1. Missing/incorrect ARIA labels and roles
2. Keyboard navigation (tab order, focus management)
3. Color contrast issues (describe any colors used)
4. Missing alt text for images
5. Form labels and error messaging
6. Screen reader compatibility
7. Focus traps in modals/dropdowns
8. Dynamic content announcements (aria-live)
9. Touch target sizes (minimum 44x44px)
10. Semantic HTML usage

For each issue, provide the fix and explain which WCAG criterion it violates.
```

---

## 4. Architecture & Design

### 43. System Design from Requirements
**When to use:** You need to design a system from business requirements.
```
Design a system for [DESCRIBE THE PRODUCT/FEATURE].

Requirements:
[LIST FUNCTIONAL REQUIREMENTS]

Non-functional requirements:
- Expected users: [NUMBER]
- Requests/sec: [NUMBER]
- Availability: [TARGET, e.g., 99.9%]
- Data retention: [DURATION]
- Latency: [TARGET, e.g., p99 < 200ms]

Provide:
1. High-level architecture diagram (describe in text)
2. Component breakdown with responsibilities
3. Data flow for the [N] most important operations
4. Technology recommendations with reasoning
5. Database schema (key tables/collections)
6. API contracts (key endpoints)
7. Scaling strategy (what changes at 10x, 100x current load)
8. Key trade-offs you're making and why
```

### 44. Microservices Decomposition
**When to use:** You need to break a monolith into services or design new microservices.
```
Help me decompose this system into microservices:

Current monolith / system:
[DESCRIBE THE SYSTEM AND ITS MAIN FUNCTIONS]

Domain areas:
[LIST THE MAIN BUSINESS DOMAINS]

For each proposed service, provide:
1. Name and bounded context
2. Responsibilities (what it owns)
3. Data it owns (tables/collections)
4. APIs it exposes
5. Events it publishes and subscribes to
6. Dependencies on other services

Also address:
- How to handle distributed transactions
- Service-to-service authentication
- Data consistency strategy
- What should stay in a shared library vs. per-service
- Migration strategy from monolith (which service to extract first and why)
```

### 45. API Contract Design
**When to use:** You need to design an API that multiple teams/clients will consume.
```
Design an API contract for [FEATURE/SYSTEM]:

Consumers: [WHO WILL USE THIS API — web app, mobile, third-party, internal services]
Core operations: [LIST WHAT USERS NEED TO DO]

Provide:
1. OpenAPI/Swagger-style spec (YAML) with all endpoints
2. Request/response schemas with examples
3. Error response format (consistent across all endpoints)
4. Authentication scheme
5. Pagination, filtering, sorting conventions
6. Rate limiting tiers
7. Versioning strategy
8. Webhook/callback spec (if applicable)
9. SDK usage examples in [LANGUAGE]

Optimize for: [CHOOSE — developer experience / performance / backward compatibility]
```

### 46. Database Schema Design
**When to use:** You need to design a database from scratch for a new feature.
```
Design a database schema for [FEATURE/SYSTEM]:

Entities and relationships:
[DESCRIBE YOUR DOMAIN MODEL IN PLAIN ENGLISH]

Requirements:
- Database type: [PostgreSQL / MySQL / MongoDB / etc.]
- Expected data volume: [ROWS PER TABLE / GROWTH RATE]
- Read/write ratio: [e.g., 80% reads, 20% writes]
- Key query patterns: [LIST THE MOST COMMON QUERIES]

Provide:
1. Complete schema (CREATE TABLE statements or equivalent)
2. Indexes for each common query pattern
3. Constraints (unique, check, foreign key)
4. Partitioning strategy (if applicable)
5. Migration script (initial setup)
6. Seed data for development
7. Explain normalization decisions (when you chose to denormalize, why)
```

### 47. Caching Strategy
**When to use:** You need to add caching to improve performance.
```
Design a caching strategy for [SYSTEM/FEATURE]:

Current architecture:
[DESCRIBE YOUR SYSTEM — services, databases, API patterns]

Hot paths (what's slow):
[LIST THE OPERATIONS THAT NEED CACHING]

For each cached resource, specify:
1. Cache location (browser, CDN, application, database query cache)
2. Cache key pattern
3. TTL and eviction policy
4. Invalidation trigger (when does cached data become stale?)
5. Cache-miss behavior (stale-while-revalidate? block until fresh?)
6. Consistency guarantees (how stale is acceptable?)

Also address:
- Cold start / cache warming strategy
- Thundering herd protection
- Monitoring (hit rate, memory usage)
- What NOT to cache and why
```

### 48. Event-Driven Architecture
**When to use:** You need to design an event-driven system.
```
Design an event-driven architecture for [SYSTEM]:

Current architecture: [DESCRIBE CURRENT SYNCHRONOUS FLOW]
Why events: [WHAT PROBLEM ARE YOU SOLVING — decoupling, scaling, audit trail, etc.]

Provide:
1. Event catalog (name, payload schema, producer, consumers)
2. Event broker choice (Kafka/RabbitMQ/SNS+SQS/etc.) with reasoning
3. Event schema evolution strategy
4. Ordering guarantees (which events need ordering?)
5. Idempotency strategy for consumers
6. Dead letter queue handling
7. Event replay capability
8. Monitoring and alerting for event lag/failures
9. Migration plan from synchronous to event-driven
```

### 49. Authentication & Authorization Design
**When to use:** You need to design an auth system.
```
Design authentication and authorization for [SYSTEM]:

User types: [LIST USER ROLES AND THEIR PERMISSIONS]
Auth requirements:
- [LIST REQUIREMENTS, e.g., "SSO with Google", "API keys for service accounts", "MFA for admin users"]

Provide:
1. Auth flow diagrams (signup, login, token refresh, logout)
2. Token strategy (JWT structure, claims, expiry)
3. Authorization model (RBAC / ABAC / ACL)
4. Permission definitions and role-to-permission mapping
5. API protection (how middleware checks auth)
6. Session management strategy
7. Security considerations (token storage, CSRF, XSS protection)
8. Implementation plan (which components to build, which to use off-the-shelf)
```

### 50. Scaling Plan
**When to use:** You need to plan how your system will handle growth.
```
Create a scaling plan for [SYSTEM]:

Current state:
- Users: [NUMBER]
- Requests/sec: [NUMBER]
- Database size: [SIZE]
- Infrastructure: [DESCRIBE — single server, cloud, containers, etc.]

Growth targets:
- 6 months: [PROJECTED NUMBERS]
- 12 months: [PROJECTED NUMBERS]
- 24 months: [PROJECTED NUMBERS]

For each growth stage, provide:
1. Bottleneck analysis (what breaks first?)
2. Infrastructure changes needed
3. Application changes needed (connection pooling, caching, async, etc.)
4. Database scaling (read replicas, sharding, etc.)
5. Cost estimate (rough monthly infrastructure cost)
6. Effort estimate (engineering weeks)
7. Risk assessment (what could go wrong at each stage)

Prioritize changes by: impact / effort ratio
```

### 51. Migration Strategy
**When to use:** You need to migrate between technologies, databases, or architectures.
```
Plan a migration from [CURRENT STATE] to [TARGET STATE]:

Current: [DESCRIBE CURRENT SYSTEM]
Target: [DESCRIBE TARGET SYSTEM]
Why: [BUSINESS/TECHNICAL REASON]

Constraints:
- Zero/minimal downtime requirement: [YES/NO]
- Data volume: [SIZE]
- Timeline: [TARGET COMPLETION]
- Team size: [NUMBER]

Provide:
1. Migration phases with clear milestones
2. Data migration plan (ETL pipeline, dual-write, etc.)
3. Rollback plan for each phase
4. Testing strategy (how to verify correctness)
5. Feature flag / gradual rollout plan
6. Communication plan for stakeholders
7. Risk register with mitigations
8. Go/no-go criteria for each phase
```

### 52. Tech Stack Evaluation
**When to use:** You need to choose technologies for a new project.
```
Help me evaluate tech stacks for [PROJECT]:

Project requirements:
[LIST KEY REQUIREMENTS]

Team: [SIZE, EXPERIENCE LEVEL, EXISTING EXPERTISE]
Timeline: [DEADLINE]
Budget: [CONSTRAINTS]

Compare these options:
[LIST 2-3 OPTIONS, e.g., "Next.js + PostgreSQL vs. Django + PostgreSQL vs. Rails + PostgreSQL"]

For each option, evaluate:
1. Suitability for requirements (score 1-10)
2. Team ramp-up time
3. Development speed (time to MVP)
4. Long-term maintenance burden
5. Ecosystem (libraries, community, hiring)
6. Performance characteristics
7. Hosting/infrastructure costs
8. Scalability ceiling

Provide a recommendation with clear reasoning.
```

### 53. Trade-Off Analysis
**When to use:** You need to make a technical decision and want structured analysis.
```
Help me analyze this technical trade-off:

Decision: [DESCRIBE THE DECISION, e.g., "SQL vs. NoSQL for our user analytics data"]

Option A: [DESCRIBE]
Option B: [DESCRIBE]
[Option C: DESCRIBE, if applicable]

Context:
- Team: [SIZE, EXPERTISE]
- Timeline: [URGENCY]
- Scale: [CURRENT AND EXPECTED]
- Constraints: [HARD REQUIREMENTS]

For each option, analyze:
1. Pros (with weight: how much does this matter?)
2. Cons (with weight)
3. Risks (with probability and mitigation)
4. Total cost of ownership (setup + ongoing)
5. Reversibility (how hard to switch later?)
6. Hidden costs people usually miss

Provide a decision matrix and your recommendation.
```

---

## 5. Testing

### 54. Unit Test Generation
**When to use:** You need unit tests for a function or class.
```
Write comprehensive unit tests for this code:

Code:
[PASTE YOUR CODE]

Testing framework: [FRAMEWORK, e.g., Jest / pytest / Go testing / JUnit]

Cover:
1. Happy path (expected inputs → expected outputs)
2. Edge cases (empty, null, boundary values, maximum values)
3. Error cases (invalid inputs, missing data, network failures)
4. Type edge cases (wrong types, special characters, unicode)

For each test:
- Descriptive test name that reads like a sentence
- Arrange / Act / Assert structure
- Clear comments for non-obvious test cases
- Mock external dependencies

Target: 90%+ code coverage. List any lines you can't test and why.
```

### 55. Integration Test Planning
**When to use:** You need to test how components work together.
```
Design integration tests for [FEATURE/SYSTEM]:

Components involved:
[LIST COMPONENTS AND HOW THEY INTERACT]

External dependencies:
[LIST DATABASES, APIs, QUEUES, etc.]

Provide:
1. Test scenarios (user journey / data flow through the system)
2. Test setup (database seeding, mock servers, test containers)
3. Test code for each scenario
4. Cleanup/teardown strategy
5. How to run these in CI (Docker Compose, test containers, etc.)
6. What to mock vs. what to test with real instances

Framework: [FRAMEWORK]
```

### 56. Edge Case Discovery
**When to use:** You want to find edge cases you haven't thought of.
```
Identify edge cases for this function/feature:

Code:
[PASTE YOUR CODE]

What it does: [DESCRIBE THE FUNCTION'S PURPOSE]
Input types: [DESCRIBE EXPECTED INPUTS]

Generate edge cases in these categories:
1. Boundary values (min, max, off-by-one)
2. Empty/null/undefined inputs
3. Type mismatches
4. Unicode / special characters / encoding issues
5. Concurrency (if applicable)
6. Large inputs (performance / memory)
7. Time-related (timezones, DST, leap years, epoch)
8. State-dependent (first run, after error, cache cold/warm)

For each edge case, provide:
- A test case with input and expected output
- Why this edge case matters (what bug it would catch)
```

### 57. Mock and Stub Creation
**When to use:** You need to mock dependencies for isolated testing.
```
Create mocks/stubs for these dependencies so I can test [MODULE] in isolation:

Module under test:
[PASTE YOUR CODE]

Dependencies to mock:
[LIST DEPENDENCIES — database, API clients, file system, etc.]

For each dependency, create:
1. A mock implementation with configurable responses
2. Spy capability (track what methods were called with what args)
3. Failure simulation (make the mock throw errors)
4. Realistic test data fixtures

Testing framework: [FRAMEWORK]
Show how to inject the mocks and write a test using them.
```

### 58. Test Data Generation
**When to use:** You need realistic test data for testing or development.
```
Generate test data for [SYSTEM/FEATURE]:

Schema:
[PASTE YOUR DATA MODEL / SCHEMA]

Generate:
- [N] records for [ENTITY]
- With realistic values (not just "test1", "test2")
- Including edge cases (long names, special characters, null optional fields)
- With valid relationships between entities
- In [FORMAT: JSON / SQL INSERT / CSV / factory functions]

Also create:
1. A "happy path" dataset (everything valid and complete)
2. An "edge case" dataset (boundary values, optional fields null)
3. A "stress test" dataset (maximum lengths, many relationships)

If using factory functions, make them composable (e.g., createUser({ overrides })).
```

### 59. API Endpoint Testing
**When to use:** You need to test your REST/GraphQL API endpoints.
```
Write API tests for these endpoints:

Endpoints:
[LIST ENDPOINTS WITH METHOD, PATH, EXPECTED REQUEST/RESPONSE]

Test each endpoint for:
1. Successful request with valid data
2. Validation errors (missing fields, wrong types, invalid values)
3. Authentication (no token, expired token, wrong permissions)
4. Not found (non-existent resource)
5. Conflict (duplicate creation, concurrent updates)
6. Rate limiting response

Framework: [FRAMEWORK, e.g., supertest / httpx / RestAssured]
Include test setup (seed data, auth tokens) and cleanup.
```

### 60. Error Path Testing
**When to use:** You want to test what happens when things fail.
```
Write tests for the failure modes of this code:

Code:
[PASTE YOUR CODE]

Test these failure scenarios:
1. Network failures (API calls that timeout or fail)
2. Database failures (connection lost, query errors, deadlocks)
3. Invalid state (data that shouldn't exist but does)
4. Resource exhaustion (memory, disk, connections)
5. Permission errors (file access, API authorization)
6. Partial failures (2 of 3 operations succeed, one fails)

For each scenario:
- How to simulate the failure (mock setup)
- Expected behavior (graceful degradation, retry, error message)
- Assertion on side effects (did it clean up? did it log? did it alert?)

Framework: [FRAMEWORK]
```

### 61. Performance Test Script
**When to use:** You need to load test an endpoint or system.
```
Write a performance test for [ENDPOINT/SYSTEM]:

Target: [URL/ENDPOINT]
Load profile:
- Ramp up: [N] users over [T] seconds
- Sustain: [N] concurrent users for [T] minutes
- Peak: [N] concurrent users

Scenarios to test:
[LIST USER JOURNEYS, e.g., "login → browse → add to cart → checkout"]

Metrics to capture:
- Response time (p50, p95, p99)
- Throughput (requests/sec)
- Error rate
- Resource utilization

Tool: [k6 / Artillery / Locust / JMeter]
Include: test script, configuration, and how to analyze the results.
```

### 62. Security Test Cases
**When to use:** You need to test for security vulnerabilities.
```
Write security test cases for [FEATURE/API]:

Code/endpoints:
[PASTE OR DESCRIBE WHAT TO TEST]

Test for:
1. SQL injection (all input fields)
2. XSS (stored and reflected)
3. CSRF token validation
4. Authentication bypass
5. Authorization escalation (access other users' data)
6. Rate limiting enforcement
7. Input size limits (request body, file uploads)
8. Header injection
9. Path traversal
10. SSRF (if the app makes outbound requests)

For each test:
- Malicious input/payload
- Expected behavior (blocked, sanitized, error)
- How to automate this check in CI

Framework: [FRAMEWORK]
```

### 63. Regression Test Suite
**When to use:** You need tests that catch regressions when code changes.
```
Design a regression test suite for [FEATURE]:

Feature description:
[DESCRIBE THE FEATURE AND ITS KEY BEHAVIORS]

Recent bugs that were fixed:
[LIST BUGS WITH DESCRIPTIONS]

Create tests that:
1. Verify each key behavior still works after code changes
2. Specifically prevent each historical bug from recurring
3. Test integration points with adjacent features
4. Run fast enough for CI (target: <[N] seconds total)

Organize tests by:
- Smoke tests (critical path, run always)
- Regression tests (specific bug prevention)
- Full suite (comprehensive, run before release)

Framework: [FRAMEWORK]
```

### 64. Snapshot Testing Setup
**When to use:** You want to detect unexpected output changes.
```
Set up snapshot testing for [COMPONENT/FUNCTION]:

Code:
[PASTE YOUR CODE]

Create snapshot tests that capture:
1. [OUTPUT TYPE: HTML output / JSON response / CLI output / etc.]
2. For each key input scenario: [LIST SCENARIOS]

Include:
- Initial snapshot creation
- How to review and update snapshots when intentional changes are made
- Strategy for handling dynamic values (timestamps, IDs) in snapshots
- CI configuration (fail on snapshot mismatch)

Framework: [FRAMEWORK]
When should snapshot tests be used vs. explicit assertion tests? Provide guidelines.
```

---

## 6. Documentation

### 65. README Generation
**When to use:** You need a README for a project or library.
```
Write a comprehensive README.md for this project:

Project: [NAME]
What it does: [DESCRIPTION]
Tech stack: [LANGUAGES, FRAMEWORKS]
Target audience: [WHO USES THIS]

Include these sections:
1. Badges (build status, version, license)
2. One-line description + longer overview
3. Features list
4. Quick start (install + hello world in <5 steps)
5. Installation (all methods: npm/pip/brew/docker)
6. Usage examples (3-5 common use cases with code)
7. Configuration options (table format)
8. API reference (if library)
9. Contributing guide
10. License
11. FAQ (3-5 common questions)

Style: Clear, scannable, useful. Not marketing copy.
```

### 66. API Documentation
**When to use:** You need to document your API for consumers.
```
Write API documentation for these endpoints:

[LIST ALL ENDPOINTS WITH METHOD, PATH, HANDLER CODE]

For each endpoint, document:
1. Description (what it does, when to use it)
2. Authentication requirements
3. Request (parameters, body schema with types, required/optional)
4. Response (success body with example, status code)
5. Error responses (all possible error codes with examples)
6. Rate limits
7. Code examples in [LANGUAGES: curl, Python, JavaScript]

Format: [Markdown / OpenAPI YAML / Both]
Tone: Concise and practical. Assume the reader is a developer who just wants to integrate quickly.
```

### 67. Inline Comment Generation
**When to use:** You need to add comments to uncommented code.
```
Add inline comments to this code. Follow these rules:

Code:
[PASTE YOUR CODE]

Rules:
1. Comment WHY, not WHAT (don't say "// increment counter" — say "// Track retries for backoff calculation")
2. Comment non-obvious logic, business rules, and workarounds
3. Add JSDoc/docstring for all public functions (params, return, throws)
4. Mark TODO/FIXME/HACK with explanations
5. Don't comment obvious code
6. Keep comments concise (1 line preferred)

Return the full code with comments added. Don't change any logic.
```

### 68. Changelog Writing
**When to use:** You need to write a changelog for a release.
```
Write a changelog entry for this release:

Version: [VERSION]
Previous version: [PREV VERSION]

Changes (git log / PR list):
[PASTE GIT LOG OR LIST OF CHANGES]

Format: Keep a Changelog (keepachangelog.com) format with sections:
- Added (new features)
- Changed (changes in existing functionality)
- Deprecated (soon-to-be removed features)
- Removed (removed features)
- Fixed (bug fixes)
- Security (vulnerability fixes)

Write each entry from the user's perspective (what changed FOR THEM), not the developer's perspective. Technical details in parentheses where helpful.
```

### 69. Architecture Decision Record (ADR)
**When to use:** You need to document a technical decision.
```
Write an Architecture Decision Record (ADR) for this decision:

Decision: [DESCRIBE THE DECISION]
Context: [WHY THIS DECISION NEEDED TO BE MADE]
Options considered: [LIST 2-4 OPTIONS]
Decision made: [WHICH OPTION WAS CHOSEN]

Format:
1. Title (ADR-[NUMBER]: [DECISION TITLE])
2. Status (Proposed / Accepted / Deprecated / Superseded)
3. Context (the problem and constraints)
4. Decision (what we decided)
5. Options Considered (pros/cons table for each)
6. Consequences (positive, negative, risks)
7. Follow-up actions
8. References (links, prior art)

Be honest about trade-offs. Future-you will thank present-you.
```

### 70. Onboarding Guide
**When to use:** You need to help new team members get set up.
```
Write a developer onboarding guide for [PROJECT]:

Tech stack: [LIST TECHNOLOGIES]
Team size: [NUMBER]
Repo structure: [DESCRIBE OR PASTE tree output]

Include:
1. Prerequisites (what to install, accounts needed)
2. Getting started (clone → run in <10 commands)
3. Project structure walkthrough (what's where and why)
4. Development workflow (branches, PRs, CI, deployment)
5. Key concepts (domain terms, architecture patterns used)
6. Common tasks (with exact commands):
   - Running tests
   - Running locally
   - Adding a new [API endpoint / feature / migration]
   - Debugging tips
7. Who to ask (team contacts for different areas)
8. First tasks (good starter issues)
```

### 71. Runbook Creation
**When to use:** You need operational runbooks for incident response.
```
Create a runbook for [SCENARIO, e.g., "database connection exhaustion" / "API latency spike" / "deployment rollback"]:

System: [DESCRIBE YOUR SYSTEM]
Monitoring: [WHAT TOOLS — Datadog, Grafana, CloudWatch, etc.]
Infrastructure: [DESCRIBE — cloud provider, services used]

Include:
1. Alert definition (what triggers this runbook)
2. Severity assessment (how to classify P1/P2/P3)
3. Diagnostic steps (what to check, in order, with exact commands)
4. Resolution steps (for each likely cause)
5. Rollback procedure (if the fix makes things worse)
6. Communication template (what to tell stakeholders)
7. Post-incident (what to document, who to notify)
8. Prevention (how to avoid this happening again)

Write it so someone at 3 AM with no context can follow it.
```

### 72. Configuration Documentation
**When to use:** You need to document environment variables and config options.
```
Document all configuration options for [PROJECT]:

Config sources:
[PASTE YOUR CONFIG FILE / ENV VARS / CODE THAT READS CONFIG]

For each option, document:
| Name | Type | Default | Required | Description | Example |

Group by category (Database, Auth, Logging, Feature Flags, etc.)

Also include:
1. Environment-specific configs (dev vs. staging vs. prod)
2. Sensitive values that should be in secrets manager
3. Common misconfigurations and their symptoms
4. Validation rules (min/max, format, allowed values)
5. Example .env file with all options
```

### 73. Troubleshooting Guide
**When to use:** You need to document common problems and solutions.
```
Write a troubleshooting guide for [PROJECT/SYSTEM]:

Common issues reported:
[LIST ISSUES YOU'VE SEEN]

For each issue, provide:
1. Symptom (what the user sees)
2. Possible causes (ranked by likelihood)
3. Diagnostic steps (how to confirm the cause)
4. Solution (step-by-step fix)
5. Prevention (how to avoid it)

Also include:
- "It's not working" general diagnostic flowchart
- How to collect diagnostic information for bug reports
- Common environment issues (version mismatches, missing deps, permissions)
- Where to find logs and how to read them
```

### 74. Migration Guide
**When to use:** You need to help users upgrade between versions.
```
Write a migration guide from [OLD VERSION] to [NEW VERSION]:

Breaking changes:
[LIST ALL BREAKING CHANGES]

New features:
[LIST NEW FEATURES]

Deprecated features:
[LIST DEPRECATIONS]

For each breaking change:
1. What changed and why
2. Before/after code comparison
3. Step-by-step migration instructions
4. Automated migration script (if possible)

Include:
- Estimated migration time by project size (small/medium/large)
- Order of operations (what to migrate first)
- How to test the migration
- Rollback plan if something goes wrong
- Common migration errors and fixes
```

### 75. Code Example Documentation
**When to use:** You need to add examples to your library documentation.
```
Write code examples for [LIBRARY/API]:

Available functions/methods:
[LIST THE API SURFACE]

For each major feature, provide:
1. Minimal example (smallest working code)
2. Real-world example (actual use case with realistic data)
3. Advanced example (combining features, edge cases, best practices)

Rules:
- Every example must be copy-pasteable and runnable
- Include imports/setup needed
- Show expected output as comments
- Handle errors (don't just show the happy path)
- Use realistic variable names (not foo/bar)
- Language: [LANGUAGE]
```

---

## 7. Refactoring

### 76. Extract Reusable Functions
**When to use:** You have duplicated logic that should be extracted.
```
Identify and extract reusable functions from this code:

Code:
[PASTE YOUR CODE — the more the better, include multiple files if possible]

For each extraction:
1. What pattern is repeated
2. The extracted function with clear name and types
3. How each call site changes
4. Tests for the new function

Prioritize extractions by: most duplicated first, then most complex.
Don't over-abstract — only extract if the pattern appears 3+ times or the logic is complex.
```

### 77. Simplify Complex Conditionals
**When to use:** You have nested if/else chains or complex boolean logic.
```
Simplify these conditionals while preserving behavior:

Code:
[PASTE YOUR CODE WITH COMPLEX CONDITIONALS]

Apply these techniques as appropriate:
1. Early returns / guard clauses
2. Lookup tables / maps instead of switch/if chains
3. Decompose complex boolean expressions into named variables
4. Strategy pattern for behavior that varies by type
5. Null object pattern to eliminate null checks
6. Polymorphism instead of type checking

For each change:
- Show before and after
- Explain the technique used
- Confirm the behavior is identical (or flag differences)
```

### 78. Remove Code Duplication
**When to use:** You've identified duplicated code across your codebase.
```
Refactor to remove duplication in this code:

File 1: [PASTE CODE]
File 2: [PASTE CODE]
[File 3: PASTE CODE, if applicable]

Identify:
1. Exact duplicates (copy-pasted code)
2. Near duplicates (same structure, different values)
3. Structural duplicates (same pattern, different types)

For each:
- Show the shared abstraction
- Show how each file changes to use it
- Decide: shared utility function vs. base class vs. higher-order function vs. template/generic

Don't create abstractions that are harder to understand than the duplication.
```

### 79. Apply Design Patterns
**When to use:** You want to apply a specific design pattern to improve code structure.
```
Refactor this code to use the [PATTERN NAME, e.g., Strategy / Observer / Factory / Builder / Decorator] pattern:

Current code:
[PASTE YOUR CODE]

Problem with current approach:
[DESCRIBE WHY REFACTORING IS NEEDED]

Provide:
1. The refactored code using the pattern
2. Explanation of how the pattern solves the problem
3. Class/module diagram (text description)
4. How to add new [variants/behaviors] with the new pattern vs. the old way
5. Any downsides of applying this pattern here
6. Tests for the refactored code
```

### 80. Optimize Performance-Critical Code
**When to use:** You need to optimize a function for speed or memory.
```
Optimize this code for [SPEED / MEMORY / BOTH]:

Code:
[PASTE YOUR CODE]

Current performance: [MEASUREMENTS IF AVAILABLE]
Target performance: [TARGET]
Input characteristics: [SIZE, PATTERNS, DISTRIBUTION]

Apply these techniques as appropriate:
1. Algorithm complexity improvements (O(n²) → O(n log n), etc.)
2. Data structure changes (array → set, object → map)
3. Lazy evaluation / early termination
4. Caching / memoization
5. Batch operations (reduce I/O calls)
6. Memory pooling / buffer reuse
7. Parallelization (if applicable)

For each optimization:
- Before/after code
- Expected improvement with reasoning
- Any trade-offs (readability, memory vs speed, etc.)
- Benchmark code to verify
```

### 81. Reduce Coupling
**When to use:** Components are too tightly coupled and hard to change independently.
```
Reduce coupling in this code:

Code:
[PASTE YOUR CODE — ideally multiple files showing the dependencies]

Current coupling issues I see:
[DESCRIBE, e.g., "Module A directly imports and calls Module B's internals"]

Apply these techniques:
1. Dependency injection
2. Interface / protocol extraction
3. Event-driven communication
4. Facade pattern for complex subsystems
5. Adapter pattern for external dependencies

For each change:
- What was coupled and how
- The decoupled version
- How to test each component independently now
- What changes are now possible that weren't before
```

### 82. Improve Error Handling
**When to use:** Error handling is inconsistent, incomplete, or overly verbose.
```
Refactor the error handling in this code:

Code:
[PASTE YOUR CODE]

Current problems:
[DESCRIBE, e.g., "errors are swallowed", "generic error messages", "no cleanup on failure"]

Refactor to:
1. Use typed/custom errors instead of generic ones
2. Ensure all error paths are handled (no unhandled promise rejections, etc.)
3. Add proper cleanup (finally blocks, defer statements)
4. Provide user-friendly error messages while logging technical details
5. Implement retry logic where appropriate
6. Add circuit breakers for external dependency failures

Show the complete refactored code with error handling annotations.
```

### 83. Convert Callbacks to Async/Await
**When to use:** You have callback-based code that should use modern async patterns.
```
Convert this callback-based code to async/await:

Code:
[PASTE YOUR CALLBACK-HEAVY CODE]

Requirements:
1. Maintain identical behavior and error handling
2. Handle concurrent operations with Promise.all where possible
3. Add proper error handling for each async operation
4. Convert callback-based libraries to promise-based usage
5. Handle cleanup (close connections, release resources) even on failure
6. Add abort/cancellation support where applicable

Show the complete converted code and flag any behavior differences.
```

### 84. Split Large Files
**When to use:** A file has grown too large and needs to be broken up.
```
This file is too large ([LINE COUNT] lines). Help me split it into smaller, focused modules:

Code:
[PASTE THE LARGE FILE, OR DESCRIBE ITS SECTIONS]

For each proposed module:
1. Name and responsibility
2. What functions/classes move there
3. Exports (public API of each module)
4. Dependencies between modules (import graph)
5. Index file that re-exports for backward compatibility

Rules:
- Each module should have a single, clear responsibility
- Minimize circular dependencies
- Keep related code together (don't split a feature across 5 files)
- Maintain the current public API (callers shouldn't need to change)
```

### 85. Add Type Safety
**When to use:** You want to add or improve types in dynamically typed code.
```
Add type safety to this [JavaScript → TypeScript / Python → typed Python / etc.] code:

Code:
[PASTE YOUR CODE]

Add:
1. Type annotations for all function parameters and return types
2. Interfaces/types for all data structures
3. Generic types where code works with multiple types
4. Union types for values that can be multiple types
5. Literal types for constrained values (status codes, enum-like strings)
6. Type guards for runtime type checking
7. Strict null checks (handle null/undefined explicitly)

Flag any type errors discovered during this process — they're likely real bugs.
```

### 86. Modernize Legacy Code
**When to use:** You need to bring old code up to current standards.
```
Modernize this [LANGUAGE] code to use current best practices:

Code:
[PASTE YOUR LEGACY CODE]

Current [LANGUAGE] version target: [VERSION]

Update:
1. Replace deprecated APIs with modern equivalents
2. Use modern syntax ([LANGUAGE]-specific — destructuring, optional chaining, pattern matching, etc.)
3. Update error handling to modern patterns
4. Replace old dependency patterns with modern ones
5. Add types if the language supports it
6. Update code style to current conventions

For each change, note:
- What was old/deprecated
- The modern replacement
- Minimum language version required
- Any behavior differences to watch for
```

---

## 8. DevOps & Deployment

### 87. Dockerfile Creation
**When to use:** You need to containerize an application.
```
Create a production-ready Dockerfile for:

Application: [DESCRIBE YOUR APP]
Language/Runtime: [LANGUAGE AND VERSION]
Build steps: [HOW TO BUILD — npm run build, go build, etc.]
Runtime command: [HOW TO START — npm start, ./binary, etc.]

Requirements:
- Multi-stage build (separate build and runtime stages)
- Minimal final image (alpine/distroless/slim)
- Non-root user
- Health check
- Proper .dockerignore
- Layer caching optimization (dependencies before code)
- Build args for configurable values
- Labels (maintainer, version, description)
- Security: no secrets in image, no unnecessary tools in final stage

Also provide docker-compose.yml for local development with [DEPENDENCIES, e.g., PostgreSQL, Redis].
```

### 88. CI/CD Pipeline
**When to use:** You need to set up continuous integration and deployment.
```
Create a CI/CD pipeline for [PROJECT]:

Platform: [GitHub Actions / GitLab CI / CircleCI / Jenkins]
Language: [LANGUAGE]
Infrastructure: [WHERE TO DEPLOY — AWS, Vercel, GCP, self-hosted]

Pipeline stages:
1. Lint (code style, formatting)
2. Test (unit + integration)
3. Security scan (dependency audit, SAST)
4. Build (compile, create artifact)
5. Deploy to staging (on PR merge to develop)
6. Deploy to production (on release tag / merge to main)

Include:
- Caching strategy (dependencies, build artifacts)
- Parallelization where possible
- Environment variables / secrets management
- Notification on failure (Slack / email)
- Rollback trigger
- Branch protection rules recommendation
```

### 89. Kubernetes Manifests
**When to use:** You need to deploy an application to Kubernetes.
```
Create Kubernetes manifests for [APPLICATION]:

Container image: [IMAGE:TAG]
Replicas: [NUMBER]
Resources: CPU [REQUEST/LIMIT], Memory [REQUEST/LIMIT]
Environment: [LIST ENV VARS]
Secrets: [LIST SECRETS NEEDED]
Ports: [LIST PORTS]
Dependencies: [DATABASE, CACHE, QUEUE, etc.]

Create:
1. Deployment (with rolling update strategy)
2. Service (ClusterIP + LoadBalancer/Ingress)
3. ConfigMap (non-sensitive config)
4. Secret (sensitive config)
5. HPA (Horizontal Pod Autoscaler) based on [CPU/memory/custom metric]
6. PDB (Pod Disruption Budget)
7. Ingress with TLS
8. Health checks (liveness, readiness, startup probes)
9. Network Policy

Also provide a Kustomize overlay structure for dev/staging/prod.
```

### 90. Monitoring and Alerting Setup
**When to use:** You need to set up monitoring for a system.
```
Design a monitoring and alerting strategy for [SYSTEM]:

Stack: [DESCRIBE — web app, microservices, data pipeline, etc.]
Tools: [Prometheus/Grafana / Datadog / CloudWatch / New Relic]
SLAs: [AVAILABILITY %, LATENCY TARGETS]

Define:
1. Key metrics to collect (RED method: Rate, Errors, Duration)
2. Application-level metrics (business metrics, queue depth, cache hit rate)
3. Infrastructure metrics (CPU, memory, disk, network)
4. Dashboard layout (what graphs, what grouping)
5. Alert rules with:
   - Threshold and evaluation window
   - Severity (P1/P2/P3)
   - Routing (who gets notified and how)
   - Runbook link
6. On-call rotation recommendation

Provide the configuration files for [TOOL] and the Grafana dashboard JSON.
```

### 91. Infrastructure as Code
**When to use:** You need to define infrastructure programmatically.
```
Write [IaC TOOL: Terraform / Pulumi / CDK / CloudFormation] for:

Infrastructure needed:
[DESCRIBE — VPC, compute, database, cache, queue, CDN, DNS, etc.]

Cloud provider: [AWS / GCP / Azure]
Environment: [production / staging / development]

Requirements:
- Modular structure (reusable modules)
- Remote state storage
- Environment separation (workspaces or separate configs)
- Least-privilege IAM
- Encryption at rest and in transit
- Tagging strategy
- Cost estimation comments

Include:
1. All resource definitions
2. Variable files with descriptions and validation
3. Output values (endpoints, connection strings)
4. README with apply instructions
```

### 92. Deployment Rollback Strategy
**When to use:** You need a plan for quickly reverting bad deployments.
```
Design a deployment and rollback strategy for [SYSTEM]:

Current deployment: [DESCRIBE — how you deploy now]
Infrastructure: [DESCRIBE]
Deployment frequency: [HOW OFTEN]
Team size: [NUMBER]

Provide:
1. Deployment process (step-by-step, automated)
2. Pre-deployment checklist
3. Canary / blue-green / rolling deployment strategy
4. Automated rollback triggers (error rate > X%, latency > Yms)
5. Manual rollback procedure (exact commands)
6. Database migration rollback (forward-only migrations vs. reversible)
7. Feature flag strategy for separating deploy from release
8. Post-deployment validation checks
9. Communication template for stakeholders
```

### 93. Secrets Management
**When to use:** You need to manage secrets across environments securely.
```
Design a secrets management strategy for [SYSTEM]:

Current approach: [HOW SECRETS ARE MANAGED NOW]
Environments: [LIST — dev, staging, prod]
Infrastructure: [CLOUD PROVIDER / ON-PREM]
Team size: [NUMBER OF PEOPLE WHO NEED ACCESS]

Provide:
1. Secrets store recommendation ([Vault / AWS Secrets Manager / etc.]) with reasoning
2. Secret rotation strategy (which secrets, how often, automated?)
3. Access control (who can read/write which secrets)
4. Application integration (how apps retrieve secrets at runtime)
5. Local development (how devs access secrets safely)
6. CI/CD integration (how pipelines access secrets)
7. Audit logging (who accessed what, when)
8. Emergency procedures (compromised secret, rotate everything)
9. Migration plan from current approach
```

### 94. Health Check Endpoints
**When to use:** You need health checks for load balancers, Kubernetes, or monitoring.
```
Implement health check endpoints for [APPLICATION]:

Framework: [FRAMEWORK]
Dependencies: [DATABASE, CACHE, QUEUE, EXTERNAL APIs]

Create:
1. /health/live — Is the process running? (for Kubernetes liveness probe)
2. /health/ready — Can it serve traffic? (for Kubernetes readiness probe)
3. /health/startup — Has it finished initializing? (for Kubernetes startup probe)
4. /health/detailed — Full dependency check with individual status (for debugging)

For each dependency check:
- Timeout (don't let a slow dependency kill the health check)
- Caching (don't check every second; cache for 10-30s)
- Degraded vs. unhealthy distinction

Response format:
{
  "status": "healthy|degraded|unhealthy",
  "checks": { "database": { "status": "...", "latencyMs": N }, ... },
  "version": "...",
  "uptime": "..."
}
```

### 95. Log Aggregation Setup
**When to use:** You need structured logging across services.
```
Set up structured logging for [APPLICATION/SYSTEM]:

Language/Framework: [LANGUAGE/FRAMEWORK]
Services: [LIST SERVICES]
Log destination: [stdout / file / ELK / Datadog / CloudWatch]

Provide:
1. Logger configuration (structured JSON format)
2. Standard log fields (timestamp, level, service, traceId, requestId)
3. Log levels usage guide (when to use debug/info/warn/error/fatal)
4. Request logging middleware (method, path, status, duration)
5. Error logging (stack traces, context, user impact)
6. Sensitive data filtering (no passwords, tokens, PII in logs)
7. Correlation IDs for tracing requests across services
8. Log rotation / retention policy
9. Useful log queries for common debugging scenarios
```

### 96. Auto-Scaling Configuration
**When to use:** You need to configure auto-scaling for your infrastructure.
```
Design an auto-scaling strategy for [SYSTEM]:

Current setup: [DESCRIBE INSTANCES, SIZES, COUNTS]
Traffic pattern: [DESCRIBE — steady, spiky, time-of-day, seasonal]
Cost budget: [MONTHLY LIMIT]

Define:
1. Scaling metrics (CPU, memory, request count, queue depth, custom)
2. Scale-up policy (threshold, cooldown, increment)
3. Scale-down policy (threshold, cooldown, step-down)
4. Minimum and maximum instances
5. Scheduled scaling (if predictable patterns)
6. Cost optimization (spot/preemptible instances, reserved capacity)
7. Load testing plan to validate scaling behavior

Platform: [AWS ASG / Kubernetes HPA / GCP MIG / etc.]
Provide the configuration files.
```

### 97. Cost Optimization
**When to use:** Your cloud bill is too high and you need to reduce costs.
```
Analyze and optimize cloud costs for [SYSTEM]:

Current monthly bill: $[AMOUNT]
Infrastructure:
[DESCRIBE — services used, instance types, storage, data transfer]

Top cost items:
[LIST TOP 5 COST LINE ITEMS]

Analyze and recommend:
1. Right-sizing (are instances over-provisioned?)
2. Reserved/spot instance opportunities
3. Storage tier optimization (hot → warm → cold)
4. Data transfer reduction
5. Unused resource cleanup
6. Architecture changes for cost efficiency
7. Monitoring/alerting for cost anomalies

For each recommendation:
- Current cost
- Projected cost after optimization
- Implementation effort
- Risk level
- Priority (savings × ease)
```

---

## 9. Database

### 98. Schema Design from Requirements
**When to use:** You need to design a database schema from business requirements.
```
Design a [DATABASE TYPE] schema for this domain:

Business description:
[DESCRIBE YOUR DOMAIN IN PLAIN ENGLISH]

Key business rules:
[LIST 5-10 BUSINESS RULES]

Common operations (ranked by frequency):
[LIST READS AND WRITES THE SYSTEM PERFORMS MOST]

Provide:
1. Entity-relationship diagram (text description)
2. Complete schema (DDL statements)
3. Indexes for each common query pattern
4. Constraints that enforce business rules at the database level
5. Sample queries for each common operation
6. Considerations for: data growth, archiving, multi-tenancy (if applicable)
```

### 99. Query Optimization
**When to use:** A database query is slow and needs optimization.
```
Optimize this slow query:

Query:
[PASTE THE SLOW QUERY]

Schema:
[PASTE RELEVANT TABLE DEFINITIONS]

Current EXPLAIN output:
[PASTE EXPLAIN / EXPLAIN ANALYZE OUTPUT]

Table sizes:
[LIST APPROXIMATE ROW COUNTS FOR INVOLVED TABLES]

Please:
1. Identify why it's slow (what the query planner is doing wrong)
2. Suggest index additions
3. Rewrite the query for better performance
4. Show the expected EXPLAIN output after optimization
5. Consider if the data model should change (denormalization, materialized view)
6. Provide benchmarking queries to measure improvement
```

### 100. Migration Scripts
**When to use:** You need to change the database schema safely.
```
Write a database migration for:

Current schema:
[PASTE CURRENT SCHEMA]

Desired change:
[DESCRIBE THE CHANGE — add column, rename table, etc.]

Requirements:
- Zero-downtime migration (no table locks on large tables)
- Backward compatible (old code should still work during migration)
- Reversible (include down migration)
- Data backfill (if adding a column that should have values for existing rows)

Migration tool: [Prisma / Flyway / Alembic / knex / raw SQL]

Provide:
1. Up migration
2. Down migration
3. Data backfill script (if needed)
4. Verification query (confirm migration succeeded)
5. Estimated execution time for [TABLE SIZE]
6. Deployment order (migration → code deploy, or code deploy → migration?)
```

### 101. Indexing Strategy
**When to use:** You need to plan indexes for a database.
```
Design an indexing strategy for these tables and queries:

Schema:
[PASTE YOUR SCHEMA]

Queries (ranked by frequency):
[LIST YOUR MOST COMMON QUERIES WITH ESTIMATED QPS]

Current indexes:
[LIST EXISTING INDEXES, or "none beyond primary keys"]

Provide:
1. Recommended indexes with reasoning for each
2. Composite index column ordering explanation
3. Covering indexes for high-frequency queries
4. Partial indexes for filtered queries
5. Indexes to REMOVE (unused, redundant, or more expensive than beneficial)
6. Index maintenance impact on writes
7. Total estimated index size

Database: [PostgreSQL / MySQL / MongoDB / etc.]
```

### 102. Data Modeling
**When to use:** You need to decide how to model a complex domain.
```
Help me model this data:

Domain:
[DESCRIBE YOUR DOMAIN]

Specific modeling challenges:
[DESCRIBE WHAT'S HARD — polymorphism, hierarchies, many-to-many, temporal data, etc.]

Database: [TYPE]

Compare these modeling approaches for my case:
1. [APPROACH 1, e.g., "Single table with type column"]
2. [APPROACH 2, e.g., "Table-per-type inheritance"]
3. [APPROACH 3, e.g., "JSONB column for flexible attributes"]

For each approach:
- Schema design
- Query examples for common operations
- Pros (performance, simplicity, flexibility)
- Cons (complexity, data integrity, query difficulty)
- When it breaks down (at what scale/complexity)

Recommend the best approach for my requirements.
```

### 103. Backup and Restore Procedures
**When to use:** You need to set up database backup and recovery.
```
Design a backup and restore strategy for:

Database: [TYPE AND VERSION]
Data size: [SIZE]
Growth rate: [PER MONTH]
RPO: [MAXIMUM DATA LOSS ACCEPTABLE, e.g., "1 hour"]
RTO: [MAXIMUM DOWNTIME ACCEPTABLE, e.g., "30 minutes"]

Provide:
1. Backup types (full, incremental, WAL/binlog)
2. Backup schedule
3. Storage location and retention policy
4. Backup verification (automated restore tests)
5. Restore procedure (step-by-step commands)
6. Point-in-time recovery procedure
7. Disaster recovery (cross-region backup)
8. Monitoring and alerting for backup failures
9. Cost estimate for storage
10. Automation scripts for backup and verify
```

### 104. Connection Pooling
**When to use:** You need to manage database connections efficiently.
```
Configure connection pooling for:

Application: [LANGUAGE/FRAMEWORK]
Database: [TYPE]
App instances: [NUMBER]
Concurrent requests per instance: [NUMBER]
Database max connections: [NUMBER]

Provide:
1. Pool size calculation (formula and recommended values)
2. Configuration code for [CONNECTION POOL LIBRARY]
3. Connection lifecycle settings (min, max, idle timeout, max lifetime)
4. Health check configuration
5. Monitoring queries (active connections, pool utilization, wait time)
6. Troubleshooting guide for common issues (pool exhaustion, stale connections)
7. Load testing approach to validate pool settings
8. PgBouncer / ProxySQL configuration (if applicable)
```

### 105. Query Debugging
**When to use:** A query returns wrong results or unexpected data.
```
Help me debug this query that returns wrong results:

Query:
[PASTE YOUR QUERY]

Expected result:
[DESCRIBE WHAT YOU EXPECT]

Actual result:
[DESCRIBE WHAT YOU GET — too many rows, missing data, wrong values]

Schema:
[PASTE RELEVANT TABLES]

Sample data:
[PASTE A FEW ROWS FROM EACH RELEVANT TABLE]

Please:
1. Trace through the query logic step by step with my sample data
2. Identify where the logic goes wrong
3. Fix the query
4. Add a comment explaining the tricky part
5. Suggest a way to validate results (checksum query, count comparison)
```

### 106. Schema Evolution Planning
**When to use:** You need to evolve your schema as requirements change.
```
Plan the schema evolution from current to target state:

Current schema:
[PASTE CURRENT SCHEMA]

New requirements:
[DESCRIBE WHAT'S CHANGING AND WHY]

Constraints:
- Zero-downtime deployment: [YES/NO]
- Backward compatibility period: [DURATION]
- Data volume: [ROWS IN AFFECTED TABLES]

Provide:
1. Target schema
2. Migration sequence (ordered steps with dependencies)
3. For each step: migration SQL, rollback SQL, estimated duration
4. Application code changes needed at each step
5. Deploy order (which step goes with which code change)
6. Verification queries at each step
7. Risk assessment and rollback trigger criteria
```

### 107. Seed Data Generation
**When to use:** You need database seed data for development/testing.
```
Generate seed data for development:

Schema:
[PASTE YOUR SCHEMA]

Generate:
- [N] of each entity
- Realistic values (use faker-style data, not "test1", "test2")
- Valid relationships (foreign keys that exist)
- Diverse data (different statuses, edge cases, various dates)
- [SPECIAL SCENARIOS, e.g., "include 1 admin user, 5 users with expired subscriptions, 10 users with orders"]

Format: [SQL INSERT statements / JSON / migration file]

Also include a "known test account" with predictable credentials for testing:
- Email: test@example.com
- Password: testpassword123 (hashed appropriately)
```

### 108. Database Performance Audit
**When to use:** You need a comprehensive performance review of your database.
```
Perform a performance audit of my [DATABASE TYPE] database:

Schema:
[PASTE SCHEMA OR DESCRIBE TABLES/SIZES]

Current performance issues:
[DESCRIBE — slow queries, high CPU, connection issues, etc.]

Available diagnostics:
[PASTE ANY OF: slow query log, pg_stat_statements output, EXPLAIN results, server config]

Audit:
1. Schema analysis (normalization, data types, constraints)
2. Index analysis (missing, unused, redundant, bloated)
3. Query analysis (slow queries, full scans, N+1 patterns)
4. Configuration tuning (memory, connections, work_mem, etc.)
5. Maintenance check (vacuum, analyze, reindex needs)
6. Storage analysis (table bloat, index bloat, TOAST)
7. Connection analysis (pool sizing, idle connections)

For each finding: severity, impact, fix, and effort to implement.
```

---

## 10. AI/ML Integration

### 109. RAG Pipeline Setup
**When to use:** You need to build retrieval-augmented generation.
```
Design and implement a RAG pipeline for [USE CASE, e.g., "answering questions about our documentation"]:

Data source: [DESCRIBE — docs, knowledge base, database, files]
Data volume: [NUMBER OF DOCUMENTS AND TOTAL SIZE]
Query types: [WHAT USERS WILL ASK]

Provide:
1. Document chunking strategy (size, overlap, method)
2. Embedding model recommendation with reasoning
3. Vector database setup ([Pinecone / Weaviate / pgvector / Chroma])
4. Ingestion pipeline code (load → chunk → embed → store)
5. Query pipeline code (embed query → retrieve → rerank → generate)
6. Prompt template for the LLM with retrieved context
7. Evaluation framework (relevance, accuracy, hallucination detection)
8. Performance optimization (caching, batch embedding)

Language: [LANGUAGE]
LLM: [MODEL, e.g., GPT-4 / Claude / local model]
```

### 110. Embedding Generation and Search
**When to use:** You need to create and search text embeddings.
```
Implement semantic search using embeddings for [USE CASE]:

Data: [DESCRIBE YOUR DATA — type, volume, update frequency]

Provide:
1. Embedding model selection ([MODEL]) with reasoning
2. Text preprocessing pipeline
3. Batch embedding generation code
4. Vector storage and indexing ([DATABASE])
5. Search function (query → top-K results with scores)
6. Hybrid search (combine vector search with keyword/filter)
7. Re-ranking step for improved relevance
8. Incremental update strategy (new/modified documents)
9. Performance benchmarks to measure search quality

Language: [LANGUAGE]
Show end-to-end code from ingestion to search.
```

### 111. LLM API Integration
**When to use:** You need to integrate an LLM API into your application.
```
Implement [LLM PROVIDER, e.g., OpenAI / Anthropic / local] integration for [USE CASE]:

Features needed:
[LIST — chat, completion, function calling, vision, etc.]

Provide:
1. Client setup with proper error handling
2. Retry logic with exponential backoff
3. Rate limiting (respect API limits)
4. Token counting and cost tracking
5. Streaming response handling
6. Function/tool calling implementation
7. Conversation memory management
8. Fallback to secondary model if primary fails
9. Request/response logging (without logging sensitive content)
10. Cost estimation before making calls

Language: [LANGUAGE]
Include production-ready error handling, not just happy-path examples.
```

### 112. Prompt Template Engineering
**When to use:** You need to create reusable, reliable prompt templates.
```
Create a prompt template system for [USE CASE, e.g., "customer support bot" / "code review" / "content generation"]:

Use cases:
[LIST 3-5 SPECIFIC TASKS THE SYSTEM NEEDS TO HANDLE]

For each use case, provide:
1. System prompt (role, rules, constraints)
2. User prompt template with variables
3. Few-shot examples (2-3 input/output pairs)
4. Output format specification (JSON schema, markdown, etc.)
5. Guard rails (prevent hallucination, off-topic, harmful content)
6. Evaluation criteria (how to measure if the output is good)

Also provide:
- A prompt template engine (load, render, version templates)
- A/B testing framework for prompt variants
- Prompt versioning strategy
```

### 113. Fine-Tuning Data Preparation
**When to use:** You need to prepare data for fine-tuning an LLM.
```
Prepare a fine-tuning dataset for [MODEL, e.g., GPT-3.5 / Llama / Mistral]:

Task: [DESCRIBE WHAT THE FINE-TUNED MODEL SHOULD DO]
Raw data: [DESCRIBE YOUR SOURCE DATA]

Provide:
1. Data cleaning pipeline (dedup, quality filter, formatting)
2. Conversation/instruction formatting ([MODEL]'s required format)
3. Train/validation/test split strategy
4. Data augmentation techniques (if dataset is small)
5. Quality validation checks (format, length, diversity)
6. Bias detection and mitigation
7. Dataset statistics (token counts, distribution analysis)
8. Fine-tuning configuration (hyperparameters, epochs, learning rate)
9. Evaluation plan (metrics, held-out test set, human evaluation)

Output: Clean dataset file in [FORMAT, e.g., JSONL] ready for fine-tuning.
```

### 114. Vector Database Setup
**When to use:** You need to set up a vector database for similarity search.
```
Set up [VECTOR DB: Pinecone / Weaviate / Qdrant / Milvus / pgvector / Chroma] for [USE CASE]:

Data:
- Vector dimensions: [NUMBER]
- Collection size: [NUMBER OF VECTORS]
- Growth rate: [VECTORS PER DAY/WEEK]
- Metadata fields: [LIST FIELDS FOR FILTERING]

Provide:
1. Database setup and configuration
2. Collection/index creation with optimal settings
3. Ingestion code (batch upsert with metadata)
4. Search function (vector search + metadata filtering)
5. Performance tuning (index type, replicas, shards)
6. Monitoring (vector count, query latency, storage)
7. Backup and restore procedure
8. Migration plan (if switching from another vector DB)
9. Cost estimation at current and projected scale

Language: [LANGUAGE]
```

### 115. AI-Powered Code Review Setup
**When to use:** You want to automate code review with AI.
```
Build an AI-powered code review system:

Repository: [LANGUAGE, SIZE, TEAM SIZE]
CI/CD: [PLATFORM — GitHub Actions, GitLab CI, etc.]

Features:
1. Automatic review on PR creation
2. Check for: bugs, security issues, performance, style consistency
3. Inline comments on specific lines
4. Summary comment with overall assessment
5. Severity labels (critical, suggestion, nitpick)
6. Approval/block based on critical findings
7. Context-aware (understand the codebase, not just the diff)

Provide:
- CI/CD pipeline integration code
- Prompt templates for code review
- Diff parsing and context extraction
- Comment formatting and posting via [PLATFORM] API
- Configuration file for customizing rules
- Rate limiting and cost control
```

### 116. Chatbot Building
**When to use:** You need to build a conversational AI application.
```
Build a chatbot for [USE CASE, e.g., "customer support" / "sales qualification" / "onboarding wizard"]:

Knowledge base: [DESCRIBE — FAQs, docs, product info]
Channels: [WHERE — web widget, Slack, Discord, API]
Tone: [DESCRIBE — formal, friendly, technical, etc.]

Provide:
1. Conversation flow design (state machine or flow diagram)
2. System prompt with persona, rules, and guardrails
3. Intent detection approach (keyword, classifier, or LLM-native)
4. Entity extraction for [LIST ENTITIES — names, dates, products, etc.]
5. Conversation memory (how much context to retain)
6. Handoff to human (when and how to escalate)
7. Fallback responses (when the bot doesn't know)
8. Analytics (track: resolution rate, handoff rate, user satisfaction)
9. Complete implementation code

Language: [LANGUAGE]
LLM: [MODEL]
```

### 117. Content Classification
**When to use:** You need to classify text content using AI.
```
Build a content classification system for [USE CASE]:

Categories:
[LIST CATEGORIES WITH DESCRIPTIONS]

Input: [DESCRIBE — user messages, support tickets, articles, etc.]
Volume: [ITEMS PER DAY]
Latency requirement: [REALTIME / BATCH]

Provide:
1. Classification approach comparison:
   - Zero-shot LLM classification
   - Few-shot with examples
   - Fine-tuned classifier
   - Traditional ML (if appropriate)
2. Recommended approach with reasoning
3. Implementation code
4. Confidence scoring and threshold handling
5. Multi-label support (if items can belong to multiple categories)
6. Human review queue for low-confidence classifications
7. Evaluation metrics (accuracy, precision, recall, F1)
8. Feedback loop (improve from corrections)
9. Cost analysis at volume
```

### 118. Structured Output Parsing
**When to use:** You need LLMs to return structured data reliably.
```
Implement structured output parsing for [USE CASE]:

Required output schema:
[PASTE YOUR JSON SCHEMA OR DESCRIBE THE STRUCTURE]

Input type: [WHAT THE LLM IS PROCESSING]

Provide:
1. Prompt engineering for consistent structured output
2. JSON mode / function calling implementation (if supported by model)
3. Output validation against schema
4. Retry logic for malformed outputs
5. Partial parsing (extract what's valid even from bad output)
6. Type-safe parsing into [LANGUAGE] types
7. Fallback strategies (simpler prompt, different model)
8. Testing with adversarial inputs
9. Monitoring for parse failure rate

Language: [LANGUAGE]
Model: [MODEL]
```

### 119. AI Cost Optimization
**When to use:** Your AI/LLM costs are too high.
```
Optimize AI/LLM costs for [SYSTEM]:

Current usage:
- Model: [MODEL]
- Requests/day: [NUMBER]
- Average tokens per request: [INPUT / OUTPUT]
- Current monthly cost: $[AMOUNT]

Optimization strategies to evaluate:
1. Prompt compression (reduce input tokens without losing quality)
2. Model tiering (cheap model for simple tasks, expensive for complex)
3. Caching (identical or similar requests)
4. Batching (combine multiple small requests)
5. Fine-tuned smaller model for high-volume tasks
6. Response streaming (fail fast on bad responses)
7. Token budgets per request type
8. Async processing (batch during off-peak pricing, if applicable)

For each strategy:
- Implementation code
- Expected cost reduction
- Quality impact (if any)
- Effort to implement

Provide a prioritized optimization roadmap.
```

### 120. AI Evaluation and Testing
**When to use:** You need to measure AI/LLM output quality.
```
Build an evaluation framework for [AI FEATURE]:

What to evaluate:
[DESCRIBE THE AI'S TASK AND WHAT "GOOD" LOOKS LIKE]

Evaluation dimensions:
1. Accuracy (is the output correct?)
2. Relevance (does it answer the actual question?)
3. Completeness (does it cover all aspects?)
4. Hallucination detection (does it make things up?)
5. Consistency (same input → similar output?)
6. Safety (no harmful, biased, or inappropriate content?)
7. Format compliance (does it follow the output spec?)

Provide:
1. Automated evaluation pipeline code
2. LLM-as-judge prompts for subjective quality assessment
3. Golden dataset creation guidelines
4. A/B testing framework for prompt/model changes
5. Regression test suite (ensure changes don't break existing quality)
6. Dashboard for tracking quality metrics over time
7. Alert when quality drops below threshold

Language: [LANGUAGE]
```

---

*That's all 120 prompts. Copy, paste, customize, ship. 🚀*

*Questions or suggestions? Reach out at [YOUR EMAIL].*
