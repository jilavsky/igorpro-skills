---
description: "The CsrInfo function returns a keyword-value pair list of information about the specified cursor (cursorName is A through J) in the top graph or graph…"
slug: /commands/csrinfo
---

<div className="command-signature">

## <strong>CsrInfo</strong> (<em>cursorName</em>  [, <em>graphNameStr</em> ]) {#csrinfo}

</div>

The CsrInfo function returns a keyword-value pair list of information about the specified cursor (*cursorName* is A through J) in the top graph or graph specified by *graphNameStr*. It returns "" if the cursor is not in the graph.

### *Details* {#details}
The returned string contains information about the cursor in the following format:


```
TNAME:traceName; ISFREE:freeNum;POINT:xPointNumber;
[YPOINT:yPointNumber;] RECREATION:command;
```

The *traceName* value is the name of the graph trace or image to which it is attached or which supplies the x (and y) values even if the cursor isn't attached to it.

If `TNAME` is empty, fields `POINT`, `ISFREE`, and `YPOINT` are not present.

The *freeNum* value is 1 if the cursor is not attached to anything, 0 if attached to a trace or image.

The POINT value is the same value [pcsr](/igorpro/commands/pcsr.md) returns.

The YPOINT keyword and value are present only when the cursor is attached to a two-dimensional item such as an image, contour, or waterfall plot or when the cursor is free. Its value is the same as returned by [qcsr](/igorpro/commands/qcsr.md).

If cursor is free, POINT and YPOINT values are fractional relative positions (see description in the Cursor command).

The RECREATION keyword contains the Cursor commands (including /W) necessary to regenerate the current settings.

### *Examples* {#examples}

```igor
Variable aExists= strlen(CsrInfo(A)) > 0	// A is a name, not a string
Variable bIsFree= NumberByKey("ISFREE",CsrInfo(B,"Graph0"))
```

### *See Also* {#see-also}
[Programming With Cursors](/igorpro/graphing/graphs.md#programming-with-cursors)

[Cursors - Moving Cursor Calls Function](/igorpro/advanced-topics.md#cursors-moving-cursor-calls-function)

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)