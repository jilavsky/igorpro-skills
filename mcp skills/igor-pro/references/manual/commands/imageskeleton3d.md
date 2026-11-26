---
description: "ImageSkeleton3D computes the skeleton of a 3D binary object in srcWave using a thinning algorithm."
slug: /commands/imageskeleton3d
---

<div className="command-signature">

## <strong>ImageSkeleton3D</strong>  [<em>Flags</em> ] <em>srcWave</em> {#imageskeleton3d}

</div>

ImageSkeleton3D computes the skeleton of a 3D binary object in *srcWave* using a thinning algorithm. One approach to thinning is a layer-by-layer erosion until only the "skeleton" of an object remains. Other methods include 3D template matching to remove voxels that do not belong to the skeleton.

ImageSkeleton3D was added in Igor Pro 7.00.

### *Parameters* {#parameters}
*srcWave* is a 3D unsigned-byte wave where object voxels are set to 1 and background voxels are set to 0.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DEST = *destWave*</span> |  |
|  | Specifies the wave to contain the output of the operation. If the specified wave already exists, it is overwritten. If this flag is not specified, the operation saves the output in the wave M_Skeleton in the current data folder. |
|  | When used in a user-defined function, ImageSkeleton3D creates a wave reference for *destWave* if it is a simple name. See [Automatic Creation of Wave References](/igorpro/programming/programming.md#automatic-creation-of-wave-references) for details. |
|  | If you omit /DEST, the output wave is M_Skeleton in the current data folder. |
| <span class="table-cell-nowrap">/DSTL = *dstL*</span> | Specifies the wave to contain lengths of the segments computed in method 2. If this flag is not used, the operation saves the lengths data in the wave W_segmentLength in the current data folder. |
|  | The /DSTL flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/DSTP = *dstP*</span> | Specifies the wave to contain the 3D paths segments computed in method 2. If this flag is not used, the operation saves the lengths wave in M_SkeletonPath in the current data folder. |
|  | The /DSTP flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/FREE</span> | Creates the destination waves as free waves. |
|  | /FREE is allowed only in functions and only if the destiion wave name is a simple name or wave reference structure field. |
|  | See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/METH = *m*</span> | Sets the method used to compute the skeleton. |
|  |<table class="nested-table"><tbody><tr><td>*m*=1:</td><td>Uses elements of the Ma-Sonka thinning algorithm (default). Use this method if you are only interested in obtaining the thinned image.</td></tr><tr><td>*m*=2:</td><td>Same Ma-Sonka algorithm, but also attempts to generate a wave containing segment paths and a wave containing the lengths of each segment. The path wave (named by default M_SkeletonPath) is a triplet wave where each segment is deliniated by NaN entries. The length of each segment assumes isotropic voxels of 1^3 dimensionless units. The lengths are sequentially stored in the wave W_segmentLength.</td></tr><tr><td>m=3:</td><td>Uses an algorithm by Kalman Palagyi.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z</span> | Do not report any errors. The operation creates the variable V_Flag which is set to zero if the operation succeeds or to an error code otherwise. |

### *Details* {#details}
The processed image is stored in the wave M_Skeleton in the current data folder or in the wave specified by /DEST. Skeleton voxels are set to the value 1 and background voxels are set to 0.

The optional output waves are stored in M_SkeletonPath (/DSTP) and W_SegmentLength (/DSTL). You can display the wave M_SkeletonPath using a Path object in Gizmo.

### *Example* {#example}

```igor
// Create a cube with orthogonal square holes:
Make/O/B/U/N=(30,30,30) ddd=0
ddd[2,27][2,27][2,27]=1
ddd[2,27][10,20][10,20]=0
ddd[10,20][2,27][10,20]=0
ddd[10,20][10,20][2,27]=0
// Execute the operation:
ImageSkeleton3D/METH=1 ddd
```


|  |
| --- |
| You can display the output wave using the following Gizmo recreation macro: |


```igor
Window gizmo0() : GizmoPlot
	PauseUpdate; Silent 1		// building window...
	// Building Gizmo 9 window...
	NewGizmo/W=(110.25,41.75,624.75,501.5)
	ModifyGizmo startRecMacro=901
	ModifyGizmo scalingOption=63
	AppendToGizmo voxelgram=root:ddd,name=voxelgram0
	ModifyGizmo ModifyObject=voxelgram0,objectType=voxelgram,property={valueRGBA,0,1,1,0,0,0.2}
	ModifyGizmo ModifyObject=voxelgram0,objectType=voxelgram,property={valueUsed,0,1}
	ModifyGizmo ModifyObject=voxelgram0,objectType=voxelgram,property={mode,1}
	ModifyGizmo modifyObject=voxelgram0,objectType=Surface,property={calcNormals,1}
	AppendToGizmo light=Directional,name=light0
	ModifyGizmo modifyObject=light0,objectType=light,property={position,-0.53,0.7697,0.342,0.0}
	ModifyGizmo modifyObject=light0,objectType=light,property={direction,-0.53,0.7697,0.342}
	ModifyGizmo modifyObject=light0,objectType=light,property={specular,1.0,1.0,1.0,1.0}
	AppendToGizmo voxelgram=root:M_Skeleton,name=skeleton
	ModifyGizmo ModifyObject=skeleton,objectType=voxelgram,property={valueRGBA,0,1,0.000015,0.244,1.0,1.0}
	ModifyGizmo ModifyObject=skeleton,objectType=voxelgram,property={valueUsed,0,1}
	ModifyGizmo ModifyObject=skeleton,objectType=voxelgram,property={mode,1}
	ModifyGizmo ModifyObject=skeleton,objectType=voxelgram,property={method,0}
	ModifyGizmo modifyObject=skeleton,objectType=Surface,property={calcNormals,1}
	AppendToGizmo attribute blendFunc={770,771},name=blendFunc0
	ModifyGizmo setDisplayList=0, attribute=blendFunc0
	ModifyGizmo setDisplayList=1, opName=enableBlend, operation=enable, data=3042
	ModifyGizmo setDisplayList=2, object=light0
	ModifyGizmo setDisplayList=3, object=skeleton
	ModifyGizmo setDisplayList=4, object=voxelgram0
	ModifyGizmo autoscaling=1
	ModifyGizmo currentGroupObject=""
	ModifyGizmo zoomFactor=0.730000
	ModifyGizmo SETQUATERNION={0.028707,0.961745,0.101554,-0.252802}
	ModifyGizmo endRecMacro
EndMacro
```

### *See Also* {#see-also}
[Image Processing](/igorpro/analysis/image-processing.md), [ImageMorphology](/igorpro/commands/imagemorphology.md), [ImageSeedFill](/igorpro/commands/imageseedfill.md)

### *Reference* {#reference}
K. Palagyi, "A 3D fully parallel surface-thinning algorithm", *Theoretical Computer Science* **406** (2008) 119-135.

C. M. Ma, M. Sonka, A fully parallel 3D thinning algorithm and its applications , Computer Vision and Image Understanding, 64 (3), November 1996, pp. 420-433.