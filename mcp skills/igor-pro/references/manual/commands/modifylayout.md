---
description: "The ModifyLayout operation modifies objects in the top layout or in the layout specified by the /W flag."
slug: /commands/modifylayout
---

<div className="command-signature">

## <strong>ModifyLayout</strong>  [/W=<em>winName</em> /I/M/Z] [<em>bgRGB</em>=(<em>r</em>,<em>g</em>,<em>b</em>[,<em>a</em>]), <em>columns</em>(<em>obj</em>)=<em>c</em>, <em>fidelity</em>(<em>obj</em>)=<em>f</em>, <em>frame</em>(<em>obj</em>)=<em>f</em>, <em>height</em>(<em>obj</em>)=<em>h</em>,  <em>left</em>(<em>obj</em>)=<em>l</em>, <em>mag</em>=<em>m</em>, <em>rows</em>(<em>obj</em>)=<em>r</em>, <em>top</em>(<em>obj</em>)=<em>t</em>, <em>trans</em>(<em>obj</em>)=<em>t</em>,  <em>units</em>=<em>u</em>, <em>width</em>(<em>obj</em>)=<em>w</em>] {#modifylayout}

</div>

The ModifyLayout operation modifies objects in the top layout or in the layout specified by the /W flag.

### *Parameters* {#parameters}
Each parameter has the syntax:

*key* [(*objectName* )] = *value*

Each *key* parameter may take an optional *objectName* enclosed in parentheses. If "(*objectName*)" is omitted, all objects in the layout are affected.

Though not shown in the syntax, the optional "(*objectName*)" may be replaced with "[*objectIndex* ]", where *objectIndex* is zero or a positive integer denoting the object to be modified. "[0]" denotes the first object appended to the layout, "[1]" denotes the second object , etc. This syntax is used for style macros, in conjunction with the /Z flag.

The parameter descriptions below omit the optional "(*objectName*)".

The "units", "mag", and "bgRGB" keywords apply to the layout as a whole, not to a specific object and do not accept an *objectName*.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">bgRGB = *(r,g,b*[,*a*]*)*</span> | Specifies the background color for the layout. *r*, *g,* *b,* and *a* specify the the color and optional opacity as [RGBA Values](/igorpro/programming/commands.md#rgba-values). |
| <span class="table-cell-nowrap">columns = *c*</span> | Specifies the number of columns for a table object. |
| fidelity=*f* |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>Low fidelity.</td></tr><tr><td>*f*&nbsp;=1:</td><td>High fidelity.</td></tr></tbody></table>
| frame=*f* |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>No frame.</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single frame.</td></tr><tr><td>*f*&nbsp;=2:</td><td>Double frame.</td></tr><tr><td>*f*&nbsp;=3:</td><td>Triple frame.</td></tr><tr><td>*f*&nbsp;=4:</td><td>Shadow frame.</td></tr></tbody></table>
| gradient | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| gradientExtra | See [Gradient Fills](/igorpro/graphing/making-figures/graphics.md#gradient-fills) for parameters and details. |
| <span class="table-cell-nowrap">height = *h*</span> | Sets the height of the object. |
| <span class="table-cell-nowrap">left = *l*</span> | *l* is the horizontal coordinate of the left edge of the object relative to the left edge of the paper. |
| <span class="table-cell-nowrap">mag = *m*</span> | Sets the on screen layout magnification where *m* is a value between 0.05 and 10. |
|  | *m*=1 corresponds to 100%. |
|  | Factors of two, such as *m*=.25, *m*=.5, *m*=1, and *m*=2, tend to produce the best on screen graphics. |
| <span class="table-cell-nowrap">rows = *r*</span> | Specifies the number of rows for table object. |
| <span class="table-cell-nowrap">top = *t*</span> | *t* is the vertical coordinate of the top edge of the object relative to the top edge of the paper. |
| trans=*t* |<table class="nested-table"><tbody><tr><td>*t*&nbsp;=0:</td><td>Opaque (default).</td></tr><tr><td>*t*&nbsp;=1:</td><td>Transparent.</td></tr></tbody></table>
|  | For trans =1 to be effective, the object itself must also be transparent. Annotations have their own transparent/opaque settings. Graphs are transparent only if their backgrounds are white. PICTs may have been created transparent or opaque, and Igor cannot make an opaque PICT transparent. |
| <span class="table-cell-nowrap">units = *u*</span> | Sets dimension units in the layout info panel and in the Modify Objects dialog. |
|  |<table class="nested-table"><tbody><tr><td>*u*&nbsp;=0:</td><td>Points.</td></tr><tr><td>*u*&nbsp;=1:</td><td>Inches.</td></tr><tr><td>*u*&nbsp;=2:</td><td>Centimeters.</td></tr></tbody></table>
| <span class="table-cell-nowrap">width = *w*</span> | Sets the object width. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Dimensions in inches. |
| <span class="table-cell-nowrap">/M</span> | Dimensions in centimeters. |
| <span class="table-cell-nowrap">/W = *winName*</span> | *winName* is the name of the page layout window to be modified. If /W is omitted or if *winName* is $"", the top page layout is modified. |
| <span class="table-cell-nowrap">/Z</span> | Does not generate an error if the indexed or named object does not exist in a style macro. |

The /I and /M flags affect the units of the parameters for the left, top, width and height keywords only. If neither /I nor /M is present then the parameters for the left, top, width and height keywords are points.

### *Details* {#details}
Note that the units keyword affects only the units used in the layout info panel and in the Modify Objects dialog. It has nothing to do with the units used for the left, top, width and height keywords. Those units are points unless the /I or /M flags is present.

### *See Also* {#see-also}
[NewLayout](/igorpro/commands/newlayout.md), [AppendLayoutObject](/igorpro/commands/appendlayoutobject.md), [RemoveLayoutObjects](/igorpro/commands/removelayoutobjects.md), [LayoutPageAction](/igorpro/commands/layoutpageaction.md)