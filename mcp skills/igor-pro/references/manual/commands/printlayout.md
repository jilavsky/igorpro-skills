---
description: "The PrintLayout operation prints the named page layout window. winName is the window name of the page layout to print."
slug: /commands/printlayout
---

<div className="command-signature">

## <strong>PrintLayout</strong>  [/C=<em>num</em> /D] <em>winName</em> {#printlayout}

</div>

The PrintLayout operation prints the named page layout window.

### *Parameters* {#parameters}
*winName*  is the window name of the page layout to print.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C = *num*</span> | Renders graphs, tables, and annotations in black-and-white (*num* =0) or in color (*num* =1; default). It has no effect on pictures, which are colored independently. |
| <span class="table-cell-nowrap">/D</span> | Specifies the layout is to be printed at the default resolution of the output device. Otherwise it is printed at the highest resolution. |
| This flag is no longer supported and has no effect. |  |

### *Details* {#details}
Normally page layouts are printed at the highest available resolution of the output device (printer, plotter, or whatever).

### *See Also* {#see-also}
[Exporting Graphics (Windows)](/igorpro/graphing/making-figures/graphics.md#exporting-graphics-windows)

[PrintSettings](/igorpro/commands/printsettings.md), [PrintGraphs](/igorpro/commands/printgraphs.md), [PrintTable](/igorpro/commands/printtable.md), [PrintNotebook](/igorpro/commands/printnotebook.md)