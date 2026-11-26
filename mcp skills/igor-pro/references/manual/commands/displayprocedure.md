---
description: "The DisplayProcedure operation displays the named function, macro or line by bringing the procedure window it is defined in to the front with the function…"
slug: /commands/displayprocedure
---

<div className="command-signature">

## <strong>DisplayProcedure</strong>  [/B=<em>winTitleOrName</em>  /L=<em>lineNum</em>  /W=<em>procWinTitle</em> ] [<em>functionOrMacroNameStr</em> ] {#displayprocedure}

</div>

The DisplayProcedure operation displays the named function, macro or line by bringing the procedure window it is defined in to the front with the function, macro or line highlighted.

### *Parameters* {#parameters}
*functionOrMacroNameStr* is a string expression containing the name of the function or macro to display. If you omit *functionOrMacroNameStr* then you must use /W or /L.

*functionOrMacroNameStr* may be a simple name or may include independent module and/or module name prefixes to display static functions.

If you use /L to display a particular line then you must omit *functionOrMacroNameStr* .

To display a procedure window without changing its scrolling or selection, use /W and omit *functionOrMacroNameStr*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B = *winTitleOrName*</span> | Brings the procedure window up just behind the window with this name or title. |
| <span class="table-cell-nowrap">/L = *lineNum*</span> | If /W is specified, *lineNum* is a zero-based line number in the specified window. |
|  | If /W is not specified, *lineNum* is a "global" line number. Each procedure window line has a unique global line number as if all open procedure files were concatenated into one big file. The order of concatenation of files can change when procedures are recompiled. |
|  | If you use /L then you must omit *functionOrMacroNameStr* . |
| <span class="table-cell-nowrap">/W = *procWinTitle*</span> | Searches in the procedure window with this title. |
|  | procWinTitle is a name, not a string, so you construct /W like this: |
|  | <code class="igor">/W=$"New Polar Graph.ipf"</code> |
|  | If you omit /W, DisplayProcedure searches all open (nonindependent module) procedure windows. |

### *Details* {#details}
If a procedure window has syntax errors that prevent Igor from determining where functions and macros start and end, then DisplayProcedure may not be able to locate the procedure.

*winTitleOrName* is not a string; it is a name. To position the found procedure window behind a window whose title has a space in the name, use the $ operator as in the second example, below.

If *winTitleOrName* does not match any window, then the found procedure window is placed  behind the top target window.

*lineNum* is a zero-based line number: 0 is the first line of the window. Because each line of a procedure window is a paragraph, line numbers and paragraph numbers are the same. You can use the Procedure->Info menu item to show a selection's starting and ending paragraph/line number.

*procWinTitle* is also a name. Use /W=$"New Polar Graph.ipf" to search for the function or macro in only that procedure file.

Don't specify both *functionOrMacroNameStr* and /L=*lineNum* as this is ambiguous and not allowed.

### *Advanced Details* {#advanced-details}
If SetIgorOption IndependentModuleDev=1, *procWinTitle* can also be a title followed by a space and, in brackets, an independent module name. In such cases searches for the function or macro are in the specified procedure window and independent module. (See [Independent Modules](/igorpro/advanced-topics.md#independent-modules) for independent module details.)

For example, if any procedure file contains these statements:

```igor
#pragma IndependentModule=myIM
#include <Axis Utilities>
```

The command

```igor
DisplayProcedure/W=$"Axis Utilities.ipf [myIM]" "HVAxisList"
```

opens the procedure window that contains the HVAxisList function, which is in the Axis Utilities.ipf file and the independent module myIM. The command uses the $"" syntax because space and bracket characters interfere with command parsing.

Similarly, if SetIgorOption IndependentModuleDev=1 then *functionOrMacroNameStr* may also contain an independent module prefix followed by the # character. The preceding command can be rewritten as:

```igor
DisplayProcedure/W=$"Axis Utilities.ipf" "myIM#HVAxisList"
```

or more simply

```igor
DisplayProcedure "myIM#HVAxisList"
```

You can use the same syntax to display a static function in a non-independent module procedure file using a module name instead of (or in addition to) the independent module name.

*procWinTitle* can also be just an independent module name in brackets to display all procedure windows that belong to the named independent module and define the specified function:

```igor
DisplayProcedure/W=$"[myIM]" "HVAxisList"
```

### *Examples* {#examples}

```igor
DisplayProcedure "Graph0"
DisplayProcedure/B=Panel0 "MyOwnUserFunction"
DisplayProcedure/W=Procedure		// Shows the main Procedure window
DisplayProcedure/W=Procedure/L=5		// Shows line 5 (the sixth line)
DisplayProcedure/W=$"Wave Lists.ipf"
DisplayProcedure "moduleName#myStaticFunctionName"
SetIgorOption IndependentModuleDev=1
DisplayProcedure "WMGP#GizmoBoxAxes#DrawAxis"
```

### *See Also* {#see-also}
[Independent Modules](/igorpro/advanced-topics.md#independent-modules)

[HideProcedures](/igorpro/commands/hideprocedures.md), [DoWindow](/igorpro/commands/dowindow.md)

[ProcedureText](/igorpro/commands/proceduretext.md), [ProcedureVersion](/igorpro/commands/procedureversion.md), [ModifyProcedure](/igorpro/commands/modifyprocedure.md)

[MacroList](/igorpro/commands/macrolist.md), [FunctionList](/igorpro/commands/functionlist.md)