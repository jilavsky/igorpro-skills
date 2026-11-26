---
description: "The TextBox operation puts a textbox on the target or named graph. A textbox is an annotation that is not associated with any particular trace."
slug: /commands/textbox
---

<div className="command-signature">

## <strong>TextBox</strong>  [/W=<em>winName</em> /A=<em>anchorCode</em> /B=(<em>r</em>,<em>g</em>,<em>b</em>[,<em>a</em>])/B=<em>trans</em> /C/D={<em>thickMult</em>  [, <em>shadowThick</em> [, <em>haloThick</em> ]]}/E[=<em>exterior</em> ] /F=<em>frame</em> /G=(<em>r</em>,<em>g</em>,<em>b</em>) /H=<em>legendSymbolWidth</em> /K/LS= <em>linespace</em> /M[=<em>saMeSize</em> ] /N=<em>name</em> /O=<em>rot</em> /R=<em>newName</em> /S=<em>style</em> /T=<em>tabSpec</em> /V=<em>vis</em> /X=<em>xOffset</em> /Y=<em>yOffset</em> /Z=<em>freeze</em> [<em>textStr</em> ] {#textbox}

</div>

The TextBox operation puts a textbox on the target or named graph. A textbox is an annotation that is not associated with any particular trace.

### *Parameters* {#parameters}
*textStr* is the text that is to appear in the textbox. It is optional.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *anchorCode*</span> | *anchorCode* = LT for left top, LC for left center, LB for left bottom, MT for mid top, MC for mid center, MB for mid bottom, RT for right top, RC for right center, RB for right bottom. |
|  | *anchorCode* is a literal, not a string. |
|  | For interior textboxes, the anchor point is on the rectangular edge of the plot area of the graph window (where the left, bottom, right, and top axes are drawn). |
|  | For exterior textboxes, the anchor point is on the rectangular edge of the entire graph window. |
| <span class="table-cell-nowrap">/B = (*r*,*g*,*b*[,*a*])</span> | Sets color of the textbox background. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| /B=*b* |<table class="nested-table"><tbody><tr><td>*b*&nbsp;=0:</td><td>Opaque background.</td></tr><tr><td>*b*&nbsp;=1:</td><td>Transparent background.</td></tr><tr><td>*b*&nbsp;=2:</td><td>Same background as the graph plot area background.</td></tr><tr><td>*b*&nbsp;=3:</td><td>Same background as the window background.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/C</span> | changes existing textbox. |
| <span class="table-cell-nowrap">/D = {*thickMult* [, *shadowThick* [, *haloThick*]]}</span> |  |
|  | *thickMult* multiplies the normal frame thickness of a textbox. The thickness may be set using just /D=*thickMult*. |
|  | *shadowThick*, if present, overrides Igor's normal shadow thickness. It is in units of fractional points. |
|  | *haloThick* governs the annotation's halo thickness (a surrounding band of the annotation's background color), which can vary from -1 to 10 points. |
|  | The default *haloThick* value is -1, which preserves the behavior of previous versions of Igor where the halo of all annotations was set by the global variable root:V_TBBufZone. Any negative value of haloThick (-0.5, for example) will be overridden by V_TBBufZone if it exists, otherwise the absolute value of *haloThick* will be used. A zero or positive value overrides V_TBBufZone. |
|  | Any of the parameters may be missing. To set *haloThick* to 0 without changing other parameters, use /D={,,0}. |
| <span class="table-cell-nowrap">/E[ = *exterior*]</span> | /E or /E=1 forces textbox (or legend) to be exterior to graph (provided *anchorCode* is not MC) and pushes the graph margins away from the anchor edge(s). /E=2 also forces exterior mode but does not push the margins. |
|  | /E=0 returns it to the default (an "interior textbox" which  can be anywhere in the graph window). |
| /F=*frame* |<table class="nested-table"><tbody><tr><td>*frame*&nbsp;=0:</td><td>No frame.</td></tr><tr><td>*frame*&nbsp;=1:</td><td>Underline frame.</td></tr><tr><td>*frame*&nbsp;=2:</td><td>Box frame (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/G = (*r*,*g*,*b*[,*a*])</span> | Sets color of the text in the textbox. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">/H = *legendSymbolWidth*</span> |  |
|  | Sets width of the legend symbol (the sample line or marker) in points. Use 0 for the default, automatic width. |
| <span class="table-cell-nowrap">/K</span> | Kills existing textbox. |
| <span class="table-cell-nowrap">/LS = *linespace*</span> | Specifies a tweak to the normal line spacing where *linespace* is points of extra (plus or minus) line spacing. For negative values, a blank line may be necessary to avoid clipping the bottom of the last line. |
| <span class="table-cell-nowrap">/M[ = *saMeSize*]</span> | /M or /M=1 specifies that legend markers should be the same size as the marker in the graph. |
|  | /M=0 turns same-size mode off so that the size of the marker in the legend is based on text size. |
| <span class="table-cell-nowrap">/N = *name*</span> | Specifies the name of the textbox to change or create. |
| <span class="table-cell-nowrap">/O = *rot*</span> | Sets the text's rotation in degrees counterclockwise. *rot* is a value from -360 to 360. |
|  | 0 is normal horizontal left-to-right text, 90 is vertical bottom-to-top text. |
| <span class="table-cell-nowrap">/R = *newName*</span> | Renames the textbox. |
| /S=*style* |<table class="nested-table"><tbody><tr><td>*style*&nbsp;=&nbsp;0:</td><td>Single frame.</td></tr><tr><td>*style*&nbsp;=&nbsp;1:</td><td>Double frame.</td></tr><tr><td>*style*&nbsp;=&nbsp;2:</td><td>Triple frame.</td></tr><tr><td>*style*&nbsp;=&nbsp;3:</td><td>Shadow frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/T = *tabSpec*</span> | *tabSpec* is a single number in points, such as /T=72, for evenly spaced tabs or a list of tab stops in points such as /T={50, 150, 225}. |
| /V=*vis* |<table class="nested-table"><tbody><tr><td>*vis*&nbsp;=0:</td><td>Annotation is invisible, and cannot be selected. The annotation is still listed in [AnnotationList](/igorpro/commands/annotationlist.md).</td></tr><tr><td>*vis*&nbsp;=1:</td><td>Annotation is visible (the default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = *winName*</span> | Operates in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/X = *xOffset*</span> | For interior textboxes *xOffset* is the distance from anchor to textbox as a percentage of the plot area width. |
|  | For exterior textboxes *xOffset* is the distance from anchor to textbox as a percentage of the graph window width. See /E and /A. |
| <span class="table-cell-nowrap">/Y = *yOffset*</span> | *yOffset* is the distance from anchor to textbox as a percentage of the plot area height (interior textboxes) or graph window height (exterior textboxes). See /E and /A. |
| /Z=*freeze* |<table class="nested-table"><tbody><tr><td>*freeze*&nbsp;=0:</td><td>Unfreezes it. Annotations are always unfrozen in page layouts.</td></tr><tr><td>*freeze*&nbsp;=1:</td><td>Freezes annotation position (you can&#39;t move it with the mouse). This works in graphs but is not implemented for page layouts.</td></tr></tbody></table>

### *Details* {#details}
Use the optional /W=*winName* flag to specify a specific graph or layout window. When used on the command line or in a Macro, Proc, or Window procedure, /W must precede all other flags.

If the /C flag is used, it must be the first flag in the command (except that it may follow an initial /W) and must be followed immediately by the /N=*name* flag.

If the /K flag is used, it must be the first flag in the command (or follow an initial /W) and must be followed immediately by the /N=*name* flag with no further flags or parameters.

*textStr* is optional. If missing, the textbox text is unchanged. This allows changes to the textbox to be made through the flags without changing the text.

A textbox can have at most 100 lines.

*textStr* can contain escape codes which affect subsequent characters in the text. An escape code is introduced by a backslash character. In a literal string, you must enter two backslashes to produce one. See [Backslashes in Annotation Escape Sequences](/igorpro/graphing/annotations.md#backslashes-in-annotation-escape-sequences) for details.

Using escape codes you can change the font, size, style and color of text, create superscripts and subscripts, create dynamically-updated text, insert legend symbols, and apply other effects. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details.

The characters "<??>" in a textbox indicate that you specified an invalid escape code or used a font that is not available.

### *Examples* {#examples}

```igor
TextBox/C/N=t1/X=25/Y=50
```

moves the textbox named t1 to the location defined by X=25 and Y=50.


```igor
TextBox/C/N=t1 "New Text"
```

changes the text for t1.

### *See Also* {#see-also}
[Tag](/igorpro/commands/tag.md), [Legend](/igorpro/commands/legend.md), [AppendText](/igorpro/commands/appendtext.md), [AnnotationInfo](/igorpro/commands/annotationinfo.md), [AnnotationList](/igorpro/commands/annotationlist.md)

[Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes)

See [printf](/igorpro/commands/printf.md) for formatting codes used in *formatStr*.

[Programming with Annotations](/igorpro/graphing/annotations.md#programming-with-annotations)

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)