---
description: "The stringIsNull function returns the truth that the string str is null (undefined)."
slug: /commands/stringisnull
---

<div className="command-signature">

## <strong>stringIsNull</strong> (<em>str</em>) {#stringisnull}

</div>

The stringIsNull function returns the truth that the string *str* is null (undefined).

stringIsNull returns 1 if the *str* is NULL, or 0 if it is not NULL.

A local string variable or a string field in a structure that has never been set is NULL. NULL is not the same as a string of zero length. A global string is never NULL.

stringIsNull was added in Igor 10.

### *Example* {#example}

```igor
Function test()
	String zeroLength = ""
	String neverSet
	Print stringIsNull(zeroLength), stringIsNull(neverSet)  // 0, 1
	Print strlen(zeroLength), strlen(neverSet)              // 0, NaN
	String/G globalStr
	SVAR gStr = globalStr
	Print stringIsNull(gStr), strlen(gStr)                  // 0, 0
End
```

### *See Also* {#see-also}
[strlen](/igorpro/commands/strlen.md)