---
description: "The betai function returns the regularized incomplete beta function Ix (a, b)."
slug: /commands/betai
---

<div className="command-signature">

## <strong>betai</strong> (<em>a</em>, <em>b</em>, <em>x</em> [, <em>accuracy</em> ]) {#betai}

</div>

The betai function returns the regularized incomplete beta function I<sub>x </sub>(*a*, *b* ),

$$
\displaystyle I_{x}(a, b)=\frac{B(x ; a, b)}{B(a, b)} .
$$

Here

$$
\displaystyle B(x ; a, b)=\int_{0}^{x} t^{a-1}(1-t)^{b-1} d t .
$$

where *a*, *b* > 0, and 0 <= *x* <= 1.

Optionally, *accuracy* can be used to specify the desired fractional accuracy.

### *Details* {#details}
The *accuracy* parameter specifies the fractional accuracy that you desire. That is, if you set *accuracy* to 1e-7, that means that you wish that the absolute value of (f<sub>actual</sub>-f<sub>returned</sub>)/f<sub>actual</sub> be less than 10<sup>-</sup><sup>7</sup>.

Larger values of *accuracy* (poorer accuracy) result in evaluation of fewer terms of a series, which means the function executes somewhat faster.

A single-precision level of accuracy is about 3x10<sup>-</sup><sup>7</sup>, double-precision about 2x10<sup>-</sup><sup>16</sup>. The betai function will return full double-precision accuracy for small values of a and b. Achievable accuracy declines as a and b increase:

| a | b | x | betai | Accuracy Achievable |
| --- | --- | --- | --- | --- |
| 1 | 1.5 | 0.5 | 0.646447 | full double precision (2x10<sup>-</sup><sup>16</sup>) |
| 8 | 10 | 0.5 | 0.685470 | 6x10<sup>-</sup><sup>16</sup> |
| 20 | 21 | 0.5 | 0.562685 | 2x10<sup>-</sup><sup>15</sup> |
| 20 | 21 | 0.1 | 1.87186e-10 | 5x10<sup>-</sup><sup>15</sup> |