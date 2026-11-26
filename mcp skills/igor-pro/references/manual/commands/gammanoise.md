---
description: "The gammaNoise function returns a pseudo-random value from the gamma distribution."
slug: /commands/gammanoise
---

<div className="command-signature">

## <strong>gammaNoise</strong> (<em>a</em> [,<em>b</em> ]) {#gammanoise}

</div>

The gammaNoise function returns a pseudo-random value from the gamma distribution

$$
\displaystyle f(x)=\frac{x^{a-1} \exp \left(-\frac{x}{b}\right)}{b^{a} \Gamma(a)}, \quad x>0, a>0, b>0,
$$

whose mean is ab and variance is ab<sup>2</sup>. For backward compatibility you can omit the parameter b in which case its value is set to 1. When a→1 gammaNoise reduces to [expNoise](/igorpro/commands/expnoise.md).

The random number generator initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat a sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator.

### *References* {#references}
Marsaglia, G., and W. W. Tsang, *ACM*, *26*, 363-372, 2000.

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)