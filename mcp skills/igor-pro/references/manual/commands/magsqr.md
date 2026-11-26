---
description: "The magsqr function returns the sum of the squares of the real and imaginary parts of the complex number z, that is, the magnitude squared."
slug: /commands/magsqr
---

<div className="command-signature">

## <strong>magsqr</strong> (<em>z</em>) {#magsqr}

</div>

The magsqr function returns the sum of the squares of the real and imaginary parts of the complex number *z*, that is, the magnitude squared.

### *Examples* {#examples}
Assume waveCmplx is complex and waveReal is real.


```igor
waveReal= sqrt(magsqr(waveCmplx))
```

sets each point of waveReal to the magnitude of the complex points in waveCmplx.

You may get unexpected results if the number of points in waveCmplx differs from the number of points in waveReal. See [Mismatched Waves](/igorpro/igor-basics/waves.md#mismatched-waves) for details.

### *See Also* {#see-also}
[cabs](/igorpro/commands/cabs.md)

WaveMetrics provides Igor Technical Note 006, "DSP Support Macros" which uses the magsqr function to compute the magnitude of FFT data, and Power Spectral Density with options such as windowing and segmenting. See the Technical Notes folder. Some of the techniques discussed there are available as Igor procedure files in the WaveMetrics Procedures:Analysis folder.

### *Demos* {#demos}
[Open PSD Demo](#igor-pxp/Examples/Analysis/PSD__Demo.pxp)