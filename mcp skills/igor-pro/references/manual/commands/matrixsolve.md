---
description: "The MatrixSolve operation was superseded by MatrixLLS and is included for backward compatibility only."
slug: /commands/matrixsolve
---

<div className="command-signature">

## <strong>MatrixSolve</strong>  <em>method</em>, <em>matrixA</em>, <em>vectorB</em> {#matrixsolve}

</div>

The MatrixSolve operation was superseded by MatrixLLS and is included for backward compatibility only.

Used to solve matrix equation Ax=b using the method of your choice. Method keywords are:

|  |  |
| --- | --- |
| GJ | Gauss Jordan |
| LU | LU decomposition |
| SV | Singular Value decomposition |

### *Details* {#details}
The array *b* can be a matrix containing a number of *b* vectors and the output matrix M_x will contain a corresponding set of solution vectors.

V_flag is set to zero if success, 1 if singular matrix using GJ or LU and 1 if SV fails to converge.

For normal problems you should use LU. GJ is provided only for completeness and has no practical use.

When using SV, singular values smaller than 1e-6 times the largest singular value are set to zero before back substitution.

Generates an error if the dimensions of the input matrices are not appropriate.

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.

[MatrixLLS](/igorpro/commands/matrixlls.md)