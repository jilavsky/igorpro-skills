---
description: "The num2str function returns a string representing the number num. The optional formatStr parameter was added in Igor Pro 9.00."
slug: /commands/num2str
---

<div className="command-signature">

## <strong>num2str</strong> (<em>num</em> [, <em>formatStr</em>]) {#num2str}

</div>

The num2str function returns a string representing the number *num*.

The optional formatStr parameter was added in Igor Pro 9.00.

If you omit *formatStr*, the precision of the output string is limited to only five significant digits. This can cause unexpected and confusing results. For this reason, we recommend that that you specify a larger precision with *formatStr* or use [num2istr](/igorpro/commands/num2istr.md) or [sprintf](/igorpro/commands/sprintf.md) for more control of the format and precision of the number conversion.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| *num* | The value to be converted to string representation. |
| *formatStr* | Controls the format of the output string. See [printf](/igorpro/commands/printf.md) for details on format strings. |
|  | *formatStr* is optional and requires Igor Pro 9.00 or later. |
|  | If you omit *formatStr*, the format used is "%.5g". For more precision use something like "%.15g". |

### *See Also* {#see-also}
[printf](/igorpro/commands/printf.md), [sprintf](/igorpro/commands/sprintf.md), [str2num](/igorpro/commands/str2num.md), [num2char](/igorpro/commands/num2char.md), [char2num](/igorpro/commands/char2num.md)