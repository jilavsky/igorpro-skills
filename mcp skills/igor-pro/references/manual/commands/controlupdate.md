---
description: "The ControlUpdate operation updates the named control or all controls in a window, which can be the top graph or control panel or the named graph or control…"
slug: /commands/controlupdate
---

<div className="command-signature">

## <strong>ControlUpdate</strong>  [/A /W=<em>winName</em> ] [<em>controlName</em> ] {#controlupdate}

</div>

The ControlUpdate operation updates the named control or all controls in a window, which can be the top graph or control panel or the named graph or control panel if you use /W.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/A</span> | Updates all controls in the window. You must omit *controlName* . |
| <span class="table-cell-nowrap">/W = *winName*</span> | Specifies the window or subwindow containing the control. If you omit *winName*  Igor will use the top graph or control panel window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
ControlUpdate is useful for forcing a pop-up menu to rebuild, to update a ValDisplay control, or to forcibly accept a SetVariable's currently-being-edited value.

Normally, a pop-up menu rebuilds only when the user clicks on it. If you set up a pop-up menu so that its contents depends on a global string variable, on a user-defined string function or on an Igor function (e.g., WaveList), you may want to force the pop-up menu to be updated at your command.

Usually, a ValDisplay control displays the value of a global variable or of an expression involving a global variable. If the global variable changes, the ValDisplay will automatically update. However, you can create a ValDisplay that displays a value that does not depend on a global variable. For example, it might display the result of an external function. In a case like this, the ValDisplay will not automatically update. You can update it by calling ControlUpdate.

When a SetVariable control is being edited, the text the user types isn't "accepted" (or processed) until the user presses Return or Enter. ControlUpdate effectively causes the named control to act as though the user has pressed one of those keys. If /A is specified, the currently active SetVariable control (if any) is affected this way. The motivation here is that the user may have typed a new value without having yet pressed return, and then may click a button in a different panel which runs a routine that uses the SetVariable value as input. The user expected the typed value to have been accepted but the variable has not yet been set. Calling ControlUpdate/A on the first panel will read the typed value in the variable, avoiding a discrepancy between the visible value of the SetVariable control and the actual value of the variable.

### *Examples* {#examples}
When a pop-up control's list is a string expression, such as a global variable or a string function, Igor sometimes won't update the pop-up menu when the expression's value changes. For example:


```igor
NewPanel;DoWindow/C PanelX
String/G popupList="First;Second;Third"
PopupMenu oneOfThree value=popupList      // popup shows "First"
popupList="1;2;3"                         // popup is unchanged
ControlUpdate/W=PanelX oneOfThree         // popup shows "1"
```

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.