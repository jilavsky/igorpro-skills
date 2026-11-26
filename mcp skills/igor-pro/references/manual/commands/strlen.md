---
description: "The strlen function returns the number of bytes in the string expression str."
slug: /commands/strlen
---

<div className="command-signature">

## <strong>strlen</strong> (<em>str</em>) {#strlen}

</div>

The strlen function returns the number of bytes in the string expression *str*.

strlen returns NaN if the *str* is NULL. A local string variable or a string field in a structure that has never been set is NULL. NULL is not the same as zero length. (A global string is never NULL.) You can use [numtype](/igorpro/commands/numtype.md) to test if the result from strlen is NaN, or use the [stringIsNull](/igorpro/commands/stringisnull.md) function.

### *Examples* {#examples}

```igor
String zeroLength = ""
String neverSet
Print strlen(zeroLength), strlen(neverSet)

// Test if a string is null
Variable len = strlen(neverSet) // NaN if neverSet is null
if (numtype(len) == 2)          // strlen returned NaN?
	Print "neverSet is null"
endif
```

### *See Also* {#see-also}
[stringIsNull](/igorpro/commands/stringisnull.md), [Characters Versus Bytes](/igorpro/igor-basics/text-encodings.md#characters-versus-bytes), [Character-by-Character Operations](/igorpro/programming/programming-techniques.md#character-by-character-operations)