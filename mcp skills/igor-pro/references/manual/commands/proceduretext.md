---
description: "The ProcedureText function returns a string containing the text of the named macro or function as it exists in some procedure file, optionally with additional…"
slug: /commands/proceduretext
---

<div className="command-signature">

## <strong>ProcedureText</strong> (<em>macroOrFunctionNameStr</em> [, <em>linesOfContext</em> [, <em>procedureWinTitleStr</em>]]) {#proceduretext}

</div>

The ProcedureText function returns a string containing the text of the named macro or function as it exists in some procedure file, optionally with additional lines that are before and after to provide context or to collect documenting comments.

Alternatively, all of the text in the specified procedure window can be returned.

### *Parameters* {#parameters}
*macroOrFunctionNameStr* identifies the macro or function. It may be just the name of a global (nonstatic) procedure, or it may include a module name, such as "myModule#myFunction" to specify the static function myFunction in a procedure window that contains a #pragma ModuleName=myModule statement.

If *macroOrFunctionNameStr* is set to "", and *procedureWinTitleStr* specifies the title of a single procedure window, then all of the text in the procedure window is returned.

*linesOfContext* optionally specifies the number of lines around the function to include in the returned string.

The default is 0 (no additional contextual lines of text are returned). This parameter is ignored if *macroOrFunctionNameStr* is "" and *procedureWinTitleStr* specifies the title of a single procedure window.

Setting *linesOfContext* to a positive number returns that many lines before the procedure and after the procedure. Blank lines are not omitted.

Setting *linesOfContext* to -1 returns lines before the procedure that are not part of the preceding macro or function. Usually these lines are comment lines describing the named procedure. Blank lines are omitted.

Setting *linesOfContext* to -*n* , where *n* >1, returns at most *n* lines before the procedure that are not part of the preceding macro or function. Blank lines are not omitted in this case. *n* can be -inf, which acts the same as -1 but includes blank lines.

The optional *procedureWinTitleStr* can be the title of a procedure window (such as "Procedure" or "File Name Utilities.ipf"). The text of the named macro or function in the specified procedure window is returned.

You can use *procedureWinTitleStr* to select one of several [Static Functions](/igorpro/programming/programming.md#static-functions) with identical names among different procedure windows, even if they do not use a #pragma moduleName=myModule statement.

### *Advanced Parameters* {#advanced-parameters}
If SetIgorOption IndependentModuleDev=1, *procedureWinTitleStr* can also be a title followed by a space and, in brackets, an independent module name. In such cases ProcedureText retrieves function text from the specified procedure window and independent module. (See [Independent Modules](/igorpro/advanced-topics.md#independent-modules) for independent module details.)

For example, in any procedure file containing:


```igor
#pragma IndependentModule=myIM
#include <Axis Utilities>
```

A call to ProcedureText like this:


```igor
String text=ProcedureText("HVAxisList",0,"Axis Utilities.ipf [myIM]")
```

will return the text of the HVAxisList function located in the Axis Utilities.ipf procedure window, which is normally a hidden part of the myIM independent module.

You can see procedure window titles in this format in the Windows->Procedure Windows menu when SetIgorOption IndependentModuleDev=1 and when an experiment contains procedure windows that comprise an independent module, as does #include \<New Polar Graphs\>.

*procedureWinTitleStr* can also be just an independent module name in brackets to retrieve the function text from **any** procedure window that belongs to the named independent module:


```igor
String text=ProcedureText("HVAxisList",0,"[myIM]")
```

### *See Also* {#see-also}
[Regular Modules](/igorpro/advanced-topics.md#regular-modules), [Independent Modules](/igorpro/advanced-topics.md#independent-modules)

[WinRecreation](/igorpro/commands/winrecreation.md), [FunctionList](/igorpro/commands/functionlist.md)