---
description: "This structure is passed to action procedures for listbox controls created using the ListBox operation."
slug: /programming/structures/wmlistboxaction
---

## WMListboxAction {#wmlistboxaction}

This structure is passed to action procedures for listbox controls created using the [ListBox](/igorpro/user-interface/controls.md#listbox) operation.


```igor
Structure WMListboxAction
   char ctrlName[MAX_OBJ_NAME+1] // Control name
   char win[MAX_WIN_PATH+1]      // Host window or subwindow name
   STRUCT Rect winRect           // Local coordinates of host window
   STRUCT Rect ctrlRect          // Enclosing rectangle of the control
   STRUCT Point mouseLoc         // Mouse location
   Int32 eventCode               // See details below
   Int32 eventMod                // See Control Structure eventMod Field
   String userData               // Primary unnamed user data
   Int32 blockReentry            // Obsolete, see Control Structure blockReentry Field
   Int32 eventCode2              // Obsolete
   Int32 row                     // Selection row. See details below.
   Int32 col                     // Selection column. See details below.
   WAVE/T listWave               // List wave specified by ListBox command
   WAVE selWave                  // Selection wave specified by ListBox command
   WAVE colorWave                // Color wave specified by ListBox command
   WAVE/T titleWave              // Title wave specified by ListBox command
EndStructure
```

The constants used to specify the size of structure char arrays are internal to Igor Pro and may change.

### *WMListboxAction eventCode Field* {#wmlistboxaction-eventcode-field}

Your action function should test the eventCode field and respond only to documented eventCode values because other event codes may be added in the future.

The event code passed to the listbox action procedure has the following meaning:


| Event Code | Event |
| --- | --- |
| -3 | Control received keyboard focus (Igor 8 or later) |
| -2 | Control lost keyboard focus (Igor 8 or later) |
| -1 | Control being killed |
| 1 | Mouse down |
| 2 | Mouse up |
| 3 | Double click |
| 4 | Cell selection (mouse or arrow keys) |
| 5 | Cell selection plus Shift key |
| 6 | Begin edit |
| 7 | End edit |
| 8 | Vertical scroll |
|  | See *Scroll Event Warnings* under [ListBox](/igorpro/user-interface/controls.md#listbox) |
| 9 | Horizontal scroll by user or by the hScroll=*h*  keyword |
| 10 | Top row set by row=*r*  or first column set by col=*c*  keywords |
| 11 | Column divider resized |
| 12 | Keystroke, character code is place in row field |
|  | See *Note on Keystroke Event* under [ListBox](/igorpro/user-interface/controls.md#listbox) |
| 13 | Checkbox was clicked. This event is sent after selWave is updated. |

### *WMListboxAction row and col Fields* {#wmlistboxaction-row-and-col-fields}

The row field is the zero-based row number of the first selected row in the list or -1 if the selection is in title area. If an event occurs in the empty space below the last row, the row field is set to the number of rows in the list which is one greater than the row number of the last row. A mouse down event in an empty list reports row=0.

The col field is the column number of the selection.

The meanings of row and col are different for eventCodes 8 through 11:


|  |  |  |
| --- | --- | --- |
| Code | row | col |
| 8 | Top visible row | Horizontal shift in pixels. |
| 9 | Top visible row | Horizontal shift (user scroll). |
| 9 | -1 | Horizontal shift (hScroll keyword). |
| 10 | Top visible row | -1 (row keyword). |
| 10 | -1 | First visible col (col keyword). |
| 11 | Column shift | Column resized by user. |

If eventCode is 11, row is the horizontal shift in pixels of the column col that was resized, not the total horizontal shift of the list as reported in V_horizScroll by [ControlInfo](/igorpro/commands/controlinfo.md). If row is negative, the divider was moved to the left. col=0 corresponds to adjusting the divider on the right side of the first column. Use ControlInfo to get a list of all column widths.

### *Selection Events 4 and 5* {#selection-events-4-and-5}

These events are sent when a click on the Listbox could result in a change in selection. If it is important to you to respond only when the selection actually changes, you will need to keep track of the selection yourself.

These events are not sent if the list is empty.