---
description: "The NewGizmo operation creates a new Gizmo display window. The NewGizmo operation will fail if the graphics hardware or drivers are incompatible with Gizmo."
slug: /commands/newgizmo
---

<div className="command-signature">

## <strong>NewGizmo</strong>  [ /FG=(<em>gLeft</em>, <em>gTop</em>, <em>gRight</em>, <em>gBottom</em>) /HOST=<em>hcSpec</em> /I /N=<em>name</em>  /T=<em>titleStr</em> /K=<em>k</em> /W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em>)] {#newgizmo}

</div>

The NewGizmo operation creates a new Gizmo display window.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FG = (*gLeft*, *gTop*, *gRight*, *gBottom* )</span> |  |
|  | Specifies the frame guide to which the outer frame of the subwindow is attached inside the host window. |
|  | The standard frame guide names are FL, FR, FT, and FB for the left, right, top, and bottom frame guides, respectively, or user-defined guide names as defined by the host. Use * to specify a default guide name. |
|  | Guides may override the numeric positioning set by /W. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new Gizmo in the host window or subwindow specified by *hcSpec*. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/I</span> | Opens the info window. |
|  | The info window may be opened by default if that option is set in Gizmo section of the Miscellaneous Settings dialog. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default)</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills without dialog</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window</td></tr><tr><td>*k*&nbsp;=4:</td><td>Kills with no dialog and is not saved with the experiment.</td></tr></tbody></table>
|  | If you use /K=2 or /K=3, you can still kill the window using the [KillWindow](/igorpro/commands/killwindow.md) operation. |
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the created Gizmo window have the specified name, if it is not in use. If it is in use, then *name*0, *name*1, etc. are tried until an unused window name is found. In a function or macro, the output string variable S_name is set to the chosen window name. |
|  | A function or macro with the same name will cause a name conflict. |
| <span class="table-cell-nowrap">/T = *titleStr*</span> | *titleStr* is a string expression containing the title of the new Gizmo window. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Sets the initial coordinates of the Gizmo window in points. The coordinates may be clipped depending on the dimensions of the connected display. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr><tr><td></td><td>When the subwindow position is fully specified using guides (using the /HOST or /FG flags), the /W flag may still be used although it is not needed.</td></tr></tbody></table>

### *Details* {#details}
The NewGizmo operation will fail if the graphics hardware or drivers are incompatible with Gizmo. In some cases this problem can be resolved by updating the graphics drivers.

### *See Also* {#see-also}
[3D Graphics](/igorpro/graphing/3d-graphics.md), [AppendToGizmo](/igorpro/commands/appendtogizmo.md), [ExportGizmo](/igorpro/commands/exportgizmo.md), [GetGizmo](/igorpro/commands/getgizmo.md), [GizmoInfo](/igorpro/commands/gizmoinfo.md), [ModifyGizmo](/igorpro/commands/modifygizmo.md), [RemoveFromGizmo](/igorpro/commands/removefromgizmo.md)