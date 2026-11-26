---
description: "The ModifyViolinPlot operation modifies a violin plot trace in the target or named graph."
slug: /commands/modifyviolinplot
---

<div className="command-signature">

## <strong>ModifyViolinPlot</strong>  [/W=<em>winName</em>] [<em>keyword</em>=<em>value</em>, <em>keyword</em>=<em>value</em>, ...] {#modifyviolinplot}

</div>

The ModifyViolinPlot operation modifies a violin plot trace in the target or named graph.

ModifyViolinPlot was added in Igor Pro 8.00.

For a detailed discussion of violin plots and the parts of a violin plot, see [Violin Plots](/igorpro/graphing/graphs.md#violin-plots).

### *Parameters* {#parameters}
ModifyViolinPlot parameters consist of keyword=value pairs. The trace keyword specifies the trace targeted by the subsequent keywords. For example, the command:


```igor
ModifyViolinPlot trace=trace0, markerSize=5
```

sets the marker size for all datasets of the trace0 trace.

As of Igor Pro 9.00, you can modify a setting for a specific dataset of a specific trace by adding a zero-based dataset index in square brackets after the keyword. For example:


```igor
ModifyViolinPlot trace=trace0, markerSize[1]=7
```

This sets the marker size for the second dataset (index=1) to 7 leaving the marker size for other datasets unchanged.

### *General Parameters* {#general-parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">trace = *traceName*</span> | Specifies the name of a violin plot trace to be modified. An error results if the named trace is not a violin plot trace. Without the trace keyword, ModifyViolinPlot uses the first trace in the graph, whether it is a violin plot trace or not but see the instance keyword for an exception. |
| <span class="table-cell-nowrap">instance = i*nstanceNum*</span> | The combination of trace and instance works the same as (*traceName*#*instanceNum*) for a [ModifyGraph](/igorpro/commands/modifygraph.md) keyword. |
|  | The instance keyword without the trace keyword accesses the *instanceNum*'th trace in the graph, just like [*traceNum*] used with a ModifyGraph keyword. See [Trace Names](/igorpro/graphing/graphs.md#trace-names) and [Object Indexing](/igorpro/programming/commands.md#object-indexing). |
| <span class="table-cell-nowrap">bandwidth[(*ds*)] = *bw*</span> | Sets the bandwidth used in computing the KDE curves. If you include *ds*, the bandwidth is set to *bw* for data set *ds*. If you omit *ds*, the bandwidth is set for all data sets. *bw* must be greater than or equal to 0. 0 uses the bandwidth estimated by the method set by the bandwidthMethod keyword. |
| <span class="table-cell-nowrap">bandwidthMethod = *m*</span> | Sets the method used to estimate the appropriate bandwidth used in computing the KDE curves. The methods are: |
|  |<table class="nested-table"><tbody><tr><td>*m*=0:</td><td>Silverman</td></tr><tr><td>*m*=1:</td><td>Scott (default)</td></tr><tr><td>*m*=2:</td><td>Bowman and Azzalini</td></tr></tbody></table>
|  | See [StatsKDE](/igorpro/commands/statskde.md) for details. |
|  | You can override the estimated bandwidth using the bandwidth keyword. |
| <span class="table-cell-nowrap">boxWidth = *w*</span> | For a non-category X axis, boxWidth sets the width of the space reserved for displaying the KDE curves. If *w* is between zero and one, it is taken to be a fraction of the width of the plot rectangle. If *w* is greater than one, it is in points. |
|  | All the KDE curves are normalized such that the maximum density value of the KDEs over all data sets fills the box width so only one of the violin plots will be as wide as *w*. You can control the normalization using the maxDensity keyword. |
|  | If the violin plot is displayed using a category X axis, boxWidth is ignored. The space reserved for each data set is controlled by the category axis and is affected by [ModifyGraph](/igorpro/commands/modifygraph.md) barGap and catGap. |
|  | A new non-category violin plot has box width set as boxWidth=1/(2 \* *n*) where *n* is the number of data sets (the number of violin plots) on the trace. |
| <span class="table-cell-nowrap">closeOutline[ = *close*]</span> | If *close* is 1 or omitted, the ends of the KDE curves are connected by a straight line. Closed curves are more visible if side=1 or side=2 in which case the KDE curves are closed by a straight line at the midline between the curves. |
| <span class="table-cell-nowrap">curveExtension = *ext*</span> | Sets the range of the KDE curves. The KDE curves are computed for a range of y=minData-*ext* to y=maxData+*ext*, where *ext* is in units of bandwidth. *ext* defaults to 1. |
| <span class="table-cell-nowrap">dataMarker = *marker*</span> | Sets the marker number used to display the raw data. If *marker* is -1, the marker for the trace as set by ModifyGraph marker is used. The default is 8 (hollow circle). |
| <span class="table-cell-nowrap">jitter = *j*</span> | In order to separate closely-spaced raw data points, the data points can be displaced horizontally. *j* controls the maximum offset applied to any data point, expressed as a fraction of the box width. The value of *j* may be greater than 1, but in general values less than 1 look better. The default value is 0.5. |
| <span class="table-cell-nowrap">kernel = *k*</span> | Sets the kernel function to be used in computing the KDE curves. Supported values are: |
|  |<table class="nested-table"><tbody><tr><td>*k*=1:</td><td>Epanechnikov</td></tr><tr><td>*k*=2:</td><td>Bi-weight</td></tr><tr><td>*k*=3:</td><td>Tri-weight</td></tr><tr><td>*k*=4:</td><td>Triangular</td></tr><tr><td>*k*=5:</td><td>Gaussian (default)</td></tr><tr><td>*k*=6:</td><td>Rectangular</td></tr></tbody></table>
|  | It is unusual for a violin plot to use anything other than Gaussian, which is the default. See [StatsKDE](/igorpro/commands/statskde.md) for details. |
| <span class="table-cell-nowrap">lineStyle = *style*</span> | Sets the line style used to draw the KDE curves. See [Dashed Lines](/igorpro/graphing/making-figures/graphics.md#dashed-lines) for a description of line styles. |
|  | A line style of -1 uses the line style set by [ModifyGraph](/igorpro/commands/modifygraph.md) lstyle. |
|  | *style* defaults to -1. |
| <span class="table-cell-nowrap">lineThickness = *thick*</span> | Sets the thickness of the line used to plot the KDE curves. A thickness less than zero uses the line width set by the [ModifyGraph](/igorpro/commands/modifygraph.md) lsize keyword. *thick*=0 hides the KDE curve. The default value is -1. |
| <span class="table-cell-nowrap">markerSize = *size*</span> | Sets the size of the marker used to display the raw data. A marker size of zero uses one-half of the marker size as set by [ModifyGraph](/igorpro/commands/modifygraph.md) msize. *size* defaults to zero. |
| <span class="table-cell-nowrap">markerThick = *t*</span> | Sets the thickness in points of the strokes of markers used to display the raw data. |
|  | The markerThick keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">maxDensity = *d*</span> | Sets the normalization for the width of the KDE curves to *d*. All the KDE curves are normalized such that the maximum density value of all KDEs fills the box width. The width of each curve gives an indication of the relative maximum density. maxDensity allows you to set the same normalization for multiple violin plots so that the width for all is relative to the same value. |
| <span class="table-cell-nowrap">plotSide = *side*</span> | By default, a violin plot is symmetrical with the KDE curve plotted twice in mirror image. You can control which side is plotted: |
|  |<table class="nested-table"><tbody><tr><td>*side*=0:</td><td>Both sides in mirror image (default)</td></tr><tr><td>*side*=1:</td><td>The left side</td></tr><tr><td>*side*=2:</td><td>The right side</td></tr></tbody></table>
|  | Using 1 or 2 allows you to combine two violin plots in an asymmetric plot. |
| <span class="table-cell-nowrap">showData[ = *sd*]</span> | Shows or hides the raw data points. *sd* is 0 or 1. showData by itself is equivalent to showData=1. The default is 1. |

### *Mean and Median Parameters* {#mean-and-median-parameters}
You can display markers showing the mean and the median of each data set using the keywords documented in this section. See [Markers](/igorpro/graphing/graphs.md#markers) for a list of available markers. For both mean and median, a marker size of zero uses the marker size set by [ModifyGraph](/igorpro/commands/modifygraph.md) msize.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">showMean[ = *show*]</span> | Shows or hides the marker representing the mean value. *show* is 0 or 1. showMean by itself is equivalent to showMean=1. The default is 0. |
| <span class="table-cell-nowrap">meanMarker = *marker*</span> | Sets the marker to use for the mean value. The default for the mean marker is 27 (hollow horizontal diamond with dot). |
| <span class="table-cell-nowrap">meanMarkerSize = *size*</span> | Sets the size of the marker used to display the mean value. A value of zero uses the trace marker size as set by ModifyGraph msize, or the normal trace default marker size. The default is zero. |
| <span class="table-cell-nowrap">meanMarkerThick = *t*</span> | Sets the thickness in points of the strokes of markers used to display the mean value if showMean is enabled. |
|  | The meanMarkerThick keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">showMedian[ = *show*]</span> | Shows or hides the marker representing the median value. *show* is 0 or 1. showMedian by itself is equivalent to showMedian=1. The default is 0. |
| <span class="table-cell-nowrap">medianMarker = *marker*</span> | Sets the marker to use for the median value. The default for the median marker is 26 (filled horizontal diamond). |
| <span class="table-cell-nowrap">medianMarkerSize = *size*</span> | Sets the size of the marker used to display the median value. A value of zero uses the trace marker size as set by ModifyGraph msize, or the normal trace default marker size. The default is zero. |
| <span class="table-cell-nowrap">medianMarkerThick = *t*</span> | Sets the thickness in points of the strokes of markers used to display the median value if showMedian is enabled. |
|  | The medianMarkerThick keyword was added in Igor Pro 9.00. |

### *Color Parameters* {#color-parameters}
All colors are specified as (*r*,*g*,*b*[,*a*]) [RGBA Values](/igorpro/programming/commands.md#rgba-values).


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">fillColor = (*r*,*g*,*b*[,*a*])</span> | Fills the area between the distribution curves with the specified color. Specifying fillColor=(0,0,0,0) removes the fill. If side=1 or side=2, the fill is between the curve and the mid line. |
| <span class="table-cell-nowrap">lineColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of the KDE curves. |
|  | Specify lineColor=(0,0,0,0) to use the trace color set using ModifyGraph rgb as the line color. The default is black. |
| <span class="table-cell-nowrap">markerColor = (*r*,*g*,*b*[,*a*])</span> | Sets the color of markers used to display the raw data. |
|  | Specify markerColor=(0,0,0,0) to use the trace color set using ModifyGraph rgb as the marker color. This is the default behavior. |
| <span class="table-cell-nowrap">markerStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of the strokes of markers used to display the raw data. |
|  | Specify markerStrokeColor=(0,0,0,0) to use the to use the trace color set using ModifyGraph rgb as the marker color. This is the default behavior. |
|  | The markerStrokeColor keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">markerFilled = *f*</span> | If *f* is non-zero, markers are filled with color. Normally, hollow markers have transparent fill. Default fill color is white. Applies only to hollow markers such as marker 8, the hollow circle marker. |
|  | The markerFilled keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">markerFillColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the fill color of markers used to display the raw data. Applies only to hollow markers such as marker 8, the hollow circle marker. |
|  | The markerFillColor keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">meanMarkerColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of markers used to display the mean value. |
|  | Specify meanMarkerColor=(0,0,0,0) to use the trace color set using ModifyGraph rgb as the mean marker color. This is the default behavior. |
| <span class="table-cell-nowrap">meanMarkerStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of the strokes of markers used to display the mean of the data if showMean is enabled. |
|  | Specify meanMarkerStrokeColor=(0,0,0,0) to use the to use the trace color set using ModifyGraph rgb as the marker color. This is the default behavior. |
|  | The meanMarkerStrokeColor keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">meanMarkerFilled = *f*</span> | If *f* is non-zero, the mean value marker is filled with color. Normally, hollow markers have transparent fill. Default fill color is white. Applies only to hollow markers such as marker 8, the hollow circle marker. |
|  | The meanMarkerFilled keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">meanMarkerFillColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the fill color of markers used to display the mean value if showMean is enabled. Applies only to hollow markers such as marker 8, the hollow circle marker. |
|  | The meanMarkerFillColor keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">medianMarkerColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of markers used to display the median value. |
|  | Specify medianMarkerColor=(0,0,0,0) to use the trace color set using ModifyGraph rgb as the median marker color. This is the default behavior. |
| <span class="table-cell-nowrap">medianMarkerStrokeColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the color of the strokes of markers used to display the median of the data if showMedian is enabled. |
|  | Specify medianMarkerStrokeColor=(0,0,0,0) to use the to use the trace color set using ModifyGraph rgb as the marker color. This is the default behavior. |
|  | The medianMarkerStrokeColor keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">medianMarkerFilled = *f*</span> | If *f* is non-zero, the median value marker is filled with color. Normally, hollow markers have transparent fill. Default fill color is white. Applies only to hollow markers such as marker 8, the hollow circle marker. |
|  | The medianMarkerFilled keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">medianMarkerFillColor = (*r*,*g*,*b*[,*a*])</span> |  |
|  | Sets the fill color of markers used to display the median value if showMedian is enabled. Applies only to hollow markers such as marker 8, the hollow circle marker. |
|  | The medianMarkerFillColor keyword was added in Igor Pro 9.00. |

### *Violin Plot Per-Data-Point Marker Settings* {#violin-plot-per-data-point-marker-settings}
You can override the basic settings for data point marker color, marker style and marker size using marker settings waves containing per-data-point settings.

You can apply per-data-point marker settings to an entire trace (to all datasets comprising a trace) or to a specific dataset of a trace. For example:


```igor
Function DemoViolinPlotPerPointMarkerSettings()
	Make/O violin0={1,2,3,4,5}, violin1={2,3,4,5,6}, violin2={3,4,5,6,7}
	String title = "Violin Plot Per Point Marker Settings"
	Display/W=(557,99,948,310)/N=ViolinPlotPerPointPlot as title
	
	// Create a trace named trace0 with three datasets: violin0, violin1, violin2
	AppendViolinPlot/TN=trace0 violin0,violin1,violin2
	
	// Set the marker and marker size for all datasets of trace trace0
	ModifyViolinPlot trace=trace0, dataMarker=18	// 18=Diamond
	ModifyViolinPlot trace=trace0, markerSize=5
	
	// Set the per-data-point marker for all datasets of trace trace0
	Make/O violinMarkers = {15,16,17,18,19}
	ModifyViolinPlot trace=trace0, dataMarkerWave=violinMarkers
		
	// Set the per-data-point marker for dataset violin1 only
	Make/O violinMarkersForViolin1 = {32,33,34,35,36}
	ModifyViolinPlot trace=trace0, dataMarkerWave[1]=violinMarkersForViolin1
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

### *Examples* {#examples}
A violin plot with transparent marker color used to give a visual indication of the density of data points.


```igor
// Create a violin plot with transparent marker color used to give
// a visual indication of the density of data points
Make/O/N=(25,3) multicol	// A three-column wave with 25 rows
SetRandomSeed(.4)	// for reproducible "randomness"
multicol = gnoise(1)	// Three normally-distributed data sets
multicol[20][1] = 5	// A "far" outlier
multicol[13][2] = -4	// An outlier
Display; AppendViolinPlot multicol
ModifyViolinPlot lineColor=(0,0,65535)
ModifyViolinPlot fillColor=(0,0,65535,19661)
ModifyViolinPlot jitter=0
ModifyViolinPlot showData=1
ModifyViolinPlot dataMarker=19
ModifyViolinPlot markerSize=6
ModifyViolinPlot markerColor=(0,0,65535,6554)
```

<img src="Images/ModifyViolinPlot/ModifyViolinPlot_8.png" width="75%"/>


```igor
ModifyViolinPlot fillColor[1]=(0,65535,0,19661)	// Second dataset transparent green
```



<img src="Images/ModifyViolinPlot/ModifyViolinPlot_1.png" width="75%"/>


```igor
// Add jitter, choose the circle-with-plus marker
ModifyViolinPlot trace=multicol,Jitter=0.7
ModifyViolinPlot trace=multicol,DataMarker=42,MarkerSize=5

// Set marker color to blue with a one-point outline
ModifyViolinPlot trace=multicol,MarkerColor=(16385,16388,65535)
ModifyViolinPlot trace=multicol,MarkerThick=1

// Set the marker to filled with dark green fill color
ModifyViolinPlot trace=multicol,MarkerFilled=1,MarkerFillColor=(3,52428,1)
```

<img src="Images/ModifyViolinPlot/ModifyViolinPlot_3.png" width="75%"/>


```igor
// Set a marker size wave for data set 0 (the first data set)
Make/N=25/O sizeWave = enoise(5)+7
ModifyViolinPlot DataSizeWave[0] = sizeWave
```

<img src="Images/ModifyViolinPlot/ModifyViolinPlot_0.png" width="75%"/>


```igor

// Create a violin plot with asymmetric curves plotted on a category axis
Make/O/N=(25,3) ds1, ds2
SetRandomSeed(.4)		// For reproducible "randomness"
ds1 = gnoise(1)
ds2 = gnoise(2)+q

// To make a category plot we need a text wave
Make/N=3/T/O labels={"treatment 1", "treatment 2", "treatment 3"}
Display
AppendViolinPlot ds1 vs labels
AppendViolinPlot ds2 vs labels

// Keep plots together in a single category space
ModifyGraph toMode(ds1)=-1

// Display ds1 on the left, ds2 on the right
ModifyViolinPlot trace=ds1,plotSide=1
ModifyViolinPlot trace=ds2,plotSide=2

// Extend the KDE curves
ModifyViolinPlot trace=ds1,CurveExtension=2
ModifyViolinPlot trace=ds2,CurveExtension=2

// Close the curves with line at the midline
ModifyViolinPlot trace=ds1,closeOutline=1
ModifyViolinPlot trace=ds2,closeOutline=1

// Use the same normalization for both curves
ModifyViolinPlot trace=ds1,maxDensity=0.36
ModifyViolinPlot trace=ds2,maxDensity=0.36

// Apply jitter to the data points
ModifyViolinPlot trace=ds1,jitter=0.5
ModifyViolinPlot trace=ds2,jitter=0.5

// Set markers and colors
ModifyViolinPlot trace=ds1,showData=1,dataMarker=16,markerColor=(2,39321,1),lineColor=(2,39321,1)
ModifyViolinPlot trace=ds2,showData=1,dataMarker=19,markerColor=(0,0,65535),lineColor=(0,0,65535)
ModifyViolinPlot trace=ds1,fillColor=(2,39321,1,19661)
ModifyViolinPlot trace=ds2,fillColor=(0,0,65535,19661)
```

<img src="Images/ModifyViolinPlot/ModifyViolinPlot_6.png" width="100%"/>

### *See Also* {#see-also}
[Violin Plots](/igorpro/graphing/graphs.md#violin-plots), [AppendViolinPlot](/igorpro/commands/appendviolinplot.md), [AddWavesToViolinPlot](/igorpro/commands/addwavestoviolinplot.md), [ModifyGraph](/igorpro/commands/modifygraph.md)