---
description: "The SetRandomSeed operation seeds the random number generator used for the noise functions listed under Noise Functions."
slug: /commands/setrandomseed
---

<div className="command-signature">

## <strong>SetRandomSeed</strong>  <em>seed</em> {#setrandomseed}

</div>

The SetRandomSeed operation seeds the random number generator used for the noise functions listed under [Noise Functions](/igorpro/analysis/statistics.md#noise-functions).

Use SetRandomSeed if you need "random" numbers that are reproducible. If you don't use SetRandomSeed, the random number generator is initialized using the system clock when Igor starts. This almost guarantees that you will never get the same sequence twice unless you use SetRandomSeed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/BETR[ = *better*]</span> | If *better* is absent or non-zero, a better method is used for seeding the Mersenne Twister random number generator. /BETR is ignored for all other generators. |

### *Parameters* {#parameters}
*seed*  should be a number in the interval (0, 1]. For any given *seed*, enoise or gnoise or any of the other random-number generator functions generates a particular sequence of pseudorandom numbers. Calling SetRandomSeed with the same seed restarts and repeats the sequence.

### *Details* {#details}
Igor's noise functions are listed under [Noise Functions](/igorpro/analysis/statistics.md#noise-functions). The enoise and gnoise functions allow you to choose a random number generator. The other functions always use the Mersenne Twister generator.

How the seed is used internally depends on the generator. For the Linear Congruential Generator the seed is scaled to a 32-bit signed integer. For the Mersenne Twister the seed is scaled to a 32-bit unsigned integer. Both only use the lower 16-bits of the so scaled value for historic reasons.

The Xoshiro256\*\* generator uses all available bits and scales it to an unsigned 64-bit integer.

All generators use the scaled seed value when initializing their internal state tables.

### *See Also* {#see-also}
[enoise](/igorpro/commands/enoise.md), [gnoise](/igorpro/commands/gnoise.md), [Noise Functions](/igorpro/analysis/statistics.md#noise-functions)