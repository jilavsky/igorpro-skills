---
description: "The ReplaceString function returns inStr after replacing any instance of replaceThisStr with withThisStr."
slug: /commands/replacestring
---

<div className="command-signature">

## <strong>ReplaceString</strong> (<em>replaceThisStr</em>, <em>inStr</em>, <em>withThisStr</em> [, <em>caseSense</em> [, <em>maxReplace</em>]]) {#replacestring}

</div>

The ReplaceString function returns *inStr* after replacing any instance of *replaceThisStr* with *withThisStr*.

The comparison of *replaceThisStr* to the contents of *inStr* is case-insensitive. Setting the optional *caseSense* parameter to nonzero makes the comparison case-sensitive.

Usually all instances of *replaceThisStr* are replaced. Setting the optional *maxReplace* parameter limits the replacements to that number.

### *Details* {#details}
If *replaceThisStr* is not found, *inStr* is returned unchanged.

If *maxReplace* is less than 1, then no replacements are made. Setting *maxReplace* = [Inf](/igorpro/commands/inf.md) is the same as omitting it.

### *Examples* {#examples}

```igor
Print ReplaceString("hello", "say hello", "goodbye")    // prints "say goodbye"
Print ReplaceString("\r\n", "line1\r\nline2", "")       // prints "line1line2"
Print ReplaceString("A", "an Ack-Ack", "a", 1)          // prints "an ack-ack"
Print ReplaceString("A", "an Ack-Ack", "a", 1, 1)       // prints "an ack-Ack"
Print ReplaceString("", "input", "whatever")            // prints "input" (no change)
```

### *See Also* {#see-also}
[ReplaceStringByKey](/igorpro/commands/replacestringbykey.md), [CmpStr](/igorpro/commands/cmpstr.md), [StringMatch](/igorpro/commands/stringmatch.md), [StrSearch](/igorpro/commands/strsearch.md), [TrimString](/igorpro/commands/trimstring.md), [ReplicateString](/igorpro/commands/replicatestring.md)