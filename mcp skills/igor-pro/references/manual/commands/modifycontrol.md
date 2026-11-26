---
description: "The ModifyControl operation modifies the named control. ModifyControl works on any kind of existing control. To modify multiple controls, use ModifyControlList."
slug: /commands/modifycontrol
---

<div className="command-signature">

## <strong>ModifyControl</strong>  [/Z] <em>ctrlName</em>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#modifycontrol}

</div>

The ModifyControl operation modifies the named control. ModifyControl works on any kind of existing control. To modify multiple controls, use [ModifyControlList](/igorpro/commands/modifycontrollist.md).

### *Parameters* {#parameters}
*ctrlName*  is the name of the control to be created or changed. The control must exist.

### *Keywords* {#keywords}
The following keyword=value parameters are supported:


```
activate, align, appearance, bodywidth, disable, fColor, focusRing, font, fSize, fStyle,
help, labelBack, noproc, pos, proc, rename, size, title, userdata,
valueBackColor, valueColor, win
```

Coordinates are in [control panel units](/igorpro/user-interface/controls.md#control-panel-units).

For details on these keywords, see the documentation for [SetVariable](/igorpro/user-interface/controls.md#setvariable).

The following keywords are not supported:


```
mode, popmatch, popvalue, value, variable
```

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
Use ModifyControl to move, hide, disable, or change the appearance of a control without regard to its kind.

### *Example* {#example}
Here is a [TabControl](/igorpro/user-interface/controls.md#tabcontrol) procedure that shows and hides all controls in the tabs appropriately, without knowing what kind of controls they are.

The "trick" here is that all controls that are to be shown within particular tab *n* have been assigned names that end with "_tab*n*" such as "_tab0" and "_tab1":


```igor
Function TabProc(ctrlName,tabNum) : TabControl
	String ctrlName	
	Variable tabNum

	String curTabMatch= "*_tab"+num2istr(tabNum)

	String controls= ControlNameList("")
	Variable i, n= ItemsInList(controls)
	for(i=0; i<n; i+=1)
		String control= StringFromList(i, controls)
		Variable isInATab= stringmatch(control,"*_tab*")
		if( isInATab )
			Variable show= stringmatch(control,curTabMatch)
			ControlInfo $control                // gets V_disable
			if( show )
				V_disable= V_disable & ~0x1     // clear the hide bit
			else
				V_disable= V_disable | 0x1      // set the hide bit
			endif
			ModifyControl $control disable=V_disable
		endif
	endfor
	return 0
End

// Action procedures that enable or disable the buttons
Function Tab1CheckProc(ctrlName,enableButton) : CheckBoxControl
	String ctrlName
	Variable enableButton

	ModifyControl button_tab1, disable=(enableButton ? 0 : 2 )

	return 0
End

Function Tab0CheckProc(ctrlName,enableButton) : CheckBoxControl
	String ctrlName
	Variable enableButton

	ModifyControl button_tab0, disable=(enableButton ? 0 : 2 )

	return 0
End

// Panel macro that creates a TabControl which uses TabProc
Window TabbedPanel() : Panel
	PauseUpdate; Silent 1		// building window...
	NewPanel /W=(381,121,614,237) as "Tab Demo"
	TabControl tab, pos={12,9},size={205,91},proc=TabProc,tabLabel(0)="Tab 0"
	TabControl tab, tabLabel(1)="Tab 1",value= 0
	Button button_tab0, pos={54,39},size={110,20},disable=2
	Button button_tab0, title="Button in Tab0"
	Button button_tab1, pos={54,63},size={110,20},disable=1
	Button button_tab1, title="Button in Tab1"
	CheckBox check1_tab1, pos={51,41}, size={117,14}, disable=1, value= 1
	CheckBox check1_tab1, proc=Tab1CheckProc, title="Enable Button in Tab 1"
	CheckBox check0_tab0, pos={51,73}, size={117,14}, proc=Tab0CheckProc
	CheckBox check0_tab0, value= 0, title="Enable Button in Tab 0"
EndMacro
```

Run TabbedPanel to create the panel. Then click on "Tab 0" and "Tab 1" to run TabProc.

### *See Also* {#see-also}
[Controls and Control Panels](/igorpro/user-interface/controls.md) for details about control panels and controls.

[Control Panel Units](/igorpro/user-interface/controls.md#control-panel-units) for a discussion of the units used for controls.

[ModifyControlList](/igorpro/commands/modifycontrollist.md), [ControlNameList](/igorpro/commands/controlnamelist.md)

[Button](/igorpro/commands/button.md), [Chart](/igorpro/commands/chart.md), [CheckBox](/igorpro/commands/checkbox.md), [GroupBox](/igorpro/user-interface/controls.md#groupbox), [ListBox](/igorpro/user-interface/controls.md#listbox), [PopupMenu](/igorpro/commands/popupmenu.md), [SetVariable](/igorpro/user-interface/controls.md#setvariable), [Slider](/igorpro/commands/slider.md), [TabControl](/igorpro/user-interface/controls.md#tabcontrol), [TitleBox](/igorpro/user-interface/controls.md#titlebox), [ValDisplay](/igorpro/commands/valdisplay.md)