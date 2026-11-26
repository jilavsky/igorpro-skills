---
description: "The PadString function returns a string identical to str except that it has been extended to a total length of finalLength using bytes of padValue."
slug: /commands/padstring
---

<div className="command-signature">

## <strong>PadString</strong> (<em>str</em>, <em>finalLength</em>, <em>padValue</em>) {#padstring}

</div>

The PadString function returns a string identical to *str* except that it has been extended to a total length of *finalLength* using bytes of *padValue*. Use zero to create a C-language style string or use 0x20 to pad with spaces (FORTRAN style). This is useful when reading or writing binary files using [FBinRead](/igorpro/commands/fbinread.md) and [FBinWrite](/igorpro/commands/fbinwrite.md).

### *See Also* {#see-also}
[UnPadString](/igorpro/commands/unpadstring.md), [ReplaceString](/igorpro/commands/replacestring.md), [ReplicateString](/igorpro/commands/replicatestring.md)