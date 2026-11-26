---
description: "The binomial function returns the ratio: $$ \\displaystyle \\frac{n!}{k!(n-k)!} $$."
slug: /commands/binomial
---

<div className="command-signature">

## <strong>binomial</strong> (<em>n</em>, <em>k</em>) {#binomial}

</div>

The binomial function returns the ratio:

$$
\displaystyle \frac{n!}{k!(n-k)!}
$$
<sub></sub>

It is assumed that *n* and *k* are integers and 0 <= *k* <= *n* and ! denotes the factorial function.

When k>n, the binomial function returns 0. If either n or k are singular (i.e., NaN or INF), the binomial function returns NaN.

Note that while the binomial function is an integer-valued function, a double-precision number has 53 bits for the mantissa. This means that numbers over 2<sup>52</sup> (about 4.5x10<sup>15</sup>) will be accurate to about one part in 2x10<sup>16</sup>.

If you encounter overflow you can use the [APMath](/igorpro/commands/apmath.md) operation to obtain the result. For example:


```igor
Print factorial(1000)
  inf
APMath/V result = factorial(1000)
  4.02387260077093773543702433923003985719374864210715E+2567
```