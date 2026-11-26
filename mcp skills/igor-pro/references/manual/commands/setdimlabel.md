---
description: "The SetDimLabel operation sets the dimension label or dimension element label to the specified label."
slug: /commands/setdimlabel
---

<div className="command-signature">

## <strong>SetDimLabel</strong>  <em>dimNumber</em>,<em>dimIndex</em>,<em>label</em>,<em>wavelist</em> {#setdimlabel}

</div>

The SetDimLabel operation sets the dimension label or dimension element label to the specified label.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *dimNumber* is one of the following: |  |
| 0: | Rows |
| 1: | Columns |
| 2: | Layers |
| 3: | Chunks |

If *dimIndex*  is -1, it sets the label for the entire dimension, giving that dimension a name that appears in a table when dimension labels are displayed. This dimension-level label is distinct from the per-element labels set using `dimIndex >= 0`, and does not affect them. It has no other use.

If *dimIndex*  is >= 0, it sets the dimension label for that element of the dimension.

*label*  is a name (e.g., time), not a string (e.g., "time").

*label*  is limited to 255 bytes. If you use more than 31 bytes, your wave will require Igor Pro 8.00 or later.

### *Details* {#details}
Dimension labels can contain up to 255 bytes and may contain spaces and other normally-illegal characters allowed in liberal names if you surround the name in single quotes or if you use the $ operator to convert a string expression to a name.

Dimension labels have the same characteristics as object names. See [Object Names](/igorpro/igor-basics/using-igor.md#object-names) for a discussion of object names in general.

Prior to Igor Pro 9.00, Igor allowed you to create dimension labels containing illegal characters (double-quote, single-quote, colon, semicolon, and control characters). This is now flagged as an error. Existing experiments containing dimension labels with illegal names can still be loaded without error.

### *See Also* {#see-also}
[GetDimLabel](/igorpro/commands/getdimlabel.md), [FindDimLabel](/igorpro/commands/finddimlabel.md), [CopyDimLabels](/igorpro/commands/copydimlabels.md)

[Dimension Labels](/igorpro/igor-basics/multidimensional-waves.md#dimension-labels) and [Example: Wave Assignment and Indexing Using Labels](/igorpro/igor-basics/waves.md#example-wave-assignment-and-indexing-using-labels) for further usage details and examples.