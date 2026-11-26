---
description: "The WinRecreation function returns a string containing the window recreation macro (or style macro) for the named window."
slug: /commands/winrecreation
---

<div className="command-signature">

## <strong>WinRecreation</strong> (<em>winStr</em>, <em>options</em>) {#winrecreation}

</div>

The WinRecreation function returns a string containing the window recreation macro (or style macro) for the named window.

### *Parameters* {#parameters}
*winStr* is the name of a graph, table, page layout, panel, notebook, Gizmo, camera, or XOP target window or the title of a procedure window or help file. If *winStr* is "" and *options* is 0 or 1, information for the top graph, table, page layout, panel, notebook, or XOP target window is returned.

As of Igor Pro 7.00, *winStr* may be a subwindow path. The returned recreation macro is generated as if the subwindow were extracted from its host as a standalone window. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the path to a subwindow.

The meaning of *options* depends on the type of window as described in the following sections.

### *Target Window Details* {#target-window-details}
Target windows include graphs, tables, page layouts, panels, notebooks, and XOP target windows.

If *options* is 0, WinRecreation returns the window recreation macro.

If *options* is 1, WinRecreation returns the style macro or an empty string if the window does not support style macros.

### *Graphs Details* {#graphs-details}
If *options* is 2, WinRecreation returns a recreation macro in which all occurrences of wave names are replaced with an ID number having the form ##\<number\>## (for instance, ##25##). These ID numbers can be found easily using the function [strsearch](/igorpro/commands/strsearch.md). This is intended for applications that need to alter the recreation macro by replacing wave names with something else, usually other wave names. The ID numbers are the same as those returned by the [GetWindow](/igorpro/commands/getwindow.md) operation with the wavelist keyword.

### *Graphs and Panels Details* {#graphs-and-panels-details}
If *options* is 4, WinRecreation returns the window recreation macro without the default behavior of causing the graph to revert to "normal" mode (as if the GraphNormal operation had been called). This allows the use of WinRecreation when a graph or panel is in drawing tools mode without exiting that mode. For windows other than graphs or panels, this is equivalent to an *options* value of 0.

### *Notebooks Details* {#notebooks-details}
If *options* is -1, WinRecreation returns the same text that the Generate Commands menu item would generate with the Selected paragraphs radio button selected and all the checkboxes selected (includes text commands).

If *options* is 0, WinRecreation returns the same text that the Generate Commands menu item would generate with the Entire document radio button selected and all the checkboxes **except** "Generate text commands" selected).

If *options* is 1, WinRecreation returns the same text that the Generate Commands menu item would generate with the Entire document radio button selected and all the checkboxes selected (includes text commands).

Regardless of the value of *options,* the text returned by WinRecreation for notebook always ends with 5 lines of file-related information formatted as comments:


```igor
// File Name: MyNotebook.txt
// Path: "C:\Users\John\Documents\WaveMetrics\"
// Symbolic Path: \_none\_
// Selection Start: paragraph 0, position 9
// Selection End: paragraph 0, position 9
```

### *Help Windows Details* {#help-windows-details}
WinRecreation returns the same 5 lines of file-related information as described above for notebooks.

Set *options* to -3 to ensure that *winStr* is interpreted as a help window title (help windows have only titles, not window names).

### *Procedures Details* {#procedures-details}
WinRecreation returns the same 5 lines of file-related information as described above for notebooks.

Set *options* to -2 to ensure that *winStr* is interpreted as a procedure window title (procedure windows have only titles, not window names).

If SetIgorOption IndependentModuleDev=1 is in effect, *winStr* can also be a procedure window title followed by a space and, in brackets, an independent module name. In such cases WinRecreation returns text from or information about the specified procedure file which is part of that independent module. (See [Independent Modules](/igorpro/advanced-topics.md#independent-modules) for independent module details.)

For example, in an experiment containing:


```igor
#pragma IndependentModule=myIM
#include <Axis Utilities>
```

Code like this:


```igor
String text=WinRecreation("Axis Utilities.ipf [myIM]",-2)
```

will return the file-related information for the Axis Utilities.ipf procedure window, which is normally a hidden part of the myIM independent module.

To get the text contents of a procedure window, use [ProcedureText](/igorpro/commands/proceduretext.md).

### *Examples* {#examples}

```igor
WinRecreation("Graph0",0)               // Returns recreation macro for Graph0.
WinRecreation("",1)                     // Style macro for top window.
String win= WinName(0,16,1)             // top visible notebook
String str= WinRecreation(str,-1)       // Selected Text commands
Variable line= itemsInList(str,"\r")-5  // First file info line
Print StringFromList(line, str,"\r")    // Print File Name:
Print StringFromList(line+1, str,"\r")  // Print Path:
Print StringFromList(line+2, str,"\r")  // Print Symbolic Path:
Print StringFromList(line+3, str,"\r")  // Selection Start:
Print StringFromList(line+4, str,"\r")  // Selection End:
```

### *See Also* {#see-also}
[Saving a Window as a Recreation Macro](/igorpro/igor-basics/using-igor.md#saving-a-window-as-a-recreation-macro)