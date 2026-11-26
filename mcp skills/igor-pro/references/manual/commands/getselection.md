---
description: "The GetSelection operation returns information about the selection in the specified window."
slug: /commands/getselection
---

<div className="command-signature">

## <strong>GetSelection</strong>  <em>winType</em>, <em>winName</em>, <em>bitflags</em> {#getselection}

</div>

The GetSelection operation returns information about the selection in the specified window.

### *Parameters* {#parameters}
*winType*  is one of the following keywords:

`graph`, `panel`, `table`, `layout`, `notebook`, `procedure`

*winName* is the name of a window of the specified type.

When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

If *winType* is procedure then *winName* is actually a procedure window title inside a $"" wrapper, such as:


```igor
GetSelection procedure $"DemoLoader.ipf", 3
```

*bitflags* is a bitwise parameter that is used in different ways for different window types, as described below. You should use 0 for undefined bits. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

### *Details* {#details}
For all window types, GetSelection sets V_flag:


|  |  |  |
| --- | --- | --- |
| V_flag | 0: | there was no selection when GetSelection was invoked. |
|  | 1: | there was a selection when GetSelection was invoked. |

Here is a description of what GetSelection does for each window type:


| winType | bitflags | Action |
| --- | --- | --- |
| graph |  | Does nothing. |
| panel |  | Does nothing. |
| table | 1 | Sets V_startRow, V_startCol, V_endRow, V_endCol based on the selected cells in the table. The top/left cell, not including the Point column, is (0, 0). |
|  | 2 | Sets S_selection to a semicolon-separated list of column names. |
|  | 4 | Sets S_dataFolder to a semicolon-separated list of data folders, one for each column. |
| layout | 2 | Sets S_selection to a semicolon separated list of selected objects in the layout layer (not any drawing layers). S_selection will be "" if no objects are selected. |
| notebook | 1 | Sets V_startParagraph, V_startPos, V_endParagraph, V_endPos based on the selected text in the notebook. |
|  | 2 | Sets S_selection to the selected text. |
|  | 4 | Requires Igor Pro 8.05 or later. |
|  |  | Sets V_startParagraph and V_endParagraph to the left margin and right margin respectively of the current ruler in points relative to the ruler 0 position. |
|  |  | Sets V_startPos, and V_endPos to the left edge and right edge respectively of the selection in points relative to the ruler 0 position. |
| procedure | 1 | Sets V_startParagraph, V_startPos, V_endParagraph, V_endPos based on the selected text in the procedure window. |
|  | 2 | Sets S_selection to the selected text. |

### *Examples* {#examples}
In a new experiment, make a table named "Table0" with some columns, and select some combination of rows and columns:


```igor
Make wave0 = p
Make wave1 = p + 1
Edit wave0, wave1
ModifyTable  selection=(3 , 0 , 8 , 1, 3, 0)
```

Now execute these commands in a procedure or in the command line:


```igor
GetSelection table, Table0, 3
Print V_flag, V_startRow, V_startCol, V_endRow, V_endCol
Print S_selection
```

This prints the following in the history area:


```
  1  3  0  8  1
  wave0.d;wave1.d;
```