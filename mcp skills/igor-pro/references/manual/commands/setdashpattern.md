---
description: "The SetDashPattern operation defines a dashed-line pattern for a user-defined dashed line."
slug: /commands/setdashpattern
---

<div className="command-signature">

## <strong>SetDashPattern</strong>  <em>dashNumber</em>, {<em>d1</em>,<em>s1</em> [,<em>d2</em>,<em>s2</em> ]...} {#setdashpattern}

</div>

The SetDashPattern operation defines a dashed-line pattern for a user-defined dashed line. These dashed lines are used by the drawing tools and the Modify Trace Appearance dialog, and are elsewhere referred to as "line styles".

### *Parameters* {#parameters}
*dashNumber* specifies which dash pattern is to be set. It must be between 1 and 17. Dash pattern 0 is reserved for a solid line.

<img src="Images/SetDashPattern/SetDashPattern_2.png" width="85%"/><img src="Images/SetDashPattern/SetDashPattern_3.png" width="85%"/>

{*d1*,*s1* [,*d2*,*s2* ]...} defines the dash pattern. The dash pattern consists of 1 to 8 "dash,skip" pairs. Each pair consists of the number of drawn points followed by the number of skipped points.

*d1* specifies the number of drawn points and *s1* specifies the number of skipped points in the first "dash,skip" pair. *d2* and *s2* specify the number of drawn and skipped points in the second pair and so on. Each draw or skip value must be between 1 and 127.

### *Details* {#details}
SetDashPattern updates ***all*** graphs, panels and layouts so that any dashed lines will be updated with the new pattern. If you repeatedly call SetDashPattern from within a macro, you should precede the commands with the [PauseUpdate](/igorpro/commands/pauseupdate.md) operation to prevent multiple updates (which would be slow).

Dashed lines may also be redefined by the Dashed Lines dialog which you can select from the Misc menu.

The dashed line patterns are saved as part of the experiment. When a new experiment is opened, the preferred dash patterns are restored.

Some programs and printer drivers do not properly render dashed lines with many "dash,skip" pairs.

### *Examples* {#examples}

```igor
Make test; Display test
SetDashPattern 17, {20,3,15,8}  // sets last dashed line pattern
ModifyGraph lstyle(test)=17     // apply pattern to trace
```

### *See Also* {#see-also}
[PauseUpdate](/igorpro/commands/pauseupdate.md), [ResumeUpdate](/igorpro/commands/resumeupdate.md)