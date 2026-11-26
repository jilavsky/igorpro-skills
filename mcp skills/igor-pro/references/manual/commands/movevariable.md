---
description: "The MoveVariable operation removes the source numeric variable and places it in the specified location optionally with a new name."
slug: /commands/movevariable
---

<div className="command-signature">

## <strong>MoveVariable</strong>  <em>sourceVar</em>, <em>destDataFolderPath</em> [<em>newname</em> ] {#movevariable}

</div>

The MoveVariable operation removes the source numeric variable and places it in the specified location optionally with a new name.

### *Parameters* {#parameters}
*sourceVar*  can be just the name of a numeric variable in the current data folder, a partial path (relative to the current data folder) and variable name or an absolute path (starting from root) and variable name.

*destDataFolderPath*  can be a partial path (relative to the current data folder) or an absolute path (starting from root).

### *Details* {#details}
An error is issued if a variable or wave of the same name already exists at the destination.

### *Examples* {#examples}

```igor
MoveVariable :foo:v1,:bar:      // Move variable v1 into data folder bar
MoveVariable :foo:v1,:bar:vv1   // Move variable v1 into bar with new name vv1
```

### *See Also* {#see-also}
[MoveString](/igorpro/commands/movestring.md), [MoveWave](/igorpro/commands/movewave.md), [Rename](/igorpro/commands/rename.md), [Data Folders](/igorpro/igor-basics/data-folders.md)