---
description: "The TraceFromPixel function returns a string based on an attempt to hit test the provided X and Y coordinates."
slug: /commands/tracefrompixel
---

<div className="command-signature">

## <strong>TraceFromPixel</strong> (<em>xpixel</em>, <em>ypixel</em>, <em>optionsString</em>) {#tracefrompixel}

</div>

The TraceFromPixel function returns a string based on an attempt to hit test the provided X and Y coordinates. Used to determine if the mouse was clicked on a trace in a graph.

When a trace is found, TraceFromPixel returns a string containing the following `KEY:value;` pairs:

TRACE:*tracename*

HITPOINT:*pnt*

*tracename* will be quoted if necessary and may contain instance notation. *pnt* is the point number index into the trace's wave when the hit was detected. If a trace is not found near the coordinate point, a zero length string is returned.

### *Parameters* {#parameters}
*xpixel* and *ypixel* are the X and Y pixel coordinates.

*optionsString* can contain the following:

WINDOW:*winName*;

PREF:*traceName*;

ONLY:*traceName*;

DELTAX:*dx*;DELTAY:*dy*;

Use the `WINDOW` option to hit test in a graph other than the top graph. Use the `ONLY` option to search only for a special target trace. If the `PREF` option is used then the search will start with the specified trace but if no hit is detected, it will go on to the others.

When identifying a subwindow with WINDOW:*winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The `DELTAX` and `DELTAY` values must both be specified to alter the region that Igor searches for traces. The *dx* and *dy* values are in pixels and the region searched is the rectangle from *xpixel* -*dx* to *xpixel* +*dx* and *ypixel* -*dy* to *ypixel* +*dy*.

If `DELTAX` or `DELTAY` are omitted, the search region depends on whether `PREF` or `ONLY` are specified. If either are specified then Igor first searches for the trace using *dx = 3* and *dy = 3*. If the trace is not identified, Igor searches again using *dx = 6* and *dy = 6*. If the trace is still not identified, Igor gives up and returns a zero-length result string.

If neither `PREF` nor `ONLY` are specified then Igor uses tries 3, 6, 12, and 24 for *dx* and *dy* until it finds a trace or gives up and returns a zero-length result string.

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

[NumberByKey](/igorpro/commands/numberbykey.md), [StringByKey](/igorpro/commands/stringbykey.md), [AxisValFromPixel](/igorpro/commands/axisvalfrompixel.md), [PixelFromAxisVal](/igorpro/commands/pixelfromaxisval.md)