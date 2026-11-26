# Igor Pro — Graphs: axes, traces, styling, queries

Read this before creating or modifying any graph (`Display`, `AppendToGraph`, `ModifyGraph`,
`Label`, `SetAxis`, `ErrorBars`, `Legend`, `NewImage`). When a flag is not listed here,
call `Igor__get_help` with the operation name - do not guess.

## 1. Axis names - there is no "x" or "y" axis

Igor axes are named by **position**, not by data dimension:

| Axis | Name | Created by |
|---|---|---|
| default vertical (Y) | `left` | `Display` / `AppendToGraph` (default) |
| default horizontal (X) | `bottom` | `Display` / `AppendToGraph` (default) |
| right vertical | `right` | `AppendToGraph/R` |
| top horizontal | `top` | `AppendToGraph/T` |
| free axis | any name you choose | `AppendToGraph/L=myAxis` or `/B=myAxis`, or `NewFreeAxis` |

```igor
Label/W=G1 bottom "Q [Å\\S-1\\M]"        // NOT: Label x "..."
Label/W=G1 left "Intensity [cm\\S-1\\M]" // NOT: Label y "..."
ModifyGraph/W=G1 log(left)=1, log(bottom)=1
SetAxis/W=G1 bottom 0.001, 0.5
SetAxis/W=G1/A left                      // autoscale one axis
SetAxis/W=G1/A                           // autoscale all axes
```

`X`/`Y` *do* appear in other places - do not confuse them with axis names:
- `ErrorBars traceName,Y wave=(...)` - `X`/`Y`/`XY` here is the error-bar *direction*.
- `GetAxis/W=G1/Q left` returns `V_min`, `V_max` - still uses the axis name.
- In `NewImage` plots the image axes are `left` (reversed, so pictures are right-side-up) and **`top`**;
  `AppendImage` uses `left`/`bottom` by default.

Use `AxisList("G1")` to see which axes a graph really has.

## 2. Creating graphs - always name the window and target it

```igor
KillWindow/Z G1                              // makes the command safe to re-run
Display/N=G1/K=1 yW vs xW                    // XY pair: Y wave first, then vs X wave
AppendToGraph/W=G1 y2 vs x2
AppendToGraph/W=G1/R ratioW vs xW            // on the right axis
Display/N=G2/K=1 w1                          // waveform plot: X comes from w1's scaling
```

- `vs` is required for XY data. Without it, X comes from the Y wave's own X scaling
  (`SetScale`), not from another wave.
- `/K=1` = close window without the "save recreation macro" dialog.
- If a window named `G1` already exists, `Display/N=G1` does **not** reuse it; Igor tries `G10`,
  `G11`, ... and stores the chosen name in `S_name`. Kill it first (`KillWindow/Z G1`) or check
  with `WinType("G1")` (0 = no such window).
- `/W=(left,top,right,bottom)` on `Display` sets window position/size in points.
- Every `ModifyGraph`, `Label`, `SetAxis`, `ErrorBars`, `Legend`, `RemoveFromGraph` in code should
  carry `/W=graphName`; otherwise it acts on whatever graph is on top.

## 3. Trace names

- The trace name is the **Y wave's name** (not the path, not the X wave).
- The same wave appended twice gives `yW` and `yW#1`; use the instance suffix in
  `ModifyGraph rgb(yW#1)=...`.
- Give a trace an explicit name with `/TN=` after the wave: `AppendToGraph/W=G1 yW/TN=fit vs xW`.
- Waves from different data folders with the same name get `#1`, `#2`... - check with
  `TraceNameList("G1", ";", 1)` rather than assuming.
- Trace -> wave: `TraceNameToWaveRef("G1", "yW")`, `XWaveRefFromTrace("G1", "yW")`.

## 4. ModifyGraph syntax

`ModifyGraph/W=G1 keyword(traceOrAxisName)=value, keyword2(name)=value2`

- Name in parentheses = apply to that one trace or axis. **No parentheses = apply to all**
  traces (or all axes, for axis keywords).
- Colors are 16-bit: `rgb(yW)=(65535,0,0)`; optional 4th value is alpha (0-65535).

| Want | Keyword (example) |
|---|---|
| markers only / lines / lines+markers | `mode(yW)=3` / `mode(yW)=0` / `mode(yW)=4` |
| marker shape, size | `marker(yW)=19`, `msize(yW)=3` (19 = filled circle, 8 = open circle) |
| line width, dash | `lsize(yW)=2`, `lstyle(yW)=3` |
| color | `rgb(yW)=(0,0,65535)` |
| log axis | `log(left)=1` |
| ticks inside, mirror axes | `tick=2`, `mirror=1` |
| minor ticks | `minor=1` |
| font size of tick labels | `fSize=12` |
| axis label gap | `lblMargin(left)=5`, `standoff=0` |
| fixed plot-area size (points) | `width=400, height=300`; `width=0` returns to auto |
| hide an axis | `noLabel(right)=2, axThick(right)=0` |

## 5. Labels, legends, text

- Escape codes inside label/annotation text (write `\\` inside a string literal in procedures):
  `\\S` superscript, `\\B` subscript, `\\M` back to normal, `\\Z14` font size 14,
  `\\f01` bold.
- `Legend/W=G1/C/N=legend0/A=RT` - `/C` changes an existing annotation with that name, `/A=` anchor
  (LT, RT, LB, RB, MC ...). Legend text can reference traces with `\\s(traceName)`.
- Free text: `TextBox/W=G1/C/N=note0/A=LT "text"`.

## 6. Error bars

```igor
ErrorBars/W=G1 yW,Y wave=(dyW,dyW)                  // +/- from wave dyW on trace yW
ErrorBars/W=G1 yW,XY wave=(dxW,dxW), wave=(dyW,dyW)
ErrorBars/W=G1 yW,OFF
```
Syntax: `ErrorBars traceName, mode errorSpec` - comma after the **trace name**, then the mode
(`X`, `Y`, `XY`, `OFF`...), a space, then `wave=(plusWave, minusWave)`.

## 7. Querying a graph

| Need | Use |
|---|---|
| top graph's name | `WinName(0, 1)` |
| does window exist | `WinType("G1")` (1 = graph) |
| traces on graph | `TraceNameList("G1", ";", 1)` |
| axes on graph | `AxisList("G1")` |
| current axis range | `GetAxis/W=G1/Q bottom` -> `V_min`, `V_max` |
| trace/axis settings | `TraceInfo("G1", "yW", 0)`, `AxisInfo("G1", "left")` |

## 8. Removing, killing, exporting

```igor
RemoveFromGraph/W=G1/Z yW
KillWindow/Z G1
SavePICT/W=G1/O/E=-5/B=144 as "graph.png"   // /E=-5 PNG, -8 PDF, -9 SVG
```

## 9. Images

```igor
NewImage/N=Img1/K=1 matrixW                  // axes: left + top
Display/N=Img2/K=1; AppendImage/W=Img2 matrixW // axes: left + bottom
ModifyImage/W=Img2 matrixW ctab={*,*,Rainbow,0}, log=1
```
The image *instance* name for `ModifyImage` is the matrix wave's name.

## Reference URLs
- https://docs.wavemetrics.com/igorpro/commands/modifygraph
- https://docs.wavemetrics.com/igorpro/commands/display
- https://docs.wavemetrics.com/igorpro/commands/label
