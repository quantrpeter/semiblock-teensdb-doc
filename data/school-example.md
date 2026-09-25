# A worked example: School

This is the database used in the screenshots. It has two tables and one foreign key: a student belongs to a class.

![School diagram](../img/design-view.png){width=100%}

## Create the tables

Open **Data view** and run:

```sql
DROP TABLE IF EXISTS students;
DROP TABLE IF EXISTS classes;

CREATE TABLE classes (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  room TEXT
);

CREATE TABLE students (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  name TEXT NOT NULL,
  age INTEGER,
  class_id INTEGER REFERENCES classes(id)
);
```

`students` is dropped first because the example is safe to re-run. `REFERENCES` is what draws the dashed line.

## Insert rows

```sql
INSERT INTO classes (name, room) VALUES
  ('Year 8 Science', 'Lab 2'),
  ('Year 9 Maths', 'Room 14'),
  ('Year 10 Art', 'Studio A');

INSERT INTO students (name, age, class_id) VALUES
  ('Alice', 13, 1),
  ('Ben', 14, 2),
  ('Chloe', 13, 1),
  ('David', 15, 3),
  ('Eva', 14, 2);
```

`id` is omitted. Auto increment assigns 1, 2, 3… in the order of the `VALUES` list. Alice's `class_id` is `1`, which is Year 8 Science.

You can type the same rows in the grid. See [Typing rows in the grid](../design/input-data.md).

## Ask a question

"Who is in which class, and which room?"

```sql
SELECT s.name AS student, s.age, c.name AS class_name, c.room
FROM students s
INNER JOIN classes c ON s.class_id = c.id
ORDER BY s.name;
```

![Join result](../img/data-view.png){width=100%}

| student | age | class_name | room |
|---------|-----|------------|------|
| Alice | 13 | Year 8 Science | Lab 2 |
| Ben | 14 | Year 9 Maths | Room 14 |
| Chloe | 13 | Year 8 Science | Lab 2 |
| David | 15 | Year 10 Art | Studio A |
| Eva | 14 | Year 9 Maths | Room 14 |

`s` and `c` are aliases — short names for the tables. `AS student` renames a column in the result only. It does not rename the column in the table.

## A few more questions

How many students are in each class?

```sql
SELECT c.name AS class_name, COUNT(*) AS students
FROM classes c
LEFT JOIN students s ON s.class_id = c.id
GROUP BY c.name
ORDER BY c.name;
```

`LEFT JOIN` keeps a class even if nobody is in it. `COUNT(*)` counts the joined rows.

Who is older than 13, youngest first?

```sql
SELECT name, age
FROM students
WHERE age > 13
ORDER BY age;
```

Move everyone in class 1 up by one year:

```sql
UPDATE students
SET age = age + 1
WHERE class_id = 1;
```

Remove one student:

```sql
DELETE FROM students WHERE name = 'Eva';
```

`DELETE` without a `WHERE` deletes every row in the table. The table itself remains. `DROP TABLE` removes the table.

## Look at the file

Open the **JSON** tab. The same two tables, the foreign key, and the eight rows are one document. That format is described in [The JSON document](../json/format.md).
