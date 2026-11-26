---
description: "The GrepString function tests string for a match to the regular expression regExprStr. Returns 1 to indicate a match, or 0 for no match."
slug: /commands/grepstring
---

<div className="command-signature">

## <strong>GrepString</strong> (<em>string</em>, <em>regExprStr</em>) {#grepstring}

</div>

The GrepString function tests *string* for a match to the regular expression *regExprStr* . Returns 1 to indicate a match, or 0 for no match.

### *Details* {#details}
*regExprStr* is a regular expression such as is used by the UNIX grep(1) command. It is much more powerful than the wildcard syntax used for [stringmatch](/igorpro/commands/stringmatch.md). See [Regular Expressions](/igorpro/programming/programming-techniques.md#regular-expressions) for *regExprStr* details.

Character matching is case-sensitive by default, similar to [strsearch](/igorpro/commands/strsearch.md). Prepend the Perl 5 modifier "(?i)" to match upper and lower-case text.

### *Examples* {#examples}
Test for truth that the string contains at least one digit:


```igor
if( GrepString(str,"[0-9]+") )
```

Test for truth that the string contains at least one "abc", "Abc", "ABC", etc:


```igor
if( GrepString(str,"(?i)abc") )	// case-insensitive test
```

### *See Also* {#see-also}
[stringmatch](/igorpro/commands/stringmatch.md), [cmpstr](/igorpro/commands/cmpstr.md), [strsearch](/igorpro/commands/strsearch.md), [SplitString](/igorpro/commands/splitstring.md), [sscanf](/igorpro/commands/sscanf.md), [ListMatch](/igorpro/commands/listmatch.md), [ReplaceString](/igorpro/commands/replacestring.md)