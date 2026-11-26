---
description: "The Interp2D function returns a double precision number as the bilinear interpolation value at the specified coordinates of the source wave."
slug: /commands/interp2d
---

<div className="command-signature">

## <strong>Interp2D</strong> (<em>srcWaveName</em>, <em>x</em>, <em>y</em>) {#interp2d}

</div>

The Interp2D function returns a double precision number as the bilinear interpolation value at the specified coordinates of the source wave. It returns NaN if the point is outside the source wave domain or if the source wave is complex.

### *Parameters* {#parameters}
*srcWaveName* is the name of a 2D wave which must be real.

*x* is the X location of the interpolated point.

*y* is the Y location of the interpolated point.

### *See Also* {#see-also}
[ImageInterpolate](/igorpro/commands/imageinterpolate.md)