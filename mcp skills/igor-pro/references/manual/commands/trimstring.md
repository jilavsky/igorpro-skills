---
description: "The TrimString function returns a string identical to str except that leading and trailing whitespace characters are removed."
slug: /commands/trimstring
---

<div className="command-signature">

## <strong>TrimString</strong> (<em>str</em> [, <em>simplifyInternalSpaces</em>]) {#trimstring}

</div>

The TrimString function returns a string identical to *str* except that leading and trailing whitespace characters are removed. The whitespace characters are space, tab, carriage-return and linefeed.

If the optional second parameter is non-zero, then each run of whitespace characters between words in *str* is "simplified" to a single space character.

The TrimString function was added in Igor Pro 7.00.

### *Examples* {#examples}

```igor
Print TrimString("   spaces   at  ends  ")      // Prints "spaces   at  ends"
Print TrimString("   spaces   at  ends  ", 1)   // Prints "spaces at ends"
```

### *See Also* {#see-also}
[SplitString](/igorpro/commands/splitstring.md), [RemoveEnding](/igorpro/commands/removeending.md), [ReplaceString](/igorpro/commands/replacestring.md)