---
description: "The BezierToPolygon operation creates an XY pair of waves approximating the Bezier curves described by bezXWave and bezYWave."
slug: /commands/beziertopolygon
---

<div className="command-signature">

## <strong>BezierToPolygon</strong>  [ /DSTX=<em>destXWave</em> /DSTY=<em>dstYWave</em> /FREE /NSEG=<em>nseg</em> ] <em>bezXWave</em>, <em>bezYWave</em> {#beziertopolygon}

</div>

The BezierToPolygon operation creates an XY pair of waves approximating the Bezier curves described by *bezXWave* and *bezYWave*.

The BezierToPolygon operation was added in Igor Pro 9.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTX = *destX*</span> | Specifies the X destination wave to be created or overwritten. If you omit /DSTX, *destX* defaults to W_PolyX. |
| <span class="table-cell-nowrap">/DSTY = *destY*</span> | Specifies the Y destination wave to be created or overwritten. If you omit /DSTY, *destY* defaults to W_PolyY. |
| <span class="table-cell-nowrap">/FREE</span> | Creates output waves as free waves (see [Free Waves](/igorpro/programming/programming.md#free-waves)). |
|  | /FREE is allowed only in functions. If you use /DSTX or /DSTY then the specified parameter must be either a simple name or a valid wave reference. |
| <span class="table-cell-nowrap">/NSEG = *nseg*</span> | The number of segments used to render each Bezier segment from 1 and 500. The default of 20 is usually sufficient. |

### *Details* {#details}
The Bezier waves *bezXWave* and *bezYWave* must be 1-dimensional real-valued floating point waves of the same length and type.

Each Bezier curve is a minimum of 1 segment comprised of 4 XY pairs. A Bezier curve of *n* segments consists of 1 + *n* * 3 XY pairs.

*bezXWave* and *bezYWave* may have NaN values between Bezier segments but not within a segment. BezierToPolygon issues an error at runtime if the data in the input waves does not conform to these requirements. NaNs in the input waves are copied to the polygon output waves.

If you omit /DSTX the output polygon X data is written to W_PolyX in the current data folder. If you omit /DSTY the output polygon Y data is written to W_PolyY in the current data folder. The output waves are created or redimensioned as single-precision or double-precision floating point waves to match the type of *bezXWave* and *bezYWave*.

### *Example* {#example}

```igor
Function DemoBezierToPolygon()
	Make/O wx={0.5, 0.6, 0.9, 1}
	Make/O wy={0.0, 0.2, 0.5, 0.1}
	BezierToPolygon wx,wy
	Execute "BezierToPolygonExample()"
End

Window BezierToPolygonExample() : Graph
	PauseUpdate; Silent 1
	Display /W=(237,45,1419,669)/K=1  wy vs wx
	AppendToGraph W_PolyY vs W_PolyX
	ModifyGraph expand=-3
	ModifyGraph mode(wy)=4
	ModifyGraph marker(wy)=19
	ModifyGraph rgb(wy)=(1,16019,65535)
	Legend/C/N=text0/J/X=15.66/Y=68.34 "\\s(wy)\\[1 Bezier Control Points"
	AppendText "\\K(48059,48059,48059)\\y+15\\L1700\\X1\\M\\K(0,0,0) DrawBezier \n\\s(W_PolyY) Polygon Approximation to Bezier"
	SetDrawLayer UserBack
	SetDrawEnv xcoord= bottom,ycoord= left,save
	SetDrawEnv linethick= 3,linefgc= (48059,48059,48059)
	DrawBezier wx[0],wy[0],1,1,wx,wy
	SetDrawLayer UserFront
EndMacro
```

### *See Also* {#see-also}
[DrawBezier](/igorpro/commands/drawbezier.md), [DrawPoly](/igorpro/commands/drawpoly.md), [Drawing Polygons and Bezier Curves](/igorpro/graphing/drawing.md#drawing-polygons-and-bezier-curves)