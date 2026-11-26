---
description: "The Make operation creates the named waves. Use braces to assign data values when creating the wave."
slug: /commands/make
---

<div className="command-signature overload">

## <strong>Make</strong>  [<em>flags</em> ] <em>waveName</em>  [, <em>waveName</em> ]... {#make}

</div>
<div className="command-signature overload">

## <strong>Make</strong>  [<em>flags</em> ] <em>waveName</em>  [= {<em>n0</em>,<em>n1</em>,...}]... {#make}

</div>
<div className="command-signature">

## <strong>Make</strong>  [<em>flags</em> ] <em>waveName</em>  [= {{<em>n0</em>,<em>n1</em>,...},{<em>n0</em>,<em>n1</em>,...},...}]... {#make}

</div>

The Make operation creates the named waves. Use braces to assign data values when creating the wave.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/B</span> | Makes 8-bit signed integer or unsigned integer waves if /U is present. |
| <span class="table-cell-nowrap">/C</span> | Makes complex waves. |
| <span class="table-cell-nowrap">/D</span> | Makes double precision waves. |
| <span class="table-cell-nowrap">/DF</span> | Wave holds data folder references. |
|  | See [Data Folder References](/igorpro/programming/programming.md#data-folder-references) for more discussion. |
| <span class="table-cell-nowrap">/FREE[ = *nm*]</span> | Creates a free wave. Allowed only in functions and only if a simple name or wave reference structure field is specified. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for further discussion. |
|  | If *nm* is present and non-zero, then *waveName* is used as the name for the free wave, overriding the default name '\_free\_'. The ability to specify the name of a free wave was added in Igor Pro 9.00 as a debugging aid - see [Free Wave Names](/igorpro/programming/programming.md#free-wave-names) and [Wave Tracking](/igorpro/programming/programming-techniques.md#wave-tracking) for details. |
| <span class="table-cell-nowrap">/I</span> | Makes 32-bit signed integer or unsigned integer waves if /U is present. |
| <span class="table-cell-nowrap">/L</span> | Makes 64-bit signed integer or unsigned integer waves if /U is present. Requires Igor Pro 7.00 or later. |
| <span class="table-cell-nowrap">/N = *n*</span> | *n* is the number of points each wave will have. If n is an expression, it must be enclosed in parentheses: |
|  | <code class="igor">Make/N=(myVar+1) aNewWave</code> |
| <span class="table-cell-nowrap">/N = (*n1*, *n2*, *n3*, *n4*)</span> |  |
|  | *n1*, *n2*, *n3*, *n4* specify the number of rows, columns, layers and chunks each wave will have. Trailing zeros can be omitted (e.g., /N=(*n1*, *n2*, 0, 0) can be abbreviated as /N=(*n1*, *n2*)). |
| <span class="table-cell-nowrap">/O</span> | Overwrites existing waves in case of a name conflict. After an overwrite, you cannot rely on the contents of the waves and you will need to reinitialize them or to assign appropriate starting values. |
| <span class="table-cell-nowrap">/R</span> | Makes real value waves (default). |
| <span class="table-cell-nowrap">/T</span> | Makes text waves. |
| <span class="table-cell-nowrap">/T = *size*</span> | Makes text waves with pre-allocated storage. |
|  | *size* is the number of bytes preallocated by Igor for each element in each text wave. The waves are not initialized - it is up to you to initialize them. |
|  | Preallocation can dramatically speed up text wave assignment when the wave has a very large number of points but only when all strings assigned to the wave are exactly the same size as the preallocation size. |
| <span class="table-cell-nowrap">/U</span> | Makes unsigned integer waves. |
| <span class="table-cell-nowrap">/W</span> | Makes 16-bit signed integer or unsigned integer waves if /U is present. |
| <span class="table-cell-nowrap">/Y = *type*</span> | See ***Wave Data Types*** below. |
| <span class="table-cell-nowrap">/WAVE</span> | Wave holds wave references. |
|  | See [Wave References](/igorpro/programming/programming.md#wave-references) for more discussion. |

### *Wave Data Types* {#wave-data-types}
You can use /Y=(*numType*) to set the data type instead of the /B, /C, /D, /I, /L, /R, /T, /U, and /W data type flags. See [WaveType](/igorpro/commands/wavetype.md) for *numType* values. The /Y flag overrides other type flags. You still need to use the explicit data type flags to control the automatic wave reference created by the compiler if you use the wave in an assignment statement in the same function; see [Automatic Creation of WAVE References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details.

### *Details* {#details}
Unless overridden by the flags, the created waves have the default length, type, precision, units and scaling:


| Property | Default |
| --- | --- |
| Number of points | 128 |
| Precision | Single precision floating point |
| Type | Real |
| x, y, z, and t scaling | x0=0, Δx=1 ("point scaling") |
| x, y, z, and t units | "" (blank) |
| Data Full Scale | 0, 0 |
| Data units | "" (blank) |

The maximum allowed number of elements (*rows* \* *columns* \* *layers* \* *chunks*) in a wave is 214,700,000,000.

:::note
The preferred precision set by the Miscellaneous Settings dialog only presets the Make Waves dialog checkbox, and determines the precision of imported waves. It does not affect the Make operation.
:::

### *See Also* {#see-also}

[SetScale](/igorpro/commands/setscale.md), [Duplicate](/igorpro/commands/duplicate.md), [Redimension](/igorpro/commands/redimension.md)