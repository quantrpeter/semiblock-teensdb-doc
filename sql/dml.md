# Insert, update, and delete

These three statements change rows. The table must already exist.

## INSERT

```sql
INSERT INTO students (name, age, class_id) VALUES ('Alice', 13, 1);
```

Several rows in one statement:

```sql
INSERT INTO students (name, age, class_id) VALUES
  ('Alice', 13, 1),
  ('Ben', 14, 2);
```

Rules:

- The column list and each `VALUES` list must have the same length. Otherwise: `Column count does not match value count`.
- A column you omit gets its default, or the next auto-increment number if it is an integer primary key, or `NULL`.
- `NOT NULL` columns cannot end up as `NULL`.
- A repeated primary key or `UNIQUE` value fails: `Duplicate value for unique column "id"`.
- Values are coerced to the column type. `'13'` into an `INTEGER` column becomes `13`.
- A foreign key is **not** checked. `class_id = 99` is stored even if no class has that id.

The notice is `N row(s) inserted`.

Insert every column, in table order, by omitting the column list:

```sql
INSERT INTO classes VALUES (1, 'Year 8 Science', 'Lab 2');
```

Prefer the column list. It still works if someone adds a column later.

## UPDATE

```sql
UPDATE students
SET age = age + 1
WHERE class_id = 1;
```

Set several columns:

```sql
UPDATE classes
SET name = 'Year 8 Physics', room = 'Lab 3'
WHERE id = 1;
```

Without a `WHERE`, every row is updated. The notice is `N row(s) updated`.

`SET` can use the row's current values, as `age = age + 1` does.

## DELETE

```sql
DELETE FROM students WHERE name = 'Eva';
```

Without a `WHERE`, every row in that table is deleted. The table and its columns remain.

```sql
DELETE FROM students;
```

The notice is `N row(s) deleted`.

`DELETE` is not `DROP TABLE`. After `DELETE FROM students` you can still `INSERT INTO students`. After `DROP TABLE students` the name is gone.

## Seeing the change

Click the table chip, or run:

```sql
SELECT * FROM students;
```

The grid on the diagram shows the same rows. See [Typing rows in the grid](../design/input-data.md).
