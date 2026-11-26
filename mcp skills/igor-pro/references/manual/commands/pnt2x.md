---
description: "The pnt2x function returns the X value of the named wave at the point pointNum. The point number is truncated to an integer before use."
slug: /commands/pnt2x
---

<div className="command-signature">

## <strong>pnt2x</strong> (<em>waveName</em>, <em>pointNum</em>) {#pnt2x}

</div>

The pnt2x function returns the X value of the named wave at the point *pointNum*. The point number is truncated to an integer before use.

For higher dimensions, use [IndexToScale](/igorpro/commands/indextoscale.md).

### *Details* {#details}
The result is derived from the wave's X scaling, not any X axis of a graph it may be displayed in.

If you would like to convert a fractional point number to an X value you can use: 

```igor
leftx(waveName) + deltax(waveName) * pointNum
```

### *See Also* {#see-also}
[DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md), [x2pnt](/igorpro/commands/x2pnt.md), [IndexToScale](/igorpro/commands/indextoscale.md)

For an explanation of waves and X scaling, see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).