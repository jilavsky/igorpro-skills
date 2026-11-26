---
description: "The GizmoInfo function is used to determine if a particular name is valid and unique as a Gizmo item names."
slug: /commands/gizmoinfo
---

<div className="command-signature">

## <strong>GizmoInfo</strong> (<em>nameStr</em>, <em>key</em>) {#gizmoinfo}

</div>

The GizmoInfo function is used to determine if a particular name is valid and unique as a Gizmo item names.

GizmoInfo works on the top Gizmo window. In the presence of group objects, the function provides information on the current group object as set by ModifyGizmo currentGroupObject.

### *Parameters* {#parameters}
*nameStr* contains the name that we want to test for validity.

*key* is one of the following:

|  |  |
| --- | --- |
| 0: | Attribute name |
| 1: | Object name |
| 2: | Display item name |

### *Details* {#details}
The function returns one of the following values:


|  |  |
| --- | --- |
| -1: | *nameStr* is invalid or if the key is invalid |
| 0: | *nameStr* is conflicts with another Gizmo name |
| 1: | *nameStr* is unique and valid |

### *See Also* {#see-also}
[3D Graphics](/igorpro/graphing/3d-graphics.md)

[ModifyGizmo](/igorpro/commands/modifygizmo.md), [NewGizmo](/igorpro/commands/newgizmo.md), [AppendToGizmo](/igorpro/commands/appendtogizmo.md), [ExportGizmo](/igorpro/commands/exportgizmo.md), [GetGizmo](/igorpro/commands/getgizmo.md), [RemoveFromGizmo](/igorpro/commands/removefromgizmo.md)