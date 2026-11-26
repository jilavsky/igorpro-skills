---
description: "MatrixLUBkSub provides back substitution for LU decomposition. This operation is used to solve the matrix equation Ax=b after you have performed LU…"
slug: /commands/matrixlubksub
---

<div className="command-signature">

## <strong>MatrixLUBkSub</strong>  <em>matrtixL</em>, <em>matrixU</em>, <em>index</em>, <em>vectorB</em> {#matrixlubksub}

</div>

MatrixLUBkSub provides back substitution for LU decomposition.

### *Details* {#details}
This operation is used to solve the matrix equation Ax=b after you have performed LU decomposition (see [MatrixLUD](/igorpro/commands/matrixlud.md)). Feed this routine M_Lower,M_Upper and W_LUPermutation from MatrixLUD along with your right-hand-side vector b. The solution vector x is returned as M_x. The array b can be a matrix containing a number of b vectors and the M_x will contain a corresponding set of solution vectors.

Generates an error if the dimensions of the input matrices are not appropriate.

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.