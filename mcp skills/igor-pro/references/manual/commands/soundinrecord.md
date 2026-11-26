---
description: "The SoundInRecord operation records audio input at the sample rate obtained from the wave's X scaling and for the number of points determined by the length of…"
slug: /commands/soundinrecord
---

<div className="command-signature">

## <strong>SoundInRecord</strong>  [/BITS=<em>bits</em> /Z] <em>wave</em> {#soundinrecord}

</div>

The SoundInRecord operation records audio input at the sample rate obtained from the wave's X scaling and for the number of points determined by the length of the wave. The recording is done synchronously.

The number type of the wave must be a type supported by the sound input hardware as reported by the [SoundInStatus](/igorpro/commands/soundinstatus.md) operation. Use SoundInStatus with the format keyword to check if a particular format is supported.

8-bit or 16-bit integer are typically supported.

To record in stereo, provide a 2 column wave. (The software is designed to handle any number of channels but has not been tested on more than 2.)

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/BITS = *bits*</span> | Controls the number of bits used for each recorded sound sample. |
|  | Use /BITS=24 with a 32-bit integer wave for 24-bit sound data capable of representing values from -8,388,608 to +8,388,607. |
|  | If you omit /BITS or use /BITS=0, SoundInRecord uses the wave's data type and size to determine how many bits are recorded for each sound sample. |
|  | The /BITS flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/Z</span> | Prevents errors from being fatal. V_flag is set to zero if no error, else nonzero if error. |

### *Details* {#details}
This operation requires a computer equipped with sound input hardware. Several sample experiments involving sound input can be found in your Igor Pro Folder in the Examples folder.

### *See Also* {#see-also}
[SoundInStatus](/igorpro/commands/soundinstatus.md), [SoundInSet](/igorpro/commands/soundinset.md), [SoundInStartChart](/igorpro/commands/soundinstartchart.md)

### *Demos* {#demos}
[Open Audio Snarfer Demo](#igor-pxp/Examples/Movies__&__Audio/Sound__Input/Audio__Snarfer.pxp)

[Open Sound Chart Demo](#igor-pxp/Examples/Movies__&__Audio/Sound__Input/Sound__Chart__Demo.pxp)

[Open Sound System Eval Demo](#igor-pxp/Examples/Movies__&__Audio/Sound__Input/Sound__System__Eval.pxp)