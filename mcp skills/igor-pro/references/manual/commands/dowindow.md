---
description: "The DoWindow operation controls various window parameters and aspects. There are additional forms for DoWindow when the /S or /T flags are used (see below)."
slug: /commands/dowindow
---

<div className="command-signature">

## <strong>DoWindow</strong>  [/B[=<em>bname</em> ]/C/D/F/H/HIDE=<em>h</em> /K/N/R/W=<em>targWin</em> ] [<em>windowName</em> ] {#dowindow}

</div>

The DoWindow operation controls various window parameters and aspects. There are additional forms for DoWindow when the /S or /T flags are used (see below).

DoWindow does not support [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax).

### *Parameters* {#parameters}
*windowName* is the name of a top-level graph, table, page layout, notebook, panel, Gizmo, camera, or XOP target window. *windowName* cannot be a subwindow path.

A window's name is not the same as its title. The title is shown in the window's title bar. The name is used to manipulate the window from Igor commands. You can check both the name and the title using the Window Control dialog (in the Control submenu of the Windows menu).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B[ = *bname* ]</span> | Moves the specified window to the back (to the bottom of desktop) or behind window *bname*. |
| <span class="table-cell-nowrap">/C</span> | Changes the name of the target window to the specified name. The specified name must not be used for any other object except that it can be the name of an existing window macro. |
| <span class="table-cell-nowrap">/C/N</span> | Changes the target window name and creates a new window macro for it. However, /N does nothing if a macro or function is running. /N is not applicable to notebooks. |
| <span class="table-cell-nowrap">/D</span> | Deletes the file associated with window, if any (for notebooks only). |
| <span class="table-cell-nowrap">/F</span> | Brings the window with the given name to the front (top of desktop). |
| <span class="table-cell-nowrap">/H</span> | Specifies the command window as the target of the operation. When using /H, *windowName* must not be specified and only the /B and /HIDE flags are honored. |
|  | Use /H to bring the command window to the front (top of desktop). |
|  | Use /H/B to send the command window to the bottom of the desktop. |
|  | Use /H/HIDE to hide or show the command window. |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Sets hidden state of a window. |
|  |<table class="nested-table"><tbody><tr><td>*h*&nbsp;=0:</td><td>Visible.</td></tr><tr><td>*h*&nbsp;=1:</td><td>Hidden.</td></tr><tr><td>*h*&nbsp;=?:</td><td>Sets the variable V_flag as follows:</td></tr><tr><td></td><td>0: The window does not exist.</td></tr><tr><td></td><td>1: The window is visible.</td></tr><tr><td></td><td>2: The window is hidden.</td></tr></tbody></table>
|  | You can also read the hidden state using [GetWindow](/igorpro/commands/getwindow.md) and set it using [SetWindow](/igorpro/commands/setwindow.md). |
| <span class="table-cell-nowrap">/K</span> | Kills the window with the given name. |
|  | We recommend using [KillWindow](/igorpro/commands/killwindow.md) instead of DoWindow/K. |
| <span class="table-cell-nowrap">/N</span> | Creates a new window macro for the window with the given name. However, /N does nothing if a macro or function is running. /N is not applicable to notebooks. |
| <span class="table-cell-nowrap">/R</span> | Replaces (updates) the window macro for the named window or creates it if it does not yet exist. However, /R does nothing if a macro or function is running. /R is not applicable to notebooks. |
| <span class="table-cell-nowrap">/R/K</span> | Replaces (updates) the window macro for the named window or creates it if it does not yet exist and then kills the window. However, /R does nothing if a macro or function is running. /R is not applicable to notebooks. |
| <span class="table-cell-nowrap">/W = *targWin*</span> | Designates *targWin* as the target window; it also requires that you specify *windowName*. Use this mainly with floating panels, which are always on top. You can use a subwindow specification of an external subwindow only with the /T flag or without any flags. |

### *Details* {#details}
DoWindow sets the variable V_flag to 1 if there was a window with the specified name after DoWindow executed, to 0 if there was no such window, or to 2 if the window is hidden.

You can call DoWindow with a *windowName* and no flags to check if a window exists without altering the window. A better method is to use [WinType](/igorpro/commands/wintype.md) which supports subwindows.

When used with the /N flag, *windowName* must not conflict with the name of any other object. When used with the /C flag, *windowName* must not conflict with the name of any other object except that it can be the name of an existing window macro.

The /R and /N flags do nothing when executed while a macro or function is running. This is necessary because changing procedures while they are executing causes unpredictable and undesirable results. However you can use the Execute/P operation to cause the DoWindow command to be executed after procedures are finished running. For example:


```igor
Function SaveWindowMacro(windowName)
	String windowName             // "" for top graph or table
	
	if (strlen(windowName) ==  0)
		windowName = WinName(0, 3) // Name of top graph or table
	endif
	
	String cmd
	sprintf cmd, "DoWindow/R %s", windowName
	Execute/P cmd
End
```

You can use the /D flag in conjunction with the /K flag to kill a notebook window and delete its associated file, if any. /D has no effect on any other type of window and has no effect if the /K flag is not present.

### *Examples* {#examples}

```igor
DoWindow Graph0         // Set V_flag to 1 if Graph0 window exists.
DoWindow/F Graph0       // Make Graph0 the top/target window.
DoWindow/C MyGraph      // Target window (Graph0) renamed MyGraph.
DoWindow/H/B            // Put the command window in back.
DoWindow/D/K Notebook2  // Kill Notebook2, delete its file.
```

### *See Also* {#see-also}
[RenameWindow](/igorpro/commands/renamewindow.md), [MoveWindow](/igorpro/commands/movewindow.md), [MoveSubWindow](/igorpro/commands/movesubwindow.md), [SetActiveSubwindow](/igorpro/commands/setactivesubwindow.md), [KillWindow](/igorpro/commands/killwindow.md)

[HideProcedures](/igorpro/commands/hideprocedures.md), [IgorInfo](/igorpro/commands/igorinfo.md)
<br>

<div className="command-signature">

## <strong>DoWindow</strong>  /T windowName, <em>windowTitleStr</em> {#dowindow}

</div>

The DoWindow/T operation sets the window title for the named window to the specified title.

### *Details* {#dowindow-details}
The title is shown in the window's title bar, and listed in the appropriate Windows submenu. The window name is still used to manipulate the window, so, for example, the window name (if *windowName* is a graph or table) is listed in the New Layout dialog, not the title.

You can check both the name and the title using the Window Control dialog (in the Control submenu of the Windows menu).

*windowName* is the name of the window or a special keyword, kwTopWin or kwFrame.

If *windowName* is kwTopWin, DoWindow retitles the top target window.

If *windowName* is kwFrame, DoWindow retitles the "frame" or "application" window that Igor has only under Windows. This is the window that contains Igor's menus and status bar.

The Window Control dialog does not support kwFrame. The frame title persists until Igor quits or until it is restored as shown in the example. Setting *windowTitleStr* to "" will restore the normal frame title.

### *Examples* {#dowindow-examples}

```igor
DoWindow/T MyGraph, "My Really Neat Graph"
DoWindow/T kwFrame, "My Igor-based Application"
DoWindow/T kwFrame, ""	// restore normal frame title
```

### *See Also* {#dowindow-see-also}
Other DoWindow sections.
<br>

<div className="command-signature overload">

## <strong>DoWindow</strong>  /N/S=<em>styleMacroName</em> <em>windowName</em> {#dowindow}

</div>
<div className="command-signature">

## <strong>DoWindow</strong>  /R/S=<em>styleMacroName</em> <em>windowName</em> {#dowindow}

</div>

The DoWindow/S operation creates a new style macro for the named window, using the specified style macro name. Does not create or replace the window macro for the specified window.

### *Flags* {#dowindow-flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N/S = *styleMacroName*</span> | Creates a new style macro with the given name based on the named window. |
| <span class="table-cell-nowrap">/R/S = *styleMacroName*</span> | Creates or replaces the style macro with the given name based on the named window. |

### *Details* {#dowindow-details}
The /R or /N flag must appear before the /S flag.

If the /S flag is present, the DoWindow operations does not create or replace the window macro for the specified window.

The /R and /N flags do nothing when executed while a macro or function is running. This is necessary because changing procedures while they are executing causes unpredictable and undesirable results.

### *See Also* {#dowindow-see-also}
Previous DoWindow sections.