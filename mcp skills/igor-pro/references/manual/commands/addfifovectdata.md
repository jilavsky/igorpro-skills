---
description: "The AddFIFOVectData operation is similar to AddFIFOData except the expressions use a keyword to allow either a single numeric value for a normal channel or a…"
slug: /commands/addfifovectdata
---

<div className="command-signature">

## <strong>AddFIFOVectData</strong>  <em>FIFOName</em>, <em>FIFO_channelKeyExpr</em> [, <em>FIFO_channelKeyExpr</em> ]... {#addfifovectdata}

</div>

The AddFIFOVectData operation is similar to AddFIFOData except the expressions use a keyword to allow either a single numeric value for a normal channel or a wave containing the data for a special image vector channel.

### *Details* {#details}
There must be one *FIFO_channelKeyExpr*  for each channel in the FIFO.

A *FIFO_channelKeyExpr* may be one of:

- num= *numericExpression*
- vect= *wave*

For best results, the wave should have the same number of points as used to define the FIFO channel and the same number type. See [NewFIFOChan](/igorpro/commands/newfifochan.md).

### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)