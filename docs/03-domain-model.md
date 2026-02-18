# 03 - Domain Model - RDR2 API 

> Character
# Fields
. id (UUID)
. name (string, required)
. slug (string, required, unique, immutable)
. shortDescription (string, required)
. longDescription (text, optional)
. imageUrl (string, optional)
. honorLevel (integer, required)
. currentGangId (UUID, nullable, FK → Gang.id)
. createdAt (timestamp)
. updatedAt (timestamp)
. deletedAt (timestamp, nullable)

# Invariant
. HonorLevel must be between -100 and 100.

# Relationships
. Many Characters → One Gang (optional)
. One Gang → Many Characters

> Weapon
# Fields
. id (UUID)
. name (string, required)
. slug (string, required, unique, immutable)
. description (text, required)
. imageUrl (string, optional)
. type (enum: REVOLVER | RIFLE | SHOTGUN | MELEE | BOW | THROWABLE)
. damage (integer, required)
. range (integer, optional)
. fireRate (integer, optional)
. createdAt (timestamp)
. updatedAt (timestamp)
. deletedAt (timestamp, nullable)

# Invariant
. Damage must be >= 0.

# Relationships
. None in MVP.

> Gang
# Fields
. id (UUID)
. name (string, required)
. slug (string, required, unique, immutable)
. description (text, required)
. leaderId (UUID, nullable, FK → Character.id)
. reputation (integer, required)
. createdAt (timestamp)
. updatedAt (timestamp)
. deletedAt (timestamp, nullable)

# Invariant
. Reputation must be between -100 and 100.

# Relationships
. One Gang → Many Characters
. Optional One Gang → One Leader (Character)

> Place
# Fields
. id (UUID)
. name (string, required)
. slug (string, required, unique, immutable)
. description (text, required)
. imageUrl (string, optional)
. type (enum: TOWN | CITY | CAMP | REGION | HIDEOUT)
. createdAt (timestamp)
. updatedAt (timestamp)
. deletedAt (timestamp, nullable)

# Invariant
. Type must be a valid enum value.

# Relationships
. None in MVP.

> Important Notes
. Slug is immutable.
. Soft delete is handled via deletedAt.
. Unique constraints enforced at database level.
. No historical tracking.
. No many-to-many relationships yet.
. Current state modeling only.