---
description: "SoundInSet is used to setup the input device for recording. SoundInSet can accept multiple keyword =value parameters on one line."
slug: /commands/soundinset
---

<div className="command-signature">

## <strong>SoundInSet</strong>  [/Z] [<em>gain</em>=<em>g</em>, <em>agc</em>=<em>a</em> ] {#soundinset}

</div>

SoundInSet is used to setup the input device for recording.

### *Parameters* {#parameters}
SoundInSet can accept multiple *keyword* =*value*  parameters on one line.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">agc = *a*</span> | Turns automatic gain control mode on (*a* =1) or off (*a* =0). Will generate an error if device does not support setting agc. Use SoundInStatus to check or use /Z flag to make errors nonfatal. |
|  | <div><Admonition type="note"><p>This is not supported and V_SoundInAGC from the SoundInStatus command always returns -1.</p></Admonition></div> |
| <span class="table-cell-nowrap">gain = *g*</span> | Sets input gain, 0 is lowest gain and 1 is highest. Will generate an error if device does not support setting gain. Use SoundInStatus to check or use /Z flag to make errors nonfatal. |
|  | <div><Admonition type="note"><p>SoundInSet attempts to adjust the master gain of the sound input device but not all sound cards have a master gain. If V_SoundInGain from the SoundInStatus command returns -1, you will have to use your sound card software to adjust the input gain for the particular input source your are using. On some cards there are separate line-in and microphone-in sources.</p></Admonition></div> |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents errors from being fatal. V_flag is set to zero if no error, else nonzero if error. |

### *Details* {#details}
SoundInSet requires a computer with sound inputs. Several sample experiments using sound inputs are in your Igor Pro Folder in the Examples folder.

### *See Also* {#see-also}
[SoundInStatus](/igorpro/commands/soundinstatus.md), [SoundInRecord](/igorpro/commands/soundinrecord.md), [SoundInStartChart](/igorpro/commands/soundinstartchart.md)