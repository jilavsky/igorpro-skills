---
description: "The FindPointsInPoly operation determines if points fall within a certain polygon."
slug: /commands/findpointsinpoly
---

<div className="command-signature">

## <strong>FindPointsInPoly</strong>  <em>xWaveName</em>, <em>yWaveName</em>, <em>xPolyWaveName</em>, <em>yPolyWaveName</em> {#findpointsinpoly}

</div>

The FindPointsInPoly operation determines if points fall within a certain polygon. It can be used to write a procedure that operates on a subset of the data identified graphically in a graph.

### *Details* {#details}
FindPointsInPoly determines which points in *yWaveName* vs *xWaveName* fall within the polygon defined by *yPolyWaveName* vs *xPolyWaveName*.

*xWaveName* must have the same number of points as *yWaveName*  and *xPolyWaveName* must have the same number of points as *yPolyWaveName*.

FindPointsInPoly creates an output wave named W_inPoly with the same number of points as *xWaveName*. FindPointsInPoly indicates whether the point *yWaveName*[p] vs *xWaveName*[p] falls within the polygon by setting W_inPoly[p] to 1 if it is within the polygon, or to 0 if not.

FindPointsInPoly uses integer arithmetic with a precision of about 1 part in 1000. This should be good enough for visually determined (hand-drawn) polygons but might not be sufficient for mathematically generated polygons.

The FindPointsInPoly operation is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[GraphWaveDraw](/igorpro/commands/graphwavedraw.md), [PolygonOp](/igorpro/commands/polygonop.md)