# SQL errors

A failed statement turns the result area into a red error. The database is left as it was after the last statement that succeeded. Fix the SQL and run again.

The message looks like:

```text
Statement 2: No such table: student
```

`Statement 2` means the second statement in the editor (statements are separated by `;`). The rest is the reason.

## Common messages

| Message | Cause | Fix |
|---------|-------|-----|
| `No such table: student` | Typo, or the table was never created. Names ignore capitals, but not spelling. | Click the table chip to insert the real name. |
| `No such column: students.nam` | The column is not on that table. | Check the card on Design view, or `SELECT *`. |
| `Column count does not match value count` | The `INSERT` column list and the `VALUES` list differ in length. | Count both lists. |
| `Column "name" cannot be NULL` | A `NOT NULL` column was omitted or set to `NULL`. | Provide a value. |
| `Duplicate value for unique column "id"` | That primary key or unique value is already used. | Omit `id` and let auto increment assign one, or pick an unused number. |
| `Expected ...` / `Unexpected token` | The statement is not in the TeensDB subset, or a quote or comma is missing. | Compare with [SQL reference](../sql/reference.md). |
| `Ambiguous column: name` | Two tables in the query have `name`. | Write `s.name` and `c.name`. |

## A command that "should work"

TeensDB will not run `ALTER TABLE`, subqueries, `UNION`, or `RIGHT JOIN`. The error is a parse error, not a bug. The substitute for each one is in [What TeensDB does not run](../sql/limits.md).

## Quotes

```sql
-- Wrong. Double quotes are not a string.
SELECT * FROM students WHERE name = "Alice";

-- Right.
SELECT * FROM students WHERE name = 'Alice';
```

A missing closing quote makes the rest of the editor part of the string, so the error often points at the end of the script rather than the line you think.

## Several statements, and only one is wrong

TeensDB stops at the first failure. Earlier statements in that run have already been applied. If statement 1 was `DROP TABLE` and statement 2 failed, the table is already gone. Re-run the `CREATE TABLE` and the inserts, not only the line that failed.

## The result is empty, but there is no error

That is not a failure. The query ran and matched zero rows.

- `INNER JOIN` hides rows that do not match. Try `LEFT JOIN` to see the gaps.
- `WHERE age = NULL` never matches. Use `IS NULL`.
- `LIKE 'alice'` does not match `Alice`. Use `UPPER`, or match the capitals you stored.
