---
description: "See ModifyFreeAxis for further explanation of WMAxisHookStruct."
slug: /programming/structures/wmaxishookstruct
---

## WMAxisHookStruct {#wmaxishookstruct}

See [ModifyFreeAxis](/igorpro/commands/modifyfreeaxis.md) for further explanation of WMAxisHookStruct.


```igor
Structure WMAxisHookStruct
   char win[MAX_WIN_PATH+1]      // Host window or subwindow name
   char axName[MAX_OBJ_NAME+1]   // Name of axis
   char mastName[MAX_OBJ_NAME+1] // Name of controlling axis or ""
   char units[MAX_UNITS+1]       // Axis units
   Variable min                  // Current axis range minimum value
   Variable max                  // Current axis range maximum value
EndStructure
```