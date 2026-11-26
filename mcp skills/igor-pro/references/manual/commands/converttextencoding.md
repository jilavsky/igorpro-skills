---
description: "ConvertTextEncoding converts text from one text encoding to another. The ConvertTextEncoding function was added in Igor Pro 7.00."
slug: /commands/converttextencoding
---

<div className="command-signature">

## <strong>ConvertTextEncoding</strong> (<em>sourceTextStr</em>, <em>sourceTextEncoding</em>, <em>destTextEncoding</em>, <em>mapErrorMode</em>, <em>options</em>) {#converttextencoding}

</div>

ConvertTextEncoding converts text from one text encoding to another.

The ConvertTextEncoding function was added in Igor Pro 7.00.

All text in memory is assumed to be in UTF-8 format except for text stored in waves which can be stored in any text encoding. You might want to convert text from UTF-8 to Windows-1252 (Windows Western European), for example, to export it to a program that expects Windows-1252.

You might have text already loaded into Igor that you know to be in Windows-1252. To display it correctly, you need to convert it to UTF-8.

You can also use ConvertTextEncoding to test if text is valid in a given text encoding, by specifying the same text encoding for *sourceTextEncoding* and *destTextEncoding*.

### *Parameters* {#parameters}
*sourceTextStr* is the text that you want to convert.

*sourceTextEncoding* specifies the source text encoding.

*destTextEncoding* specifies the output text encoding.

See [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes) for a list of acceptable text encoding codes.

*mapErrorMode* determines what happens if an input character cannot be mapped to the output text encoding because the character does not exist in the output text encoding. It takes one of these values:


|  |  |
| --- | --- |
| 1: | Generate error. The function returns "" and generates an error. |
| 2: | Return a substitute character for the unmappable character. The substitute character for Unicode is the Unicode replacement character, � (U+FFFD). For most non-Unicode text encodings it is either control-Z or a question mark. |
| 3: | Skip unmappable input character. |
| 4: | Return an escape sequence representing the unmappable code point. |
|  | If the source text is valid in the source text encoding but cannot be represented in the destination text encoding, unmappable characters are replaced with \\uXXXX where XXXX specifies the UTF-16 code point of the unmappable character in hexadecimal. The DemoUnmappable example function below illustrates this. |
|  | If the conversion cannot be done because the source text is not valid in the source text encoding, invalid bytes are replaced with \\xXX where XX specifies the value of the invalid byte in hexadecimal. The DemoInvalid example function below illustrates this. |
|  | If mapErrorMode is 2, 3 or 4, the function does not return an error in the event of an unmappable character. |


|  |  |
| --- | --- |
| *options* is a bitwise parameter which defaults to 0 and with the bits defined as follows: |  |
| Bit 0: | If cleared, in the event of a text conversion error, a null string is returned and an error is generated. Use this if you want to abort procedure execution if an error occurs. |
|  | If set, in the event of a text conversion error, a null string is returned but no error is generated. Use this if you want to detect and handle a text conversion error. You can test for null using strlen as shown in the example below. |
| Bit 1: | If cleared (default), null bytes in *sourceTextStr* are considered invalid and ConvertTextEncoding returns an error. If set, null bytes are considered valid. |
| Bit 2: | If cleared (default) and *sourceTextEncoding* and *destTextEncoding* are the same, ConvertTextEncoding attempts to do the conversion anyway. If *sourceTextStr* is invalid in the specified text encoding, the issue is handled according to *mapErrorMode*. This allows you check the validity of text whose text encoding you think you know, by passing 1 for *mapErrorMode* and 5 for *options* . Use [strlen](/igorpro/commands/strlen.md) to test if the returned string is null, indicating that *sourceTextStr* is not valid in the specified text encoding. |
|  | If set and *sourceTextEncoding* and *destTextEncoding* are the same, ConvertTextEncoding merely returns *sourceTextStr* without doing any conversion. |

All other bits are reserved and must be cleared.

### *Details* {#details}
ConvertTextEncoding returns a null result string if *sourceTextEncoding* or *destTextEncoding* are not valid text encoding codes or if a text conversion error occurs. You can test for a null string using [strlen](/igorpro/commands/strlen.md) which returns NaN if the string is null.

If bit 0 of the *options* parameter is cleared, Igor generates an error which halts procedure execution. If it is set, Igor generates no error and you should test for null and attempt to handle the error, as illustrated by the example below.

A text conversion error occurs if *mapErrorMode* is 1 and the source text contains one or more characters that are not mappable to the destination text encoding. A text conversion error also occurs if the source text contains a sequence of bytes that is not valid in the source text encoding.

The "binary" text encoding (255) is not a real text encoding. If either *sourceTextEncoding* or *destTextEncoding* are binary (255), ConvertTextEncoding does no conversion and just returns *sourceTextStr* unchanged.

See [Text Encodings](/igorpro/igor-basics/text-encodings.md) for further details.

### *Example* {#example}
In reading these examples, keep in mind that Igor converts escape codes such as "\\u8C4A", when they appear in literal text, to the corresponding UTF-8 character. See [Unicode Escape Sequences in Strings](/igorpro/programming/commands.md#unicode-escape-sequences-in-strings) for details.


```igor
Function DemoConvertTextEncoding()
	// Get text encoding codes for text the text encodings used below
	Variable textEncodingUTF8 = TextEncodingCode("UTF-8")
	Variable textEncodingWindows1252 = TextEncodingCode("Windows-1252")
	Variable textEncodingShiftJIS = TextEncodingCode("ShiftJIS")

	// Convert from Windows-1252 to UTF-8
	String source = "Division sign: " + num2char(0xF7)
	String result = ConvertTextEncoding(source, textEncodingWindows1252, textEncodingUTF8, 1, 0)
	Print result

	// Convert unmappable character from UTF-8 to Windows-1252
	// \u8C4A is an escape sequence representing a Japanese character in Unicode
	// for which there is no corresponding character in Windows-1252
	
	// Demonstrate mapErrorMode = 1 (fail unmappable character)
	source = "Unmappable character causes failure: {\u8C4A}"
	// Pass 1 for options parameter to tell Igor to ignore error and let us handle it
	result = ConvertTextEncoding(source, textEncodingUTF8, textEncodingWindows1252, 1, 1)
	Variable len = strlen(result)		// Will be NaN if conversion failed
	if (NumType(len) == 2)
		Print "Conversion failed (as expected). Result is NULL."
		// You could cope with this error by trying again with the mapErrorMode
		// parameter set to 2, 3 or 4.
	else
		// We should not get here
		Print "Conversion succeeded (should not happen)."
		Print result
	endif
	
	// Demonstrate mapErrorMode = 2 (substitute for unmappable character)
	source = "Unmappable character replaced by question mark: {\u8C4A}"
	result = ConvertTextEncoding(source, textEncodingUTF8, textEncodingWindows1252, 2, 0)
	Print result		// Prints "?" in place of unmappable character
	
	// Demonstrate mapErrorMode = 3 (skip unmappable character)
	source = "Unmappable character skipped: {\u8C4A}"
	result = ConvertTextEncoding(source, textEncodingUTF8, textEncodingWindows1252, 3, 0)
	Print result		// Skips unmappable character
	
	// Demonstrate mapErrorMode = 4 (insert escape sequence for unmappable character)
	source = "Unmappable character replaced by escape sequence: {\u8C4A}"
	result = ConvertTextEncoding(source, textEncodingUTF8, textEncodingWindows1252, 4, 0)
	Print result		// Unmappable character represented as escape sequence
	
	// Demonstrate mapErrorMode = 4 (insert escape sequence for unmappable character)
	source = "Unmappable character replaced by escape sequence: {\u8C4A}"

	// First convert UTF-8 to Shift_JIS (Japanese). This will succeed.
	result = ConvertTextEncoding(source, textEncodingUTF8, textEncodingShiftJIS, 1, 0)

	// Next convert Shift_JIS (Japanese) to Windows-1252. The character cannot
	// be mapped and is replaced by an escape sequence.
	result = ConvertTextEncoding(result, textEncodingShiftJIS, textEncodingWindows1252, 4, 0)
	Print result		// Unmappable character represented as escape sequence
End

// Demo unmappable character
// In this example, the source text is valid but not representable in destination text encoding.
// Because we pass 4 for the mapErrorMode parameter, ConvertTextEncoding uses an escape sequence
// to represent the unmappable text.
Function DemoUnmappable()
	String input = "\u2135"	// Alef symbol - available in UTF-8 but not in MacRoman
	String output = ConvertTextEncoding(input, 1, 2, 4, 0)	// 1=UTF-8, 2=MacRoman
	Print output					// Prints "\u2135"
End

// Demo invalid input text
// In this example, the source text is invalid in the source text encoding.
// Because we pass 4 for the mapErrorMode parameter, ConvertTextEncoding uses an escape sequences
// to represent the invalid text.
Function DemoInvalidInput()
	String input = "\x8E"	// Represents e with acute accent in MacRoman but is not valid in UTF-8
	String output = ConvertTextEncoding(input, 1, 1, 4, 0)	// 1=UTF-8
	Print output					// Prints "\x8E"
End
```

### *See Also* {#see-also}
[Text Encodings](/igorpro/igor-basics/text-encodings.md), [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes)

[TextEncodingCode](/igorpro/commands/textencodingcode.md), [TextEncodingName](/igorpro/commands/textencodingname.md), [SetWaveTextEncoding](/igorpro/commands/setwavetextencoding.md)

[ConvertGlobalStringTextEncoding](/igorpro/commands/convertglobalstringtextencoding.md), [String Variable Text Encoding Error Example](/igorpro/igor-basics/text-encodings.md#string-variable-text-encoding-error-example)