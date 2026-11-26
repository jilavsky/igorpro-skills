---
description: "The rightx function returns the X value corresponding to point N of the named 1D wave of length N."
slug: /commands/rightx
---

<div className="command-signature">

## <strong>rightx</strong> (<em>waveName</em>) {#rightx}

</div>

The rightx function returns the X value corresponding to point N of the named 1D wave of length N.

### *Details* {#details}
Note that the point numbers in a wave run from 0 to N-1 so there is no point with this X value. To get the X value of the last point in a wave (point N-1), use the following:


```igor
pnt2x(waveName,numpnts(waveName)-1)	// N = numpnts(waveName)
```

which is more accurate than:


```igor
rightx(waveName) - deltax(waveName)
```

The rightx function is not multidimensional aware. The equivalent information for any dimension can be calculated this way:

*IndexN* = DimSize(*wave*, *dim*)*DimDelta(*wave*, *dim*) + DimOffset(*wave*, *dim*)

Here *IndexN* is the value of the scaled dimension index corresponding to element N of the dimension *dim* in a wave named *wave* that has N elements in that dimension.

### *See Also* {#see-also}
[deltax](/igorpro/commands/deltax.md), [leftx](/igorpro/commands/leftx.md), [pnt2x](/igorpro/commands/pnt2x.md), [numpnts](/igorpro/commands/numpnts.md)

For an explanation of waves and X scaling, see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).

For multidimensional waves, see [DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md), and [DimSize](/igorpro/commands/dimsize.md).