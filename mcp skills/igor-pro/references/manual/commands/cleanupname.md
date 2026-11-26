---
description: "The CleanupName function returns the input name string, possibly altered to make it a legal object name."
slug: /commands/cleanupname
---

<div className="command-signature">

## <strong>CleanupName</strong> (<em>nameStr</em>, <em>beLiberal</em> [, <em>maxBytes</em> ]) {#cleanupname}

</div>

The CleanupName function returns the input name string, possibly altered to make it a legal object name.

The *maxBytes* parameter requires Igor Pro 8.00 or later.

In Igor Pro 9.00 or later, you can use the [CreateDataObjectName](/igorpro/commands/createdataobjectname.md) function as a replacement for some combination of CheckName, CleanupName, and UniqueName to create names of waves, global variables, and data folders.

### *Parameters* {#parameters}
*nameStr* must contain an unquoted (i.e., no single quotes for liberal names) name, such as you might receive from the user through a dialog or control panel.

*beLiberal* is 0 to use strict name rules or 1 to use liberal name rules. Strict rules allow only letters, digits and the underscore character. Liberal rules allow other characters such as spaces and dots. Liberal names are allowed for names of waves and data folders only.

*maxBytes* is the maximum number of bytes allowed in the result. This parameter requires Igor Pro 8.00 or later. *maxBytes* is optional, defaults to 255, and is clipped to the range 1..255. The returned value will never be longer than *maxBytes* but may be shorter.

Prior to Igor Pro 8.00, Igor names were limited to 31 bytes so CleanupName never returned names longer than 31 bytes. In Igor Pro 8.00 or later, names for most types of objects may be up to 255 bytes so CleanupName may return very long names. You may want to use the *maxBytes* parameter to prevent the use of inconveniently-long names.

If *nameStr* includes non-ASCII characters, which in UTF-8 consist of multiple bytes, CleanupName clips the name at a character boundary if clipping is required.

### *Details* {#details}
A cleaned up name is not necessarily unique. Call CheckName to check for uniqueness or UniqueName to ensure uniqueness.

Prior to Igor 8, all object names were limited to 31 bytes. Now, for most types of objects, names can be up to 255 bytes. CleanupName always allows up to 255 bytes. Global picture names and notebook ruler names are still limited to 31 bytes so, if you are cleaning up those names, you must test for long names yourself. See [Long Object Names](/igorpro/igor-basics/using-igor.md#long-object-names) for details.

If a cleaned up name is liberal, you may need to quote it. See [Programming With Liberal Names](/igorpro/programming/programming-techniques.md#programming-with-liberal-names) for details.

### *Examples* {#examples}

```igor
String cleanStrVarName = CleanupName(proposedStrVarName, 0)

// In UTF-8, the "±" character consists of two bytes: 0xC2 and 0XB1
Print CleanupName("±", 1, 1)	// maxBytes=1; returns "X"
Print CleanupName("±", 1, 2)	// maxBytes=2; returns "±" (2 bytes)
```

### *See Also* {#see-also}
[Object Names](/igorpro/igor-basics/using-igor.md#object-names), [Programming With Liberal Names](/igorpro/programming/programming-techniques.md#programming-with-liberal-names), [CreateDataObjectName](/igorpro/commands/createdataobjectname.md), [CheckName](/igorpro/commands/checkname.md), [UniqueName](/igorpro/commands/uniquename.md)