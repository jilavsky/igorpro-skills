---
description: "The Close operation closes a file previously opened by the Open operation or closes all such files, if /A is used."
slug: /commands/close
---

<div className="command-signature">

## <strong>Close</strong>  [/A] [<em>fileRefNum</em> ] {#close}

</div>

The Close operation closes a file previously opened by the Open operation or closes all such files, if /A is used.

### *Parameters* {#parameters}
*fileRefNum*  is the file reference number of the file to close. This number comes from the Open operation. If /A is used, *fileRefNum*  should be omitted.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Closes all files. Mainly useful for cleaning up after an error during procedure execution occurs so that the normal Close operation is never executed. |

### *See Also* {#see-also}
[Open](/igorpro/commands/open.md)