---
description: "The InsertPoints operation inserts numElements points in front of point beforeElement in each waveName. The new elements have the value zero."
slug: /commands/insertpoints
---

<div className="command-signature">

## <strong>InsertPoints</strong>  [ /M=<em>dim</em> /V=<em>value</em> ] <em>beforeElement</em>, <em>numElements</em>, <em>waveName</em> [, <em>waveName</em> ]... {#insertpoints}

</div>

The InsertPoints operation inserts *numElements*  points in front of point *beforeElement*  in each *waveName*. The new elements have the value zero.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/M = *dim*</span> | *dim*  specifies the dimension into which elements are to be inserted. Values are 0 for rows, 1 for columns, 2 for layers, 3 for chunks. If /M is omitted, InsertPoints inserts in the rows dimension. |
| <span class="table-cell-nowrap">/V = *value*</span> | When used with numeric waves, *value* specifies the value for new elements. If you omit /V, new elements are set to zero. The /V flag was added in Igor Pro 8.00. |

### *Details* {#details}
Trying to insert points into any but the rows of a zero-point wave results in a zero-point wave. You must first make the number of rows nonzero before anything else has an effect.

### *See Also* {#see-also}
[Lists of Values](/igorpro/igor-basics/waves.md#lists-of-values)