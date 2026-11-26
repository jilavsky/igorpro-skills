---
description: "The CopyScales operation copies the x, y, z, and t scaling, x, y, z, and t units, the data Full Scale and data units from srcWaveName to the other waves."
slug: /commands/copyscales
---

<div className="command-signature">

## <strong>CopyScales</strong>  [/I/P] <em>srcWaveName</em>, <em>waveName</em> [, <em>waveName</em> ]... {#copyscales}

</div>

The CopyScales operation copies the x, y, z, and t scaling, x, y, z, and t units, the data Full Scale and data units from *srcWaveName* to the other waves.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/I</span> | Copies the x, y, z, and t scaling in inclusive format. |
| <span class="table-cell-nowrap">/P</span> | Copies the x, y, z, and t scaling in slope/intercept format (x<sub>0</sub>, delta x format). |

### *Details* {#details}
Normally the x, y, z, and t (dimension) scaling is copied in min/max format. However, if you use /P, the dimension scaling is copied in slope/intercept format so that if *srcWaveName*  and the other waves have differing dimension size (number of points if the wave is a 1D wave), then their dimension values will still match for the points they have in common. Similarly, /I uses the inclusive variant of the min/max format. See [SetScale](/igorpro/commands/setscale.md) for a discussion of these dimension scaling formats.

If a wave has only one point, /I mode reverts to /P mode.

CopyScales copies scales only for the dimensions that *srcWaveName* and *waveName* have in common.