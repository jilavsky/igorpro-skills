---
description: "The RemoveFromGizmo operation removes the specified object from the specified list and optionally performs an update."
slug: /commands/removefromgizmo
---

<div className="command-signature">

## <strong>RemoveFromGizmo</strong>  [<em>flags</em>][<em>keyword</em> = <em>value</em>] {#removefromgizmo}

</div>

The RemoveFromGizmo operation removes the specified object from the specified list and optionally performs an update.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = *gizmoName*</span> | Apply the command to a specific Gizmo window. |
| <span class="table-cell-nowrap">/U = *mode*</span> | Determines if an update is performed. |
|  |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>Performs a silent update mostly during idle events.</td></tr><tr><td>*mode*=1:</td><td>Checks if any object needs updating or if the rotation changed and updates only if necessary.</td></tr><tr><td>*mode*=2:</td><td>Forces immediate update that includes reloading all the waves, finding the minima and maxima, computing their scale factors and redrawing the associated objects.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">attribute = *attrName*</span> | Removes an attribute specified by *attrName* from the attribute list. |
|  | Removing an attribute from the attribute list also removes all instances of the attribute in the object list and display list. |
| <span class="table-cell-nowrap">displayItem = *dispName*</span> | Removes the named display list item. If the item is an object, all its instances are removed from the display list but it is not removed from the object list. |
| <span class="table-cell-nowrap">displayItemNumber = *n*</span> | Removes zero-based item number *n*  from the display list. |
| <span class="table-cell-nowrap">object = *objName*</span> | Removes the named object from the object list. |
|  | Removing an item from the object list also removes all instances of the item from the display list. |

### *See Also* {#see-also}
[3D Graphics](/igorpro/graphing/3d-graphics.md), [NewGizmo](/igorpro/commands/newgizmo.md), [ModifyGizmo](/igorpro/commands/modifygizmo.md), [AppendToGizmo](/igorpro/commands/appendtogizmo.md), [ExportGizmo](/igorpro/commands/exportgizmo.md), [GetGizmo](/igorpro/commands/getgizmo.md), [GizmoInfo](/igorpro/commands/gizmoinfo.md)