---
description: "The AnnotationInfo function returns a string containing a semicolon-separated list of information about the named annotation in the named graph or page layout…"
slug: /commands/annotationinfo
---

<div className="command-signature">

## <strong>AnnotationInfo</strong> (<em>winNameStr</em>, <em>annotationNameStr</em>  [, <em>options</em>  ] ) {#annotationinfo}

</div>

The AnnotationInfo function returns a string containing a semicolon-separated list of information about the named annotation in the named graph or page layout window or subwindow.

One application of AnnotationInfo is to use a tag or textbox as an input mechanism to a procedure. This is illustrated in the "Tags as Markers Demo" sample experiment, which includes handy utility functions (supplied by AnnotationInfo Procs.ipf) for working with AnnotationInfo.

### *Parameters* {#parameters}
*winNameStr* can be "" to refer to the top graph or layout window or subwindow. If the window does not exist, an error is raised and an empty string is returned.

When identifying a subwindow with *winNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*options* is an optional bitmask that controls the text formatting in the annotation output. The default value is 0.

Omit *options* or use 0 for *options* to escape the returned annotation text, which is appropriate for printing the output to the history or for using the text in an Execute operation.

Setting the 0x1 bit for *options* causes AnnotationInfo to not escape the returned annotation text because you intend to extract the text for use in a subsequent command such as Textbox or Tag.

In Igor 10 and later, setting bit 0x2 causes AnnotationInfo to return an empty string when the named annotation doesn't exist, instead of the usual behavior or returning a null string and raising an error.

### *Details* {#details}
The string contains multiple pieces of information. All but the last piece are prefaced by a keyword and colon and terminated with a semicolon. The last piece is the text of the annotation, which is prefaced with a keyword and a colon but is not terminated with a semicolon.


| Keyword | Information Following Keyword |
| --- | --- |
| ABSX | X location, in points, of the anchor point of the annotation. For graphs, this is relative to the top-left corner of the graph window. For layouts, it is relative to the top-left corner of the page. |
| ABSY | Y location, in points, of the anchor point of the annotation. For graphs, this is relative to the top-left corner of the graph window. For layouts, it is relative to the top-left corner of the page. |
| ATTACHX | For tags, it is the X value of the wave at the point where the tag is attached, as specified with the Tag operation. For textboxes, color scales, and legends, this will be zero and has no meaning. |
| AXISX | X location of the anchor point of the annotation. For tags or color scales in graphs, it is in terms of the X axis against which the tagged wave is plotted. For textboxes and legends in graphs, it is in terms of the first X axis. For layouts, this has no meaning and is always zero. |
| AXISY | Y location of the anchor point of the annotation. For tags or color scales in graphs, it is in terms of the Y axis against which the tagged wave is plotted. For textboxes and legends in graphs, it is in terms of the first Y axis. For layouts, this has no meaning and is always zero. |
| AXISZ | Z value of the image or contour level trace to which the tag is attached or NaN if the trace is not a contour level trace or the annotation is not a tag. |
| COLORSCALE | Parameters that would be used in a ColorScale operation to create the annotation. |
| FLAGS | Flags that would be used in a Tag, Textbox, ColorScale, or Legend operation to create the annotation. |
| RECT | Outermost corners of the annotation (values are in points): RECT:*left*, *top*, *right*, *bottom* |
| TEXT | Text that defines the contents of the annotation or the main axis label of a color scale. |
| TYPE | Annotation type: "Tag", "TextBox", "ColorScale", or "Legend". |
| XWAVE | For tags, it is the name of the X wave in the XY pair to which the tag is attached. If the tag is attached to a single wave rather than an XY pair, this will be empty. For textboxes, color scales, and legends, this will be empty and has no meaning. |
| XWAVEDF | For tags, the full path to the data folder containing the X wave associated with the trace to which the tag is attached. For textboxes, color scales, and legends, this will be empty and has no meaning. |
| YWAVE | For tags, it is the name of the trace or image to which the tag is attached. See [ModifyGraph](/igorpro/commands/modifygraph.md) (traces) for a discussion of trace names. For color scales, it is the name of the wave displayed in associated the contour plot, image plot, f(z) trace, or the name of the color scale's cindex wave. For textboxes and legends, this will be empty and has no meaning. |
| YWAVEDF | Full path to the data folder containing the Y wave or blank if the annotation is not a tag or color scale. |

### *Demos* {#demos}
[Open Tags as Markers Demo](#igor-pxp/Examples/Techniques/Tags__As__Markers.pxp)