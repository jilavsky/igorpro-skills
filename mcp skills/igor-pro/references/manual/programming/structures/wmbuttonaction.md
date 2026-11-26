---
description: "This structure is passed to action procedures for button controls created using the Button operation."
slug: /programming/structures/wmbuttonaction
---

## WMButtonAction {#wmbuttonaction}

This structure is passed to action procedures for button controls created using the [Button](/igorpro/commands/button.md) operation.


```igor
Structure WMButtonAction
   char ctrlName[MAX_OBJ_NAME+1] // Control name
   char win[MAX_WIN_PATH+1]      // Host window or subwindow name
   STRUCT Rect winRect           // Local coordinates of host window
   STRUCT Rect ctrlRect          // Enclosing rectangle of the control
   STRUCT Point mouseLoc         // Mouse location
   Int32 eventCode               // See details below
   Int32 eventMod                // See 'Control Structure eventMod' Field
   String userData               // Primary unnamed user data.
   Int32 blockReentry            // Obsolete, see 'Control Structure blockReentry' Field
EndStructure
```

The constants used to specify the size of structure char arrays are internal to Igor Pro and may change.

### *WMButtonAction eventCode Field* {#wmbuttonaction-eventcode-field}

Your action function should test the eventCode field and respond only to documented eventCode values because other event codes may be added in the future.

The event code passed to the button action procedure has the following meaning:


| Event Code | Meaning |
| --- | --- |
| -3 | Control received keyboard focus (Igor 8 or later) |
| -2 | Control lost keyboard focus (Igor 8 or later) |
| -1 | Control being killed |
| 1 | Mouse down |
| 2 | Mouse up |
| 3 | Mouse up outside control |
| 4 | Mouse moved |
| 5 | Mouse enter |
| 6 | Mouse leave |
| 7 | Mouse dragged while outside the control |

Events 2 and 3 happen only after event 1.

Events 4, 5, and 6 happen only when the mouse is over the control but happen regardless of the mouse button state.

Event 7 happens only when the mouse is pressed inside the control and then dragged outside.