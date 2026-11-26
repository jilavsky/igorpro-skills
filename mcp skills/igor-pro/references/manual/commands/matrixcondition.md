---
description: "MatrixCondition returns the estimated reciprocal of the condition number of a 2D square matrix wave2D."
slug: /commands/matrixcondition
---

<div className="command-signature">

## <strong>MatrixCondition</strong> (<em>wave2D</em>, <em>mode</em>) {#matrixcondition}

</div>

MatrixCondition returns the estimated reciprocal of the condition number of a 2D square matrix *wave2D*.

The condition number is the product of the norm of the matrix with the norm of the inverse of the matrix (see details below). The type of norm is determined by the value of the *mode* parameter. 1-norm is used if *mode* is 1 and infinity-norm is used otherwise.

The MatrixCondition function was added in Igor Pro 7.00.

### *Details* {#details}
The function uses LAPACK routines to estimate the reciprocal condition number by first obaining the norm of the input matrix and then using LU decomposition to obtain the norm of the inverse of the matrix. The estimate returned is

$$
\displaystyle { reciprocalCon }=\frac{1}{\| { wave2D } \|*\| { wave2D } ^{-1} \|},
$$

where the norms are selected by the choice of the *mode* parameter. The 1-norm of matrix A with elements a<sub>ij</sub> is defined as

$$
\displaystyle \|A\|_{1}=\max _{1 \leq j \leq n} \sum_{i=1}^{m}\left|a_{i j}\right|,
$$

and the infinity-norm is defined by

$$
\displaystyle \|A\|_{\infty}=\max _{1 \leq i \leq m} \sum_{j=1}^{n}\left|a_{i j}\right| .
$$

The function returns a NaN if there is any error in the input parameters.

### *References* {#references}
[http://en.wikipedia.org/wiki/Matrix_norm](http://en.wikipedia.org/wiki/Matrix_norm)

### *See Also* {#see-also}
[MatrixSVD](/igorpro/commands/matrixsvd.md) provides a condition number for L2 norm using the ratio of singular values.

The [MatrixOp](/igorpro/commands/matrixop.md) operation for more efficient matrix operations.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.