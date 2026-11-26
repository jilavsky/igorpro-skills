---
description: "The poly2D function returns the value of a 2D polynomial function at x = x1, y = y1."
slug: /commands/poly2d
---

<div className="command-signature">

## <strong>poly2D</strong> (<em>coefsWaveName</em>, <em>x1</em>, <em>y1</em>) {#poly2d}

</div>

The poly2D function returns the value of a 2D polynomial function at x = *x1*, y = *y1*.

*coefsWaveName* is a wave that contains the polynomial coefficients. The number of points in the wave determines the number of terms in the polynomial and therefore the polynomial degree.

In a complex expression, poly2D requires x1 and y1 to be complex numbers, and returns a complex value. The wave containing the coefficients may be real or complex. Real coefficients are interpreted as cmplx(coef, 0). Passing complex coefficients in a real expression will use only the real part of the coefficients.

### *Details* {#details}
The coefficients wave contains polynomial coefficients for low degree terms first. All coefficients for terms of a given degree must be present, even if they are zero. Among coefficients for a given degree, those for terms having higher powers of X are first. Thus, poly2D returns, for a coefficient wave cw:

```igor
f(x,y) = cw[0] + cw[1]*x + cw[2]*y + cw[3]*x^2 + cw[4]*x*y + cw[5]*y^2 + ...
```

A 2D polynomial of degree N has (N+1)(N+2)/2 terms.

### *Poly2D Example 1* {#poly2d-example-1}
Fill mat1 with the polynomial 1 + 2\*x + 2.5\*y + 3\*x<sup>2</sup> + 3.5\*xy + 4\*y<sup>2</sup> evaluated over the range x = (-1, 1) and y = (-1, 1):


```igor
Function Poly2DExample1()
	Make/O coefs1 = {1, 2, 2.5, 3, 3.5, 4}
	Make/N=(20,20)/O mat1
	SetScale/I x, -1, 1, mat1
	SetScale/I y, -1, 1, mat1
	mat1 = poly2D(coefs1, x, y)
	Display; AppendMatrixContour mat1
End
```

The polynomial is second degree, so the first command above made the wave coefs with six elements because (2+1)(2+2)/2 = 6.

### *Poly2D Example 2* {#poly2d-example-2}
Fill mat2 with the polynomial 1 + 2*x + 3*y+ 4*x<sup>2</sup> + 4*y<sup>2</sup> + 5*x<sup>3</sup> + 6*y<sup>3</sup> evaluated over the range x =  (-1, 1) and y = (-1, 1). The first zero eliminates the second-order cross term x\*y and the second and third zeroes eliminate the third-order cross terms x<sup>2</sup>\*y and x\*y<sup>2</sup>:


```igor
Function Poly2DExample2()
	Make/O coefs2 = {1, 2, 3, 4, 0, 4, 5, 0, 0, 6}
	Make/N=(20,20)/O mat2
	SetScale/I x, -1, 1, mat2
	SetScale/I y, -1, 1, mat2
	mat2 = poly2D(coefs2, x, y)
	Display; AppendMatrixContour mat2
End
```

### *Poly2D Example 3* {#poly2d-example-3}
This example illustrates using poly2D in a complex expression:


```igor
Function Poly2DExample3()
	Make/N=(200,200)/C/O cMat3      // Complex-valued matrix
	SetScale/I x -pi,pi,cMat3
	SetScale/I y -pi,pi,cMat3
	Make/D/O coefs3={1,1.5,2,2.5,3,3.5}
	cMat3 = poly2d(coefs3, cmplx(sin(x),cos(y)), cmplx(cos(x),sin(y)))
	Display; Appendimage cMat3
	ModifyImage cMat3 ctab= {*,*,Rainbow256,0}
	ModifyImage cMat3 imCmplxMode=3 // Display the complex phase
End
```