---
description: "The GetMouse operation returns information about the position of the input mouse, and the state of the mouse buttons."
slug: /commands/getmouse
---

<div className="command-signature">

## <strong>GetMouse</strong>  [ /W=<em>winName</em> ] {#getmouse}

</div>

The GetMouse operation returns information about the position of the input mouse, and the state of the mouse buttons.

GetMouse is useful in situations such as [background tasks](/igorpro/advanced-topics.md#background-tasks) where the mouse position and state aren't available as they are in control procedures and window hook functions.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Returns the mouse position relative to the named window or subwindow. When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax). |
| <span class="table-cell-nowrap">/W = kwTopWin</span> | Returns the mouse position relative to the currently frontmost non-floating window. |
| <span class="table-cell-nowrap">/W = kwCmdHist</span> | Returns the mouse position relative to the command window. |
| <span class="table-cell-nowrap">/W = Procedure</span> | Returns the mouse position relative to the main Procedure window. |

### *Details* {#details}
GetMouse returns the mouse position in local coordinates relative to the specified window unless /W is omitted in which case the returned coordinates are global.

Global coordinates are actually relative to the frame window. See [GetWindow](/igorpro/commands/getwindow.md) wsizeDC kwFrameInner.

Information is returned via the following string and numeric variables:


|  |  |
| --- | --- |
| V_left | Horizontal mouse position, in pixels. |
| V_top | Vertical mouse position, in pixels. |
| V_flag | Mouse button state. V_flag  is a bitwise value with each bit reporting the mouse button states: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>1 if the primary mouse button (usually the left) is down, 0 if it is up.</td></tr><tr><td>bit&nbsp;1:</td><td>1 if the secondary mouse button (usually the right) is down, 0 if it is up.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| S_name | Name of the window or subwindow which the position is relative to, or "" if not a nameable window or if /W was omitted. Most useful with /W=kwTopWin. The result can be kwCmdHist or Procedure, or the name of a target window. |

### *See Also* {#see-also}
[GetWindow](/igorpro/commands/getwindow.md), [GetKeyState](/igorpro/commands/getkeystate.md), [SetWindow](/igorpro/commands/setwindow.md), [WMWinHookStruct](/igorpro/advanced-topics.md#wmwinhookstruct), [WMButtonAction](/igorpro/programming/structures/wmbuttonaction.md), [Background Tasks](/igorpro/advanced-topics.md#background-tasks), [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax)