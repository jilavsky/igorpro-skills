---
description: "The ItemsInList function returns the number of items in listStr. listStr should contain items separated by listSepStr which typically is \";\"."
slug: /commands/itemsinlist
---

<div className="command-signature">

## <strong>ItemsInList</strong> (<em>listStr</em> [, <em>listSepStr</em>]) {#itemsinlist}

</div>

The ItemsInList function returns the number of items in *listStr.* *listStr* should contain items separated by *listSepStr* which typically is ";".

Use ItemsInList to count the number of items in a string containing a list of items separated by a string (usually a single ASCII character), such as those returned by functions like [TraceNameList](/igorpro/commands/tracenamelist.md) or [AnnotationList](/igorpro/commands/annotationlist.md), or a line from a delimited text file.

If *listStr* is "" then 0  is returned.

*listSepStr* is optional. If missing, *listSepStr* defaults to ";" .

### *Details* {#details}
*listStr* is searched for item strings bound by *listSepStr* on the left and right.

An item can be empty. In "abc;def;;ghi", the third item, whose zero-based index is 2, is empty. In ";def;;ghi;", the first and third items, whose zero-based indices are 0 and 2, are empty.

*listStr* is treated as if it ends with a *listSepStr* even if it doesn't. The search is case-sensitive.

In Igor 6, only the first byte of *listSepStr* was used. In Igor 7 and later, all bytes are used.

### *Examples* {#examples}

```igor
Print ItemsInList("wave0;wave1;wave1#1;")       // prints 3
3

Print ItemsInList("key1=val1,key2=val2", ",")   // prints 2
Print ItemsInList("1 \t 2 \t", "\t")            // prints 2
Print ItemsInList(";")                          // prints 1
Print ItemsInList(";;")                         // prints 2
Print ItemsInList(";a;")                        // prints 2
Print ItemsInList(";;;")                        // prints 3
```

### *See Also* {#see-also}
[AddListItem](/igorpro/commands/addlistitem.md), [StringFromList](/igorpro/commands/stringfromlist.md), [FindListItem](/igorpro/commands/findlistitem.md), [RemoveListItem](/igorpro/commands/removelistitem.md), [RemoveFromList](/igorpro/commands/removefromlist.md), [WaveList](/igorpro/commands/wavelist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [StringList](/igorpro/commands/stringlist.md), [VariableList](/igorpro/commands/variablelist.md), [FunctionList](/igorpro/commands/functionlist.md)