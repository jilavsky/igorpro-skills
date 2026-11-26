---
description: "The AxisInfo function returns a string containing a semicolon-separated list of information about the named axis in the named graph window or subwindow."
slug: /commands/axisinfo
---

<div className="command-signature">

## <strong>AxisInfo</strong> (<em>graphNameStr</em>, <em>axisNameStr</em>) {#axisinfo}

</div>

The AxisInfo function returns a string containing a semicolon-separated list of information about the named axis in the named graph window or subwindow.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph window.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*axisNameStr* is the name of the axis.

### *Details* {#details}
The string contains groups of information. Each group is prefaced by a keyword and colon, and terminated with a semicolon. The keywords are:


| Keyword | Information Following Keyword |
| --- | --- |
| AXFLAG | Flag used to select the axis in any of the operations that display waves (Display, AppendMatrixContour, AppendImage, etc.). |
| AXTYPE | Axis type, such as "left", "right", "top", or "bottom". |
| CATWAVE | The wave supplying the categories for the axis if this is a category plot. |
| CATWAVEDF | Full path to data folder containing category wave. |
| CTRACE | Name of the trace controlling the named axis. See [Trace Names](/igorpro/graphing/graphs.md#trace-names) for background information. This field was added in Igor Pro 9.00. |
| CWAVE | Name of wave controlling named axis. |
| CWAVEDF | Full path to data folder containing controlling wave. |
| FONT | Actual name of font used to draw axis tick labels. |
| FONTSIZE | Actual size of font used to draw axis tick labels, in points. |
| FONTSTYLE | Actual font style used to draw axis tick labels, in points. See [ModifyGraph for Axes](/igorpro/commands/modifygraph.md#modifygraph-for-axes) fstyle for the meaning of this integer value. |
| HOOK | Name set by ModifyFreeAxis with hook keyword. |
| ISCAT | Truth that this is a category axis (used in a category plot). |
| ISTFREE | Truth that this is truly free axis (created via NewFreeAxis). |
| MASTERAXIS | Name set by ModifyFreeAxis with master keyword. |
| RECREATION | List of keyword commands as used by ModifyGraph command. The format of these keyword commands is: |
|  | *keyword* (x)=*modifyParameters*; |
| SETAXISCMD | Full SetAxis command. |
| SETAXISFLAGS | Flags that would be used with the SetAxis function to set the particular auto-scaling behavior that the axis uses. If the axis uses a manual axis range, SETAXISFLAGS is blank. |
| UNITS | Axis units, if any. |

The format of the RECREATION information is designed so that you can extract a keyword command from the keyword up to the ";", prepend "ModifyGraph ", replace the "x" with the name of an actual axis and then [Execute](/igorpro/commands/execute.md) the resultant string as a command.

### *Examples* {#examples}

```igor
Make/O data=x;Display data
Print StringByKey("CWAVE", AxisInfo("","left"))		// Prints data
	// Get a numeric value from the RECREATION keyword nested keyword values
	String info = AxisInfo("","left")
	String key = ";RECREATION:"
	Variable index = strsearch(info,key,0)
	String recreation = info[index+strlen(key),inf]
	Print recreation	// prints catGap(x)=0.1;barGap(x)=0.1;...
Print NumberByKey("barGap(x)",recreation,"=")		// Prints 0.1
```

### *See Also* {#see-also}
[GetAxis](/igorpro/commands/getaxis.md), [SetAxis](/igorpro/commands/setaxis.md), [AxisLabel](/igorpro/commands/axislabel.md), [StringByKey](/igorpro/commands/stringbykey.md), [NumberByKey](/igorpro/commands/numberbykey.md)

The "Readback ModifyStr.ipf" WaveMetrics procedure file is useful for parsing strings returned by AxisInfo.