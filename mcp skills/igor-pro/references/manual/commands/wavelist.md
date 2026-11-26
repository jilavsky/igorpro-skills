---
description: "The WaveList function returns a string containing a list of wave names selected from the current data folder or the data folder specified by dfr based on…"
slug: /commands/wavelist
---

<div className="command-signature">

## <strong>WaveList</strong> (<em>matchStr</em>, <em>separatorStr</em>, <em>optionsStr</em> [, <em>dfr</em>]) {#wavelist}

</div>

The WaveList function returns a string containing a list of wave names selected from the current data folder or the data folder specified by *dfr* based on *matchStr* and *optionsStr*.  The *dfr* parameter requires Igor Pro 9.00 or later.

See details below for information on listing waves in graphs, and for references to newer, data folder-aware functions.

### *Details* {#details}
For a wave name to appear in the output string, it must match *matchStr* and also must fit the requirements of *optionsStr* and it must be in the current data folder. *separatorStr* is appended to each wave name as the output string is generated.

The name of each wave is compared to *matchStr*, which is some combination of normal characters and the asterisk wildcard character that matches anything. For example:

|  |  |
| --- | --- |
| "*" | Matches all wave names in current data folder. |
| "xyz" | Matches wave name xyz only. |
| "\*xyz" | Matches wave names which end with xyz. |
| "xyz\*" | Matches wave names which begin with xyz. |
| "\*xyz\*" | Matches wave names which contain xyz. |
| "abc\*xyz" | Matches wave names which begin with abc and end with xyz. |
| *matchStr* may begin with the "!" character to return items that do not match the rest of *matchStr*. For example: |  |
| "!\*xyz" | Matches wave names which do not end with xyz. |

The "!" character is considered to be a normal character if it appears anywhere else, but there is no practical use for it except as the first character of *matchStr*.

*optionsStr* is used to further qualify the wave.

Use "" to accept all waves in the current data folder that are permitted by *matchStr*.

Set *optionsStr* to one or more of the following comma-separated keyword-value pairs to limit the waves to those meeting the specified criteria:


|  |  |
| --- | --- |
| "DIMS:*numberOfDims*" |  |
|  | Consider all waves in the current data folder that have *numberOfDims* dimensions. This is number of dimensions reported by [WaveDims](/igorpro/commands/wavedims.md). Use "DIMS:1" for graph traces (or one of the X, Y, and Z waves of a contour plot), "DIMS:2" for false color and indexed color images (see [Indexed Color Details](/igorpro/graphing/image-plots.md#indexed-color-details)), and "DIMS:3" for direct color images (see [Direct Color Details](/igorpro/graphing/image-plots.md#direct-color-details)). |
| "BYTE:0" *or* "BYTE:1" |  |
|  | Consider waves that are not 8-bit integer (if 0) or only waves that are 8-bit integer (if 1). |
| "CMPLX:0" *or* "CMPLX:1" |  |
|  | Consider waves that are not complex (if 0) or only waves that are complex (if 1). |
| "DF:0" *or* "DF:1" |  |
|  | Consider waves that are not data folder reference waves (if 0) or only waves that are data folder reference waves (if 1). You can create waves that contain data folder references using the Make /DF flag. |
| "DP:0" *or* "DP:1" | Consider waves that are not double precision floating point (if 0) or only waves that are double precision floating point (if 1). |
| "INT64:0" *or* "INT64:1" |  |
|  | Consider waves that are not 64-bit integer (if 0) or only waves that are 64-bit integer (if 1). 64-bit integer waves are supported in Igor 7 and later. |
| "INTEGER:0" *or* "INTEGER:1" |  |
|  | Consider waves that are not 32-bit integer (if 0) or only waves that are 32-bit integer (if 1). |
| "MAXCHUNKS:*max*" | Consider waves that have no more than *max* chunks. |
| "MAXCOLS:*max*" | Consider waves that have no more than *max* columns. |
| "MAXLAYERS:*max*" | Consider waves that have no more than *max* layers. |
| "MAXROWS:*max*" | Consider waves that have no more than *max* rows. |
| "MINCHUNKS:*min*" | Consider waves that have at least *min* chunks. |
| "MINCOLS:*min*" | Consider waves that have at least *min* columns. |
| "MINLAYERS:*min*" | Consider waves that have at least *min* layers. |
| "MINROWS:*min*" | Consider waves that have at least *min* rows. |
| "SP:0" *or* "SP:1" | Consider waves that are not single precision floating point (if 0) or only waves that are single precision floating point (if 1). |
| "TEXT:0" *or* "TEXT:1" |  |
|  | Consider waves that are not text (if 0) or only waves that are text (if 1). |
| "UNSIGNED:0" *or* "UNSIGNED:1" |  |
|  | Consider waves that are not unsigned integer (if 0) or only waves that are unsigned integer (if 1). |
| "WAVE:0" *or* "WAVE:1" |  |
|  | Consider waves that do not contain wave references (if 0) or only waves that contain wave references (if 1). You can create waves that contain wave references using the [Make](/igorpro/commands/make.md) /WAVE flag. |
| "WIN:" | Consider all waves in the current or specified data folder that are displayed in the top graph or table. The WIN option is not threadsafe. |
| "WIN:*windowName*" | Consider all waves in the current or specified data folder that are displayed in the named table or graph window or subwindow. The WIN option is not threadsafe. |
| "WORD:0" *or* "WORD:1" |  |
|  | Consider waves that are not 16-bit integer (if 0) or only waves that are 16-bit integer (if 1). |

You can specify more than one option by separating the options with a comma: see the Examples, below.

:::note
Even when optionsStr  is used to list waves used in a graph or table, the waves must be in the current data folder.
:::

:::note
In addition to waves displayed as normal graph traces, WaveList will list matrix waves used with AppendImage or NewImage and the X, Y, and Z waves used with AppendXYZContour.
:::

:::note
Individual contour traces are not listed because they have no corresponding waves. See Contour Traces.
:::

WaveList with WIN:*windowName* gives only the names of the waves in the graph or table and does not include the data folder for each wave. If you need to know what data folder the waves are in, use [WaveRefIndexed](/igorpro/commands/waverefindexed.md) to get the wave itself and then if needed use [GetWavesDataFolder](/igorpro/commands/getwavesdatafolder.md) to get the path.

When identifying a subwindow with WIN:*windowName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy.

To list the actual waves used in a graph, or to distinguish two or more instances of the same named wave in a graph, use [TraceNameList](/igorpro/commands/tracenamelist.md). This function can be used in conjunction with [TraceNameToWaveRef](/igorpro/commands/tracenametowaveref.md), and [XWaveRefFromTrace](/igorpro/commands/xwavereffromtrace.md).

Use [ContourNameList](/igorpro/commands/contournamelist.md) to list contour plots in a given window and [ContourNameToWaveRef](/igorpro/commands/contournametowaveref.md) to access the waves used to generate the contour plot.

To list the contour traces (that is, the contours themselves) use [TraceNameList](/igorpro/commands/tracenamelist.md) with the appropriate option.

Use [ImageNameList](/igorpro/commands/imagenamelist.md) to list images in a given window and [ImageNameToWaveRef](/igorpro/commands/imagenametowaveref.md) to access the waves used to generate the images.

### *Processing Lists of Waves* {#processing-lists-of-waves}
Contrary to what you might expect, you cannot use the output of WaveList directly with operations that have a list of waves as their parameters. See [Processing Lists of Waves](/igorpro/programming/programming-techniques.md#processing-lists-of-waves) for ways of dealing with this.

### *Examples* {#examples}

```igor
// Returns a list of all waves in the current data folder.
WaveList("*",";","")

// Returns a list of all waves in the current data folder
// and displayed in the top table or graph.
WaveList("*", ";","WIN:")

// Returns a list of waves in the current data folder whose names
// end in "_bkg" and which are displayed in Graph0 as a trace, image,
// or contour.
WaveList("*_bkg", ";", "WIN:Graph0")

// Returns a list of waves in the current data folder whose names do
// not end in "X" and which are displayed in Graph0 as 1D traces or
// as one of the X, Y, and Z waves of an AppendXYZContour plot.
WaveList("!*X", ";", "WIN:Graph0,DIMS:1")

// Returns a list of waves in the root:Packages:MyPackage data folder
WaveList("*", ";", "", root:Packages:MyPackage)
```

### *See Also* {#see-also}
[Multidimensional Waves](/igorpro/igor-basics/multidimensional-waves.md)

[Execute](/igorpro/commands/execute.md), [ContourNameList](/igorpro/commands/contournamelist.md), [ImageNameList](/igorpro/commands/imagenamelist.md), [StringFromList](/igorpro/commands/stringfromlist.md), [TraceNameList](/igorpro/commands/tracenamelist.md), [WaveRefIndexed](/igorpro/commands/waverefindexed.md)