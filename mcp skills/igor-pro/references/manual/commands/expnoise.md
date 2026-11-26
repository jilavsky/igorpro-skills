---
description: "The expNoise function returns a pseudo-random value from an exponential distribution whose average and standard deviation are b and the probability…"
slug: /commands/expnoise
---

<div className="command-signature">

## <strong>expNoise</strong> (<em>b</em>) {#expnoise}

</div>

The expNoise function returns a pseudo-random value from an exponential distribution whose average and standard deviation are *b* and the probability distribution function is

$$
\displaystyle f(x)=\frac{1}{b} \exp \left(-\frac{x}{b}\right) .
$$

The random number generator initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat a sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator.

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)