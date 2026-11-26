---
description: "The p2rect function returns a complex value in rectangular coordinates derived from the complex value z which is assumed to be in polar coordinates (magnitude…"
slug: /commands/p2rect
---

<div className="command-signature">

## <strong>p2rect</strong> (<em>z</em>)  {#p2rect}

</div>

The p2rect function returns a complex value in rectangular coordinates derived from the complex value *z* which is assumed to be in polar coordinates (magnitude is stored in the real part and the angle, in radians, in the imaginary part of *z*).

### *Examples* {#examples}
Assume waveIn and waveOut are complex.


```igor
waveOut = p2rect(waveIn)
```

sets each point of waveOut to the rectangular coordinates derived from the magnitude in the real part and the angle (in radians) in the imaginary part of the points in waveIn.

You may get unexpected results if the number of points in waveIn differs from the number of points in waveOut.

### *See Also* {#see-also}
[cmplx](/igorpro/commands/cmplx.md), [conj](/igorpro/commands/conj.md), [imag](/igorpro/commands/imag.md), [r2polar](/igorpro/commands/r2polar.md), [real](/igorpro/commands/real.md)