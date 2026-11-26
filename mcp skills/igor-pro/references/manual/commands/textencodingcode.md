---
description: "The TextEncodingCode function returns the Igor text encoding code for the named text encoding or 0 if the text encoding is unknown."
slug: /commands/textencodingcode
---

<div className="command-signature">

## <strong>TextEncodingCode</strong> (<em>textEncodingNameStr</em>) {#textencodingcode}

</div>

The TextEncodingCode function returns the Igor text encoding code for the named text encoding or 0 if the text encoding is unknown.

The TextEncodingCode function was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*textEncodingNameStr* is an Igor text encoding name as listed under [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes).

### *Details* {#details}
Igor ignores all non-alphanumeric characters in text encoding names so "Shift JIS", "ShiftJIS", "Shift_JIS" and "Shift-JIS" are equivalent.

It also ignores leading zeros in numbers embedded in text encoding names so "ISO-8859-1" and "ISO-8859-01" are equivalent.

TextEncodingCode does a case-insensitive comparison.

### *See Also* {#see-also}
[Text Encodings](/igorpro/igor-basics/text-encodings.md), [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes), [TextEncodingName](/igorpro/commands/textencodingname.md)