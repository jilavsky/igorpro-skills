---
description: "The FGetPos operation returns the file position for a file. FGetPos is a faster alternative to FStatus if the only thing you are interested in is the file…"
slug: /commands/fgetpos
---

<div className="command-signature">

## <strong>FGetPos</strong>  <em>refNum</em> {#fgetpos}

</div>

The FGetPos operation returns the file position for a file.

FGetPos is a faster alternative to FStatus if the only thing you are interested in is the file position.

The FGetPos operation was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*refNum*  is a file reference number obtained from the [Open](/igorpro/commands/open.md) operation.

### *Details* {#details}
FGetPos supports very big files theoretically up to about 4.5E15 bytes in length.

FGetPos sets the following variables:


|  |  |
| --- | --- |
| V_flag | Nonzero (true) if *refNum*  is valid. |
| V_filePos | Current file position for the file in bytes from the start. |

### *See Also* {#see-also}
[Open](/igorpro/commands/open.md), [FSetPos](/igorpro/commands/fsetpos.md), [FStatus](/igorpro/commands/fstatus.md)