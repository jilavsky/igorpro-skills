---
description: "The LambertW function returns the complex value of Lambert's W function for complex z and integer index branch. The function can be defined through its inverse."
slug: /commands/lambertw
---

<div className="command-signature">

## <strong>LambertW</strong> (<em>z</em>, <em>branch</em>) {#lambertw}

</div>

The LambertW function returns the complex value of Lambert's W function for complex z and integer index branch. The function can be defined through its inverse,

$$
\displaystyle z=w \mathrm{e}^{w} .
$$

Since w is multivalued, the *branch* parameter is used to differentiate between solutions for the equation.

The LambertW function was added in Igor Pro 7.00.

### *Details* {#details}
IGOR's LambertW uses complex input and output. You can use LambertW in real expressions but you must make sure that you are not calling the function in a range where its imaginary part is non-zero.

The average accuracy of the function defined by:

```igor
cabs(z-w*exp(w))
```

in the region 

```igor
|real(z)| < 10, |imag(z)| < 10
```

is 5e-14. In general the accuracy decreases with increasing |*branch*| and with increasing distance from the origin in the z-plane.

IGOR uses a hybrid algorithm to compute the function which requires longer computation times in the presence of numerical instabilities.

### *References* {#references}
R.M. Corless, G.H. Gonnet, D.E.G. Hare, D.J. Jeffrey and D.E. Knuth, "On Lambert W Function", Advances in Computational Mathematics **5**: 329–359