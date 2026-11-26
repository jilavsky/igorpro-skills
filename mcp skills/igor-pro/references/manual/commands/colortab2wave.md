---
description: "The ColorTab2Wave operation extracts colors from the built-in color table and places them in an Nx3 matrix of red, green and blue columns named M_colors."
slug: /commands/colortab2wave
---

<div className="command-signature">

## <strong>ColorTab2Wave</strong>  <em>colorTableName</em> {#colortab2wave}

</div>

The ColorTab2Wave operation extracts colors from the built-in color table and places them in an Nx3 matrix of red, green and blue columns named M_colors. Values are unsigned 16-bit integers and range from 0 to 65535.

N will typically be 100 but may be as little as 9 and as large as 476. Use


```igor
Variable N= DimSize(M_colors,0)
```

to determine the actual number of colors.

The wave M_colors is created in the current data folder. Red is in column 0, green is in column 1, and blue in column 2.

### *Parameters* {#parameters}
*colorTableName* can be any of those returned by the [CTabList](/igorpro/commands/ctablist.md) function, such as Grays or Rainbow.

*colorTableName* can also be Igor or IgorRecent, to return either the 128 standard or 0-32 user-selected colors from Igor's color menu.

### *Details* {#details}
See [Color Tables](/igorpro/graphing/contour-plots.md#color-tables).