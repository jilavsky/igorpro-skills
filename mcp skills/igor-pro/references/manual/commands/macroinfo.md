---
description: "The MacroInfo function returns a keyword-value pair list of information about the named macro."
slug: /commands/macroinfo
---

<div className="command-signature">

## <strong>MacroInfo</strong> (<em>macroNameStr</em>) {#macroinfo}

</div>

The MacroInfo function returns a keyword-value pair list of information about the named macro.

### *Parameters* {#parameters}
*macroNameStr* is a string expression containing the name of a Macro, Proc, or Window procedure.

*macroNameStr* can also be "" to return information about the currently running macro.

### *Details* {#details}
The returned string contains several groups of information. Each group is prefaced by a keyword and colon, and terminated with the semicolon. Use [StringByKey](/igorpro/commands/stringbykey.md) and [NumberByKey](/igorpro/commands/numberbykey.md) to extract the values that follow the keywords. The keywords are as follows:


| Keyword | Information Following Keyword |
| --- | --- |
| KIND | "Proc", "Macro", or "Window", depending on how the procedure is defined. |
| NAME | The name of the macro. Same as contents of *macroNameStr* in most cases. |
| N_PARAMS | Number of parameters for the macro. |
| PARAM_*n*_TYPE | Number encoding the type of each parameter. There will be N of these keywords, one for each parameter. The part shown as *n* will be a number from 0 to N-1. |
| PROCLINE | Line number within the procedure window of the macro definition. |
| PROCWIN | Title of procedure window containing the macro definition. |
| SUBTYPE | The procedure subtype, for instance [GraphStyle](/igorpro/programming/keywords/procedure-subtype-keywords.md#graphstyle). See [Procedure Subtype Keywords](/igorpro/programming/keywords/procedure-subtype-keywords.md) for others. |

**PARAM_*n*_TYPE Codes**

| Type | Code | Code in Hex |
| --- | --- | --- |
| Variable | 4 | 0x4 |
| Variable<span class="table-cell-nowrap">/C</span> | 5 | 0x5 |
| String | 8192 | 0x2000 |

### *Example* {#example}

```igor
Proc MyGraphStyle() : GraphStyle
	String info = MacroInfo("")
	String myName = StringByKey("NAME", info)
	ModifyGraph/Z standoff=0
End
```

### *See Also* {#see-also}
[FunctionInfo](/igorpro/commands/functioninfo.md), [FunctionList](/igorpro/commands/functionlist.md), [MacroList](/igorpro/commands/macrolist.md), [NumberByKey](/igorpro/commands/numberbykey.md), [StringByKey](/igorpro/commands/stringbykey.md).

For details on procedure subtypes, see [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes), [Button](/igorpro/commands/button.md), [CheckBox](/igorpro/commands/checkbox.md), [PopupMenu](/igorpro/commands/popupmenu.md),  [SetVariable](/igorpro/user-interface/controls.md#setvariable).