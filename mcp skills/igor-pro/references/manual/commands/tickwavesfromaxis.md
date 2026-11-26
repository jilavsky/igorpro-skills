---
description: "The TickWavesFromAxis operation generates a pair of waves suitable for use as user tick waves (see User Ticks from Waves)."
slug: /commands/tickwavesfromaxis
---

<div className="command-signature">

## <strong>TickWavesFromAxis</strong>  [ /W=<em>graphName</em> /DEST= {<em>textWaveName</em>, <em>numericWaveName</em>} /O /AUTO=<em>mode</em> ] <em>axisName</em> {#tickwavesfromaxis}

</div>

The TickWavesFromAxis operation generates a pair of waves suitable for use as user tick waves (see [User Ticks from Waves](/igorpro/graphing/graphs.md#user-ticks-from-waves)). This allows you to programmatically determine the tick marks and tick labels that Igor would create for a given graph axis in auto mode.

TickWavesFromAxis was added in Igor Pro 8.00.

TickWavesFromAxis generates two waves: a two-column text wave containing tick labels and the names of tick types, and a numeric wave giving the positions of the ticks along the axis. By default, the information stored in the output waves reflects the automatically generated ticks based on the current axis settings but you can change this using the /AUTO flag.

By default the waves are given names derived from the graph window and axis name: *\<graphname\>\_\<axisname\>_label*s and *\<graphname\>\_\<axisname\>_valu*es. Use /DEST to give the waves custom names.

### *Parameters* {#parameters}
*axisName* is the name of the axis for which the tick waves are generated. This will usually be left, bottom, right or top, but may be the name of a free axis.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AUTO = *mode*</span> | Controls the axis settings that are used when generating the output waves: |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=&nbsp;0:</td><td>Computed manual tick settings are used.</td></tr><tr><td>*mode*&nbsp;=&nbsp;1:</td><td>The automatic tick settings are used (default).</td></tr><tr><td>*mode*&nbsp;=&nbsp;2:</td><td>Either computed manual ticks or auto ticks are used, depending on the current setting of the graph.</td></tr></tbody></table>
|  | If you use /AUTO=0 and the graph is currently in auto mode, the results could be surprising if you haven't actually set the computed manual ticks settings. |
|  | /AUTO was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/DEST = {*textWaveName*, *numericWaveName*}</span> |  |
|  | Specifies custom names for the generated waves. *textWaveName* is the name of the text wave containing the tick labels. *numericWaveName* is the name of the numeric wave containing the axis position values for the ticks. If the waves don't already exist, they are created. |
|  | You may use data folder syntax as long as the data folders already exist. |
|  | The operation may create wave references for the destination waves if called in a user-defined function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/O</span> | Tells TickWavesFromAxis that it can overwrite existing waves. |
|  | Igor returns an error if you attempt to overwrite a numeric wave with a text wave or a text wave with a numeric wave. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the graph containing the axis. This may be a subwindow path. If you omit /W, the top graph window is used. |

### *Details* {#details}
The TickWavesFromAxis operation depends on drawing the axis to generate the list of ticks. It causes a screen refresh, equivalent to calling [DoUpdate](/igorpro/commands/doupdate.md), twice during its execution.

The TickWavesFromAxis operation honors your axis format settings and manual range. It works on regular numeric axes, log axes and date/time axes. At this time it does not work on category axes or axes using user ticks from waves.

### *See Also* {#see-also}
[User Ticks from Waves](/igorpro/graphing/graphs.md#user-ticks-from-waves), [ModifyGraph](/igorpro/commands/modifygraph.md) UserTicks, ManTick and ManMinor keywords