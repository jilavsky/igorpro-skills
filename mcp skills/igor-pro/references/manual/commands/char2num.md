---
description: "The char2num function returns a numeric code representing the first byte of str or the first character of str."
slug: /commands/char2num
---

<div className="command-signature">

## <strong>char2num</strong> (<em>str</em>) {#char2num}

</div>

The char2num function returns a numeric code representing the first byte of *str* or the first character of *str* .

If *str* contains zero bytes, char2num returns NaN.

If *str* contains exactly one byte, char2num returns the value of that byte, treated as a signed byte. For backward compatibility with Igor 6, if the input is a single byte in the range 0x80..0xFF, char2num returns a negative number.

If *str* contains more than one byte, char2num returns a number which is the Unicode code point for the first character in *str* treated as UTF-8 text. If *str* does not start with a valid UTF-8 character, char2num returns NaN.

Prior to Igor Pro 7.00, char2num always returned the value of the first byte, treated as a signed byte.

### *Examples* {#examples}

```igor
Function DemoChar2Num()
	String str
	
	str = "A"
	Printf "Single ASCII character: %02X\r", char2num(str)          // Prints 0x41
	
	str = "ABC"
	Printf "Multiple ASCII characters: %02X\r", char2num(str)       // Prints 0x41
	
	str = U+2022                                                    // Bullet character
	Printf "Valid UTF-8 text: U+%04X\r", char2num(str)              // Prints U+2022
	Printf "First byte value: %02X\r", char2num(str[0]) & 0xFF      // Prints E2
	Printf "Second byte value: %02X\r", char2num(str[1]) & 0xFF     // Prints 80
	
	str = num2char(0xE2, 1) + num2char(0x41, 1)                     // Invalid UTF-8 text
	Printf "Invalid UTF-8 text: %g\r", char2num(str)                // Prints NaN
	
	str = ""
	Printf "Empty string: %g\r", char2num(str)                      // Prints NaN
End
```

### *See Also* {#see-also}
[num2char](/igorpro/commands/num2char.md), [num2str](/igorpro/commands/num2str.md), [str2num](/igorpro/commands/str2num.md)

[Text Encodings](/igorpro/igor-basics/text-encodings.md)