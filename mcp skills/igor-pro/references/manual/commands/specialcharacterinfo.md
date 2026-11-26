---
description: "The SpecialCharacterInfo function returns a string containing information about the named special character in the named notebook window."
slug: /commands/specialcharacterinfo
---

<div className="command-signature">

## <strong>SpecialCharacterInfo</strong> (<em>notebookNameStr</em>, <em>specialCharacterNameStr</em>, <em>whichStr</em>) {#specialcharacterinfo}

</div>

The SpecialCharacterInfo function returns a string containing information about the named special character in the named notebook window.

### *Parameters* {#parameters}
If *notebookNameStr* is "", the top visible notebook is used. Otherwise n*otebookNameStr* contains either kwTopWin for the top notebook window, the name of a notebook window or a host-child specification (an hcSpec) such as Panel0#nb0. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on host-child specifications.

*specialCharacterNameStr* is the name of a special character in the notebook.

If *specialCharacterNameStr* is "" and if exactly one special character is selected, the selected special character is used. If other than exactly one special character is selected, an error is returned.

*whichStr* identifies the information item you want. Because SpecialCharacterInfo can return several items that may contain semicolons, it does not return a semicolon-separated keyword-value list like other info functions. Instead it returns just one item as specified by *whichStr*.

### *Details* {#details}
Here are the supported values for whichStr.


| Keyword | Returned Action Information |
| --- | --- |
| NAME | The name of the special character. |
| FRAME | Value of the frame property: 0 = none; 1 = single; 2 = double; 3 = triple; 4 = shadow. |
| LOC | Paragraph and character position (e.g., 1,3). |
| SCALING | Horizontal and vertical scaling in units of one tenth of a percent (e.g., 1000,1000). |
| TYPE | Special character type is: Picture, Graph, Table, Layout, Action, ShortDate, LongDate, AbbreviatedDate, Time, Page, TotalPages, or WindowTitle. |



These keywords apply to Igor-object pictures only. If the specified special character is not an Igor-object picture, "" is returned.


| Keyword | Returned Action Information |
| --- | --- |
| WINTYPE | Returns a window type code: 1 for graphs, 2 for tables, 3 for layouts. |
| OBJECTNAME | Returns the name of the window with which the special character is associated. |



The remaining keywords apply to notebook action characters only. If the specified special character is not a notebook action character, "" is returned.


| Keyword | Returned Action Information |
| --- | --- |
| BGRGB | Background color in RGB format (e.g., 65535,65534,49151). |
| COMMANDS | Command string. |
| ENABLEBGRGB | 1 if the action's background color is enabled, 0 if not. |
| HELPTEXT | Help text string. |
| IGNOREERRORS | 0 or 1. |
| LINKSTYLE | 0 or 1. |
| PADDING | The value of the left, right, top, bottom and internal padding properties, in that order (.e.g, 4,4,4,4,8). |
| PICTURE | 1 if the action has a picture, 0 if not. |
| PROCPICTNAME | The name of the action Proc Picture or "" if none. |
| QUIET | 0 or 1. |
| SHOWMODE | Show mode property: 
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Display title only</td></tr><tr><td>2:</td><td>Display picture only</td></tr><tr><td>3:</td><td>Display picture below title</td></tr><tr><td>4:</td><td>Display picture above title</td></tr><tr><td>5:</td><td>Display picture to the left of title</td></tr><tr><td>6:</td><td>Display picture to the right of title</td></tr></tbody></table>
| TITLE | Title string. |

If *whichStr* is an unknown keyword, SpecialCharacterInfo returns "" but does not generate an error.

### *Examples* {#examples}

```igor
Function PrintSpecialCharacterInfo(notebookName, specialCharacterName)
	String notebookName, specialCharacterName

	String typeStr = SpecialCharacterInfo(notebookName, specialCharacterName, "TYPE")
	String locStr = SpecialCharacterInfo(notebookName, specialCharacterName, "LOC")

	Printf "TYPE: %s\r", typeStr
	Printf "LOC: %s\r", locStr
End
```

### *See Also* {#see-also}
[Notebook](/igorpro/commands/notebook.md), [NotebookAction](/igorpro/commands/notebookaction.md), [SpecialCharacterList](/igorpro/commands/specialcharacterlist.md), [Using Igor-Object Pictures](/igorpro/igor-basics/notebooks.md#using-igor-object-pictures)