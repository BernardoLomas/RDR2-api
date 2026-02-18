# 05 - Architecture Decisions - RDR2 API 
> Architectural Style
. Modular Monolith (NestJS modules)
. Clear domain boundaries (characters, weapons, gangs, places)
. Shared cross-cutting modules (auth, logging, config)
. Why: fastest to iterate, clean separation, realistic production structure.

> Layering and Responsibilities
1. Structure
. Controller: HTTP contract only (routes, params, status codes)
. DTOs: request/response shapes + validation decorators
. Service: business rules orchestration (use-cases)
. Repository: database queries only
. Entity (ORM model): persistence representation

2. Global cross-cutting:
. Guards: auth + RBAC
. Pipes: validation/transform at boundaries
. Filters: centralized error handling
. Interceptors: logging and response shaping

> Database Choice
. Relational DB required (ACID + constraints + relations)
. PostgreSQL: Strong constraints, great tooling, good for real-world APIs.

> ORM / Data Access
. PrismaORM

> Identifier Strategy
. id: UUID (primary key)
. slug: unique string for public reads (immutable)
. Admin writes use id routes (PATCH/DELETE by id) to avoid slug mutation issues.

> API Conventions
1. Base route: /api/v1

2. Public reads:
. GET /characters
. GET /characters/:slug

3. Admin writes:
. POST /characters
. PATCH /characters/:id
. DELETE /characters/:id (soft delete)

4. Pagination
. page, limit (with max limit)
. Filtering: query params like name, type, gangSlug (where applicable)

> Security Model
. JWT Auth
. RBAC: simple roles enum (ADMIN, later USER)
. Public reads do not require auth
. Admin endpoints require auth + role guard

> Error Handling Standard
1. Global exception filter
2. Consistent error response shape:
. statusCode
. error
. message
. path
. timestamp
. requestId

> Logging Standard
1. Structured logs (JSON)
2. Include:
. requestId
. method, path
. userId (if authenticated)
. statusCode
. latency

10) Project Folder Structure
src/
    main.ts
    app.module.ts
    config/
    common/ (filters, interceptors, decorators, utils)
    auth/
    modules/
        characters/
        weapons/
        gangs/
        places/