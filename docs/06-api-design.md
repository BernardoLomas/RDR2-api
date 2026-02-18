# 06 - API Design Strategy - RDR2 API
> API Versioning
. All routes are prefixed with /api/v1
. Versioning allows future breaking changes without affecting existing consumers

> Resource Naming Convention
. Use plural nouns
. Lowercase routes
. No verbs in URLs
. Slugs use hyphen format (example: arthur-morgan)
. RESTful resource-based design

# Examples:
. /characters
. /weapons
. /gangs
. /places

> Public Read Endpoints (No Authentication Required)
1. List Resources
. GET /api/v1/{entity}
. Supports pagination (page, limit)
. Supports filtering (entity-specific fields)
# Examples:
. GET /api/v1/characters?page=1&limit=10
. GET /api/v1/weapons?type=RIFLE

2. Single Resource by Slug
. GET /api/v1/{entity}/{slug}
. Slug is immutable and public identifier
# Example:
. GET /api/v1/characters/arthur-morgan

> Admin Write Endpoints (JWT + RBAC Required)
1. Create
. POST /api/v1/{entity}

2. Update
. PATCH /api/v1/{entity}/{id}
. Slug cannot be updated

3. Soft Delete
. DELETE /api/v1/{entity}/{id}
. Performs soft delete (deletedAt timestamp)

> Pagination Strategy
. Offset-based pagination
. Default page = 1
. Default limit = 10
. Max limit = 50
. Always return pagination metadata

# Response format for lists:

{
  data: [...],
  meta: {
    page: number,
    limit: number,
    total: number,
    totalPages: number
  }
}


> Filtering Strategy (MVP Scope)
1. Characters
. Filter by name
. Filter by gangSlug
. Filter by honorLevel (exact match for MVP)

2. Weapons
. Filter by type
. Filter by damageMin
. Filter by damageMax

3. Gangs
. Filter by name
. Filter by reputationMin
. Filter by reputationMax

4. Places
. Filter by type
. Filter by name

> Response Standardization
1. Success Response Structure

Single resource:

{
  data: {...}
}


List response:

{
  data: [...],
  meta: {...}
}


2. Error Response Standard
All errors follow this structure:

{
  statusCode: number,
  error: string,
  message: string,
  path: string,
  timestamp: string,
  requestId: string
}


> Soft Delete Behavior
. Soft-deleted records are excluded from all public list endpoints
. GET by slug returns 404 if record is soft-deleted
. Admin endpoints may optionally support includeDeleted=true in future versions

> Data Exposure Policy
1. Public responses must NOT expose:
. deletedAt
. Internal database relation IDs (unless required for admin)

2. Public responses SHOULD expose:
. slug
. name
. description
. Public attributes

> Bulk Operations
. Bulk create/update not supported in MVP
. All write operations are single-resource