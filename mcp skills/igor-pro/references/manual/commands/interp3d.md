---
description: "The Interp3D function returns an interpolated value for location P=(x, y, z) in a 3D scalar distribution srcWave."
slug: /commands/interp3d
---

<div className="command-signature">

## <strong>Interp3D</strong> (<em>srcWave</em>, <em>x</em>, <em>y</em>, <em>z</em> [, <em>triangulationWave</em>]) {#interp3d}

</div>

The Interp3D function returns an interpolated value for location P=(*x*, *y*, *z* ) in a 3D scalar distribution *srcWave*.

If *srcWave* is a 3D wave containing a scalar distribution sampled on a regular lattice, the function returns a linearly interpolated value for any P=(*x*, *y*, *z* ) location within the domain of srcWave. If P is outside the domain, the function returns NaN.

To interpolate a 3D scalar distribution that is not sampled on a regular lattice, *srcWave* is a 4 column 2D wave where the columns correspond to *x*, *y*, *z* , f(*z*, *y*, *z*), respectively. You must also use a "triangulation" wave for *srcWave* (you can obtain the triangulation wave with the operation Triangulate3D/out=1). If P falls within the convex domain defined by the tetrahedra in *triangulationWave*, the function returns the barycentric linear interpolation for P using the tetrahedron where P is found. If P is outside the convex domain the function returns NaN..

### *Examples* {#examples}

```igor
Make/O/N=(10,20,30) ddd=gnoise(10)

Print interp3d(ddd,1,0,0)
Print interp3d(ddd,1,1,1)

Make/O/N=(10,4) ddd=gnoise(10)
Triangulate3D/OUT=1 ddd
Print interp3d(ddd,1,0,0,M_3DVertexList)
Print interp3d(ddd,1,1,1,M_3DVertexList)
```

### *See Also* {#see-also}
[Interpolate3D](/igorpro/commands/interpolate3d.md)