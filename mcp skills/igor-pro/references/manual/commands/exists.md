---
description: "The exists function returns a number which indicates if objNameStr contains the name of an Igor object, function or operation."
slug: /commands/exists
---

<div className="command-signature">

## <strong>exists</strong> (<em>objNameStr</em>) {#exists}

</div>

The exists function returns a number which indicates if *objNameStr* contains the name of an Igor object, function or operation.

### *Details* {#details}
*objNameStr* can optionally include a full or partial path to the object. If the name does not include a path, exists checks for waves, strings and variables in the current data folder.

*objNameStr* can optionally include a module name or independent module name prefix such as "ProcGlobal#" to check for the existence of functions. This works for macros as well.

The return values are:

|  |  |
| --- | --- |
| 0: | Name not in use, or does not conflict with a wave, numeric variable or string variable in the specified data folder. |
| 1: | Name of a wave in the specified data folder. |
| 2: | Name of a numeric or string variable in the specified data folder. |
| 3: | Function name. |
| 4: | Operation name. |
| 5: | Macro name. |
| 6: | User-defined function name. |

exists is not aware of local variables or parameters in user-defined functions, however it is aware of local variables and parameters in macros.

*objNameStr* is a string or string expression, not a name.

### *Examples* {#examples}

```igor
// Prints 2 if V_flag exists as a global variable in the current data folder:
Print exists("V_Flag")

// Prints 5 if a macro named Graph0 exists.
Print exists("ProcGlobal#Graph0")
```

### *See Also* {#see-also}
[WaveExists](/igorpro/commands/waveexists.md), [DataFolderExists](/igorpro/commands/datafolderexists.md), [WinList](/igorpro/commands/winlist.md)