---
description: "The FunctionList function returns a string containing a list of built-in or user-defined function names satisfying certain criteria."
slug: /commands/functionlist
---

<div className="command-signature">

## <strong>FunctionList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>optionsStr</em>) {#functionlist}

</div>

The FunctionList function returns a string containing a list of built-in or user-defined function names satisfying certain criteria. This is useful for making a string to list functions in a pop-up menu control. Note that if the procedures need to be compiled, then FunctionList will not list user-defined functions.

### *Parameters* {#parameters}
Only functions having names that match the *matchStr* string are listed. Use "\*" to match all names. See [WaveList](/igorpro/commands/wavelist.md) for examples.

*separatorStr* is appended to each function name as the output string is generated. *separatorStr* is usually ";" for list processing (See the [Processing Lists of Waves](/igorpro/programming/programming-techniques.md#processing-lists-of-waves) topic in the Programming Techniques help file for details on list processing).

*optionsStr* is used to further qualify the list of functions. It is a string containing keyword-value pairs separated by commas. Available options are:


|  |  |
| --- | --- |
| KIND:*nk* |<table class="nested-table"><tbody><tr><td>*nk*&nbsp;=&nbsp;1:</td><td>List built-in functions.</td></tr><tr><td>*nk*&nbsp;=&nbsp;2:</td><td>List normal and [override](/igorpro/programming/keywords/other-programming-keywords.md#override) user-defined functions.</td></tr><tr><td>*nk*&nbsp;=&nbsp;4:</td><td>List external functions (defined by an XOP).</td></tr><tr><td>*nk*&nbsp;=&nbsp;8:</td><td>List only curve fitting functions; must be summed with 1, 2, 4, or 16. For example, use 10 to list user-defined fitting functions.</td></tr><tr><td>*nk*&nbsp;=&nbsp;16:</td><td>Include [static](/igorpro/programming/keywords/other-programming-keywords.md#static) user-defined functions; requires WIN: option, must be summed with 1, 2, or 8. To list only static functions, subtract the non-static functions using RemoveFromList.</td></tr></tbody></table>
| NPARAMS:*np* | Restricts the list to functions having exactly *np* parameters. Omitting this option lists functions having any number of parameters. |
| NINDVARS:*ni* | Restricts the list to fitting functions for exactly *ni* independent variables. NINDVARS is ignored if you have not elected to list curve fitting functions using the KIND option. Functions for any number of independent variables are listed if the NINDVARS option is omitted. |
| NRETURN:*nRet* | Restricts list to user-defined functions that use the [Multiple Return Syntax](/igorpro/programming/programming.md#multiple-return-syntax) to return *nRet* values. |
|  | NRETURN is ignored if KIND:8 is specified. |
|  | NRETURN was added in Igor Pro 9.00. |
| PARAM_*n*_TYPE:*pType* | Restricts list to functions whose *n*th input parameter type is a certain kind as described by *pType*. |
|  | PARAM_*n*_TYPE is ignored if KIND:8 is specified. |
|  | PARAM_*n*_TYPE was added in Igor Pro 9.00. |
|  | Use PARAM_0_TYPE for the first parameter, PARAM_1_TYPE for the second parameter, and so on. You can use any number of PARAM_*n*_TYPE keyword=value pairs in a given FunctionList call. |
|  | For each parameter, set *pType* to a parameter type code as described under ***Return Type and Parameter Type Codes*** below. |
|  | See also ***Return Type and Parameter Type Code Examples*** below. |
| RETURN_*n*_TYPE:*rType* | Restricts list to user-defined functions whose *n*th [Multiple Return Syntax](/igorpro/programming/programming.md#multiple-return-syntax) return type is a certain kind described by *rType*. |
|  | RETURN_*n*_TYPE is ignored if KIND:8 is specified. |
|  | RETURN_*n*_TYPE was added in Igor Pro 9.00. |
|  | Use RETURN_0_TYPE for the first return value, RETURN_1_TYPE for the second return value, and so on. You can use any number of RETURN_*n*_TYPE keyword=value pairs in a given FunctionList call. |
|  | For each return value, set *rType* to a return type code as described under ***Return Type and Parameter Type Code*s** below. |
| SUBTYPE:*typeName* | Lists functions that have the type *typeName*. That is, you could use ButtonControl as *typeName* to list only functions that are action procedures for buttons. |
| VALTYPE:*nv* | Restricts list to functions whose return type is a certain kind. |
|  |<table class="nested-table"><tbody><tr><td>*nv*&nbsp;=&nbsp;1:</td><td>Real-valued functions</td></tr><tr><td>*nv*&nbsp;=&nbsp;2:</td><td>Complex-valued functions</td></tr><tr><td>*nv*&nbsp;=&nbsp;4:</td><td>String functions</td></tr><tr><td>*nv*&nbsp;=&nbsp;8:</td><td>WAVE functions</td></tr><tr><td>*nv*&nbsp;=&nbsp;16:</td><td>DFREF functions</td></tr><tr><td>*nv*&nbsp;=&nbsp;32:</td><td>[Multiple Return Syntax](/igorpro/programming/programming.md#multiple-return-syntax) functions.</td></tr><tr><td></td><td>See also RETURN_n_TYPE.</td></tr></tbody></table>
|  | Use a sum of these values to include more than one type. The return type is not restricted if this option is omitted. |
| WIN:*windowTitle* | Lists functions that are defined in the procedure window with the given title. "Procedure" is the title of the built-in procedure window. |
|  | <div><Admonition type="note"><p>Because the *optionsStr* keyword-value pairs are comma separated and procedure window titles can have commas in them, the WIN: keyword must be the last one specified.</p></Admonition></div> |
| WIN:*windowTitle* [*independentModuleName* ] |  |
|  | Lists functions that are defined in the named procedure window that belongs to the independent module *independentModuleName*. See [Independent Modules](/igorpro/advanced-topics.md#independent-modules) for details. Requires SetIgorOption independentModuleDev=1, otherwise no functions are listed. |
|  | Requires *independentModuleName* = ProcGlobal or SetIgorOption independentModuleDev=1, otherwise no functions are listed. |
|  | <div><Admonition type="note"><p>The syntax is literal and strict: the window title must be followed by one space and a left bracket, followed directly by the independent module name and a closing right bracket.</p></Admonition></div> |
| WIN:[*independentModuleName* ] |  |
|  | Lists functions that are defined in any procedure file that belongs to the named independent module. |
|  | Requires *independentModuleName* = ProcGlobal or SetIgorOption independentModuleDev=1, otherwise no functions are listed. |
|  | <div><Admonition type="note"><p>The syntax is literal and strict: 'WIN:' must be followed by a left bracket, followed directly by the independent module name and a closing right bracket, like this:</p></Admonition></div> |
|  | <code class="igor">FunctionList(...,"WIN:[myIndependentModuleName]")</code> |

### *Return Type and Parameter Type Codes* {#return-type-and-parameter-type-codes}
These codes are used with the PARAM_N_TYPE and RETURN_N_TYPE keywords:

| Type | Code | Code in Hex |
| --- | --- | --- |
| Complex | 1 | 0x1 |
| Single Precision | 2 | 0x2 |
| Variable | 4 | 0x4 |
| Double Precision | 4 | 0x4 |
| Byte | 8 | 0x8 |
| 16-bit Integer | 16 | 0x10 |
| 32-bit Integer | 32 | 0x20 |
| Unsigned | 64 | 0x40 |
| <span class="table-cell-nowrap">/WAVE</span> | 128 | 0x80 |
| Data folder reference | 256 | 0x100 |
| Structure | 512 | 0x200 |
| Function reference | 1024 | 0x400 |
| Pass by reference parameter | 4096 | 0x1000 |
| String | 8192 | 0x2000 |
| Wave | 16384 | 0x4000 |
| <span class="table-cell-nowrap">/Z</span> | 32768 | 0x8000 |

### *Special Return Type and Parameter Type Codes* {#special-return-type-and-parameter-type-codes}
These special codes are used with the PARAM_N_TYPE and RETURN_N_TYPE keywords:


| Type | Code |
| --- | --- |
| Any real-valued numeric wave | -2 |
| Any complex-valued numeric wave | -3 |
| Any text wave | -4 |
| Any WAVE<span class="table-cell-nowrap">/WAVE</span> | -5 |
| Any WAVE<span class="table-cell-nowrap">/DF</span> | -6 |

### *Return Type and Parameter Type Code Examples* {#return-type-and-parameter-type-code-examples}
This section shows common values used withe PARAM_N_TYPE and RETURN_N_TYPE keywords:


| Type | Code | Code in Hex |
| --- | --- | --- |
| Any real-valued numeric wave | -2 |  |
| Any complex numeric wave | -3 |  |
| Any text wave | -4 |  |
| Wave<span class="table-cell-nowrap">/S</span> | 16386 | 0x4000 + 2 |
| Wave or Wave<span class="table-cell-nowrap">/D</span> | 16388 | 0x4000 + 4 |
| Wave<span class="table-cell-nowrap">/C</span> or Wave<span class="table-cell-nowrap">/D/C</span> | 16389 | 0x4000 + 4 + 1 |
| Wave<span class="table-cell-nowrap">/T</span> | 16384 | 0x4000 + 0 |

If /Z is used, add 32768 or 0x8000.

For pass-by-reference parameters, add 4096 or 0x1000.

To list user-defined functions in the main procedure window that have either a Wave or Wave/D first parameter, with or without /Z:


```igor
Print FunctionList("*",";","KIND:2,PARAM_0_TYPE:-2,WIN:Procedure") // WIN must be last option
```

### *Examples* {#examples}
To list user-defined fitting functions for two independent variables:


```igor
Print FunctionList("*",";","KIND:10,NINDVARS:2")
```

To list button-control functions that start with the letter "b" (note that button-control functions are user-defined):


```igor
Print FunctionList("b*",";","KIND:2,SUBTYPE:ButtonControl")
```

### *See Also* {#see-also}
[DisplayProcedure](/igorpro/commands/displayprocedure.md), [FunctionInfo](/igorpro/commands/functioninfo.md), [Independent Modules](/igorpro/advanced-topics.md#independent-modules), [MacroList](/igorpro/commands/macrolist.md), [Multiple Return Syntax](/igorpro/programming/programming.md#multiple-return-syntax),   [OperationList](/igorpro/commands/operationlist.md), [Procedure Subtypes](/igorpro/programming/programming-techniques.md#procedure-subtypes), [StringFromList](/igorpro/commands/stringfromlist.md), [WinList](/igorpro/commands/winlist.md).