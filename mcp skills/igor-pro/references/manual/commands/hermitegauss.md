---
description: "The hermiteGauss function returns the normalized Hermite polynomial of order n."
slug: /commands/hermitegauss
---

<div className="command-signature">

## <strong>hermiteGauss</strong> (<em>n</em>, <em>x</em>) {#hermitegauss}

</div>

The hermiteGauss function returns the normalized Hermite polynomial of order *n* :

$$
H_{n}(x)=\frac{1}{\displaystyle \sqrt{\sqrt{\pi} 2^{n} n!}}(-1)^{n} \exp \left(x^{2}\right) \frac{d^{n}}{d x^{n}} \exp \left(-x^{2}\right) .
$$

Here the normalization was chosen such that

$$
\displaystyle \int_{-\infty}^{\infty} e^{-x^{2}} H_{n}(x) H_{m}(x) d x=\delta_{m n},
$$

where *δ*<sub>nm</sub> is the Kronecker symbol.

You can verify the Hermite-Gauss normalization using the following functions:


```igor
Function TestNormalization(order)
	Variable order
	
	Variable/G theOrder = order
	// The integrand vanishes in double-precision outside [-30,30]
	Print/D Integrate1D(hermiteIntegrand,-30,30,2)
End

Function HermiteIntegrand(inX)
	Variable inX
	
	NVAR n = root:theOrder
	return  HermiteGauss(n,inx)^2*exp(-inx*inx)
End
```

### *See Also* {#see-also}
[hermite](/igorpro/commands/hermite.md)