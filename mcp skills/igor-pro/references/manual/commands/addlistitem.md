---
description: "The AddListItem function returns listStr after adding itemStr to it. listStr should contain items separated by listSepStr which typically is \";\"."
slug: /commands/addlistitem
---

<div className="command-signature">

## <strong>AddListItem</strong> (<em>itemStr</em>, <em>listStr</em>  [, <em>listSepStr</em>  [, <em>itemNum</em> ]]) {#addlistitem}

</div>

The AddListItem function returns *listStr* after adding *itemStr* to it. *listStr* should contain items separated by *listSepStr* which typically is ";".

Use AddListItem to add an item to a string containing a list of items separated by a string (usually a single ASCII character), such as those returned by functions like [TraceNameList](/igorpro/commands/tracenamelist.md) or [AnnotationList](/igorpro/commands/annotationlist.md), or to a line from a delimited text file.

*listSepStr* and *itemNum* are optional; their defaults are ";" and 0, respectively.

### *Details* {#details}
By default *itemStr* is added to the start of the list. Use the optional list index *itemNum* to add *itemStr* at a different location. The returned list will have *itemStr* at the index *itemNum* or at [ItemsInList](/igorpro/commands/itemsinlist.md)(*returnedListStr*)-1 when *itemNum* equals or exceeds ItemsInList(*listStr*).

*itemNum* can be any value from -infinity to infinity. Values from -infinity to 0 prepend *itemStr* to the list, and values from ItemsInList(*listStr*) to infinity append *itemStr* to the list.

*itemStr* may be "", in which case an empty item (consisting of only a separator) is added.

If *listSepStr* is "" then *listStr* is returned unchanged (unless *listStr* contains only list separators, in which case an empty string ("") is returned).

*listStr* is treated as if it ends with a *listSepStr* even if it doesn't.

In Igor 6, only the first byte of *listSepStr* was used. In Igor 7 and later, all bytes are used.

### *Examples* {#examples}

```igor
Print AddListItem("hello","kitty;cat;")     // prints "hello;kitty;cat;"
Print AddListItem("z", "b,c,", ",", 1)      // prints "b,z,c,"
Print AddListItem("z", "b,c,", ",", 999)    // prints "b,c,z,"
Print AddListItem("z", "b,c,", ",", Inf)    // prints "b,c,z,"
Print AddListItem("", "b-c-", "-")          // prints "-b-c-"
```

### *See Also* {#see-also}
[RemoveListItem](/igorpro/commands/removelistitem.md), [RemoveFromList](/igorpro/commands/removefromlist.md), [StringFromList](/igorpro/commands/stringfromlist.md), [FindListItem](/igorpro/commands/findlistitem.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [RemoveByKey](/igorpro/commands/removebykey.md), [WaveList](/igorpro/commands/wavelist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [StringList](/igorpro/commands/stringlist.md), [VariableList](/igorpro/commands/variablelist.md), [FunctionList](/igorpro/commands/functionlist.md)