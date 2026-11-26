---
description: "The faverage function returns the trapezoidal average value of the named wave from x=x1 to x=x2."
slug: /commands/faverage
---

<div className="command-signature">

## <strong>faverage</strong> (<em>waveName</em> [, <em>x1</em>, <em>x2</em>  ] ) {#faverage}

</div>

The faverage function returns the trapezoidal average value of the named wave from x=*x1* to x=*x2*.

If your data are in the form of an XY pair of waves, see [faverageXY](/igorpro/commands/faveragexy.md).

### *Details* {#details}
If *x1* and *x2* are not specified, they default to -inf and +inf, respectively.

If *x1* or *x2* are not within the X range of *waveName*, faverage limits them to the nearest X range limit of *waveName*.

faverage returns the area divided by (*x2* -*x1* ). In other words, the X scaling of *waveName* is eliminated when computing the average.

If any values in the X range are NaN, faverage returns NaN.

Unlike the [area](/igorpro/commands/area.md) function reversing the order of *x1* and *x2* does not change the sign of the returned value.

The faverage function is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

The faverage function returns a complex result for a complex input wave. The real part of the result is the average of the real components in the input wave and the imaginary part of the result is the average of the imaginary components.

### *Examples* {#examples}
**Comparison of area, faverage and mean functions over interval (12.75,13.32)**

<img src="Images/faverage/faverage_1.png" width="100%"/>

```igor
area(wave,12.75,13.32)      = 0.05 * (43+55)/2      // first trapezoid
                            + 0.20 * (55+88)/2      // second trapezoid
                            + 0.20 * (88+100)/2     // third trapezoid
                            + 0.12 * (100+92.2)/2   // fourth trapezoid
                            = 47.082

faverage(wave,12.75,13.32)  = area(wave,12.75,13.32)/(13.32-12.75)
                            = 47.082/0.57 = 82.6

mean(wave,12.75,13.32)      = (55+88+100+87)/4 = 82.5
```

### *See Also* {#see-also}
[Integrate](/igorpro/commands/integrate.md), [area](/igorpro/commands/area.md), [areaXY](/igorpro/commands/areaxy.md), [faverageXY](/igorpro/commands/faveragexy.md), [PolygonArea](/igorpro/commands/polygonarea.md)