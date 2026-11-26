---
description: "The ModifyBoxPlot operation modifies a box plot trace in the target or named graph. To create a box plot trace, see AppendBoxPlot."
slug: /commands/modifyboxplot
---

<div className="command-signature">

## <strong>ModifyBoxPlot</strong>  [/W=<em>winName</em>] [<em>keyword</em>=<em>value</em>, <em>keyword</em>=<em>value</em>, ...] {#modifyboxplot}

</div>

The ModifyBoxPlot operation modifies a box plot trace in the target or named graph. To create a box plot trace, see [AppendBoxPlot](/igorpro/commands/appendboxplot.md). For a detailed discussion of box plots and the parts of a box plot, see [Box Plots](/igorpro/graphing/graphs.md#box-plots).

ModifyBoxPlot was added in Igor Pro 8.00.

### *Parameters* {#parameters}
ModifyBoxPlot parameters consist of keyword=value pairs. The trace keyword specifies the trace targeted by the subsequent keywords. For example, the command:


```igor
ModifyBoxPlot trace=trace0, boxFill=(49151,60031,65535)		// Light blue
```

sets the box fill for all datasets of the trace0 trace to light blue.

As of Igor Pro 9.00, you can modify a setting for a specific dataset of a specific trace by adding a zero-based dataset index in square brackets after the keyword. For example:


```igor
ModifyBoxPlot trace=trace0, boxFill[1]=(49151,65535,49151)	// Light green
```

This sets the box fill for the second dataset (index=1) to light green leaving the box fill for other datasets unchanged.

### *General Parameters* {#general-parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">trace = *traceName*</span> | Specifies the name of a box plot trace to be modified. An error results if the named trace is not a box plot trace. Without the trace keyword, ModifyBoxPlot uses the first trace in the graph, whether it is a box plot trace or not. But, see the instance keyword for an exception. |
| <span class="table-cell-nowrap">instance = *instanceNum*</span> | The combination of trace and instance works the same as (*traceName*#*instanceNum*) for a [ModifyGraph](/igorpro/commands/modifygraph.md) keyword. |
|  | The instance keyword without the trace keyword accesses the *instanceNum*'th trace in the graph, just like [*traceNum*] used with a ModifyGraph keyword. See [Trace Names](/igorpro/graphing/graphs.md#trace-names) and [Object Indexing](/igorpro/programming/commands.md#object-indexing). |
| <span class="table-cell-nowrap">medianIsMarker[ = *v*]</span> | If *v* is omitted or is non-zero, the median is shown using a marker instead of with a line across the box part of the box plot. |
| <span class="table-cell-nowrap">notched[ = *n*]</span> | If *n* omitted or is non-zero, a notched box plot is drawn. The notches represent the 95 percent confidence limits of the median value. |
| <span class="table-cell-nowrap">outlierMethod = *m*</span> |  |
| <span class="table-cell-nowrap">outlierMethod = {*m*, *p1*, *p2*, *p3*, *p4*}</span> |  |
|  | When the raw data values are drawn on the box plot, they are classified as normal data points, outliers and far outliers. There are four methods for classifying the values. Method 0 and 1 require no parameters and can use the outlierMethod=*m* format. Method 2 and 3 require extra parameters and require the extended format that uses curly braces. |
|  |<table class="nested-table"><tbody><tr><td>*m*=0:</td><td>Tukey&#39;s method (default): outliers are values outside of the inner fences and far outliers are values outside the outer fences. For details including the definition of the fences, see [Box Plots](/igorpro/graphing/graphs.md#box-plots).</td></tr><tr><td>*m*=1:</td><td>Outliers are any data values beyond the ends of the whiskers. With this method, there are no far outliers.</td></tr><tr><td>*m*=2:</td><td>Outliers are values beyond the mean +- factor1\*SD. Far outliers are values beyond the mean +- factor2\*SD, where SD is the standard deviation. The factor1 is given by *p1* and factor2 is given by *p2*. The parameters *p3* and *p4* are not used.</td></tr><tr><td>*m*=3:</td><td>Outliers and far outliers are completely specified by the parameters. *p1* sets the boundary for lower far outliers, *p2* for lower outliers, *p3* for upper outliers, and *p4* for upper far outliers. All four parameters are required.</td></tr></tbody></table>
|  | The outlierMethod keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">quartileMethod = *m*</span> | Selects the method to be used in computing the quartiles (top and bottom of the boxes): |
|  |<table class="nested-table"><tbody><tr><td>*m*=0:</td><td>Tukey&#39;s method (default)</td></tr><tr><td>*m*=1:</td><td>Minitab method</td></tr><tr><td>*m*=2:</td><td>Moore and McCabe method</td></tr><tr><td>*m*=3:</td><td>Mendenhall and Sincich method</td></tr></tbody></table>
|  | See the discusion of [StatsQuantiles](/igorpro/commands/statsquantiles.md) /QM flag for details. |
| <span class="table-cell-nowrap">showData = *whatData*</span> | Selects a subset of the raw data for each box plot in a trace to be displayed using markers. The value of *whatData* is a name: |
|  |<table class="nested-table"><tbody><tr><td>All:</td><td>Show all data points (default)</td></tr><tr><td>None:</td><td>Show no data points</td></tr><tr><td>Outliers:</td><td>Show only outliers and far outliers</td></tr><tr><td>FarOutliers:</td><td>Show only far outliers</td></tr></tbody></table>
|  | See [Box Plots](/igorpro/graphing/graphs.md#box-plots) for more information about outliers. |
|  | By default, the marker for normal data points is a hollow circle 0.7 times the size of a normal trace marker, outliers are shown by a full-size filled circle, and far outliers are shown using a full-size filled box. |
| <span class="table-cell-nowrap">showFences[ = *v*]</span> | If *v* is omitted or non-zero, the fences are shown as dotted lines the same width as the boxes. See [Box Plots](/igorpro/graphing/graphs.md#box-plots) for a discussion of fences. *v* defaults to 0. |
| <span class="table-cell-nowrap">showMean[ = *v*]</span> | If *v* is omitted or non-zero, the mean of the data is shown as a marker. *v* defaults to 0. |
| <span class="table-cell-nowrap">whiskerMethod = *m*</span> |  |
| <span class="table-cell-nowrap">whiskerMethod = {*m* [, *p1*, *p2*]}</span> |  |
|  | The whiskers are drawn from the quartiles (top and bottom of the box) to some extreme value, as determined by whiskerMethod. Methods 0-5 do not take extra parameters, and can be specified using the whiskerMethod=*m* format. Methods 6 and 7 take extra parameters and require the extended format with curly braces. |
|  | The extended format was added in Igor Pro 9.00. |
|  |<table class="nested-table"><tbody><tr><td>*m*=0:</td><td>The extreme data values (default)</td></tr><tr><td>*m*=1:</td><td>The inner fences</td></tr><tr><td>*m*=2:</td><td>The &quot;adjacent&quot; points - the last data points inside the inner fences</td></tr><tr><td>*m*=3:</td><td>One standard deviation away from the mean value</td></tr><tr><td>*m*=4:</td><td>The 9th and 91st percentiles</td></tr><tr><td>*m*=5:</td><td>The 2nd and 98th percentiles</td></tr><tr><td>*m*=6:</td><td>The lower whisker is drawn from the box to a percentile given by *p1*. The upper whisker is drawn from the box to a percentile given by *p2*. This method requires both *p1* and *p2*. Added in Igor Pro 9.00.</td></tr><tr><td>*m*=7:</td><td>Whisker ends are at values given by mean data value +- a factor times the standard deviation. The factor is given by *p1*. *p2* is not used for this method. Added in Igor Pro 9.00.</td></tr></tbody></table>
|  | See [Box Plots](/igorpro/graphing/graphs.md#box-plots) for a discussion of fences and percentiles. |

### *Appearance Parameters* {#appearance-parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">boxWidth = *w*</span> | For a non-category X axis, boxWidth sets the width of the box showing the quartiles. If *w* is between zero and one, it is taken to be a fraction of the width of the plot rectangle. If *w* is greater than one, it is in points. |
|  | If the box plot is displayed using a category X axis, boxWidth is ignored. The box width is set the same as a category plot box and is affected by [ModifyGraph](/igorpro/commands/modifygraph.md) barGap and catGap. |
|  | A new non-category box plot has box width set as boxWidth=(1/2\**n*) where *n* is the number of data sets (the number of boxes) on the trace. |
| <span class="table-cell-nowrap">capWidth = *w*</span> | The whiskers may optionally be terminated with a horizontal line of width controlled by the capWidth keyword. If *w* is between zero and one, it is a fraction of the box width. If *w* is greater than one, it is in points. If *w* is zero (default), no cap is drawn. |
| <span class="table-cell-nowrap">jitter = *j*</span> | Applies a horizontal offset to each displayed data point in order to make it easier to see dense data sets. The argument, *j*, controls the maximum offset applied to any data point, expressed as a fraction of the box width. The value of *j* may be greater than 1, but in general values less than 1 look better. The default is 0.7. |
| <span class="table-cell-nowrap">lineStyles = {*boxStyle*, *whiskerStyle*, *medianStyle*[, *capStyle*]}</span> |  |
|  | Set the line style used to draw the box, the whiskers, the median line, and optionally the whisker caps. See [Dashed Lines](/igorpro/graphing/making-figures/graphics.md#dashed-lines) for a description of line styles. |
|  | A line style of -1 uses the line style set by [ModifyGraph](/igorpro/commands/modifygraph.md) lstyle. |
|  | All parameters default to -1. |
| <span class="table-cell-nowrap">lineThickness = {*boxThickness*, *whiskerThickness*, *medianThickness*[, *capThickness*]}</span> |  |
|  | Sets the line thickness used to draw the box, the whiskers, the median line, and optionally the whisker caps. A thickness less than zero uses the thickness set by the [ModifyGraph](/igorpro/commands/modifygraph.md) lsize keyword. A zero thickness hides the corresponding element of the box plot. |
|  | All parameters default to -1. |
| <span class="table-cell-nowrap">markers = {*dataMarker*, *outlierMarker*, *farOutlierMarker*[, *medianMarker*, *meanMarker*]}</span> |  |
|  | Sets the marker number to be used for ordinary data points, outliers, far outliers, the median value if the medianIsMarker keyword was specified and the mean value if the showMean keyword was specified. See [Markers](/igorpro/graphing/graphs.md#markers) for a complete list. |
|  | These parameters default to markers={8, 19, 16, 26, 27} (hollow circle, filled circle, filled square, X, horizontal diamond). Setting a any of the parameters to -1 uses the corresponding default marker. |
| <span class="table-cell-nowrap">markersOnTop = {*dataOnTop*, *medianOnTop*, *meanOnTop*}</span> |  |
|  | By default, the data markers, median marker if enabled by medianIsMarker, and mean marker if enabled by showMean, are drawn below the box and whisker lines so that they don't obscure the lines. But some special effects require the markers to be on top. |
|  | Setting *dataOnTop* to 1 causes all raw data points (normal data points, outliers and far outliers) to be drawn above the box and whisker lines. *medianOnTop* and *meanOnTop* similarly control the drawing of the median and mean markers. |
|  | The *markersOnTop* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">markerSizes = {*dataSize*, *outlierSize*, *farOutlierSize*[, *medianSize*, *meanSize*]}</span> |  |
|  | Sets the marker size for ordinary data points, outliers, far outliers, the median value if the *medianIsMarker* keyword has been specified and the mean value if the showMean keyword has been specified. A marker size of zero uses the marker size set by [ModifyGraph](/igorpro/commands/modifygraph.md) msize times a scaling factor. The scaling factor is 2/3 for non-outlier points, 1 for outliers and the median and mean markers, and 4/3 for far outliers. |
|  | All parameters default to 0. |
| <span class="table-cell-nowrap">opaqueMarkers = {*opaqueData*, *opaqueOutliers*, *opaqueFarOutliers*, *opaqueMedian*, *opaqueMean*}</span> |  |
|  | Causes the interior of hollow markers to be drawn opaque, covering up items underneath. This keyword has a separate settings for normal data points, outliers, far outliers, the median marker (if medianIsMarker is enabled) and the mean marker (if showMean is enabled). Markers of a given type are drawn opaque if the corresponding parameter is 1. |
|  | The opaqueMarkers keyword was added in Igor Pro 9.00. |

### *Color Parameters* {#color-parameters}
All colors are specified as (*r*,*g*,*b*[,*a*]) [RGBA Values](/igorpro/programming/commands.md#rgba-values). Specify color=(0,0,0,0) to use the color set by ModifyGraph rgb.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">boxColor = (*r*,*g*,*b*[,*a*])</span> | Sets the outline color of the box part. The default color is black. |
| <span class="table-cell-nowrap">boxFill = (*r*,*g*,*b*[,*a*])</span> | Sets the fill color of the box. |
| <span class="table-cell-nowrap">capColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the cap line, if present. The default color is black. |
| <span class="table-cell-nowrap">dataColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of non-outlier data points. The default color is the trace color. |
| <span class="table-cell-nowrap">dataStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the stroke color of non-outlier data points. The default color is black. |
|  | The *dataStrokeColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">dataFillColor = (*r*,*g*,*b*[,*a*])</span> | Sets the fill color of non-outlier data points when the markers are hollow. The default color is white. |
|  | The *dataFillColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">farOutlierColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of far outlier points. The default color is the trace color. |
| <span class="table-cell-nowrap">farOutlierStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the stroke color of far outlier data points. The default color is black. |
|  | The *farOutlierStrokeColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">farOutlierFillColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the fill color of far outlier data points when the markers are hollow. The default color is white. |
|  | The *farOutlierFillColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">meanColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the mean marker. The default color is the trace color. |
| <span class="table-cell-nowrap">meanStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the stroke color of the mean marker, if *showMean* is enabled. The default color is black. |
|  | The *meanStrokeColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">meanFillColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the fill color of the mean marker, if *showMean* is enabled. Applies when the marker is hollow. The default color is white. |
|  | The *meanFillColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">medianLineColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of the median line. You can see the effect only if *medianIsMarker* is not set. The default color is black. |
| <span class="table-cell-nowrap">medianMarkerColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of the median marker. You can see the effect only if *medianIsMarker* is set. The default color is the trace color. |
| <span class="table-cell-nowrap">medianStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the stroke color of the median marker which is displayed if *medianIsMarker* is enabled. The default color is black. |
|  | The *medianStrokeColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">medianFillColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the fill color of the median marker which is displayed if *medianIsMarker* is enabled. Applies when the marker is hollow. The default color is white. |
|  | The *medianFillColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">outlierColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the markers for normal outliers. The default color is the trace color. |
| <span class="table-cell-nowrap">outlierStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the stroke color of outlier data points. The default color is black. |
|  | The *outlierStrokeColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">outlierFillColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the fill color of outlier data points when the markers are hollow. The default color is white. |
|  | The *outlierFillColor* keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">whiskerColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color the whisker lines. The default color is black. |

### *Box Plot Per-Data-Point Marker Settings* {#box-plot-per-data-point-marker-settings}
You can override the basic settings for data point marker color, marker style and marker size using marker settings waves containing per-data-point settings. This feature was added in Igor Pro 9.00.

You can apply per-data-point marker settings to an entire trace (to all datasets comprising a trace) or to a specific dataset of a trace. For example:


```igor
Function DemoBoxPlotPerPointMarkerSettings()
	Make/O box0={1,2,3,4,5}, box1={2,3,4,5,6}, box2={3,4,5,6,7}
	String title = "Box Plot Per Point Marker Settings"
	Display/W=(557,99,948,310)/N=BoxPlotPerPointPlot as title
	
	// Create a trace named trace0 with three datasets: box0, box1, box2
	AppendBoxPlot/TN=trace0 box0,box1,box2
	
	// Set the marker and marker size for all datasets of trace trace0
	ModifyBoxPlot trace=trace0, markers={18,-1,-1}		// 18=Diamond
	ModifyBoxPlot trace=trace0, markerSizes={5,5,5}
	
	// Set the per-data-point marker for all datasets of trace0
	Make/O boxMarkers = {15,16,17,18,19}
	ModifyBoxPlot trace=trace0, dataMarkerWave=boxMarkers
		
	// Set the per-data-point marker for dataset box1 only
	Make/O boxMarkersForBox1 = {32,33,34,35,36}
	ModifyBoxPlot trace=trace0, dataMarkerWave[1]=boxMarkersForBox1
End
```

Usually a marker settings wave will have the same number of rows as there are data points in a given data set, but that is not required. If there are fewer rows in the settings wave than in the dataset, the extra data points retain their basic settings. If there are more rows in the settings wave than in the dataset, the extra settings wave points are not used.

See [Making Each Data Point Look Different](/igorpro/graphing/graphs.md#making-each-data-point-look-different) for more information and examples.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">dataColorWave [ = *colorWave*]</span> |  |
|  | Sets *colorWave* to override data point marker color on a point-by-point basis. The wave must be a 3 or 4 column wave containing red, green, blue and optionally alpha values. |
|  | If you omit "=*colorWave*", any previous marker color wave setting is cleared. |
|  | The dataColorWave keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">dataMarkerWave [ = *markerWave*]</span> |  |
|  | Sets *markerWave* to override data point markers on a point-by-point basis. The values in *markerWave* are standard graph marker numbers: see [Markers](/igorpro/graphing/graphs.md#markers) for a table of the markers and the associated marker numbers. The marker numbers are clipped to a valid range. |
|  | If you omit "=*markerWave*", any previous marker wave setting is cleared. |
|  | The dataMarkerWave keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">dataSizeWave [ = *markerSizeWave*]</span> |  |
|  | Sets *markerSizeWave* to override data point marker size on a point-by-point basis. The values in *markerWave* are clipped to the range [0,200]. |
|  | If you omit "=*markerSizeWave*", any previous marker size wave setting is cleared. |
|  | The dataSizeWave keyword was added in Igor Pro 9.00. |

### *Example* {#example}

```igor
Make/O/N=(25,3) multicol    // A three-column wave with 25 rows
SetRandomSeed(.4)           // For reproducible "randomness"
multicol = gnoise(1)        // Three normally-distributed data sets
multicol[20][1] = 5         // A "far" outlier
multicol[13][2] = -4        // An outlier
Display; AppendBoxPlot multicol
ModifyGraph lSize=2
ModifyBoxPlot markers={8,19,19}
ModifyBoxPlot markerSizes={3,5,9}
ModifyBoxPlot capWidth=0.5
ModifyBoxPlot boxColor=(0,0,65535)
ModifyBoxPlot medianLineColor=(0,0,65535)
ModifyBoxPlot whiskerColor=(40000,40000,65535)
ModifyBoxPlot capColor=(40000,40000,65535)
ModifyBoxPlot boxFill=(0,0,65535,20000)
ModifyBoxPlot dataColor=(0,0,0)
ModifyBoxPlot outlierColor=(0,0,0)
ModifyBoxPlot farOutlierColor=(0,0,0)
ModifyBoxPlot jitter=0.75
```

<img src="Images/ModifyBoxPlot/ModifyBoxPlot_5.png" width="75%"/>


```igor
ModifyBoxPlot trace=multicol,markerThick={1,0,0},markersFilled={1,0,0,0,0}
ModifyBoxPlot trace=multicol,markerThick={1,0,0},dataFillColor=(2,39321,1)
```

<img src="Images/ModifyBoxPlot/ModifyBoxPlot_1.png" width="75%"/>


```igor
ModifyBoxPlot trace=multicol,dataFillColor[1]=(0,65535,0)
```

<img src="Images/ModifyBoxPlot/ModifyBoxPlot_3.png" width="75%"/>

### *See Also* {#see-also}
[Box Plots](/igorpro/graphing/graphs.md#box-plots), [AppendBoxPlot](/igorpro/commands/appendboxplot.md), [AddWavesToBoxPlot](/igorpro/commands/addwavestoboxplot.md), [ModifyGraph](/igorpro/commands/modifygraph.md)