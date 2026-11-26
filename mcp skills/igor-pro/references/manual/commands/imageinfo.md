---
description: "The ImageInfo function returns a string containing a semicolon-separated list of information about the specified image in the named graph window or subwindow."
slug: /commands/imageinfo
---

<div className="command-signature">

## <strong>ImageInfo</strong> (<em>graphNameStr</em>, <em>imageWaveNameStr</em>, <em>instanceNumber</em>) {#imageinfo}

</div>

The ImageInfo function returns a string containing a semicolon-separated list of information about the specified image in the named graph window or subwindow.

### *Parameters* {#parameters}
*graphNameStr* can be "" to refer to the top graph.

When identifying a subwindow with *graphNameStr*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

*imageWaveNameStr* contains either the name of a wave displayed as an image in the named graph, or an image instance name (wave name with "#n" appended to distinguish the nth image of the wave in the graph). You might get an image instance name from the [ImageNameList](/igorpro/commands/imagenamelist.md) function.

If *imageWaveNameStr* contains a wave name, *instanceNumber* identifies which instance you want information about. *instanceNumber* is usually 0 because there is normally only one instance of a wave displayed as an image in a graph. Set *instanceNumber* to 1 for information about the second image of the wave, etc. If *imageWaveNameStr* is "", then information is returned on the *instanceNumber*th image in the graph.

If *imageWaveNameStr* is an instance name, and *instanceNumber* is zero, the instance is taken from *imageWaveNameStr*. If *instanceNumber* is greater than zero, the wave name is extracted from *imageWaveNameStr*, and information is returned concerning the *instanceNumber*th instance of the wave.

### *Details* {#details}
The string contains several groups of information. Each group is prefaced by a keyword and colon, and terminated with the semicolon for ease of use with [StringByKey](/igorpro/commands/stringbykey.md). The keywords are as follows:


| Keyword | Information Following Keyword |
| --- | --- |
| AXISFLAGS | Flags used to specify the axes. Usually blank because /L and /B (left and bottom axes) are the defaults. |
| COLORMODE | A number indicating how the image colors are derived: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Color table (see [Color Tables](/igorpro/graphing/contour-plots.md#color-tables)).</td></tr><tr><td>2:</td><td>Scaled color index wave (see [Indexed Color Details](/igorpro/graphing/image-plots.md#indexed-color-details)).</td></tr><tr><td>3:</td><td>Point-scaled color index (See [Example: Point-scaled Color Index Wave](/igorpro/graphing/image-plots.md#example-point-scaled-color-index-wave)).</td></tr><tr><td>4:</td><td>Direct color (see [Direct Color Details](/igorpro/graphing/image-plots.md#direct-color-details)).</td></tr><tr><td>5:</td><td>Explicit mode (see [ModifyImage](/igorpro/commands/modifyimage.md) explicit keyword).</td></tr><tr><td>6:</td><td>Color table wave (see [Color Table Waves](/igorpro/graphing/image-plots.md#color-table-waves)).</td></tr></tbody></table>
| LAYER | Either 0 or 1 indicating that the image is in Layer 0 (below traces and axes) or in Layer 1 (above traces and axes). |
| RECREATION | Semicolon-separated list of *keyword*=*modifyParameters* commands for the [ModifyImage](/igorpro/commands/modifyimage.md) command. |
| XAXIS | X axis name. |
| XWAVE | X wave name if any, else blank. |
| XWAVEDF | The full path to the data folder containing the X wave or blank if there is no X wave. |
| YAXIS | Y axis name. |
| YWAVE | Y wave name if any, else blank. |
| YWAVEDF | The full path to the data folder containing the Y wave or blank if there is no Y wave. |
| ZWAVE | Name of wave containing Z data from which the image plot was calculated. |
| ZWAVEDF | The full path to the data folder containing the Z data wave. |



The format of the RECREATION list is designed so that (once you extract the list) you can extract one keyword command from the list using [StringByKey](/igorpro/commands/stringbykey.md) and append it to "ModifyImage " followed by the name of an image plot ("data#1" for instance) and then [Execute](/igorpro/commands/execute.md) the resultant string as a command.

A helpful routine for extracting the RECREATION list from ImageInfo's return value is WMGetRECREATIONFromInfo in the "Graph Utility Procs" WaveMetrics procedure file (see WaveMetrics Procedures).

### *Example 1* {#example-1}
This example gets the image information for the second image plot of the wave "jack" (which has an instance number of 1) and applies its [ModifyImage](/igorpro/commands/modifyimage.md) settings to the first image plot.


```igor
#include <Graph Utility Procs>, version>=6.1    // For WMGetRECREATIONFromInfo

// Make two image plots of the same data on different left and right axes
Make/O/N=(20,20) jack=sin(x/5)+cos(y/4)
Display;AppendImage jack                        // bottom and left axes
AppendImage/R jack                              // bottom and right axes

// Put image plot jack#0 above jack#1
ModifyGraph axisEnab(left)={0.5,1},axisEnab(right)={0,0.5}

// Set jack#1 to use the Rainbow color table instead of the default Grays
ModifyImage jack#1 ctab={*,*,Rainbow,0}
```

<img src="Images/ImageInfo/ImageInfo_0.png" width="75%">


Now we peek at some of the image information for the second image plot of the wave "jack" (which has an instance number of 1) displayed in the top graph:


```igor
Print ImageInfo("","jack",1)[69,148]            // Just the interesting stuff
;ZWAVE:jack;ZWAVEDF:root:;COLORMODE:1;RECREATION:ctab= {*,*,Rainbow,0};plane= 0;

// Apply the color table, etc from jack#1 to jack:
String info= WMGetRECREATIONFromInfo(ImageInfo("","jack",1))
info= RemoveEnding(info)                        // Remove trailing semicolon

// Use comma instead of semicolon separators
String text = ReplaceString(";", info, ",")
Execute "ModifyImage jack " + text
```

<img src="Images/ImageInfo/ImageInfo_1.png" width="75%">

### *Example 2* {#example-2}
This example gets the full path to the wave containing the Z data from which the first image plot in the top graph was calculated.


```igor
String info= ImageInfo("","",0)		// 0 is index of first image plot
String pathToZ= StringByKey("ZWAVEDF",info)+StringByKey("ZWAVE",info)
Print pathToZ
	root:jack
```

### *See Also* {#see-also}
[ModifyImage](/igorpro/commands/modifyimage.md), [AppendImage](/igorpro/commands/appendimage.md), [NewImage](/igorpro/commands/newimage.md), [Execute](/igorpro/commands/execute.md)

[Image Plots](/igorpro/graphing/image-plots.md), [Image Instance Names](/igorpro/graphing/image-plots.md#image-instance-names)