---
description: "The ImageNameToWaveRef function returns a wave reference to the 2D wave corresponding to the given image name in the graph window or subwindow named by…"
slug: /commands/imagenametowaveref
---

<div className="command-signature">

## <strong>ImageNameToWaveRef</strong> (<em>graphNameStr</em>, <em>imageNameStr</em>) {#imagenametowaveref}

</div>

The ImageNameToWaveRef function returns a wave reference to the 2D wave corresponding to the given image name in the graph window or subwindow named by *graphNameStr*.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

The image is identified by the string in *imageNameStr*, which could be a string determined using ImageNameList. Note that the same image name can refer to different waves in different graphs.

### *See Also* {#see-also}
[ImageNameList](/igorpro/commands/imagenamelist.md)