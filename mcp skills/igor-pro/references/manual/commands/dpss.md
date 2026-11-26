---
description: "The DPSS operation generates Slepian's Discrete Prolate Spheroidal Sequences."
slug: /commands/dpss
---

<div className="command-signature">

## <strong>DPSS</strong>  [<em>flags</em>] <em>numPoints</em>, <em>numWindows</em> {#dpss}

</div>

The DPSS operation generates Slepian's Discrete Prolate Spheroidal Sequences.

The DPSS operation was added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Saves the DPSS in a wave specified by *destWave*. The destination wave is overwritten if it exists. |
|  | Creates a wave reference for the destination wave in a user function. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If you omit /DEST the operation saves the result in the wave M_DPSS in the current data folder. |
| <span class="table-cell-nowrap">/EV = *evWave*</span> | Saves the first *numWindows*  eigenvalues in a wave specified by *evWave*. The eigenvalues are computed for a symmetric tridiagonal matrix. They are real, positive and close to 1. They can be used to estimate bias in multitaper calculations. |
| <span class="table-cell-nowrap">/FREE</span> | Creates output waves as free waves. |
|  | /FREE is permitted in user-defined functions only, not from the command line or in macros. |
|  | If you use /FREE then *destWave* , *evWave*  and *sumsWave*  must be simple names, not paths. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for details on free waves. |
| <span class="table-cell-nowrap">/NW = *nw*</span> | Specifies the time-bandwidth product. This value should typically be in the range [2,6]. Given a time-bandwidth product *nw* it is recommended to use no more than 2\**nw* tapers in order to maximize variance efficiency. The default value of the time-bandwidth product is 3. |
| <span class="table-cell-nowrap">/DTPS = *sumsWave*</span> |  |
|  | Saves the sums of the generated DPSS windows in a wave specified by *sumsWave*. |
| <span class="table-cell-nowrap">/Q</span> | Suppress printing information in the history. |
| <span class="table-cell-nowrap">/Z</span> | Suppress errors. The variable V_Flag is set to 0 if successful and to -1 otherwise. |

### *Details* {#details}
DPSS generates Slepian's Discrete Prolate Spheroidal Sequences in a 2D double-precision wave of dimensions *numPoints* by *numWindows*.

If you do omit /DEST the operation creates the output wave M_DPSS in the current data folder. The sequences/tapers are arranged as columns in the output wave.

### *Examples* {#examples}

```igor
DPSS/DEST=dpss5 1000,5				
Display dpss5[][0],dpss5[][1],dpss5[][2],dpss5[][3],dpss5[][4]
ModifyGraph rgb(dpss5#1)=(0,65535,0),rgb(dpss5#2)=(1,16019,65535)
ModifyGraph rgb(dpss5#3)=(65535,0,52428),rgb(dpss5#4)=(0,0,0)

// Different sequences are orthogonal
MatrixOp/o aa=col(dpss5,1)*col(dpss5,4)
Integrate/METH=1 aa/D=W_INT
Print W_INT[numpnts(W_INT)-1]
```

### *See Also* {#see-also}
[MultiTaperPSD](/igorpro/commands/multitaperpsd.md), [WindowFunction](/igorpro/commands/windowfunction.md), [ImageWindow](/igorpro/commands/imagewindow.md), [Hanning](/igorpro/commands/hanning.md)

### *References* {#references}
D. Slepian, "Prolate spheroidal wave functions, Fourier analysis and uncertainty -- V: The discrete case.", Bell Syst. Tech J., vol 57 pp. 1317-1430, May 1978.