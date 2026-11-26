---
description: "The MatrixDet function returns the determinant of dataMatrix. The matrix wave must be a real, square matrix or else the returned value will be NaN."
slug: /commands/matrixdet
---

<div className="command-signature">

## <strong>MatrixDet</strong> (<em>dataMatrix</em>) {#matrixdet}

</div>

The MatrixDet function returns the determinant of *dataMatrix*. The matrix wave must be a real, square matrix or else the returned value will be NaN.

### *Details* {#details}
The function calculates the determinant using LU decomposition. If, following the decomposition, any one of the diagonal elements is either identically zero or equal to 10^-100, the return value of the function will be zero.

### *See Also* {#see-also}
The [MatrixOp](/igorpro/commands/matrixop.md) operation for more efficient matrix operations.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.