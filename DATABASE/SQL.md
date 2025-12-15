## PRISM-SQL CHEAT SHEET

**NOTE :** We can assume `OnCallTicket` as `<modelName>` &&  `oncall_tickets` as `<table_name>` 

### Prisma model = SQL Table

```prisma
model OnCallTicket {
  id         String   @id
  uri        String   @unique
  status     String   @default("open")
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt
}
```

```sql
CREATE TABLE oncall_tickets (
  id TEXT PRIMARY KEY,
  uri TEXT UNIQUE,
  status TEXT DEFAULT 'open',
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP NOT NULL
);
```

**NOTE :** Model(in camel case), table (snake_case)

### Prisma Client = SQL Query Builder

```prisma
prisma.onCallTicket.findMany({
  where: { status: "open" }
});
```

```sql
SELECT * FROM oncall_tickets
WHERE status = 'open';
```

- `findMany`, `findOne` (LIMIT 1), `findUnique`

### Prisma `create` = SQL `INSERT`

