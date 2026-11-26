---
description: "The StringByKey function returns a substring extracted from kwListStr based on the specified key contained in keyStr."
slug: /commands/stringbykey
---

<div className="command-signature">

## <strong>StringByKey</strong> (<em>keyStr</em>, <em>kwListStr</em> [, <em>keySepStr</em> [, <em>listSepStr</em> [, <em>matchCase</em>]]]) {#stringbykey}

</div>

The StringByKey function returns a substring extracted from *kwListStr* based on the specified key contained in *keyStr*. *kwListStr* should contain keyword-value pairs such as "KEY=value1,KEY2=value2" or "Key:value1;KEY2:value2", depending on the values for *keySepStr* and *listSepStr*.

Use StringByKey to extract a string value from a string containing a "key1=value1,key2=value2," style list such as those returned by functions like [AxisInfo](/igorpro/commands/axisinfo.md) or [TraceInfo](/igorpro/commands/traceinfo.md).

If the key is not found or if any of the arguments is "" then a zero length string is returned.

*keySepStr*, *listSepStr* and *matchCase* are optional; their defaults are ":", ";", and 0 respectively.

### *Details* {#details}
*kwListStr* is searched for an instance of the key string bound by *listSepStr* on the left and a *keySepStr* on the right. The text up to the next *listSepStr* is returned.

*kwListStr* is treated as if it ends with a *listSepStr* even if it doesn't.

Searches for *keySepStr* and *listSepStr* are always case-sensitive. Searches for *keyStr* in *kwListStr* are usually case-insensitive. Setting the optional *matchCase* parameter to 1 makes the comparisons case sensitive.

In Igor 6, only the first byte of *keySepStr* and *listSepStr* was used. In Igor 7 and later, all bytes are used.

If *listSepStr* is specified, then *keySepStr* must also be specified.  If *matchCase* is specified, *keySepStr* and *listSepStr* must be specified.

### *Examples* {#examples}

```igor
Print StringByKey("BKEY", "AKEY:hello;BKEY:nok-nok")    // prints "nok-nok"
Print StringByKey("KY", "KX=1;ky=hello", "=")           // prints "hello"
Print StringByKey("KY", "KX:1,KY:joey,", ":", ",")      // prints "joey"
Print StringByKey("kz", "KZ:1st,kz:2nd,", ":", ",")     // prints "1st"
Print StringByKey("kz", "KZ:1st,kz:2nd,", ":", ",", 1)  // prints "2nd"
```

### *See Also* {#see-also}
[NumberByKey](/igorpro/commands/numberbykey.md), [RemoveByKey](/igorpro/commands/removebykey.md), [ReplaceNumberByKey](/igorpro/commands/replacenumberbykey.md), [ReplaceStringByKey](/igorpro/commands/replacestringbykey.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [AxisInfo](/igorpro/commands/axisinfo.md), [IgorInfo](/igorpro/commands/igorinfo.md), [SetWindow](/igorpro/commands/setwindow.md), [TraceInfo](/igorpro/commands/traceinfo.md)