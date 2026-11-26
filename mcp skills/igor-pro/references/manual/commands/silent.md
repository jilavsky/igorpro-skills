---
description: "The Silent operation is largely obsolete. Only very obscure uses remain and most users can ignore this operation."
slug: /commands/silent
---

<div className="command-signature">

## <strong>Silent</strong>  <em>num</em> {#silent}

</div>

:::warning
The Silent operation is largely obsolete. Only very obscure uses remain and most users can ignore this operation.
:::

Prior to Igor Pro 7, Silent was used to enable or disable the display of macro commands in the command line as they were executed. It was also used to enable compatibility modes for very old experiments.

### *Parameters* {#parameters}
If *num* is 2, commands issued by ActiveX Automation are not shown in the history are of the command window. Use 3 to re-enable.

If num is 100, 101 or 102, all procedures are recompiled. For 102, the time to recompile is displayed in the history.