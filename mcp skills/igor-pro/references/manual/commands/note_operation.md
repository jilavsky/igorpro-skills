---
description: "The Note operation appends str to the wave note for the named wave. str is a string expression."
slug: /commands/note_operation
title: "Note"
---

<div className="command-signature">

## <strong>Note</strong>  [/K/NOCR] <em>waveName</em> [, <em>str</em> ] {#note}

</div>

The Note operation appends str  to the wave note for the named wave.

### *Parameters* {#parameters}

*str* is a string expression.

### *Flags* {#flags}
|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/K</span> | Kills existing note for specified wave. |
| <span class="table-cell-nowrap">/NOCR</span> | Appends note without a preceding carriage return (\\r character). No effect when used with /K. |

### *Examples* {#examples}

```igor
Note/K wave0		// remove existing note
Note wave0, "This is the first line of the note"
Note wave0, "This is the second line of the note"
Note/K wave0, "This is now the only line of the note"
```

### *See Also* {#see-also}
To get the contents of a wave note, use [Functions[note]](/igorpro/commands/note_function.md).