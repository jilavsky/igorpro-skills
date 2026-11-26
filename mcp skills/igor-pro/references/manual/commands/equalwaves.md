---
description: "The EqualWaves function compares waveA to waveB. Each wave can be of any data type. It returns 1 for equality and zero otherwise."
slug: /commands/equalwaves
---

<div className="command-signature">

## <strong>EqualWaves</strong> (<em>waveA</em>, <em>waveB</em> , <em>selector</em>  [, <em>tolerance</em> ]) {#equalwaves}

</div>

The EqualWaves function compares *waveA* to *waveB*. Each wave can be of any data type. It returns 1 for equality and zero otherwise.

Use the *selector* parameter to determine which aspects of the wave are compared. You can add *selector* values to test more than one field at a time or pass -1 to compare all aspects.

| selector | Field Compared |
| --- | --- |
| 1 | wave data |
| 2 | wave data type |
| 4 | wave scaling |
| 8 | data units |
| 16 | dimension units |
| 32 | dimension labels |
| 64 | wave note |
| 128 | wave lock state |
| 256 | data full scale |
| 512 | dimension sizes |

If you use the selectors for wave data, wave scaling, dimension units, dimension labels or dimension sizes, EqualWaves will return zero if the waves have unequal dimension sizes. The other selectors do not require equal dimension sizes.

### *Details* {#details}
If you are testing for equality of wave data and if the *tolerance* is specified, it must be a positive number. The function returns 1 for equality if the data satisfies:

$$
\displaystyle \sum_{i}({ waveA }[i]-{ waveB } [i])^{2}< { tolerance } .
$$

If *tolerance* is not specified, it defaults to 10<sup>-8</sup>.

If *tolerance* is set to zero and *selector* is set to 1 then the data in the two waves undergo a binary comparison (byte-by-byte).

If *tolerance* is non-zero then the presence of NaNs at a given point in both waves does not contribute to the sum shown in the equation above when both waves contain NaNs at the same point. A NaN entry that is present in only one of the waves is sufficient to flag inequality. Similarly, INF entries are excluded from the tolerance calculation when they appear in both waves at the same position and have the same signs.

If you are comparing wave data (*selector* =1) and both waves contain zero points the function returns 1.

The EqualWaves() function comparison of all text fields is case-sensitive.

### *See Also* {#see-also}
[MatrixOp](/igorpro/commands/matrixop.md) `equal` keyword