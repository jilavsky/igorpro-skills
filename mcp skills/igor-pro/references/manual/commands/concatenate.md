---
description: "The Concatenate operation combines data from the source waves into destWave, which is created if it does not already exist."
slug: /commands/concatenate
---

<div className="command-signature overload">

## <strong>Concatenate</strong>  [ /DL /FREE /KILL /NP[=<em>dim</em> ] /O] [<em>typeFlags</em> ]  <em>waveListStr</em>, <em>destWave</em> {#concatenate}

</div>
<div className="command-signature overload">

## <strong>Concatenate</strong>  [/DL /FREE /KILL /NP[=<em>dim</em> ] /O] [<em>typeFlags</em> ]  {<em>wave1</em>, <em>wave2</em>, <em>wave3</em>,...}, <em>destWave</em> {#concatenate}

</div>
<div className="command-signature">

## <strong>Concatenate</strong>  [/DL /FREE /KILL /NP[=<em>dim</em> ] /O] [<em>typeFlags</em> ]  {<em>waveWave</em> }, <em>destWave</em> {#concatenate}

</div>

The Concatenate operation combines data from the source waves into *destWave*, which is created if it does not already exist. If *destWave* does exists and overwrite is not specified, the source waves' data is concatenated with the existing data in the destination wave.

By default the concatenation increases the dimensionality of the destination wave if possible. For example, if you concatenate two 1D waves of the same length you get a 2D wave with two columns. The destination wave is said to be "promoted" to a higher dimensionality.

If you use the /NP (no promotion) flag, the dimensionality of the destination wave is not changed. For example, if you concatenate two 1D waves of the same length using /NP you get a 1D wave whose length is the sum of the lengths of the source waves.

If the source waves are of different lengths, no promotion is done whether /NP is used or not.

### *Parameters* {#parameters}
*waveListStr* is a string expression containing a list of input wave names separated by semicolons with a semicolon at the end. There is no limit to the number of wave names in *waveListStr*.

The {*wave1*, *wave2*, ...} syntax is limited to 100 waves.

In the {*waveWave*} syntax, *waveWave* is a single WAVE reference wave containing references to the input waves. This syntax was added in Igor Pro 8.00.

*destWave*  is the name of a new or existing wave that will contain the concatenation result.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DL</span> | Sets dimension labels. When doing promotion, it uses source wave names for new dimension labels otherwise it uses existing labels. |
| <span class="table-cell-nowrap">/FREE</span> | Creates *destWave* as a free wave (see [Free Waves](/igorpro/programming/programming.md#free-waves)). The /FREE flag was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">/KILL</span> | Kills source waves. |
| <span class="table-cell-nowrap">/NP</span> | Prevents promotion to higher dimension. |
| <span class="table-cell-nowrap">/NP = dim</span> | Prevents promotion and appends data along the specified dimension (0= rows, 1= columns, 2=layers, 3=chunks). All dimensions other than the one specified by dim must be the same in all waves. |
| <span class="table-cell-nowrap">/O</span> | Overwrites *destWave*. |

### *Type Flags (functions only)* {#type-flags-functions-only}
Concatenate also can use various type flags in user functions to specify the type of destination wave reference variables. These type flags do not need to be used except when it is necessary to match another wave reference variable of the same name or to tell Igor what kind of expression to compile for a wave assignment. See [WAVE Reference Types](/igorpro/programming/programming.md#wave-reference-types) and [WAVE Reference Type Flags](/igorpro/programming/programming.md#wave-reference-type-flags) for a complete list of type flags and further details.

### *Details* {#details}
If *destWave*  does not already exist or, if the /O flag is used, *destWave*  is created by duplication of the first source wave. Waves are concatenated in order through the list of source waves. If *destWave*  exists and the /O flag is not used, then the concatenation starts with *destWave*.

*destWave*  cannot be used in the source wave list.

Source waves must be either all numeric or all text.

If promotion is allowed, the number of low-order dimensions that all waves share in common determines the dimensionality of *destWave*  so that the dimensionality of *destWave*  will then be one greater. The default behaviors will vary according to the source wave sizes. Concatenating 1D waves that are all the same length will produce a 2D wave, whereas concatenating 1D waves of differing lengths will produce a 1D wave. Similarly, concatenating 2D waves of the same size will produce a 3D wave; but if the 2D source waves have differing numbers of columns then *destWave*  will be a 2D wave, or if the 2D waves have differing numbers of rows then *destWave*  will be a 1D wave. Concatenating 1D and 2D waves that have the same number of rows will produce a 2D wave, but when the number of rows differs, *destWave*  will be a 1D wave. See the examples.

Use the /NP flag to suppress dimension promotion and keep the dimensionality of *destWave*  the same as input waves.

:::warning
Under some circumstances, such as in loops in user-defined functions, Concatenate may exhibit unexpected behavior.
:::

When you have a statement like this in a user-defined function:


```igor
Concatenate/O ..., DestWaveName
```

at compile time, Igor creates an automatic local wave reference variable named DestWaveName. At runtime, if the wave reference variable is NULL, the name is taken to be a literal name and a wave of that name is created in the current data folder.

If the wave reference variable is not NULL, as would occur after the first call to Concatenate in a loop, then the referenced wave is overwritten no matter where it is located.

If your intention is to create or overwrite a wave in the current data folder, you should use one of the following two methods:


```igor
Concatenate/O ..., $"DestWaveName"
WAVE DestWaveName		// Needed only if you subsequently reference the dest wave
```

or


```igor
Concatenate/O ..., DestWaveName
// Then after you are finished using DestWaveName...
WAVE DestWaveName=$""
```

### *Examples* {#examples}

```igor
// Given the following waves:
Make/N=10 w1,w2,w3
Make/N=11 w4
Make/N=(10,7) m1,m2,m3
Make/N=(10,8) m4
Make/N=(9,8) m5

// Concatenate 1D waves
Concatenate/O {w1,w2,w3},wdest      // wdest is a 10x3 matrix
Concatenate {w1,w2,w3},wdest        // wdest is a 10x6 matrix
Concatenate/NP/O {w1,w2,w3},wdest   // wdest is a 30-point 1D wave
Concatenate/O {w1,w2,w3,w4},wdest   // wdest is a 41-point 1D wave

// Concatenate 2D waves
Concatenate/O {m1,m2,m3},wdest      // wdest is a 10x7x3 volume
Concatenate/NP/O {m1,m2,m3},wdest   // wdest is a 10x21 matrix
Concatenate/O {m1,m2,m3,m4},wdest   // wdest is a 10x29 matrix
Concatenate/O {m4,m5},wdest         // wdest is a 152-point 1D wave
Concatenate/O/NP=0 {m4,m5},wdest    // wdest is a 19x8 matrix

// Concatenate 1D and 2D waves
Concatenate/O {w1,m1},wdest         // wdest is a 10x8 matrix
Concatenate/O {w4,m1},wdest         // wdest is a 81-point 1D wave

// Append rows to 2D wave
Make/O/N=(3,2) m6, m7
Concatenate/NP=0 {m6}, m7           // m7 is a 6x2 matrix

// Append columns to 2D wave
Make/O/N=(3,2) m6, m7
Concatenate/NP=1 {m6}, m7           // m7 is a 3x4 matrix

// Append layer to 2D wave
Make/O/N=(3,2) m6, m7
Concatenate/NP=2 {m6}, m7           // m7 is a 3x2x2 volume
// The last command has the same effect as:
// Concatenate {m6}, m7
// Both versions extend add a third dimension to m7
```

### *See Also* {#see-also}
[Duplicate](/igorpro/commands/duplicate.md), [Redimension](/igorpro/commands/redimension.md), [SplitWave](/igorpro/commands/splitwave.md)