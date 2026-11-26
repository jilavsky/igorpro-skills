---
description: "The MatrixMultiplyAdd operation calculates the matrix expression: where * indicates scalar multiplication and x indicates matrix multiplication."
slug: /commands/matrixmultiplyadd
---

<div className="command-signature">

## <strong>MatrixMultiplyAdd</strong>  [/ZC or /DC] [/A=<em>alpha</em>] [/B=<em>beta</em>] <em>matA</em>[/T], <em>matB</em>[/T] <em>matC</em> {#matrixmultiplyadd}

</div>

The MatrixMultiplyAdd operation calculates the matrix expression:


```igor
matC = alpha*matA x matB + beta*matC
```

where `*` indicates scalar multiplication and `x` indicates matrix multiplication.

MatrixMultiplyAdd uses the LAPACK library for fast computation. It was added in Igor Pro 9.00.

Use /B=0 for just matrix multiply with no addition. In this case, the *beta*\**matC* term is not evaluated.

### *Parameters* {#parameters}
*matA*, *matB* and *matC* must be of the same number type and must be single or double precision real or complex.

If *matA* is an NxP matrix then *matB* must be a PxM matrix and the product is an NxM matrix. If these conditions are violated MatrixMultiplyAdd generates an error.

Include the /T flag after *matA* and/or *matB* to indicate that the transpose of *matA* and/or *matB* should be used.

If *matC* is a NULL wave reference, then a free wave is created and a reference to it is stored in the wave reference *matC*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A = *alpha*</span> | *alpha* is the scalar value multiplied with *matA*. It defaults to 1. |
| <span class="table-cell-nowrap">/B = *beta*</span> | *beta* is the scalar value multiplied with *matB*. It defaults to 1. Use /B=0 to omit the *beta*\**matC* term. |
| <span class="table-cell-nowrap">/DC</span> | Duplicates the wave referenced by *matC* as a free wave, performs the calculation with the duplicate as the destination, and stores a reference to the free wave in *matC*. |
|  | /DC is allowed only when calling MatrixMultiplyAdd from a user-defined function. It is an error to use /DC from the command line or in a macro. |
| <span class="table-cell-nowrap">/T</span> | Used after *matA* and/or *matB*, /T indicates tells MatrixMultiplyAdd to use the transform of *matA* and/or *matB* in the calculation. |
| <span class="table-cell-nowrap">/ZC</span> | Clears the input wave reference *matC*. This guarantees that *matC* is NULL which causes MatrixMultiplyAdd to create a free output wave and store a reference to it in *matC*. |
|  | When using MatrixMultiplyAdd in a loop, use /ZC to clear the input wave reference to ensure that a new free wave is created each time through the loop rather than re-using the same output wave. |
|  | /ZC is allowed only when calling MatrixMultiplyAdd from a user-defined function. It is an error to use /ZC from the command line or in a macro. |

### *Details* {#details}
*matA* and *matB* must exist but, when running in a user-defined function, *matC* may or may not exist. If it does not exist, MatrixMultiplyAdd creates a free output wave, creates a wave reference named *matC*, and stores a reference to the free output wave in *matC*.

Both *alpha* and *beta* must be real and default to 1.


|  |
| --- |
| <span class="table-cell-nowrap">Use /B = 0 to omit the *beta*\**matC* term.</span> |

### *Example* {#example}

```igor
Function Demo()	// Demonstrates various ways to call MatrixMultiplyAdd
	// Create input waves
	Make/O/N=(3,3) matA = p + 10*q
	Make/O/N=(3,3) matB = p == q
	
	Print "=== matC = matA x matB ==="
	Make/O/N=(3,3) matC = 0
	MatrixMultiplyAdd /B=0 matA, matB, matC
	Print matC
	
	Print "=== matC = 2*matA x matB ==="
	Make/O/N=(3,3) matC = 0
	MatrixMultiplyAdd /A=2 /B=0 matA, matB, matC
	Print matC
	
	Print "=== Free Wave Using WaveClear = matA x matB ==="
	Make/O/N=(3,3) matC = 0	// matC wave ref is cleared by WaveClear
	WaveClear matC	// MatrixMultiplyAdd creates a free output wave
	MatrixMultiplyAdd /B=0 matA, matB, matC
	Print matC
	
	Print "=== Free Wave Using /ZC = matA x matB ==="
	Make/O/N=(3,3) matC = 0	// matC wave ref is cleared by /ZC
	MatrixMultiplyAdd /B=0 /ZC matA, matB, matC
	Print matC
	
	Print "=== Create dest wave using string variable ==="
	String dest = "matDest1"
	Make/O/N=(3,3) $dest = 0
	WAVE destWave = $dest
	MatrixMultiplyAdd /B=0 matA, matB, destWave
	Print destWave
End
```

### *See Also* {#see-also}
[MatrixOp](/igorpro/commands/matrixop.md) and [MatrixMultiply](/igorpro/commands/matrixmultiply.md) for additional efficient matrix operations.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for further information on Igor's matrix routines.

[FastOp](/igorpro/commands/fastop.md) for additional efficient non-matrix operations.