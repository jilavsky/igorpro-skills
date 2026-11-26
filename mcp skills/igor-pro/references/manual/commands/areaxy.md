---
description: "The areaXY function returns the signed area between the named YWaveName and the line y=0 from x=x1 to x=x2 using trapezoidal integration, using X values…"
slug: /commands/areaxy
---

<div className="command-signature">

## <strong>areaXY</strong> (<em>XWaveName</em>, <em>YWaveName</em>  [, <em>x1</em>, <em>x2</em>  ] ) {#areaxy}

</div>

The areaXY function returns the signed area between the named YWaveName and the line y=0 from x=x1  to x=x2  using trapezoidal integration, using X values supplied by XWaveName.

This function is identical to the [area](/igorpro/commands/area.md) function except that it works on an XY wave pair and does not work with complex waves.

### *Details* {#details}
If *x1* and *x2* are not specified, they default to -[inf](/igorpro/commands/inf.md) and +inf, respectively.

If *x1* or *x2* are not within the X range of *XWaveName*, areaXY limits them to the nearest X range limit of *XWaveName*.

If any values in the Y range are NaN, areaXY returns NaN.

If any values in the entire X wave are NaN, areaXY returns NaN.

The function returns NaN if the input wave has zero points.

Reversing the order of *x1* and *x2* changes the sign of the returned area.

If *x1* or *x2* are not found in *XWaveName*, a Y value is found by linear interpolation based on the two bracketing X values and the corresponding values from *YWaveName*.

The values in *XWaveName* may be increasing or decreasing. AreaXY assumes that the values in *XWaveName* are monotonic. If they are not monotonic, Igor does not complain, but the result is not meaningful.

See the figure "Comparison of area, faverage and mean functions over interval (12.75,13.32)", in the Details section of the faverage function.

The areaXY operation is intended to work on 1D waves only.

### *Examples* {#examples}

```igor
Make/O/N=101 Xdata, Ydata
Xdata = x*pi/100
Ydata = sin(Xdata[p])
Print areaXY(Xdata, Ydata,0,Pi)     // the entire X range, and no more
Print areaXY(Xdata, Ydata)          // same as -infinity to +infinity
Print areaXY(Xdata, Ydata,Inf,-Inf) // +infinity to -infinity
```

The following is printed to the history area:


```igor
Print areaXY(Xdata, Ydata,0,Pi)     // the entire X range, and no more
  1.99984
Print areaXY(Xdata, Ydata)          // same as -infinity to +infinity
  1.99984
Print areaXY(Xdata, Ydata,Inf,-Inf) // +infinity to -infinity
  -1.99984
```

The -Inf value was limited to 0 and Inf was limited to Pi to keep them within the X range of data.

### *See Also* {#see-also}
[Integrate](/igorpro/commands/integrate.md), [area](/igorpro/commands/area.md), [faverage](/igorpro/commands/faverage.md), [faverageXY](/igorpro/commands/faveragexy.md), [PolygonArea](/igorpro/commands/polygonarea.md)