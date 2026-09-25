# Select, joins, and aggregates

`SELECT` reads rows. It does not change them.

```sql
SELECT name, age
FROM students
WHERE age >= 14
ORDER BY age DESC;
```

## The pieces

| Clause | Required | Role |
|--------|----------|------|
| `SELECT` | yes | Which columns to return. |
| `FROM` | no | Which table. Omit it to select a value by itself: `SELECT 1 + 1;` |
| `JOIN ... ON` | no | Bring in another table. |
| `WHERE` | no | Keep rows that match. Applied before grouping. |
| `GROUP BY` | no | Collapse rows that share a key. |
| `HAVING` | no | Filter groups, after aggregates. |
| `ORDER BY` | no | Sort the result. |
| `LIMIT` / `OFFSET` | no | Return only a slice. |

`SELECT *` means every column of the row. `SELECT DISTINCT name` removes duplicate names from the result.

## Aliases

```sql
SELECT s.name AS student, c.name AS class_name
FROM students AS s
INNER JOIN classes AS c ON s.class_id = c.id;
```

`AS` is optional: `FROM students s` is the same as `FROM students AS s`. Aliases exist only for that query.

If two tables have a column with the same name, write `table.column` (or `alias.column`). `name` alone is ambiguous once both `students` and `classes` are in the query.

## WHERE

```sql
SELECT * FROM students
WHERE age > 13 AND class_id = 1;
```

Operators and `LIKE` / `IN` / `IS NULL` are listed in [Names, types, and literals](types.md).

## Joins

```sql
-- Only students who have a matching class.
SELECT s.name, c.name
FROM students s
INNER JOIN classes c ON s.class_id = c.id;

-- Every class, even if it has no students. Student columns are NULL then.
SELECT c.name, s.name
FROM classes c
LEFT JOIN students s ON s.class_id = c.id;
```

`JOIN` without a word in front is an inner join. `LEFT JOIN` keeps every row of the left table.

You can join more than two tables. Each `JOIN` has its own `ON`.

There is no `RIGHT JOIN`, `FULL JOIN`, or `CROSS JOIN`. Swap the tables and use `LEFT JOIN` if you need to keep the other side.

A join does not have to follow a foreign key, but it should. The foreign key is the column that was designed for this match. See [Foreign keys](../design/foreign-keys.md).

## GROUP BY and aggregates

| Function | Result |
|----------|--------|
| `COUNT(*)` | How many rows. |
| `COUNT(column)` | How many rows where that column is not `NULL`. |
| `COUNT(DISTINCT column)` | How many different values. |
| `SUM(column)` | Total. Ignores `NULL`. |
| `AVG(column)` | Average. Ignores `NULL`. |
| `MIN(column)` / `MAX(column)` | Smallest / largest. |

```sql
SELECT class_id, COUNT(*) AS how_many, AVG(age) AS avg_age
FROM students
GROUP BY class_id
HAVING COUNT(*) >= 2
ORDER BY how_many DESC;
```

If you `GROUP BY class_id`, the other selected columns should be aggregates or the grouped column. TeensDB evaluates the select list per group.

`WHERE` filters rows first. `HAVING` filters groups. This keeps groups of at least two students. It does not filter students before they are counted — that would be a `WHERE`.

## ORDER BY, LIMIT, OFFSET

```sql
SELECT name, age
FROM students
ORDER BY age DESC, name ASC
LIMIT 3 OFFSET 0;
```

`ASC` is the default. `DESC` reverses it. `NULLS` sort as empty values, so they group together.

`LIMIT 3` returns at most three rows. `OFFSET 3` skips the first three. Use both to page through a result:

```sql
SELECT * FROM students ORDER BY id LIMIT 2 OFFSET 2;
```

## Scalar functions in the select list

`UPPER`, `LOWER`, `LENGTH`, `ABS`, `ROUND`, `COALESCE`, and `TRIM` work in `SELECT`, `WHERE`, and `ORDER BY`. See [Names, types, and literals](types.md).

```sql
SELECT UPPER(name) AS name, LENGTH(name) AS letters
FROM students
ORDER BY letters DESC;
```
