---
description: "The faverageXY function returns the trapezoidal average value of YWaveName from x=x1 to x=x2, using X values from XWaveName."
slug: /commands/faveragexy
---

<div className="command-signature">

## <strong>faverageXY</strong> (<em>XWaveName</em>, <em>YWaveName</em> [, <em>x1</em>, <em>x2</em> ]) {#faveragexy}

</div>

The faverageXY function returns the trapezoidal average value of *YWaveName* from x=*x1* to x=*x2*, using X values from *XWaveName*.

This function operates identically to [faverage](/igorpro/commands/faverage.md), except that it uses an XY pair of waves for X and Y values and it does not work with complex waves.

### *Details* {#details}
If *x1* and *x2* are not specified, they default to -[inf](/igorpro/commands/inf.md) and +inf, respectively.

If *x1* or *x2* are not within the X range of *XWaveName*, faverageXY limits them to the nearest X range limit of *XWaveName*.

faverageXY returns the area divided by (*x2* -*x1*).

If any values in the X range are NaN, faverageXY returns NaN.

Reversing the order of *x1* and *x2* does not change the sign of the returned value.

The values in *XWaveName* may be increasing or decreasing. faverageXY assumes that the values in *XWaveName* are monotonic. If they are not monotonic, Igor does not complain, but the result is not meaningful.

The faverageXY function is not multidimensional aware. See [Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md), particularly [Analysis on Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md#analysis-on-multidimensional-waves) for details.

### *See Also* {#see-also}
[Integrate](/igorpro/commands/integrate.md), [area](/igorpro/commands/area.md), [areaXY](/igorpro/commands/areaxy.md), [faverage](/igorpro/commands/faverage.md), [PolygonArea](/igorpro/commands/polygonarea.md)