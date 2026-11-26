---
description: "The PrintGraphs operation prints one or more graphs. PrintGraphs prints one or more graphs on a single page from the command line or from a procedure."
slug: /commands/printgraphs
---

<div className="command-signature">

## <strong>PrintGraphs</strong>  [ <em>flags</em> ] <em>graphSpec</em>  [, <em>graphSpec</em> ]... {#printgraphs}

</div>

The PrintGraphs operation prints one or more graphs.

PrintGraphs prints one or more graphs on a single page from the command line or from a procedure. The graphs can be overlaid or positioned any way you want.

### *Parameters* {#parameters}
The *graphSpec* specifies the name of a graph to print, the position of the graph on the page and some other options.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C = *num*</span> | Renders graphs in black and white (*num* =0) or in color (*num* =1; default). Does not affect the Print or Page Setup dialogs. |
| <span class="table-cell-nowrap">/D</span> | Disables high resolution printing. |
| This flag is no longer supported and has no effect. |  |
| <span class="table-cell-nowrap">/G = *grout*</span> | Specifies grout, the spacing between objects, for tiling in prevailing units. |
| <span class="table-cell-nowrap">/I</span> | Coordinates are in inches. |
| <span class="table-cell-nowrap">/M</span> | Coordinates are in centimeters. |
| <span class="table-cell-nowrap">/R</span> | Coordinates are in percent of page size (see example below). |
| <span class="table-cell-nowrap">/PD [ = *d* ]</span> | Displays print dialog. This allows the user to use Print Preview or to print to a file. |
|  | If present the /PD flag must be the first flag. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=0:</td><td>Default. Prints without displaying the Print dialog.</td></tr><tr><td>*d*&nbsp;=1:</td><td>Displays the Print dialog. /PD is equivalent to /PD=1.</td></tr><tr><td>*d*&nbsp;=2:</td><td>Displays the Print Preview dialog. Requires Igor Pro 7.00 or later.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/S</span> | Stacks graphs. |
| <span class="table-cell-nowrap">/T</span> | Tiles graphs. |

### *Details* {#details}
Graph coordinates are in inches (/I) or centimeters (/M) relative to the top left corner of the physical page. If none of these options is present, coordinates are assumed to be in points.

The form of a *graphSpec* is:


```igor
graphName [(left, top, right, bottom)] [/F=f ] [/T]
```

Here are some examples:


```igor
// Take size and position from window size and position.
PrintGraphs Graph0, Graph1
// Specify size and position explicitly.
PrintGraphs/I Graph0(1, 1, 6, 5)/F=1, Graph1(1, 6, 6, 10)/F=1
```

If the coordinates are missing and the /T or /S flags are present before *graphSpec* then the graphs are tiled or stacked. If the coordinates are missing but no /T or /S flags are present then the graph is sized and positioned based on its position on the desktop.

Finally there are these *graphSpec* options, which appear after the graph name:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F = *f*</span> | Specifies a frame around the graph. |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>No frame (default).</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single frame.</td></tr><tr><td>*f*&nbsp;=2:</td><td>Double frame.</td></tr><tr><td>*f*&nbsp;=3:</td><td>Triple frame.</td></tr><tr><td>*f*&nbsp;=4:</td><td>Shadow box frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/T</span> | Graph is transparent. This allows special effects when graphs are overlaid. |
|  | For this to be effective, the graph and its contents must also be transparent. Graphs are transparent only if their backgrounds are white. Annotations have their own transparent/opaque settings. PICTs may have been created transparent or opaque; an opaque PICT cannot be made transparent. |

You can put an entire *graphSpec* into a string variable and use the string variable in its place. In this case the name of the string variable must be preceded by the $ character. This is handy for printing from a procedure and also keeps the PrintGraphs command down to a reasonable number of characters. For example:


```igor
String spec0, spec1, spec2
spec0 = "Graph0(1, 1, 6, 5)/F=1"
spec1 = "Graph1(1, 6, 6, 10)/F=1"
spec2 = ""				// PrintGraphs will ignore spec2.
PrintGraphs/I $spec0, $spec1, $spec2
```

If you use a string for a *graphSpec* and that string contains no characters then PrintGraphs will ignore that *graphSpec*.

### *See Also* {#see-also}
[PrintSettings](/igorpro/commands/printsettings.md), [PrintTable](/igorpro/commands/printtable.md), [PrintLayout](/igorpro/commands/printlayout.md), [PrintNotebook](/igorpro/commands/printnotebook.md)