# Database Design & Patterns

> **Status:** [NOT YET CONFIGURED] — Update this file when the database technology and conventions are established.

## Database Engine

[Specify: PostgreSQL, MySQL, SQLite, MongoDB, etc.]

## Schema Conventions

### Primary Keys

[Document primary key strategy: auto-increment, UUID, ULID, etc.]

```
# Example migration or schema definition goes here
```

**Rationale:** [Why this approach?]

### Timestamps

[Document timestamp conventions: timezone-aware, precision, column names]

### Naming

[Tables, columns, indexes — naming conventions]

## Enums / Status Fields

[How are enums handled? Native DB types, string columns, integer codes?]

**Rationale:** [Why this approach?]

## Query Patterns

### Preloading / Eager Loading

[How to handle N+1 queries, association loading patterns]

### Pagination

[Pagination strategy: offset-based, cursor-based, keyset]

### Batch Operations

[Bulk insert, update, delete patterns]

## Connection Management

[Connection pooling, timeout settings, environment-specific config]

## Migrations

See [migrations.md](../development/migrations.md) for migration conventions and safe patterns.

## Backup & Recovery

[Backup strategy, retention, recovery procedures]
