---
description: "The RemoveListItem function returns listStr after removing the item specified by the list index index."
slug: /commands/removelistitem
---

<div className="command-signature">

## <strong>RemoveListItem</strong> (<em>index</em>, <em>listStr</em> [, <em>listSepStr</em> [, <em>offset</em>]]) {#removelistitem}

</div>

The RemoveListItem function returns *listStr* after removing the item specified by the list index *index*.

Use RemoveListItem to remove an item from a string containing a list of items separated by a separator, such as strings returned by functions like [TraceNameList](/igorpro/commands/tracenamelist.md) and [AnnotationList](/igorpro/commands/annotationlist.md).

### *Parameters* {#parameters}
*index* is the zero-based index of the list item that you want to remove.

*listStr* contains a series of text items separated by *listSepStr* . The trailing separator is optional though recommended.

*listSepStr* is optional. If omitted it defaults to ";". Prior to Igor Pro 7.00, only the first byte of *listSepStr* was used. Now all bytes are used.

*offset* is optional and requires Igor Pro 7.00 or later. If omitted it defaults to 0. The search begins *offset* bytes into *listStr*. When iterating through lists containing large numbers of items, using the *offset* parameter provides dramatically faster execution. For an example using the *offset* parameter, see [StringFromList](/igorpro/commands/stringfromlist.md).

### *Details* {#details}
RemoveListItem differs from [RemoveFromList](/igorpro/commands/removefromlist.md) in that it specifies the item to be removed by index and removes only that item, while RemoveFromList specifies the item to be removed by value, and removes all items that match it.

If *index* less than 0 or greater than  ItemsInList(*listStr*) - 1, or if *listSepStr* is "" then *listStr* is returned unchanged (unless *listStr* contains only list separators, in which case an empty string ("") is returned).

If the resulting string contains only *listSepStr* characters, then an empty string ("") is returned.

### *Examples* {#examples}

```igor
Print RemoveListItem(1, "wave0;wave1;w2;")      // Prints "wave0;w2;"
```

### *See Also* {#see-also}
[AddListItem](/igorpro/commands/addlistitem.md), [RemoveFromList](/igorpro/commands/removefromlist.md), [WhichListItem](/igorpro/commands/whichlistitem.md), [StringFromList](/igorpro/commands/stringfromlist.md), [FindListItem](/igorpro/commands/findlistitem.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [RemoveByKey](/igorpro/commands/removebykey.md), [AddListItem](/igorpro/commands/addlistitem.md), [WaveList](/igorpro/commands/wavelist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [StringList](/igorpro/commands/stringlist.md), [VariableList](/igorpro/commands/variablelist.md), [FunctionList](/igorpro/commands/functionlist.md)