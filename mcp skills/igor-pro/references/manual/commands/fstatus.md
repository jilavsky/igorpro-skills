---
description: "The FStatus operation provides file status information for a file. refNum is a file reference number obtained from the Open operation."
slug: /commands/fstatus
---

<div className="command-signature">

## <strong>FStatus</strong>  <em>refNum</em> {#fstatus}

</div>

The FStatus operation provides file status information for a file.

### *Parameters* {#parameters}
*refNum*  is a file reference number obtained from the [Open](/igorpro/commands/open.md) operation.

### *Details* {#details}
FStatus supports files of any length.

FStatus sets the following variables:


|  |  |
| --- | --- |
| V_flag | Nonzero (true) if *refNum* is valid, in which case FStatus sets the other variables as well. |
| V_filePos | Current file position for the file in bytes from the start. |
|  | In Igor 7 or later, if you only want to know the current file position, use FGetPos instead of FStatus, which is slower. |
| V_logEOF | Total number of bytes in the file. |
| S_fileName | (string) the name of the file. |
| S_path | Path from the volume to the folder containing the file. For example, "hd:Folder1:Folder2:". This is suitable for use as an input to the [NewPath](/igorpro/commands/newpath.md) operation. Note that on the Windows operating system, Igor uses a colon between folders instead of the Windows-standard backslash to avoid confusion with Igor's use of backslash to start an escape sequence (see [Escape Sequences in Strings](/igorpro/programming/commands.md#escape-sequences-in-strings)). |
| S_info | Keyword-packed information string. |

The keyword-packed information string for S_info consists of a sequence of sections with the following form: *keyword*:*value*; You can pick a value out of a keyword-packed string using the [NumberByKey](/igorpro/commands/numberbykey.md) and [StringByKey](/igorpro/commands/stringbykey.md) functions.

Here are the keywords for S_info:


| Keyword | Type | Meaning |
| --- | --- | --- |
| PATH | string | Name of the symbolic path in which the file is located. This will be empty if there is no such symbolic path. |
| WRITEABLE | number | 1 if file can be written to, 0 if not. |

### *See Also* {#see-also}
[Open](/igorpro/commands/open.md), [FGetPos](/igorpro/commands/fgetpos.md), [FSetPos](/igorpro/commands/fsetpos.md)