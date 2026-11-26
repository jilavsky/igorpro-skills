---
description: "The ModifyControlList operation modifies the controls named in the listStr string expression. ModifyControlList works on any kind of existing control."
slug: /commands/modifycontrollist
---

<div className="command-signature">

## <strong>ModifyControlList</strong>  [/Z] <em>listStr</em>  [, <em>keyword</em> =<em>value</em> ]... {#modifycontrollist}

</div>

The ModifyControlList operation modifies the controls named in the *listStr* string expression. ModifyControlList works on any kind of existing control.

### *Parameters* {#parameters}
*listStr* is a semicolon-separated list of names in a string expression. The expression can be an explicit list of control names such as "button0;checkbox1;" or it can be any string expression such as a call to the [ControlNameList](/igorpro/commands/controlnamelist.md) string function:


```igor
ModifyControlList ControlNameList("", ";", "*_tab0") disable=1
```

The controls must exist.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Keywords* {#keywords}
The following keyword=value parameters are supported:


```
activate, align, appearance, bodywidth, disable, fColor, focusRing, font, fSize, fStyle,
help, labelBack, noproc, pos, proc, rename, size, title, userdata,
valueBackColor, valueColor, win
```

Coordinates are in [control panel units](/igorpro/user-interface/controls.md#control-panel-units).

For details on these keywords, see the documentation for [SetVariable](/igorpro/user-interface/controls.md#setvariable).

The following keywords are *not* supported:


```
mod, popmatch, popvalue, value, variable
```

### *Details* {#details}
Use ModifyControlList to move, hide, or disable multiple controls without regard to their kind.

If *listStr* contains the name of a nonexistent control, an error is generated.

if *listStr* is "" (or any list element in *listStr* is ""), it is ignored and no error is generated.

### *Example* {#example}
Here is the [TabControl](/igorpro/user-interface/controls.md#tabcontrol) procedure example from the [ModifyControl](/igorpro/commands/modifycontrol.md) documentation rewritten to use ModifyControlList. It shows and hides all controls in the tabs appropriately, without knowing what kind of controls they are, but the code is simpler. This method does not, however, preserve the enable bit when a control is hidden.

The "trick" here is that all controls that are to be shown within particular tab *n* have been assigned names that end with "_tab*n*" such as "_tab0" and "_tab1":


```igor
// Action procedure
Function TabProc2(ctrlName,tabNum) : TabControl
	String ctrlName	
	Variable tabNum

	String controlsInATab= ControlNameList("", ";", "*_tab*")

	String curTabMatch= "*_tab"+num2istr(tabNum)
	String controlsInCurTab= ListMatch(controlsInATab, curTabMatch)
	String controlsInOtherTabs= ListMatch(controlsInATab, "!"+curTabMatch)

	ModifyControlList controlsInOtherTabs disable=1	// hide
	ModifyControlList controlsInCurTab disable=0		// show

	return 0
End

// Panel macro that creates a TabControl which uses TabProc2
Window TabbedPanel2() : Panel
	PauseUpdate; Silent 1		// building window...
	NewPanel /W=(35,208,266,374) as "Tab Demo"
	TabControl tab,pos={12,9},size={205,140},proc=TabProc2
	TabControl tab,tabLabel(0)="Tab 0"
	TabControl tab,tabLabel(1)="Tab 1",value= 0
	Button button_tab0,pos={26,43},size={110,20},title="Button in Tab0"
	Button button2_tab0,pos={26,74},size={110,20},title="Button in Tab0"
	Button button3_tab0,pos={26,106},size={110,20},title="Button in Tab0"
	Button button_tab1,pos={85,43},size={110,20},title="Button in Tab1"
	Button button2_tab1,pos={85,75},size={110,20},title="Button in Tab1"
	Button button3_tab1,pos={84,108},size={110,20},title="Button in Tab1"
	ModifyControlList ControlNameList("", ";", "*_tab1") disable=1
EndMacro
```

Run TabbedPanel2 and then click on "Tab 0" and "Tab 1" to run TabProc2.

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

[ModifyControl](/igorpro/commands/modifycontrol.md), [ControlNameList](/igorpro/commands/controlnamelist.md)

[Button](/igorpro/commands/button.md), [Chart](/igorpro/commands/chart.md), [CheckBox](/igorpro/commands/checkbox.md), [GroupBox](/igorpro/user-interface/controls.md#groupbox), [ListBox](/igorpro/user-interface/controls.md#listbox), [PopupMenu](/igorpro/commands/popupmenu.md), [SetVariable](/igorpro/user-interface/controls.md#setvariable), [Slider](/igorpro/commands/slider.md), [TabControl](/igorpro/user-interface/controls.md#tabcontrol), [TitleBox](/igorpro/user-interface/controls.md#titlebox), [ValDisplay](/igorpro/commands/valdisplay.md)