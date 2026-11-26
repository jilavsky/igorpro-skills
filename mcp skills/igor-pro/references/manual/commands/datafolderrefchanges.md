---
description: "The DataFolderRefChanges function returns the number of changes to the data folder specified by the data folder reference dfr."
slug: /commands/datafolderrefchanges
---

<div className="command-signature">

## <strong>DataFolderRefChanges</strong> (<em>dfr</em>, <em>changeType</em>) {#datafolderrefchanges}

</div>

The DataFolderRefChanges function returns the number of changes to the data folder specified by the data folder reference *dfr*.

Use DataFolderRefChanges to decide when to update something that depends on the data folder's state by comparing the current number of changes to the change count when your previous update was done. DataFolderRefChanges is not thread-safe so this must be done in the main thread.

Changes to the data folder and its contents are tracked by incrementing a count specific to kind of change. The *changeType* parameter select one of those counts.

The DataFolderRefChanges function was added in Igor Pro 9.00.

### *Parameters* {#parameters}
*dfr* is a data folder reference.

*changeType* is one of the following values:

|  |  |
| --- | --- |
| 0: | Changes to any to the data folder's waves, numeric variables, strings, or child data folders. |
| 1: | Changes to the data folder's waves. |
| 2: | Changes to the data folder's numeric variables. |
| 3: | Changes to the data folder's string variables. |
| 4: | Changes to the data folder's child data folders. |

### *Details* {#details}
The definition of a "change" depends on the object.

For data folders, a "change" is when a child data folder is created, killed, or renamed.

For waves, a "change" is when a wave is created, killed, renamed, locked, or modified.

For string or numeric values, a "change" is when they are created, killed, renamed, or modified.

The change counts are reset to 0 when the experiment is reopened.

### *Examples* {#examples}

```igor
Variable oldWaveChanges = DataFolderRefChanges(GetDataFolderDFR(),1)
Make/O/N=10 aWave = p
Variable newWaveChanges = DataFolderRefChanges(GetDataFolderDFR(),1)
Variable dif = newWaveChanges - oldWaveChanges
Print dif 		// Prints 2: 1 for Make, 1 for aWave=p
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references), [Built-in DFREF Functions](/igorpro/programming/programming.md#built-in-dfref-functions)