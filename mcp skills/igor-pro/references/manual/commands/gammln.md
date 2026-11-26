---
description: "The gammln function returns the natural log of the gamma function of num, where."
slug: /commands/gammln
---

<div className="command-signature">

## <strong>gammln</strong> (<em>num</em>  [, <em>accuracy</em> ]) {#gammln}

</div>

The gammln function returns the natural log of the gamma function of *num*, where

*num* > 0. If *num* is complex, it returns a complex result. Optionally, *accuracy* can be used to specify the desired fractional accuracy. If *num* is complex, a complex result is returned. In this case, *accuracy* is ignored.

### *Details* {#details}
The *accuracy* parameter specifies the fractional accuracy that you desire. That is, if you set *accuracy* to 1e-7, that means that you wish that the absolute value of (f<sub>actual</sub>-f<sub>returned</sub>)/f<sub>actual</sub> be less than 10<sup>-</sup><sup>7</sup>.

For backward compatibility, if you don't include *accuracy* , gammln uses older code that achieves an accuracy of about 2x10<sup>-</sup><sup>10</sup>.

With *accuracy*, newer code is used that is both faster and more accurate. The output has fractional accuracy better than 1x10<sup>-</sup><sup>15</sup> except for values near zero, where the absolute accuracy (f<sub>actual</sub>-f<sub>returned</sub>) is better than 2x10<sup>-</sup><sup>16</sup>.

The speed of calculation depends only weakly on accuracy. Higher accuracy is significantly slower than lower accuracy only for *num* between 6 and about 10.

### *See Also* {#see-also}
[gamma](/igorpro/commands/gamma.md)