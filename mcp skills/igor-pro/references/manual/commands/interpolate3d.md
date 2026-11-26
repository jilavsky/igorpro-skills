---
description: "The Interpolate3D operation uses a precomputed triangulation of sWave (see Triangulate3D) to calculate regularly spaced interpolated values from an…"
slug: /commands/interpolate3d
---

<div className="command-signature">

## <strong>Interpolate3D</strong>  [/Z ] /RNGX={<em>x0</em>,<em>dx</em>,<em>nx</em>}/RNGY={<em>y0</em>,<em>dy</em>,<em>ny</em>}/RNGZ={<em>z0</em>,<em>dz</em>,<em>nz</em>} /DEST=<em>dataFolderAndName</em>, <em>triangulationWave</em>=<em>tWave</em>, <em>srcWave</em>=<em>sWave</em> {#interpolate3d}

</div>

The Interpolate3D operation uses a precomputed triangulation of *sWave* (see [Triangulate3D](/igorpro/commands/triangulate3d.md)) to calculate regularly spaced interpolated values from an irregularly spaced source. The interpolated values are calculated for a lattice defined by the range flags /RNGX, /RNGY, and /RNGZ. *sWave* is a 4 column wave where the first three columns represent the spatial coordinates and the fourth column represents the associated scalar value. The operation is essentially equivalent to calling the function [Interp3D](/igorpro/commands/interp3d.md) for each interpolated point in the range but it is much more efficient.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">triangulationWave = *tWave*</span> |  |
|  | Specifies a 2D index wave, *tWave*, in which each row corresponds to one tetrahedron and each column (tetrahedron vertex) is represented by an index of a row in *sWave*. Use Triangulate3D with /OUT=1 to obtain *tWave*. |
| <span class="table-cell-nowrap">srcWave = *sWave*</span> | Specifies a real-valued 4 column 2D source wave, *sWave*, in which columns correspond to *x*, *y*, *z*, f(*x*, *y*, *z* ). Requires that the domain occupied by the set of {*x*, *y*, *z* } be convex. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *dataFolderAndName*</span> |  |
|  | Saves the result in the specified destination wave. The destination wave will be created or overwritten if it already exists. *dataFolderAndName* can include a full or partial path with the wave name. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the wave specified by /DEST (*dataFolderAndName*) as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/RNGX = {*x0*,*dx*,*nx* }</span> | Specifies the range along the X-axis. The interpolated values start at *x0*. There are *nx* equally spaced interpolated values where the last value is at:<br>`x0 +(nx -1)dx`<br>If you would like to interpolate the data for a single plane you can set the appropriate number of values to 1. For example, a YZ plane would have *nx* =1. |
| <span class="table-cell-nowrap">/RNGY = {*y0*,*dy*,*ny* }</span> | Specifies the range along the Y-axis. The interpolated values start at *y0*. There are *nx* equally spaced interpolated values where the last value is at:<br>`y0 +(ny -1)dy`<br>If you would like to interpolate the data for a single plane you can set the appropriate number of values to 1. For example, a XZ plane would have *ny* =1. |
| <span class="table-cell-nowrap">/RNGZ = {*z0*,*dz*,*nz* }</span> | Specifies the range along the Z-axis. The interpolated values start at *z0*. There are *nz* equally spaced interpolated values where the last value is at:<br>`z0 +(nz -1)dz`<br>If you would like to interpolate the data for a single plane you can set the appropriate number of values to 1. For example, a XY plane would have *nz* =1. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The triangulation wave defines a set of tetrahedra that spans the convex source domain. If the requested range consists of points outside the domain, the interpolated values will be set to NaN. The interpolation process for points inside the convex domain consists of first finding the tetrahedron in which the point resides and then linearly interpolating the scalar value using the barycentric coordinate of the interpolated point.

In some cases the interpolation may result in NaN values for points that are clearly inside the convex domain. This may happen when the preceding Triangulate3D results in tetrahedra that are too thin. You can try using Triangulate3D with the flag /OUT=4 to get more specific information about the triangulation. Alternatively you can introduce a slight random perturbation to the input source wave before the triangulation.

### *Example* {#example}

```igor
Function Interpolate3DDemo()
	Make/O/N=(50,4) ddd=gnoise(20)	// First 3 columns store XYZ coordinates
	ddd[][3]=ddd[p][2]	// Fourth column stores a scalar which is set to z in this example
	Triangulate3D ddd	// Perform the triangulation
	Wave M_3dVertexList
	Interpolate3D /RNGX={-30,1,80}/RNGY={-40,1,80}/RNGZ={-40,1,80}/DEST=W_Interp triangulationWave=M_3dVertexList,srcWave=ddd
End
```

### *See Also* {#see-also}
[Triangulate3D](/igorpro/commands/triangulate3d.md), [Interp3D](/igorpro/commands/interp3d.md)

### *References* {#references}
Schneider, P.J., and D. H. Eberly, *Geometric Tools for Computer Graphics*, Morgan Kaufmann, 2003.