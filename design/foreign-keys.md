# Foreign keys

A foreign key is a column that stores the primary key of a row in another table. It is how two tables stay connected.

In the School database, each student has a `class_id`. That number is not the class name. It is the `id` of a row in `classes`.

```text
classes.id  1  =  Year 8 Science
students.class_id  1  →  Alice is in Year 8 Science
```

## Draw the link

1. Open **Design view**.
2. Find the small handle on the right edge of the column that should point somewhere else (`class_id`).
3. Drag from that handle to the handle on the left edge of the column it points at (`classes.id`).
4. TeensDB saves a reference and draws a dashed line.

The line in the [design view](index.md) screenshot runs from `students` to `classes`. `class_id` shows a link icon.

You can also tick **Foreign key (references another table)** in the [column dialog](columns.md) and pick the table and column from the lists.

## Write it in SQL

```sql
CREATE TABLE students (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  age INTEGER,
  class_id INTEGER REFERENCES classes(id)
);
```

`REFERENCES classes(id)` is the same link the diagram draws. After you run this, switch to **Design view** and the dashed line is there.

## What the link does — and what it does not do

The link is stored and drawn. It is how you teach the idea of a foreign key, and it is how `JOIN` queries know which columns belong together.

TeensDB does **not** reject an insert just because the foreign key points at a missing row. This is allowed, and it creates a student with no matching class:

```sql
INSERT INTO students (name, age, class_id) VALUES ('Sam', 13, 99);
```

There is no class `99`. `Sam` is still stored. An `INNER JOIN` will hide that row, because there is nothing to join it to. A `LEFT JOIN` will show `Sam` with an empty class name.

That is a useful classroom moment: the diagram says what the column *means*, and the join shows what the data *actually* matches.

Primary key and `NOT NULL` **are** enforced. You cannot insert a second row with the same `id`, and you cannot leave `name` empty if it is `NOT NULL`.

## Join on the foreign key

```sql
SELECT s.name AS student, c.name AS class_name
FROM students s
INNER JOIN classes c ON s.class_id = c.id;
```

The `ON` clause is the foreign key written out as a condition. The full School query is in [A worked example](../data/school-example.md).
