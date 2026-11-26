---
description: "The DataFolderDir function returns a string containing a listing of some or all of the objects contained in the current data folder or in the data folder…"
slug: /commands/datafolderdir
---

<div className="command-signature">

## <strong>DataFolderDir</strong> (<em>mode</em> [, <em>dfr</em> ]) {#datafolderdir}

</div>

The DataFolderDir function returns a string containing a listing of some or all of the objects contained in the current data folder or in the data folder referenced by *dfr*.

### *Parameters* {#parameters}
*mode* is a bitwise flag for each type of object. Use -1 for all types.


| Type | Bit Number | Bit Value |
| --- | --- | --- |
| All |  | -1 |
| Data Folders | 0 | 1 |
| Waves | 1 | 2 |
| Numeric Variables | 2 | 4 |
| String Variables | 3 | 8 |

*dfr* is a data folder reference.

### *Details* {#details}
The returned string has the following format:

FOLDERS:*name*,*name*,...;\<CR\>

WAVES:*name*,*name*,...;\<CR\>

VARIABLES:*name*,*name*,...;\<CR\>

STRINGS:*name*,*name*,...;\<CR\>

Where \<CR\> represents the carriage return character.

:::note
This function is mostly useful during debugging, used in a Print command. For programmatically finding the contents of a data folder, it will be easier to use the functions [CountObjects](/igorpro/commands/countobjects.md) and [GetIndexedObjName](/igorpro/commands/getindexedobjname.md).
:::

### *Examples* {#examples}

```igor
Print DataFolderDir(8+4)	// prints variables and strings
Print DataFolderDir(-1)	// prints all objects
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters)