---
description: "The WinName function returns a string containing the name of the indexth window of the specified windowTypes, or an empty string (\"\") if no window fits the…"
slug: /commands/winname
---

<div className="command-signature">

## <strong>WinName</strong> (<em>index</em>, <em>windowTypes</em> [, <em>visibleWindowsOnly</em> [, <em>floatKind</em>]]) {#winname}

</div>

The WinName function returns a string containing the name of the *index*th window of the specified *windowTypes*, or an empty string ("") if no window fits the parameters.

If the optional *visibleWindowsOnly* parameter is nonzero, only visible windows are considered. Otherwise both visible and hidden windows are considered.

If the optional *floatKind* parameter is 1, only floating windows created with [NewPanel](/igorpro/commands/newpanel.md)/FLT=1 are considered. If *floatKind* is 2, only [NewPanel](/igorpro/commands/newpanel.md)/FLT=2 windows are considered. *windowTypes* must contain at least 64 (panels).

If *floatKind* is omitted or is 0 only non-floating ("normal") windows are considered.

Procedure windows don't have names. WinName returns the procedure window title instead.

### *Details* {#details}
*index* starts from zero, and returns the top-most window matching the parameters.

The window names are ordered in window-stacking order, as returned by [WinList](/igorpro/commands/winlist.md).

[DoWindow](/igorpro/commands/dowindow.md)/B moves the window to the back and changes the index needed to retrieve its name to the greatest index that returns any name.

Hiding or showing a window (with [SetWindow](/igorpro/commands/setwindow.md) hide=1 or [Notebook](/igorpro/commands/notebook.md) visible=0 or by manual means) does not affect the index associated with the window.

*windowTypes* is a bitwise parameter:

|  |  |
| --- | --- |
| 1: | Graphs |
| 2: | Tables |
| 4: | Layouts |
| 16: | Notebooks |
| 64: | Panels |
| 128: | Procedure windows |
| 512: | Help windows |
| 4096: | XOP target windows |
| 16384: | Camera windows in Igor Pro 7.00 and later |
| 65536: | Gizmo windows in Igor Pro 7.00 and later |


See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings.

### *Examples* {#examples}

```igor
Print WinName(0,1)      // Prints the name of the top graph.
Print WinName(0,3)      // Prints the name of the top graph or table.
String win=WinName(0,1) // The name of the top visible graph.
SetWindow $win hide=1   // Hide the graph (it may already be hidden).
Print WinName(0,1)      // Prints the name of the now-hidden graph.
Print WinName(0,1,1)    // Prints the name of the top visible graph.
Print WinName(0,64,1,1) // Name of the top visible NewPanel/FLT=1 window.
```

### *See Also* {#see-also}
[WinList](/igorpro/commands/winlist.md), [DoWindow](/igorpro/commands/dowindow.md) (the /F and /B flags)

[SetWindow](/igorpro/commands/setwindow.md) (the hide keyword), [Notebook](/igorpro/commands/notebook.md) (the visible keyword)

[NewPanel](/igorpro/commands/newpanel.md) (/FLT flag)