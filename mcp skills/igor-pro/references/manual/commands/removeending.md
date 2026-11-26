---
description: "The RemoveEnding function returns str with endingStr removed from the end. If you omit endingStr, it returns str with one grapheme removed from the end."
slug: /commands/removeending
---

<div className="command-signature">

## <strong>RemoveEnding</strong> (<em>str</em> [, <em>endingStr</em>]) {#removeending}

</div>

The RemoveEnding function returns *str* with *endingStr* removed from the end. If you omit *endingStr*, it returns *str* with one grapheme removed from the end.

### *Details* {#details}
If you specify *endingStr*, RemoveEnding compares it to the end of str using case-insensitive comparison. If there is a match, RemoveEnding returns the contents of *str* up to *endingStr*. If there is no match, RemoveEnding returns the entirety of *str*.

If you omit *endingStr*, RemoveEnding returns *str* with the last grapheme removed. A grapheme is whatever visually appears to be one character even if it consists of more than one character. In "ABC", the last grapheme is "C" which is also the last character. In "ABÇ", "Ç" consists of two characters: a C character and a "combining cedilla" character; RemoveEnding removes "Ç" which is the last grapheme.

### *Examples* {#examples}

```igor
Print RemoveEnding("123")                   // Prints "12"
Print RemoveEnding("ABÇ")                   // Prints "AB"
Print RemoveEnding("no semi" , ";")         // Prints "no semi"
Print RemoveEnding("trailing semi;" , ";")  // Prints "trailing semi"
Print RemoveEnding("file.txt" , ".TXT")     // Prints "file"
```

### *See Also* {#see-also}
[ParseFilePath](/igorpro/commands/parsefilepath.md), [CmpStr](/igorpro/commands/cmpstr.md)