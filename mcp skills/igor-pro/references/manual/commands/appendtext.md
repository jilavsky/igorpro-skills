---
description: "The AppendText operation appends a carriage return and textStr to the most recently created annotation, or to the named annotation in the target or named…"
slug: /commands/appendtext
---

<div className="command-signature">

## <strong>AppendText</strong>  [/W=<em>winName</em> /N=<em>name</em> /NOCR[=<em>n</em> ]] <em>textStr</em> {#appendtext}

</div>

The AppendText operation appends a carriage return and *textStr*  to the most recently created annotation, or to the named annotation in the target or named graph or layout window. Annotations include tags, textboxes, color scales, and legends.

### *Parameters* {#parameters}
*textStr*  can contain escape codes to control font, font size and other stylistic variations. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = *name*</span> | Appends *textStr*  to the named tag or textbox. |
| <span class="table-cell-nowrap">/NOCR[ = *n* ]</span> | Omits the initial appending of a carriage return (allows a long line to be created with multiple AppendText commands). /NOCR=0 is the same as not specifying /NOCR at all, and /NOCR=1 is the same as just /NOCR. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to an annotation in the named graph or layout window or subwindow. Without /W, AppendText appends to an annotation in the topmost graph or layout window or subwindow. This must be the first flag specified when AppendText is used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
A textbox, tag, or legend can have at most 100 lines. A color scale can have at most one line, and this line is the color scale's main axis label.

### *See Also* {#see-also}
[Tag](/igorpro/commands/tag.md), [TextBox](/igorpro/commands/textbox.md), [ColorScale](/igorpro/commands/colorscale.md), [Legend](/igorpro/commands/legend.md), [ReplaceText](/igorpro/commands/replacetext.md), [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes)