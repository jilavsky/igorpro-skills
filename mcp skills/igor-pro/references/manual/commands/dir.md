---
description: "The Dir operation returns a listing of all the objects in the specified data folder."
slug: /commands/dir
---

<div className="command-signature">

## <strong>Dir</strong>  [<em>dataFolderSpec</em> ] {#dir}

</div>

The Dir operation returns a listing of all the objects in the specified data folder.

### *Parameters* {#parameters}
If you omit *dataFolderSpec*  then the current data folder is used.

If present, *dataFolderSpec*  can be just the name of a child data folder in the current data folder, a partial path (relative to the current data folder) and name or an absolute path (starting from root) and name.

### *Details* {#details}
The format of the printed information is the same as the format used by the string function [DataFolderDir](/igorpro/commands/datafolderdir.md). Igor programmers may find it more convenient to use [CountObjects](/igorpro/commands/countobjects.md) and [GetIndexedObjName](/igorpro/commands/getindexedobjname.md).

Usually it is easier to use the Igor Browser (Data menu). However, dir is useful when you want to copy a name into the command line or when you want to document the current state of the folder in the history.

### *See Also* {#see-also}
[Data Folders](/igorpro/igor-basics/data-folders.md)