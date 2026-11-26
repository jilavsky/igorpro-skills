---
description: "The Edit operation creates a table window or subwindow containing the specified columns."
slug: /commands/edit
---

<div className="command-signature">

## <strong>Edit</strong>  [ /FG=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em>) /HIDE=<em>h</em> /HOST=<em>hcSpec</em> /I /K=<em>k</em> /M/N=<em>name</em>/W=(<em>left</em>, <em>top</em>, <em>right</em>, <em>bottom</em>)] [<em>columnSpec</em> [,<em>columnSpec</em>]...] [<em>as</em> <em>titleStr</em>] {#edit}

</div>

The Edit operation creates a table window or subwindow containing the specified columns.

### *Parameters* {#parameters}
*columnSpec*  is usually just the name of a wave. If no *columnSpecs* are given, an empty table is created.

Column specifications are wave names optionally followed by one of the suffixes:

|  |  |
| --- | --- |
| .i | Index values. |
| .l | Dimension labels. |
| .d | Data values. |
| .id | Index and data values. |
| .ld | Dimension labels and data values. |

If the wave is complex, the wave names may be followed by .real or .imag suffixes. However, as of Igor Pro 3.0, both the real and imaginary columns are added to the table together — you cannot add one without the other — so using these suffixes is discouraged.

*titleStr* is a string expression containing the table's title. If not specified, Igor will provide one which identifies the columns displayed in the table.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the frame guide to which the outer frame of the subwindow is attached inside the host window. |
|  | The standard frame guide names are FL, FR, FT, and FB for the left, right, top, and bottom frame guides, respectively, or user-defined guide names as defined by the host. Use \* to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new table in the host window or subwindow specified by *hcSpec*. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/I</span> | Specifies that /W coordinates are in inches. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
| <span class="table-cell-nowrap">/M</span> | Specifies that /W coordinates are in centimeters. |
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the created table have this name, if it is not in use. If it is in use, then *name*0, *name*1, etc are tried until an unused window name is found. In a function or macro, S_name is set to the chosen table name. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Gives the table a specific location and size on the screen. Coordinates for /W are in points unless /I or /M are specified before /W. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr></tbody></table>

### *Details* {#details}
You cannot change dimension index values shown in a table. Use the Change Wave Scaling dialog or the [SetScale](/igorpro/commands/setscale.md) operation.

If /N is not used, Edit automatically assigns to the table window a name of the form "Table*n*", where *n* is some integer. In a function or macro, the assigned name is stored in the S_name string. This is the name you can use to refer to the table from a procedure. Use the [RenameWindow](/igorpro/commands/renamewindow.md) operation to rename the graph.

### *Examples* {#examples}
These examples assume that the waves are 1D.

```igor
Edit myWave,otherWave   // 2 columns: data values from each wave
Edit myWave.id          // 2 columns: x and data values
Edit cmplxWave          // 2 columns: real and imaginary data values
Edit cmplxWave.i        // One column: x values
```

The following examples illustrate the use of column name suffixes in procedures when the name of the wave is in a string variable.

```igor
Macro TestEdit()
	String w = "wave0"
	Edit $w             // edit data values
	Edit $w.i           // show index values
	Edit $w.id          // index and data values
End
```

Note that the suffix, if any, must not be stored in the string. In a user-defined function, the syntax would be slightly different:

```igor
Function TestEditFunction()
	Wave w = $"wave0"
	Edit w              // no $, because w is wave, not string
	Edit w.i            // show index values
	Edit w.id           // index and data values
End
```

### *See Also* {#see-also}
[Tables](/igorpro/igor-basics/tables.md)