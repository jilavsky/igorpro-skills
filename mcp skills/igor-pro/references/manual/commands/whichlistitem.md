---
description: "The WhichListItem function returns the index of the first item of listStr that matches itemStr."
slug: /commands/whichlistitem
---

<div className="command-signature">

## <strong>WhichListItem</strong> (<em>itemStr</em>, <em>listStr</em> [, <em>listSepStr</em> [, <em>startIndex</em> [, <em>matchCase</em>]]]) {#whichlistitem}

</div>

The WhichListItem function returns the index of the first item of *listStr* that matches *itemStr. listStr* should contain items separated by *listSepStr* which typically is ";". If the item is not found in the list, -1 is returned.

Use WhichListItem to locate an item in a string containing a list of items separated by a string (usually a single ASCII character), such as those returned by functions like [TraceNameList](/igorpro/commands/tracenamelist.md) or [AnnotationList](/igorpro/commands/annotationlist.md), or a line from a delimited text file.

*listSepStr*, *startIndex*,  and *matchCase* are optional; their defaults are ";", 0, and 1 respectively.

### *Details* {#details}
WhichListItem differs from [FindListItem](/igorpro/commands/findlistitem.md) in that WhichListItem returns a list index, while FindListItem returns a character offset into a string.

*listStr* is searched for *itemStr* bound by *listSepStr* on the left and right.

*listStr* is treated as if it ends with a *listSepStr* even if it doesn't.

Searches for *listSepStr* are always case-sensitive. The comparison of *itemStr* to the contents of *listStr* is usually case-sensitive. Setting the optional *matchCase* parameter to 0 makes the comparison case insensitive.

If *itemStr* is not found,  if *listStr* is "",  or if *startIndex* is not within the range of 0 to ItemsInList(*listStr* )-1, then -1 is returned.

In Igor 6, only the first byte of *listSepStr* was used. In Igor 7 and later, all bytes are used.

An item can be empty. The lists "abc;def;;ghi" and ";abc;def;;ghi;" have four items (the third item is ""). Use WhichListItem("", *listStr* ) to find the first empty item.

If *startIndex* is specified, then *listSepStr* must also be specified. If *matchCase* is specified, *startIndex* and *listSepStr* must be specified.

### *Examples* {#examples}

```igor
Print WhichListItem("wave0", "wave0;wave1;")    // prints 0
Print WhichListItem("c", "a;b;")                // prints -1
Print WhichListItem("", "a;;b;")                // prints 1
Print WhichListItem("c", "a,b,c,x,c", ",")      // prints 2
Print WhichListItem("c", "a,b,c,x,c", ",", 3)   // prints 4
Print WhichListItem("C", "x;c;C;")              // prints 2
Print WhichListItem("C", "x;c;C;", ";", 0, 0)   // prints 1
```

### *See Also* {#see-also}
[StringFromList](/igorpro/commands/stringfromlist.md), [FindListItem](/igorpro/commands/findlistitem.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [AddListItem](/igorpro/commands/addlistitem.md), [RemoveListItem](/igorpro/commands/removelistitem.md), [RemoveFromList](/igorpro/commands/removefromlist.md), [WaveList](/igorpro/commands/wavelist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [StringList](/igorpro/commands/stringlist.md), [VariableList](/igorpro/commands/variablelist.md), [FunctionList](/igorpro/commands/functionlist.md)