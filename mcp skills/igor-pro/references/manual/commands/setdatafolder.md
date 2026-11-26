---
description: "The SetDataFolder operation sets the current data folder to the specified data folder."
slug: /commands/setdatafolder
---

<div className="command-signature">

## <strong>SetDataFolder</strong>  <em>dataFolderSpec</em> {#setdatafolder}

</div>

The SetDataFolder operation sets the current data folder to the specified data folder.

### *Parameters* {#parameters}
*dataFolderSpec* can be a simple name (MyDataFolder), a path (root:MyDataFolder) or a string expression containing a name or path. It can also be a data folder reference created by the [DFREF](/igorpro/programming/keywords/object-reference-keywords.md#dfref) keyword or returned by [GetDataFolderDFR](/igorpro/commands/getdatafolderdfr.md).

If *dataFolderSpec* is a path it can be a partial path relative to the current data folder (:MyDataFolder) or an absolute path starting from root (root:MyDataFolder).

### *Examples* {#examples}

```igor
SetDataFolder foo                   // Sets CDF to foo in the current data folder
SetDataFolder :bar:foo              // Sets CDF to foo in bar in current data folder
SetDataFolder root:foo              // Sets CDF to foo in the root data folder
DFREF savedDF= GetDataFolderDFR()   // Save current data folder
NewDataFolder/O/S root:MyDataFolder // Set CDF to a new data folder
Variable/G newVariable=1            // Do work in the new data folder
SetDataFolder savedDF               // Restore current data folder
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references)