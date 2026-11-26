---
description: "The UTF8CharLength function returns the number of bytes in the UTF-8 character (\"code point\") that begins at the startByte offset in the string expression str."
slug: /commands/utf8charlength
---

<div className="command-signature">

## <strong>UTF8CharLength</strong> (<em>str</em>, <em>startByte</em>) {#utf8charlength}

</div>

The UTF8CharLength function returns the number of bytes in the UTF-8 character ("code point") that begins at the *startByte* offset in the string expression *str*.

When *str*[*startByte*] is a normal ASCII character (byte value in the range of 0 to 127), UTF8CharLength returns 1.

In Unicode, a grapheme cluster is a sequence of one or more code points that together represent a single visual character, as seen by the user. Code points (or "UTF-8 characters") are encoded in UTF-8 as one, two, three, or four bytes.

For example, the grapheme á (the letter 'a' with an acute accent) can be represented two ways in Unicode:

1) as a single Unicode code point U+00E1 (a precomposed á) encoded in UTF-8 as a two-byte UTF-8 character sequence of 0xC3 and 0xA1,

2) as a grapheme composed of two UTF-8 code points: a 1-byte UTF-8 character 0x61 encoding the lower-case 'a' character (which is also a normal ASCII character code) followed by a two-byte UTF-8 character sequence of 0xCC and 0x81 to encode the U+0301 COMBINING ACUTE ACCENT Unicode code point.

In the first case, UTF8CharLength returns 2, and in the second case it returns 1.

UTF8CharLength returns NaN if the *str* is NULL or if *startByte* is NaN or ±Inf.

You can use [numtype](/igorpro/commands/numtype.md) to test if the result is NaN, or use the [stringIsNull](/igorpro/commands/stringisnull.md) function on *str*.

UTF8CharLength returns 0 if *startByte* is < 0 or *startByte* >= strlen(*str*).

The UTF8CharLength function was added in Igor Pro 10.00. It is the equivalent of the NumBytesInUTF8Character user function described in [Character-by-Character Operations](/igorpro/programming/programming-techniques.md#character-by-character-operations).

### *Example* {#example}

```igor
// print the string and break it down to the graphemes and UTF-8 code points
Function ExamineUTF8Text(String str)
	
	Variable totalBytes = strlen(str)
	Printf "Entire string = \"%s\", total bytes = %d\r",str,totalBytes

	Print "UTF8 code points and graphemes individually"
	Variable startByte = 0
	do
		Variable graphemeLen = graphemeLength(str,startByte)
		String grapheme = str[startByte,startByte+graphemeLen-1]
		Printf "startByte=%d, %d bytes in grapheme, grapheme=\"%s\"\r", startByte, graphemeLen, grapheme

		// enumerate the code points.
		Variable codePointStart = startByte
		Variable codePointBytes = 0
		Variable codePointNum = 1 // first code point

		// The first code point is known to be <= graphemeLen. It may be ==.
		do
			Variable codepointLen = UTF8CharLength(str,codePointStart)
			String character = str[codePointStart,codePointStart+codepointLen-1]

			// print each byte in the code point/character
			String chars=""
			Variable c
			for (c=0; c<codepointLen; c+=1)
				Variable byteVal = char2num(character[c]) & 0x00FF
				sprintf chars, "%s 0x%X", chars, byteVal
			endfor 
			Printf "\t\tcodepoint=%d, startByte=%d, UTF8CharLength = %d bytes = %s\r", codePointNum, codePointStart, codepointLen, chars	
			
			codePointNum += 1
			codePointStart += codepointLen // advance
			codePointBytes += codepointLen
		while (codePointBytes < graphemeLen )
		
		startByte += graphemeLen // advance to start of next grapheme
	while (startByte < totalBytes)
	Print ""
End
```




```igor
•ExamineUTF8Text("a\xCC\x81 ♣ Δ") // á is the letter "a" combined with an acute accent U+0301
  Entire string = "á ♣ Δ", total bytes = 10
  UTF8 code points and graphemes individually
  startByte=0, 3 bytes in grapheme, grapheme="á"
               codepoint=1, startByte=0, UTF8CharLength = 1 bytes =  0x61
               codepoint=2, startByte=1, UTF8CharLength = 2 bytes =  0xCC 0x81
  startByte=3, 1 bytes in grapheme, grapheme=" "
               codepoint=1, startByte=3, UTF8CharLength = 1 bytes =  0x20
  startByte=4, 3 bytes in grapheme, grapheme="♣"
               codepoint=1, startByte=4, UTF8CharLength = 3 bytes =  0xE2 0x99 0xA3
  startByte=7, 1 bytes in grapheme, grapheme=" "
               codepoint=1, startByte=7, UTF8CharLength = 1 bytes =  0x20
  startByte=8, 2 bytes in grapheme, grapheme="Δ"
               codepoint=1, startByte=8, UTF8CharLength = 2 bytes =  0xCE 0x94
```

### *References* {#references}
[https://symbl.cc/](https://symbl.cc/)

### *See Also* {#see-also}
[strlen](/igorpro/commands/strlen.md), [graphemeLength](/igorpro/commands/graphemelength.md), [String Indexing](/igorpro/programming/commands.md#string-indexing), [Unicode Escape Sequences in Strings](/igorpro/programming/commands.md#unicode-escape-sequences-in-strings), [Characters Versus Bytes](/igorpro/igor-basics/text-encodings.md#characters-versus-bytes), [Character-by-Character Operations](/igorpro/programming/programming-techniques.md#character-by-character-operations)