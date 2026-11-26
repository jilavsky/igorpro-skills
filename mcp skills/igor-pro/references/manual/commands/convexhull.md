---
description: "The ConvexHull operation calculates the convex hull in either 2 or 3 dimensions. The dimensionality is deduced from the input wave(s)."
slug: /commands/convexhull
---

<div className="command-signature overload">

## <strong>ConvexHull</strong>  [/C/E/I/S/T=<em>tolerance</em> /V/Z] <em>xwave</em>, <em>ywave</em>  {#convexhull}

</div>
<div className="command-signature">

## <strong>ConvexHull</strong>  [/C/E/I/S/T=<em>tolerance</em> /V/Z] <em>tripletWave</em> {#convexhull}

</div>

The ConvexHull operation calculates the convex hull in either 2 or 3 dimensions. The dimensionality is deduced from the input wave(s). If the input consists of two 1D waves of the same length, the number of dimensions is assumed to be 2. If the input consists of a single triplet wave (a wave of 3 columns), then the number of dimensions is 3.

In 2D cases the operation calculates the convex hull and produces the result in a pair of x and y waves, W_XHull and W_YHull.

In 3D cases the operation calculates the convex hull and stores it in a triplet wave M_Hull that describes ordered facets of the convex hull.

ConvexHull returns an error if the input waves have fewer than 3 data points.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | (applies in 2D convex hull only) adds the first point to the end of the W_XHull and W_YHull waves so that the first and the last points are the same. |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> | Specifies the output wave created by the the operation. If the convex hull is calculated for a 2D domain the resulting *destWave* is a 2-column wave. If the convex hull is calculated for a 3D domain then destWave is a 3-column wave (corresponding to M_Hull that would be created by default).<br>It is an error to specify the same wave as both *srcWave* and *destWave*.<br>When used in a function, the ConvexHull operation creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
| <span class="table-cell-nowrap">/E</span> | (3D case only) if you use this flag the operation also creates a wave that lists the indices of the vertices which are not part of the convex hull, i.e., vertices which are interior to the hull. The output is in the wave W_HullExcluded. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave*  as a free wave. |
|  | /FREE is allowed only in functions and only if *destWave* , as specified by /DEST, is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/I</span> | (applies in 3D convex hull only) use this flag to get the corresponding index of the vertex as the fourth column in the M_Hull wave. |
| <span class="table-cell-nowrap">/S</span> | (applies in 3D convex hull only) use this flag if you want the resulting M_Hull to have NaN lines separating each triangle. |
| <span class="table-cell-nowrap">/T = *tolerance*</span> | (3D case only) The default tolerance for measuring if a point is inside or outside the convex hull is 1.0e-20. You can use any other positive value. |
| <span class="table-cell-nowrap">/V</span> | (3D case only) if you use this flag the operation also creates a wave containing the output in a list of vertex indices. The wave M_HullVertices contains a row per triangle where each entry on a row corresponds to the index of the input vertex. |
| <span class="table-cell-nowrap">/Z</span> | no error reporting. |

### *Examples* {#examples}

```igor
Make/O/N=33 xxx=gnoise(5),yyy=gnoise(7)
Convexhull/c  xxx,yyy
Display W_Yhull vs W_Xhull
Appendtograph yyy vs xxx
ModifyGraph mode(yyy)=3,marker(yyy)=8,rgb(W_YHull)=(0,15872,65280)
```

### *See Also* {#see-also}
[Triangulate3D](/igorpro/commands/triangulate3d.md)