---
description: "The FindListItem function returns the byte offset into listStr where itemStr begins. listStr should contain items separated by the listSepStr."
slug: /commands/findlistitem
---

<div className="command-signature">

## <strong>FindListItem</strong> (<em>itemStr</em>, <em>listStr</em> [, <em>listSepStr</em> [, <em>start</em> [, <em>matchCase</em> ]]]) {#findlistitem}

</div>

The FindListItem function returns the byte offset into *listStr* where *itemStr* begins. *listStr* should contain items separated by the *listSepStr*.

Use FindListItem to locate the start of an item in a string containing a "wave0;wave1;" style list such as those returned by functions like [TraceNameList](/igorpro/commands/tracenamelist.md) or [AnnotationList](/igorpro/commands/annotationlist.md), or a line from a delimited text file.

Use [WhichListItem](/igorpro/commands/whichlistitem.md) to determine the index of an item in the list.

If *itemStr* is not found,  if *listStr* is *"",* or if *start* is not within the range of 0 to strlen(*listStr* )-1, then -1 is returned.

*listSepStr*, *start* and *matchCase* are optional; their defaults are ";", 0, and 1 respectively.

### *Details* {#details}
*ItemStr* may have any length.

*listStr* is searched for the first instance of the item string bound by a *listSepStr*  on the left and a *listSepStr* on the right. The returned number is the byte index where the first character of *itemStr* was found in *listSepStr*.

The search starts from the byte position in *listStr* specified by *start*. A value of 0 starts with the first character in *listStr*, which is the default if *start* is not specified.

*listString* is treated as if it starts and ends with a *listSepStr* even if it doesn't.

Searches for *listSepStr* are always case-sensitive.

The comparison of *itemStr* to the contents of *listStr* is usually case-sensitive. Setting the optional *matchCase* parameter to 0 makes the comparison case insensitive.

In Igor 6, only the first byte of *listSepStr* was used. In Igor 7 and later, all bytes are used.

If *start* is specified, then *listSepStr* must also be specified.  If *matchCase* is specified, *start* and *listSepStr* must be specified.

### *Examples* {#examples}

```igor
Print FindListItem("w1", "w0;w1;w2,")           // prints 3
Print FindListItem("v2", "v1,v2,v3,", ",")      // prints 3
Print FindListItem("v2", "v0,v2,v2,", ",", 4)   // prints 6
Print FindListItem("C", "a;c;C;")               // prints 4
Print FindListItem("C", "a;c;C;", ";", 0, 0)    // prints 2
```

### *See Also* {#see-also}
[AddListItem](/igorpro/commands/addlistitem.md), [strsearch](/igorpro/commands/strsearch.md), [StringFromList](/igorpro/commands/stringfromlist.md), [RemoveListItem](/igorpro/commands/removelistitem.md), [RemoveFromList](/igorpro/commands/removefromlist.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [WhichListItem](/igorpro/commands/whichlistitem.md), [WaveList](/igorpro/commands/wavelist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [StringList](/igorpro/commands/stringlist.md), [VariableList](/igorpro/commands/variablelist.md), [FunctionList](/igorpro/commands/functionlist.md)