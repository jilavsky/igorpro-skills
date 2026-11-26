---
description: "StructFill is a programmer-convenience operation that initializes NVAR, SVAR and WAVE fields in a structure."
slug: /commands/structfill
---

<div className="command-signature">

## <strong>StructFill</strong>  [ /AC=<em>createFlags</em> /SDFR=<em>dfr</em> ] <em>structVar</em> {#structfill}

</div>

StructFill is a programmer-convenience operation that initializes NVAR, SVAR and WAVE fields in a structure. At run time, it scans through the fields in the specified structure and attempts to set all null NVAR, SVAR and WAVE fields by looking up corresponding same-named globals in the current data folder or in the specified data folder.

StructFill was added in Igor Pro 8.00.

### *Parameters* {#parameters}
*structVar* is the name of a STRUCT variable.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AC = *createFlags*</span> |  |
|  | Enables auto-creation of globals. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Enables creation of numeric and string global variables which are set to 0 and &quot;&quot; respectively. Variables are auto-created only if they do not already exist.</td></tr><tr><td>Bit&nbsp;1:</td><td>Enables creation of waves which are created with zero points. Waves are auto-created only if they do not already exist.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/SDFR = *dfr*</span> | Specifies a data folder. If you omit /SDFR, the current data folder used. |
|  | See [The /SDFR Flag](/igorpro/programming/programming.md#the-sdfr-flag) for details. |

### *Output Variables* {#output-variables}
StructFill sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | The number of NVAR, SVAR and WAVE fields that were successfully initialized. |
| V_Error | The number of NVAR, SVAR and WAVE fields that could not be initialized. |

If auto-creation is off, a field cannot be initialized if the corresponding global variable, string variable, or wave does not exist. If auto-creation is on, a field cannot be initialized if there was an error creating the global variable or wave.

When using auto-creation, errors are not reported other than via V_Error.

If you unexpectedly get non-zero for V_Error, you can print the structure to see which fields were left null.

### *See Also* {#see-also}
[Structures in Functions](/igorpro/programming/programming.md#structures-in-functions)