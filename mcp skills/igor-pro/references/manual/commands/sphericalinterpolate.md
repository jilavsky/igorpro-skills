---
description: "The SphericalInterpolate operation works in conjunction with the SphericalTriangulate operation to calculate interpolated values on a surface of a sphere."
slug: /commands/sphericalinterpolate
---

<div className="command-signature">

## <strong>SphericalInterpolate</strong>  <em>triangulationDataWave</em>, <em>dataPointsWave</em>, <em>newLocationsWave</em> {#sphericalinterpolate}

</div>

The SphericalInterpolate operation works in conjunction with the SphericalTriangulate operation to calculate interpolated values on a surface of a sphere. Given a set of {x<sub>i</sub>, y<sub>i</sub>, z<sub>i</sub>} points on the surface of a sphere with their associated values {v<sub>i</sub>}, the SphericalTriangulate operation performs the Delaunay triangulation and creates an output that is used by the SphericalInterpolate operation to calculate values at any other point on the surface of a sphere. The interpolation calculation uses Voronoi polygons to weigh the contribution of the nearest neighbors to any given location on the sphere.

### *Parameters* {#parameters}
*triangulationDataWave*  is a 13 column wave that was created by the SphericalTriangulate operation.

*dataPoints*  is a 4 column wave. The first 3 columns are the {x<sub>i</sub>, y<sub>i</sub>, z<sub>i</sub>} locations that were used to create the triangulation, and the last column corresponds to the {v<sub>i</sub>} values at the triangulation locations.

*newLocationsWave*  is a 3 column wave that specifies the x,y,z locations on the sphere at which the interpolated values are calculated. Note that internally, each triplet is normalized to a point on the unit sphere before it is used in the interpolation.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *iWave*</span> | Specify the destination wave.  If this flag is not specified, the operation saves the interpolation in the wave W_SphericalInterpolation in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error reporting. |

### *Details* {#details}
You will always need to use the SphericalTriangulate operation first to generate the *triangulationDataWave* input for this operation.

The result of the operation are put in the wave W_SphericalInterpolation.

### *See Also* {#see-also}
[SphericalTriangulate](/igorpro/commands/sphericaltriangulate.md), [Triangulate3D](/igorpro/commands/triangulate3d.md), [ImageInterpolate](/igorpro/commands/imageinterpolate.md) with keyword Voronoi

### *Demo* {#demo}
[Open Spherical Triangulation Demo](#igor-pxp/Examples/Analysis/SphericalTriangulationDemo.pxp)