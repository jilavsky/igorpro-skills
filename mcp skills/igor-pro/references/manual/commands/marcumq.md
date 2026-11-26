---
description: "The MarcumQ function returns the generalized Q-function defined by the integral."
slug: /commands/marcumq
---

<div className="command-signature">

## <strong>MarcumQ</strong> (<em>m</em>, <em>a</em>, <em>b</em>) {#marcumq}

</div>

The MarcumQ function returns the generalized Q-function defined by the integral

$$
\displaystyle Q_{m}(a, b)=\int_{b}^{\infty} u\left(\frac{u}{a}\right)^{m-1} \exp \left(-\frac{\left(a^{2}+u^{2}\right)}{2}\right) I_{m-1}(a u) d u,
$$

where *I*<sub>k</sub> is the modified Bessel function of the first kind and order *k*.

Its applications have been primarily in the fields of communication and detection theory. However, an interesting interpretation of its result with m=1 and appropriate parameter scaling is the fractional power of a two-dimensional circular Gaussian function within a displaced circular aperture.

Depending on the input arguments, the MarcumQ function may be computationally intensive but you can abort the calculation at any time.

### *References* {#references}
Cantrell, P.E., and A.K. Ojha, Comparison of Generalized Q-Function Algorithms, *IEEE Transactions on Information Theory*, *IT-33*, 591-596, 1987.

Simon, M. K., A New Twist on the Marcum Q-Function and Its Application, *IEEE Communications Letters*, 3, 39-41, 1998.