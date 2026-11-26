---
description: "The Gauss function returns a normalized Gaussian for the specified dimension."
slug: /commands/gauss
---

<div className="command-signature">

## <strong>Gauss</strong> (<em>x</em>,<em>xc</em>,<em>wx</em>[,<em>y</em>,<em>yc</em>,<em>wy</em> [,<em>z</em>,<em>zc</em>,<em>wz</em> [,<em>t</em>,<em>tc</em>,<em>wt</em>]]]) {#gauss}

</div>

The Gauss function returns a normalized Gaussian for the specified dimension.

$$
\displaystyle \operatorname{Gauss}(\mathbf{r}, \mathbf{c}, \mathbf{w})=\prod_{i=1}^{n} \frac{1}{w_{i} \sqrt{2 \pi}} \exp \left[-\frac{1}{2}\left(\frac{r_{i}-c_{i}}{w_{i}}\right)^{2}\right],
$$

where *n* is the number of dimensions.

### *Parameters* {#parameters}
*xc*, *yc*, *zc*, and *tc* are the centers of the Gaussian in the X, Y, Z, and T directions, respectively.

*wx*, *wy*, *wz*, and *wt* are the widths of the Gaussian in the X, Y, Z, and T directions, respectively.

Note that *w*<sub>i</sub>  here is the standard deviation of the Gaussian. This is different from the width parameter in the gauss curve fitting function, which is sqrt(2) times the standard deviation.

Note also that the Gauss function lacks the cross-correlation parameter that is included in the Gauss2D curve fitting function.

### *Examples* {#examples}

```igor
Make/N=100 eee=gauss(x,50,10)
Print area(eee,-inf,inf)
  0.999999
Make/N=(100,100) ddd=gauss(x,50,10,y,50,15)
Print area(ddd,-inf,inf)
  0.999137
```

### *See Also* {#see-also}
[Gauss1D](/igorpro/commands/gauss1d.md) (duplicates the Gauss built-in curve fitting function)

[Gauss2D](/igorpro/commands/gauss2d.md) (duplicates the Gauss2D built-in curve fitting function)