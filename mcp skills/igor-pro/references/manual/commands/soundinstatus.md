---
description: "The SoundInStatus operation creates and sets a set of variables and strings with information about the current sound input device."
slug: /commands/soundinstatus
---

<div className="command-signature">

## <strong>SoundInStatus</strong>  [ <em>format</em>={<em>intOrFloat</em>, <em>channels</em>, <em>bits</em>, <em>frequency</em>} ] {#soundinstatus}

</div>

The SoundInStatus operation creates and sets a set of variables and strings with information about the current sound input device.

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">format = {*intOrFloat*, *channels*, *bits*, *frequency*}</span> |  |
|  | Checks if a specific sound input format is supported. This is useful because it is often the case that more sound input formats are supported than are reported via the V_SoundInSampSize and W_SoundInRates outputs. |
|  | V_Flag is set to 0 if the specified format is supported by the input device or to a non-zero error code otherwise. |
|  | The format keyword was added in Igor Pro 9.00. |
|  | *intOrFloat* is a keyword (unquoted), either int or float. |
|  | *channels* is 1 for mono, 2 for stereo. Additional channels may also work with some sound hardware. |
|  | *bits* may be any value between 8 and 64, though 8, 16, 24, and 32 are most likely to be supported by the operating system. CD audio samples use 16 bits. |
|  | *frequency* is the sampling rate in Hertz, with a minimum of 4800. CD audio is sampled at 44100 Hz. A practical upper limit is 192000. |

### *Outputs* {#outputs}

|  |  |
| --- | --- |
| V_Flag | Set to 0 if the device is available or to a non-zero error code. |
|  | Also, if you use the format keyword and the specified format is not supported then V_Flag is set to a non-zero error code. |
|  | If V_Flag is non-zero then none of the following outputs are valid. |
| S_SoundInName | String with name of device. |
| V_SoundInAGC | Automatic gain control on or off (1 or 0). This is an optional item and if the current device does not support AGC then V_SoundInAGC will be set to -1. |
| V_SoundInChansAv | Available number of channels (e.g., 1 for mono, 2 for stereo). |
| V_SoundInGain | Current input gain. Ranges from 0 (lowest) to 1. This is an optional item and if the current device does not support gain then V_SoundInGain will be set to -1. |
| V_SoundInSampSize | Bits set depending on number of bits available in a sample. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Set if 8-bit integer is supported.</td></tr><tr><td>Bit&nbsp;1:</td><td>Set if 16-bit integer is supported.</td></tr><tr><td>Bit&nbsp;2:</td><td>Set if 32-bit integer is supported.</td></tr><tr><td>Bit&nbsp;3:</td><td>Set if 32-bit floating point is supported (range is -1 to 1).</td></tr><tr><td>Bit&nbsp;4:</td><td>Set if 64-bit floating point is supported (range is -1 to 1).</td></tr></tbody></table>
| W_SoundInRates | Wave containing sample rate information: If point zero contains zero then points 1 and 2 contain the lower and upper limits of a continuous range else point zero contains the number of discrete rates which follow in the wave. The usual rates are 44100 Hz and 4800 Hz. |

### *See Also* {#see-also}
[SoundInSet](/igorpro/commands/soundinset.md), [SoundInRecord](/igorpro/commands/soundinrecord.md), [SoundInStartChart](/igorpro/commands/soundinstartchart.md)