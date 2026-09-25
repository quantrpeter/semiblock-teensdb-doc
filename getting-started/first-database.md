# Your first database

A database in TeensDB is one named document. Create it, open it, then add tables.

## Create it

1. Open [TeensDB](https://build.semiblock.ai/teensDB).
2. Click **+** next to **My Databases**, or click **Create a database** on the welcome screen.
3. When the browser asks for a name, type one and confirm. Names like `School`, `Library`, or `Shop` work well for class exercises.
4. The new database appears in the sidebar. Double-click it.

The browser uses its own name prompt. If nothing pops up, see [The name prompt never appears](../troubleshooting/prompts.md).

## What opens

The workspace has three tabs:

| Tab | Starts as |
|-----|-----------|
| **Design view** | An empty diagram with an **Add table** button. |
| **Data view** | An empty SQL editor and a **Run** button. |
| **JSON** | The document for this database, with no tables yet. |

The header shows the database name and a count such as `2 tables`. A download icon next to the name saves this database as a `.json` file.

## The sidebar entry

![School in the sidebar](../img/design-view.png){width=100%}

An open database is marked **open**. Under the name you see a short summary, for example `2 tables · 8 rows`. That count updates after you run SQL or save the data grid.

The **⋮** menu on a database has:

| Action | Effect |
|--------|--------|
| **Open** | Same as a double-click. |
| **Download JSON** | Saves the file to your computer. |
| **Duplicate** | Makes a second copy on your account. |
| **Delete** | Removes the database after you confirm. This cannot be undone from the app. |

## Add the first table

You can add a table in either place. Both write the same JSON.

**From the diagram**

1. Stay on **Design view**.
2. Click **Add table**.
3. Type a table name, such as `classes`.
4. TeensDB creates the table with one column already: `id INTEGER`, primary key, not null, auto increment.

**From SQL**

1. Open **Data view**.
2. Type a `CREATE TABLE` statement. See [Creating and dropping tables](../sql/ddl.md).
3. Click **Run**.

A green notice such as `Table "classes" created` means it worked. Switch back to **Design view** and the new table is on the diagram.

## It is already saved

Creating a database, changing a table, and running SQL all save the JSON to your account. You do not click a separate Save for the database itself. The data grid is the exception: **Edit data** has its own **Save data** button, and **Cancel** throws away grid edits.

Next: [Design view](../design/index.md), or jump straight to [the School example](../data/school-example.md).
