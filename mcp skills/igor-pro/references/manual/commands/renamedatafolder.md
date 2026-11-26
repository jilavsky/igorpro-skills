---
description: "The RenameDataFolder operation changes the name of the source data folder to the new name."
slug: /commands/renamedatafolder
---

<div className="command-signature">

## <strong>RenameDataFolder</strong>  <em>sourceDataFolderSpec</em>, <em>newName</em> {#renamedatafolder}

</div>

The RenameDataFolder operation changes the name of the source data folder to the new name.

*sourceDataFolderSpec* can be just the name of a child data folder in the current data folder, a partial path (relative to the current data folder) and name or an absolute path (starting from root) and name.

*newName* is just the new name for the data folder, without any path.

### *Details* {#details}
RenameDataFolder generates an error if the new name is already in use as a data folder contained within the source data folder.

### *Examples* {#examples}

```igor
RenameDataFolder root:foo,foo2 	// Change name of foo to foo2
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md)