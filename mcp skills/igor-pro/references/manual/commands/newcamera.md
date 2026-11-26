---
description: "The NewCamera operation creates a new camera window to display live video from supported hardware cameras."
slug: /commands/newcamera
---

<div className="command-signature">

## <strong>NewCamera</strong>  [/HIDE=<em>h</em>  /HOST=<em>hcSpec</em> /K=<em>k</em> /S=<em>sequence</em>  /N=<em>winName</em> /W=(<em>left</em>,<em>top</em>,<em>right</em>,<em>bottom</em> ) ] [<em>hardwareName</em>=<em>hwName</em>] {#newcamera}

</div>

The NewCamera operation creates a new camera window to display live video from supported hardware cameras.

NewCamera was added in Igor Pro 7.00, and deprecated in Igor Pro 10.00.

Use [MMI_NewCamera](/igorpro/extensions/data-acquisition/mmi/interface-methods.md#mmi_newcamera) instead.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/HIDE = *h*</span> | Hides (*h* = 1) or shows (*h* = 0, default) the window. |
| <span class="table-cell-nowrap">/HOST = *hcSpec*</span> | Embeds the new camera window in the host window or subwindow specified by *hcSpec*. The host window or subwindow must be a control panel or a graph. |
|  | When identifying a subwindow with *hcSpec*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/K = *k*</span> | Specifies window behavior when the user attempts to close it. |
|  |<table class="nested-table"><tbody><tr><td>*k*&nbsp;=0:</td><td>Normal with dialog (default).</td></tr><tr><td>*k*&nbsp;=1:</td><td>Kills with no dialog.</td></tr><tr><td>*k*&nbsp;=2:</td><td>Disables killing.</td></tr><tr><td>*k*&nbsp;=3:</td><td>Hides the window.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/N = *name*</span> | Requests that the created camera window have the specified name, if it is not in use. If it is in use, then *name*0, *name*1, etc. are tried until an unused window name is found. |
|  | If you omit /N, NewCamera uses a name like Camera0. |
|  | NewCamera sets S_name to the chosen name. |
| <span class="table-cell-nowrap">/S = *n*</span> | Selects camera *n* from the sequence of available cameras on the current machine. *n* is zero-based. See also the [GetCamera](/igorpro/commands/getcamera.md) availableCameras keyword. |
| <span class="table-cell-nowrap">/W = (*left*,*top*,*right*,*bottom*)</span> |  |
|  | Sets the window location. Coordinates are in points for top-level windows. |
|  | When used with the /HOST flag, the specified location coordinates can have one of two possible meanings: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>When all values are less than 1, coordinates are assumed to be fractional relative to the host frame size.</td></tr><tr><td>2.</td><td>When any value is greater than 1, coordinates are taken to be fixed locations measured in points, or [control panel units](/igorpro/user-interface/controls.md#control-panel-units) for control panel hosts, relative to the top left corner of the host frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Suppress errors. If present, NewCamera sets V_Flag to 0 if the operation succeeded or to a non-zero error code. In the event of an error, it creates the window as if the operation succeeded but with a small missing camera indicator. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">hardwareName = *hwName*</span> | Selects the hardware camera using the full camera name. *hwName* is the camera's description. See also the [GetCamera](/igorpro/commands/getcamera.md) availableCameras keyword. |

### *Details* {#details}
If you have a single camera connected to your computer you can display live video by simply executing NewCamera without any flags or keywords.

You can control a camera window like other Igor target windows, using MoveWindow, SetWindow, etc.

If you have more than one camera connected to your computer you can specify the camera using its hardware name via the hardwareName keyword or using its zero-based sequence number using the /S flag.

Igor saves camera windows saved with the experiment and opens them live mode if you have a matching camera connected to the computer on which you open the experiment. If you do not have a matching camera, Igor still displays the camera window with a missing camera indicator.

Camera settings are not saved with the experiment.

### *Output Variables* {#output-variables}
NewCamera sets the following output variables:


|  |  |
| --- | --- |
| V_flag | 0 if the operation succeeded or a non-zero error code. |
| S_name | The name of the new camera window. |

### *See Also* {#see-also}
[GetCamera](/igorpro/commands/getcamera.md), [ModifyCamera](/igorpro/commands/modifycamera.md), [MMI - Overview](/igorpro/extensions/data-acquisition/mmi/mmi-overview.md)