---
description: "The DimOffset function returns the scaling offset of the given dimension."
slug: /commands/dimoffset
---

<div className="command-signature">

## <strong>DimOffset</strong> (<em>waveName</em>, <em>dimNumber</em>) {#dimoffset}

</div>

The DimOffset function returns the scaling offset of the given dimension.

*dimNumber*  is one of the following:

|  |  |
| --- | --- |
| 0: | Rows |
| 1: | Columns |
| 2: | Layers |
| 3: | Chunks |

If *dimNumber* =0 this is identical to leftx(*waveName*).

### *See Also* {#see-also}
[DimDelta](/igorpro/commands/dimdelta.md), [DimSize](/igorpro/commands/dimsize.md), [SetScale](/igorpro/commands/setscale.md), [WaveUnits](/igorpro/commands/waveunits.md), [ScaleToIndex](/igorpro/commands/scaletoindex.md)