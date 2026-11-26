---
description: "The mean function returns the arithmetic mean of the wave for points from x=x1 to x=x2."
slug: /commands/mean
---

<div className="command-signature">

## <strong>mean</strong> (<em>waveName</em> [, <em>x1</em>, <em>x2</em>]) {#mean}

</div>

The mean function returns the arithmetic mean of the wave for points from x=*x1* to x=*x2*.

### *Details* {#details}
If *x1* and *x2* are not specified, they default to -INF and +INF, respectively.

The wave values from *x1* to *x2* are summed, and the result divided by the number of points in the range.

The X scaling of the wave is used only to locate the points nearest to x=*x1* and x=*x2*. To use point indexing, replace *x1* with "pnt2x(*waveName*,*pointNumber1* )", and a similar expression for *x2*.

If the points nearest to *x1* or *x2* are not within the point range of 0 to numpnts(*waveName* )-1, mean limits them to the nearest of point 0 or point numpnts(waveName)-1.

If any values in the point range are NaN, mean returns NaN.

The function returns NaN if the input wave has zero points.

Unlike the area function, reversing the order of *x1* and *x2* does not change the sign of the returned value.

The mean function is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *Examples* {#examples}

```igor
Make/O/N=100 data; SetScale/I x 0,Pi,data
data=sin(x)
Print mean(data,0,Pi)     // the entire point range, and no more
Print mean(data)          // same as -infinity to +infinity
Print mean(data,Inf,-Inf) // +infinity to -infinity
```

The following is printed to the history area:


```igor
Print mean(data,0,Pi)     // the entire point range, and no more
  0.630201
Print mean(data)          // same as -infinity to +infinity
  0.630201
Print mean(data,Inf,-Inf) // +infinity to -infinity
  0.630201
```

### *See Also* {#see-also}
[Variance](/igorpro/commands/variance.md), [WaveStats](/igorpro/commands/wavestats.md), [median](/igorpro/commands/median.md), [APMath](/igorpro/commands/apmath.md)

The figure "Comparison of area, faverage and mean functions over interval (12.75,13.32)", in the Details section of [faverage](/igorpro/commands/faverage.md).