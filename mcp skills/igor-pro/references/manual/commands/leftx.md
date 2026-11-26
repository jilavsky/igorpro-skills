---
description: "The leftx function returns the X value of point 0 (the first point) of the named 1D wave. The leftx function is not multidimensional aware."
slug: /commands/leftx
---

<div className="command-signature">

## <strong>leftx</strong> (<em>waveName</em>) {#leftx}

</div>

The leftx function returns the X value of point 0 (the first point) of the named 1D wave. The leftx function is not multidimensional aware. The multidimensional equivalent of this function is [DimOffset](/igorpro/commands/dimoffset.md).

### *Details* {#details}
Point 0 contains a wave's ***first*** value, which is usually the leftmost point when displayed in a graph. Leftx returns the value elsewhere called "x<sub>0</sub>". The function DimOffset returns any of x0, y0, z0, or t0, for dimensions 0, 1, 2 or 3.

### *See Also* {#see-also}
[deltax](/igorpro/commands/deltax.md), [rightx](/igorpro/commands/rightx.md)

For multidimensional waves, see [DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md), and [DimSize](/igorpro/commands/dimsize.md).

For an explanation of waves and wave scaling, see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).