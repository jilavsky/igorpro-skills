---
description: "See Named Window Hook Functions for further explanation of WMWinHookStruct."
slug: /programming/structures/wmwinhookstruct
---

## WMWinHookStruct {#wmwinhookstruct}

See [Named Window Hook Functions](/igorpro/advanced-topics.md#named-window-hook-functions) for further explanation of WMWinHookStruct.


```igor
Structure WMWinHookStruct
   char winName[MAX_WIN_PATH+1]     // Host window or subwindow name
   STRUCT Rect winRect              // Local coordinates of the affected (sub)window
   STRUCT Point mouseLoc            // Mouse location
   Variable ticks                   // Tick count when event happened
   Int32 eventCode                  // See 'Named Window Hook Events'
   char eventName[MAX_OBJ_NAME+1]   // See 'Named Window Hook Events'
   Int32 eventMod                   // See 'Control Structure eventMod' Field
   char menuName[255+1]             // Name of the menu item as for SetIgorMenuMode
   char menuItem[255+1]             // Text of the menu item as for SetIgorMenuMode
   char traceName[MAX_OBJ_NAME+1]   // See 'Named Window Hook Functions'
   char cursorName[2]               // Cursor name A through J
   Variable pointNumber             // See 'Named Window Hook Functions'
   Variable yPointNumber            // See 'Named Window Hook Functions'
   Int32 isFree                     // 1 if the cursor is not attached to anything
   Int32 keycode                    // ASCII value of key struck
   Int32 specialKeyCode             // See Keyboard Events - Igor Pro 7 or later
   char keyText[16]                 // UTF-8 string representing key struck - Igor Pro 7 or later
   char oldWinName[MAX_OBJ_NAME+1]  // Simple name of the window or subwindow
   Int32 doSetCursor                // Set to 1 to change cursor to cursorCode
   Int32 cursorCode                 // See 'Setting the Mouse Cursor'
   Variable wheelDx                 // Vertical lines to scroll
   Variable wheelDy                 // Horizontal lines to scroll
   char focusCtrl[MAX_WIN_PATH+1]   // Added in Igor Pro 9.00. See EarlyKeyboard Events.
                                    // for event 27 to 29 related to wave drag and drop
   String droppedWaves              // Added in Igor Pro 10.00. See 'Named Window Hook Events'
   Int32 PLPageNumber               // Added in Igor Pro 10.00. See 'Named Window Hook Events'
   String PLObjectName              // Added in Igor Pro 10.00. See 'Named Window Hook Events'
   String PLObjectType              // Added in Igor Pro 10.00. See 'Named Window Hook Events'
   Int32 PLObjectIndex              // Added in Igor Pro 10.00. See 'Named Window Hook Events'
EndStructure
```