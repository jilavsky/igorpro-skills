---
description: "The MacroList function returns a string containing a list of the names of user-defined procedures that start with the Proc, Macro, or Window keywords that…"
slug: /commands/macrolist
---

<div className="command-signature">

## <strong>MacroList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>optionsStr</em>) {#macrolist}

</div>

The MacroList function returns a string containing a list of the names of user-defined procedures that start with the Proc, Macro, or Window keywords that also satisfy certain criteria. Note that if the procedures need to be compiled, then MacroList may not list all of the procedures.

### *Parameters* {#parameters}
Only macros having names that match *matchStr* string are listed. See [WaveList](/igorpro/commands/wavelist.md) for examples.

The first character of *separatorStr* is appended to each macro name as the output string is generated. *separatorStr* is usually ";" for list processing (See the [Processing Lists of Waves](/igorpro/programming/programming-techniques.md#processing-lists-of-waves) topic in the Programming Techniques help file for details on list processing).

*optionsStr* is used to further qualify the macros. It is a string containing keyword-value pairs separated by commas. Available options are:


|  |  |
| --- | --- |
| KIND:*nk* |<table class="nested-table"><tbody><tr><td>*nk*&nbsp;=&nbsp;1:</td><td>List Proc procedures.</td></tr><tr><td>*nk*&nbsp;=&nbsp;2:</td><td>List Macro procedures.</td></tr><tr><td>*nk*&nbsp;=&nbsp;4:</td><td>List Window procedures.</td></tr></tbody></table>
|  | *nk* can be the sum of these values to match multiple procedure kinds. For example, use 3 to list both Proc and Macro procedures. |
| NPARAMS:*np* | Restricts the list to macros having exactly *np* parameters. Omitting this option lists macros having any number of parameters. |
| SUBTYPE:*typeStr* | Lists macros that have the type *typeStr*. That is, you could use ButtonControl as *typeStr* to list only macros that are action procedures for buttons. |
| WIN:*windowNameStr* | Lists macros that are defined in the named procedure window. "Procedure" is the name of the built-in procedure window. |
|  | <div><Admonition type="note"><p>Because the *optionsStr* keyword-value pairs are comma separated and procedure window names can have commas in them, the WIN: keyword must be the last one specified.</p></Admonition></div> |

### *Examples* {#examples}
To list all Macros with three parameters:


```igor
Print MacroList("*",";","KIND:2,NPARAMS:3")
```

To list all Macro, Proc, and Window procedures in the main procedure window whose names start with b:


```igor
Print MacroList("b*",";","WIN:Procedure")
```

### *See Also* {#see-also}
[DisplayProcedure](/igorpro/commands/displayprocedure.md)

[FunctionList](/igorpro/commands/functionlist.md), [StringFromList](/igorpro/commands/stringfromlist.md), [WinList](/igorpro/commands/winlist.md)

For details on procedure subtypes, see [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes), [Button](/igorpro/commands/button.md), [CheckBox](/igorpro/commands/checkbox.md), [SetVariable](/igorpro/user-interface/controls.md#setvariable), [PopupMenu](/igorpro/commands/popupmenu.md).