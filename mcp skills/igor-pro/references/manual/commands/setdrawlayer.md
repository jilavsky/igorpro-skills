---
description: "The SetDrawLayer operation makes all future drawing operations use the named layer."
slug: /commands/setdrawlayer
---

<div className="command-signature">

## <strong>SetDrawLayer</strong>  [/W=<em>winName</em> /K] <em>layerName</em> {#setdrawlayer}

</div>

The SetDrawLayer operation makes all future drawing operations use the named layer.

### *Parameters* {#parameters}
Valid *layerNames*  for graphs:

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| ProgBack | UserBack | ProgAxes | UserAxes | ProgFront | UserFront

ProgTop	UserTop	Overlay

Valid *layerNames*  for page layouts:

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| ProgBack | UserBack | ProgFront | UserFront | Overlay |
Valid *layerNames*  for control panels:

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| ProgBack | UserBack | ProgFront | UserFront | Overlay |

There are really only three layers for control panels. ProgFront is treated as an alias for ProgBack and UserFront is treated as an alias for UserBack.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/K</span> | kills (erases) the given layer. |
| <span class="table-cell-nowrap">/W = *winName*</span> | specifies the named window for drawing. This must be the first flag specified when used in a Proc or Macro or on the command line. |

### *Details* {#details}
The Overlay layer is drawn above all else. It is not included when printing or exporting graphics and is provided for programmers who wish to add user-interface drawing elements without disturbing graphics elements. Overlay was added in Igor Pro 7.00.

Layer icon in the drawing tool palette: <img src="Images/SetDrawLayer/SetDrawLayer_0.png" width="50%"/>. A checkmark indicates the current layer. Non-drawing layers are indicated with gray text.

### *Output Variables* {#output-variables}
SetDrawLayer sets S_Name to the name of the previously-selected drawing layer. You can use this to restore the active drawing layer after programmatic drawing.

### *See Also* {#see-also}
[Drawing](/igorpro/graphing/drawing.md), [Drawing Layers](/igorpro/graphing/drawing.md#drawing-layers), [DrawAction](/igorpro/commands/drawaction.md)