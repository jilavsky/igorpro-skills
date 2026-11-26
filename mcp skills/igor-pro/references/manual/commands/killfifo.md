---
description: "The KillFIFO operation discards the named FIFO. FIFOs are used for data acquisition."
slug: /commands/killfifo
---

<div className="command-signature">

## <strong>KillFIFO</strong>  <em>FIFOName</em> {#killfifo}

</div>

The KillFIFO operation discards the named FIFO.

### *Details* {#details}
FIFOs are used for data acquisition.

If there is an output or review file associated with the FIFO, KillFIFO closes the file. If the FIFO is used by an XOP, you should call the XOP to release the FIFO before killing it.

### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)