---
description: "The StartMSTimer function creates a new microsecond timer and returns a timer reference number."
slug: /commands/startmstimer
---

<div className="command-signature">

## <strong>StartMSTimer</strong> {#startmstimer}

</div>

The StartMSTimer function creates a new microsecond timer and returns a timer reference number.

### *Details* {#details}
You can create up to ten different microsecond timers using StartMSTimer. A valid timer  reference  number is a  number between 0 and 9. If StartMSTimer returns -1, there are no free timers available. StartMSTimer works in conjunction with StopMSTimer as illustrated below.

### *See Also* {#see-also}
[StopMSTimer](/igorpro/commands/stopmstimer.md), [ticks](/igorpro/commands/ticks.md), [DateTime](/igorpro/commands/datetime.md)