---
description: "The DataFolderExists function returns the truth that the specified data folder exists."
slug: /commands/datafolderexists
---

<div className="command-signature">

## <strong>DataFolderExists</strong> (<em>dataFolderNameStr</em>) {#datafolderexists}

</div>

The DataFolderExists function returns the truth that the specified data folder exists.

*dataFolderNameStr* can be a full path or partial path relative to the current data folder.

If *dataFolderNameStr* is empty (""), DataFolderExists returns 1 because, for historical reasons, an empty data folder path is taken to refer to the current data folder.

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md)