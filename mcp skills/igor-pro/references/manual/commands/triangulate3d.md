---
description: "The Triangulate3D operation creates a Delaunay \"triangulation\" of a 3D scatter wave."
slug: /commands/triangulate3d
---

<div className="command-signature">

## <strong>Triangulate3D</strong>  [/OUT=<em>format</em> ] <em>srcWave</em> {#triangulate3d}

</div>

The Triangulate3D operation creates a Delaunay "triangulation" of a 3D scatter wave. The output is a list of tetrahedra that completely span the convex volume defined by *srcWave*. Triangulate3D can also generate the triangulation needed for performing 3D interpolation for the same domain. Normally *srcWave*  is a triplet wave (a 2D wave of 3 columns), but can use any 2D wave that has more than 3 columns (the operation ignores all but the first 3 columns).

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DSTI = *iWave*</span> | Specify the destination wave for the 9-column triangulation data wave.  If you do not specify this flag, the operation saves the output in the wave M_3DTriData in the current data folder.  Note that this wave is useful for diagnostics only. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTP = *pWave*</span> | Specify the destination wave for the tetrahedra path triplet wave.  If you do not specify this flag, the operation saves the output in the wave M_TetraPath in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTV = *vWave*</span> | Specify the destination wave for the vertex list.  If you do not specify this flag, the operation saves the output in the wave M_3DVertexList in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all user-specified destination waves as free waves. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/OUT = *format*</span> | Specifies how the output triangulation data are saved. |
|  |<table class="nested-table"><tbody><tr><td>*format*&nbsp;=1:</td><td>Default; saves the triangulation result in the wave M_3DVertexList, which contains in each row, indices to rows in *srcWave*  that describe the X, Y, Z coordinates of a single tetrahedral vertex. Each tetrahedron is described by one row in M_3DVertexList.</td></tr><tr><td>*format*&nbsp;=2:</td><td>Saves the triangulation result in the wave M_TetraPath, which is a triplet path wave describing the tetrahedra edges. For each tetrahedron, there are four rows (triangles) separated by row of NaNs. The total number of rows in M_TetraPath is 20 times the number of tetrahedra in the triangulation.</td></tr><tr><td>*format*&nbsp;=4:</td><td>Saves a wave containing internal diagnostic information generated during the triangulation process.</td></tr></tbody></table>
|  | <div><Admonition type="note"><p>*format* consists of binary flags that can be combined to output any combination of the waves: M_3DTriData, M_3DVertexList and M_TetraPath.</p></Admonition></div> |
| <span class="table-cell-nowrap">/VOL</span> | Computes the volume of the full convex hull by summing the volumes of the tetrahedra generated in the triangulation. The result is stored in the variable V_value. This flag requires Igor Pro 7.00 or later. |

### *Details* {#details}
The operation is an implementation of Watson's algorithm for tetrahedralization of a set of points in three dimensions. It starts by creating a very large tetrahedron which inscribes all the data points followed by a sequential insertion of one datum at a time. With each new datum the algorithm finds the tetrahedron in which the datum falls. It then proceeds to subdivide the tetrahedron so that the datum becomes a vertex of new tetrahedra.

The algorithm suffers from two known problems. First, it may, due to numerical instabilities, result in tetrahedra that are too thin. You can get around this problem by introducing a slight random perturbation in the input wave. For example:


```igor
srcWave+=enoise(amp)
```

Here amp is chosen so that it is much smaller than the smallest cartesian distance between two input points.

The second problem has to do with memory allocations which may exhaust available memory for some pathological spatial distributions of data points. The operation reports both problems in the history area.

### *Examples* {#examples}

```igor
Make/O/N=(10,3) ddd=gnoise(5)	// create random 10 points in space
Triangulate3D/out=2  ddd

// now display the triangulation in Gizmo:
Window Gizmo0() : GizmoPlot
	PauseUpdate; Silent 1 
	if(exists("NewGizmo")!=4)
		DoAlert 0, "Gizmo XOP must be installed"
		return
	endif
	NewGizmo/N=Gizmo0 /W=(309,44,642,373)
	ModifyGizmo startRecMacro
	ModifyGizmo scalingMode=2
	AppendToGizmo Scatter=root:ddd,name=scatter0
	ModifyGizmo ModifyObject=scatter0 property={ scatterColorType,0}
	ModifyGizmo ModifyObject=scatter0 property={ Shape,2}
	ModifyGizmo ModifyObject=scatter0 property={ size,0.2}
	ModifyGizmo ModifyObject=scatter0 property={ color,0,0,0,1}
	AppendToGizmo Path=root:M_TetraPath,name=path0
	ModifyGizmo ModifyObject=path0 property={ pathColor,0,0,1,1}
	ModifyGizmo setDisplayList=0, object=scatter0
	ModifyGizmo setDisplayList=1, object=path0
	ModifyGizmo autoscaling=1
	ModifyGizmo compile
	ModifyGizmo endRecMacro
End
```

### *References* {#references}
Watson, D.F., Computing the n-dimensional Delaunay tessellation with application to Voronoi polytopes, *The Computer J.*, *24*, 167-172, 1981.

Additional information about this algorithm can be found in:

Watson, D.F., *CONTOURING: A guide to the analysis and display of spatial data*, Pergamon Press, 1992.

### *See Also* {#see-also}
[Interpolate3D](/igorpro/commands/interpolate3d.md), [Interp3D](/igorpro/commands/interp3d.md)