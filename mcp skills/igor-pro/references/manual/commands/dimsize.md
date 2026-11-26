---
description: "The DimSize function returns the size of the given dimension. dimNumber is one of the following."
slug: /commands/dimsize
---

<div className="command-signature">

## <strong>DimSize</strong> (<em>waveName</em>, <em>dimNumber</em>) {#dimsize}

</div>

The DimSize function returns the size of the given dimension.

*dimNumber* is one of the following:

|  |  |
| --- | --- |
| 0: | Rows |
| 1: | Columns |
| 2: | Layers |
| 3: | Chunks |

For a 1D wave, DimSize(*waveName*,0) is identical to `numpnts(waveName)`.

### *See Also* {#see-also}
[DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md), [SetScale](/igorpro/commands/setscale.md), [WaveUnits](/igorpro/commands/waveunits.md)