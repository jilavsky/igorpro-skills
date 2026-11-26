---
description: "PrimeFactors calculates the prime factors of inNumber. By default factors are printed in the history and are also stored in the wave W_PrimeFactors in the…"
slug: /commands/primefactors
---

<div className="command-signature">

## <strong>PrimeFactors</strong>  [/Q]  <em>inNumber</em> {#primefactors}

</div>

PrimeFactors calculates the prime factors of *inNumber*. By default factors are printed in the history and are also stored in the wave W_PrimeFactors in the current data folder. On input, inNumber is converted into an unsigned 64-bit integer. The largest number that this operation can handle is 2<sup>53</sup>-1.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *fWave*</span> | Specify the output wave for the prime factors. If you do not specify this flag, the operation saves the data in the wave W_PrimeFactors in the current data folder. |
|  | This flag was added in Igor Pro 10. |




|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination wave as a free wave. |
|  | /FREE is allowed only in functions, and only if the destination wave is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/Q</span> | Suppresses printing of factors in the history area. |

### *Details* {#details}
The largest number that this operation can handle is 2<sup>53</sup>-1.

### *See Also* {#see-also}
[gcd](/igorpro/commands/gcd.md), [RatioFromNumber](/igorpro/commands/ratiofromnumber.md)