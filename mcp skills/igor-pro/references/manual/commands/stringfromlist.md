---
description: "The StringFromList function returns the index-th substring extracted from listStr starting offset bytes into listStr."
slug: /commands/stringfromlist
---

<div className="command-signature">

## <strong>StringFromList</strong> (<em>index</em>, <em>listStr</em> [, <em>listSepStr</em> [, <em>offset</em>]]) {#stringfromlist}

</div>

The StringFromList function returns the *index*-th substring extracted from *listStr* starting *offset* bytes into *listStr* . *listStr* should contain items items separated by *listSepStr* which typically is ";".

Use StringFromList to extract an item from a string such as those returned by functions like [TraceNameList](/igorpro/commands/tracenamelist.md) and [AnnotationList](/igorpro/commands/annotationlist.md).

### *Parameters* {#parameters}
*index* is the zero-based index of the list item that you want to get. If *index* < 0, or *index* >= the number of items in list, or if *listStr* or *listSepStr* is "", then a zero length string is returned.

*listStr* contains a series of text items separated by *listSepStr*. The trailing separator is optional though recommended. For example, these are both valid lists:


```igor
"First;Second;"
"First;Second"
```

*listSepStr* is optional. If omitted it defaults to ";". Prior to Igor Pro 7.00, only the first byte of *listSepStr* was used. Now all bytes are used.

*offset* is optional and requires Igor Pro 7.00 or later. If omitted it defaults to 0. The search begins *offset* bytes into *listStr*. When iterating through lists containing large numbers of items, using the *offset* parameter provides dramatically faster execution.

### *Details* {#details}
For optimal performance, especially with lists larger than 100 items, provide the *separatorStr* and *offset* parameters as shown in the DemoStringFromList example below. When using this technique, the index parameter must be 0 and the *offset* parameter controls which list item is returned.

### *Examples* {#examples}

```igor
Print StringFromList(0, "wave0;wave1;")	 // Prints "wave0"
Print StringFromList(2, "wave0;wave1;")	 // Prints ""
Print StringFromList(1, "wave0;;wave2;")	 // Prints ""

// Iterate quickly over a list using the offset parameter
Function DemoQuickStringFromList(list)
	String list			// A semicolon-separated string list

	String separator = ";"
	Variable separatorLen = strlen(separator)
	Variable numItems = ItemsInList(list, separator)

	Variable offset = 0
	Variable i
	for(i=0; i<numItems; i+=1)
		// When using offset, the index parameter is always 0
		String item = StringFromList(0, list, separator, offset)
		// Do something with item
		offset += strlen(item) + separatorLen
	endfor
End
```

### *See Also* {#see-also}
[AddListItem](/igorpro/commands/addlistitem.md), [ItemsInList](/igorpro/commands/itemsinlist.md), [FindListItem](/igorpro/commands/findlistitem.md), [RemoveListItem](/igorpro/commands/removelistitem.md), [RemoveFromList](/igorpro/commands/removefromlist.md), [WhichListItem](/igorpro/commands/whichlistitem.md), [WaveList](/igorpro/commands/wavelist.md), [StringByKey](/igorpro/commands/stringbykey.md), [ListMatch](/igorpro/commands/listmatch.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [StringList](/igorpro/commands/stringlist.md), [VariableList](/igorpro/commands/variablelist.md), [FunctionList](/igorpro/commands/functionlist.md), [ListToTextWave](/igorpro/commands/listtotextwave.md)