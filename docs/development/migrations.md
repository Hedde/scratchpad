# Database Migrations

> **Status:** [NOT YET CONFIGURED] — Update this file when the migration tooling is established.

## Migration Tool

[Specify: Ecto, Alembic, Flyway, Prisma, Rails migrations, etc.]

## Conventions

### Table Creation

```
# Example migration for creating a new table
```

**Always:**
- [Convention 1 — e.g., primary key strategy]
- [Convention 2 — e.g., timestamp format]
- [Convention 3 — e.g., null constraints]

### Foreign Keys

```
# Example foreign key migration
```

**on_delete strategies:**
- `cascade` / `delete_all` — for owned children
- `restrict` — for important referential integrity
- `set null` / `nilify_all` — for optional associations

## Safe Migration Patterns

### Adding a NOT NULL Column to Existing Table

Multi-step process to avoid locking issues on large tables:

```
# Step 1: Add nullable column
# Step 2: Backfill data
# Step 3: Add NOT NULL constraint
```

### Removing a Column

Two-deployment process:
1. **First deploy:** Remove all code references to the column
2. **Second deploy:** Drop the column in a migration

### Adding an Index on Large Tables

Use concurrent index creation to avoid table locks:

```
# Example concurrent index creation
```

### Renaming a Column

Multi-step to avoid downtime:
1. Add new column
2. Backfill data from old column
3. Deploy code using new column
4. Drop old column

## Commands

```bash
# Create a migration
[COMMAND]

# Run migrations
[COMMAND]

# Rollback last migration
[COMMAND]

# Reset database (dev only)
[COMMAND]

# Check migration status
[COMMAND]
```

## Testing Migrations

Always test that migrations can roll back cleanly:

```bash
[COMMAND for migrate + rollback + migrate]
```
