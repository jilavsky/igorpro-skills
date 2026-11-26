---
description: "The ContourInfo function returns a string containing a semicolon-separated list of information about the specified contour plot in the named graph."
slug: /commands/contourinfo
---

<div className="command-signature">

## <strong>ContourInfo</strong> (<em>graphNameStr</em>, <em>contourWaveNameStr</em>, <em>instanceNumber</em>) {#contourinfo}

</div>

The ContourInfo function returns a string containing a semicolon-separated list of information about the specified contour plot in the named graph.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph.

*contourWaveNameStr* is a string containing either the name of the wave displayed as a contour plot in the named graph, or a contour instance name (wave name with "#n" appended to distinguish the nth contour plot of the wave in the graph). You might get a contour instance name from the [ContourNameList](/igorpro/commands/contournamelist.md) function.

If *contourWaveNameStr* contains a wave name, *instanceNumber* identifies which contour plot of *contourWaveNameStr* you want information about. *instanceNumber* is usually 0 because there is normally only one instance of a wave displayed as a contour plot in a graph. Set *instanceNumber* to 1 for information about the second contour plot of *contourWaveNameStr* , etc. If *contourWaveNameStr* contains "", then information is returned on the *instanceNumber*th contour plot in the graph.

If *contourWaveNameStr* contains an instance name, and *instanceNumber* is zero, the instance is taken from *contourWaveNameStr* . If *instanceNumber* is greater than zero, the wave name is extracted from *contourWaveNameStr* , and information is returned concerning the *instanceNumber*th instance of the wave.

### *Details* {#details}
The string contains several groups of information. Each group is prefaced by a keyword and colon, and terminated with the semicolon. The keywords are as follows:


| Keyword | Information Following Keyword |
| --- | --- |
| AXISFLAGS | Flags used to specify the axes. Usually blank because /L and /B (left and bottom axes) are the defaults. |
| DATAFORMAT | Either XYZ or Matrix. |
| LEVELS | A comma-separated list of the contour levels, including the final automatic levels, (or manual or from-wave levels), and the "more levels", all sorted into ascending Z order. |
| RECREATION | List of keyword commands as used by ModifyContour command. The format of these keyword commands is: |
|  | *keyword* (x)=*modifyParameters*; |
| TRACESFORMAT | Format string used to name the contour traces (see [AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md) or [AppendXYZContour](/igorpro/commands/appendxyzcontour.md)). |
| XAXIS | X axis name. |
| XWAVE | X wave name if any, else blank. |
| XWAVEDF | The full path to the data folder containing the X wave or blank if there is no X wave. |
| YAXIS | Y axis name. |
| YWAVE | Y wave name if any, else blank. |
| YWAVEDF | The full path to the data folder containing the Y wave or blank if there is no Y wave. |
| ZWAVE | Name of wave containing Z data from which the contour plot was calculated. |
| ZWAVEDF | The full path to the data folder containing the Z data wave. |



The format of the RECREATION information is designed so that you can extract a keyword command from the keyword and colon up to the ";", prepend "ModifyContour ", replace the "x" with the name of a contour plot ("data#1" for instance) and then [Execute](/igorpro/commands/execute.md) the resultant string as a command.

### *Examples* {#examples}
The following command lines create a very unlikely contour display. If you did this, you would most likely want to put each contour plot on different axes, and arrange the axes such that they don't overlap. That would greatly complicate the example.


```igor
Make/O/N=(20,20) jack=sin(x/5)+cos(y/4)
Display;AppendMatrixContour jack;DelayUpdate
AppendMatrixContour/T/R jack;DelayUpdate                // Second instance of jack
ModifyContour jack labels=0;DelayUpdate                 // Don't print labels-
ModifyContour jack#1 labels=0                           //  they take a long time
```

This example accesses the contour information for the second contour plot of the wave "jack" (which has an instance number of 1) displayed in the top graph:


```igor
Print StringByKey("ZWAVE", ContourInfo("","jack",1))    // prints jack
```

### *See Also* {#see-also}
[Execute](/igorpro/commands/execute.md), [ModifyContour](/igorpro/commands/modifycontour.md)