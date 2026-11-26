---
description: "This structure is passed to action procedures for checkbox controls created using the Checkbox operation."
slug: /programming/structures/wmcheckboxaction
---

## WMCheckboxAction {#wmcheckboxaction}

This structure is passed to action procedures for checkbox controls created using the [Checkbox](/igorpro/commands/checkbox.md) operation.


```igor
Structure WMCheckboxAction
   char ctrlName[MAX_OBJ_NAME+1]    // Control name
   char win[MAX_WIN_PATH+1]         // Host window or subwindow name
   STRUCT Rect winRect              // Local coordinates of host window
   STRUCT Rect ctrlRect             // Enclosing rectangle of the control
   STRUCT Point mouseLoc            // Mouse location
   Int32 eventCode                  // See details below
   Int32 eventMod                   // See Control Structure eventMod Field
   String userData                  // Primary unnamed user data
   Int32 blockReentry               // Obsolete, see Control Structure blockReentry Field
   Int32 checked                    // Checkbox state
   char vName[MAX_OBJ_NAME+2 + (MAXDIMS * (MAX_OBJ_NAME+5)) + 1]	// Name of variable
   WAVE ckWave;                     // Valid if using wave
   Int32 rowIndex                   // Row index for a wave, if rowLabel is empty
   char rowLabel[MAX_OBJ_NAME+1]    // Wave row dimension label
   Int32 colIndex                   // Column index for a wave if colLabel is empty
   char colLabel[MAX_OBJ_NAME+1]    // Wave column dimension label
   Int32 layerIndex                 // Layer index for a wave if layerLabel is empty
   char layerLabel[MAX_OBJ_NAME+1]  // Wave layer dimension label
   Int32 chunkIndex                 // Chunk index for a wave if chunkLabel is empty
   char chunkLabel[MAX_OBJ_NAME+1]  // Wave chunk dimension label
EndStructure
```

The constants used to specify the size of structure char arrays are internal to Igor Pro and may change.

### *WMCheckboxAction eventCode Field* {#wmcheckboxaction-eventcode-field}

Your action function should test the eventCode field and respond only to documented eventCode values because other event codes may be added in the future.

The event code passed to the checkbox action procedure has the following meaning:


| Event Code | Meaning |
| --- | --- |
| -3 | Control received keyboard focus (Igor 8 or later) |
| -2 | Control lost keyboard focus (Igor 8 or later) |
| -1 | Control being killed |
| 2 | Mouse up, checkbox toggled |