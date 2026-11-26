---
description: "The SphericalTriangulate operation triangulates an arbitrary x, y, z triplet wave on a surface of a sphere."
slug: /commands/sphericaltriangulate
---

<div className="command-signature">

## <strong>SphericalTriangulate</strong>  [/Z] <em>tripletWaveName</em> {#sphericaltriangulate}

</div>

The SphericalTriangulate operation triangulates an arbitrary x, y, z triplet wave on a surface of a sphere.

It starts by normalizing the data to make sure that sqrt(x^2+y^2+z^2)=1, and then proceeds to calculate the Delaunay triangulation.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Saves the computed Delaunay triangulation in the wave M_SphericalDelaunay in the current data folder or in a destination specified by /DSTD. The output is a triplet wave consisting of vertices on the surface of the sphere. See also /DANG for setting the resolution of the output paths. |
| <span class="table-cell-nowrap">/DANG = *dAngle*</span> | Sets the resolution of line segments in the Voronoi and Delaunay paths. By default, line segments are generated using a differential angle of 0.1 radian. You can set the differential angle to a smaller value to increase the resolution and generate smoother paths on the surface of the sphere.<br>This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTD = *dWave*</span> | Specify the destination wave for the Delaunay triangulation path. If you do not specify this flag, the output is saved in the wave M_SphericalDelaunay in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTT = *tWave*</span> | Specify the destination wave for the triangulation output (the wave used in SphericalInterpolate). If you do not specify this flag, the triangulation output is saved in the wave M_TriangulationData in the current data folder. |
|  | This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTV = *vWave*</span> | Specify the output wave for the Voronoi tesselation path. If you do not specify this flag, the output is saved in the wave  M_SphericalVoronoi in the current data folder.<br>This flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves. This flag does not affect any of the output waves that are created by default without a user-specified destination. |
|  | /FREE is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/V</span> | Saves the computed Voronoi tesselation. The output is a triplet wave consisting of vertices along the path of the Voronoi polygons on the surface of the sphere. The data is saved in the wave M_SphericalVoronoi. See also /DANG for setting the resolution of the path. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The result of the triangulation is the wave M_SphericalTriangulation. This 13 column wave is used in SphericalInterpolate to obtain the interpolated values.

### *Example* {#example}

```igor
// This function generates output waves that can be used in Gizmo to display the triangulation.
// The triangulationData parameter is the M_TriangulationData output from the SphericalTriangulation operation.
// The tripletWave parameter is the source wave input to the SphericalTriangulation operation. 
// The output wave sphereTrianglesPath can be used to display the triangulation as a path object.
// The output wave sphereTrianglesSurf can be used to display the triangulation as a surface object. 
Function BuildTriangleWaves(triangulationData,tripletWave)
	Wave triangulationData, tripletWave
	
	// Extract 3 columns from triangulationData that contain the index of the row.
	Duplicate/O/FREE/r=[][1,3] triangulationData,triIndices
	Variable finalNumTriangles=dimSize(triIndices,0),i,j,k

	// Initialize both waves to NaN so any unassigned point would appear as a hole.
	Make/O/N=(5*finalNumTriangles,3) sphereTrianglesPath=NaN
	Make/O/N=(3*finalNumTriangles,3) sphereTrianglesSurf=NaN
	
	// Assign the values of the vertices to the two waves:
	Variable rowIndex,rowIndex0,outRowCount=0,outcount2=0
	for(i=1;i<finalNumTriangles;i+=1)
		for(j=0;j<3;j+=1)
			rowIndex=triIndices[i][j]
			for(k=0;k<3;k+=1)
				sphereTrianglesPath[outRowCount][k]=tripletWave[rowIndex][k]
				sphereTrianglesSurf[outcount2][k]=tripletWave[rowIndex][k]
			endfor
			outRowCount+=1
			outcount2+=1
		endfor

		// Close the triangle path by returning to the first vertex:
		rowIndex0=triIndices[i][0]
		sphereTrianglesPath[outRowCount][0]=tripletWave[rowIndex0][0]
		sphereTrianglesPath[outRowCount][1]=tripletWave[rowIndex0][1]
		sphereTrianglesPath[outRowCount][2]=tripletWave[rowIndex0][2]
		outRowCount+=2	// Increment row count and skip the NaN
	endfor
End
```

### *See Also* {#see-also}
[SphericalInterpolate](/igorpro/commands/sphericalinterpolate.md), [Triangulate3D](/igorpro/commands/triangulate3d.md), [ImageInterpolate](/igorpro/commands/imageinterpolate.md) with keyword Voronoi

### *Demo* {#demo}
[Open Spherical Triangulation Demo](#igor-pxp/Examples/Analysis/SphericalTriangulationDemo.pxp)