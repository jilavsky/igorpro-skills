---
description: "The PolygonArea function returns the area of a simple, closed, convex or nonconvex planar polygon described by consecutive vertices in xWave and yWave."
slug: /commands/polygonarea
---

<div className="command-signature">

## <strong>PolygonArea</strong> (<em>xWave</em>, <em>yWave</em>) {#polygonarea}

</div>

The PolygonArea function returns the area of a simple, closed, convex or nonconvex planar polygon described by consecutive vertices in *xWave* and *yWave*.

A simple polygon has no internal "holes" and its boundary curve does not intersect itself. Both *xWave* and *yWave* must be 1D, real, numerical waves of the same dimensions. The minimum number of vertices is 3. The function uses the shoelace algorithm to compute the area (see theorem 1.3.3 in the reference below). If there is any error in the input, the function returns NaN.

### *Example* {#example}

```igor
Function estimatePi(num)
	Variable num

	Make/O/N=(num+1) xxx,yyy
	xxx=sin(2*pi*x/num)
	yyy=cos(2*pi*x/num)

	Printf "Relative Error=%g\r",(pi-PolygonArea(xxx,yyy))/pi
End
```

### *See Also* {#see-also}
[areaXY](/igorpro/commands/areaxy.md), [faverageXY](/igorpro/commands/faveragexy.md), [PolygonOp](/igorpro/commands/polygonop.md)

### *References* {#references}
O'Rourke, Joseph, *Computational Geometry in C*, 2nd ed., Cambridge University Press, New York, 1998.