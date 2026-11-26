---
description: "The ModifyProcedure operation modifies one or more procedure windows, depending on the /A and /W flags and on the procedure keyword."
slug: /commands/modifyprocedure
---

<div className="command-signature">

## <strong>ModifyProcedure</strong>  [/A[=<em>all</em>] /W=<em>procWinTitleListStr</em>] /Z[=<em>z</em>][<em>procedure</em>=<em>functionOrMacroNameStr</em>, <em>hide</em>=<em>h</em>, <em>lock</em>=<em>ro</em>, <em>writeProtect</em>=<em>wp</em>, <em>userCanOverride</em>=<em>ovr</em>] {#modifyprocedure}

</div>

The ModifyProcedure operation modifies one or more procedure windows, depending on the /A and /W flags and on the procedure keyword.

The ModifyProcedure operation was added in Igor 8.03.

Use /W="Procedure" to modify the built-in procedure window.

Use /W=*procWinTitleListStr* to modify a procedure window specified by its title, such as /W="MyProc" for packed procedure files or /W="MyProc.ipf" for standalone procedure files.

Use procedure=*functionOrMacroNameStr* to modify a procedure window containing a particular function.

See **Specifying Which Procedure Windows to Modify** below for other usages.

If the procedure window is associated with a standalone file, as opposed to being packed, the file's read-only setting may be set or cleared, as described below for the lock and writeProtect keywords.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">procedure = *functionOrMacroNameStr*</span> |  |
|  | *functionOrMacroNameStr* is a string containing the name of a function or macro in the procedure window to modify. |
|  | *functionOrMacroNameStr* may be a simple name or may include independent module and/or module name prefixes to designate static functions. For use with independent modules, see ***Using ModifyProcedure With Independent Modules*** below. |
| <span class="table-cell-nowrap">hide = *h*</span> | Hides or shows the targeted procedure windows. Added in Igor 9.00. |
|  |<table class="nested-table"><tbody><tr><td>*h*=-1:</td><td>The procedure window visibility is not changed.</td></tr><tr><td>*h*=0:</td><td>Shows the procedure window.</td></tr><tr><td>*h*=1:</td><td>Hides the procedure window.</td></tr></tbody></table>
| <span class="table-cell-nowrap">lock = *ro*</span> | Sets or clears the read-only state of the targeted procedure windows. |
|  |<table class="nested-table"><tbody><tr><td>*ro*=-2:</td><td>Clears the read-only state, like *ro*=0.</td></tr><tr><td></td><td>In addition, if the procedure window is associated with a standalone file, as opposed to being packed, the file&#39;s read-only setting is set to unlocked, as with [SetFileFolderInfo](/igorpro/commands/setfilefolderinfo.md)/RO=0.</td></tr><tr><td>*ro*=-1:</td><td>The read-only state is not changed.</td></tr><tr><td>*ro*=0:</td><td>Clears the read-only state. This allows the user to change the text if the procedure window is also not write-protected.</td></tr><tr><td>*ro*=1:</td><td>Sets the read-only state. The procedure window shows a lock icon in the lower left corner.</td></tr><tr><td>*ro*=2:</td><td>Sets the read-only state, like *ro*=1.</td></tr><tr><td></td><td>In addition, if the procedure window is associated with a standalone file, as opposed to being packed, the file&#39;s read-only setting is set to locked, as with [SetFileFolderInfo](/igorpro/commands/setfilefolderinfo.md)/RO=1.</td></tr></tbody></table>
| <span class="table-cell-nowrap">writeProtect = *wp*</span> | Set or clears the write-protect state of the targeted procedure windows. |
|  |<table class="nested-table"><tbody><tr><td>*wp*=-2:</td><td>Clears the write-protect state, like *wp*=0.</td></tr><tr><td></td><td>In addition, if the procedure window is associated with a standalone file, as opposed to being packed, the file&#39;s read-only setting is set to unlocked, as with [SetFileFolderInfo](/igorpro/commands/setfilefolderinfo.md)/RO=0.</td></tr><tr><td>*wp*=-1:</td><td>The write-protect state is not changed.</td></tr><tr><td>*wp*=0:</td><td>Clears the write-protect state. The user can change the text if the procedure window is also not locked.</td></tr><tr><td>*wp*=1:</td><td>Sets the write-protect state. The procedure window shows a write-protect icon (a pencil with a red circle-and-line indicator).</td></tr><tr><td>*wp*=2:</td><td>Sets the write-protect state, like *wp*=1.</td></tr><tr><td></td><td>In addition, if the procedure window is associated with a standalone file, as opposed to being packed, the file&#39;s read-only setting is set to locked, as with [SetFileFolderInfo](/igorpro/commands/setfilefolderinfo.md)/RO=1.</td></tr></tbody></table>
| <span class="table-cell-nowrap">userCanOverride = *ovr*</span> | Controls the ability of the user to change the write-protect state of the targeted procedure windows. |
|  |<table class="nested-table"><tbody><tr><td>*ovr*=0:</td><td>Prevents the user from changing the write-protect state by clicking the write-protect icon.</td></tr><tr><td>*ovr*=1:</td><td>Allows the user to change the write-protect state by clicking the write-protect icon.</td></tr></tbody></table>

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A[ = *all* ]</span> | Specifies all procedure windows as the targets of the ModifyProcedure operation. |
|  | Use /A=1 to target all procedure windows in the ProcGlobal module. /A alone is the same as /A=1. |
|  | Use /A=2 to target all procedure windows in independent modules. See **Using ModifyProcedure With Independent Modules** for details. |
| <span class="table-cell-nowrap">/W = *procWinTitleListStr*</span> | Specifies a particular procedure window or a list of procedure windows as the targets of the ModifyProcedure operation. |
|  | If *procWinTitleListStr* is the title of a single procedure window, this specifies that procedure window as the single target. |
|  | If *procWinTitleListStr* contains a semicolon-separated list of procedure window titles, this specifies those procedure windows as targets. |
|  | See ***Specifying Which Procedure Windows to Modify*** below for details. |
| <span class="table-cell-nowrap">/Z[ = *z* ]</span> | Prevents procedure execution from aborting if an error occurs. Use /Z or /Z=1 if you want to handle errors from ModifyProcedure in your procedures rather than having execution abort. |

### *Details* {#details}
When changing the lock or write-protect states for a standalone file (lock=+/-2 or writeProtect=+/-2), there are scenarios where the file's locked state can't be changed. This would occur, for example, if the file is open in another program or if you do not have sufficient privileges to modify the file.

### *Specifying Which Procedure Windows to Modify* {#specifying-which-procedure-windows-to-modify}
The simplest way to modify one procedure window whose title you know is to use /W:


```igor
ModifyProcedure/W="My Procedure.ipf" writeProtect=2 // Use 2 for standalone file
ModifyProcedure/W="Procedure" writeProtect=1        // Modifies the built-in procedure window
```

Use /A=1 to target all procedure windows in the ProcGlobal module:


```igor
ModifyProcedure/A=1 writeProtect=1
```

Don't specify both /A and /W as this is ambiguous and generates an error.

Use procedure=*functionOrMacroNameStr* to modify all procedure windows in the ProcGlobal module containing a procedure with the specified name:


```igor
ModifyProcedure procedure=MyFunction, writeProtect=1
```

If you omit procedure=*functionOrMacroNameStr*, /A, and /W then the built-in procedure window is modified.

Use *functionOrMacroNameStr* only when you are not certain which procedure window contains the function or macro. If a procedure window has syntax errors that prevent Igor from determining where functions and macros start and end, then ModifyProcedure may not be able to locate the correct procedure window in which case it returns an error.

You can use /W and procedure=*functionOrMacroNameStr* to search for a function or macro in one or more procedure windows. This is useful when *functionOrMacroNameStr* is the name of a static function in a procedure window that uses #pragma moduleName.

### *Using ModifyProcedure With Independent Modules* {#using-modifyprocedure-with-independent-modules}
To work with independent modules, you must enable independent module development. This is for advanced programmers only. See [Independent Modules](/igorpro/advanced-topics.md#independent-modules) for details. The material in this section assumes that independent module development is enabled.

/W=*procWinTitleListStr* can be a list of procedure window titles each followed by a space and an independent module name in brackets. Then procedure=*functionOrMacroNameStr* applies to the specified procedure windows and independent modules.

For example, if any procedure file contains these statements:


```igor
#pragma IndependentModule=myIM
#include <Axis Utilities>
```

then the commands


```igor
ModifyProcedure/W="Axis Utilities.ipf [myIM]" procedure="HVAxisList"
Print S_windowList, V_isReadOnly, V_writeProtect
```

report the title, read-only state, and write-protect state of the procedure window that contains the HVAxisList function, which is in the "Axis Utilities.ipf" file and the independent module myIM.

Similarly, procedure=*functionOrMacroNameStr* may also specify an independent module prefix followed by the # character. The preceding ModifyProcedure command can be rewritten as:


```igor
ModifyProcedure/W="Axis Utilities.ipf" procedure="myIM#HVAxisList"
```

or simply:


```igor
ModifyProcedure procedure="myIM#HVAxisList"
```

You can use the same syntax to modify the procedure window containing a static function in a non-independent module procedure file using a module name instead of, or in addition to, the independent module name.

*procWinTitleListStr* can also be just an independent module name in brackets to target all procedure windows that belong to the named independent module containing the specified function:


```igor
ModifyProcedure/W="[myIM]" procedure="HVAxisList", writeProtect=0
```

### *Output Variables* {#output-variables}
The ModifyProcedure operation returns information in the following variables for the last procedure window targeted by the parameters. The information returned reflects the state of affairs after the ModifyProcedure command performs any requested modifications except for V_wasHidden.


|  |  |
| --- | --- |
| V_wasHidden | If the procedure was previously hidden, V_wasHidden is set to 1, otherwise to 0. |
| V_isReadOnly | If the procedure's lock icon is showing, V_isReadOnly is set to 1, otherwise to 0. |
| V_writeProtect | If the pencil with the red line icon is showing, V_writeProtect is set to 1, otherwise to 0. |
| V_userCanOverride |  |
|  | Set to 1 (the default) if the user can change the write-protect state to writable. |
| S_windowList | Set to a semicolon-separated list of procedure window titles that match the parameters, with an appended independent module name in brackets if necessary. |
|  | If S_windowList is empty, then no procedure windows matched the parameters, and no modifications were performed. |

You can obtain the information provided by the output variables without modifying any procedure windows by omitting the lock, writeProtect, and userCanOverride keywords.

### *Examples* {#examples}

```igor
// Completely unlock main Procedure window
ModifyProcedure lock=0, writeProtect=0, userCanOverride=1; Print S_windowList

// Completely unlock the procedure window containing the function named MyFunction
ModifyProcedure procedure="MyFunction", lock=0, writeProtect=0, userCanOverride=1
Print S_windowList	// Print procedure window title

// Lock all procedure windows in the myIM independent module, even those included into it,
// and print the titles of the matching procedure windows
Execute "SetIgorOption IndependentModuleDev=1"
ModifyProcedure/W="[myIM]" lock=1, writeProtect=1, userCanOverride=0; Print S_windowList

// Unlock all procedure windows in the ProcGlobal module
ModifyProcedure/A=1 lock=0, writeProtect=0, userCanOverride=1

// Hide all procedures in ProcGlobal and all independent modules
ModifyProcedure/A=2 hide=1	// Equivalent to HideProcedures
```

### *See Also* {#see-also}
[Independent Modules](/igorpro/advanced-topics.md#independent-modules)

[HideProcedures](/igorpro/commands/hideprocedures.md), [DisplayProcedure](/igorpro/commands/displayprocedure.md), [ProcedureText](/igorpro/commands/proceduretext.md), [ProcedureVersion](/igorpro/commands/procedureversion.md)

[DoWindow](/igorpro/commands/dowindow.md), [WinList](/igorpro/commands/winlist.md)

[MacroList](/igorpro/commands/macrolist.md), [FunctionList](/igorpro/commands/functionlist.md)