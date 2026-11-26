---
description: "The FSetPos operation attempts to set the current file position to the given position."
slug: /commands/fsetpos
---

<div className="command-signature">

## <strong>FSetPos</strong>  <em>refNum</em>, <em>filePos</em> {#fsetpos}

</div>

The FSetPos operation attempts to set the current file position to the given position.

### *Parameters* {#parameters}
*refNum* is a file reference number obtained from the [Open](/igorpro/commands/open.md) operation when the file was opened.

*filePos* is the desired position of the file in bytes from the start of the file.

### *Details* {#details}
FSetPos generates an error if *filePos* is greater than the number of bytes in the file. You can ascertain this limit with the FStatus operation.

When a file that is open for writing is closed, any bytes past the end of the current file position are deleted by the operating system. Therefore, if you use FSetPos, make sure to set the current file position properly before closing the file.

FSetPos supports files of any length.

### *See Also* {#see-also}
[Open](/igorpro/commands/open.md), [FGetPos](/igorpro/commands/fgetpos.md), [FStatus](/igorpro/commands/fstatus.md)