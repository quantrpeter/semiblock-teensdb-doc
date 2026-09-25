# The name prompt never appears

Creating a database, adding a table, and renaming a table ask for a name with the browser's prompt. Deleting asks for a confirmation.

## Allow prompts for the site

Some browsers block `prompt` and `confirm` after the user dismisses them, or when a privacy setting disables JavaScript dialogs.

1. Click the icon to the left of the address bar on `build.semiblock.ai`.
2. Allow pop-ups and JavaScript dialogs for the site.
3. Reload TeensDB and click **+** again.

If a prompt was blocked, TeensDB may show nothing, or it may show an alert that the browser blocked the dialog. Allow the site and retry. The database was not created if you never confirmed a name.

## You dismissed the prompt

**Cancel** on the name prompt aborts that action. The sidebar does not change. Click **+** or **Add table** again.

## The name was rejected

Table names must start with a letter or `_` and contain only letters, digits, and `_`. `8A` is rejected. `year_8` is fine.

Two tables in the same database cannot share a name. Pick another name, or drop the old table first.

## Do not rely on a pasted name dialog in a locked-down browser

School browsers sometimes disable prompts entirely. If you cannot turn them back on:

- Import a starter `.json` instead of creating a database by hand. See [Import, download, and duplicate](../json/import-export.md).
- Create tables with SQL once a database is open. `CREATE TABLE` does not use a prompt. You still need one database first, from **+** or from import.
