---
description: "The erfc function returns the complementary error function of num (erfc(x) = 1 - erf(x))."
slug: /commands/erfc
---

<div className="command-signature">

## <strong>erfc</strong> (<em>num</em>  [, <em>accuracy</em> ]) {#erfc}

</div>

The erfc function returns the complementary error function of *num* (erfc(x) = 1 - erf(x)). Optionally, *accuracy* can be used to specify the desired fractional accuracy.

In complex expressions the complementary error function is

$$
\displaystyle \operatorname{erfc}(z)=1-\operatorname{erf}(z)=1-\frac{2 z}{\sqrt{\pi}} \space{_1} F_{1}\left(\frac{1}{2} ; \frac{3}{2} ;-z^{2}\right),
$$

where

$$
\displaystyle { }_{1} F_{1}\left(\frac{1}{2} ; \frac{3}{2} ;-z^{2}\right)
$$

is the confluent hypergeometric function of the first kind [HyperG1F1](/igorpro/commands/hyperg1f1.md). In this case the accuracy parameter is ignored.

### *Details* {#details}
The *accuracy* parameter specifies the fractional accuracy that you desire. That is, if you set *accuracy* to 1e-7, that means that you wish that the absolute value of (f<sub>actual</sub>-f<sub>returned</sub>)/f<sub>actual</sub> be less than 10<sup>-</sup><sup>7</sup>.

For backwards compatibility, in the absence of *accuracy* an alternate calculation method is used that achieves fractional accuracy better than 2x10<sup>-</sup><sup>7</sup>.

If *accuracy* is present, erfc can achieve fractional accuracy better than 2x10<sup>-</sup><sup>16</sup> for *num* up to 1. From *num* = 1 to 10 fractional accuracy is better than 2x10<sup>-</sup><sup>15</sup>.

Higher accuracy takes somewhat longer to calculate. With *accuracy* set to 1e-16 erfc takes about 50% more time than with *accuracy* set to 1e-7.

### *See Also* {#see-also}
[erf](/igorpro/commands/erf.md), [erfcw](/igorpro/commands/erfcw.md), [erfcx](/igorpro/commands/erfcx.md), [inverseErfc](/igorpro/commands/inverseerfc.md), [dawson](/igorpro/commands/dawson.md)