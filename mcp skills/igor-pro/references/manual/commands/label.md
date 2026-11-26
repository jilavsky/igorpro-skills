---
description: "The Label operation labels the named axis with labelStr. axisName is the name of an existing axis in the top graph."
slug: /commands/label
---

<div className="command-signature">

## <strong>Label</strong>  [/W=<em>winName</em> /Z] <em>axisName</em>, <em>labelStr</em> {#label}

</div>

The Label operation labels the named axis with *labelStr*.

### *Parameters* {#parameters}
*axisName* is the name of an existing axis in the top graph. It is usually one of "left", "right", "top", or "bottom", though it may also be the name of a free axis such as "VertCrossing".

*labelStr* contains the text that labels the axis.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Adds axis label in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/Z</span> | No errors generated if the named axis doesn't exist. Used for style macros. |

### *Details* {#details}
*labelStr* can contain escape codes which affect subsequent characters in the text. An escape code is introduced by a backslash character. In a literal string, you must enter two backslashes to produce one. See [Backslashes in Annotation Escape Sequences](/igorpro/graphing/annotations.md#backslashes-in-annotation-escape-sequences) for details.

Using escape codes you can change the font, size, style and color of text, create superscripts and subscripts, create dynamically-updated text, insert legend symbols, and apply other effects. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details.

Some escape codes insert text based on axis properties. See [Axis Label Escape Codes](/igorpro/graphing/annotations.md#axis-label-escape-codes) for details.

The characters "<??>" in an axis label indicate that you specified an invalid escape code or used a font that is not available.

### *See Also* {#see-also}
[Axis Labels](/igorpro/graphing/graphs.md#axis-labels), [Escape Sequences in Strings](/igorpro/programming/commands.md#escape-sequences-in-strings), [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes), [Legend](/igorpro/commands/legend.md)ions[Legend] about wave symbols.

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)