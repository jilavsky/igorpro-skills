---
description: "The WinType function returns a value indicating the type of the named window."
slug: /commands/wintype
---

<div className="command-signature">

## <strong>WinType</strong> (<em>winNameStr</em>) {#wintype}

</div>

The WinType function returns a value indicating the type of the named window.

### *Details* {#details}
*winNameStr* is a string or string expression containing the name of a window or subwindow, or "" to signify the target window. When identifying a subwindow with *winNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

WinType returns the following values:

|  |  |
| --- | --- |
| 0: | No window by that name |
| 1: | Graph |
| 2: | Table |
| 3: | Layout |
| 5: | Notebook |
| 7: | Panel |
| 13 | XOP target window |
| 17 | Gizmo window in Igor Pro 7.00 or later |

Since command and procedure windows do not have ***names*** (they only have ***titles***), WinType cannot even be asked about those windows.

### *See Also* {#see-also}
[WinName](/igorpro/commands/winname.md), [ChildWindowList](/igorpro/commands/childwindowlist.md), [WinList](/igorpro/commands/winlist.md)