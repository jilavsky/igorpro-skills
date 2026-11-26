---
description: "The AppendXYZContour operation appends to the target or named graph a contour of a 2D wave consisting of XYZ triples with autoscaled contour levels and using…"
slug: /commands/appendxyzcontour
---

<div className="command-signature">

## <strong>AppendXYZContour</strong>  [<em>axisFlags</em> ][/W=<em>winName</em> /F=<em>formatStr</em> ] <em>zWave</em> [<em>vs</em> {<em>xWave</em>, <em>yWave</em> }] {#appendxyzcontour}

</div>

The AppendXYZContour operation appends to the target or named graph a contour of a 2D wave consisting of XYZ triples with autoscaled contour levels and using the Rainbow color table.

To contour a matrix of Z values, use [AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md).

:::note
There is no DisplayContour operation. Use Display; AppendXYZContour.
:::

If you provide the *xWave*  and *yWave*  specification, *xWave*  provides X values for the rows, and *yWave*  provides Y values for the columns, *zWave*  provides Z values and all three waves must be 1D. All must have at least four rows and must have the same number of rows.

If you omit the *xWave*  and *yWave*  specification, *zWave*  must be a 2D wave with 4 or more rows and 3 or more columns. The first column is X, the second is Y, and the third is Z. Any additional columns are ignored.

If any of X, Y, or Z in a row is blank (NaN), that row is ignored.

In a macro, to modify the appearance of contour levels before the contour is calculated and displayed with the default values, append ";DelayUpdate" and immediately follow the AppendXYZContour command with the appropriate [ModifyContour](/igorpro/commands/modifycontour.md) commands. All but the last ModifyContour command should also have ;DelayUpdate appended. DelayUpdate is not needed in a function, but DoUpdate is useful in a function to force the contour traces to be built immediately rather than the default behavior of waiting until all functions have completed.

On the command line, the Display command and subsequent AppendXYZContour commands and any ModifyContour commands can be typed all on one line with semicolons between:


```igor
Display; AppendXYZContour zWave; ModifyContour ...
```

### *Flags* {#flags}

|  |  |
| --- | --- |
| *axisFlags* | Flags /L/R/B/T are the same as used by [AppendToGraph](/igorpro/commands/appendtograph.md). |
| <span class="table-cell-nowrap">/F = *formatStr*</span> | Determines the names assigned to the contour level traces. This is the same as for [AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md). |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to the named graph window or subwindow. When omitted, action is directed to the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
AppendXYZContour creates and displays contour level traces. You can modify these as a group using the Modify Contour Appearance dialog or individually using the Modify Trace Appearance dialog. In most cases, you will have no need to modify the traces individually.

See [AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md) for a discussion of how the contour level traces are named.

### *Examples* {#examples}

```igor
Make/O/N=(100) xW, yW, zW                   // Make X, Y and Z waves
xW = sawtooth(2*PI*p/10)                    // Generate X values
yW = trunc(p/10)/10                         // Generate Y values
zW = sin(2*PI*xW)*cos(2*PI*yW)              // Generate Z values
Display; AppendXYZContour zW vs {xW, yW}
ModifyContour zW autoLevels={*,*,9}         // Roughly 9 automatic levels
```

### *See Also* {#see-also}
[Display](/igorpro/commands/display.md), [AppendToGraph](/igorpro/commands/appendtograph.md), [ModifyGraph](/igorpro/commands/modifygraph.md), [ModifyContour](/igorpro/commands/modifycontour.md), [AppendMatrixContour](/igorpro/commands/appendmatrixcontour.md)

[Contour Plots](/igorpro/graphing/contour-plots.md)

### *Demos* {#demos}
[Open Contour Demo](#igor-pxp/Examples/Sample__Graphs/Contour__Demo.pxp)