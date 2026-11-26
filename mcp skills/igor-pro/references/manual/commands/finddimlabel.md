---
description: "The FindDimLabel function returns the index value corresponding to the label for the given dimension."
slug: /commands/finddimlabel
---

<div className="command-signature">

## <strong>FindDimLabel</strong> (<em>waveName</em>, <em>dimNumber</em>, <em>labelString</em>) {#finddimlabel}

</div>

The FindDimLabel function returns the index value corresponding to the label for the given dimension.

Returns -2 if the label is not found.

*dimNumber* is one of the following:

|  |  |
| --- | --- |
| 0: | Rows |
| 1: | Columns |
| 2: | Layers |
| 3: | Chunks |

Returns -1 if the label is for the entire dimension.

### *See Also* {#see-also}
[GetDimLabel](/igorpro/commands/getdimlabel.md), [SetDimLabel](/igorpro/commands/setdimlabel.md), [CopyDimLabels](/igorpro/commands/copydimlabels.md)