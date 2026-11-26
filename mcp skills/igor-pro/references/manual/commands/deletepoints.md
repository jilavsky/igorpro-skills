---
description: "The DeletePoints operation deletes numElements elements from the named waves starting from element startElement."
slug: /commands/deletepoints
---

<div className="command-signature">

## <strong>DeletePoints</strong>  [/M=<em>dim</em> ] <em>startElement</em>, <em>numElements</em>, <em>waveName</em> [, <em>waveName</em> ]... {#deletepoints}

</div>

The DeletePoints operation deletes *numElements* elements from the named waves starting from element *startElement*.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/M = *dim*</span> | *dim*  specifies the dimension from which elements are to be deleted. Values are 0 for rows, 1 for columns, 2 for layers, 3 for chunks. If /M is omitted, DeletePoints deletes from the rows dimension. |

### *Details* {#details}
A wave may have any number of points, including zero. Removing all elements from any dimension removes all points from the wave, leaving a 1D wave with zero points.

Except for the case of removing all elements, DeletePoints does not change the dimensionality of a wave. Use [Redimension](/igorpro/commands/redimension.md) for that.

### *See Also* {#see-also}
[Redimension](/igorpro/commands/redimension.md)

### *Demos* {#demos}
[Open Delete Points From Wave Demo](#igor-pxp/Examples/Techniques/Delete__Points__From__Wave.pxp)

[Open Delete XY Points Demo](#igor-pxp/Examples/Techniques/Delete__XY__Points__Demo.pxp)