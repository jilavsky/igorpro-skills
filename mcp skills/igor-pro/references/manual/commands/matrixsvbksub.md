---
description: "The MatrixSVBkSub operation does back substitution for SV decomposition."
slug: /commands/matrixsvbksub
---

<div className="command-signature">

## <strong>MatrixSVBkSub</strong>  <em>matrixU</em>, <em>vectorW</em>, <em>matrixV</em>, <em>vectorB</em> {#matrixsvbksub}

</div>

The MatrixSVBkSub operation does back substitution for SV decomposition.

### *Details* {#details}
Used to solve matrix equation Ax=b after you have performed an SV decomposition.

Feed this routine the M_U, W_W and M_V waves from [MatrixSVD](/igorpro/commands/matrixsvd.md) along with your right-hand-side vector *b*. The solution vector x is returned as M_x.

The array *b* can be a matrix containing a number of *b* vectors and the M_x will contain a corresponding set of solution vectors.

Generates an error if the dimensions of the input matrices are not appropriate.

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.