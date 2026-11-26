---
description: "The GetDataFolderDFR function returns the data folder reference for the current data folder."
slug: /commands/getdatafolderdfr
---

<div className="command-signature">

## <strong>GetDataFolderDFR</strong> ( ) {#getdatafolderdfr}

</div>

The GetDataFolderDFR function returns the data folder reference for the current data folder.

### *Details* {#details}
GetDataFolderDFR can be used to save and restore the current data folder in a procedure. It is like GetDataFolder but returns a data folder reference rather than a string.

### *Examples* {#examples}

```igor
DFREF saveDFR = GetDataFolderDFR()  // Save
SetDataFolder root:
Variable/G gGlobalRootVar
SetDataFolder saveDFR               // and restore
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references), [Built-in DFREF Functions](/igorpro/programming/programming.md#built-in-dfref-functions), [SetDataFolder](/igorpro/commands/setdatafolder.md)