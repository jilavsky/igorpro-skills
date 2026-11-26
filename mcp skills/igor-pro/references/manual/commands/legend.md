---
description: "The Legend operation puts a legend on a graph or page layout. legendStr contains the text that is printed in the legend."
slug: /commands/legend
---

<div className="command-signature">

## <strong>Legend</strong>  [/A=<em>attach</em> /C/E[=<em>exterior</em>]/F=<em>frame</em> /H=<em>legendSymbolWidth</em> /H={<em>legendSymbolWidth</em>, <em>minThickness</em>, <em>maxThickness</em> } /J/K /M[=<em>saMeSize</em>]/N=<em>name</em> /R=<em>newName</em> /S=<em>style</em> /T=<em>tabSpec</em> /V=<em>vis</em> /W=<em>winName</em> /X=<em>xoffset</em> /Y=<em>yoffset</em> ] [<em>legendStr</em> ] {#legend}

</div>

The Legend operation puts a legend on a graph or page layout.

### *Parameters* {#parameters}
*legendStr* contains the text that is printed in the legend.

If *legendStr* is missing or is an empty string (""), the text needed for a default legend is automatically generated. Legends are automatically updated when waves are appended to or removed from the graph or when you rename a wave in the graph.

*legendStr* can contain escape codes which affect subsequent characters in the text. An escape code is introduced by a backslash character. In a literal string, you must enter two backslashes to produce one. See [Backslashes in Annotation Escape Sequences](/igorpro/graphing/annotations.md#backslashes-in-annotation-escape-sequences) for details.

Using escape codes you can change the font, size, style and color of text, create superscripts and subscripts, create dynamically-updated text, insert legend symbols, and apply other effects. See [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes) for details. However normally you leave it to Igor to automatically manage the legend.

See [Legend Text](/igorpro/graphing/annotations.md#legend-text) for a discussion of what *legendStr* may contain.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/H = *legendSymbolWidth*</span> |  |
|  | Sets the width in points of the area in which to draw the wave symbols. A value of 0 means "default". This results in a width that is based on the text size in effect when the symbol is drawn. A value of 36 gives a .5 inch (36 points) width which is nice in most cases. |
| <span class="table-cell-nowrap">/H = {*legendSymbolWidth*, *minThickness*, *maxThickness* }</span> |  |
|  | This is an additional form of the /H flag. The *legendSymbolWidth* parameter works the same as described above. |
|  | The *minThickness* and *maxThickness* parameters allow you to create a legend whose line and marker thicknesses are different from the thicknesses of the associated traces in the graph. This can be handy to make the legend more readable when you use very thin lines or markers for the traces. |
|  | *minThickness* and *maxThickness* are values from 0.0 to 10.0. Also, setting *minThickness* to 0.0 and *maxThickness* to 0.0 (the default setting) tells Igor to use the same thicknesses for the legend symbols as for the traces. |
| <span class="table-cell-nowrap">/J</span> | Disables the default legend mechanism so that a default legend is not created even if *legendStr* is an empty string ("") or omitted. |
|  | Window recreation macros use /J in case *legendStr* is too long to fit on the same command line as the Legend operation itself. In this case, an AppendText command appears after the Legend command to append *legendStr* to the empty legend. For really long values of *legendStr*, Igor might generate multiple AppendText commands. |
| /M[=*sameSize*] |<table class="nested-table"><tbody><tr><td>/M&nbsp;or&nbsp;/M=1:</td><td>Legend markers should be the same size as the marker in the graph.</td></tr><tr><td>/M=0:</td><td>Same-size mode off. The size of the marker in the legend is based on text size.</td></tr></tbody></table>

See the [TextBox](/igorpro/commands/textbox.md) operation for documentation for all other flags.

### *Details* {#details}
A legend can have at most 100 lines. We don't expect anyone to come even close.

### *Examples* {#examples}
The command `Legend` (with no parameters) creates a default legend. A default legend in a layout contains a line for each wave in each of the graphs in the layout, starting from the bottom graph and working toward the front.

The command:


```igor
Legend/C/N=name ""
```

changes the named existing legend to a default legend.

You can put a legend in a page layout with a command such as:


```igor
Legend "\s(Graph0.wave0) this is wave0"
```

This creates a legend in the layout that shows the symbol for wave0 in Graph0. The graph named in the command is usually in the layout but it doesn't have to be.

### *See Also* {#see-also}
[Legend Text](/igorpro/graphing/annotations.md#legend-text), [TextBox](/igorpro/commands/textbox.md), [Tag](/igorpro/commands/tag.md), [ColorScale](/igorpro/commands/colorscale.md), [AnnotationInfo](/igorpro/commands/annotationinfo.md), [AnnotationList](/igorpro/commands/annotationlist.md), [Annotation Escape Codes](/igorpro/graphing/annotations.md#annotation-escape-codes)

[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

[Color as f(z) Example](/igorpro/graphing/graphs.md#color-as-f-z-example) for a discussion of creating a legend whose symbols match the markers in a graph that uses color as f(z).