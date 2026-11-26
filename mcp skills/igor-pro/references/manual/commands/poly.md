---
description: "The poly function returns the value of a polynomial function at x = x1."
slug: /commands/poly
---

<div className="command-signature">

## <strong>poly</strong> (<em>coefsWaveName</em>, <em>x1</em>) {#poly}

</div>

The poly function returns the value of a polynomial function at x = *x1*.

*coefsWaveName* is a wave that contains the polynomial coefficients. The number of points in the wave determines the number of terms in the polynomial.

If you use poly in a real expression, x1 must be real and poly returns a real value.  The wave containing the coefficients can be real or complex. Complex coefficients are interpreted as real(coef).

If you use poly in a complex expression, x1 must complex and poly returns a complex value. The wave containing the coefficients can be real or complex. Real coefficients are interpreted as cmplx(coef,0). Support for complex expressions was added in Igor Pro 9.00.

### *Examples* {#examples}

```igor
// Fill wave0 with 100 points containing the polynomial 1 + 2*x + 3*x^2 + 4*x^3
// evaluated over the range from x = -1 to x= 1
Make coefs = {1, 2, 3, 4}	// f(x) = 1 + 2*x + 3*x^2 + 4*x^3
Make/N=100/O wave0; SetScale/I x, -1, 1, wave0; Display wave0
wave0 = poly(coefs, x)
```