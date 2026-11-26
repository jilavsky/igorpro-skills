---
description: "The NewDataFolder operation creates a new data folder of the given name."
slug: /commands/newdatafolder
---

<div className="command-signature">

## <strong>NewDataFolder</strong>  [/O/S] <em>dataFolderSpec</em> {#newdatafolder}

</div>

The NewDataFolder operation creates a new data folder of the given name.

### *Parameters* {#parameters}
*dataFolderSpec* can be just a data folder name, a partial path (relative to the current data folder) and name or a full path (starting from root) and name. If just a data folder name is used then the new data folder is created in the current data folder. If a full or partial path is used, all data folders except for the last in the path must already exist.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/O</span> | No error if a data folder of the same name already exists. |
| <span class="table-cell-nowrap">/S</span> | Sets the current data folder to *dataFolderSpec* after creating the data folder. |

### *Examples* {#examples}

```igor
NewDataFolder foo       // Creates foo in current data folder.
NewDataFolder :bar:foo  // Creates foo in bar in current data folder.
NewDataFolder root:foo  // Creates foo in the root data folder.
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md)