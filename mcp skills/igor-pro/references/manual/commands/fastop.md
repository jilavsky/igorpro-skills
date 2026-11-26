---
description: "The FastOp operation can be used to get improved speed out of certain wave assignment statements."
slug: /commands/fastop
---

<div className="command-signature overload">

## <strong>FastOp</strong>  <em>destWave</em> = <em>prod1</em> [± <em>prod2</em>  [± <em>prod3</em> ]] {#fastop}

</div>
<div className="command-signature">

## <strong>FastOp</strong>  <em>destWave</em> += <em>prod1</em> [± <em>prod2</em>] {#fastop}

</div>

The FastOp operation can be used to get improved speed out of certain wave assignment statements. The syntax was designed so that you can simply insert "FastOp" in front of any wave assignment statement that meets the syntax requirements. The += syntax was added in  Igor Pro 9.00.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *destWave* | Existing destination wave for the assignment expression. An error will be reported at runtime if the waves are not all the same length or number type. |
| *prod1*, *prod2*, *prod3* | Products of the following form: |
|  | <code class="igor">constexpr \* wave1 \* wave2</code> |
|  | or |
|  | <code class="igor">constexpr \* wave1 / wave2</code> |
|  | *constexpr* may be a literal numeric constant or a constant expression in parentheses. Such an expression is evaluated only once. |
|  | Any of the components of a prod expression may be omitted. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C</span> | The /C flag is obsolete in Igor Pro 9.00 and later and is ignored. For floating point waves, the type of expressions, real or complex, is determined by the type of the destination wave. |
|  | In Igor Pro 8 and before, /C is required when using a complex destination wave. |
|  | FastOp supports real and complex for floating point waves but only real for integer waves. |

### *Details* {#details}
FastOp supports real and complex for floating point waves. It supports real only for integer waves.

If your waves are complex, make sure to use WAVE/C when declaring wave references in user-defined functions.

Certain combinations, listed in the following table, are evaluated using faster optimized code rather than more general but slower generic code. SP means "single-precision floating point" and DP means "double-precision floating point".


| Statement | Optimized Data Types |
| --- | --- |
| <span class="table-cell-nowrap">dest = 0</span> | All |
| <span class="table-cell-nowrap">dest = waveA</span> | All |
| <span class="table-cell-nowrap">dest + = C0 \* waveA</span> | SP and DP, real and complex |
| <span class="table-cell-nowrap">dest = dest + C0 \* waveA</span> | SP and DP, real and complex |
| <span class="table-cell-nowrap">dest = dest + waveA \* C0</span> | SP and DP, real and complex |
| <span class="table-cell-nowrap">dest = C0</span> | SP and DP and integer, real only |
| <span class="table-cell-nowrap">dest = waveA + C1</span> | SP and DP and integer, real only |
| <span class="table-cell-nowrap">dest = C0 \* waveA + C1</span> | SP and DP, real only |
| <span class="table-cell-nowrap">dest = waveA + waveB + C2</span> | Integer only, real only |

In the statements above, pluses may be minuses and the trailing constant (*C0*, *C1*, *C2* ) can be omitted.

:::note
Except for the optimized cases listed above which use integer calculations for integer waves, integer results are evaluated using double precision intermediate values. This limits precision for 64-bit integer waves to 53 bits.
:::

Speedups generally range from 10 to 40 times faster than the equivalent statement with FastOp removed. The speedup is dependent on the computer and on the length of the waves with the greatest improvement occurring for waves with 1000 to 100,000 points.

### *Examples* {#examples}
Valid expressions:


```igor
FastOp dest = 3
FastOp dest = waveA + waveB
FastOp dest = 0.5*waveA + 0.5*waveB
FastOp dest = waveA*waveB
FastOp dest = (2*3)*waveA + 6
FastOp dest = (locvar)*waveA
FastOp dest += waveA + waveB
```

Expressions that are **NOT** valid:


```igor
FastOp dest = 3*4
FastOp dest = (waveA + waveB)
FastOp dest = waveA*0.5 + 0.5*waveB
FastOp dest = waveA*waveB/2
FastOp dest = 2*3*waveA + 6
FastOp dest = locvar*waveA
FastOp dest += waveA + waveB + waveC
```

### *See Also* {#see-also}
[MatrixOp](/igorpro/commands/matrixop.md), [MatrixMultiply](/igorpro/commands/matrixmultiply.md) and [MatrixMultiplyAdd](/igorpro/commands/matrixmultiplyadd.md) for additional efficient matrix operations.

[MultiThread](/igorpro/programming/keywords/other-programming-keywords.md#multithread)