---
description: "The ContourZ function returns the interpolated Z value of the named contour plot data displayed in the named graph."
slug: /commands/contourz
---

<div className="command-signature">

## <strong>ContourZ</strong> (<em>graphNameStr</em>, <em>contourNameStr</em>, <em>instance</em>, <em>x</em>, <em>y</em> [,<em>pointFindingTolerance</em>] ) {#contourz}

</div>

The ContourZ function returns the interpolated Z value of the named contour plot data displayed in the named graph.

For gridded contour data, ContourZ  returns the bilinear interpolation of the four surrounding XYZ values.

For XYZ triplet contour data, ContourZ returns the value interpolated from the three surrounding XYZ values identified by the Delaunay triangulation.

### *Parameters* {#parameters}
*graphNameStr* can be "" to specify the topmost graph.

*contourNameStr* is a string containing either the name of the wave displayed as a contour plot in the named graph, or a contour instance name (wave name with "#n" appended to distinguish the nth contour plot of the wave in the graph). You might get a contour instance name from the [ContourNameList](/igorpro/commands/contournamelist.md) function.

If *contourNameStr* contains a wave name, *instance* identifies which contour plot of *contourNameStr* you want information about. *instance* is usually 0 because there is normally only one instance of a wave displayed as a contour plot in a graph. Set *instance* to 1 for information about the second contour plot of *contourNameStr* , etc. If *contourNameStr* is "", then information is returned on the *instance*th contour plot in the graph.

If *contourNameStr* contains an instance name, and *instance* is zero, the instance is taken from *contourNameStr* . If *instance* is greater than zero, the wave name is extracted from *contourNameStr* , and information is returned concerning the *instance*th instance of the wave.

*x* and*y* specify the x and y coordinates of the value to be returned. This may or may not be the location of a data point in the wave selected by *contourNameStr* and *instance.*

For XYZ contours, you may set the optional *pointFindingTolerance* parameter to a small number to more agressively seek out triangulated (possibly perturbed) x/y coordinates near the given *x/y* coordinate.

Set *pointFindingTolerance* =1e-5 to overcome the effects of perturbation (see the perturbation keyword of the [ModifyContour](/igorpro/commands/modifycontour.md) operation).

The default value is 1e-15 to account for rounding errors created by the triangulation scaling (see ModifyContour's equalVoronoiDistances keyword), which works well ModifyContour perturbation=0.

A value of 0 would require an exact match between the scaled *x/y* coordinate and the scaled and possibly perturbed coordinates to return the original z value; that is an unlikely outcome.

### *Details* {#details}
For gridded contour data, ContourZ returns NaN if *x* or *y* falls outside the XY domain of the contour data. If *x* and *y* fall on the contour data grid, the corresponding Z value is returned.

For XYZ triplet contour data, ContourZ returns the null value *if x* or *y* falls outside the XY domain of the contour data. You can set the null value to *v* with this command: ModifyContour *contourName* nullValue=*v* . If *x* and *y* match one of the XYZ triplets, the corresponding Z value from the triplet is returned.

If *x* and *y* match one of the XYZ triplet values, the corresponding Z value from the triplet usually won't be returned because Igor uses the Watson contouring algorithm which perturbs the x and y values by a small random amount. This also means that normally x and y coordinates on the boundary will return a null value about half the time if perturbation is on and *pointFindingTolerance* is greater than 1e-5.

### *Examples* {#examples}
Because ContourZ can interpolate the Z value of the contour data at any x and y coordinates, you can use ContourZ to convert XYZ triplet data into gridded data.


```igor
// Make example XYZ triplet contour data
Make/O/N=50 wx,wy,wz
wx= enoise(2)                           // x = -2 to 2
wy= enoise(2)                           // y = -2 to 2
wz= exp(-(wx[p]*wx[p] + wy[p]*wy[p]))   // XY gaussian, z= 0 to 1

// ContourZ requires a displayed contour data set
Display; AppendXYZContour wz vs {wx,wy};DelayUpdate
ModifyContour wz autoLevels={*,*,0}
ModifyContour wz xymarkers=1            // show the X and Y locations

// Set the null (out-of-XY domain) value
ModifyContour wz nullValue=NaN          // default is min(wz) - 1

// Convert to grid: Make matrix that spans X and Y
Make/O/N=(30,30) matrix
SetScale/I x, -2, 2, "", matrix
SetScale/I y, -2, 2, "", matrix
matrix= ContourZ("","wz",0,x,y)         // or = ContourZ("","",0,x,y)
AppendImage matrix
```

### *See Also* {#see-also}
[AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md), [AppendXYZContour](/igorpro/commands/appendxyzcontour.md), [ModifyContour](/igorpro/commands/modifycontour.md), [FindContour](/igorpro/commands/findcontour.md)

[zcsr](/igorpro/commands/zcsr.md), [ContourInfo](/igorpro/commands/contourinfo.md)

### *References* {#references}
Watson, David F., *Contouring: A Guide To The Analysis and Display of Spatial Data*, Pergamon, 1992.