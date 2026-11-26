---
description: "Stops audio data acquisition started by SoundInStartChart. This operation requires a computer equipped with sound input hardware."
slug: /commands/soundinstopchart
---

<div className="command-signature">

## <strong>SoundInStopChart</strong>  [/Z] {#soundinstopchart}

</div>

Stops audio data acquisition started by SoundInStartChart.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents errors from being fatal. V_flag is set to zero if no error, else nonzero if error. |

### *Details* {#details}
This operation requires a computer equipped with sound input hardware.

Audio data acquisition also stops automatically when an experiment is closed.

### *See Also* {#see-also}
[SoundInStatus](/igorpro/commands/soundinstatus.md), [SoundInStartChart](/igorpro/commands/soundinstartchart.md)