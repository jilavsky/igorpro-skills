---
description: "The PolygonOp operation performs operations on planar polygons. Polygons and polygon paths are represented by XY pairs of waves with NaNs separating closed…"
slug: /commands/polygonop
---

<div className="command-signature">

## <strong>PolygonOp</strong>  [<em>flags</em>] [<em>keyword</em>=<em>value</em>] {#polygonop}

</div>

The PolygonOp operation performs operations on planar polygons. Polygons and polygon paths are represented by XY pairs of waves with NaNs separating closed polygons.

The operation performed is specified using the operation keyword. The resulting polygon is returned as an XY pair of waves as specified by the /DSTX and /DSTY flags.

PolygonOp uses the clipper library by Angus Johnson. It was added in Igor Pro 9.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ADDR = *addingRule*</span> |  |
|  | *addingRule* determines how the primary and secondary polygons are added to the primary and secondary paths. The interior of the polygon is defined as the region that would be "filled" using one of the standard fill rules. The even-odd rule applies to scan lines while the other rules are based on winding counts. |
|  | *addingRule* is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>0</td><td>Even-odd (default). All odd numbered sub-regions are filled, while even numbered sub-regions are not filled.</td></tr><tr><td>1</td><td>Non-zero. All non-zero winding subregions are filled.</td></tr><tr><td>2</td><td>Positive. All sub-regions with winding counts&gt;0 are filled.</td></tr><tr><td>3</td><td>Negative. All sub-regions with winding counts&lt;0 are filled.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/D</span> | Tells Igor to create double precision output waves. |
| <span class="table-cell-nowrap">/DIST = *dist*</span> | Specifies the distance in scaled units (see the /SM flag) below which vertices are stripped. The default value is approximately sqrt(2). |
| <span class="table-cell-nowrap">/DSTX = *dest*X</span> | Specifies the X destination wave. The output is corrected for any scaling (see /SM below). |
|  | In a user-defined function, if *dest*X is a simple wave name, PolygonOp automatically creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If you omit /DSTX, the X destination wave defaults to polyOpWaveX in the current data folder. |
|  | If destX is a simple name and you include /FREE, the X destination is created as a free wave. |
| <span class="table-cell-nowrap">/DSTY = *dest*Y</span> | Specifies the Y destination wave. The output is corrected for any scaling (see /SM below). |
|  | In a user-defined function, if *dest*Y is a simple wave name, PolygonOp automatically creates a real wave reference for the destination wave. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If you omit /DSTY, the Y destination wave defaults to polyOpWaveX in the current data folder. |
|  | If *dest*Y is a simple name and you include /FREE, the Y destination is created as a free wave. |
| <span class="table-cell-nowrap">/FA</span> | Computes the final area of the resulting polygon and stores it in V_area. This is an algebraic (signed) area in contrast to the area returned by PolygonArea which is always non-negative. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the output waves specified by /DSTX and /DSTY as free waves. |
| <span class="table-cell-nowrap">/JTYP = *jointType*</span> | Specifies the joint type used when offsetting a polygon. The following joint types are supported: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Square joint</td></tr><tr><td>1:</td><td>Round joint</td></tr><tr><td>2:</td><td>Miter joint</td></tr></tbody></table>
|  | Square and round joints may give rise to additional vertices along the path. |
| <span class="table-cell-nowrap">/MLMT = *miterLimit*</span> |  |
|  | When the path consists of two edges connected at an acute angle, the offset could give rise to very long spikes. The miter limit sets the maximum distance in multiples of the offset that vertices can be offset from their original positions before a square joint (see /JTYP) is used. The default value for *miterLimit* is 2. The *miterLimit* parameter is scaled by /SM *scaleFactor*. |
| <span class="table-cell-nowrap">/NCFP</span> | Disables closing the resulting polygons by connecting the last vertex to the first vertex of each output path. |
| <span class="table-cell-nowrap">/OFST = *offset*</span> | Applies an offset to the final polygon. For example, if the polygon represents a rectangle, a positive offset creates an inscribing rectangle while a negative offset creates an inscribed rectangle. If the command includes a binary operation between primary and secondary polygon paths then the offset applies to the result of the binary operation. The *offset* parameter is scaled by /SM *scaleFactor*. |
| <span class="table-cell-nowrap">/Q</span> | Quiet mode. Do not print any information in the history area of the command window. |
| <span class="table-cell-nowrap">/RPRC = *rPrecision*</span> |  |
|  | The rounding precision *rPrecision* specifies the maximum distance in scaled units that a line segment can deviate from the exact arc. This applies only when /JTYP=1 and when offseting a polygon. The *rPrecision* parameter is scaled by /SM *scaleFactor*. |
| <span class="table-cell-nowrap">/SM = {*scaleMethod* [,*scaleFactor*]}</span> |  |
|  | Specifies a scaling method and a scaling factor used when converting the input data into the internal integer representation employed by the algorithm. |
|  | *scaleMethod* is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No scaling. Floating point vertex locations are converted to integers by simple truncation:</td></tr></tbody></table>
|  | <code class="igor">Vc = trunc(Vin)</code> |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Multiplication by *scaleFactor* followed by truncation to integer:</td></tr></tbody></table>
|  | <code class="igor">Vc = trunc(Vin*scaleFactor)</code> |
|  |<table class="nested-table"><tbody><tr><td>2:</td><td>Scaling followed by rounding to integer:</td></tr></tbody></table>
|  | <code class="igor">Vc = round(Vin*scaleFactor)</code> |
|  | *scaleFactor* must be a finite positive number and defaults to 1.0. All scaling is reversed on output using multiplication by the reciprocal of *scaleFactor*. Depending on the range of your data you may be able to use a scale factor which improves the resolution of the calculation. For example, if your data are O(1) and you use a scale factor of 10 or 100 the resulting conversion into integers will be more accurate. On the other hand, if your data are O(2^30) a scale factor greater than 1 is not ideal. |
| <span class="table-cell-nowrap">/SPT = {*testPointX,* *testPointY*}</span> |  |
|  | Specifies a single point for testing if the point is inside the primary path polygon. The coordinates of point are scaled using the same scaling as the primary waves. The result of the test is stored in V_value as 0 if that the point is outside the polygon, 1 if that the point that is inside the polygon and 2 if the point is on the boundary of the polygon. |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error reporting. If you use /Z, check the V_Flag output variable to see if the operation succeeded. |

### *Keywords* {#keywords}

|  |  |  |
| --- | --- | --- |
| <span class="table-cell-nowrap">operation = *op*</span> |  |  |
|  | You can omit the operation=*op* pair when you are applying an offset to the primary polygon or when testing for pointsInPoly. Otherwise, *op* is one of the following: |  |
|  | **Intersection** | Computes the intersection of the region defined by the primary path or paths and the region defined by the secondary path or paths. |
|  | **Union** | Computes the union between the region defined by the primary path or paths and the region defined by the secondary path or paths. |
|  | **Difference** | Computes the difference between the region defined by the primary path or paths and the region defined by the secondary path or paths. |
|  | **XOR** | Computes the exclusive OR between the regions defined by the primary path or paths and the regions defined by the secondary path or paths. This includes all regions where either the primary or secondary polygons are filled but not where both are filled. |
|  | **PointInPoly** | Tests if the points specified by *pointsWaves* are inside the target polygon. The results are stored in the unsigned byte wave W_inPoly in the current data folder: 0 for a point outside, 1 for a point inside, and 2 for a point on the boundary. |
|  |  | The target polygon is defined by *primaryWaves*. The tested points are internally scaled with the same scaling method (/SM) that applies to primary waves. You can perform this test on a target polygon that is a result of any binary polygon operation if you only specify the *pointsWaves*, for example: |
|  |  | <code class="igor">PolygonOp operation=union, primaryWaves={wx,wy}, secondarywaves={sx,sy}, pointsWaves={px,py}</code> |
|  | **Area** | Computes the polygon area and stores it in V_area when secondary polygons are not specified. Use the /FA flag to compute the final area if you also want to perform a binary operation between the primary and secondary polygons. |
|  | **CleanPolygon** | Removes vertices from the primary paths that satisfy one of the following conditions: |
|  |  |<table class="nested-table"><tbody><tr><td>1.</td><td>The vertices lie on a co-linear edge. For every three vertices the middle vertex is removed if it lies close enough (see /DIST above) to the edge connecting the vertices on both of its sides.</td></tr><tr><td>2.</td><td>The vertices are situated below a critical distance from an adjacent vertex (see /DIST above).</td></tr></tbody></table>
|  | **MinkowskiDiff** | If the primary and secondary paths represent sets of vectors, the Minkowski difference of the two sets is defined as the set formed by subtracting each vector in the primary set from each vector in the secondary set. |
|  | **MinkowskiSum** | If the primary and secondary paths represent sets of vectors, the Minkowski sum of the two sets is defined as the set formed by adding each vector in the primary set to each vector in the secondary set. |
|  | **Simplify** | Removes self-intersections from the input polygons. In case of touching vertices the resulting polygon is split into two polygons. |
|  | **Reverse** | Reverses the polygon paths. |
| <span class="table-cell-nowrap">pointsWaves = {*pointsXWave*, *pointsYWave*}</span> |  |  |
|  | Specifies a pair of 1D waves that define points for testing pointInPoly. The waves must have the same number type and the same number of points. The polygon that is used in the test is either the primary polygon, when the operation is PointInPoly, or the polygon resulting from the combination of the primary and secondary polygons together with the operation specified by the operation keyword. The waves must contain at least one point. |  |
| <span class="table-cell-nowrap">primaryWaves = {*srcXWave*, *srcYWave*}</span> |  |  |
|  | Specifies the primary path or paths. In case of more than one path, the paths are separated by a NaN in both waves. Both waves must have the same number type and the same number of points. The waves must contain at least 3 points. |  |
| <span class="table-cell-nowrap">secondaryWaves = {*secondaryXWave*, *secondaryYWave*}</span> |  |  |
|  | Specifies a the secondary or clipping path or paths. In case of more than one path, the paths are separated by a NaN in both waves. Both waves must have the same number type and the same number of points. The waves must contain at least 3 points. |  |

### *Details* {#details}
PolygonOp performs various operations on polygon paths that are defined by pairs of 1D real numeric waves. A path is defined by an XY pair of waves that may describe one or more closed polygons. Consecutive polygons are separated by a single NaN value in both path waves.

You must always specify the primary path waves. You must specify the secondary waves if you need to perform a binary polygon operation.

To simplify the computation the input waves are internally mapped into 32-bit signed integer arrays so that vertices correspond to discrete integer pairs (pixels).

To support a broad range of inputs, the operation allows you to specify how the input waves are scaled into integers. Scaling is isotropic; there is currently no support for anamorphic scaling. The scaling factor determines the number of significant figures that remain after conversion to integers. In extreme cases it is advisable to preprocess the polygon waves, e.g., by removing a mean offset and/or applying anamorphic scaling. On output, an inverse scaling is applied with no compensation for the initial truncation or rounding. The inverse scaling is also applied to area calculations.

### *Output Variables* {#output-variables}
PolygonOp sets the following output variables:


|  |  |
| --- | --- |
| V_flag | Zero if the operation succeeds or to a non-zero error code. |
| V_value | The pointInPolyResult result for a single point specified using /SPT. |
| V_area | The area of the resulting polygon corrected for scaling. |
| S_waveNames | Semicolon separated list of the names of the waves created by the operation. |

### *See Also* {#see-also}
[DrawPoly](/igorpro/commands/drawpoly.md), [FindPointsInPoly](/igorpro/commands/findpointsinpoly.md), [PolygonArea](/igorpro/commands/polygonarea.md)

### *Demos* {#demos}
[Open PolygonOp Demo](#igor-pxp/Examples/Feature__Demos__2/PolygonOp__Demo.pxp)