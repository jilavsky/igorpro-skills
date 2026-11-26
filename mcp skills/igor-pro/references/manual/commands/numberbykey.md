---
description: "The NumberByKey function returns a numeric value extracted from kwListStr based on the specified key contained in keyStr."
slug: /commands/numberbykey
---

<div className="command-signature">

## <strong>NumberByKey</strong> (<em>keyStr</em>, <em>kwListStr</em> [, <em>keySepStr</em> [, <em>listSepStr</em> [, <em>matchCase</em> ]]]) {#numberbykey}

</div>

The NumberByKey function returns a numeric value extracted from *kwListStr* based on the specified key contained in *keyStr*. *kwListStr* should contain keyword-value pairs such as "KEY=value1,KEY2=value2" or "Key:value1;KEY2:value2", depending on the values for *keySepStr* and *listSepStr*.

Use NumberByKey to extract a numeric value from a string containing a "key1=value1;key2=value2;" style list such as those returned by functions like [AxisInfo](/igorpro/commands/axisinfo.md) or [TraceInfo](/igorpro/commands/traceinfo.md).

If the key is not found or if any of the arguments  is "" or if the conversion to a number fails then NaN is returned.

*keySepStr*, *listSepStr* and *matchCase* are optional; their defaults are ":", ";", and 0 respectively.

### *Details* {#details}
*kwListStr* is searched for an instance of the key string bound by *listSepStr* on the left and a *keySepStr* on the right. The text up to the next *listSepStr* is converted to the returned number.

*kwListStr* is treated as if it ends with a *listSepStr* even if it doesn't.

Searches for *keySepStr* and *listSepStr* are always case-sensitive. Searches for *keyStr* in *kwListStr* are usually case-insensitive. Setting the optional *matchCase* parameter to 1 makes the comparisons case sensitive.

In Igor 6, only the first byte of *keySepStr* and *listSepStr* was used. In Igor 7 and later, all bytes are used.

If *listSepStr* is specified, then *keySepStr* must also be specified.  If *matchCase* is specified, *keySepStr* and *listSepStr* must be specified.

### *Examples* {#examples}

```igor
Print NumberByKey("AKEY", "AKEY:123;")                          // prints 123
Print NumberByKey("BKEY", "AKEY=123;Bkey=456;", "=")            // prints 456
Print NumberByKey("KEY2", "KEY1=123,KEY2=999,", "=", ",")       // prints 999
Print NumberByKey("ckey", "CKEY=123;ckey=456;", "=")            // prints 123
Print NumberByKey("ckey", "CKEY=123;ckey=456;", "=", ";", 1)    // prints 456
```

### *See Also* {#see-also}
[StringByKey](/igorpro/commands/stringbykey.md), [RemoveByKey](/igorpro/commands/removebykey.md), [ReplaceNumberByKey](/igorpro/commands/replacenumberbykey.md), [ReplaceStringByKey](/igorpro/commands/replacestringbykey.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [AxisInfo](/igorpro/commands/axisinfo.md), [IgorInfo](/igorpro/commands/igorinfo.md), [SetWindow](/igorpro/commands/setwindow.md), [TraceInfo](/igorpro/commands/traceinfo.md)