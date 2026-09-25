# Tables

A table is a card on the diagram and a name you can use in SQL.

## Add a table

1. Open the database and stay on **Design view**.
2. Click **Add table**.
3. Type a name when the browser asks.

Rules for the name:

- Letters, digits, and underscores. `students` and `class_list` are fine.
- Do not start with a digit.
- Names are matched without caring about capitals. `Students` and `students` are the same table.
- Do not reuse a name that is already in this database.

The new card starts with one column:

```text
id   INTEGER   primary key, not null, auto increment
```

That `id` is filled in for you when you add a row and leave it empty. You can rename it, but a simple integer primary key is the usual choice in class exercises.

## Rename a table

1. Click **⋮** on the card.
2. Choose **Rename table**.
3. Type the new name.

Renaming also updates foreign keys that pointed at this table, so the dashed line stays connected. See [Foreign keys](foreign-keys.md).

## Delete a table

1. Click **⋮** on the card.
2. Choose **Delete table**.
3. Confirm.

This removes the table and every row in it. SQL does the same thing:

```sql
DROP TABLE classes;
```

`DROP TABLE IF EXISTS classes;` does nothing if the table is already gone, instead of showing an error.

Deleting a table clears the foreign-key link on any column that pointed at it. The dashed line disappears. It does not delete rows in other tables. If `students.class_id` still holds `1` after `classes` is gone, those numbers are just integers.

## Where the table sits

Drag the card. When you drop it, TeensDB writes a `position` into that table's JSON:

```json
"position": { "x": 80, "y": 40 }
```

You never have to edit `position` yourself. It only affects the picture, not the query results.
