---
description: "The graphemeLength function returns the number of bytes in the grapheme cluster that begins at the startByte offset in the string expression str."
slug: /commands/graphemelength
---

<div className="command-signature">

## <strong>graphemeLength</strong> (<em>str</em>, <em>startByte</em>) {#graphemelength}

</div>

The graphemeLength function returns the number of bytes in the grapheme cluster that begins at the *startByte* offset in the string expression *str*.

When *str*[*startByte*] is a normal ASCII character (byte value in the range of 0 to 127), graphemeLength returns 1.

In Unicode, a grapheme cluster is a sequence of one or more code points that together represent a single visual character, as seen by the user.

For example, the grapheme á (the letter 'a' with an acute accent) can be represented two ways in Unicode:

1) as a single UTF-8 code point U+00E1 (a precomposed á) encoded in UTF-8 as a two-byte UTF-8 character sequence of 0xC3 and 0xA1,

2) as a grapheme composed of two UTF-8 code points: a 1-byte UTF-8 character 0x61 encoding the lower-case 'a' character (which is also a normal ASCII character code) followed by a two-byte UTF-8 character sequence of 0xCC and 0x81 to encode the U+0301 COMBINING ACUTE ACCENT Unicode code point.

In the first case, graphemeLength returns 2, and in the second case it returns 3.

graphemeLength returns NaN if the *str* is NULL or if *startByte* is NaN or ±Inf.

You can use [numtype](/igorpro/commands/numtype.md) to test if the result is NaN, or use the [stringIsNull](/igorpro/commands/stringisnull.md) function on *str*.

graphemeLength returns 0 if *startByte* is < 0 or *startByte* >= strlen(*str*).

The graphemeLength function was added in Igor Pro 10.00.

### *Examples* {#examples}

```igor
Function GraphemeLengthExample1()
    String str = "😂 laugh"     // face with tears of joy emoji (4 bytes)
    Print str                   // entire string
    Print str[0] + " is wrong"  // only first byte of 4 bytes

	Print "Each grapheme individually:"
	Variable bytes = strlen(str)
	Variable startByte = 0
	do
		Variable graphemeLen = graphemeLength(str,startByte)
		String grapheme = str[startByte,startByte+graphemeLen-1]
		Print grapheme
		startByte += graphemeLen // advance to start of next grapheme (Unicode character(s))
	while (startByte < bytes)
End
```



Prints:


```igor
•GraphemeLengthExample1()
  😂 laugh
  � is wrong
  Each grapheme individually:
  😂
   
  l
  a
  u
  g
  h

Function GraphemeLengthExample2()
	String str = "日本語サポート情報の更新" 	// "Updated Japanese support information"
	Print graphemes(str, 0, 5)
	Print graphemes(str, 6, inf)
End

// Zero-based grapheme indexes. Use same index for both to get just one grapheme
Function/S graphemes(String str, Variable startGrapheme, Variable endGrapheme)
	String graphemes = ""
	Variable bytes = strlen(str)
	Variable startByte = 0, graphemeIndex = 0, graphemeLen
	for (startByte=0; startByte < bytes && graphemeIndex <= endGrapheme; startByte += graphemeLen)
		graphemeLen = graphemeLength(str, startByte)
		if (graphemeIndex >= startGrapheme) 
			String grapheme = str[startByte, startByte+graphemeLen-1]
			graphemes += grapheme
		endif
		graphemeIndex += 1
	endfor
	return graphemes
End
```

Prints:


```igor
•GraphemeLengthExample2()
  日本語サポー
  ト情報の更新
```

### *References* {#references}
[https://symbl.cc/](https://symbl.cc/)

### *See Also* {#see-also}
[strlen](/igorpro/commands/strlen.md), [UTF8CharLength](/igorpro/commands/utf8charlength.md), [String Indexing](/igorpro/programming/commands.md#string-indexing), [Unicode Escape Sequences in Strings](/igorpro/programming/commands.md#unicode-escape-sequences-in-strings), [Characters Versus Bytes](/igorpro/igor-basics/text-encodings.md#characters-versus-bytes), [Character-by-Character Operations](/igorpro/programming/programming-techniques.md#character-by-character-operations)