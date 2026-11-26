---
description: "The NewFIFO operation creates a new FIFO. Useless until channel info is added with NewFIFOChan."
slug: /commands/newfifo
---

<div className="command-signature">

## <strong>NewFIFO</strong>  <em>FIFOName</em> {#newfifo}

</div>

The NewFIFO operation creates a new FIFO.

### *Details* {#details}
Useless until channel info is added with [NewFIFOChan](/igorpro/commands/newfifochan.md).

An error is generated if a FIFO of same name already exists. *FIFOName* needs to be unique only among FIFOs. You cannot overwrite a FIFO.

### *See Also* {#see-also}
[FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)

### *Demos* {#demos}
[Open FIFO Chart Demo](#igor-pxp/Examples/Feature__Demos/FIFO__Chart__Demo__FM.pxp)

[Open FIFO File Parse Demo](#igor-pxp/Examples/Programming/FIFO__File__Parse.pxp)