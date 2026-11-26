---
description: "The ZernikeR function returns the Zernike radial polynomials of degree n that contains no power of r that is less than m."
slug: /commands/zerniker
---

<div className="command-signature">

## <strong>ZernikeR</strong> (<em>n</em>, <em>m</em>, <em>r</em>) {#zerniker}

</div>

The ZernikeR function returns the Zernike radial polynomials of degree *n* that contains no power of *r* that is less than *m*.  Here *m* is even or odd according to whether *n* is even or odd, and *r* is in the range [0,1].

Note that the full circle polynomials are complex.  For any angle *t* (theta), they are given by:  

```igor
ZernikeR(n, m, r) * exp(imt)
```