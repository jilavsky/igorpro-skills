---
description: "The area function returns the signed area between the named wave and the line y=0 from x=x1 to x=x2 using trapezoidal integration, accounting for the wave's X…"
slug: /commands/area
---

<div className="command-signature">

## <strong>area</strong> (<em>waveName</em>  [, <em>x1</em>, <em>x2</em>  ] ) {#area}

</div>

The area function returns the signed area between the named wave and the line y=0 from x=*x1* to x=*x2* using trapezoidal integration, accounting for the wave's X scaling. If your data are in the form of an XY pair of waves, see [areaXY](/igorpro/commands/areaxy.md).

### *Details* {#details}
If *x1* and *x2* are not specified, they default to -[inf](/igorpro/commands/inf.md) and +inf, respectively.

If *x1* or *x2* are not within the X range of *waveName*, area limits them to the nearest X range limit of *waveName*.

If any values in the X range are NaN, area returns NaN.

The function returns NaN if the input wave has zero points.

Reversing the order of *x1* and *x2* changes the sign of the returned area.

The area function is intended to work on 1D real or complex waves only.

The area function returns a complex result for a complex input wave. The real part of the result is the area of the real components in the input wave, and the imaginary part of the result is the area of the imaginary components.

### *Examples* {#examples}

```igor
Make/O/N=100 data;SetScale/I x 0,Pi,data
data=sin(x)
Print area(data,0,Pi)     // the entire X range, and no more
Print area(data)          // same as -infinity to +infinity
Print area(data,Inf,-Inf) // +infinity to -infinity
```

The following is printed to the history area:


```igor
Print area(data,0,Pi)     // the entire X range, and no more
  1.99983
Print area(data)          // same as -infinity to +infinity
  1.99983
Print area(data,Inf,-Inf) // +infinity to -infinity
  -1.99983
```

The -Inf value was limited to 0 and Inf was limited to Pi to keep them within the X range of data.

### *See Also* {#see-also}
See the figure "Comparison of area, faverage and mean functions over interval (12.75,13.32)", in the Examples section of the [faverage](/igorpro/commands/faverage.md) function.

[Integrate](/igorpro/commands/integrate.md), [areaXY](/igorpro/commands/areaxy.md), [faverage](/igorpro/commands/faverage.md), [faverageXY](/igorpro/commands/faveragexy.md), [PolygonArea](/igorpro/commands/polygonarea.md)