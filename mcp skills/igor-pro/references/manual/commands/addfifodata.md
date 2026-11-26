---
description: "The AddFIFOData operation evaluates FIFO_channelExpr expressions as double precision floating point and places values into the named FIFO."
slug: /commands/addfifodata
---

<div className="command-signature">

## <strong>AddFIFOData</strong>  <em>FIFOName</em>, <em>FIFO_channelExpr</em> [, <em>FIFO_channelExpr</em> ]... {#addfifodata}

</div>

The AddFIFOData operation evaluates *FIFO_channelExpr*  expressions as double precision floating point and places values into the named FIFO.

### *Details* {#details}
There must be one *FIFO_channelExpr*  for each channel in the FIFO.

FIFOs are used for data acquisition.

### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)