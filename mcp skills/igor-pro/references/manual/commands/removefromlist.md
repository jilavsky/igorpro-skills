---
description: "The RemoveFromList function returns listStr after removing the item or items specified by itemOrListStr."
slug: /commands/removefromlist
---

<div className="command-signature">

## <strong>RemoveFromList</strong> (<em>itemOrListStr</em>, <em>listStr</em> [, <em>listSepStr</em> [, <em>matchCase</em> ]]) {#removefromlist}

</div>

The RemoveFromList function returns *listStr* after removing the item or items specified by *itemOrListStr*. *listStr* should contain items separated by *listSepStr* which typically is ";".

If *itemOrListStr* contains multiple items, they should be separated by the *listSepStr* character, too.

Use RemoveFromList to remove item(s) from a string containing a list of items separated by a string (usually a single ASCII character), such as those returned by functions like [TraceNameList](/igorpro/commands/tracenamelist.md) or [AnnotationList](/igorpro/commands/annotationlist.md), or a line from a delimited text file.

If all items in *itemOrListStr* are not found or if any of the arguments  is "" then *listStr* is returned unchanged (unless *listStr* contains only list separators, in which case an empty string ("") is returned).

*listSepStr* is optional. If missing, *listSepStr* is presumed to be  ";" .

*listSepStr* and *matchCase* are optional; their defaults are ";" and 1 respectively.

### *Details* {#details}
*listStr* is searched for an instance of the item string(s) bound by *listSepStr* on the left and right. All instances of the item(s) and any trailing *listSepStr* (if any) are removed from the returned string.

If the resulting string contains only *listSepStr* characters, then an empty string ("") is returned.

*listStr* is treated as if it ends with a *listSepStr* even if it doesn't.

Searches for *listSepStr* are always case-sensitive. The searches for items in *itemOrListStr* are usually case-sensitive. Setting the optional *matchCase* parameter to 0 makes the comparisons case insensitive.

In Igor 6, only the first byte of *listSepStr* was used. In Igor 7 and later, all bytes are used.

If *matchCase* is specified, then *listSepStr* must also be specified.

### *Examples* {#examples}

```igor
Print RemoveFromList("wave1", "wave0;wave1;")           // prints "wave0;"
Print RemoveFromList("wave1", ";wave1;;;;")             // prints ""
Print RemoveFromList("KEY=joy", "AX=3,KEY=joy", ",")    // prints "AX=3,"
Print RemoveFromList("fred", "fred\twilma", "\t")       // prints "wilma"
Print RemoveFromList("fred;barney","fred;wilma;barney") // prints "wilma;"
Print "X"+RemoveFromList("",";;;;")+"Y"                 // prints "XY"
Print RemoveFromList("FRED", "fred;wilma")              // prints "fred;wilma"
Print RemoveFromList("FRED", "fred;wilma", ";", 0)      // prints "wilma"
```

### *See Also* {#see-also}
[StringFromList](/igorpro/commands/stringfromlist.md), [RemoveListItem](/igorpro/commands/removelistitem.md), [RemoveByKey](/igorpro/commands/removebykey.md), [FindListItem](/igorpro/commands/findlistitem.md), [ItemsInList](/igorpro/commands/itemsinlist.md),  [WaveList](/igorpro/commands/wavelist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [StringList](/igorpro/commands/stringlist.md), [VariableList](/igorpro/commands/variablelist.md), [FunctionList](/igorpro/commands/functionlist.md), [UpperStr](/igorpro/commands/upperstr.md)