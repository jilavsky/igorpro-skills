---
description: "This structure is passed to action procedures for tab controls created using the TabControl operation."
slug: /programming/structures/wmtabcontrolaction
---

## WMTabControlAction {#wmtabcontrolaction}

This structure is passed to action procedures for tab controls created using the [TabControl](/igorpro/user-interface/controls.md#tabcontrol) operation.


```igor
Structure WMTabControlAction
   char ctrlName[MAX_OBJ_NAME+1]    // Control name
   char win[MAX_WIN_PATH+1]         // Host window or subwindow name
   STRUCT Rect winRect              // Local coordinates of host window
   STRUCT Rect ctrlRect             // Enclosing rectangle of the control
   STRUCT Point mouseLoc            // Mouse location
   Int32 eventCode                  // See details below
   Int32 eventMod                   // See 'Control Structure eventMod' Field
   String userData                  // Primary unnamed user data
   Int32 blockReentry               // Obsolete, see 'Control Structure blockReentry' Field
   Int32 tab                        // Tab number
EndStructure
```

The constants used to specify the size of structure char arrays are internal to Igor Pro and may change.

**WMTabControlAction eventCode Field**

Your action function should test the eventCode field and respond only to documented eventCode values because other event codes may be added in the future.

The event code passed to tab control action procedure has the following meaning:


| Event Code | Meaning |
| --- | --- |
| -3 | Control received keyboard focus (Igor 8 or later) |
| -2 | Control lost keyboard focus (Igor 8 or later) |
| -1 | Control being killed |
| 2 | Mouse up |