---
description: "The chebyshev function returns the Chebyshev polynomial of the first kind and of degree n."
slug: /commands/chebyshev
---

<div className="command-signature">

## <strong>chebyshev</strong> (<em>n</em>, <em>x</em>) {#chebyshev}

</div>

The chebyshev function returns the Chebyshev polynomial of the first kind and of degree *n*.

The Chebyshev polynomials satisfy the recurrence relation:

$$
\displaystyle T_{n+1}(x)=2 x T_{n}(x)-T_{n-1}(x)
$$

with: 
$$
\displaystyle \begin{array}{l}
T_{0}(x)=1 \\
T_{1}(x)=x \\
T_{2}(x)=2 x^{2}-1 .
\end{array}
$$

The orthogonality of the polynomial is expressed by the integral:

$$
\displaystyle \int_{-1}^{1} \frac{T_{n}(x) T_{m}(x)}{\sqrt{1-x^{2}}} d x=\left\{\begin{array}{ll}
0 & m \neq n \\
\\
\pi / 2 & m=n \neq 0 \\
\\
\pi & m=m=0
\end{array} .\right.
$$

### *References* {#references}
Abramowitz, M., and I.A. Stegun, "Handbook of Mathematical Functions", 446 pp., Dover, New York, 1972.

### *See Also* {#see-also}
[chebyshevU](/igorpro/commands/chebyshevu.md)