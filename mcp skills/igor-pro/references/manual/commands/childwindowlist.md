---
description: "The ChildWindowList function returns a string containing a semicolon-separated list of immediate subwindow window names of the specified host window or…"
slug: /commands/childwindowlist
---

<div className="command-signature">

## <strong>ChildWindowList</strong> (<em>hostNameStr</em>) {#childwindowlist}

</div>

The ChildWindowList function returns a string containing a semicolon-separated list of immediate subwindow window names of the specified host window or subwindow.

### *Parameters* {#parameters}
*hostNameStr* is a string or string expression containing the name of an existing host window or subwindow.

When identifying a subwindow with *hostNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Details* {#details}
Error if host does not exist or if it is not an allowed host type.

### *See Also* {#see-also}
[WinType](/igorpro/commands/wintype.md), [WinList](/igorpro/commands/winlist.md)