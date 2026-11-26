---
description: "The Duplicate operation creates new waves; the names of which are specified by destWaveNames and the contents, data type and scaling of which are identical to…"
slug: /commands/duplicate
---

<div className="command-signature">

## <strong>Duplicate</strong>  [ /FREE[=<em>nm</em>] /O /R=(<em>startX</em>,<em>endX</em> )[(<em>startY</em>, <em>endY</em> )...]] [<em>typeFlags</em> ] <em>srcWaveName</em>, <em>destWaveName</em> [, <em>destWaveName</em> ]... {#duplicate}

</div>

The Duplicate operation creates new waves; the names of which are specified by *destWaveNames* and the contents, data type and scaling of which are identical to *srcWaveName*.

### *Parameters* {#parameters}
*srcWaveName* must be the name of an existing wave.

The *destWaveNames* should be wave names not currently in use unless the /O flag is used to overwrite existing waves, or the /FREE flag is used.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FREE[ = *nm*]</span> | Creates a free wave. Allowed only in functions and only if a simple name or wave reference structure field is specified. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for further discussion. |
|  | A wave reference variable is created for each *destWaveName*. That is how you refer to each new free wave in your function. If a wave reference with that name already exists, it is reset to point to the new free wave. The fate of the previous wave depends on whether it was a free wave or a global wave and on whether there are other wave references that refer to the old wave. See [Wave References](/igorpro/programming/programming.md#wave-references). |
|  | If *nm* is present and non-zero, then *destWaveName* is used as the name of the free wave, overriding the default name '\_free\_'. The ability to specify the name of a free wave was added in Igor Pro 9.00 as a debugging aid - see [Free Wave Names](/igorpro/programming/programming.md#free-wave-names) and [Wave Tracking](/igorpro/programming/programming-techniques.md#wave-tracking) for details. |
| <span class="table-cell-nowrap">/O</span> | Existing waves with the same name as a *destWaveName* are overwritten. |
|  | If the /FREE flag is present, the /O flag is ignored because free waves are always newly created. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX* )</span> | Specifies an X range in the source wave from which the destination wave is created. See Details for further discussion of /R. |
| <span class="table-cell-nowrap">/R = (*startX*,*endX* )(*startY*,*endY*)</span> |  |
|  | Specifies both X and Y range. Further dimensions are constructed analogously. See Details for further discussion of /R. |
| <span class="table-cell-nowrap">/R = [*startP*,*endP* ]</span> | Specifies a row range in the source wave from which the destination wave is created. Further dimensions are constructed just like the scaled dimension ranges. See Details for further discussion of /R. |
| <span class="table-cell-nowrap">/RMD = [*firstRow*, *lastRow* ][*firstColumn*, *lastColumn* ][*firstLayer*, *lastLayer* ][*firstChunk*, *lastChunk* ]</span> |  |
|  | Designates a contiguous range of data in the source wave to which the operation is to be applied. This flag was added in Igor Pro 7.00. |
|  | You can include all higher dimensions by leaving off the corresponding brackets. For example: |
|  | <code class="igor">/RMD=[firstRow,lastRow]</code> |
|  | includes all available columns, layers and chunks. |
|  | You can use empty brackets to include all of a given dimension. For example: |
|  | <code class="igor">/RMD=[][firstColumn,lastColumn]</code> |
|  | means "all rows from firstColumn to lastColumn". |
|  | You can use a * to specify the end of any dimension. For example: |
|  | <code class="igor">/RMD=[firstRow,*]</code> |
|  | means "from firstRow through the last row". |

### *Type Flags (functions only)* {#type-flags-functions-only}
When used in user defined functions, Duplicate can also take the /B, /C, /D, /I, /S, /U, /W, /T, /DF and /WAVE flags. This does not affect the result of the Duplicate operation - these flags are used only to tell Igor what kind of wave is expected at runtime.

This information is used by Igor if, later in the function, you create a wave assignment statement using a duplicated wave as the destination:


```igor
Function DupIt(wv)
	WAVE/C wv               // complex wave

	Duplicate/O/C wv,dupWv  // tell Igor that dupWv is complex 
	dupWv[0]=cmplx(5.0,1.0) // no error, because dupWv known complex
	...
```

If Duplicate did not have the /C flag, Igor would complain with a "function not available for this number type" message when it tried to compile the assignment of dupWv to the result of the cmplx function.

These type flags do not need to be used except when it is necessary to match another wave reference variable of the same name or to tell Igor what kind of expression to compile for a wave assignment. See [WAVE Reference Types](/igorpro/programming/programming.md#wave-reference-types) and [WAVE Reference Type Flags](/igorpro/programming/programming.md#wave-reference-type-flags) for a complete list of type flags and further details.

### *Details* {#details}
If /R is omitted, the entire wave is duplicated.

In the range specifications used with /R, a * for the end means duplicate to the end. You can also simply leave out the end specification. To include all of a given dimension, use /R=[]. If you leave off higher dimensions, all those dimensions are duplicated. That is, /R=[1,5] for a 2D wave is equivalent to /R=[1,5][].

The destination wave will always be unlocked, even if the source wave was locked.

:::warning
Under some circumstances, such as in loops in user-defined functions, Duplicate may exhibit undesired behavior.
:::

When you use

```igor
Duplicate/O srcWave, DestWaveName
```

in a user-defined function, a local WAVE variable named DestWaveName is created at compile time. At runtime, if the WAVE variable is NULL, a wave of the same name will be created in the current data folder. If, however, the WAVE variable is not NULL, as it would be in a loop, then the referenced wave will be overwritten no matter where it is located. If the desired behavior is to create (or overwrite) a wave in the current data folder, you should use one of the following two methods:


```igor
Duplicate/O srcWave,$"DestWaveName"
WAVE DestWaveName	// needed only if you need to reference the dest wave
```

or


```igor
Duplicate/O srcWave,DestWaveName
// then after you are finished using DestWaveName...
WAVE DestWaveName=$""
```

### *See Also* {#see-also}
[Rename](/igorpro/commands/rename.md), [Concatenate](/igorpro/commands/concatenate.md), [SplitWave](/igorpro/commands/splitwave.md)