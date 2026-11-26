---
description: "The KillWaves operation destroys the named waves. The memory the waves occupied becomes available for other uses."
slug: /commands/killwaves
---

<div className="command-signature">

## <strong>KillWaves</strong>  [/A/F/Z] <em>waveName</em> [, <em>waveName</em> ]... {#killwaves}

</div>

The KillWaves operation destroys the named waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Kill all waves in the current data folder. If you use /A, omit *waveName*. |
| <span class="table-cell-nowrap">/F</span> | Delete the Igor binary wave file from which *waveName*  was loaded. |
| <span class="table-cell-nowrap">/Z</span> | Doesn't generate an error if a wave to be killed is in use or does not exist. |

### *Details* {#details}
The memory the waves occupied becomes available for other uses. You can't kill a wave used in a graph or table or which is reserved by an XOP.

XOPs reserve a wave by sending the OBJINUSE message.

For functions compiled with the obsolete rtGlobals=0 setting, you also can't kill a wave referenced from a user-defined function.

### *Examples* {#examples}

```igor
KillWaves/A/Z			// kill waves not in use in the current data folder
```