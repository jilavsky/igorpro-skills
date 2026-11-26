---
description: "The ModifyFreeAxis operation designates the free axis (created with NewFreeAxis) to follow a controlling axis from which it gets axis range and units…"
slug: /commands/modifyfreeaxis
---

<div className="command-signature">

## <strong>ModifyFreeAxis</strong>  [/W=<em>winName</em> ] <em>axisName</em>, <em>master</em>=<em>mastName</em>  [, <em>hook</em>=<em>funcName</em> ] {#modifyfreeaxis}

</div>

The ModifyFreeAxis operation designates the free axis (created with [NewFreeAxis](/igorpro/commands/newfreeaxis.md)) to follow a controlling axis from which it gets axis range and units information. The free axis updates whenever the controlling axis changes. The axis limits and units can be modified by a user hook function.

### *Parameters* {#parameters}
*axisName* is the name of the free axis (which must have been created by [NewFreeAxis](/igorpro/commands/newfreeaxis.md)).

*masterName* is the name of the master axis controlling axisName.

*funcName* is the name of the user function that modifies the limits and units properties of the axis. If *funcName* is $"", the named hook function is removed.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Modifies *axisName* in the named graph window or subwindow. If /W is omitted the command affects the top graph window or subwindow. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
The free axis can also be designated to call a user-defined hook function that can modify limits and units properties of the axis. The hook function must be of the following form:


```igor
Function MyAxisHook(info)
	STRUCT WMAxisHookStruct &info

	<code to modify graph units or limits>
	return 0
End
```

where WMAxisHookStruct is a built-in structure with the following members:


### *WMAxisHookStruct Structure Members* {#wmaxishookstruct-structure-members}

| Member | Description |
| --- | --- |
| char win[MAX_WIN_PATH+1] | Host (sub)window. |
| char axName[MAX_OBJ_NAME+1] | Name of the axis. |
| char mastName[MAX_OBJ_NAME+1] | Name of controlling axis or nil. |
| char units[MAX_UNITS+1] | Axis units. User modifiable. |
| double min, max | Axis range minimum and maximum values. User modifiable. |

The constants used to size the char arrays are internal to Igor and are subject to change in future versions.

The hook function is called when refreshing axis range information (generally early in the update of a graph). Your hook must never kill a graph or an axis.

### *Example* {#example}
This example demonstrates how to program a free axis hook function, whose most important task is to change the values of info.min and info.max to alter the axis range of the free axis. The example free axis displays Fahrenheit values for data in Celsius.


```igor
Function CentigradeAndFahrenheit()
	Make/O/N=20 temperatures = -2+p/3+gnoise(0.5)	// sample data
	Display temperatures	// default left axis will indicate data's centigrade range
	String graphName = S_name
	Label/W=$graphName left "°C"
	ModifyGraph/W=$graphName zero(left)=1
	Legend/W=$graphName

	NewFreeAxis/R/O/W=$graphName fahrenheit	// make a right axis whose range will be Fahrenheit
	ModifyGraph/W=$graphName freePos(fahrenheit)={0,kwFraction},lblPos(fahrenheit)=43
	Label/W=$graphName fahrenheit "°F"

	ModifyFreeAxis/W=$graphName fahrenheit, master=left, hook=CtoF_FreeAxisHook
	// NOTE master=left part which makes the "free" axis
	// actually a "slave" to the left ("master") axis.
End

Function CtoF_FreeAxisHook(info)
	STRUCT WMAxisHookStruct &info
	
	GetAxis/Q/W=$info.win $info.mastName	// get master (left) axis' range in V_min, V_Max
	Variable minF =  V_min*9/5+32
	Variable maxF =  V_max*9/5+32

//	SetAxis/W=$info.win $info.axName, minF, maxF
//	SetAxis here is fruitless. These values get overwritten by Igor
//	after reading info.min and info.max, which we now set:
	info.min = minF	// new min for free axis
	info.max= maxF	// new max for free axis
	return 0
End
```

### *See Also* {#see-also}
[SetAxis](/igorpro/commands/setaxis.md), [KillFreeAxis](/igorpro/commands/killfreeaxis.md), [NewFreeAxis](/igorpro/commands/newfreeaxis.md)

The [ModifyGraph](/igorpro/commands/modifygraph.md) (axes) operation for changing other aspects of a free axis.