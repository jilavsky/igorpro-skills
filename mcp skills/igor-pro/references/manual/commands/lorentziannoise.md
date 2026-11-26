---
description: "The function returns a pseudo-random value from a Lorentzian distribution."
slug: /commands/lorentziannoise
---

<div className="command-signature">

## <strong>lorentzianNoise</strong> (<em>a</em>, <em>b</em>) {#lorentziannoise}

</div>

The function returns a pseudo-random value from a Lorentzian distribution

$$
\displaystyle f(x)=\frac{1}{\pi} \frac{(b / 2)}{(x-a)^{2}+(b / 2)^{2}} .
$$

Here *a*  is the center and *b*  is the full line width at half maximum (FWHM).

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [enoise](/igorpro/commands/enoise.md), [gnoise](/igorpro/commands/gnoise.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)