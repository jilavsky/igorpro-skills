---
description: "The MatrixBalance operation permutes and/or scales an NxN real or complex matrix to obtain a similar matrix that is more stable for subsequent calculations…"
slug: /commands/matrixbalance
---

<div className="command-signature">

## <strong>MatrixBalance</strong>  [<em>flags</em>] <em>srcWave</em> {#matrixbalance}

</div>

The MatrixBalance operation permutes and/or scales an NxN real or complex matrix to obtain a similar matrix that is more stable for subsequent calculations such as eigenvalues and eigenvectors. Balancing a matrix is useful when some matrix elements are much smaller than others.

MatrixBalance saves the resulting matrix in the wave specified by the /DSTM flag. It creates a secondary output wave specified by the /DSTS flag containing permutation and scaling information.

MatrixBalance was added in Igor Pro 9.00.

### *Parameters* {#parameters}
*srcWave* must be single-precision or double-precision floating point, real or complex, and must contain no NaNs. MatrixBalance returns an error if these conditions are not met.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTM = *dest*</span> | Specifies the destination wave for the balanced output matrix. If you omit /DSTM, the output is saved in M_Balanced in the current data folder. |
| <span class="table-cell-nowrap">/DSTS = *dest*</span> | Specifies the destination wave for the scaling array. If you omit /DSTS, the scaling wave is saved as W_Scale in the current data folder. |
| <span class="table-cell-nowrap">/FREE</span> | Creates free destination waves when they are are specified via /DSTM or /DSTS. |
| <span class="table-cell-nowrap">/J = *job*</span> | *job* is one of the following letters: |
|  | **N** *srcWave* is not permuted or scaled. |
|  | **P** *srcWave* is permuted but not scaled. |
|  | **S** *srcWave* is scaled but not permuted. The scaling applies a diagonal similarity transformation to make the norms of the various columns close to each other. |
|  | **B** *srcWave* is both scaled and permuted (default). |
| <span class="table-cell-nowrap">/Z</span> | Do not report any errors. V_flag will be set to 0 if successful or to an error code. V_min and V_max will be set to NaN in case of an error. |

### *Details* {#details}
Matrix balancing is usually called internally by LAPACK routines when there is large variation in the magnitude of matrix elements. The /J flag supports the granularity of applying only permutation, only scaling or both.

After balancing there will be a block diagonal form that could typically be handled using Schur decomposition (see [MatrixSchur](/igorpro/commands/matrixschur.md)). The rows/columns corresponding to this block diagonal are saved in zero based V_min and V_max. The scaling wave W_scale[i] (for i<V_min) contains the index of the row/column that was interchanged with row/col i. For i>=V_min the scaling wave contains the scaling factor use to balance row and column i.

When you balance *srcWave* using this operation the resulting eigenvectors belong to the balanced matrix. Use [MatrixReverseBalance](/igorpro/commands/matrixreversebalance.md) to obtain the eigenvectors of *srcWave*.

When solving for the Schur vectors of *srcWave* after using /J=P for permuting only, use [MatrixReverseBalance](/igorpro/commands/matrixreversebalance.md) to transform the vectors. If you are solving for the Schur vectors do not use either /J=S or /J=B because that balancing transformation is not orthogonal.

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| V_Flag | Set to zero when the operation succeeds. Otherwise, when V_flag is positive the value is a standard error code. When V_flag is negative it is an indication of a wrong input parameter. |
| V_min | Set to zero if /J=N or /J=S. |
| V_max | Set to N-1 (where N is the number of rows or columns) if /J=N or /J=S. |

When /J=B or /J=P the matrix M_Balanced[i][j]=0 if i>j and j=0...V_min-2 or i=V_max,...N-1.

### *Examples* {#examples}

```igor
Function DemoMatrixBalance1()
	// Generate random unbalanced data
	Make/D/O/N=(7,7) srcWave=p+10*q+enoise(5)
	MatrixBalance srcWave
	Wave M_Balanced
	Wave W_Scale
	
	MatrixOP/O/FREE matD=diagonal(W_Scale)
	MatrixOP/O/FREE matDInv=inv(matD)
	
	// Check that W_Scale produces the correct balanced matrix
	MatrixOP/O/FREE matProd=matDInv x srcWave x matD
	
	// Compare with M_Balanced
	MatrixOP/O/FREE/P=1 aa=sum(abs(M_Balanced-matProd)) 
End
Function DemoMatrixBalance2()
	Make/O/N=(3,3) mat
	mat[0][0] = {2,88,164}
	mat[0][1] = {0,1,1}
	mat[0][2] = {1e-05,0,1}
	
	MatrixBalance mat
	Wave W_scale,M_Balanced
	Print "EqualWaves(input,output,-1)", EqualWaves(mat,M_Balanced,-1)
	
	// Calculate right eigenvectors for the original matrix
	MatrixEigenV/R mat
	Wave/Z M_R_eigenVectors
	Duplicate/O M_R_eigenVectors, origEigenVectors
	Wave/Z W_eigenValues
	Duplicate/O W_eigenValues,origEigenValues
	
	// Calculate the right eigenvectors for the balanced matrix
	MatrixEigenV/R M_Balanced
	Wave/Z M_R_eigenVectors
	Wave/Z W_eigenValues
	MatrixOP/O/FREE tmp = sum(abs(origEigenValues-W_eigenValues))
	if (tmp[0] > 0.1)
		Print "Eigenvalues difference"
	else
		Print "Eigenvalues OK"
	endif

	// Reverse the balance and compare with original eigenvectors
	MatrixReverseBalance/J=P/SIDE=R/LH={V_min,V_max} W_Scale,M_R_eigenVectors
	Wave/Z M_RBEigenvectors
	MatrixOP/O/FREE tmp = sum(abs(M_RBEigenvectors-origEigenVectors))
	if (tmp[0] > 0.1)
		Print "Eigenvectors difference on reverse"
	else
		Print "Eigenvectors ok on reverse"
	endif
End
```

### *References* {#references}
The operation uses the following LAPACK routines: sgebal, dgebal, cgebal, and zgebal.

### *See Also* {#see-also}
[MatrixReverseBalance](/igorpro/commands/matrixreversebalance.md)