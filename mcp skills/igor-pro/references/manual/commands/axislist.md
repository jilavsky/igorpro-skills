---
description: "The AxisList function returns a semicolon-separated list of axis names from the named graph window or subwindow."
slug: /commands/axislist
---

<div className="command-signature">

## <strong>AxisList</strong> (<em>graphNameStr</em>) {#axislist}

</div>

The AxisList function returns a semicolon-separated list of axis names from the named graph window or subwindow.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

### *Examples* {#examples}

```igor
Make/O data=x;Display/L/T data
Print AxisList("")		// prints  left;top;
```