---
description: "The ProcedureVersion function returns the version number as specified by the first #pragma version=versionNum in the procedure file containing the named…"
slug: /commands/procedureversion
---

<div className="command-signature">

## <strong>ProcedureVersion</strong> (<em>macroOrFunctionNameStr</em> [, <em>procedureWinTitleStr</em>]) {#procedureversion}

</div>

The ProcedureVersion function returns the version number as specified by the first #pragma version=*versionNum* in the procedure file containing the named macro, function. Alternatively it can returh the version number of a specified procedure window.

The ProcedureVersion function was added in Igor Pro 9.01.

### *Parameters* {#parameters}
*macroOrFunctionNameStr* identifies the macro or function. It may be just the name of a global (nonstatic) procedure, or it may include a module name, such as "MyModule#MyFunction" to specify the static function MyFunction in a procedure window that contains a #pragma ModuleName=MyModule statement.

If *macroOrFunctionNameStr* is "" and *procedureWinTitleStr* is not specified then the value of the first #pragma version statement in the procedure window containing the currently running macro or function is returned.

If *macroOrFunctionNameStr* is "" and *procedureWinTitleStr* is specified then the value of the first #pragma version statement in that procedure window is returned.

### *Details* {#details}
The return value is rounded to a multiple of 0.001.

The returned value is 0 if the #pragma version statement is absent or the procedure window is "invisible" because the function is an independent module but SetIgorOption IndependentModule=0.

### *Example* {#example}

```igor
#pragma version=1.2345  // 1 more digit than recommended
...
Function Test()
	Variable version = ProcedureVersion("") // Version of procedure file containing test
	Print version                           // 1.234
End
```

### *See Also* {#see-also}
[ProcedureText](/igorpro/commands/proceduretext.md), [FunctionList](/igorpro/commands/functionlist.md), [MacroList](/igorpro/commands/macrolist.md)

[Procedure File Version Information](/igorpro/programming/programming-techniques.md#procedure-file-version-information), [ProcedureVersion](/igorpro/commands/procedureversion.md), [The ModuleName Pragma](/igorpro/programming/programming.md#the-modulename-pragma)

[SetIgorOption IndependentModuleDev=1](/igorpro/advanced-topics.md#setigoroption-independentmoduledev-1), [Invisible Procedure Files Using Independent Modules](/igorpro/programming/procedure-windows.md#invisible-procedure-files-using-independent-modules)