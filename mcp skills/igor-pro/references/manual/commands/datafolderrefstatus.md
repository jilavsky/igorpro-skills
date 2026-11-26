---
description: "The DataFolderRefStatus function returns the status of a data folder reference."
slug: /commands/datafolderrefstatus
---

<div className="command-signature">

## <strong>DataFolderRefStatus</strong> (<em>dfr</em>) {#datafolderrefstatus}

</div>

The DataFolderRefStatus function returns the status of a data folder reference.

### *Details* {#details}
DataFolderRefStatus returns zero if the data folder reference is invalid or non-zero if it is valid.

DataFolderRefStatus returns a bitwise result with bit 0 indicating if the reference is valid and bit 1 indicating if the reference data folder is free. Therefore the returned values are:

|  |  |
| --- | --- |
| 0: | The data folder reference is invalid. |
| 1: | The data folder reference refers to a regular global data folder. |
| 3: | The data folder reference refers to a free data folder. |

A data folder reference is invalid if it was never assigned a value or if it is assigned an invalid value. For example:


```igor
DFREF dfr                               // dfr is invalid
DFREF dfr = root:                       // dfr is valid
DFREF dfr = root:NonExistentDataFolder  // dfr is invalid
DFREF dfr = root:ExistingDataFolder     // dfr is valid
KillDataFolder dfr                      // dfr is invalid
```

You should use DataFolderRefStatus to test any DFREF variables that might not be valid, such as after assigning a reference when you are not sure that the referenced data folder exists. For historical reasons, if you use an invalid DFREF it will often act like root.

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references), [Built-in DFREF Functions](/igorpro/programming/programming.md#built-in-dfref-functions)