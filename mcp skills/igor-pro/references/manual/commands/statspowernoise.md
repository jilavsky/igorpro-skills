---
description: "The StatsPowerNoise function returns a pseudorandom value from the power distribution function with probability distribution."
slug: /commands/statspowernoise
---

<div className="command-signature">

## <strong>StatsPowerNoise</strong> (<em>b</em>, <em>c</em>) {#statspowernoise}

</div>

The StatsPowerNoise function returns a pseudorandom value from the power distribution function with probability distribution:

$$
\displaystyle f(x ; b, c)=\frac{c}{x}\left(\frac{x}{b}\right)^{c}.
$$

The random number generator initializes using the system clock when Igor Pro starts. This almost guarantees that you will never repeat a sequence. For repeatable "random" numbers, use [SetRandomSeed](/igorpro/commands/setrandomseed.md). The algorithm uses the Mersenne Twister random number generator.

### *See Also* {#see-also}
[SetRandomSeed](/igorpro/commands/setrandomseed.md), [StatsPowerCDF](/igorpro/commands/statspowercdf.md), [StatsPowerPDF](/igorpro/commands/statspowerpdf.md), [StatsInvPowerCDF](/igorpro/commands/statsinvpowercdf.md)

[Noise Functions](/igorpro/analysis/statistics.md#noise-functions), [Statistical Analysis](/igorpro/analysis/statistics.md)