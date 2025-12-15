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

```
prisma.onCallTicket.create({
  data: {
    id: "123",
    uri: "/grafana/alert",
  }
});
```

```
INSERT INTO oncall_tickets (id, uri)
VALUES ('123', '/grafana/alert');
```

### Prisma `update` = SQL `UPDATE`

```
prisma.onCallTicket.update({
  where: { id: "123" },
  data: { status: "resolved" }
});
```

```
UPDATE oncall_tickets
SET status = 'resolved'
WHERE id = '123';
```

### Prisma `upsert` = SQL `INSERT … ON CONFLICT`

```
prisma.onCallTicket.upsert({
  where: { uri: normalizedUri },
  update: { status: "open" },
  create: { id, uri: normalizedUri }
});
```

```
INSERT INTO oncall_tickets (id, uri)
VALUES ('id1', '/alert')
ON CONFLICT (uri)
DO UPDATE SET status = 'open';
```

**NOTE :** CREATE UNIQUE INDEX oncall_tickets_uri_key ON oncall_tickets(uri); => Require unique index.


### Prisma `where` = SQL `WHERE`

```
where: {
  status: "open",
  severity: { in: ["P1", "P2"] }
}
```

```
WHERE status = 'open'
AND severity IN ('P1', 'P2');
```

### Prisma orderBy, take, skip

```
orderBy: { createdAt: "desc" },
take: 10,
skip: 20
```

```
ORDER BY createdAt DESC
LIMIT 10 OFFSET 20;
```

### Prisma Relations = Foreign Keys

```
model Ticket {
  id     String @id
  tags   Tag[]
}

model Tag {
  id       String @id
  ticketId String
  ticket   Ticket @relation(fields: [ticketId], references: [id])
}
```

```
CREATE TABLE tags (
  id TEXT PRIMARY KEY,
  ticketId TEXT REFERENCES tickets(id)
);
```

### Prisma `include` = SQL `JOIN`

```
prisma.ticket.findMany({
  include: { tags: true }
});
```

```
SELECT * FROM tickets
LEFT JOIN tags ON tags.ticketId = tickets.id;
```












