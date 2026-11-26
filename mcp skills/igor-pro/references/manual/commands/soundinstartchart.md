---
description: "Starts audio data acquisition into the given FIFO. buffersize is the number of bytes to allocate for the interrupt time buffer which then feeds into the given…"
slug: /commands/soundinstartchart
---

<div className="command-signature">

## <strong>SoundInStartChart</strong>  [/Z] <em>buffersize</em> , <em>destFIFOname</em> {#soundinstartchart}

</div>

Starts audio data acquisition into the given FIFO.

### *Parameters* {#parameters}
*buffersize*  is the number of bytes to allocate for the interrupt time buffer which then feeds into the given Igor named FIFO *destFIFOname*. The FIFO must be set up with the correct number of channels and number type - use [SoundInStatus](/igorpro/commands/soundinstatus.md) to find legal values. The sample rate is read from the FIFO also, so that also needs to be correct.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Prevents errors from being fatal. V_flag is set to zero if no error, else nonzero if error. |

### *Details* {#details}
SoundInStartChart requires a computer with sound inputs. Several sample experiments using sound inputs are in your Igor Pro Folder in the Examples folder.

On systems where 32-bit floating point data is supported, you can use NewFIFOChan with no flags and a range of -1 to 1.

### *See Also* {#see-also}
[SoundInStatus](/igorpro/commands/soundinstatus.md), [SoundInRecord](/igorpro/commands/soundinrecord.md), [SoundInStopChart](/igorpro/commands/soundinstopchart.md), [SoundInSet](/igorpro/commands/soundinset.md), [FIFOs and Charts](/igorpro/advanced-topics.md#fifos-and-charts)