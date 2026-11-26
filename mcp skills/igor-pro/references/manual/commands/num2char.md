---
description: "The num2char function returns a string containing a character. The options parameter was added in Igor Pro 7.00 and defaults to 0."
slug: /commands/num2char
---

<div className="command-signature">

## <strong>num2char</strong> (<em>num</em> [, <em>options</em> ]) {#num2char}

</div>

The num2char function returns a string containing a character.

The *options* parameter was added in Igor Pro 7.00 and defaults to 0.

As of Igor 7, Igor represents text internally as UTF-8, a form of Unicode. Previously it represented text as system text encoding. Because of this change, the behavior of num2char is complicated.

### *Recommended use of num2char in Igor 7 or later* {#recommended-use-of-num2char-in-igor-7-or-later}
If *num* is a Unicode code point, pass 0 for *options* and num2char will return a UTF-8 string containing the character for the Unicode code point represented by *num* .

If you want a string containing a single byte, even though it may not be a valid UTF-8 string, pass 1 for *options* and num2char will return a string containing the single byte whose value is *num* , provided that *num* is between 0 and 255.

### *Detailed description of num2char in Igor 7 or later* {#detailed-description-of-num2char-in-igor-7-or-later}
If *num* is between 0 and 127, num2char returns a string containing a single byte whose value is *num* . This represents an ASCII character.

If *num* is between 128 and 255 and *options* is 1, num2char returns a string containing a single byte whose value is *num* . This is not valid UTF-8 text, but it is consistent with the behavior of num2char in Igor 6.

If *num* is between 128 and 255 and *options* is 0 or omitted, num2char returns the UTF-8 representation of the character for the Unicode code point represented by *num* .

If *num* is greater than 255, num2char returns the UTF-8 representation of the character for the Unicode code point represented by *num* regardless of the value of *options* .

If you provide the *options* parameter, it must be either 0 or 1. Other values may be used for other purposes in the future.

### *Examples* {#examples}

```igor
Print num2char(65)          // Prints A
Print num2char(97)          // Prints a
Print num2char(0xF7)        // Prints division sign
Print num2char(0xF7,0)      // Prints division sign
Print num2char(0xF7,1)      // Prints missing character symbol
Print num2char(0x0127)      // Prints small letter h with stroke (h-bar)
Print num2char(0x0127,0)    // Prints small letter h with stroke (h-bar)
Print num2char(0x0127,1)    // Prints small letter h with stroke (h-bar)
// In the case of num2char(0xF7,1), num2char returns a string containing
//	a single byte whose value is 0xF7. This is not a valid UTF-8 string.
```

### *See Also* {#see-also}
[char2num](/igorpro/commands/char2num.md), [num2str](/igorpro/commands/num2str.md), [str2num](/igorpro/commands/str2num.md)

[Text Encodings](/igorpro/igor-basics/text-encodings.md)