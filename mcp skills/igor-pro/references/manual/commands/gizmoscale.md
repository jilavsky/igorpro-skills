---
description: "The GizmoScale function returns a scaled dataValue for the specified dimension."
slug: /commands/gizmoscale
---

<div className="command-signature">

## <strong>GizmoScale</strong> (<em>dataValue</em>, <em>dimNumber</em> [, <em>gizmoNameStr</em>]) {#gizmoscale}

</div>

The GizmoScale function returns a scaled *dataValue* for the specified dimension.  The scaled values are used to position non-data drawing objects in the Gizmo window.

### *Parameters* {#parameters}
*dataValue* is the data value to be scaled.

*dimNumber* is 0 for the x-direction, 1 for the y-direction and 2 for the z-direction.

*gizmoNameStr* is the name of the Gizmo window. If you omit it the function returns the scaled value for the top Gizmo window.

*gizmoNameStr* may be a subwindow path. See [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the path to a subwindow.

The GizmoScale function was added in Igor Pro 7.00.

### *Details* {#details}
By default, Gizmo scales all the data it displays to the +/-1 cube.  This means that the global minima along any axis, for all the items on the display list, are scaled to -1 and the global maxima are scaled to +1 on the corresponding plot axes.

Non-data Gizmo objects are specified in scaled coordinates so if, for example, you want to draw a quad object parallel to the XY plane at a z=z0, you need to be able to scale z0.  To do so execute:


```igor
Print GizmoScale(z0,2)
```

### *See Also* {#see-also}
[GetGizmo](/igorpro/commands/getgizmo.md), [ModifyGizmo](/igorpro/commands/modifygizmo.md), [3D Graphics](/igorpro/graphing/3d-graphics.md)