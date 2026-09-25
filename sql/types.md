# Names, types, and literals

## Names

Table names, column names, and aliases:

- Start with a letter or `_`.
- Then letters, digits, or `_`.
- `students`, `class_id`, and `s` are valid.
- `Students` and `students` are the same name.
- Quote an awkward name with double quotes or square brackets if you need to: `"class name"`, `[order]`. Prefer a simple name instead.

These words cannot be used as a plain name:

`SELECT`, `FROM`, `WHERE`, `INSERT`, `INTO`, `VALUES`, `UPDATE`, `SET`, `DELETE`, `CREATE`, `TABLE`, `DROP`, `IF`, `EXISTS`, `PRIMARY`, `KEY`, `NOT`, `NULL`, `UNIQUE`, `DEFAULT`, `REFERENCES`, `AND`, `OR`, `JOIN`, `INNER`, `LEFT`, `ON`, `AS`, `ORDER`, `BY`, `GROUP`, `HAVING`, `LIMIT`, `OFFSET`, `ASC`, `DESC`, `DISTINCT`, `LIKE`, `IN`, `IS`, `TRUE`, `FALSE`, `AUTOINCREMENT`.

## Types

| Type | Literal | Notes |
|------|---------|-------|
| `INTEGER` | `13`, `-2`, `0` | Whole numbers. |
| `REAL` | `3.5`, `0.1` | Fractional numbers. |
| `TEXT` | `'Alice'` | Single quotes. |
| `BOOLEAN` | `TRUE`, `FALSE` | Also accepted as `1` and `0` when coerced. |

`NULL` means no value. It is not the same as `0`, `FALSE`, or `''`.

Comparisons with `NULL` are unknown, not true. `WHERE age = NULL` does not match rows. Write:

```sql
WHERE age IS NULL
WHERE age IS NOT NULL
```

## Operators

| Operator | Meaning |
|----------|---------|
| `=`, `<>`, `<`, `>`, `<=`, `>=` | Compare. `<>` is "not equal". |
| `+`, `-`, `*`, `/`, `%` | Arithmetic. `%` is remainder. |
| `\|\|` | Join two texts: `'Year ' \|\| '8'` is `Year 8`. |
| `AND`, `OR`, `NOT` | Combine conditions. |
| `LIKE` | Pattern match. `%` is any text, `_` is one character. |
| `IN (...)` | Value is one of a list. |
| `IS NULL`, `IS NOT NULL` | Test for `NULL`. |

```sql
SELECT name FROM students WHERE age >= 14 AND name LIKE 'B%';
SELECT name FROM students WHERE class_id IN (1, 3);
```

`LIKE` is case-sensitive in the way the browser's text match is case-sensitive. `'alice'` does not match `'Alice'`. Use `UPPER` or `LOWER` on both sides if you need to ignore capitals:

```sql
SELECT name FROM students WHERE UPPER(name) LIKE 'AL%';
```

## Functions

| Function | Result |
|----------|--------|
| `UPPER(text)` | Capitals. |
| `LOWER(text)` | Small letters. |
| `LENGTH(text)` | Number of characters. |
| `TRIM(text)` | Text with spaces removed from both ends. |
| `ABS(number)` | Absolute value. |
| `ROUND(number)` | Nearest whole number. `ROUND(number, digits)` keeps that many decimal places. |
| `COALESCE(a, b, ...)` | The first argument that is not `NULL`. |

```sql
SELECT COALESCE(room, 'no room yet') FROM classes;
```

Aggregates (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) are covered in [Select, joins, and aggregates](select.md).
