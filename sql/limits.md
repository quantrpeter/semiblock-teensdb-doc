# What TeensDB does not run

TeensDB is a teaching engine. If a statement is not in this list, it will not run — even if it is valid SQL on another database.

## Not supported

| You might try | What to do instead |
|----------------|--------------------|
| `ALTER TABLE` | Add the column on the diagram, or `DROP TABLE` and `CREATE TABLE` again. |
| `CREATE INDEX`, `CREATE VIEW`, `CREATE DATABASE` | Not needed. Each TeensDB database is already one document. The sidebar creates databases. |
| `RIGHT JOIN`, `FULL JOIN`, `CROSS JOIN` | Use `INNER JOIN` or `LEFT JOIN`. Swap table order for a right join. |
| Subqueries (`SELECT` inside `WHERE` or `FROM`) | Run the inner question first, note the values, then use `IN (1, 2, 3)` or a join. |
| `UNION` | Run the two selects separately. |
| Transactions (`BEGIN`, `COMMIT`, `ROLLBACK`) | Statements apply immediately, in order. |
| `GRANT`, users, passwords | Sign-in is your SemiBlock account. SQL has no users. |
| Stored procedures, triggers | Not available. |
| Multiple databases in one query | One open database at a time. Names in SQL refer to tables in that database. |

## Enforced vs recorded

| Rule | Checked when you insert or update? |
|------|-------------------------------------|
| `PRIMARY KEY` | Yes. Duplicates fail. |
| `UNIQUE` | Yes. |
| `NOT NULL` | Yes. |
| `AUTOINCREMENT` / integer primary key | Yes. A missing value is filled in. |
| Column type | Coerced. A bad value becomes `NULL`, which then fails if the column is `NOT NULL`. |
| `REFERENCES` (foreign key) | No. The link is stored and drawn. A missing target is allowed. |
| `DEFAULT` | Applied when the column is omitted. |

Foreign keys are still worth drawing. They document the relationship and they tell you which columns to put in `ON`. See [Foreign keys](../design/foreign-keys.md).

## Case and quotes

- Names are case-insensitive.
- Strings use single quotes, not double quotes. Double quotes are for names.
- There is no backslash escape. A quote inside a string is written twice: `'it''s'`.

## Errors are part of the lesson

A red error is the parser or the engine refusing the statement. Read the message, fix that statement, and run again. Common messages are listed in [SQL errors](../troubleshooting/sql-errors.md).
