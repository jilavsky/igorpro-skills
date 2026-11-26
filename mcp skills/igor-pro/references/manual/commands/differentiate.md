---
description: "The Differentiate operation calculates the 1D numerical derivative of a wave."
slug: /commands/differentiate
---

<div className="command-signature">

## <strong>Differentiate</strong>  [/DIM = <em>d</em>  /EP=<em>e</em>  /METH=<em>m</em>  /P ][<em>typeFlags</em> ] <em>yWaveA</em>  [/X=<em>xWaveA</em> ] [/D=<em>destWaveA</em> ][, <em>yWaveB</em>  [/X=<em>xWaveB</em> ][/D=<em>destWaveB</em> ][, ...]] {#differentiate}

</div>

The Differentiate operation calculates the 1D numerical derivative of a wave.

Differentiate is multi-dimension-aware in the sense that it computes a 1D differentiation along the single dimension specified by the /DIM flag or along the rows dimension if you omit /DIM.

Complex waves have their real and imaginary components differentiated individually.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D = *destWave*</span> | Specifies the name of the wave to hold the differentiated data. It creates *destWave* if it does not already exist or overwrites it if it exists. This flag must follow the source wave name. |
| <span class="table-cell-nowrap">/DIM = *d*</span> | Specifies the wave dimension along which to differentiate when *yWave*  is multidimensional. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=-1:</td><td>Treats entire wave as 1D (default).</td></tr></tbody></table>
|  | For *d* =0, 1, 2, 3, Differentiate operates along rows, columns, layers or chunks. |
|  | For example, for a 2D wave, /DIM=0 differentiates each row and /DIM=1 differentiates each column. |
| <span class="table-cell-nowrap">/EP = *e*</span> | Controls end point handling. |
|  |<table class="nested-table"><tbody><tr><td>*e*&nbsp;=0:</td><td>Replaces undefined points with an approximation (default).</td></tr><tr><td>*e*&nbsp;=1:</td><td>Deletes the point(s).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/METH = *m*</span> | Sets the differentiation method. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Central difference (default).</td></tr><tr><td>*m*&nbsp;=1:</td><td>Forward difference.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Backward difference.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P</span> | Forces point scaling. |
| <span class="table-cell-nowrap">/X = *xWave*</span> | Specifies the name of the corresponding X wave. This flag must follow the source wave name. |

### *Type Flags (functions only)* {#type-flags-functions-only}
Differentiate also can use various type flags in user functions to specify the type of destination wave reference variables. These type flags do not need to be used except when it is necessary to match another wave reference variable of the same name or to tell Igor what kind of expression to compile for a wave assignment. See [WAVE Reference Types](/igorpro/programming/programming.md#wave-reference-types) and [WAVE Reference Type Flags](/igorpro/programming/programming.md#wave-reference-type-flags) for a complete list of type flags and further details.

For example, when the input waves are complex, the output wave will be complex. To get the Igor compiler to create a complex output wave reference, use the /C type flag with /D=*destwave* :


```igor
Make/O/C cInput=cmplx(sin(p/8), cos(p/8))
Make/O/C/N=0 cOutput
Differentiate/C cInput /D=cOutput
```

### *Details* {#details}
If the optional /D = *destWave*  flag is omitted, then the wave is differentiated in place.

When using a method that deletes points (/EP=1) with a multidimensional wave, deletion is not done if no dimension is specified.

When using an X wave, the X wave must match the Y wave data type (excluding the complex type flag) and it must be 1D with the number points matching the size of the dimension being differentiated. X waves are not used with integer source waves.

`Differentiate/METH=1/EP=1` is the inverse of `Integrate/METH=2`, but `Integrate/METH=2` is the inverse of `Differentiate/METH=1/EP=1` only if the original first data point is added to the output wave.

Differentiate applied to an XY pair of waves does not check the ordering of the X values and doesn't care about it. However, it is usually the case that your X values should be monotonic. If your X values are not monotonic, you should be aware that the X values will be taken from your X wave in the order they are found, which will result in random X intervals for the X differences. It is usually best to sort the X and Y waves first using [Sort](/igorpro/commands/sort.md).

### *See Also* {#see-also}
[Integrate](/igorpro/commands/integrate.md)