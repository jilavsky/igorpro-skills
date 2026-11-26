---
description: "The ParseOperationTemplate operation helps XOP programmers and WaveMetrics programmers write code to implement Igor operations."
slug: /commands/parseoperationtemplate
---

<div className="command-signature">

## <strong>ParseOperationTemplate</strong>  [/C=<em>c</em> /S=<em>s</em> /T/TS] <em>cmdTemplate</em> {#parseoperationtemplate}

</div>

The ParseOperationTemplate operation helps XOP programmers and WaveMetrics programmers write code to implement Igor operations. If you are not an XOP programmer nor a WaveMetrics programmer, it will be of no interest.

ParseOperationTemplate generates starter code for programmers who are creating Igor operations. The starter code is copied to the clipboard, overwriting any previous clipboard contents.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C = *c*</span> | If *c* is nonzero, ParseOperationTemplate stores code for your ExecuteOperation and RegisterOperation functions in the clipboard. |
|  |<table class="nested-table"><tbody><tr><td>*c*&nbsp;=0:</td><td>Do not generate code</td></tr><tr><td>*c*&nbsp;=1:</td><td>Generate simplified C code - not recommended</td></tr><tr><td>*c*&nbsp;=2:</td><td>Generate C code</td></tr><tr><td>*c*&nbsp;=6:</td><td>Generate C++ code</td></tr></tbody></table>
|  | The only difference between /C=6 and /C=2 is that the ExecuteOperation function is declared as extern "C" instead of static. C++ files that use static work fine although extern "C" is correct. |
| <span class="table-cell-nowrap">/S = *s*</span> | Stores a definition of your runtime parameter structure in the clipboard if *s* is nonzero. |
|  |<table class="nested-table"><tbody><tr><td>*s*&nbsp;=0:</td><td>Do not generate the runtime parameter structure</td></tr><tr><td>*s*&nbsp;=1:</td><td>Use your mnemonic names - recommended</td></tr><tr><td>*s*&nbsp;=2:</td><td>Automatically generate mnemonic names - not recommended</td></tr></tbody></table>
|  | We recommend that you use /S=1 and provide unique mnemonic parameter names in your template. ParseOperationTemplate then uses your parameter names as structure field names. |
|  | If you use /S=2, ParseOperationTemplate creates unique field names by concatenating flag or keyword text and your mnemonic names. This is left over from the early days of Operation Handler and is not recommended. |
| <span class="table-cell-nowrap">/T</span> | Stores a comment listing your command template in the clipboard. |
| <span class="table-cell-nowrap">/TS</span> | Identifies a ThreadSafe operation by adding an extra field to the runtime parameter structure. This is only of use to WaveMetrics programmers. |

### *Parameters* {#parameters}
*cmdTemplate* is the template that describes the syntax for your operation. See the Igor XOP Toolkit's Reference Manual for details.

### *Details* {#details}
ParseOperationTemplate parses your command template, generating structures that embody the syntax of your operation. It then uses these structures to generate code that can serve as a starting point for implementing your operation. The starter code is stored in the clipboard.

For most uses, the recommended flags are:


```igor
/T/S=1/C=6			// For non-threadsafe operations
/T/S=1/C=6/TS		// For threadsafe operations
```

ParseOperationTemplate sets the following output variable, but only when called from a function or macro:


|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>*cmdTemplate* was successfully parsed.</td></tr><tr><td>-1:</td><td>*cmdTemplate* was not successfully parsed.</td></tr></tbody></table>

If V_flag is nonzero, this indicates that your *cmdTemplate* syntax is incorrect. See the Igor XOP Toolkit's Reference Manual for details.

### *Examples* {#examples}

```igor
Function Test()
	String cmdTemplate
	cmdTemplate = "MyTest"
	cmdTemplate += " /A={number:aNum1,string:aStrH}"
	cmdTemplate += " /B=wave:bWaveH"
	cmdTemplate += " key1={name:key1Name1[,wave:key1WaveH,name:key1Name2,string[2]:key1StrHArray]}"

	// If your XOP is C instead of C++, use /C=2 instead of /C=6
	ParseOperationTemplate/T/S=1/C=6 cmdTemplate
	Print V_flag
End
```

### *See Also* {#see-also}
[Igor Extensions](/igorpro/igor-basics/using-igor.md#igor-extensions)