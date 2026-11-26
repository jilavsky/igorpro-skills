---
description: "The TraceInfo function returns a string containing a semicolon-separated list of information about the trace in the named graph."
slug: /commands/traceinfo
---

<div className="command-signature">

## <strong>TraceInfo</strong> (<em>graphNameStr</em>, <em>yWaveNameStr</em>, <em>instance</em>) {#traceinfo}

</div>

The TraceInfo function returns a string containing a semicolon-separated list of information about the trace in the named graph.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*yWaveNameStr* is either the name of a wave containing data displayed as a trace in the named graph, or a trace name (wave name with "#n" appended to distinguish the nth image of the wave in the graph). You might get a trace name from the [TraceNameList](/igorpro/commands/tracenamelist.md) function.

If *yWaveNameStr* contains a wave name, *instance* identifies which trace of *yWaveNameStr* you want information about. *instance* is usually 0 because there is normally only one instance of a given wave displayed in a graph. Set *instance* to 1 for information about the second trace of the wave named by*yWaveNameStr*, etc. If *yWaveNameStr* is "", then information is returned on the *instance*th trace in the graph.

If *yWaveNameStr* is a trace name, and *instance* is zero, the instance is taken from *yWaveNameStr*. If *instance* is greater than zero, the wave name is extracted from *yWaveNameStr*, and information is returned concerning the *instance*th instance of the wave.

### *Details* {#details}
The string contains several groups of information. Each group is prefaced by a keyword and colon, and terminated with the semicolon. The keywords are as follows:


| Keyword | Information Following Keyword |
| --- | --- |
| AXISFLAGS | Flags used to specify the axes. Usually blank because /L and /B (left and bottom axes) are the defaults. |
| AXISZ | Z value of a contour trace or NaN if the trace is not a contour trace. |
| CONTOURZWAVE | Full path to contour plot's z wave, with possibly quoted wave name. Blank if trace is not a contour trace. |
|  | CONTOURZWAVE was added in Igor Pro 10.00. |
| ERRORBARS | The [ErrorBars](/igorpro/commands/errorbars.md) command for the trace, as it would appear in the recreation macro (without the beginning tab character). |
| RECREATION | List of keyword commands as used by ModifyGraph command. The format of these keyword commands is: |
|  | *keyword* (x)=*modifyParameters*; |
| TYPE | Gives the type of trace: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>XY or waveform trace</td></tr><tr><td>1:</td><td>Contour trace</td></tr><tr><td>2:</td><td>Box plot trace</td></tr><tr><td>3:</td><td>Violin plot trace</td></tr></tbody></table>
|  | TYPE was added in Igor Pro 8.00. |
| XAXIS | X axis name. |
| XRANGE | Point subrange of the trace's X data wave in "[*startPoint*, *endPoint* : *increment* ]" format. |
|  | <div><Admonition type="note"><p>unlike the actual syntax of a trace subrange specification where *increment* is preceded by a semicolon character, here it is preceded by a colon character to preserve the notion that semicolon  is what separates the keyword-value groups.</p></Admonition></div> |
|  | If the entire X wave is displayed (the usual case), the XRANGE value is "[\*]". |
|  | If an X wave is not used to display the trace, then the XRANGE value is "". |
| XWAVE | X wave name if any, else blank. |
| XWAVEDF | The full path to the data folder containing the X wave or blank if there is no X wave. |
| YAXIS | Y axis name. |
| YRANGE | Point subrange of the trace's Y data wave or "[\*]". |

The format of the RECREATION information is designed so that you can extract a keyword command from the keyword and colon up to the ";", prepend "ModifyGraph ", replace the "x" with the name of a trace ("data#1" for instance) and then [Execute](/igorpro/commands/execute.md) the resultant string as a command.

:::note
The syntax of any subrange specifications in the RECREATION information are modified in the same way as for XRANGE and YRANGE. Currently only the zColor, zmrkSize, and zmrkNum keywords might have a subrange specification.
:::

### *Examples* {#examples}

This example shows how to extract a string value from the keyword-value list returned by TraceInfo:

```igor
String yAxisName= StringByKey("YAXIS", TraceInfo("","",0))
```

This example shows how to extract a subrange and put the semicolon back:


```igor
String yRange= StringByKey("YRANGE", TraceInfo("","",0))
Print yRange				// prints "[30,40:2]"
yRange= ReplaceString(":", yRange, ";")
Print yRange				// prints "[30,40;2]"
```

The next example shows the trace information for the second instance of the wave "data" (which has an instance number of 1) displayed in the top graph:


```igor
Make/O data=x;Display/L/T data,data		// two instances of data, 0 and 1
Print TraceInfo("","data",1)[0,64]
Print TraceInfo("","data",1)[65,128]
```

Prints something like the following in the history area:


```
XWAVE:;YAXIS:left;XAXIS:top;AXISFLAGS:/T;AXISZ:NaN;XWAVEDF:;YRANG
E:[*];XRANGE:;TYPE:0;ERRORBARS:;RECREATION:zColor(x)=0;zColorMax
```

Following is a function that returns the marker code from the given instance of a named wave in the top graph. The example uses the GetNumFromModifyStr() function provided by the #include \<Readback ModifyStr\> procedures, which are useful for parsing strings returned by TraceInfo.


```igor
#include <Readback ModifyStr>

Function MarkerOfWave(wv,instance)
	Wave wv
	Variable instance
	
	Variable marker
	String info=TraceInfo("",NameOfWave(wv),instance)
	
	marker= GetNumFromModifyStr(info,"marker","",0)
	
	return marker
End
```

### *See Also* {#see-also}
[Trace Names](/igorpro/graphing/graphs.md#trace-names), [Programming With Trace Names](/igorpro/programming/programming.md#programming-with-trace-names)

[Execute](/igorpro/commands/execute.md), [StringByKey](/igorpro/commands/stringbykey.md), [NumberByKey](/igorpro/commands/numberbykey.md)