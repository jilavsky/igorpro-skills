---
description: "The NewFIFOChan operation creates a new channel for the named FIFO. channelName must be unique for the specified FIFO."
slug: /commands/newfifochan
---

<div className="command-signature">

## <strong>NewFIFOChan</strong>  [/B/C/D/I/S/U/W/Y=<em>numType</em> ] <em>FIFOName</em>, <em>channelName</em>, <em>offset</em>, <em>gain</em>, <em>minusFS</em>, <em>plusFS</em>, <em>unitsStr</em> [, <em>vectPnts</em> ] {#newfifochan}

</div>

The NewFIFOChan operation creates a new channel for the named FIFO.

### *Parameters* {#parameters}
*channelName* must be unique for the specified FIFO.

The *offset*, *gain*, *plusFS*, *minusFS* and *unitsStr* parameters are used when the channel's data is displayed or transferred to a wave. If given, *vectPnts* must be between 1 and 65535.

### *Flags* {#flags}
The flags define the type of data to be stored in the FIFO channel:


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | 8-bit signed integer or unsigned integer if /U is present. |
| <span class="table-cell-nowrap">/C</span> | Complex. |
| <span class="table-cell-nowrap">/D</span> | Double precision IEEE floating point. |
| <span class="table-cell-nowrap">/I</span> | 32-bit signed integer or unsigned integer if /U is present. |
| <span class="table-cell-nowrap">/S</span> | Single precision IEEE floating point (default). |
| <span class="table-cell-nowrap">/U</span> | Integer data are unsigned. |
| <span class="table-cell-nowrap">/W</span> | 16-bit signed integer or unsigned integer if /U is present. |
| <span class="table-cell-nowrap">/Y = *type*</span> | Specifies wave data type. See details below. |

### *Wave Data Types* {#wave-data-types}
As a replacement for the above number type flags you can use /Y=*numType* to set the number type as an integer code. See [WaveType](/igorpro/commands/wavetype.md) for code values. Do not use /Y in combination with other type flags.

### *Details* {#details}
You cannot invoke NewFIFOChan while the named FIFO is running.

If you provide a value for *vectPnts*, you will create a channel capable of holding a vector of data rather than just a single data value. When such a channel is used in a Chart, it is displayed as an image using one of the built-in color tables.

Igor scales values in the FIFO channel before displaying them in a chart or transferring them to a wave as followed:


```igor
scaled_value = (FIFO_value - offset) * gain
```

Igor uses the *plusFS* and *minusFS* parameters (plus and minus full scale) to set the default display scaling for charts.

The *unitsStr* parameter is an Igor units string (3 bytes maximum).

When you transfer a channel's data to a wave, using the FIFO2Wave operation, Igor stores the *plusFS* and *minusFS* values and the *unitsStr* in the wave's Y scaling.

### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)