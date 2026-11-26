---
description: "The CopyDimLabels operation copies dimension labels from the source wave to the destination wave or waves."
slug: /commands/copydimlabels
---

<div className="command-signature">

## <strong>CopyDimLabels</strong>  [<em>flags</em>] <em>srcWave</em>, <em>destWave</em> [, <em>destWave</em>]... {#copydimlabels}

</div>

The CopyDimLabels operation copies dimension labels from the source wave to the destination wave or waves.

CopyDimLabels was added in Igor Pro 8.00.

Support for multiple destination waves was added in Igor Pro 9.00.

### *Flags* {#flags}
In the following flags, *dim* is 0 for the rows dimension, 1 for the columns dimension, 2 for the layers dimension, and 3 for the chunks dimension.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/ROWS = *dim*</span> | Copies the row dimension labels of *srcWave* into the *destWave* dimension specified by *dim*. |
| <span class="table-cell-nowrap">/COLS = *dim*</span> | Copies the column dimension labels of *srcWave* into the *destWave* dimension specified by *dim*. |
| <span class="table-cell-nowrap">/LAYR = *dim*</span> | Copies the layer dimension labels of *srcWave* into the *destWave* dimension specified by *dim*. |
| <span class="table-cell-nowrap">/CHNK = *dim*</span> | Copies the chunk dimension labels of *srcWave* into the *destWave* dimension specified by *dim*. |

### *Details* {#details}
If you omit all flags, CopyDimLabels copies all dimension labels in *srcWave* to the corresponding dimension labels of *destWave* for dimensions that exist in *destWave*.

You can use /ROWS, /COLS, /LAYR and /CHNK to copy dimension labels from any existing source wave dimension into any existing destination wave dimension. For example, to copy the column dimension labels of wave1 into the row dimension labels of wave2 use:


```igor
CopyDimLabels /COLS=0 wave1, wave2
```

To copy the column dimension labels of wave1 into the layer dimension labels of wave2 and the row dimension labels of wave1 into the column dimension labels of wave 2 use:


```igor
CopyDimLabels /COLS=2 /ROWS=1 wave1, wave2
```

If the source dimension has N elements and the destination dimension has M>N elements then only the first N dimension labels are set in the destination. The remaining dimension labels in the destination are unchanged.

If the source dimension has N elements and the destination dimension has M<N elements then only the first M dimension labels are copied from the source to the destination.

It is an error to attempt to copy dimension labels to a non-existent dimension in the destination.

### *See Also* {#see-also}
[FindDimLabel](/igorpro/commands/finddimlabel.md), [GetDimLabel](/igorpro/commands/getdimlabel.md), [SetDimLabel](/igorpro/commands/setdimlabel.md), [Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels)