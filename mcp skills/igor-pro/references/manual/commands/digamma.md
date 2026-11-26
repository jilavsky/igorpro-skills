---
description: "The digamma function returns the digamma, or psi function of x. This is the logarithmic derivative of the gamma function."
slug: /commands/digamma
---

<div className="command-signature">

## <strong>digamma</strong> (<em>x</em>) {#digamma}

</div>

The digamma function returns the digamma, or psi function of *x*. This is the logarithmic derivative of the gamma function:

$$
\displaystyle \Psi(z) \equiv \frac{d}{d z} \ln (\Gamma(z))=\frac{\Gamma^{\prime}(z)}{\Gamma(z)}.
$$

In complex expressions, *x* is complex, and digamma(*x*) returns a complex value.

Limited testing indicates that the accuracy is approximately 1 part in 10<sup>16</sup>, at least for moderately-sized values of *x*.