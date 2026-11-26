---
description: "The OperationList function returns a string containing a list of internal (built-in) or external operation names names corresponding to matchstr."
slug: /commands/operationlist
---

<div className="command-signature">

## <strong>OperationList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>optionsStr</em>) {#operationlist}

</div>

The OperationList function returns a string containing a list of internal (built-in) or external operation names names corresponding to *matchstr*.

### *Parameters* {#parameters}
Only operation names that match the *matchStr* string are listed. Use "*" to match all names. See [WaveList](/igorpro/commands/wavelist.md) for examples.

*separatorStr* is appended to each operation name as the output string is generated. *separatorStr* is usually ";" for list processing (See the [Processing Lists of Waves](/igorpro/programming/programming-techniques.md#processing-lists-of-waves) topic in the Programming Techniques help file for details).

*optionsStr* is used to further qualify the list of operations. It is a string containing one of these (case-insensitive) values:


|  |  |
| --- | --- |
| "internal" | Restricts the list to built-in operations. |
| "external" | Restricts the list to external operations (provided by [Igor Extensions](/igorpro/igor-basics/using-igor.md#igor-extensions)). |

Any other value for *optionsStr* ("all" is recommended) will return both internal and external operations.

### *See Also* {#see-also}
[FunctionList](/igorpro/commands/functionlist.md), [MacroList](/igorpro/commands/macrolist.md), [StringFromList](/igorpro/commands/stringfromlist.md), [WinList](/igorpro/commands/winlist.md)

[DisplayProcedure](/igorpro/commands/displayprocedure.md)