---
description: "The WaveMin function returns the minimum value in the wave for points between x=x1 to x=x2, inclusive."
slug: /commands/wavemin
---

<div className="command-signature">

## <strong>WaveMin</strong> (<em>waveName</em> [, <em>x1</em>, <em>x2</em>]) {#wavemin}

</div>

The WaveMin function returns the minimum value in the wave for points between x=*x1* to x=*x2*, inclusive.

### *Details* {#details}
If *x1* and *x2* are not specified, they default to -[inf](/igorpro/commands/inf.md) and +inf, respectively.

The X scaling of the wave is used only to locate the points nearest to x=*x1* and x=*x2*. To use point indexing, replace *x1* with "pnt2x(*waveName*,*pointNumber1* )", and a similar expression for *x2*.

If the points nearest to *x1* or *x2* are not within the point range of 0 to numpnts(*waveName* )-1, WaveMin limits them to the nearest of point 0 or point numpnts(waveName)-1.

NaN values in the wave are ignored.

### *See Also* {#see-also}
[WaveMax](/igorpro/commands/wavemax.md), [WaveMinAndMax](/igorpro/commands/waveminandmax.md), [WaveStats](/igorpro/commands/wavestats.md)