# Creating and dropping tables

`CREATE TABLE` defines a table. `DROP TABLE` removes one. There is no `ALTER TABLE` — see [What TeensDB does not run](limits.md).

## CREATE TABLE

```sql
CREATE TABLE classes (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  room TEXT
);
```

Each column is a name, a type, then optional constraints.

| Constraint | Effect |
|------------|--------|
| `PRIMARY KEY` | Identifies the row. Implies not null. Duplicate values are rejected. |
| `NOT NULL` | The value cannot be `NULL`. |
| `UNIQUE` | No two rows may share this value. `NULL` may repeat. |
| `AUTOINCREMENT` | On insert, if you omit this integer column, TeensDB stores one more than the current maximum. |
| `DEFAULT value` | Used when an `INSERT` omits the column. |
| `REFERENCES table(column)` | Records a foreign key. Drawn on the diagram. Not checked on insert. See [Foreign keys](../design/foreign-keys.md). |

Types are `INTEGER`, `REAL`, `TEXT`, and `BOOLEAN`.

A second `CREATE TABLE` with the same name fails. Drop the old table first, or pick another name.

An integer primary key auto-increments even if you do not write `AUTOINCREMENT`. Writing it makes the intention obvious, and it matches the column TeensDB creates from **Add table**.

## DROP TABLE

```sql
DROP TABLE students;
DROP TABLE IF EXISTS students;
```

Without `IF EXISTS`, dropping a table that is not there is an error: `No such table: students`.

`DROP TABLE` deletes the rows as well. It does not delete other tables.

## Recreating a table

Because there is no `ALTER TABLE`, this is the SQL way to change columns:

```sql
DROP TABLE IF EXISTS classes;
CREATE TABLE classes (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  room TEXT,
  teacher TEXT
);
```

The rows are gone after the drop. To keep them, `SELECT` them out (or copy the JSON) before you drop.

Adding a column on the diagram does not delete rows. Prefer the diagram when you are only adding a field. See [Columns](../design/columns.md).
