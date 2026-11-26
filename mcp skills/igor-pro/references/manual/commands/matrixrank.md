---
description: "The MatrixRank function returns the rank of matrixWaveA subject to the specified condition number."
slug: /commands/matrixrank
---

<div className="command-signature">

## <strong>MatrixRank</strong> (<em>matrixWaveA</em> [, <em>conditionNumberA</em> ]) {#matrixrank}

</div>

The MatrixRank function returns the rank of *matrixWaveA* subject to the specified condition number.

The matrix is not considered to have full rank if its condition number exceeds the specified *conditionNumberA*.

If the optional parameter *conditionNumberA* is not specified, IGOR uses the value 1.0E20.

MatrixRank supports the following numeric wave data types:

| Real | Complex |
| --- | --- |
| SP | SP |
| DP | DP |

The value of *conditionNumberA* should be large enough but taking into account the accuracy of the numerical representation given the numeric data type.

If there are any errors the function returns NaN.

### *See Also* {#see-also}
[Matrix Math Operations](/igorpro/analysis/analysis.md#matrix-math-operations) for more about Igor's matrix routines.