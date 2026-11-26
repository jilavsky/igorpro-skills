---
description: "The GetUserData function returns a string containing the user data for a window, subwindow, graph trace or control."
slug: /commands/getuserdata
---

<div className="command-signature">

## <strong>GetUserData</strong> (<em>winName</em>, <em>objID</em>, <em>userdataName</em>) {#getuserdata}

</div>

The GetUserData function returns a string containing the user data for a window, subwindow, graph trace or control. The return string will be empty if no user data exists.

You set user data on a window or subwindow using the userData keyword of the SetWindow operation. You set it on a graph trace using the userData keyword of the ModifyGraph operation. You set it on a control using the userData keyword of the various control operations.

### *Parameters* {#parameters}
*winName* may specify a window or subwindow name. Use "" for the top window.

When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*objID* is a string specifying the name of a control or graph trace. Use "" for a window or subwindow.

*userdataName* is the name of the user data or "" for the default unnamed user data.

### *See Also* {#see-also}
[ControlInfo](/igorpro/commands/controlinfo.md), [GetWindow](/igorpro/commands/getwindow.md), [SetWindow](/igorpro/commands/setwindow.md)