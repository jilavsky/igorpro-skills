---
description: "This structure is passed to action procedures for slider controls created using the Slider operation."
slug: /programming/structures/wmslideraction
---

## WMSliderAction {#wmslideraction}

This structure is passed to action procedures for slider controls created using the [Slider](/igorpro/commands/slider.md) operation.


```igor
Structure WMSliderAction
   char ctrlName[MAX_OBJ_NAME+1] // Control name
   char win[MAX_WIN_PATH+1]      // Host window or subwindow name
   STRUCT Rect winRect           // Local coordinates of host window
   STRUCT Rect ctrlRect          // Enclosing rectangle of the control
   STRUCT Point mouseLoc         // Mouse location
   Int32 eventCode               // See details below
   Int32 eventMod                // See 'Control Structure eventMod' Field
   String userData               // Primary unnamed user data
   Int32 blockReentry            // Obsolete, see 'Control Structure blockReentry' Field
   Variable curval               // Value of slider
EndStructure
```

The constants used to specify the size of structure char arrays are internal to Igor Pro and may change.

### *WMSliderAction eventCode Field* {#wmslideraction-eventcode-field}

Your action function should test the eventCode field and respond only to documented eventCode values because other event codes may be added in the future.

The event code passed to slider action procedure has the following meaning:


| Event Code | Event |
| --- | --- |
| -3 | Control received keyboard focus (Igor 8 or later) |
| -2 | Control lost keyboard focus (Igor 8 or later) |
| -1 | Control being killed |
| 1 | Value set |
| 2 | Mouse down |
| 4 | Mouse up |
| 8 | Mouse moved or arrow key moved the slider |
| 16 | Repeat timer fired (see [Repeating Sliders](/igorpro/user-interface/controls.md#repeating-sliders)) |

The event codes greater than zero are bits that may be combined in certain cases. For instance, if your slider does not have the live mode set, you may receive event code 5 = 1+4. This indicates that a mouse up event was detected, and that mouse up set the slider's value.

For a demo of many of these events, see [Handling Slider Events](/igorpro/user-interface/controls.md#handling-slider-events).