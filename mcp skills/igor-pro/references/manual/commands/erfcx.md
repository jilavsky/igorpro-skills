---
description: "The erfcx function returns the scaled complementary error function of num."
slug: /commands/erfcx
---

<div className="command-signature">

## <strong>erfcx</strong> (<em>num</em>) {#erfcx}

</div>

The erfcx function returns the scaled complementary error function of *num*:

f(x) = exp(x<sup>2</sup>)\*erfc(x)

### *Details* {#details}
This implementation is for real numbers only. If you need complex input and output, use:

erfcx = Faddeeva(ix)

This method has poorer accuracy for negative X and a more limited region of numerical validity than this real implementation.

Computing erfcx using the mathematical definition has a very limited range in which it is accurate, or even valid.

### *References* {#references}
Our implementation comes from this post:

[https://stackoverflow.com/questions/39777360/accurate-computation-of-scaled-complementary-error-function-erfcx](https://stackoverflow.com/questions/39777360/accurate-computation-of-scaled-complementary-error-function-erfcx)

The code in that post is based on this paper:

M. M. Shepherd and J. G. Laframboise, "*Chebyshev Approximation of (1 + 2 x) exp(x2) erfc x in 0 ≤ x < ∞.*", Mathematics of Computation, Volume 36, No. 153, January 1981, pp. 249-253

### *See Also* {#see-also}
[erf](/igorpro/commands/erf.md), [erfc](/igorpro/commands/erfc.md), [erfcw](/igorpro/commands/erfcw.md), [inverseErfc](/igorpro/commands/inverseerfc.md), [dawson](/igorpro/commands/dawson.md), [Faddeeva](/igorpro/commands/faddeeva.md)