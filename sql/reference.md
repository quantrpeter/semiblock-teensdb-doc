# SQL reference

TeensDB runs a teaching subset of SQL. It is enough for tables, rows, filters, joins, and aggregates. It is not a full database server.

Statements you can run:

| Statement | Page |
|-----------|------|
| Names, types, strings, numbers, `NULL` | [Names, types, and literals](types.md) |
| `CREATE TABLE`, `DROP TABLE` | [Creating and dropping tables](ddl.md) |
| `INSERT`, `UPDATE`, `DELETE` | [Insert, update, and delete](dml.md) |
| `SELECT`, `JOIN`, `GROUP BY`, functions | [Select, joins, and aggregates](select.md) |
| Commands that are intentionally missing | [What TeensDB does not run](limits.md) |

## How statements are run

- Separate statements with `;`.
- They run in order. Later statements see the changes made by earlier ones.
- SQL words and names are case-insensitive.
- A statement that the parser does not recognise fails with `Unexpected token` or `Expected ...`. The error names the statement number when you ran more than one.
- Strings use single quotes: `'Year 8 Science'`. To put a quote inside a string, double it: `'it''s'`.
- Comments are `--` to the end of the line, and `/* ... */` blocks.

## One-line examples

```sql
CREATE TABLE classes (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL
);

INSERT INTO classes (name) VALUES ('Year 8 Science');

SELECT * FROM classes WHERE name LIKE 'Year 8%';

UPDATE classes SET name = 'Year 8 Physics' WHERE id = 1;

DELETE FROM classes WHERE id = 1;

DROP TABLE classes;
```

Paste-ready tables and rows are in [A worked example: School](../data/school-example.md).
