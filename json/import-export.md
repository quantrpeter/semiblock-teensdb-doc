# Import, download, and duplicate

The database file is how you hand work in, share an exercise, or keep a backup.

## Download

Three places save the same JSON:

| Where | Control |
|-------|---------|
| Sidebar **⋮** menu | **Download JSON** |
| Workspace header | The download icon next to the database name |
| **JSON** tab | **Download JSON** |

The file name is the database name plus `.json`, for example `School.json`.

**Copy JSON** on the JSON tab puts the text on the clipboard instead of saving a file.

## Import

1. Click the upload arrow next to **My Databases**.
2. Choose a `.json` file that was exported from TeensDB.
3. A new database appears in the sidebar. Double-click it to open it.

Import creates a new database. It does not replace the one you have open. The imported copy gets its own id. The `name` comes from the file.

If the file is not a TeensDB document, import fails. The usual causes:

- The file is not JSON.
- `format` is missing or is not `"teensdb"`.
- The file was saved from a different SemiBlock tool.

## Duplicate

**⋮ → Duplicate** on a sidebar entry copies that database on your account. Use it before a risky `DROP TABLE`, or to give each student a starting copy of an exercise without sending a file.

## Delete

**⋮ → Delete** asks you to confirm, then removes the database from your account. Download it first if you might want it back. The app does not keep a trash folder.

## What is inside the file

The field list is in [The JSON document](format.md). You only need to open the file when you are sharing it or inspecting it. Day-to-day editing happens in Design view and Data view.
