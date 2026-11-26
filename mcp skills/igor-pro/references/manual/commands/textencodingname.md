---
description: "The TextEncodingName function returns one or more text encoding names corresponding to the specified text encoding code."
slug: /commands/textencodingname
---

<div className="command-signature">

## <strong>TextEncodingName</strong> (<em>textEncoding</em>, <em>index</em>) {#textencodingname}

</div>

The TextEncodingName function returns one or more text encoding names corresponding to the specified text encoding code. The result is returned as a string value.

If *textEncoding* is not a valid Igor text encoding code or if *index* is out of range, TextEncodingName returns "Unknown".

This function is mainly useful for providing a human-readable string corresponding to a given text encoding code for display purposes. You might use it to generate some Internet-compatible text, such as an HTML page, if you need a string to specify the charset.

The TextEncodingName function was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*textEncoding* is an Igor text encoding code as listed under [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes).

*index* specifies which text encoding name you want. A given text encoding can be identified by more than one name. Normally you will pass 0 to get the first text encoding name for the specified text encoding code. This is the preferred text encoding name. You can pass 1 for the second name, if any, 2 for the third, if any, and so on. You can pass -1 to get a semicolon-separated list of all text encoding names for the specified text encoding.

### *Details* {#details}
Internally Igor has a table of text encoding codes and the corresponding text encoding names. For a given code there may be more than one acceptable name. For example, for the code 2 (MacRoman), the names "macintosh", "MacRoman" and "x-macroman" are accepted, with "macintosh" being preferred. The TextEncodingName function returns a text encoding name from the internal table.

The preferred name is usually the name recognized by the Internet Assigned Numbers Authority (IANA) as listed at [http://www.iana.org/assignments/character-sets](http://www.iana.org/assignments/character-sets).

### *Examples* {#examples}

```igor
// Get the preferred name for the MacRoman text encoding (2)
String firstName = TextEncodingName(2, 0); Print firstName

// Get the second name for the MacRoman text encoding (2)
String secondName = TextEncodingName(2, 1); Print secondName

// Get a semicolon-separated list of all text encoding names for MacRoman
String names = TextEncodingName(2, -1); Print names
```

### *See Also* {#see-also}
[Text Encodings](/igorpro/igor-basics/text-encodings.md), [Text Encoding Names and Codes](/igorpro/igor-basics/text-encodings.md#text-encoding-names-and-codes), [TextEncodingCode](/igorpro/commands/textencodingcode.md)