---
description: "The GetDimLabel function returns a string containing the label for the given dimension or dimension element."
slug: /commands/getdimlabel
---

<div className="command-signature">

## <strong>GetDimLabel</strong> (<em>waveName</em>, <em>dimNumber</em>, <em>dimIndex</em>) {#getdimlabel}

</div>

The GetDimLabel function returns a string containing the label for the given dimension or dimension element.

*dimNumber* is one of the following:

|  |  |
| --- | --- |
| 0: | Rows |
| 1: | Columns |
| 2: | Layers |
| 3: | Chunks |

If *dimIndex* is -1, it returns the label for the entire dimension. If *dimIndex* is >= 0, it returns the dimension label for that element of the dimension.

### *See Also* {#see-also}
[SetDimLabel](/igorpro/commands/setdimlabel.md), [FindDimLabel](/igorpro/commands/finddimlabel.md), [CopyDimLabels](/igorpro/commands/copydimlabels.md), [Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels)