---
description: "See Gizmo Named Hook Functions for further explanation of WMGizmoHookStruct."
slug: /programming/structures/wmgizmohookstruct
---

## WMGizmoHookStruct {#wmgizmohookstruct}

See [Gizmo Named Hook Functions](/igorpro/graphing/3d-graphics.md#gizmo-named-hook-functions) for further explanation of WMGizmoHookStruct.


```igor
Structure WMGizmoHookStruct
	Int32 version
	char winName[MAX_HostChildSpec+1] // Full path to host window or subwindow
	char eventName[MAX_OBJ_NAME+1]
	Int32 width
	Int32 height
	Int32 mouseX
	Int32 mouseY
	Variable xmin
	Variable xmax
	Variable ymin
	Variable ymax
	Variable zmin
	Variable zmax
	Variable eulerA
	Variable eulerB
	Variable eulerC
	Variable wheelDx
	Variable wheelDy
EndStructure
```