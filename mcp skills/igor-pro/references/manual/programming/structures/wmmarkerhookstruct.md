---
description: "See Custom Marker Hook Functions for further explanation of WMMarkerHookStruct."
slug: /programming/structures/wmmarkerhookstruct
---

## WMMarkerHookStruct {#wmmarkerhookstruct}

See [Custom Marker Hook Functions](/igorpro/advanced-topics.md#custom-marker-hook-functions) for further explanation of WMMarkerHookStruct.


```igor
Structure WMMarkerHookStruct
   Int32 usage                         // 0 = normal draw, 1 = legend draw
   Int32 marker                        // Marker number minus start
   float x, y                          // Location of desired center of marker
   float size                          // Half width/height of marker
   Int32 opaque                        // 1 if marker should be opaque
   float penThick                      // Stroke width
   STRUCT RGBColor mrkRGB              // Fill color
   STRUCT RGBColor eraseRGB            // Background color
   STRUCT RGBColor penRGB              // Stroke color
   WAVE ywave                          // Trace's y wave
   double ywIndex                      // Point number on ywave where marker is being drawn
   char winName[MAX_HostChildSpec+1]   // Full path to window or subwindow. Added in Igor Pro 9.00.
   char traceName[MAX_OBJ_INST+1]      // Full name of trace or "" if no trace. Added in Igor Pro 9.00.
EndStructure
```