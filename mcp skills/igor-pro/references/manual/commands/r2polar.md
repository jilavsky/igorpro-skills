---
description: "The r2polar function returns a complex value in polar coordinates derived from the complex value z which is assumed to be in rectangular coordinates."
slug: /commands/r2polar
---

<div className="command-signature">

## <strong>r2polar</strong> (<em>z</em>) {#r2polar}

</div>

The r2polar function returns a complex value in polar coordinates derived from the complex value *z* which is assumed to be in rectangular coordinates. The magnitude is stored in the real part and the angle (in radians) is stored in the imaginary part of the returned complex value.

### *Examples* {#examples}
Assume waveIn and waveOut are complex.


```igor
waveOut= r2polar(waveIn)
```

sets each point of waveOut to the polar coordinates derived from the real and imaginary parts of waveIn.

You may get unexpected results if the number of points in waveIn differs from the number of points in waveOut because of interpolation.

### *See Also* {#see-also}
[cmplx](/igorpro/commands/cmplx.md), [conj](/igorpro/commands/conj.md), [imag](/igorpro/commands/imag.md), [p2rect](/igorpro/commands/p2rect.md), [real](/igorpro/commands/real.md)