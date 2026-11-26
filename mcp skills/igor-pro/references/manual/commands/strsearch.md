---
description: "The strsearch function returns the byte position of the string expression findThisStr in the string expression str."
slug: /commands/strsearch
---

<div className="command-signature">

## <strong>strsearch</strong> (<em>str</em>, <em>findThisStr</em>, <em>start</em>  [, <em>options</em>]) {#strsearch}

</div>

The strsearch function returns the byte position of the string expression *findThisStr* in the string expression *str*.

### *Details* {#details}
strsearch performs a case-sensitive search.

strsearch returns -1 if *findThisStr* does not occur in *str*.

The search starts from the byte position in *str* specified by *start*; 0 references the start of *str*.

strsearch clips *start* to one less than the length of *str* in bytes, so it is useful to use [Inf](/igorpro/commands/inf.md) for *start* when searching backwards to ensure that the search is from the end of *str*.

*options* is an optional bitwise parameter specifying the search options:

|  |  |
| --- | --- |
| 1: | Search backwards from *start.* |
| 2: | Ignore case. |
| 3: | Search backwards and ignore case. |

### *Examples* {#examples}

```igor
String str="This is a test isn't it?"
Print strsearch(str,"test",0)           // prints 10
Print strsearch(str,"TEST",0)           // prints -1
Print strsearch(UpperStr(str),"TEST",0) // prints 10
Print strsearch(str,"TEST",0,2)         // prints 10
Print strsearch(str,"is",0)             // prints 2
Print strsearch(str,"is",3)             // prints 5
Print strsearch(str,"is",Inf,1)         // prints 15
```

### *See Also* {#see-also}
[sscanf](/igorpro/commands/sscanf.md), [FindListItem](/igorpro/commands/findlistitem.md), [ReplaceString](/igorpro/commands/replacestring.md), [Character-by-Character Operations](/igorpro/programming/programming-techniques.md#character-by-character-operations)

[Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters)