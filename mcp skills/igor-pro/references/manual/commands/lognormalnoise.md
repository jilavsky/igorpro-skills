---
description: "The logNormalNoise function returns a pseudo-random value from the lognormal distribution function whose probability distribution function is."
slug: /commands/lognormalnoise
---

<div className="command-signature">

## <strong>logNormalNoise</strong> (<em>m</em>,<em>s</em>) {#lognormalnoise}

</div>

The logNormalNoise function returns a pseudo-random value from the lognormal distribution function whose probability distribution function is

$$
\displaystyle f(x, m, s)=\frac{1}{x s \sqrt{2 \pi}} \exp \left\{-\frac{[\ln (x)-m]^{2}}{2 s^{2}}\right\},
$$

with a mean

$$
\displaystyle \exp \left(m+\frac{1}{2} s^{2}\right),
$$

and variance

$$
\displaystyle \exp \left(2 m+s^{2}\right)\left[\exp \left(s^{2}\right)-1\right] .
$$

The random number generator initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat a sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator.

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)