---
description: "The CountObjectsDFR function returns the number of objects of the specified type in the data folder specified by the data folder reference dfr."
slug: /commands/countobjectsdfr
---

<div className="command-signature">

## <strong>CountObjectsDFR</strong> (<em>dfr</em>, <em>objectType</em>) {#countobjectsdfr}

</div>

The CountObjectsDFR function returns the number of objects of the specified type in the data folder specified by the data folder reference *dfr*.

CountObjectsDFR is the same as CountObjects except the first parameter, *dfr*, is a data folder reference instead of a string containing a path.

### *Parameters* {#parameters}
*dfr* is a data folder reference.

*objectType* is one of the following values:

|  |  |
| --- | --- |
| 1: | Waves |
| 2: | Numeric variables |
| 3: | String variables |
| 4: | Data folders |

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references), [Built-in DFREF Functions](/igorpro/programming/programming.md#built-in-dfref-functions), [GetIndexedObjNameDFR](/igorpro/commands/getindexedobjnamedfr.md)