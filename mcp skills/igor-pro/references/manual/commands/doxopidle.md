---
description: "The DoXOPIdle operation sends an IDLE event to all open XOPs. This operation is very specialized and unusual."
slug: /commands/doxopidle
---

<div className="command-signature">

## <strong>DoXOPIdle</strong> {#doxopidle}

</div>

The DoXOPIdle operation sends an IDLE event to all open XOPs. This operation is very specialized and unusual. Generally, only the author of an XOP will need to use this operation.

### *Details* {#details}
Some XOPs (External OPeration code modules) require IDLE events in order to perform certain tasks.

Igor does not automatically send IDLE events to XOPs while an Igor program is running. You can call DoXOPIdle from a user-defined program to force Igor to send the event.