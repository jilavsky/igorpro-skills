---
description: "The chebyshevU function returns the Chebyshev polynomial of the second kind, degree n and argument x."
slug: /commands/chebyshevu
---

<div className="command-signature">

## <strong>chebyshevU</strong> (<em>n</em>, <em>x</em>) {#chebyshevu}

</div>

The chebyshevU function returns the Chebyshev polynomial of the second kind, degree *n* and argument *x*.

The Chebyshev polynomial of the second kind satisfies the recurrence relation


```igor
U(n+1,x)=2xU(n,x)-U(n-1,x)
```

which is also the recurrence relation of the Chebyshev polynomials of the first kind.

The first 10 polynomials of the second kind are:


```igor
U(0,x)=1
U(1,x)=2x
U(2,x)=4x^2-1
U(3,x)=8x^3-4x
U(4,x)=16x^4-12x^2+1
U(5,x)=32x^5-32x^3+6x
U(6,x)=64x^6-80x^4+24x-1
U(7,x)=128x^7-192x^5+80x^3-8x
U(8,x)=256x^8-448x^6+240x^4-40x^2+1
U(9,x)512x^9-1024x^7+672x^5-160x^3+10x
```

### *See Also* {#see-also}
[Chebyshev](/igorpro/commands/chebyshev.md)