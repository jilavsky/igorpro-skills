---
description: "The ExportGizmo operation is obsolete but is still supported for partial backward compatibility."
slug: /commands/exportgizmo
---

<div className="command-signature">

## <strong>ExportGizmo</strong>  [<em>flags</em>] <em>keyword</em> [=<em>value</em>] {#exportgizmo}

</div>

The ExportGizmo operation is obsolete but is still supported for partial backward compatibility.

You can export Gizmo graphics using File→Save Graphics which generates a SavePICT command. The ExportGizmo operation is only partially supported. It can export to the clipboard or to an Igor wave and it can print but it can no longer export to a file. Use [SavePICT](/igorpro/commands/savepict.md) instead.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = *gizmoName*</span> | Specifies the name of the targeted Gizmo window. If you omit /N then ExportGizmo operates on the top Gizmo window. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Saves the file into folder specified by *pathName*, which is the name of an existing symbolic path. |
| <span class="table-cell-nowrap">/Z</span> | Suppress errors. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| clip | Copy the current image to the clipboard. The copy is performed at the current resolution factor and saved in TIFF format. |
| EPS | EPS is no longer supported for Gizmo windows. |
| PDF | PDF is no longer supported for Gizmo windows. |
| print | Prints the Gizmo window on the default printer without displaying a print dialog. |
| <span class="table-cell-nowrap">wave = *wName*</span> | Saves the current image using 1x resolution as the 3D image wave specified by *wName*. The Gizmo window must be visible. If the Gizmo image contains any transparency the resulting wave is an unsigned byte 4-layer RGBA wave. Otherwise the wave is an unsigned byte 3-layer RGB wave. |

### *See Also* {#see-also}
[3D Graphics](/igorpro/graphing/3d-graphics.md)

[ModifyGizmo](/igorpro/commands/modifygizmo.md), [NewGizmo](/igorpro/commands/newgizmo.md), [AppendToGizmo](/igorpro/commands/appendtogizmo.md), [GetGizmo](/igorpro/commands/getgizmo.md), [GizmoInfo](/igorpro/commands/gizmoinfo.md), [RemoveFromGizmo](/igorpro/commands/removefromgizmo.md)