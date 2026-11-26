---
description: "The laguerre function returns the Laguerre polynomial of degree n (positive integer) and argument x. The polynomials satisfy the recurrence relation."
slug: /commands/laguerre
---

<div className="command-signature">

## <strong>laguerre</strong> (<em>n</em>, <em>x</em>) {#laguerre}

</div>

The laguerre function returns the Laguerre polynomial of degree *n* (positive integer) and argument *x*.  The polynomials satisfy the recurrence relation:

$$
\displaystyle (n+1) \text { Laguerre }(n+1, x)=(2 n+1-x) \text { Laguerre }(n, x)-n \text { Laguerre }(n-1, x),
$$

with the initial conditions

$$
\displaystyle \text { Laguerre }(0, x)=1
$$

and

$$
\displaystyle \text { Laguerre }(1, x)=1-x .
$$

### *See Also* {#see-also}
[laguerreA](/igorpro/commands/laguerrea.md), [laguerreGauss](/igorpro/commands/laguerregauss.md), [chebyshev](/igorpro/commands/chebyshev.md), [chebyshevU](/igorpro/commands/chebyshevu.md), [hermite](/igorpro/commands/hermite.md), [hermiteGauss](/igorpro/commands/hermitegauss.md), [legendreA](/igorpro/commands/legendrea.md)