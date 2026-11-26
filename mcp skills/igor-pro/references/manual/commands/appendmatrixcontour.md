---
description: "The AppendMatrixContour operation appends to the target or named graph a contour of a matrix of z values with autoscaled contour levels, using the Rainbow…"
slug: /commands/appendmatrixcontour
---

<div className="command-signature">

## <strong>AppendMatrixContour</strong>  [<em>axisFlags</em> ][/W=<em>winName</em> /F=<em>formatStr</em> ] <em>zWave</em> [<em>vs</em> {<em>xWave</em>, <em>yWave</em> }] {#appendmatrixcontour}

</div>

The AppendMatrixContour operation appends to the target or named graph a contour of a matrix of z values with autoscaled contour levels, using the Rainbow color table.

:::note
There is no DisplayContour operation. Use `Display; AppendMatrixContour`.
:::

*zWave*  must be a matrix (2D wave).

To contour a set of XYZ triplets, use [AppendXYZContour](/igorpro/commands/appendxyzcontour.md).

If you provide the *xWave*  and *yWave*  specification, *xWave*  provides X values for the rows, and *yWave*  provides Y values for the columns. This implements an "uneven grid" of Z values.

If you omit the *xWave*  and *yWave*  specification, Igor uses the *zWave* 's X and Y scaled indices as the X and Y values. Igor also uses the *zWave* 's scaled indices if you use * (asterisk symbol) in place of *xWave*  or *yWave* .

In a macro, to modify the appearance of contour levels before the contour is calculated and displayed with the default values, append ";DelayUpdate" and immediately follow the AppendMatrixContour command with the appropriate [ModifyContour](/igorpro/commands/modifycontour.md) commands. All but the last ModifyContour command should also have ;DelayUpdate appended. DelayUpdate is not needed in a function, but DoUpdate is useful in a function to force the contour traces to be built immediately rather than the default behavior of waiting until all functions have completed.

On the command line, the Display command and subsequent AppendMatrixContour commands and any ModifyContour commands can be typed all on one line with semicolons between:


```igor
Display; AppendMatrixContour MyMatrix; ModifyContour ...
```

### *Flags* {#flags}

|  |  |
| --- | --- |
| *axisFlags* | Flags /L/R/B/T are the same as used by [AppendToGraph](/igorpro/commands/appendtograph.md). |
| <span class="table-cell-nowrap">/F = *formatStr*</span> | Determines the names that Igor will assign to the contour level traces. See details below. |
| <span class="table-cell-nowrap">/W = *winName*</span> | Appends to the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
AppendMatrixContour creates and displays contour level traces. You can modify these all together using the Modify Contour Appearance dialog or individually using the Modify Trace Appearance dialog. In most cases, you will have no need to modify the traces individually.

By default, Igor automatically names the contour level traces with names that show the *zWave*  and the contour level, for example, "zWave=1.5". You will see these trace names in the Modify Trace Appearance dialog and in Legends. In most cases, the default trace names will be just fine.

If you want to control the names of the contour level traces (which you might want to do for names in a Legend), use the /F=*formatStr*  flag. This flag uses a format string as described for the [printf](/igorpro/commands/printf.md) operation. The default format string is "%.17s=%g", resulting in trace names such as "zwave=1.5". *formatStr*  must contain at least %f or %g (used to insert the contour level) or %d (used to insert the zero-based index of the contour level). Include %s, to insert the *zWave*  name.

Here are some examples of format strings.


| formatStr | Examples of Resulting Name | Format |
| --- | --- | --- |
| "%g" | "100", "1e6", "-2.05e-2" | (\<level\>) |
| <span class="table-cell-nowrap">"z = %g"</span> | "z=100","z=1e6", "z=-2.05e-2" | (z=\<level\>) |
| "%s %f" | "zWave 100.000000" | (\<wave\>, space, \<level\>) |
| <span class="table-cell-nowrap">"[%d] = %g"</span> | "[0]=100", "[1]=1e6" | ([\<index\>]=\<level\>) |

### *Examples* {#examples}

```igor
Make/O/N=(25,25) w2D                    // Make a matrix
SetScale x -1, 1, w2D                   // Set row scaling
SetScale y -1, 1, w2D                   // Set column scaling
w2D = sin(x) * cos(y)                   // Store values in the matrix
Display; AppendMatrixContour w2D; DelayUpdate
ModifyContour w2D autoLevels={*,*,9}    // roughly 9 automatic levels
```

### *See Also* {#see-also}
[Display](/igorpro/commands/display.md), [AppendToGraph](/igorpro/commands/appendtograph.md), [AppendXYZContour](/igorpro/commands/appendxyzcontour.md), [ModifyGraph](/igorpro/commands/modifygraph.md), [ModifyContour](/igorpro/commands/modifycontour.md), [FindContour](/igorpro/commands/findcontour.md)

[Contour Plots](/igorpro/graphing/contour-plots.md)

### *Demos* {#demos}
[Open Contour Demo](#igor-pxp/Examples/Sample__Graphs/Contour__Demo.pxp)