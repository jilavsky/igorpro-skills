---
description: "This structure is passed to action procedures for custom controls created using the CustomControl operation."
slug: /programming/structures/wmcustomcontrolaction
---

## WMCustomControlAction {#wmcustomcontrolaction}

This structure is passed to action procedures for custom controls created using the [CustomControl](/igorpro/user-interface/controls.md#customcontrol) operation.


```igor
Structure WMCustomControlAction
   char ctrlName[MAX_OBJ_NAME+1]    // Control name
   char win[MAX_WIN_PATH+1]         // Host window or subwindow name
   STRUCT Rect winRect              // Local coordinates of host window
   STRUCT Rect ctrlRect             // Enclosing rectangle of the control
   STRUCT Point mouseLoc            // Mouse location
   Int32 eventCode                  // See details below
   Int32 eventMod                   // See Control Structure eventMod Field
   String userData                  // Primary unnamed user data
   Int32 blockReentry               // Obsolete, see Control Structure blockReentry Field
   Int32 missedEvents               // TRUE when events occurred but the user
	                                 // function was not available for action
   Int32 mode                       // General purpose

   // Used only when eventCode==kCCE_frame
   Int32 curFrame                   // Input and output

   // Used when eventCode is kCCE_mousemoved, kCCE_mouseenter or kCCE_mouseleave
   Int32 needAction                 // See below for details

   // These fields are valid only with value=varName
   Int32 isVariable                 // TRUE if varName is a variable (numeric or string)
   Int32 isWave                     // TRUE if varName referenced a wave
   Int32 isString                   // TRUE if varName is a String type
   NVAR nVal                        // Valid if isVariable and not isString
   SVAR sVal                        // Valid if isVariable and isString
   WAVE nWave                       // Valid if isWave and not isString
   WAVE/T sWave                     // Valid if isWave and isString
   Int32 rowIndex                   // Valid if isWave, this is the row index unless rowLabel is not empty
   char rowLabel[MAX_OBJ_NAME+1]    // Wave row label

   // These fields are valid only when eventCode==kCCE_char
   Int32 kbChar                     // Keyboard key character code
                                    // This field cannot represent non-ASCII text such as accented characters. Use keyText instead.
   Int32 specialKeyCode             // See Keyboard Events - Added in Igor Pro 7
   char keyText[16]                 // UTF-8 string representing key struck - Added in Igor Pro 7
   Int32 kbMods                     // Keyboard key modifiers bit field. See details below.
EndStructure
```

The constants used to specify the size of structure char arrays are internal to Igor Pro and may change.

### *WMCustomControlAction eventCode Field* {#wmcustomcontrolaction-eventcode-field}

When determining the state of the eventCode member in the WMCustomControlAction structure, the various values you use are listed in the following table. You can define the kCCE symbolic constants by adding this to your procedure file:


```igor
#include <CustomControl Definitions>
```


| Event Code | Description |
| --- | --- |
| <span class="table-cell-nowrap">kCCE_mousedown = 1</span> | Mouse down in control. |
| <span class="table-cell-nowrap">kCCE_mouseup = 2</span> | Mouse up in control. |
| <span class="table-cell-nowrap">kCCE_mouseup_out = 3</span> | Mouse up outside control. |
| <span class="table-cell-nowrap">kCCE_mousemoved = 4</span> | Mouse moved (happens only when mouse is over the control). |
| <span class="table-cell-nowrap">kCCE_enter = 5</span> | Mouse entered control. |
| <span class="table-cell-nowrap">kCCE_leave = 6</span> | Mouse left control. |
| <span class="table-cell-nowrap">kCCE_mouseDraggedOutside = 7</span> | The mouse moved while it was outside the control. This event is delivered only after the mouse is pressed inside the control and dragged outside. While the mouse is inside the control, kCCE_mousemoved is delivered whether the mouse button is up or down. |
| <span class="table-cell-nowrap">kCCE_draw = 10</span> | Time to draw custom content. |
| <span class="table-cell-nowrap">kCCE_mode = 11</span> | Sent when executing CustomControl *name*, mode=*m*. |
| <span class="table-cell-nowrap">kCCE_frame = 12</span> | Sent before drawing a subframe of a custom picture. |
| <span class="table-cell-nowrap">kCCE_dispose = 13</span> | Sent as the control is killed. |
| <span class="table-cell-nowrap">kCCE_modernize = 14</span> | Sent when dependency (variable or wave set by value=*varName* parameter) fires. It will also get draw events, which probably don't need a response. |
| <span class="table-cell-nowrap">kCCE_tab = 15</span> | Sent when user tabs into the control. If you want keystrokes (kCCE_char), then set needAction. |
| <span class="table-cell-nowrap">kCCE_char = 16</span> | Sent on keyboard events. Stores the keyboard character in kbChar and modifiers bit field is stored in kbMods. Sets needAction if key event was used and requires a redraw. |
| <span class="table-cell-nowrap">kCCE_drawOSBM = 17</span> | Called after drawing *pict* from picture parameter into an offscreen bitmap. You can draw custom content here. |
| <span class="table-cell-nowrap">kCCE_idle = 18</span> | Idle event typically used to blink insertion points etc. Set needAction to force the control to redraw. Sent only when the host window is topmost. |

**WMCustomControl needAction Field**

The meaning of needAction depends on the event.

Events kCCE_mousemoved, kCCE_enter, kCCE_leave, and kCCE_mouseDraggedOutside set needAction to TRUE to force redraw, which is normally not done for these events.

Events kCCE_tab and kCCE_mousedown set needAction to TRUE to request keyboard focus (and get kCCE_char events).

Event kCCE_idle sets needAction to TRUE to request redraw.

**WMCustomControl kbMods Field**

Bit 0:	Not supported.

Bit 1:	Shift

Bit 2:	Alpha Lock. Not supported in Igor 7 or later.

Bit 3:	Alt

Bit 4:	Windows key