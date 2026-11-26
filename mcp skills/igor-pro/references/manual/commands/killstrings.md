---
description: "The KillStrings operation discards the named global strings."
slug: /commands/killstrings
---

<div className="command-signature">

## <strong>KillStrings</strong>  [/A/Z] [<em>stringName</em> [, <em>stringName</em> ]...] {#killstrings}

</div>

The KillStrings operation discards the named global strings.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Kill all global strings in the current data folder. If you use /A, omit *stringName*. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate an error if a global string to be killed does not exist. To kill all global strings in the current data folder, use KillStrings/A/Z. |