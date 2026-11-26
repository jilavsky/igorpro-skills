---
description: "The ReplicateString function returns a string containing str repeated totalNumCopies times."
slug: /commands/replicatestring
---

<div className="command-signature">

## <strong>ReplicateString</strong> (<em>str</em>, <em>totalNumCopies</em>) {#replicatestring}

</div>

The ReplicateString function returns a string containing *str* repeated *totalNumCopies* times.

The ReplicateString function was added in Igor Pro 9.00.

### *Example* {#example}

```igor
String in = "αßγ"
String out = ReplicateString(in, 3)	// Returns "αßγαßγαßγ"
```

### *See Also* {#see-also}
[PadString](/igorpro/commands/padstring.md), [ReplaceString](/igorpro/commands/replacestring.md)