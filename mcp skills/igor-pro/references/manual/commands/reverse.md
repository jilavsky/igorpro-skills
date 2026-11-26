---
description: "The Reverse operation reverses data in a wave along a specified dimension. It does not accept text waves."
slug: /commands/reverse
---

<div className="command-signature">

## <strong>Reverse</strong>  [/DIM=<em>d</em> /P][<em>typeFlags</em> ] <em>waveA</em>  [/D=<em>destWaveA</em> ] [, <em>waveB</em> [/D=<em>destWaveB</em> ] [,...]] {#reverse}

</div>

The Reverse operation reverses data in a wave along a specified dimension. It does not accept text waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D = *destWave*</span> | Specifies the name of the wave to hold the reversed data. Creates *destWave* if it does not already exist or overwrites it if it exists. This flag must follow the source wave name. |
| <span class="table-cell-nowrap">/DIM = *d*</span> | Specifies the wave dimension to reverse. |
|  |<table class="nested-table"><tbody><tr><td>*d*&nbsp;=-1:</td><td>Treats entire wave as 1D (default).</td></tr><tr><td>*d*&nbsp;&gt;=&nbsp;0:</td><td>Operates along rows, columns, etc.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P</span> | Suppresses adjustment of dimension scaling. Without /P the scaled dimension value of reversed points remains the same. |

### *Type Flags (functions only)* {#type-flags-functions-only}
Reverse also can use various type flags in user functions to specify the type of destination wave reference variables. These type flags do not need to be used except when it is necessary to match another wave reference variable of the same name or to tell Igor what kind of expression to compile for a wave assignment. See [WAVE Reference Types](/igorpro/programming/programming.md#wave-reference-types) and [WAVE Reference Type Flags](/igorpro/programming/programming.md#wave-reference-type-flags) for a complete list of type flags and further details.

### *Details* {#details}
If the optional /D=*destWave* flag is omitted, then the wave is reversed in place.

### *See Also* {#see-also}
[Sorting](/igorpro/analysis/analysis.md#sorting), [Sort](/igorpro/commands/sort.md), [SortColumns](/igorpro/commands/sortcolumns.md)