---
description: "The NewFreeAxis operation creates a new free axis with no controlling wave."
slug: /commands/newfreeaxis
---

<div className="command-signature">

## <strong>NewFreeAxis</strong>  [/L/R/B/T/O/W=<em>winName</em> ] <em>axisName</em> {#newfreeaxis}

</div>

The NewFreeAxis operation creates a new free axis with no controlling wave.

### *Parameters* {#parameters}
*axisName* is the name for the new free axis.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/L/R/B/T</span> | Specifies whether to attach the free axis to the Left, Right, Bottom, or Top plot edge, respectively. The Left edge is used by default. |
| <span class="table-cell-nowrap">/O</span> | Replaces *axisName* if it already exists, which means any existing axis is marked as truly free. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Draws in the named graph window. *winName* may also be the name of a subwindow. *winName* must not conflict with other axis names except when using the /O flag. If /W is omitted, it creates a new axis in the active graph window or subwindow. |

### *Details* {#details}
A truly free axis does not use any scaling or units information from any associated waves (which need not exist.) You can set the properties of a free axis using [SetAxis](/igorpro/commands/setaxis.md) or [ModifyFreeAxis](/igorpro/commands/modifyfreeaxis.md).

### *Example* {#example}

```igor
Make jack=x
Display jack
NewFreeAxis fred
ModifyFreeAxis fred, master=left, hook=axhook
```

Copy this function to your Procedure window and compile before executing the code above:


```igor
Function axhook(s)
	STRUCT WMAxisHookStruct &s

	Variable t= s.max
	s.max= s.min
	s.min= t
	return 0
End
```

### *See Also* {#see-also}
The [SetAxis](/igorpro/commands/setaxis.md), [KillFreeAxis](/igorpro/commands/killfreeaxis.md), [ModifyFreeAxis](/igorpro/commands/modifyfreeaxis.md)