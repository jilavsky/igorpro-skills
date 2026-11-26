---
description: "The SetAxis operation sets the extent (or \"range\") of the named axis. axisName is usually \"left\", \"right\", \"top\", or \"bottom\", but it can also be the name of…"
slug: /commands/setaxis
---

<div className="command-signature">

## <strong>SetAxis</strong>  [/W=<em>winName</em> /A[=<em>a</em> ]/E=<em>z</em> /N=<em>n</em> /R/Z] <em>axisName</em> [, <em>num1</em>, <em>num2</em> ] {#setaxis}

</div>

The SetAxis operation sets the extent (or "range") of the named axis.

### *Parameters* {#parameters}
*axisName* is usually "left", "right", "top", or "bottom", but it can also be the name of a free axis, such as "vertCrossing".

If *axisName* is a vertical axis such as "left" or "right" then *num1* sets the bottom end of the axis and *num2* sets the top end of the axis.

If *axisName* is a horizontal axis such as "top" or "bottom" then *num1* sets the left end of the axis and *num2* sets the right end of the axis.

You can flip the graph by reversing *num1* and *num2* (or by using /A/R). This is particularly useful for images, because Igor plots an image inverted.

If you pass * (asterisk) for *num1* and/or *num2* then the corresponding end of the axis will be autoscaled.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A[ = *a* ]</span> | Autoscale axis (when used, *num1*, *num2* should be omitted). |
|  |<table class="nested-table"><tbody><tr><td>*a*&nbsp;=0:</td><td>No autoscale. Same as no /A flag.</td></tr><tr><td>*a*&nbsp;=1:</td><td>Normal autoscale. Same as /A.</td></tr><tr><td>*a*&nbsp;=2:</td><td>Autoscale Y axis to a subset of the data defined by the current X axis range.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/E = *z*</span> | Sets the treatment of zero when the axis is in autoscale mode. |
|  |<table class="nested-table"><tbody><tr><td>*z*&nbsp;=0:</td><td>Normal mode where zero is not treated special.</td></tr><tr><td>*z*&nbsp;=1:</td><td>forces the smaller end of the axis to be set to zero (autoscale from zero).</td></tr><tr><td>*z*&nbsp;=2:</td><td>Axis is symmetric about zero.</td></tr><tr><td>*z*&nbsp;=3:</td><td>If the data is unipolar (all positive or all negative), this behaves like /E=1 (autoscale from zero). If the data is bipolar, it behaves like /E=0 (normal autoscaling).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/N = *n*</span> | Sets the algorithm for autoscaling the axis. |
|  |<table class="nested-table"><tbody><tr><td>*n*&nbsp;=0:</td><td>Normal mode which sets the axis limits equal to the data limits.</td></tr><tr><td>*n*&nbsp;=1:</td><td>Tries to pick nice values for the axis limits.</td></tr><tr><td>*n*&nbsp;=2:</td><td>Picks nice values, but also ensures that the data is inset from the ends of the axis.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/R</span> | Reverses the autoscaled axis (smaller values at the left for horizontal axes, at the top for vertical axes) when used with /A. Although it only has an effect for autoscale, it can be used with nonautoscale version of SetAxis so that the next time the Axis Range tab is used the "reverse axis" check box will already be set. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Sets axes in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate error if the named axis doesn't exist. Used for style macros. |