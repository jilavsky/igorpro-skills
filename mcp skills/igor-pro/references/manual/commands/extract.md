---
description: "The Extract operation finds data in srcWave wherever LogicalExpression evaluates to TRUE and stores any matching data sequentially in destWave, which will be…"
slug: /commands/extract
---

<div className="command-signature">

## <strong>Extract</strong>  [ /FREE /INDX /O ][ <em>typeFlags</em> ] <em>srcWave</em>, <em>destWave</em>, <em>LogicalExpression</em> {#extract}

</div>

The Extract operation finds data in *srcWave* wherever *LogicalExpression* evaluates to TRUE and stores any matching data sequentially in *destWave*, which will be created if it does not already exist.

### *Parameters* {#parameters}
*srcWave*  is the name of a wave.

*destWave*  is the name of a new or existing wave that will contain the result.

*LogicalExpression*  can use any comparison or logical operator in the expression.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/FREE</span> | Creates a free *destWave* (see [Free Waves](/igorpro/programming/programming.md#free-waves)). |
|  | /FREE is allowed only in functions and only if a simple name or wave reference structure field is specified for *destWave*. |
| <span class="table-cell-nowrap">/INDX</span> | Stores the index in *destWave*  instead of data from *srcWave*. |
| <span class="table-cell-nowrap">/O</span> | Allows *destWave* to be the same as *srcWave*  (overwrite source). |

### *Type Flags (functions only)* {#type-flags-functions-only}
Extract also can use various type flags in user functions to specify the type of destination wave reference variables. These type flags do not need to be used except when it is necessary to match another wave reference variable of the same name or to tell Igor what kind of expression to compile for a wave assignment. See [WAVE Reference Types](/igorpro/programming/programming.md#wave-reference-types) and [WAVE Reference Type Flags](/igorpro/programming/programming.md#wave-reference-type-flags) for a complete list of type flags and further details.

### *Details* {#details}
*srcWave*  may be of any type including text.

*destWave*  has the same type as *srcWave*, but it is always one dimensional. With /INDX, the *destWave*  type is set to unsigned 32-bit integer and the values represent a linear index into *srcWave*  regardless of its dimensionality.

### *Example* {#example}

```igor
Make/O source= x
Extract/O source,dest,source>10 && source<20
print dest
```

Prints the following to the history area:


```
dest[0]= {11,12,13,14,15,16,17,18,19}
```

### *See Also* {#see-also}
[Duplicate](/igorpro/commands/duplicate.md)