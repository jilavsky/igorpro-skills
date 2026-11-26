---
description: "The DrawAction operation deletes, inserts, and reads back a named drawing object group or the entire draw layer."
slug: /commands/drawaction
---

<div className="command-signature">

## <strong>DrawAction</strong>  [/L=<em>layerName</em> /W=<em>winName</em>  ] <em>keyword</em> = <em>value</em> [, <em>keyword</em> = <em>value</em> ...] {#drawaction}

</div>

The DrawAction operation deletes, inserts, and reads back a named drawing object group or the entire draw layer.

### *Parameters* {#parameters}
DrawAction accepts multiple *keyword* =*value*  parameters on one line.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">beginInsert [ = *index* ]</span> | Inserts draw commands before or at index position or at position specified by getgroup or delete parameters; position otherwise is zero. |
| <span class="table-cell-nowrap">commands [ = *start*,*stop* ]</span> |  |
|  | Stores commands in S_recreation for draw objects between start and stop index values, range defined by getgroup, or entire layer otherwise.  The variable V_flag is set to the number of draw elements included. If there are none, S_recreation has zero length. |
| <span class="table-cell-nowrap">delete [ = *start*,*stop* ]</span> | Deletes draw objects between start and stop index values, range defined by getgroup, or entire layer otherwise. |
| <span class="table-cell-nowrap">extractOutline [ = *start*,*stop* ]</span> |  |
|  | Stores polygon outline between start and stop index values, range defined by getgroup, or entire layer otherwise. Waves W_PolyX and W_PolyY contain coordinates with NaN separators. V_npnts contains the number of objects, V_startPos contains the starting index value and V_endPos contains the ending index value. Coordinates are for the first object encountered. |
| endInsert | Terminates insert mode. |
| <span class="table-cell-nowrap">getgroup = *name*</span> | Stores first and last index of named group in V_startPos and V_endPos. Use `_all_` to specify the entire layer. Sets V_flag to truth group exists. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/L = *layerName*</span> | Specifies the drawing layer on which to act. *layerName* is one of the drawing layers as specified in [SetDrawLayer](/igorpro/commands/setdrawlayer.md). |
| <span class="table-cell-nowrap">/W = *winName*</span> | Sets the named window or subwindow for drawing. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with winName, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Commands stored in S_recreation are the same as those that would be generated for the range of objects in the recreation macro for the window but also have comment lines preceding each object of the form:


```igor
 // ;ITEMNO:n;
```

where *n*  is the item number of the draw object.

### *Examples* {#examples}
Create a drawing with a named group:


```igor
NewPanel /W=(455,124,936,413)
SetDrawEnv fillfgc= (65535,0,0)
DrawRect 58,45,132,103
SetDrawEnv gstart,gname= fred
SetDrawEnv fillfgc= (65535,43690,0)
DrawRect 79,62,154,120
SetDrawEnv arrow= 1
DrawLine 139,70,219,70
SetDrawEnv gstop
SetDrawEnv fillfgc= (0,65535,65535)
DrawRect 95,77,175,138
SetDrawEnv fillfgc= (0,0,65535)
DrawRect 111,91,191,156
```

Get and print commands for the "fred" group:


```igor
DrawAction getgroup=fred,commands
Print S_recreation
```

prints:


```igor
// ;ITEMNO:2;
SetDrawEnv gstart,gname= fred
// ;ITEMNO:3;
SetDrawEnv fillfgc= (65535,43690,0)
// ;ITEMNO:4;
DrawRect 79,62,154,120
// ;ITEMNO:5;
SetDrawEnv arrow= 1
// ;ITEMNO:6;
DrawLine 139,70,219,70
// ;ITEMNO:7;
SetDrawEnv gstop
```

Replace group fred (the orange rectangle and the arrow) with a different object. First delete the group and enter insert mode:


```igor
DrawAction getgroup=fred, delete, begininsert
```

Next draw the replacement:


```igor
SetDrawEnv gstart,gname= fred
SetDrawEnv fillfgc= (65535,65535,0)
DrawOval 82,62,161,123
SetDrawEnv gstop
```

Lastly exit insert mode:


```igor
DrawAction endinsert
```

### *See Also* {#see-also}
[SetDrawEnv](/igorpro/commands/setdrawenv.md), [Drawing](/igorpro/graphing/drawing.md)