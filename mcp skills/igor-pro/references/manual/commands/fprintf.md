---
description: "The fprintf operation prints formatted output to a text file. refNum is a file reference number from the Open operation used to create the file."
slug: /commands/fprintf
---

<div className="command-signature">

## <strong>fprintf</strong>  <em>refNum</em>,<em>formatStr</em>  [, <em>parameter</em>]... {#fprintf}

</div>

The fprintf operation prints formatted output to a text file.

### *Parameters* {#parameters}
*refNum* is a file reference number from the Open operation used to create the file.

*formatStr* is the format string, as used by the printf operation.

*parameter* varies depending on *formatStr*.

### *Details* {#details}
If *refNum* is 1, Igor will print to the history area instead of to a file, as if you used printf instead of fprintf. This is provided for debugging purposes.

A zero value of *refNum*  is used in conjunction with [ActiveX Automation](/igorpro/advanced-topics.md#activex-automation). The data that would normally be written to a file is appended to the ActiveX Automation result packet.

The fprintf operation supports numeric (real only) and string fields from structures. All other structure field types cause a compile error.

### *Output to Standard Streams* {#output-to-standard-streams}
If *refNum* is -1, Igor prints to the standard output stream (stdout).

If *refNum* is -2, Igor prints to the standard error stream (stderr).

This feature was added in Igor Pro 8.00. It is useful primarily when you launch Igor from a custom application. The application may be able to capture Igor's standard stream output.

stdout and stderr output is not visible even if Igor is started from the command line.

### *See Also* {#see-also}
The [printf](/igorpro/commands/printf.md) operation for complete format and parameter descriptions and [Creating Formatted Text](/igorpro/advanced-topics.md#creating-formatted-text) in the Advanced Topics help file. Also see [Open](/igorpro/commands/open.md) about files.