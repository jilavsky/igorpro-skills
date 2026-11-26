---
description: "The DefineGuide operation creates or overwrites a user-defined guide line in the target or named window or subwindow."
slug: /commands/defineguide
---

<div className="command-signature">

## <strong>DefineGuide</strong>  [/W=<em>winName</em> ] <em>newGuideName</em> = {[<em>guideName1</em>, <em>val</em>  [, <em>guideName2</em> ]]} [, ...] {#defineguide}

</div>

The DefineGuide operation creates or overwrites a user-defined guide line in the target or named window or subwindow. Guide lines help with the positioning of subwindows in a host window.

### *Parameters* {#parameters}
*newGuideName* is the name for the newly created guide. When it is the name of an existing user-defined guide, the guide will be moved to the new position.

*guideName1*, *guideName2*, etc., must be the names of existing guides.

The meaning of *val* depends on the form of the command syntax. When using only one guide name, *val*  is an offset relative to the guide. The directionality of *val* is to the right or below the guide for positive values. The units of measure are points except in panels where they are [control panel units](/igorpro/user-interface/controls.md#control-panel-units). When using two guide names, *val* is the fractional distance between the two guides.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Affects guides in the named window or subwindow. When omitted, action will affect the active window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The names for the built-in guides are as defined in the following table:

| Guide Names | Left | Right | Top | Bottom |
| --- | --- | --- | --- | --- |
| Subwindow Frame | FL | FR | FT | FB |
| Outer Graph Rectangle | GL | GR | GT | GB |
| Inner Plot Rectangle | PL | PR | PT | PB |
| Layout Margin Rectangle | ML | MR | MT | MB |

The frame guides apply to all window and subwindow types. The graph rectangle and plot rectangle guide types apply only to graph windows and subwindows. The layout margin rectangle guide types only apply to layout windows.

To delete a guide, use *GuideName*={}.

### *See Also* {#see-also}
[Display](/igorpro/commands/display.md), [Edit](/igorpro/commands/edit.md), [NewPanel](/igorpro/commands/newpanel.md), [NewImage](/igorpro/commands/newimage.md), [NewWaterfall](/igorpro/commands/newwaterfall.md), [GuideInfo](/igorpro/commands/guideinfo.md)