---
description: "The Tag operation puts a tag on the target or named graph window or subwindow."
slug: /commands/tag
---

<div className="command-signature">

## <strong>Tag</strong>  [<em>flags</em>] [<em>taggedObjectName</em>, <em>xAttach</em>  [, <em>textStr</em> ]] {#tag}

</div>

The Tag operation puts a tag on the target or named graph window or subwindow. A tag is an annotation that is attached to a particular point on a trace, image, waterfall plot, or axis in a graph.

The Tag operation can be invoked in several ways as illustrated by these examples:


```igor
// Make a wave and a graph
Make wave0 = sin(x/8); Display wave0

// Tag command with all optional parameters included
Tag/N=tag0 wave0, 0, "Point 0 on wave0" // Add a tag to a trace

// Tag command with all optional parameters omitted
Tag/C/N=tag0/F=0                        // Change frame using /F flag

// Tag command with optional text parameter omitted
Tag/C/N=tag0 wave0, 50                  // Change the tagged point
```

*taggedObjectName* and *xAttach* can be omitted only when changing an existing tag using Tag/C/N=\<tag name\>. *textStr* can be included only if *taggedObjectName* and *xAttach* are included.

### *Parameters* {#parameters}
*taggedObjectName* is a trace, image or axis name which identifies the object to which the tag is to be attached. The name can be optionally followed by the # character and an instance number to distinguish multiple trace or image instances of the same wave. An axis name can be one of the standard axis names (bottom, top, left, or right) or a user-defined free axis name.

The *taggedObjectName* parameter is a name so, if you have a string variable containing the name, you must precede the string variable name with the $ operator.

*xAttach* identifies the point on the trace, image, or axis, to which the tag is to be attached. See ***xAttach Parameter*** below for details.

*textStr* is the text that is to appear in the tag.

### *xAttach Parameter* {#xattach-parameter}
*xAttach* identifies the point on the trace, image, or axis, to which the tag is to be attached.

For a trace tag, *xAttach* is the X wave scaling value of the attachment point.

For an image tag, *xAttach* is the X index in terms of the image wave's X scaling of the wave element to be tagged treating the wave as if it were 1D.

For a horizontal axis tag, *xAttach* is the X axis value of the point on the axis to which the tag is to be attached. Specifying NaN for *xAttach* centers the tag on the axis.

For a vertical axis tag, *xAttach* is the Y axis value of the point on the axis to which the tag is to be attached. Specifying NaN for *xAttach* centers the tag on the axis.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *anchorCode*</span> | *anchorCode* = LT for left top, LC for left center, LB for left bottom, MT for mid top, MC for mid center (the default), MB for mid bottom, RT for right top, RC for right center, RB for right bottom. |
|  | *anchorCode* is a literal, not a string. |
|  | The anchor point is on the tag itself. Any line or arrow drawn from the tag to the wave starts at the tag's anchor point. The anchor point also determines the precise spot on the tag which represents its position. |
| <span class="table-cell-nowrap">/AO = *ao*</span> | Sets the text's auto-orientation mode. A non-zero *a0* value overrides the /O value. |
|  | /AO is for trace tags only. Setting /AO for any other kind of annotation has no effect. |
|  | An auto-oriented tag's text rotates whenever it is redrawn, usually when the underlying data changes, the graph is resized, or when the tag is attached to a new point. |
|  | The values for *a0* are: |
|  |<table class="nested-table"><tbody><tr><td>*ao*&nbsp;=0:</td><td>No auto-orientation. Use the /O value (default).</td></tr><tr><td>*ao*&nbsp;=1:</td><td>Tangent to the trace line at the attachment point.</td></tr><tr><td>*ao*&nbsp;=2:</td><td>Tangent to the trace line, snaps to vertical or horizontal if within 2 degrees of vertical or horizontal.</td></tr><tr><td>*ao*&nbsp;=3:</td><td>Perpendicular to the trace line.</td></tr><tr><td>*ao*&nbsp;=4:</td><td>Perpendicular to the trace line, snaps to vertical or horizontal if within 2 degrees of vertical or horizontal.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/AXS[ = *isAxisTag*]</span> | Specifies that *taggedObjectName* is to be interpreted as an axis name. This is useful when the axis name is the same as one of the graph's trace or image instance names. /AXS is the same as /AXS=1. The /AXS flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/B = (*r*,*g*,*b*[,*a*])</span> | Sets color of the tag's background. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| /B=*b* |<table class="nested-table"><tbody><tr><td>*b*&nbsp;=0:</td><td>Opaque background.</td></tr><tr><td>*b*&nbsp;=1:</td><td>Transparent background.</td></tr><tr><td>*b*&nbsp;=2:</td><td>Same background as the graph plot area background.</td></tr><tr><td>*b*&nbsp;=3:</td><td>Same background as the window background.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/C</span> | Changes the existing tag. |
| /F=*frame* |<table class="nested-table"><tbody><tr><td>*frame*&nbsp;=0:</td><td>No frame.</td></tr><tr><td>*frame*&nbsp;=1:</td><td>Underline frame.</td></tr><tr><td>*frame*&nbsp;=2:</td><td>Box frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/G = (*r*,*g*,*b*[,*a*])</span> | Sets color of the text in the tag. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">/H = *legendSymbolWidth*</span> |  |
|  | *legendSymbolWidth* sets width of the legend symbol (the sample line or marker) in points. Use 0 for the default, automatic width. |
| /I=*i* |<table class="nested-table"><tbody><tr><td>*i*&nbsp;=0:</td><td>Tag will always be visible. If it is &quot;off screen&quot;, it appears at the extreme edge of the graph.</td></tr><tr><td>*i*&nbsp;=1:</td><td>Tag will be invisible if it is &quot;off screen&quot;. &quot;Off screen&quot; means that its attachment point or any part of the tag&#39;s text is off screen. This is esthetically pleasing but gives you nothing to grab if you want to drag the tag back on screen.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/IMG[ = *isImageTag*]</span> | Specifies that *taggedObjectName* is to be interpreted as an image instance name. This is useful when the image instance name is the same as one of the graph's trace instance names or one of the axis names. /IMG is the same as /IMG=1. The /IMG flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/K</span> | Kills existing tag. |
| /L=*line* |<table class="nested-table"><tbody><tr><td>*line*&nbsp;=0:</td><td>No line from tag to attachment point.</td></tr><tr><td>*line*&nbsp;=1:</td><td>Line connecting tag to attachment point.</td></tr><tr><td>*line*&nbsp;=2:</td><td>Line with arrow pointing from tag to attachment point.</td></tr><tr><td>*line*&nbsp;=3:</td><td>Line with arrow pointing from attachment point to tag.</td></tr><tr><td>*line*&nbsp;=4:</td><td>Line with arrows at both ends.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/LS = *linespace*</span> | Specifies a tweak to the normal line spacing where *linespace* is points of extra (plus or minus) line spacing. For negative values, a blank line may be necessary to avoid clipping the bottom of the last line. |
| <span class="table-cell-nowrap">/M[ = *sameSize* ]</span> | /M or /M=1 specifies that legend markers should be the same size as the marker in the graph. |
|  | /M=0 turns same-size mode off so that the size of the marker in the legend is based on text size. |
| <span class="table-cell-nowrap">/N = *name*</span> | Specifies name of the tag to create or change. |
| <span class="table-cell-nowrap">/O = *rot*</span> | Sets the text's rotation. *rot* is in (integer) degrees, counterclockwise and must be a number from -360 to  360. |
|  | 0 is normal horizontal left-to-right text, 90 is vertical bottom-to-top text. |
|  | If the tag is attached to a trace (not an image or axis), any non-zero /AO value will overwrite this rotation value. |
| <span class="table-cell-nowrap">/P = *tipOffset*</span> | *tipOffset* sets the offset from the tip of a tag's line or arrow to the point on the wave that it is tagging. *tipOffset* is a positive number from 0 to 200 in points. If *tipOffset*=0 (the default), Igor automatically chooses an appropriate offset. |
| <span class="table-cell-nowrap">/Q[ = *contourInstance*]</span> | Associates a tag with a particular contour level trace in a graph recreation macro. Of interest mainly to hard-core Igor programmers. |
|  | When "=*contourInstance*" is present, /Q associates the tag with the contour wave. Igor will feel free to change or delete the tag, as appropriate, when it recalculates the contour (because you changed the contour data or appearance, the graph size or the axis range). *contourInstance* is a contour instance name, such as zWave or zWave#1 if you have the same wave contoured twice in the graph. |
|  | /Q by itself, with "=*contourInstance*" not present, disassociates the tag from the contour wave. Igor will no longer modify or delete the tag (unless the contour level to which it is attached is deleted). If you manually tweak a contour label, using the Modify Annotation dialog, Igor uses this flag. |
| <span class="table-cell-nowrap">/R = *newName*</span> | Renames the tag. |
| /S=*style* |<table class="nested-table"><tbody><tr><td>*style*&nbsp;=0:</td><td>Single frame.</td></tr><tr><td>*style*&nbsp;=1:</td><td>Double frame.</td></tr><tr><td>*style*&nbsp;=2:</td><td>Triple frame.</td></tr><tr><td>*style*&nbsp;=3:</td><td>Shadow frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/T = *tabSpec*</span> | *tabSpec* is a single number in points, such as /T=72, for evenly spaced tabs or a list of tab stops in points such as /T={50, 150, 225}. |
| <span class="table-cell-nowrap">/TL = *extLineSpec*</span> | Specifies extended tag line parameters similar to the [SetDrawEnv](/igorpro/commands/setdrawenv.md) arrow settings. |
|  | *extLineSpec*= {*keyword* = *value*, ...} or zero to turn off all extended specifications. |
|  | Valid *keyword* -*value* pairs are: |
|  |<table class="nested-table"><tbody><tr><td>len=*l*</td><td>Length of arrow head in points (*l* =0 for auto).</td></tr><tr><td>fat=*f*</td><td>Width to length ratio of arrow head (default is 0.5 same as *f* =0).</td></tr><tr><td>style=*s*</td><td>Sets barb side mode (see [SetDrawEnv](/igorpro/commands/setdrawenv.md) astyle for values).</td></tr><tr><td>sharp=*s*</td><td>Sets sharpness between -1 and 1 (default is 0; blunt).</td></tr><tr><td>frame=*f*</td><td>Sets frame thickness in outline mode.</td></tr><tr><td>lThick=*l*</td><td>Sets line thickness in points (default is 0.5 for *l* =0).</td></tr><tr><td>lineRGB=(*r*,*g*,*b*[,*a*])</td><td>Sets color for lines. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). The default is opaque black.</td></tr><tr><td>dash=*d*</td><td>Specifies dash pattern number between 0 and 17 (see [SetDashPattern](/igorpro/commands/setdashpattern.md) for patterns).</td></tr></tbody></table>
| /V=*vis* |<table class="nested-table"><tbody><tr><td>*vis*&nbsp;=0:</td><td>Annotation is invisible, and cannot be selected. The annotation is still listed in [AnnotationList](/igorpro/commands/annotationlist.md).</td></tr><tr><td>*vis*&nbsp;=1:</td><td>Annotation is visible (the default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/W = *winName*</span> | Operates in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |
| <span class="table-cell-nowrap">/X = *xOffset*</span> | *xOffset* = distance from point to tag as % of graph width. For axis tags, the offsets are proportional to the size of the text used for the axis labels. |
| <span class="table-cell-nowrap">/Y = *yOffset*</span> | *yOffset* = distance from point to tag as % of graph height. For axis tags, the offsets are proportional to the size of the text used for the axis labels. |
| /Z=*freeze* |<table class="nested-table"><tbody><tr><td>*freeze*&nbsp;=0:</td><td>Unfreezes it.</td></tr><tr><td>*freeze*&nbsp;=1:</td><td>Freezes tag position (you can&#39;t move it with the mouse).</td></tr></tbody></table>

### *Details* {#details}
If the /C flag is used, it must be the first flag in the command (except that it may follow an initial /W) and must be followed immediately by the /N=*name* flag.

If the /K flag is used, it must be the first flag in the command and must be followed immediately by the /N=*name* flag with no further flags or parameters.

*taggedObjectName* and *xAttach* can be omitted only when changing an existing tag using Tag/C/N=\<tag name\>. *textStr* can be included only if *taggedObjectName* and *xAttach* are included. This syntax allows changes to the tag to be made through the *flags* parameters without needing to respecify the other parameters. Similarly, the tag's attachment point can be changed without needing to respecify the *textStr* parameter.

A tag can have at most 100 lines.

*textStr* can contain escape codes which affect subsequent characters in the text. An escape code is introduced by a backslash character. In a literal string, you must enter two backslashes to produce one. See [Backslashes in Annotation Escape Sequences](/igorpro/graphing/annotations.md#backslashes-in-annotation-escape-sequences) for details.

Using escape codes you can change the font, size, style and color of text, create superscripts and subscripts, create dynamically-updated text, insert legend symbols, and apply other effects. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details.

"\\r" inserts a carriage-return character which starts a new line of text in the annotation.

Some escape codes insert text based on the wave point or axis to which a tag is attached. See [Tag Escape Codes](/igorpro/graphing/annotations.md#tag-escape-codes) and [Axis Label Escape Codes](/igorpro/graphing/annotations.md#axis-label-escape-codes) for details.

The characters "<??>" in a tag indicate that you specified an invalid escape code or used a font that is not available.

### *Examples* {#examples}
Following is an example of various ways in which axis tags can be used.


```igor
Make/O jack=sin(x/8)
SetScale x,0,14e9,"y" jack
Display jack
Label bottom "\\u#2"                       // turn off default axis label
ModifyGraph axOffset(bottom)=1.16667       // make room for tag (manual adustment)
Tag/N=axisTag0/F=0/A=MT/X=0.20/Y=-4.29/L=0 bottom, Nan, "\\JCTime (\\U)\rGratuitous 2nd line"

// Now tag a few important points
Tag/N=axisTag1/F=0/A=LB/X=1.20/Y=3.00 bottom, 0, "Big Bang"
Tag/N=axisTag2/F=0/A=MB/X=0.00/Y=2.86 bottom, 8000000000, "Earth formed"
Tag/N=axisTag3/F=0/A=RB/X=-0.80/Y=4.71 bottom, 13040000000, "Dinosaurs ruled"
```

### *See Also* {#see-also}
[TextBox](/igorpro/commands/textbox.md), [Legend](/igorpro/commands/legend.md), [AppendText](/igorpro/commands/appendtext.md), [AnnotationInfo](/igorpro/commands/annotationinfo.md), [AnnotationList](/igorpro/commands/annotationlist.md)

[TagVal](/igorpro/commands/tagval.md), [TagWaveRef](/igorpro/commands/tagwaveref.md)

[Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes)

[Label](/igorpro/commands/label.md), [Axis Labels](/igorpro/graphing/graphs.md#axis-labels)

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)