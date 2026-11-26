---
description: "The MatrixMultiply operation calculates matrix expression A*B and puts the result in a matrix wave named M_product generated in the current data folder."
slug: /commands/matrixmultiply
---

<div className="command-signature">

## <strong>MatrixMultiply</strong>  <em>matrixA</em> [/T], <em>matrixB</em> [/T] [, <em>additional</em> <em>matrices</em> ] {#matrixmultiply}

</div>

The MatrixMultiply operation calculates matrix expression A\*B and puts the result in a matrix wave named M_product generated in the current data folder. The /T flag can be included to indicate that the transpose of the specified matrix should be used.

If any of the source matrices are complex, then the result is complex.

### *Parameters* {#parameters}
If A is an NxP matrix then B must be a PxM matrix and the product is an NxM matrix. Up to 10 matrices can be specified although it is unlikely you will ever need more than three. The inner dimensions must be the same. Multiplication is performed from the right to the left.

It is legal for M_product to be one of the input matrices. Thus


```igor
MatrixMultiply A,B,C
```

could also be done as:


```igor
MatrixMultiply B,C
MatrixMultiply A,M_product
```

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *dWave*</span> | Use this flag to specify the destination wave for the product matrix. If you do not use this flag, the data is saved in the wave M_product in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the specified destination wave as a free wave. This flag does not affect any of the output waves that are created by default without explicit user-specified destination. |
|  | /FREE is allowed only in functions and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |

### *Details* {#details}
Supports multiplication of complex matrices.

An error is generated if the dimensioning of the input arrays is invalid.

### *See Also* {#see-also}
[MatrixOp](/igorpro/commands/matrixop.md) and [MatrixMultiplyAdd](/igorpro/commands/matrixmultiplyadd.md) for additional efficient matrix operations.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.

[FastOp](/igorpro/commands/fastop.md) for additional efficient non-matrix operations.