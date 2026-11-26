---
description: "The MatrixDot function calculates the inner (scalar) product for two 1D waves. A 1D wave A represents a vector in the sense."
slug: /commands/matrixdot
---

<div className="command-signature">

## <strong>MatrixDot</strong> (<em>waveA</em>, <em>waveB</em>) {#matrixdot}

</div>

The MatrixDot function calculates the inner (scalar) product for two 1D waves. A 1D wave **A** represents a vector in the sense:

$$
\displaystyle \mathbf{A}=\sum \alpha_{i} \hat{e}_{i}, \quad \hat{e}_{i} \text { is a unit vector } .
$$

Given two such waves **A** and **B**, the inner product is defined as:

$$
\displaystyle i p=\sum \alpha_{i} \beta_{i} .
$$

When both *waveA* and *waveB* are complex and the result is assigned to a complex-valued number, MatrixDot returns

$$
\displaystyle i p c=\sum \alpha_{i}^{*} \beta_{i} .
$$

If you prefer the definition where the second factor is the one that is conjugated, you can simply reverse the order of *waveA* and *waveB* in the function call.

If the result is assigned to a real number, MatrixDot returns

$$
\displaystyle i p=\left|\sum \alpha_{i}^{*} \beta_{i}\right| .
$$

If either *waveA* or *waveB* is complex and the result is assigned to a real-valued number, MatrixDot returns

$$
\displaystyle i p=\left|\sum \alpha_{i} \beta_{i}\right| .
$$

When the result is assigned to a complex-valued number MatrixDot returns

$$
\displaystyle i p c=\sum \alpha_{i} \beta_{i} .
$$

### *See Also* {#see-also}
The [MatrixOp](/igorpro/commands/matrixop.md) operation for more efficient matrix operations.

[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.