---
description: "The GetKeyState function returns a bitwise numeric value that indicates the state of certain keyboard keys."
slug: /commands/getkeystate
---

<div className="command-signature">

## <strong>GetKeyState</strong> (<em>flags</em>) {#getkeystate}

</div>

The GetKeyState function returns a bitwise numeric value that indicates the state of certain keyboard keys.

To detect keyboard events directed toward a window that you have created, such as a panel window, use the window hook function instead of GetKeyState. See [Window Hook Functions](/igorpro/advanced-topics.md#window-hook-functions) for details.

GetKeyState is normally called from a procedure that is invoked directly through a user-defined button or user-defined menu item. The procedure tests the state of one or more modifier keys and adjusts its behavior accordingly.

Another use for GetKeyState is to determine if the escape key is pressed. This can be used to detect that the user wants to stop a procedure.

GetKeyState tests the keyboard at the time it is called. It does not tell you if keys were pressed between calls to the function. Consequently, when a procedure uses the escape key to break a loop, the user must hold the escape key pressed until the running procedure gets around to calling the function.

### *Parameters* {#parameters}
*flags* is a bitwise parameter interpreted as follows:


|  |  |
| --- | --- |
| Bit 0: | If set, GetKeyState reports keys keys even if Igor is not the active application. If cleared, GetKeyState reports keys only if Igor is the active application. |

All other bits are reserved and must be zero.

### *Details* {#details}
The return value is interpreted bitwise as follows:

|  |  |
| --- | --- |
| Bit 0: | Ctrl key pressed. |
| Bit 1: | Alt key pressed. |
| Bit 2: | Shift key pressed. |
| Bit 3: | Caps Lock key pressed. |
| Bit 4: | Not supported. |
| Bit 5: | Escape key pressed. |
| Bit 6: | Left arrow key pressed. Supported in Igor Pro 7.00 or later. |
| Bit 7: | Right arrow key pressed. Supported in Igor Pro 7.00 or later. |
| Bit 8: | Up arrow key pressed. Supported in Igor Pro 7.00 or later. |
| Bit 9: | Down arrow key pressed. Supported in Igor Pro 7.00 or later. |

To test if a particular key is pressed, do a bitwise AND of the return value with the mask value 1, 2, 4, 8, 16, 32, 64, 128, 256 and 512 for bits 0 through 9 respectively. To test if a particular key and only that key is pressed compare the return value with the mask value.

You can use GetKeyState to test for a modifier key when the user chooses a user-defined menu item or clicks a user-defined button using the mouse.

### *Examples* {#examples}

```igor
Function ShiftKeyExample()
	Variable keys = GetKeyState(0)

	if (keys == 0)
		Print "No modifier keys are pressed."
	endif

	if (keys & 4)
		if (keys == 4)
			Print "The Shift key and only the Shift key is pressed."
		else
			Print "The Shift key is pressed."
		endif
	endif
End

Function EscapeKeyExample()
	Variable keys

	do
		keys = GetKeyState(0)
		if ((keys & 32) != 0)	// User is pressing escape?
			break
		endif
	while(1)
End
```

### *See Also* {#see-also}
[Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters)