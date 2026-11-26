---
description: "See Tooltip Hook Functions for further explanation of WMTooltipHookStruct."
slug: /programming/structures/wmtooltiphookstruct
---

## WMTooltipHookStruct {#wmtooltiphookstruct}

See [Tooltip Hook Functions](/igorpro/advanced-topics.md#tooltip-hook-functions) for further explanation of WMTooltipHookStruct.


```igor
Structure WMTooltipHookStruct
   char winName[MAX_WIN_PATH+1]     // Host window name or subwindow path
   double ticks                     // Tick count when event happened
   STRUCT Rect winRect              // Local coordinates of the window or subwindow
   STRUCT Point mouseLoc            // Mouse location
   STRUCT Rect trackRect            // Tooltip tracking rect
   double duration_ms;              // Time to display the tooltip, in milliseconds
   char traceName[MAX_OBJ_NAME+1]   // If in a graph window, name of the trace
   char imageName[MAX_OBJ_NAME+1]   // If in a graph window, name of the image
   waveHndl yWave                   // Y wave for trace, image, or table column
   double row                       // Row in trace, image or wave
   double column                    // Column in trace, image or wave
   double layer                     // Layer in trace, image or wave
   double chunk                     // Chunk in trace, image or wave
   char ctrlName[MAX_OBJ_NAME+1]    // Name of the control during hover event
   Int32 isHtml                     // Set to indicate tooltip contains HTML tags
   String tooltip                   // Set this to your tooltip text
EndStructure
```