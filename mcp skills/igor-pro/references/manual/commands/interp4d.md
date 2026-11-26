---
description: "The Interp4D function returns an interpolated value for location P=(x, y, z, t) in a 4D scalar distribution srcWave."
slug: /commands/interp4d
---

<div className="command-signature">

## <strong>Interp4D</strong> (<em>srcWave</em>, <em>x</em>, <em>y</em>, <em>z</em>, <em>t</em>) {#interp4d}

</div>

The Interp4D function returns an interpolated value for location P=(*x*, *y*, *z, t*) in a 4D scalar distribution *srcWave*.

If *srcWave* is a 4D wave containing a scalar distribution sampled on a regular lattice, the function returns a linearly interpolated value for any P=(*x*, *y*, *z, t*) location within the domain of srcWave. If P is outside the domain, the function returns NaN.

### *Example* {#example}

```igor
Make/O/N=(10,20,30,40) ddd=x+10*y+100*z+1000*t
Print interp4d(ddd,1,2,3,4.1)
   4421
```

### *See Also* {#see-also}
[Interpolation](/igorpro/analysis/analysis.md#interpolation) overview.  The [ImageInterpolate](/igorpro/commands/imageinterpolate.md), [Interpolate2](/igorpro/commands/interpolate2.md), [Interp3DPath](/igorpro/commands/interp3dpath.md), [Interp4DPath](/igorpro/commands/interp4dpath.md), [Interpolate3D](/igorpro/commands/interpolate3d.md), [SphericalInterpolate](/igorpro/commands/sphericalinterpolate.md), [Interp4DPath](/igorpro/commands/interp4dpath.md) operations and the [interp](/igorpro/commands/interp.md), [Interp2D](/igorpro/commands/interp2d.md), and [Interp3D](/igorpro/commands/interp3d.md) functions.