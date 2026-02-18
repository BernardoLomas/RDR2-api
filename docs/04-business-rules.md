# 04 - Business Rules - RDR2 API 
> Global Rules
1. All entities must have:
. id (UUID)
. slug (unique, immutable)
. createdAt
. updatedAt
. deletedAt (nullable)

2. Soft-deleted records:
. Must not appear in default public queries.
. Can only be accessed by admin endpoints if explicitly requested.

3. Slugs:
. Must be unique per entity type.
. Must be auto-generated from name.
. Must be immutable after creation.

> Character Rules
1. HonorLevel must be between -100 and 100.
2. A character may or may not belong to a gang.
3. If a gang is soft-deleted:
. Characters remain valid.
. The reference is preserved.
4. A character cannot be permanently deleted (only soft delete allowed).

> Weapon Rules
. Damage must be ≥ 0.
. Type must be a valid enum.
. Weapons cannot share the same slug.
. Soft-deleted weapons are excluded from public listings.

> Gang Rules
. Reputation must be between -100 and 100.
. A gang may have zero or one leader.
. The leader must be a valid Character.
. A soft-deleted gang cannot be assigned to new characters.
. Deleting a gang does NOT delete its characters.

> Place Rules
. Type must be a valid enum value.
. Slug must be unique.
. Soft-deleted places must not appear in public queries.

> Security Rules
1. Public users can only:
. GET lists
. GET single resource by slug

2. Only ADMIN role can:
. Create
. Update
. Soft-delete entities
. JWT authentication is required for all write operations.