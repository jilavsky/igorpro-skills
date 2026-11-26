---
description: "The CountObjects function returns the number of objects of the specified type in the data folder specified by the string expression."
slug: /commands/countobjects
---

<div className="command-signature">

## <strong>CountObjects</strong> (<em>sourceFolderStr</em>, <em>objectType</em>) {#countobjects}

</div>

The CountObjects function returns the number of objects of the specified type in the data folder specified by the string expression.

[CountObjectsDFR](/igorpro/commands/countobjectsdfr.md) is preferred.

### *Parameters* {#parameters}
*sourceFolderStr* can be either ":" or "" to specify the current data folder. You can also use a full or partial data folder path. *objectType* should be one of the following values:

|  |  |
| --- | --- |
| 1: | Waves |
| 2: | Numeric variables |
| 3: | String variables |
| 4: | Data folders |

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [GetIndexedObjName](/igorpro/commands/getindexedobjname.md)