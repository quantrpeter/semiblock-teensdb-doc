# SemiBlock TeensDB

![TeensDB design view](img/design-view.png){width=100%}

**SemiBlock TeensDB** is an educational relational database that runs entirely in the browser. It is built to teach teenagers SQL and database design: you draw tables, type SQL, and see the rows change immediately.

Each database is one JSON document. That file holds the table structure, the foreign keys, the diagram layout, and every row. SQL runs on your computer. Nothing is sent to a database server to be executed. The JSON itself is saved to your SemiBlock account so you can open it again later.

## What you can do

- **Design tables visually** — an entity-relationship diagram you can pan, zoom, and rearrange.
- **Write SQL** — a teaching subset of SQL: create and drop tables, insert, update, delete, and select with joins, grouping, and aggregates.
- **Edit rows in a grid** — type data without writing `INSERT`.
- **Keep the whole database as JSON** — copy it, download it, or import a file a classmate sent you.

## Core concepts

| Concept | What it means in TeensDB |
|---------|--------------------------|
| **Database** | One named JSON file in **My Databases**. Example: `School`. |
| **Table** | A named list of rows that all share the same columns. Example: `students`. |
| **Column** | One field in a table, with a type: `INTEGER`, `REAL`, `TEXT`, or `BOOLEAN`. |
| **Row** | One record. Alice, age 13, in class 1, is one row of `students`. |
| **Primary key** | The column that identifies a row. Shown with a key icon. Usually `id`. |
| **Foreign key** | A column that points at a row in another table. Drawn as a dashed line on the diagram. |
| **SQL** | The language you type in **Data view** to change or query the database. |

## How a session works

1. Sign in at [build.semiblock.ai](https://build.semiblock.ai) and open [TeensDB](https://build.semiblock.ai/teensDB).
2. Create a database. It appears in the left sidebar.
3. Double-click it to open the workspace.
4. Design tables on the diagram, or create them with `CREATE TABLE`.
5. Run SQL. Results appear under the editor. Changes are saved with the database.

## Three views

| View | Use it to |
|------|-----------|
| **Design view** | See tables, add columns, draw foreign keys, and type rows in a grid. |
| **Data view** | Write and run SQL. Copy the result table. |
| **JSON** | Read, copy, or download the whole database as one document. |

## Next steps

- [Open TeensDB and create your first database](getting-started/first-database.md)
- [Design tables and foreign keys](design/index.md)
- [Run your first query](data/sql-editor.md)
- [Look up a SQL command](sql/reference.md)

The full list of pages is in the [Table of Contents](toc.md).
