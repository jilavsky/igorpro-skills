---
description: "The DimDelta function returns the scale factor delta of the given dimension."
slug: /commands/dimdelta
---

<div className="command-signature">

## <strong>DimDelta</strong> (<em>waveName</em>, <em>dimNumber</em> ) {#dimdelta}

</div>

The DimDelta function returns the scale factor delta of the given dimension.

*dimNumber* is one of the following:

|  |  |
| --- | --- |
| 0: | Rows |
| 1: | Columns |
| 2: | Layers |
| 3: | Chunks |

If *dimNumber* =0 this is identical to `deltax(waveName)`.

### *See Also* {#see-also}
[DimOffset](/igorpro/commands/dimoffset.md), [DimSize](/igorpro/commands/dimsize.md), [SetScale](/igorpro/commands/setscale.md), [WaveUnits](/igorpro/commands/waveunits.md), [ScaleToIndex](/igorpro/commands/scaletoindex.md)