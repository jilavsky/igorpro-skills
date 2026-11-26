---
description: "The MatrixLUDTD operation computes the LU factorization of a tri-diagonal matrix."
slug: /commands/matrixludtd
---

<div className="command-signature">

## <strong>MatrixLUDTD</strong>  [/FM/PMAT/MIND/SUMP] <em>srcMain</em> , <em>srcUpper</em> , <em>srcLower</em> {#matrixludtd}

</div>

The MatrixLUDTD operation computes the LU factorization of a tri-diagonal matrix. The general form of the factorization/decomposition is expressed in terms of matrix products:


```igor
M_Pt x triDiagonalMat = M_Lower x M_Upper
```

triDiagonalMat is the matrix defined by the main diagonal specified by *srcMain*, the upper diagonal specified by *srcUpper*, and the lower diagonal specified by *srcLower*.

M_Pt is an output wave created when the /PMAT flag is present. M_Lower and M_Upper are output waves created when the /FM flag is present. M_Pt is the transpose of the permutation matrix, M_Lower is a lower triangular matrix with 1's on the main diagonal and M_Upper is an upper triangular (or trapezoidal) matrix.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/MIND</span> | Finds the minimum magnitude diagonal element of M_Upper and stores it in V_min. This feature is useful if you want to investigate the behaviour of the determinant of the matrix when it is close to being singular. |
| <span class="table-cell-nowrap">/PMAT</span> | Saves the transpose of the permutation matrix in the wave M_Pt in the current data folder. Note that the permutation matrix is orthogonal and so the inverse of the matrix is equal to its transpose. |
| <span class="table-cell-nowrap">/SUMP</span> | Computes the sum of the phases of the elements on the main diagonal of M_Upper and store in the variable V_Sum. Note that the variable is initialized to NaN and that it is not set unless this flag is specified and M_Upper is complex. |
| <span class="table-cell-nowrap">/FM</span> | The full matrix output is stored in the waves M_Lower and M_Upper in the current data folder. |

### *Details* {#details}
You specify the tridiagonal matrix using three 1D waves of the same data type (single or double precision real or complex).

If /FM is present the output of the operation consists of two 2D waves and one 1D wave:

- M_Lower is a lower triangular matrix with 1's on the main diagonal.
- M_Upper is an upper triangular (or trapezoidal) matrix.
- W_PIV is 1D wave containing pivot indices.

See code example below for implementation details.

If /FM is omitted the output of the operation consists of five 1D waves:

- W_Diagonal is the main diagonal of matrixU.
- W_UDiagonal is the first upper diagonal of M_Upper.
- W_U2Diagonal is the second diagonal of M_Upper.
- W_LDiagonal is the first lower diagonal of M_Lower.
- W_PIV is a vector of pivot indices.

In this case M_Lower can be constructed (see below) from W_LDiagonal and the pivot index wave W_PIV.

If you are working with tridiagonal matrices you can take advantage of MatrixOp functionality to reconstruct your outputs. For example:


```igor
MatrixOp/O M_Upper=Diagonal(W_diagonal)
MatrixOp/O M_Upper=setOffDiag(M_Upper,1,W_UDiagonal)
MatrixOp/O M_Upper=setOffDiag(M_Upper,2,W_U2Diagonal)
```

These commands can be combined into a single command line.

The construction of M_Lower is a bit more complicated and can be accomplished for real data using the following code:


```igor
Function MakeLTMatrix(W_diagonal,W_LDiagonal,W_PIV)
	Wave W_diagonal,W_LDiagonal,W_PIV
	
	Variable i,N=DimSize(W_diagonal,0)
	MatrixOp/O M_Lower=setOffDiag(ZeroMat(N,N,4),-1,W_LDiagonal)
	M_Lower=p==q ? 1:M_Lower[p][q]	// Set the main diagonal to 1's
	MatrixOp/O index=W_PIV-1	// Convert from 1-based array
	for(i=1;i<=N-2;i+=1)
		if(index[i]!=i)
			variable j,tmp
			for(j=0;j<=i-1;j+=1)
				tmp=M_Lower[i][j]
				M_Lower[i][j]=M_Lower[i+1][j]
				M_Lower[i+1][j]=tmp
			endfor
		endif
	endfor
End
```

This code is provided for illustration only. In practice you could use the /FM flag so that the operation creates the full lower and upper matrices for you.

The variable V_flag is set to zero if the operation succeeds and to 1 otherwise (e.g., if the input is singular). The variables V_Sum and V_min are also set by some of the flag options above.

### *See Also* {#see-also}
[MatrixLUD](/igorpro/commands/matrixlud.md), [MatrixOp](/igorpro/commands/matrixop.md), [Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations)