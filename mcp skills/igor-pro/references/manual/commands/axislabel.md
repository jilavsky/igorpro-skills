---
description: "The AxisLabel function returns a string containing the axis label for the named axis in the named graph window or subwindow."
slug: /commands/axislabel
---

<div className="command-signature">

## <strong>AxisLabel</strong> (<em>graphNameStr</em>, <em>axisNameStr</em> [, <em>escapeBackslashes</em>]) {#axislabel}

</div>

The AxisLabel function returns a string containing the axis label for the named axis in the named graph window or subwindow.  The string returned is suitable for use with the [Label](/igorpro/commands/label.md) operation. The AxisLabel function is primarily intended for copying the label from one axis to another.

The AxisLabel function was added in Igor Pro 9.00.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow via *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*axisNameStr* is the name of the axis.

*escapeBackslashes* is an optional parameter which defaults to 0 (false).

### *Details* {#details}
Specify *escapeBackslashes*=1 when using the result to create a command passed to the [Execute](/igorpro/commands/execute.md) operation. Otherwise omit *escapeBackslashes* or specify *escapeBackslashes*=0.

The "Axis Utilities.ipf" WaveMetrics procedure contains an AxisLabelText function that is very similar to AxisLabel. If you use AxisLabelText, you can replace it with AxisLabel for use with Igor Pro 9 or later.

### *Examples* {#examples}

```igor
// Label Graph0 left axis with something that has a backslash in it
Make/O data=x
Display/N=Graph0 data
Label/W=Graph0 left, "Area \\E (UV*Sec)"

// Reuse the left axis label from Graph0 for Graph1
Display/N=Graph1 data
String lblStr = AxisLabel("Graph0","left")
Label/W=Graph1 left, lblStr
```

### *See Also* {#see-also}
[AxisInfo](/igorpro/commands/axisinfo.md), [Label](/igorpro/commands/label.md), [Backslashes in Annotation Escape Sequences](/igorpro/graphing/annotations.md#backslashes-in-annotation-escape-sequences)