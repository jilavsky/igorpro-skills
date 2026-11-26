---
description: "The WaveUnits function returns a string containing the units for the given dimension."
slug: /commands/waveunits
---

<div className="command-signature">

## <strong>WaveUnits</strong> (<em>waveName</em>, <em>dimNumber</em>) {#waveunits}

</div>

The WaveUnits function returns a string containing the units for the given dimension.

Use *dimNumber* =0 for rows, 1 for columns, 2 for layers and 3 for chunks. Use -1 to get the data units. If the wave is just 1D, *dimNumber*=0 returns X units and 1 returns data units. This behavior is just like the WaveMetrics procedure WaveUnits found in the WaveMetrics Procedures folder in previous versions of Igor Pro.

### *See Also* {#see-also}
[DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md), [DimSize](/igorpro/commands/dimsize.md), [SetScale](/igorpro/commands/setscale.md)