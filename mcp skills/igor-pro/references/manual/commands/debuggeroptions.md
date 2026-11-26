---
description: "The DebuggerOptions operation programmatically changes the user-level debugger settings."
slug: /commands/debuggeroptions
---

<div className="command-signature">

## <strong>DebuggerOptions</strong>  [<em>enable</em>=<em>en</em>, <em>debugOnAbort</em>=<em>doa</em>, <em>debugOnError</em>=<em>doe</em>, <em>NVAR_SVAR_WAVE_Checking</em>=<em>nvwc</em>] {#debuggeroptions}

</div>

The DebuggerOptions operation programmatically changes the user-level debugger settings. These are the same three settings that are available in the Procedure menu (and the debugger source pane contextual menu).

### *Parameters* {#parameters}
All parameters are optional. If none are specified, no action is taken, but the output variables are still set.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">enable = *en*</span> | Turns the debugger on or off. |
|  |<table class="nested-table"><tbody><tr><td>*en*&nbsp;=&nbsp;0:</td><td>Disables the debugger</td></tr><tr><td>*en*&nbsp;=&nbsp;1:</td><td>Enables the debugger.</td></tr></tbody></table>
|  | If the debugger is disabled then the other settings are cleared even if other settings are on. |
| <span class="table-cell-nowrap">debugOnAbort = *doa*</span> | Turns Debugging On User Abort on or off. |
|  |<table class="nested-table"><tbody><tr><td>*doa*&nbsp;=&nbsp;0:</td><td>Disables Debug On Abort.</td></tr><tr><td>*doa*&nbsp;=&nbsp;1:</td><td>Enables Debug On Abort and also enables the debugger (implies enable=1).</td></tr></tbody></table>
|  | The Debug on User Abort feature was added in Igor Pro 9.00. See [Debugging On User Abort](/igorpro/programming/debugging.md#debugging-on-user-abort) for details. |
| <span class="table-cell-nowrap">debugOnError = *doe*</span> | Turns Debugging On Error on or off. |
|  |<table class="nested-table"><tbody><tr><td>*doe*&nbsp;=&nbsp;0:</td><td>Disables [Debugging On Error](/igorpro/programming/debugging.md#debugging-on-error).</td></tr><tr><td>*doe*&nbsp;=1:</td><td>Enables Debugging On Error and also enables the debugger (implies enable=1).</td></tr></tbody></table>
| <span class="table-cell-nowrap">NVAR_SVAR_WAVE_Checking = *nvwc*</span> |  |
|  | Turns NVAR, SVAR, and WAVE checking on or off. |
|  |<table class="nested-table"><tbody><tr><td>*nvwc*&nbsp;=&nbsp;0:</td><td>Disables &quot;NVAR SVAR WAVE Checking&quot;. See [Accessing Global Variables and Waves](/igorpro/programming/programming.md#accessing-global-variables-and-waves) for details.</td></tr><tr><td>*nvwc*&nbsp;=&nbsp;1:</td><td>Enables this checking and also enables the debugger (implies enable=1).</td></tr></tbody></table>

### *Output Variables* {#output-variables}
DebuggerOptions sets the following variables to indicate the Debugger settings that are in effect *after* the command is executed. A value of zero means the setting is off, nonzero means the setting is on.

`V_enable`, `V_debugOnError`, `V_debugOnAbort`, `V_NVAR_SVAR_WAVE_Checking`

### *See Also* {#see-also}
[The Debugger](/igorpro/programming/debugging.md#the-debugger), [Debugger](/igorpro/commands/debugger.md)