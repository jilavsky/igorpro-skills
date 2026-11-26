---
description: "The ContourNameToWaveRef function returns a wave reference to the wave corresponding to the given contour name in the graph window or subwindow named by…"
slug: /commands/contournametowaveref
---

<div className="command-signature">

## <strong>ContourNameToWaveRef</strong> (<em>graphNameStr</em>, <em>contourNameStr</em>) {#contournametowaveref}

</div>

The ContourNameToWaveRef function returns a wave reference to the wave corresponding to the given contour name in the graph window or subwindow named by *graphNameStr*.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The contour name is identified by the string in *contourNameStr*, which could be a string determined using ContourNameList. Note that the same contour name can refer to different waves in different graphs.

### *See Also* {#see-also}
[ContourNameList](/igorpro/commands/contournamelist.md)