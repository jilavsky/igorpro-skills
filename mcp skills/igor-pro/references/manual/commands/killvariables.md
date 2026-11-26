---
description: "The KillVariables operation discards the named global numeric variables."
slug: /commands/killvariables
---

<div className="command-signature">

## <strong>KillVariables</strong>  [/A/Z] [<em>variableName</em> [, <em>variableName</em> ]...] {#killvariables}

</div>

The KillVariables operation discards the named global numeric variables.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Kill all global variables in the current data folder. If you use /A, omit *variableName*. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate an error if a global variable to be killed does not exist. To kill all global variables in the current data folder, use KillVariables/A/Z. |