# 02 - Scope Definition - RDR2 API
> Entities Included
. Characters
. Gangs
. Places
. Weapons

> Public Endpoints 
# For each entity:
. GET /{entity}: Paginated list | Filtering support (name, slug, etc.).
. GET /{entity}/:slug: Retrieve a single resource by slug.

> Examples:
. GET /characters
. GET /characters/john-marston
. GET /weapons
. GET /gangs
. GET /places
. Reads are fully public.

> Admin Endpoints (JWT Required + RBAC)
. For each entity:
. POST /{entity}
. PATCH /{entity}/:id
. DELETE /{entity}/:id (soft delete)
. Only users with role ADMIN can access these routes.

> Security Model Summary
. Public read access
. JWT authentication required for write operations
. Role-based access control (simple enum: USER | ADMIN)
. Only ADMIN can modify compendium data

> Data Integrity Model
. Relational database
. Foreign key constraints
. Slug uniqueness
. Soft deletes using deletedAt
. Audit fields: createdAt, updatedAt, deletedAt

> Complexity Level
Includes:
. RBAC
. DTO validation
. Centralized exception filter
. Logging
. Pagination & filtering
. Soft delete
. Transactions where needed
# Excludes (for now):
. Rate limiting
. Caching
. Multi-tenant
. Real user registration
. OAuth