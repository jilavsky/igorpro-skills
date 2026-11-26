---
description: "The ScaleToIndex function returns the number of the element in the requested dimension whose scaled index value is closest to coordValue."
slug: /commands/scaletoindex
---

<div className="command-signature">

## <strong>ScaleToIndex</strong> (<em>waveName</em>, <em>coordValue</em>, <em>dim</em>) {#scaletoindex}

</div>

The ScaleToIndex function returns the number of the element in the requested dimension whose scaled index value is closest to *coordValue* .

The ScaleToIndex function was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*dim* is a dimension number: 0 for rows, 1 for columns, 2 for layers, 3 for chunks.

*coordValue* is a scaled index in that dimension.

### *Details* {#details}
The ScaleToIndex function returns the value of the expression:


```igor
round((coordValue - DimOffset(wave,dim)) / DimDelta(wave,dim))
```

With dim=0, ScaleToIndex is equivalent to [x2pnt](/igorpro/commands/x2pnt.md).

If *coordValue* is NaN or +/-INF, ScaleToIndex returns NaN. Otherwise, the result is computed based on the [DimOffset](/igorpro/commands/dimoffset.md) and [DimDelta](/igorpro/commands/dimdelta.md) of the specified dimension of the wave. The result is not clipped to a valid element number for the wave dimension.

### *See Also* {#see-also}
[IndexToScale](/igorpro/commands/indextoscale.md), [x2pnt](/igorpro/commands/x2pnt.md), [DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md)

[The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data) for an explanation of wave scaling.