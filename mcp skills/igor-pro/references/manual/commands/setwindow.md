---
description: "The SetWindow operation sets the window note and user data for the named window or subwindow."
slug: /commands/setwindow
---

<div className="command-signature">

## <strong>SetWindow</strong>  <em>winName</em> [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#setwindow}

</div>

The SetWindow operation sets the window note and user data for the named window or subwindow. SetWindow can also set hook functions for a base window or exterior subwindow (interior subwindows not supported).

### *Parameters* {#parameters}
*winName* can be the name of any target window (graph, table, page layout, notebook, control panel, Gizmo, camera, or XOP target window) or subwindow. It can also be the keyword kwTopWin to specify the topmost target window.

When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">activeChildFrame = *f*</span> | Determines if the frame indicating the active subwindow in the named window or subwindow is drawn. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=-1:</td><td>Default. Recursively check ancestors of this window. If one is found with a value of either 0 or 1, use that value. If the topmost window has a value of -1, then the frame is drawn.</td></tr><tr><td>*f*&nbsp;=1:</td><td>If this subwindow or one of its descendants becomes active, then the frame is drawn.</td></tr><tr><td>*f*&nbsp;=0:</td><td>If this subwindow or one of its descendants becomes active, then the frame is not drawn.</td></tr></tbody></table>
| <span class="table-cell-nowrap">doScroll = *mode*</span> | Controls scrolling mode for top-level graph and panel windows only. The doScroll keyword was added in Igor Pro 9.00. |
|  |<table class="nested-table"><tbody><tr><td>*mode*=1:</td><td>Turns scrolling mode on for the graph or panel.</td></tr></tbody></table>
|  | When scrolling mode is on, the size of the content area of the graph or panel is fixed and the window no longer grows or shrinks when you resize the window. If you shrink the window smaller than the size of the content area, scroll bars appear which allow you to view different parts of the content area. |
|  | When scrolling mode is on, you can change the size of the content area of the graph or panel window using doScroll=(*width*, *height*). |
|  |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>Turns scrolling mode off for the graph or panel.</td></tr></tbody></table>
|  | When scrolling mode is off, scroll bars are not shown and the size of the content area of the graph or panel grows or shrinks when you resize the window. |
| <span class="table-cell-nowrap">doScroll = (*width*, *height*)</span> | Controls scrolling mode for top-level graph and panel windows only. The doScroll keyword was added in Igor Pro 9.00. |
|  | Turns scrolling mode on if it is off. Sets the size of the content area of the graph or panel. *width* and *height* are in units of points. |
| <span class="table-cell-nowrap">graphicsTech = *t*</span> | Sets the graphics technology used to draw the window. This flag may be useful in rare cases to work around graphics limitations. See [Graphics Technology](/igorpro/graphing/making-figures/graphics.md#graphics-technology) for background information. |
|  |<table class="nested-table"><tbody><tr><td>*t*=0:</td><td>Default: The graphics technology specified in Miscellaneous Settings dialog, Miscellaneous category. This is Qt Graphics by default.</td></tr><tr><td>*t*=1:</td><td>Native: GDI+.</td></tr><tr><td>*t*=2:</td><td>Old: GDI.</td></tr></tbody></table>
| <span class="table-cell-nowrap">hide = *h*</span> | Hides or unhides widows or subwindows. |
|  |<table class="nested-table"><tbody><tr><td>*h*&nbsp;=0:</td><td>Unhides a subwindow or base window</td></tr><tr><td>*h*&nbsp;=1:</td><td>Hides a subwindow or base window.</td></tr><tr><td>*h*&nbsp;=2:</td><td>Unhides without restoring minimized windows (*Windows* only).</td></tr></tbody></table>
|  | When unhiding subwindows, you should combine with needUpdate=1 if conditions require the subwindow to be redrawn since the window was hidden. |
| <span class="table-cell-nowrap">hook = *procName*</span> | Sets the window hook function that Igor will call when certain events happen. Use SetWindow hook=$"" to specify no hook function. |
|  | See [Unnamed Window Hook Functions](/igorpro/advanced-topics.md#unnamed-window-hook-functions) below for further details. |
| <span class="table-cell-nowrap">hook(*hName* ) = *procName*</span> |  |
|  | Defines a named window hook *hName* and sets the function that Igor will call when certain events happen *hName* can be any legal name. Named hooks are called before any unnamed hooks. |
|  | Use $"" for *procName* to specify no hook. |
|  | See [Named Window Hook Functions](/igorpro/advanced-topics.md#named-window-hook-functions) for further details. |
|  | To hook a subwindow, see [Window Hooks and Subwindows](/igorpro/advanced-topics.md#window-hooks-and-subwindows). |
| <span class="table-cell-nowrap">hookcursor = *number*</span> | Sets the mouse cursor. This keyword is antiquated. See [Setting the Mouse Cursor](/igorpro/advanced-topics.md#setting-the-mouse-cursor) for the preferred technique. |
| <span class="table-cell-nowrap">hookevents = *flags*</span> | Bitfield of flags to enable certain events for the unnamed hook function: |
|  |<table class="nested-table"><tbody><tr><td>bit&nbsp;0:</td><td>Mouse button clicks</td></tr><tr><td>bit&nbsp;1:</td><td>Mouse moved events</td></tr><tr><td>bit&nbsp;2:</td><td>Cursor moved events</td></tr></tbody></table>
|  | To set bit 0 and bit 1 (mouse clicks and mouse moved), use 2<sup>0</sup>+2<sup>1</sup> = 1+2 = 3 for *flags*. Use 7 to also enable cursor moved events. See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | This keyword applies to the unnamed hook function only. It does not affect named hook functions which always receive all events. |
| <span class="table-cell-nowrap">markerHook = {*hookFuncName*, *start*, *end* }</span> |  |
|  | Specifies a user function and marker number range for custom markers. The marker range can be any positive integers less than 1000 and can overlap built-in marker numbers. See [Custom Marker Hook Functions](/igorpro/advanced-topics.md#custom-marker-hook-functions) for details. |
|  | Use $"" for *hookFuncName* to specify no hook. |
| <span class="table-cell-nowrap">needUpdate = *n*</span> | Marks a window as needing an update (*n* =1) or takes no action (*n* =0). |
| <span class="table-cell-nowrap">note = *noteStr*</span> | Sets the window note to *noteStr*, replacing any existing note. |
| <span class="table-cell-nowrap">note+ = *noteStr*</span> | Appends *noteStr* to current contents of the window note. |
| <span class="table-cell-nowrap">sizeLimit = {*minWidth, minHeight, maxWidth, maxHeight*}</span> |  |
|  | Imposes limits on a window's size when resized with the mouse or by calling [MoveWindow](/igorpro/commands/movewindow.md). The units of the limits are the same as those returned by [GetWindow](/igorpro/commands/getwindow.md) wsize. |
|  | The sizeLimit keyword was added in Igor Pro 7.00. |
|  | To allow the window width to grow essentially without bound, pass INF for *maxWidth*. |
|  | To allow the window height to grow essentially without bound, pass INF for *maxHeight*. |
|  | If *minWidth* > *maxWidth* or *minHeight* > *maxHeight*, the maximum dimensions are set to the minimum, effectively fixing the size of the window in that dimension. For control panels, it is better to use [ModifyPanel](/igorpro/commands/modifypanel.md) fixedSize=1. |
|  | Combining these limits with [ModifyGraph](/igorpro/commands/modifygraph.md) width and height modes leads to unexpected results and is discouraged. |
|  | If you first use sizeLimit and then execute ModifyPanel fixedSize=1 on the same window, the fixedSize command takes precedence. If you execute SetWindow sizeLimit on a control panel that has fixedSize=1, Igor generates an error. |
|  | Igor includes a SetWindow sizeLimit command in a window recreation macro if necessary. Igor 6 does not support SetWindow sizeLimit so this causes an error when recreating the window in Igor 6.  If you never set the sizeLimit property for a window, or if the minimum dimensions are very small and maximum dimensions are INF, then no SetWindow command is generated. |
| <span class="table-cell-nowrap">tooltipHook(*hName*) = *procName*</span> |  |
|  | A tooltip hook function is like a window hook function (see [Named Window Hook Functions](/igorpro/advanced-topics.md#named-window-hook-functions)), except that it allows you to alter the text of a tooltip in a graph or table. At present, a tooltip hook function is called for a graph when the mouse hovers over a trace or image, and for a table when the mouse hovers over the data for a wave. |
|  | Unlike a window hook function, a tooltip hook function can be set for either a top-level window or a subwindow. |
|  | For details, see [Tooltip Hook Functions](/igorpro/advanced-topics.md#tooltip-hook-functions). |
| <span class="table-cell-nowrap">userdata = *UDStr*</span> |  |
| <span class="table-cell-nowrap">userdata(*UDName* ) = *UDStr*</span> |  |
|  | Sets the window or subwindow user data to string *UDStr*. Use the optional (*UDName*) to create named user data. |
|  | Names starting with "WM_" are reserved for WaveMetrics. |
| <span class="table-cell-nowrap">userdata+ = *UDStr*</span> |  |
| <span class="table-cell-nowrap">userdata(*UDName* )+ = *UDStr*</span> |  |
|  | Appends string *UDStr* to the current window or subwindow user data. Use the optional (*UDName* ) to append to the named user data. |
|  | Names starting with "WM_" are reserved for WaveMetrics. |

### *Details* {#details}
For details on named window hooks, see [Window Hook Functions](/igorpro/advanced-topics.md#window-hook-functions).

Unnamed window hook functions are supported for backward compatibility only. New code should use [Named Window Hook Functions](/igorpro/advanced-topics.md#named-window-hook-functions). For details on unnamed window hooks, see [Unnamed Window Hook Functions](/igorpro/advanced-topics.md#unnamed-window-hook-functions).

For details on marker hooks, see [Custom Marker Hook Functions](/igorpro/advanced-topics.md#custom-marker-hook-functions).

You can also attach user data to traces in graphs using the userData keyword of the ModifyGraph operation and to controls using the userData keyword of the various control operations.

### *See Also* {#see-also}
[GetWindow](/igorpro/commands/getwindow.md), [GetUserData](/igorpro/commands/getuserdata.md), [SetIgorMenuMode](/igorpro/commands/setigormenumode.md)

[AxisValFromPixel](/igorpro/commands/axisvalfrompixel.md), [NumberByKey](/igorpro/commands/numberbykey.md), [TraceFromPixel](/igorpro/commands/tracefrompixel.md), [PopupContextualMenu](/igorpro/commands/popupcontextualmenu.md)