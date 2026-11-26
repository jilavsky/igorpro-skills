---
description: "The GetGizmo operation provides information about a Gizmo display window."
slug: /commands/getgizmo
---

<div className="command-signature">

## <strong>GetGizmo</strong>  [/N/Z] <em>keyword</em> [=<em>value</em> ] {#getgizmo}

</div>

The GetGizmo operation provides information about a Gizmo display window.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/G = *groupSpec*</span> | Directs the operation to provide information about a specific Gizmo group object. /G was added in Igor Pro 7.00. |
|  | For top level groups *groupSpec* is a simple name, for example: |
|  | <code class="igor">GetGizmo /G=group0 displayNameList</code> |
|  | Address lower level groups like this: |
|  | <code class="igor">String groupSpecStr = "root:group0:group0A"&#10;GetGizmo /G=$groupSpecStr displayNameList</code> |
| <span class="table-cell-nowrap">/N = *gizmoName*</span> | Specifies the name of the targeted Gizmo window. If you omit /N then GetGizmo operates on the top Gizmo window. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| attributeList | Stores the attribute list recreation commands in S_AttributeList and in the text wave TW_AttributeList. The wave is always created, even if there are no attributes in the attribute list. This is useful if you want to test the contents of the attribute list without creating a full recreation macro. |
| <span class="table-cell-nowrap">attributeItemExists = *name*</span> |  |
|  | Determines if the named item exists in the attribute list. |
|  | Sets V_Flag to 1 if the named item exists in the attribute list or to 0 if it does not exist. |
| attributeNameList | Stores in the string S_AttributeNames a semicolon-separated list containing the names of all items in the attribute list. |
|  | To get the attribute name list of a group object you need to set the group object as the current group object using [ModifyGizmo](/igorpro/commands/modifygizmo.md) currentGroupObject. |
| axisCueState | Determines if the axis cue is displayed. |
|  | Sets V_Flag to 1 if the Gizmo display shows the axis cue or to 0 if not. |
|  | This applies to the built-in axis cue, not to free axis cue objects. |
| <span class="table-cell-nowrap">constant = *OpenGLconst*</span> |  |
|  | Prints to history area the decimal value of the OpenGL constant passed as a name. This is useful for conversion between OpenGL constant definitions as they appear in OpenGL documentation and numerical arguments used by Gizmo. For example: |
|  | <code class="igor">GetGizmo constant=GL_FRONT</code> |
|  | See [Use of GL Constants in Gizmo Commands](/igorpro/graphing/3d-graphics.md#use-of-gl-constants-in-gizmo-commands) for details. |
| curGroup | Stores in the string S_GroupName the path to the current group. Unlike ModifyGizmo currentGroupObject, the returned group path does not start with the Gizmo window name. |
|  | If the targeted Gizmo window is named Gizmo0, and the current group was set using |
|  | <code class="igor">ModifyGizmo currentGroupObject="Gizmo0:Group0:NestedGroup0"</code> |
|  | then S_GroupName is "Group0:NestedGroup0". |
| curMatrix | Stores the current homogeneous rotation matrix in the 4x4 single precision wave M_RotationMatrix in the current data folder. |
| curQuaternion | Stores the components of the current quaternion in the variables GizmoQuat_x, GizmoQuat_y, GizmoQuat_z, GizmoQuat_w. |
| curRotation | Stores the current Euler angles in degrees in the global variables GizmoEulerA, GizmoEulerB, and GizmoEulerC. |
| dataLimits | Creates the variables GizmoXmin, GizmoXmax, GizmoYmin, GizmoYmax, GizmoZmin, GizmoZmax which are set to the corresponding global data limits of all data objects currently displayed in the Gizmo window. See also [ModifyGizmo](/igorpro/commands/modifygizmo.md) hookFunction for another method to access the same data. |
| <span class="table-cell-nowrap">displayItemExists = *name*</span> |  |
|  | Determines if the named item is in the display list. |
|  | Sets V_Flag to 1 if the named item exists in the display list or to 0 if not. This is executed in the context of the current group. |
| displayList | Stores the display list recreation commands in S_DisplayList and in the text wave TW_DisplayList. This is useful if you want to test the contents of the display list without creating a full recreation macro. |
| displayNameList | Stores in the string S_DisplayNames a semicolon-separated list containing the names of all items in the display list. |
|  | To get the display name list of a group object you need to set the group object as the current group object using [ModifyGizmo](/igorpro/commands/modifygizmo.md) currentGroupObject. |
| gizmoName | Returns the name of the top Gizmo window in S_GizmoName. This is equivalent to: WinName(0,65536). |
| gizmoNameList | Stores in the string S_GizmoNames a semicolon-separated list containing the names of all Gizmo windows. This is equivalent to: |
|  | <code class="igor">WinList("*", ";", "WIN:65536")</code> |
| objectList | Stores the object list recreation commands in S_gizmoObjectList and in the text wave TW_gizmoObjectList. This is useful if you want to test the contents of the object list without creating a full recreation macro. |
| <span class="table-cell-nowrap">objectAttributeList = *name*</span> |  |
|  | Stores the string S_objectAttributeList and in the text wave TW_objectAttributeList a list of all embedded attributes of the object specified by *name* . |
| <span class="table-cell-nowrap">objectItemExists = *name*</span> |  |
|  | Determines if the named item is in the object list. |
|  | Sets V_Flag to 1 if the named item exists in the object list or to 0 if not. This is executed in the context of the current group. |
| objectNameList | Stores in the string S_ObjectNames a semicolon-separated list containing the names of all items in the object list. |
|  | To get the object name list of a group object you need to set the group object as the current group object using [ModifyGizmo](/igorpro/commands/modifygizmo.md) currentGroupObject. |
| mouseLockState | Determines if rotation of the Gizmo display with the mouse is locked. |
|  | Sets V_Flag to 1 if mouse rotation is locked or to 0 if not. |
| userBoxLimits | Returns the six parameter box limits as specified by the user - see [ModifyGizmo](/igorpro/commands/modifygizmo.md) setOuterBox. The parameters are stored in the variables GizmoBoxXmin, GizmoBoxXmax, GizmoBoxYmin, GizmoBoxYmax, GizmoBoxZmin, GizmoBoxZmax. |
| <span class="table-cell-nowrap">userString = *name*</span> | Sets the string S_GizmoUserString to the user string saved under the specified *name*. If there is no user string of the specified name, GetGizmo sets S_GizmoUserString to "". See [ModifyGizmo](/igorpro/commands/modifygizmo.md) userString. |
| viewport | Returns the width and height of the actual drawing region, in pixels, in the variables V_width and V_Height. This excludes the internal tool palette. |
| winPixels | Stores the global pixel coordinates of the window in the variables V_left, V_top, V_right, V_bottom. |

### *See Also* {#see-also}
[3D Graphics](/igorpro/graphing/3d-graphics.md)

[NewGizmo](/igorpro/commands/newgizmo.md), [ModifyGizmo](/igorpro/commands/modifygizmo.md), [AppendToGizmo](/igorpro/commands/appendtogizmo.md), [ExportGizmo](/igorpro/commands/exportgizmo.md), [GizmoInfo](/igorpro/commands/gizmoinfo.md), [RemoveFromGizmo](/igorpro/commands/removefromgizmo.md)