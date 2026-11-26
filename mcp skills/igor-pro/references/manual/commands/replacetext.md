---
description: "The ReplaceText operation replaces the text in the most recently created or changed annotation or in the annotation specified by /W=winName and/N=name."
slug: /commands/replacetext
---

<div className="command-signature">

## <strong>ReplaceText</strong>  [/N=<em>name</em> /W=<em>winName</em> ] <em>textStr</em> {#replacetext}

</div>

The ReplaceText operation replaces the text in the most recently created or changed annotation or in the annotation specified by /W=*winName* and/N=*name*.

### *Parameters* {#parameters}
*textStr*  can contain escape codes to control font, font size and other stylistic variations.

*textStr*  can contain escape codes to set the font, size, style, color and other properties. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details.

If the annotation is a color scale, this command replaces the text of the color scale's main axis label.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = *name*</span> | Replaces the text of the named tag or textbox. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Replaces text in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *See Also* {#see-also}
[Tag](/igorpro/commands/tag.md), [TextBox](/igorpro/commands/textbox.md), [ColorScale](/igorpro/commands/colorscale.md), [Legend](/igorpro/commands/legend.md), [AppendText](/igorpro/commands/appendtext.md), [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes)