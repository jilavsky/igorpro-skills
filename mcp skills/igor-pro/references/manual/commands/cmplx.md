---
description: "The cmplx function returns a complex number whose real component is realPart and whose imaginary component is imagPart."
slug: /commands/cmplx
---

<div className="command-signature">

## <strong>cmplx</strong> (<em>realPart</em>, <em>imagPart</em>) {#cmplx}

</div>

The cmplx function returns a complex number whose real component is *realPart* and whose imaginary component is *imagPart*.

Use this to assign a value to a complex variable or complex wave.

### *Examples* {#examples}
Assume wave1 is complex. Then:


```igor
wave1(0) = cmplx(1,2)
```

sets the Y value of wave1 at x=0 such that its real component is 1 and its imaginary component is 2.

Assuming wave2 and wave3 are real, then:


```igor
wave1 = cmplx(wave2,wave3)
```

sets the real component of wave1 equal to the contents of wave2 and the imaginary component of wave1 equal to the contents of wave3.

You may get unexpected results if the number of points in wave2 or wave3 differs from the number of points in wave1. If wave2 or wave3 is shorter than wave1, the last element of the short wave is copied repeatedly to fill wave1.

### *See Also* {#see-also}
[conj](/igorpro/commands/conj.md), [imag](/igorpro/commands/imag.md), [magsqr](/igorpro/commands/magsqr.md), [p2rect](/igorpro/commands/p2rect.md), [r2polar](/igorpro/commands/r2polar.md), [real](/igorpro/commands/real.md)