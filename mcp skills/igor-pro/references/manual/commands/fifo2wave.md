---
description: "The FIFO2Wave operation copies FIFO data from the specified channel of the named FIFO into the named wave."
slug: /commands/fifo2wave
---

<div className="command-signature">

## <strong>FIFO2Wave</strong>  [/R=[<em>startPoint</em>,<em>endPoint</em> ]/S=<em>s</em> ] <em>FIFOName</em>, <em>channelName</em>, <em>waveName</em> {#fifo2wave}

</div>

The FIFO2Wave operation copies FIFO data from the specified channel of the named FIFO into the named wave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/R = [*startPoint*,*endPoint* ]</span> |  |
|  | Dumps the specified FIFO points into the wave. |
| /S=*s* |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Same as no /S at all.</td></tr><tr><td>*s*&nbsp;=1:</td><td>Sets the wave&#39;s X scaling x0 value to the number of the first sample in the FIFO.</td></tr><tr><td>*s*&nbsp;=2:</td><td>Changes the wave&#39;s number type to match the FIFO channel&#39;s type.</td></tr><tr><td>*s*&nbsp;=3:</td><td>Like *s* =1 and *s* =2 combined.</td></tr></tbody></table>

### *Details* {#details}
The FIFO must be in the valid state for FIFO2Wave to work. When you create a FIFO, using NewFIFO, it is initially invalid. It becomes valid when you issue the start command via the CtrlFIFO operation. It remains valid until you change a FIFO parameter using CtrlFIFO.

If you specify a range of FIFO data points, using /R=[*startPoint*,*endPoint* ] then FIFO2Wave dumps the specified FIFO points into the wave after clipping *startPoint* and *endPoint*  to valid point numbers.

The valid point numbers depend on whether the FIFO is running and on whether or not it is attached to a file. If the FIFO is running then *startPoint*  and *endPoint*  are truncated to the number of points in the FIFO. If the FIFO is buffering a file then the range can include the full extent of the file.

If you specify no range then FIFO2Wave transfers the most recently acquired FIFO data to the wave. The number of points transferred is the smaller of the number of points in the FIFO and number of points in the wave.

FIFO2Wave may or may not change the wave's X scaling and number type, depending on the current X scaling and on the /S flag.

Think of the wave's X scaling as being controlled by two values, x<sub>0</sub> and Δx, where the X value of point p is x<sub>0</sub> + p\*Δx. FIFO2Wave always sets the wave's Δx value equal to the FIFO's deltaT value (as set by the CtrlFIFO operation). If you use no /S flag, FIFO2Wave does not set the wave's x<sub>0</sub> value nor does it set the wave's number type.

If you are using FIFO2Wave to update a wave in a graph as quickly as possible, the /S=0 flag gives the highest update rate. The other /S values trigger more recalculation by Igor and slow down the updating.

If the number type of the wave (perhaps after being changed to match the FIFO channel) is a floating point type, FIFO2Wave scales the FIFO data before transferring it to the wave as follows:


```igor
scaled_value = (FIFO_value - offset) * gain
```

If the FIFO channel's gain is one and its offset is zero, the scaling would have no effect so FIFO2Wave skips it.

If the specified FIFO channel is an image strip channel (one defined using the optional vectPnts parameter to NewFIFOChan), then the resultant wave will be a matrix with the number of rows set by vectPnts and the number of columns set by the number of points described above for one-dimensional waves. To create an image plot that looks the same as the corresponding channel in a Chart, you will need to transpose the wave [MatrixTranspose](/igorpro/commands/matrixtranspose.md).

### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts) for an explanation of FIFOs and data acquisition.

[SetDrawEnv](/igorpro/commands/setdrawenv.md), [SetDrawLayer](/igorpro/commands/setdrawlayer.md)

For an explanation of waves and X scaling, see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).