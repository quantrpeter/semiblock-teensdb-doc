# Saving and signing in

TeensDB saves the open database to your SemiBlock account after you create it, change the diagram, or run SQL. You do not need a separate Save button for that.

## "Failed to save" or the sidebar is empty after a refresh

You are probably signed out.

1. Open [https://build.semiblock.ai](https://build.semiblock.ai) and sign in again.
2. Return to [https://build.semiblock.ai/teensDB](https://build.semiblock.ai/teensDB).
3. Double-click the database.

Work that was saved before you were signed out is still on the account. Work that failed to save is not. If a run reported a save error, run it again after signing in.

## The data grid did not save

**Edit data** is the one place with its own buttons. **Cancel** discards what you typed in the grid. **Save data** writes it. Closing the dialog with Cancel is not a save. See [Typing rows in the grid](../design/input-data.md).

## A database is missing from the sidebar

- It was deleted from the **⋮** menu. Delete is permanent unless you downloaded the JSON first.
- You are signed in as a different user. Databases belong to the account that created them.
- You imported a file but have not refreshed. Import adds a new sidebar entry immediately; if you do not see it, reload the page once.

## Download if you want a copy that does not depend on the account

**Download JSON** writes the file to your computer. That file is the whole database. You can import it later on the same account or another one. See [Import, download, and duplicate](../json/import-export.md).

## The page flashes a connection error about localhost

If a developer console mentions `localhost:8089`, ignore it. That address is only used when someone is running the TeensDB source on their own machine. The live site loads the built app from SemiBlock and works without it. You do not need to start anything locally to use [build.semiblock.ai/teensDB](https://build.semiblock.ai/teensDB).
