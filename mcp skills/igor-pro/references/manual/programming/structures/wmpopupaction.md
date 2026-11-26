---
description: "This structure is passed to action procedures for popup menu controls created using the PopupMenu operation."
slug: /programming/structures/wmpopupaction
---

## WMPopupAction {#wmpopupaction}

This structure is passed to action procedures for popup menu controls created using the [PopupMenu](/igorpro/commands/popupmenu.md) operation.


```igor
Structure WMPopupAction
   char ctrlName[MAX_OBJ_NAME+1] // Control name
   char win[MAX_WIN_PATH+1]      // Host window or subwindow name
   STRUCT Rect winRect           // Local coordinates of host window
   STRUCT Rect ctrlRect          // Enclosing rectangle of the control
   STRUCT Point mouseLoc         // Mouse location
   Int32 eventCode               // See details below
   Int32 eventMod                // See 'Control Structure eventMod' Field
   String userData               // Primary unnamed user data
   Int32 blockReentry            // Obsolete, see 'Control Structure blockReentry' Field
   Int32 popNum                  // Item number currently selected or hovered over (1-based)
   char popStr[MAXCMDLEN]        // Contents of current popup item or item hovered over
EndStructure
```

The constants used to specify the size of structure char arrays are internal to Igor Pro and may change.

### *WMPopupAction eventCode Field* {#wmpopupaction-eventcode-field}

Your action function should test the eventCode field and respond only to documented eventCode values because other event codes may be added in the future.

The event code passed to the pop-up menu action procedure has the following meaning:


| Event Code | Event |
| --- | --- |
| -3 | Control received keyboard focus (Igor 8 or later) |
| -2 | Control lost keyboard focus (Igor 8 or later) |
| -1 | Control being killed |
| 2 | Mouse up |
| 3 | Hovering - sent when the user highlights a menu item by moving the mouse cursor over it but has not selected it |
| 4 | Dismissed - sent when the user closes the menu without making a selection. This is primarily of use in conjunction with the hover event; it allows you to undo any changes made during a hover event when the menu is dismissed. This event code was added in Igor Pro 9.00. |