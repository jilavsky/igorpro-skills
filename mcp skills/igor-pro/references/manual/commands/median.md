---
description: "The median function returns the median value of the wave for points from x=x1 to x=x2."
slug: /commands/median
---

<div className="command-signature">

## <strong>median</strong> (<em>waveName</em> [, <em>x1</em>, <em>x2</em>]) {#median}

</div>

The median function returns the median value of the wave for points from x=*x1* to x=*x2* .

The median function was added in Igor Pro 7.00.

### *Details* {#details}
If you omit *x1* and *x2*, they default to -INF and +INF, respectively.

The X scaling of the wave is used only to locate the points nearest to x=*x1* and x=*x2*. To use point indexing, replace *x1* with "pnt2x(*waveName*,*pointNumber1*)", and a similar expression for *x2*.

If the points nearest to *x1* or *x2* are outside the point range of 0 to numpnts(*waveName* )-1, median limits them to the nearest of point 0 or point numpnts(waveName)-1.

If the wave contains NaNs they are skipped.

The function returns NaN if the input wave has zero non-NaN points.

### *See Also* {#see-also}
[Mean](/igorpro/commands/mean.md), [Variance](/igorpro/commands/variance.md), [StatsQuantiles](/igorpro/commands/statsquantiles.md), [WaveStats](/igorpro/commands/wavestats.md)