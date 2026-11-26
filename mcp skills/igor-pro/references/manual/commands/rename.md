---
description: "The Rename operation renames waves, strings, or numeric variables from oldName to newName."
slug: /commands/rename
---

<div className="command-signature">

## <strong>Rename</strong>  <em>oldName</em>, <em>newName</em> {#rename}

</div>

The Rename operation renames waves, strings, or numeric variables from *oldName* to *newName*.

### *Parameters* {#parameters}
*oldName* may be a simple object name or a data folder path and name. *newName* must be a simple object name.

### *Details* {#details}
You cannot rename an object using a name that already exists. The following will result in an error:


```igor
Make wave0, wave1
// Rename wave0 and overwrite wave1.
Rename wave0, wave1	// This will not work.
```

However, you can achieve the desired effect as follows:


```igor
Make wave0, wave1
Duplicate/O wave0, wave1; KillWaves wave0
```

### *See Also* {#see-also}
[Duplicate](/igorpro/commands/duplicate.md)