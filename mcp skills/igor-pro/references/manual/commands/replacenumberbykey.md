---
description: "The ReplaceNumberByKey function returns kwListStr after replacing the numeric value of the keyword-value pair specified by keyStr."
slug: /commands/replacenumberbykey
---

<div className="command-signature">

## <strong>ReplaceNumberByKey</strong> (<em>keyStr</em>, <em>kwListStr</em>, <em>newNum</em> [, <em>keySepStr</em> [, <em>listSepStr</em> [, <em>case</em>]]]) {#replacenumberbykey}

</div>

The ReplaceNumberByKey function returns *kwListStr* after replacing the numeric value of the keyword-value pair specified by *keyStr*. *kwListStr* should contain keyword-value pairs such as "KEY=value1,KEY2=value2" or "Key:value1;KEY2:value2", depending on the values for *keySepStr* and *listSepStr*.

Use ReplaceNumberByKey to add or modify numeric information in a string containing a keyword-value style string list such as those returned by functions like [AxisInfo](/igorpro/commands/axisinfo.md) or [TraceInfo](/igorpro/commands/traceinfo.md).

If *keyStr* is not found in *kwListStr*, then the key and the value are appended to the end of the returned string.

*keySepStr*, *listSepStr* and *case* are optional; their defaults are ":", ";", and 0 respectively.

### *Details* {#details}
The actual string appended is:

[ *listSepStr* ] *keyStr* *keySepStr* *newNum* *listSepStr*

The optional leading list separator *listSepStr* is added only if *kwListStr* does not already end with a list separator.

*wListStr* is searched for an instance of the key string bound by *listSepStr* on the left and a *keySepStr* on the right. The text up to the next ";" is replaced by newNum after conversion to text using the %.15g format (see [printf](/igorpro/commands/printf.md) about format conversion specifications).

*kwListStr* is treated as if it ends with a *listSepStr* even if it doesn't.

Searches for *keySepStr* and *listSepStr* are always case-sensitive. Searches for *keyStr* in *kwListStr* are usually case-insensitive. Setting the optional *case* parameter to 0 makes the comparisons case sensitive.

In Igor 6, only the first byte of *keySepStr* and *listSepStr* was used. In Igor 7 and later, all bytes are used.

If *listSepStr* is specified, then *keySepStr* must also be specified. If *case* is specified, *keySepStr* and *listSepStr* must be specified.

### *Examples* {#examples}

```igor
Print ReplaceNumberByKey("K1", "K1:7;", 4)              // prints "K1:4;"
Print ReplaceNumberByKey("k2", "K2=8;", 5, "=")         // prints "K2=5;"
Print ReplaceNumberByKey("K3", "K3:9,", 6, ":", ",")    // prints "K3:6,"
Print ReplaceNumberByKey("k3", "K0:9", 6, ":", ",")     // prints "K0:9,k3:6,"
Print ReplaceNumberByKey("k3", "K3:9,", 6, ":", ",")    // prints "K3:6,"
Print ReplaceNumberByKey("k3", "K3:9,", 6, ":", ",", 1) // prints "K3:9,k3:6,"
```

### *See Also* {#see-also}
[ReplaceStringByKey](/igorpro/commands/replacestringbykey.md), [StringByKey](/igorpro/commands/stringbykey.md), [RemoveByKey](/igorpro/commands/removebykey.md), [NumberByKey](/igorpro/commands/numberbykey.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [AxisInfo](/igorpro/commands/axisinfo.md), [IgorInfo](/igorpro/commands/igorinfo.md), [SetWindow](/igorpro/commands/setwindow.md), [TraceInfo](/igorpro/commands/traceinfo.md)