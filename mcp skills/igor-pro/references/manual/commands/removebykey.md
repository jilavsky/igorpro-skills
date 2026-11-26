---
description: "The RemoveByKey function returns kwListStr after removing the keyword-value pair specified by keyStr."
slug: /commands/removebykey
---

<div className="command-signature">

## <strong>RemoveByKey</strong> (<em>keyStr</em>, <em>kwListStr</em>  [, <em>keySepStr</em>  [, <em>listSepStr</em> [, <em>matchCase</em> ]]]) {#removebykey}

</div>

The RemoveByKey function returns *kwListStr* after removing the keyword-value pair specified by *keyStr*. *kwListStr* should contain keyword-value pairs such as "KEY=value1,KEY2=value2" or "Key:value1;KEY2:value2", depending on the values for *keySepStr* and *listSepStr*.

Use RemoveByKey to remove information from a string containing a "key1:value1;key2:value2;" or "key1=value1,key2=value2," style list such as those returned by functions like [AxisInfo](/igorpro/commands/axisinfo.md) or [TraceInfo](/igorpro/commands/traceinfo.md).

If *keyStr* is not found or if any of the arguments  is "" then *kwListStr* is returned unchanged.

*keySepStr*, *listSepStr* and *matchCase* are optional; their defaults are ":", ";", and 0 respectively.

### *Details* {#details}
*kwListStr* is searched for an instance of the key string bound by *listSepStr* on the left and a *keySepStr* on the right. The key, the *keySepStr*, and the text up to and including the next *listSepStr* (if any) are removed from the returned string.

If the resulting string contains only *listSepStr* characters, then an empty string ("") is returned.

*kwListStr* is treated as if it ends with a *listSepStr* even if it doesn't.

Searches for *keySepStr* and *listSepStr* are always case-sensitive. Searches for *keyStr* in *kwListStr* are usually case-insensitive. Setting the optional *matchCase* parameter to 1 makes the comparisons case sensitive.

In Igor 6, only the first byte of *keySepStr* and *listSepStr* was used. In Igor 7 and later, all bytes are used.

If *listSepStr* is specified, then *keySepStr* must also be specified. If *matchCase* is specified, *keySepStr* and *listSepStr* must be specified.

### *Examples* {#examples}

```igor
Print RemoveByKey("AKEY", "AKEY:123;BKEY:val")      // prints "BKEY:val"
Print RemoveByKey("AKEY", "akey=1;BK=b;", "=")      // prints "BK=b;"
Print RemoveByKey("AKEY", "AKEY=1,BK=b,", "=", ",") // prints "BK=b,"
Print RemoveByKey("ckey","CKEY:1;BKEY:2")           // prints "BKEY:2"
Print RemoveByKey("ckey","CKEY:1;BKEY:2",":",";",1) // prints "CKEY:1;BKEY:2"
```

### *See Also* {#see-also}
[NumberByKey](/igorpro/commands/numberbykey.md), [StringByKey](/igorpro/commands/stringbykey.md), [ReplaceNumberByKey](/igorpro/commands/replacenumberbykey.md), [ReplaceStringByKey](/igorpro/commands/replacestringbykey.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [AxisInfo](/igorpro/commands/axisinfo.md), [IgorInfo](/igorpro/commands/igorinfo.md), [SetWindow](/igorpro/commands/setwindow.md), [TraceInfo](/igorpro/commands/traceinfo.md)