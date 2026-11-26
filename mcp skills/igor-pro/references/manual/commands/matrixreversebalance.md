---
description: "MatrixReverseBalance inverse-transforms left or right eigenvectors contained in eigenvectorsWave that were computed for a matrix that was balanced using…"
slug: /commands/matrixreversebalance
---

<div className="command-signature">

## <strong>MatrixReverseBalance</strong>  [<em>flags</em>] <em>scaleWave</em>, <em>eigenvectorsWave</em> {#matrixreversebalance}

</div>

MatrixReverseBalance inverse-transforms left or right eigenvectors contained in *eigenvectorsWave* that were computed for a matrix that was balanced using [MatrixBalance](/igorpro/commands/matrixbalance.md). The results are the eigenvectors of the pre-balanced matrix. *scaleWave* is W_scale as returned by [MatrixBalance](/igorpro/commands/matrixbalance.md).

MatrixReverseBalance was added in Igor Pro 9.00.

### *Parameters* {#parameters}
*eigenvectorsWave* must be single-precision or double-precision floating point, real or complex, and must contain no NaNs. MatrixReverseBalance returns an error if these conditions are not met.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTM = *dest*</span> | Specifies the destination wave for the inverse-transformed eigenvectors. If you omit /DSTM, the output is saved in M_RBEigenvectors in the current data folder. |
| <span class="table-cell-nowrap">/FREE</span> | Create free destination wave when it is specified via /DSTM. |
| <span class="table-cell-nowrap">/J = *job*</span> | *job* is the type of backward transformation required. It is one of the following letters: |
|  | **N** *srcWave* is not permuted or scaled. |
|  | **P** *srcWave* is permuted but not scaled. |
|  | **S** *srcWave* is scaled but not permuted. The scaling applies a diagonal similarity transformation to make the norms of the various columns close to each other. |
|  | **B** *srcWave* is both scaled and permuted. This is also the default. |
|  | You should use the same value for *job* as was used in the original balancing. |
| <span class="table-cell-nowrap">/SIDE = *side*</span> | Use /SIDE=R for right eigenvalues or /SIDE=L for left eigenvalues. |
| <span class="table-cell-nowrap">/LH = {*low*,*high*}</span> | Specifies the zero-based low and high indices that were returned by [MatrixBalance](/igorpro/commands/matrixbalance.md) in V_min and V_max respectively. |
| <span class="table-cell-nowrap">/Z</span> | Suppresses error reporting. If you use /Z, check the V_Flag output variable to see if the operation succeeded. |

### *Details* {#details}
Matrix balancing is usually called internally by LAPACK routines when there is large variation in the magnitude of matrix elements. Following matrix balancing the computed eigenvalues are expected to be more accurate but the resulting eigenvectors are not the correct eigenvectors of the original pre-balanced matrix. MatrixReverseBalance is then applied to the balanced eigenvectors in order to obtain the eigenvectors of the original matrix.

The operation uses outputs from MatrixBalance as inputs. Pass the W_scale output from MatrixBalance as the *scaleWave* parameter. Pass the V_min and V_max outputs from MatrixBalance as the /LH *low* and *high* parameters. See [MatrixBalance](/igorpro/commands/matrixbalance.md) for an example.

### *Output Variables* {#output-variables}

|  |  |
| --- | --- |
| V_Flag | Set to zero when the operation succeeds. Otherwise, when V_flag is positive the value is a standard Igor error code. When V_flag is negative it is an indication of an invalid input parameter. |

### *References* {#references}
The operation uses the following LAPACK routines: sgebak, dgebak, cgebak, and zgebak.

### *See Also* {#see-also}
[MatrixBalance](/igorpro/commands/matrixbalance.md)