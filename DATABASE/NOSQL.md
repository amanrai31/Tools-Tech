## PRISM-SQL CHEAT SHEET

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