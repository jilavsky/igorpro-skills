---
description: "The ModifyPanel operation modifies properties of the top or named graph or panel window or subwindow."
slug: /commands/modifypanel
---

<div className="command-signature">

## <strong>ModifyPanel</strong>  [/W=<em>winName</em> ] [<em>cbRGB</em>=(<em>r</em>,<em>g</em>,<em>b</em>[,<em>a</em>]), <em>drawInOrder</em>=<em>d</em>, <em>expand</em>=<em>e</em>, <em>fixedSize</em>=<em>f</em>,  <em>frameInset</em>=<em>i</em>, <em>frameStyle</em>=<em>f</em>, <em>noEdit</em>=<em>e</em>  ] {#modifypanel}

</div>

The ModifyPanel operation modifies properties of the top or named graph or panel window or subwindow.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">cbRGB = (*r,g,b*[,*a*])</span> | Specifies the background color of the entire control panel or the graph's control bar area. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">drawInOrder = *d*</span> | Determines the drawing order of controls in the control panel. |
|  |<table class="nested-table"><tbody><tr><td>*d*=0:</td><td>Draw tab controls before any other controls (default).</td></tr><tr><td>*d*=1:</td><td>Draw all controls in the order in which they appear in the recreation macro, which is also the creation order.</td></tr></tbody></table>
|  | The drawInOrder keyword was added in Igor Pro 8.00. |
|  | Prior to Igor Pro 8.00 tab controls (see [TabControl](/igorpro/user-interface/controls.md#tabcontrol)) were always drawn before all other controls. This prevented placing a tab control inside a groupbox with a colored interior. *drawInOrder*=1 forces Igor to draw controls in creation order, which is the same as the order in which they appear in a recreation macro. |
| <span class="table-cell-nowrap">expand = *e*</span> | Sets the expansion factor of the panel. Values of *e* greater than 1.0 make the panel, its controls, and its subwindows, appear larger than normal. *e* is a number between 0.25 to 8.0. |
|  | Though rarely needed, using the expand keyword, you can set the expansion of panel subwindows independent of the main panel window's expansion. |
|  | When you change the expansion of a top-level control panel window, the panel window automatically resizes itself. |
|  | The expand keyword was added in Igor Pro 9.00. |
|  | See [Control Panel Expansion](/igorpro/user-interface/controls.md#control-panel-expansion) for further discussion. |
| fixedSize=*f* |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>Panel can be resized (the default).</td></tr><tr><td>*f*&nbsp;=1:</td><td>Panel cannot be resized by the user adjusting the grow box or frame (nor maximized on Windows), but the window can be minimized (on Windows) and the MoveWindow operation can still change the size.</td></tr></tbody></table>
|  | The *fixedSize* keyword overrides any previous size limit set using the SetWindow sizeLimit command. If you try to use SetWindow sizeLimit on a window with fixedSize=1, an error results. |
| <span class="table-cell-nowrap">frameInset = *i*</span> | Specifies the number of pixels by which to inset the frame of the panel subwindow. Mostly useful for overlaying panels in graphs to give a fake 3D frame a better appearance. |
| <span class="table-cell-nowrap">frameStyle = *f*</span> | specifies the frame style for a panel subwindow. Values for frameStyle are: |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>None</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single</td></tr><tr><td>*f*&nbsp;=2:</td><td>Indented</td></tr><tr><td>*f*&nbsp;=3:</td><td>Raised</td></tr><tr><td>*f*&nbsp;=4:</td><td>Text well</td></tr></tbody></table>
|  | The last three styles are fake 3D and will look good only if the  background color of the enclosing space and the panel itself is a light shade of gray. |
| <span class="table-cell-nowrap">noEdit = *e*</span> | Sets the editability of the panel. |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=0:</td><td>Editable (default).</td></tr><tr><td>*e*&nbsp;=1:</td><td>Not editable. For a panel window, the Panel menu item is not present and the ShowTools command is ignored. For a panel subwindow, it cannot be activated by clicking.</td></tr></tbody></table>

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies the control panel in the named graph or control panel window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
On Windows, set *r*, *g*, and *b* to 65535 (maximum white) to set the background color of the control panel to track the 3D Objects color in the Appearance Tab of the Display Properties control panel.

### *See Also* {#see-also}
[NewPanel](/igorpro/commands/newpanel.md), [Controls in Graphs](/igorpro/user-interface/controls.md#controls-in-graphs)