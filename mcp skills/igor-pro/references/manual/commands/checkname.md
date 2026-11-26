---
description: "The CheckName function returns a number which indicates if the specified name is legal and unique among objects in the namespace of the specified object type."
slug: /commands/checkname
---

<div className="command-signature">

## <strong>CheckName</strong> (<em>nameStr</em>, <em>objectType</em> [, <em>windowNameStr</em> ]) {#checkname}

</div>

The CheckName function returns a number which indicates if the specified name is legal and unique among objects in the namespace of the specified object type.

In Igor Pro 9.00 or later, you can use the [CreateDataObjectName](/igorpro/commands/createdataobjectname.md) function as a replacement for some combination of CheckName, CleanupName, and UniqueName to create names of waves, global variables, and data folders.

Waves, global numeric variables and global string variables are all in the same namespace and need to be unique only within the data folder containing them. However, they also need to be distinct from names of Igor operations and functions and from names of user-defined procedures.

Data folders are in their own namespace and need to be unique only among other data folders at the same level of the data folder hierarchy.

*WindowNameStr* is optional. If missing, it is taken to be the top graph, panel, layout, or notebook according to the value of *objectType*.

### *Details* {#details}
A result of zero indicates that the name is legal and unique within its namespace. Any nonzero result indicates that the name is illegal or not unique. You can use the CleanupName and UniqueName functions to guarantee legality and uniqueness.

*nameStr* should contain an unquoted name (i.e., no single quotes for liberal names), such as you might receive from the user through a dialog or control panel.

*objectType* is one of the following:

|  |  |
| --- | --- |
| 1: | Wave. |
| 2: | Reserved for future use. |
| 3: | Global numeric variable. |
| 4: | Global string variable. |
| 5: | XOP target window. |
| 6: | Graph window. |
| 7: | Table window. |
| 8: | Layout window. |
| 9: | Control panel window. |
| 10: | Notebook window. |
| 11: | Data folder. |
| 12: | Symbolic path. |
| 13: | Picture. |
| 14: | Annotation in the named or topmost graph or layout. |
| 15: | Control in the named topmost graph or panel. |
| 16: | Notebook action character in the named or topmost notebook. |

The *windowNameStr* argument is used only with *objectTypes* 14, 15, and 16. The *nameStr* is checked for uniqueness only within the named window (other windows might have objects with the given name). If a named window is given but does not exist, any valid *nameStr* is permitted.

### *CheckName Thread Safety* {#checkname-thread-safety}
As of Igor Pro 8.00, you can call CheckName from an Igor preemptive thread but only if *objectType* is 1 (wave), 3 (global numeric variable), 4 (global string variable), 11 (data folder) or 12 (symbolic path). For any other value of *objectType*, CheckName returns a runtime error.

### *Examples* {#examples}

```igor
Variable waveNameIsOK = CheckName(proposedWaveName, 1) == 0
Variable annotationNameIsOK = CheckName("text0", 14, "Graph0") == 0

// Create a valid and unique wave name
Function/S CreateValidAndUniqueWaveName(proposedName)
    String proposedName

    String result = proposedName
	
    if (CheckName(result,1) != 0)           // 1 for waves
        result = CleanupName(result, 1)     // Make sure it's valid
        result = UniqueName(result, 1, 0)   // Make sure it's unique
    endif
	
    return result
End
```

### *See Also* {#see-also}
[Object Names](/igorpro/igor-basics/using-igor.md#object-names), [Programming With Liberal Names](/igorpro/programming/programming-techniques.md#programming-with-liberal-names), [CreateDataObjectName](/igorpro/commands/createdataobjectname.md), [CleanupName](/igorpro/commands/cleanupname.md), [UniqueName](/igorpro/commands/uniquename.md)