---
description: "The hermite function returns the Hermite polynomial of order n: $$ \\displaystyle H_{n}(x)=(-1)^{n} \\exp \\left(x^{2}\\right) \\frac{d^{n}}{d x^{n}} \\exp…"
slug: /commands/hermite
---

<div className="command-signature">

## <strong>hermite</strong> (<em>n</em>, <em>x</em>) {#hermite}

</div>

The hermite function returns the Hermite polynomial of order *n* :

$$
\displaystyle H_{n}(x)=(-1)^{n} \exp \left(x^{2}\right) \frac{d^{n}}{d x^{n}} \exp \left(-x^{2}\right) .
$$

The first few polynomials are:

$$
\displaystyle \begin{array}{l}
1 \\
\\
2 x \\
\\
4 x^{2}-2 \\
\\
8 x^{3}-12 x
\end{array}
$$

### *See Also* {#see-also}
[hermiteGauss](/igorpro/commands/hermitegauss.md)