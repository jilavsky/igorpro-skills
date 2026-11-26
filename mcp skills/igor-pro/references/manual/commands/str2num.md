---
description: "The str2num function returns a number represented by the string expression str."
slug: /commands/str2num
---

<div className="command-signature">

## <strong>str2num</strong> (<em>str</em>) {#str2num}

</div>

The str2num function returns a number represented by the string expression *str*.

### *Details* {#details}
str2num returns NaN if *str* does not contain the text for a number.

str2num skips leading spaces and tabs and then reads up to the first non-numeric character.

### *See Also* {#see-also}
[num2char](/igorpro/commands/num2char.md), [char2num](/igorpro/commands/char2num.md), [num2str](/igorpro/commands/num2str.md)

[sscanf](/igorpro/commands/sscanf.md) for more complex parsing jobs.