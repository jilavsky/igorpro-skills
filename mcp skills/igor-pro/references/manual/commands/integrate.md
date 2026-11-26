---
description: "The Integrate operation calculates the 1D numeric integral of a wave. The X scaling of each wave is taken into account."
slug: /commands/integrate
---

<div className="command-signature">

## <strong>Integrate</strong>  [/DIM = <em>d</em>  /METH=<em>m</em>  /P/T][<em>typeFlags</em> ] <em>yWaveA</em>  [/X = <em>xWaveA</em> ][/D = <em>destWaveA</em> ] [, <em>yWaveB</em>  [/X = <em>xWaveB</em> ][/D = <em>destWaveB</em> ][, ...]] {#integrate}

</div>

The Integrate operation calculates the 1D numeric integral of a wave. The X scaling of each wave is taken into account. Rectangular integration is used by default.

Integrate is multi-dimension-aware in the sense that it computes a 1D integration along the single dimension specified by the /DIM flag or along the rows dimension if you omit /DIM.

Complex waves have their real and imaginary components integrated individually.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D = *destWave*</span> | Specifies the name of the wave to hold the integrated data. It creates destWave if it does not already exist or overwrites it if it exists. This flag must follow the source wave name. |
| <span class="table-cell-nowrap">/DIM = *d*</span> | Specifies the wave dimension along which to integrate when *yWave* is multidimensional. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=-1:</td><td>Treats entire wave as 1D (default).</td></tr><tr><td>*d*&nbsp;&gt;=&nbsp;0</td><td>Integrate operates along rows, columns, layers or chunks.</td></tr></tbody></table>
|  | For example, for a 2D wave, /DIM=0 integrates each row and /DIM=1 integrates each column. |
| <span class="table-cell-nowrap">/METH = *m*</span> | Sets the integration method. |
|  |<table class="nested-table"><tbody><tr><td>*m*&nbsp;=0:</td><td>Rectangular integration (default). Results at a point are stored at the same point (rather than at the next point as for /METH=2). This method keeps the dimension size the same.</td></tr><tr><td>*m*&nbsp;=1:</td><td>Trapezoidal integration.</td></tr><tr><td>*m*&nbsp;=2:</td><td>Rectangular integration. Results at a point are stored at the next point (rather than at the same point as for /METH=0). This method increases the dimension size by one to provide a place for the last bin.</td></tr></tbody></table>


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/P</span> | Forces point scaling. |
| <span class="table-cell-nowrap">/T</span> | Trapezoidal integration. Same as /METH=1. |
| <span class="table-cell-nowrap">/X = *xWave*</span> | Specifies the name of corresponding X wave. This flag must follow the source wave name. |

### *Type Flags (functions only)* {#type-flags-functions-only}
Integrate also can use various type flags in user functions to specify the type of destination wave reference variables. These type flags do not need to be used except when it is necessary to match another wave reference variable of the same name or to tell Igor what kind of expression to compile for a wave assignment. See [WAVE Reference Types](/igorpro/programming/programming.md#wave-reference-types) and [WAVE Reference Type Flags](/igorpro/programming/programming.md#wave-reference-type-flags) for a complete list of type flags and further details.

For example, when the input waves are complex, the output wave will be complex. To get the Igor compiler to create a complex output wave reference, use the /C type flag with /D=*destwave* :


```igor
Make/O/C cInput=cmplx(sin(p/8), cos(p/8))
Make/O/C/N=0 cOutput
Integrate/C cInput /D=cOutput
```

### *Details* {#details}
The computation equation for rectangular integration using /METH=0 is:

$$
\displaystyle { waveOut }[p]=\sum_{i=0}^{p} { waveIn }[i] \cdot \Delta x .
$$

The computation equation for rectangular integration using /METH=2 is:

$$
\begin{array}{l}
\displaystyle { waveOut }[0]=0\\
\\
\displaystyle { waveOut }[p+1]=\sum_{i=0}^{p}\left(x_{i+1}-x_{i}\right) { waveIn }[i] .
\end{array}
$$

The inverse of this rectangular integration is the backwards difference.

Trapezoidal integration is a more accurate method of computing the integral than rectangular integration. The computation equation is:

$$
\begin{array}{l}
\displaystyle { waveOut }[0]=0 \\
\\
\displaystyle { waveOut }[p]={ waveOut }[p-1]+\frac{\Delta x}{2}({ waveIn }[p-1]+{ waveIn }[p]) .
\end{array}
$$

If the optional /D = destWave flag is omitted, then the wave is integrated in place overwriting the source wave.

When using an X wave, the X wave must match the Y wave data type (excluding the complex type flag) and it must be 1D with the number points plus one matching the size of the dimension for rectangular integration. X waves with number points plus one are allowed for rectangular integration with methods needing only the number of points. X waves are not used with integer source waves.

Although it is mathematically suspect, rectangular integration using /METH=0 would be correct if the X scaling of the output wave is offset by DX.

`Differentiate/METH=1/EP=1` is the inverse of `Integrate/METH=2`, but `Integrate/METH=2` is the inverse of `Differentiate/METH=1/EP=1` only if the original first data point is added to the output wave.

Integrate applied to an XY pair of waves does not check the ordering of the X values and doesn't care about it. However, it is usually the case that your X values should be monotonic. If your X values are not monotonic, you should be aware that the X values will be taken from your X wave in the order they are found, which will result in random X intervals for the X differences. It is usually best to sort the X and Y waves first (see [Sort](/igorpro/commands/sort.md)).

### *See Also* {#see-also}
[Differentiate](/igorpro/commands/differentiate.md), [Integrate1D](/igorpro/commands/integrate1d.md), [Integrate2D](/igorpro/commands/integrate2d.md), [area](/igorpro/commands/area.md),  [areaXY](/igorpro/commands/areaxy.md)