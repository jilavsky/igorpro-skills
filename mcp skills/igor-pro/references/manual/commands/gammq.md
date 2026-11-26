---
description: "The gammq function returns the regularized incomplete gamma function 1-P(a,x), where a > 0, x >= 0."
slug: /commands/gammq
---

<div className="command-signature">

## <strong>gammq</strong> (<em>a</em>, <em>x</em>  [, <em>accuracy</em> ]) {#gammq}

</div>

The gammq function returns the regularized incomplete gamma function 1-P(*a*,*x*), where *a* > 0, *x* >= 0. Optionally, *accuracy* can be used to specify the desired fractional accuracy. Same as gammaInc(a, x)/gamma(a).

### *Details* {#details}
The *accuracy* parameter specifies the fractional accuracy that you desire. That is, if you set *accuracy* to 1e-7, that means that you wish that the absolute value of (f<sub>actual</sub>-f<sub>returned</sub>)/f<sub>actual</sub> be less than 10<sup>-</sup><sup>7</sup>.

For backward compatibility, if you don't include *accuracy* , gammq uses older code that is slower for a equivalent accuracy, and cannot achieve as high accuracy.

The ability of gammq to return a value having full fractional accuracy is limited by double-precision calculations. This means that it will mostly have fractional accuracy better than about 10<sup>-</sup><sup>15</sup>, but this is not guaranteed, especially for extreme values of *a* and *x*.

### *See Also* {#see-also}
[gammaInc](/igorpro/commands/gammainc.md), [gammq](/igorpro/commands/gammq.md)