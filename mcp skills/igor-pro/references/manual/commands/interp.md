---
description: "The interp function returns a linearly interpolated value at the location x = x1 of a curve whose X components come from the Y values of xwaveName and whose y…"
slug: /commands/interp
---

<div className="command-signature">

## <strong>interp</strong> (<em>x1</em>, <em>xwaveName</em>, <em>ywaveName</em>) {#interp}

</div>

The interp function returns a linearly interpolated value at the location x = *x1* of a curve whose X components come from the Y values of *xwaveName* and whose y components come from the Y values of *ywaveName*.

### *Details* {#details}
interp returns nonsense if the waves are complex or if *xwaveName* is not monotonic or if either wave contains NaNs.

The interp function is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *Examples* {#examples}
<img src="Images/interp/interp_0.png" width="100%"/>

### *See Also* {#see-also}
[Interpolate2](/igorpro/commands/interpolate2.md)

[Loess](/igorpro/commands/loess.md), [ImageInterpolate](/igorpro/commands/imageinterpolate.md), [Interpolate3D](/igorpro/commands/interpolate3d.md), [Interp3DPath](/igorpro/commands/interp3dpath.md)

[interp2D](/igorpro/commands/interp2d.md), [interp3D](/igorpro/commands/interp3d.md), [contourZ](/igorpro/commands/contourz.md)