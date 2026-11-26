---
description: "The RatioFromNumber operation computes two integers whose ratio is equal to num +/- maxError. The ratio is returned in variables V_numerator and V_denominator."
slug: /commands/ratiofromnumber
---

<div className="command-signature">

## <strong>RatioFromNumber</strong>  [/MERR=<em>maxError</em> /MITS=<em>maxIterations</em> /V[=<em>v</em> ]] <em>num</em> {#ratiofromnumber}

</div>

The RatioFromNumber operation computes two integers whose ratio is equal to *num* +/- *maxError*. The ratio is returned in variables V_numerator and V_denominator.

### *Parameters* {#parameters}
*num* is the number to approximate by V_numerator/V_denominator.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/MERR = *maxError*</span> |  |
|  | Specifies the maximum tolerable error. The computed ratio differs from *num* by no more than *maxError* (default value is *num*\*1e-6). |
|  | *maxError* must be a value between 0 and num. See Details about setting *maxError* to 0. |
| <span class="table-cell-nowrap">/MITS = *maxIterations*</span> |  |
|  | Keeps returned values small by specifying a small number for *maxIterations*. |
|  | *maxIterations* must be a value between 1 and 32767 (default is 100). |
| <span class="table-cell-nowrap">/V[ = *v* ]</span> | Prints output variables to history. |
|  |<table class="nested-table"><tbody><tr><td>*v*&nbsp;=1:</td><td>Prints variables (same as /V).</td></tr><tr><td>*v*&nbsp;=0:</td><td>Nothing printed (same as no /V).</td></tr></tbody></table>

### *Details* {#details}
The ratio is computed by continued fraction expansion and recurrence relations for the convergents and checking *num* - (V_numerator/V_denominator) against *maxError* .

Setting *maxError* = 0 computes a maximally accurate ratio. The returned values can be surprisingly large:


```igor
RatioFromNumber/V/MERR=0 (1/1666)
  V_numerator= 4398046511104; V_denominator= 7.3271454874993e+15; 
  ratio= 0.00060024009603842; V_difference= 0;
```

Using the default /MERR returns the expected 1 and 1666. The difference is attributable to floating-point roundoff errors.

The ratio is computed by continued fraction expansion and recurrence relations for the convergents and checking *num* - (V_numerator/V_denominator) against /MERR.

### *Output Variables* {#output-variables}
RatioFromNumber sets the following output variables:


|  |  |
| --- | --- |
| V_difference | V_numerator/V_denominator - *num* |
|  | (positive if the approximation is too big). |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>V_difference less than or equal to /MERR.</td></tr><tr><td>1:</td><td>V_difference greater than /MERR.</td></tr></tbody></table>
| V_numerator, V_denominator |  |
|  | Values for the numerator and denominator. The ratio of V_numerator/V_denominator approximates *num*. |
| V_iterations | The number of iterations actually used. |

RatioFromNumber prints the output variables if you specify /V or /V=1 but only when running in the main thread.

### *Examples* {#examples}

```igor
RatioFromNumber/V pi
  V_numerator= 355; V_denominator= 113; ratio= 3.141592920354; 
  V_difference= 2.6676418940497e-07; V_iterations= 3;

RatioFromNumber/V/MITS=2 pi
  V_numerator= 22; V_denominator= 7; ratio= 3.1428571428571; 
  V_difference= 0.0012644892673497; V_iterations= 1;
```

### *See Also* {#see-also}
[gcd](/igorpro/commands/gcd.md), [trunc](/igorpro/commands/trunc.md), [PrimeFactors](/igorpro/commands/primefactors.md)