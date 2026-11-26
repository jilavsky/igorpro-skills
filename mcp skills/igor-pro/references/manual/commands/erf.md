---
description: "The erf function returns the error function of num. $$ \\displaystyle \\operatorname{erf}(x)=\\frac{2}{\\sqrt{\\pi}} \\int_{0}^{x} e^{-t^{2}} d t."
slug: /commands/erf
---

<div className="command-signature">

## <strong>erf</strong> (<em>num</em> [, <em>accuracy</em> ]) {#erf}

</div>

The erf function returns the error function of *num*.

$$
\displaystyle \operatorname{erf}(x)=\frac{2}{\sqrt{\pi}} \int_{0}^{x} e^{-t^{2}} d t.
$$

Optionally, *accuracy* can be used to specify the desired fractional accuracy.

In complex expressions the error function is defined by

$$
\displaystyle \operatorname{erf}(z)=\frac{2 z}{\sqrt{\pi}}{ }_{1} F_{1}\left(\frac{1}{2} ; \frac{3}{2} ;-z^{2}\right),
$$

where

$$
\displaystyle { }_{1} F_{1}\left(\frac{1}{2} ; \frac{3}{2} ;-z^{2}\right)
$$

is the confluent hypergeometric function of the first kind [HyperG1F1](/igorpro/commands/hyperg1f1.md). In this case the accuracy parameter is ignored.

### *Details* {#details}
The *accuracy* parameter specifies the fractional accuracy that you desire. That is, if you set *accuracy* to 1e-7, that means that you wish that the absolute value of (f<sub>actual</sub>-f<sub>returned</sub>)/f<sub>actual</sub> be less than 10<sup>-</sup><sup>7</sup>.

For backwards compatibility, in the absence of *accuracy* an alternate calculation method is used that achieves fractional accuracy better than about 2x10<sup>-</sup><sup>7</sup>.

If *accuracy* is present, erf can achieve fractional accuracy better than 8x10<sup>-</sup><sup>16</sup> for *num* as small as 10<sup>-</sup><sup>3</sup>. For smaller *num* fractional accuracy is better than 5x10<sup>-</sup><sup>15</sup>.

Higher accuracy takes somewhat longer to calculate. With *accuracy* set to 1e-16 erfc takes about 50% more time than with *accuracy* set to 1e-7.

### *See Also* {#see-also}
[erfc](/igorpro/commands/erfc.md), [erfcw](/igorpro/commands/erfcw.md), [inverseErf](/igorpro/commands/inverseerf.md), [inverseErfc](/igorpro/commands/inverseerfc.md), [dawson](/igorpro/commands/dawson.md)