---
description: "The GetDataFolder function returns a string containing the name of or full path to the current data folder or, if dfr is present, the specified data folder."
slug: /commands/getdatafolder
---

<div className="command-signature">

## <strong>GetDataFolder</strong> (<em>mode</em> [, <em>dfr</em>]) {#getdatafolder}

</div>

The GetDataFolder function returns a string containing the name of or full path to the current data folder or, if *dfr* is present, the specified data folder.

[GetDataFolderDFR](/igorpro/commands/getdatafolderdfr.md) is preferred.

### *Parameters* {#parameters}
If *mode* =0, it returns just the name of the data folder.

If *mode* =1, GetDataFolder returns a string containing the full path to the data folder.

*dfr* , if present, specifies the data folder of interest.

### *Details* {#details}
GetDataFolder can be used to save and restore the current data folder in a procedure. However GetDataFolderDFR is preferred for that purpose.

### *Examples* {#examples}

```igor
String savedDataFolder = GetDataFolder(1)   // Save
SetDataFolder root:
Variable/G gGlobalRootVar
SetDataFolder savedDataFolder               // and restore
```

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md), [Data Folder References](/igorpro/programming/programming.md#data-folder-references)

[SetDataFolder](/igorpro/commands/setdatafolder.md), [GetDataFolderDFR](/igorpro/commands/getdatafolderdfr.md)