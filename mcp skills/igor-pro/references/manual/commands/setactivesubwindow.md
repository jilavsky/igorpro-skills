---
description: "The SetActiveSubwindow operation specifies the subwindow that is to be activated. This operation is mainly for use by recreation macros."
slug: /commands/setactivesubwindow
---

<div className="command-signature">

## <strong>SetActiveSubwindow</strong>  <em>subWinSpec</em> {#setactivesubwindow}

</div>

The SetActiveSubwindow operation specifies the subwindow that is to be activated. This operation is mainly for use by recreation macros.

### *Parameters* {#parameters}
*subWinSpec* specifies an existing subwindow. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on subwindow specifications.

Use \_endfloat\_ for *subWinSpec* to make a newly-created floating panel not be the default target.

### *See Also* {#see-also}
[GetWindow](/igorpro/commands/getwindow.md) with the activeSW keyword