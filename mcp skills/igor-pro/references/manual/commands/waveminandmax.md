---
description: "The WaveMinAndMax function returns the minimum and maximum values in the wave for points between x=x1 to x=x2, inclusive."
slug: /commands/waveminandmax
---

<div className="command-signature">

## <strong>WaveMinAndMax</strong> (<em>wave</em> [, <em>x1</em>, <em>x2</em>]) {#waveminandmax}

</div>

The WaveMinAndMax function returns the minimum and maximum values in the wave for points between x=*x1* to x=*x2*, inclusive.

WaveMinAndMax must be called from a function, not from the command line, because it uses multiple return syntax as shown in the example below.

WaveMinAndMax was added in Igor Pro 9.00.

### *Details* {#details}
If *x1* and *x2* are omitted, they default to -inf and +inf.

The X scaling of the wave is used only to locate the points nearest to x=*x1* and x=*x2*. To use point indexing, replace *x1* with "pnt2x(*wave*,*pointNumber1*)", and a similar expression for *x2*. The resulting point numbers are clipped to the range 0..n where n is the numpnts(*wave* )-1.

NaN values in the wave are ignored.

### *Example* {#example}

```igor
Function DemoWaveMinAndMax()
	Make/FREE wave0 = p
	wave0[0] = NaN	// NaN values are ignored
	SetScale/P x, 0, 0.1, "s", wave0
	double minValue, maxValue
	
	[minValue, maxValue] = WaveMinAndMax(wave0)
	Printf "Entire wave: min=%g, max=%g\r", minValue, maxValue

	[minValue, maxValue] = WaveMinAndMax(wave0, 5, 10)
	Printf "From x=5 to x=10: min=%g, max=%g\r", minValue, maxValue
End
```

### *See Also* {#see-also}
[WaveMin](/igorpro/commands/wavemin.md), [WaveMax](/igorpro/commands/wavemax.md), [WaveStats](/igorpro/commands/wavestats.md)