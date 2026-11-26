---
description: "The AppendToLayout operation appends the specified objects to the top layout."
slug: /commands/appendtolayout
---

<div className="command-signature">

## <strong>AppendToLayout</strong>  [/G=<em>g</em> /I/M/R/T/S] <em>objectSpec</em>  [, <em>objectSpec</em> ]... {#appendtolayout}

</div>

The AppendToLayout operation appends the specified objects to the top layout.

The AppendToLayout operation cannot be used in user-defined functions. Use the AppendLayoutObject operation instead.

### *Parameters* {#parameters}
The optional *objectSpec* parameters identify a graph, table, textbox or PICT to be added to the layout. An object specification can also specify the location and size of the object, whether the object should have a frame or not, whether it should be transparent or opaque, and whether it should be displayed in high fidelity or not. See [Layout](/igorpro/commands/layout.md) for details.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/G = *g*</span> | Specifies grout, the spacing between tiled objects. Units are points unless /I, /M, or /R are specified. |
| <span class="table-cell-nowrap">/I</span> | *objectSpec* coordinates are in inches. |
| <span class="table-cell-nowrap">/M</span> | *objectSpec* coordinates are in centimeters. |
| <span class="table-cell-nowrap">/R</span> | *objectSpec* coordinates are in percent of printing part of the page. |
| <span class="table-cell-nowrap">/S</span> | Stacks objects. |
| <span class="table-cell-nowrap">/T</span> | Tiles objects. |

### *See Also* {#see-also}
[Layout](/igorpro/commands/layout.md) and the [AppendLayoutObject](/igorpro/commands/appendlayoutobject.md) operation for use with user-defined functions.