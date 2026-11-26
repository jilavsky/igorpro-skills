---
description: "The MoveString operation removes the source string variable and places it in the specified location optionally with a new name."
slug: /commands/movestring
---

<div className="command-signature">

## <strong>MoveString</strong>  <em>sourceString</em>, <em>destDataFolderPath</em> [<em>newname</em> ] {#movestring}

</div>

The MoveString operation removes the source string variable and places it in the specified location optionally with a new name.

### *Parameters* {#parameters}
*sourceString* can be just the name of a string variable in the current data folder, a partial path (relative to the current data folder) and variable name or an absolute path (starting from root) and variable name.

*destDataFolderPath* can be a partial path (relative to the current data folder) or an absolute path (starting from root).

### *Details* {#details}
An error is issued if a variable or wave of the same name already exists at the destination.

### *Examples* {#examples}

```igor
MoveString :foo:s1,:bar:        // Move string s1 into data folder bar
MoveString :foo:s1,:bar:ss1     // Move string s1 into bar with new name ss1
```

### *See Also* {#see-also}
[MoveVariable](/igorpro/commands/movevariable.md), [MoveWave](/igorpro/commands/movewave.md), [Rename](/igorpro/commands/rename.md), [Data Folders](/igorpro/igor-basics/data-folders.md)