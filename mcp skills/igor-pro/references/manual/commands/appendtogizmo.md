---
description: "The AppendToGizmo operation appends a Gizmo object or attribute operation to the top Gizmo window or to the Gizmo window specified by the /N flag."
slug: /commands/appendtogizmo
---

<div className="command-signature">

## <strong>AppendToGizmo</strong>  [<em>flags</em>] <em>keyword</em> [=<em>value</em> ] {#appendtogizmo}

</div>

The AppendToGizmo operation appends a Gizmo object or attribute operation to the top Gizmo window or to the Gizmo window specified by the /N flag.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Appends the item to the bottom of the display list. |
| <span class="table-cell-nowrap">/N = *gizmoName*</span> | Specifies the name of the targeted Gizmo window. If you omit /N then AppendToGizmo operates on the top Gizmo window. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| attribute | Tells Gizmo that the remainder of the command refers to an attribute. For example: |
|  | <code class="igor">AppendToGizmo attribute pointSize=1.0, name=ps0</code> |
| <span class="table-cell-nowrap">alphaTestFunc = {*alphaTFuncSpec*, *reference*}</span> |  |
|  | Discards pixels for which the alpha value fails the selected test relative to the constant reference value. |
|  | *alphaTFuncSpec* is one of the following values: |
|  |<table class="nested-table"><tbody><tr><td>0x0200:</td><td>GL_NEVER</td></tr><tr><td>0x0202:</td><td>GL_EQUAL</td></tr><tr><td>0x0203:</td><td>GL_LEQUAL</td></tr><tr><td>0x0204:</td><td>GL_GREATER</td></tr><tr><td>0x0205:</td><td>GL_NOTEQUAL</td></tr><tr><td>0x0206:</td><td>GL_GEQUAL</td></tr><tr><td>0x0207:</td><td>GL_ALWAYS</td></tr></tbody></table>
|  | *reference* is a value in the range [0,1]. |
| <span class="table-cell-nowrap">ambient = {*R* , *G* , *B* , *A* , *face* }</span> |  |
|  | Sets material properties. |
|  | *R* , *G* , *B* , and *A* are values are in the range [0,1]. |
|  | The *face* is one of: |
|  |<table class="nested-table"><tbody><tr><td>0x0404:</td><td>GL_FRONT</td></tr><tr><td>0x0405:</td><td>GL_BACK</td></tr><tr><td>0x0408:</td><td>GL_FRONT_AND_BACK</td></tr></tbody></table>
| <span class="table-cell-nowrap">axes = *type*</span> | Appends a default axis object. |
|  | *type* is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>boxAxes</td><td>12 axes, one on each side of the display volume</td></tr><tr><td>tripletAxes</td><td>XYZ triplet drawn at the origin</td></tr><tr><td>customAxis</td><td>A single user-specified linear axis</td></tr><tr><td>defaultAxes</td><td>A boxAxes object is added only if there is no axis object of any type in the display list. The object is first added to the object list and then added to the display list.</td></tr></tbody></table>
| <span class="table-cell-nowrap">bar3d = *bar3dWave*</span> | Specifies the data wave for a 3D Bar plot. |
|  | For more information see [3D Bar Plots](/igorpro/graphing/3d-graphics.md#3d-bar-plots). |
| <span class="table-cell-nowrap">blendFunction = {*source*, *dest* }</span> |  |
|  | Appends an attribute which specifies the blending operation when blending is enabled. |
|  | *source* is one of the following values: |
|  |<table class="nested-table"><tbody><tr><td>0x0000:</td><td>GL_ZERO</td></tr><tr><td>0x0001:</td><td>GL_ONE</td></tr><tr><td>0x0300:</td><td>GL_SRC_COLOR</td></tr><tr><td>0x0301:</td><td>GL_ONE_MINUS_SRC_COLOR</td></tr><tr><td>0x0306:</td><td>GL_DST_COLOR</td></tr><tr><td>0x0307:</td><td>GL_ONE_MINUS_DST_COLOR</td></tr><tr><td>0x0302:</td><td>GL_SRC_ALPHA</td></tr><tr><td>0x0303:</td><td>GL_ONE_MINUS_SRC_ALPHA</td></tr><tr><td>0x0304:</td><td>GL_DST_ALPHA</td></tr><tr><td>0x0305:</td><td>GL_ONE_MINUS_DST_ALPHA</td></tr><tr><td>0x8001:</td><td>GL_CONSTANT_COLOR</td></tr><tr><td>0x8002:</td><td>GL_ONE_MINUS_CONSTANT_COLOR</td></tr><tr><td>0x8003:</td><td>GL_CONSTANT_ALPHA</td></tr><tr><td>0x8004:</td><td>GL_ONE_MINUS_CONSTANT_ALPHA</td></tr><tr><td>0x0308:</td><td>GL_SRC_ALPHA_SATURATE</td></tr></tbody></table>
|  | *dest* is one of the following values: |
|  |<table class="nested-table"><tbody><tr><td>0x0000:</td><td>GL_ZERO</td></tr><tr><td>0x0001:</td><td>GL_ONE</td></tr><tr><td>0x0300:</td><td>GL_SRC_COLOR,</td></tr><tr><td>0x0301:</td><td>GL_ONE_MINUS_SRC_COLOR</td></tr><tr><td>0x0306:</td><td>GL_DST_COLOR</td></tr><tr><td>0x0307:</td><td>GL_ONE_MINUS_DST_COLOR</td></tr><tr><td>0x0302:</td><td>GL_SRC_ALPHA</td></tr><tr><td>0x0303:</td><td>GL_ONE_MINUS_SRC_ALPHA</td></tr><tr><td>0x0304:</td><td>GL_DST_ALPHA</td></tr><tr><td>0x0305:</td><td>GL_ONE_MINUS_DST_ALPHA</td></tr><tr><td>0x8001:</td><td>GL_CONSTANT_COLOR</td></tr><tr><td>0x8002:</td><td>GL_ONE_MINUS_CONSTANT_COLOR</td></tr><tr><td>0x8003:</td><td>GL_CONSTANT_ALPHA</td></tr><tr><td>0x8004:</td><td>GL_ONE_MINUS_CONSTANT_ALPHA</td></tr></tbody></table>
|  | For example: |
|  | <code class="igor">AppendToGizmo attribute blendFunction={0x302,0x303}, name=blendFunc0</code> |
| <span class="table-cell-nowrap">box = {*length*, *width*, *height* }</span> |  |
|  | Append a default box object of dimensions *length*, *width* and *height* specified in +/-1 display volume coordinates. Use the name keyword to assign the new object a name. For example: |
|  | <code class="igor">AppendToGizmo box={1,1,1}, name=box0</code> |
|  | For more information see [Box Objects](/igorpro/graphing/3d-graphics.md#box-objects). |
| <span class="table-cell-nowrap">color = {*R*, *G*, *B*, *A*}</span> | Appends a color attribute with RGBA components in the range [0,1]. For example: |
|  | <code class="igor">AppendToGizmo attribute color={1.0,0.0,0.0,1.0}, name=color0</code> |
| <span class="table-cell-nowrap">colorScale = *name* (deprecated)</span> |  |
|  | Appends a default colorscale object named *name*. |
|  | Gizmo colorscales are deprecated; use standard annotation instead. See [Changes to Gizmo Text](/igorpro/graphing/3d-graphics.md#changes-to-gizmo-text) for details. |
| <span class="table-cell-nowrap">cylinder = {*baseRadius*, *topRadius*, *height*, *slices*, *rings*}</span> |  |
|  | Appends a cylinder object. For example: |
|  | <code class="igor">AppendToGizmo cylinder={1,1,1,25,5}, name=cylinder0</code> |
|  | For more information see [Cylinder Objects](/igorpro/graphing/3d-graphics.md#cylinder-objects). |
| <span class="table-cell-nowrap">disk = {*innerRadius*, *outerRadius*, *slices*, *rings*, *startAngle*, *sweepAngle*}</span> |  |
|  | Appends a disk object. For example: |
|  | <code class="igor">AppendToGizmo disk={0,1,20,20,0,360}, name=disk0</code> |
|  | For more information see [Disk Objects](/igorpro/graphing/3d-graphics.md#disk-objects). |
| <span class="table-cell-nowrap">default3DBarChart = *srcWave*</span> |  |
|  | Appends and displays a default 3D Bar plot for a 2D wave *srcWave.* For example: |
|  | <code class="igor">AppendToGizmo default3DBarChart=my2DWave</code> |
| <span class="table-cell-nowrap">defaultIsoSurface = *src3DWave*</span> |  |
|  | Appends and displays a default iso-surface. For example: |
|  | <code class="igor">AppendToGizmo defaultIsoSurface=src3DWave</code> |
|  | Gizmo sets the isosurface value as the mean value of *src3DWave*. The isosurface uses red color for front surfaces and blue for back surfaces. |
|  | The defaultIsoSurface keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">defaultPath = *srcTripletWave*</span> |  |
|  | Appends and displays a default path plot for a 3-column 2D wave *srcTripletWave.* For example, this draws a path object using a black 1-unit wide line and default axes: |
|  | <code class="igor">AppendToGizmo defaultPath=srcTripletWave</code> |
|  | The defaultPath keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">defaultScatter = *srcWave*</span> |  |
|  | Appends and displays a default scatter plot for the triplet wave *srcWave.* For example: |
|  | <code class="igor">AppendToGizmo defaultScatter=myTripletWave</code> |
| <span class="table-cell-nowrap">defaultSurface = *srcWave*</span> |  |
|  | Appends and displays a default surface plot for the 2D wave *srcWave.* For example: |
|  | <code class="igor">AppendToGizmo defaultSurface=my2DWave</code> |
|  | The defaultPath keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">defaultVolumeSlices = *src3DWave*</span> |  |
|  | Appends and displays three surface objects representing X, Y and Z slices through the center of the volume data together with default axes. For example: |
|  | <code class="igor">AppendToGizmo defaultVolumeSlices=src3DWave</code> |
|  | The three orthogonal slices are drawn using the rainbow color table. |
|  | The defaultVolumeSlices keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">defaultVoxelgram = *src3DWave*</span> |  |
|  | Appends and displays a default voxelgram. For example: |
|  | <code class="igor">AppendToGizmo defaultVoxelgram=src3DWave</code> |
|  | Gizmo sets the voxelgram value as the mean value of *src3DWave*. It also sets the voxelgram's tolerance to 5% of the variance of *src3DWave*. If the number of points in *src3DWave* is greater than 50,000 then the voxelgram uses point markers; otherwise it uses cube markers. |
|  | The defaultVoxelgram keyword was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">diffuse = {*R*, *G*, *B*, *A*, *face* }</span> |  |
|  | Sets material properties. |
|  | RGBA values are in the range [0,1]. |
|  | *face* is one of: |
|  |<table class="nested-table"><tbody><tr><td>0x0404:</td><td>GL_FRONT</td></tr><tr><td>0x0405:</td><td>GL_BACK</td></tr><tr><td>0x0408:</td><td>GL_FRONT_AND_BACK</td></tr></tbody></table>
| <span class="table-cell-nowrap">emission = {*R*, *G*, *B*, *A*, *face* }</span> |  |
|  | Set material properties. |
|  | RGBA values are in the range [0,1]. |
|  | *face* is one of: |
|  |<table class="nested-table"><tbody><tr><td>0x0404:</td><td>GL_FRONT</td></tr><tr><td>0x0405:</td><td>GL_BACK</td></tr><tr><td>0x0408:</td><td>GL_FRONT_AND_BACK</td></tr></tbody></table>
| <span class="table-cell-nowrap">freeAxesCue = {*xOff*, *yOff*, *zOff*, *scale*}</span> |  |
|  | Appends an axis cue object at offset *xOff, yOff, zOff* expressed in +/-1 display volume coordinates and using an isotropic *scale* factor. For example: |
|  | <code class="igor">AppendToGizmo freeAxesCue={0.5,0,0,1},name=fAxes0</code> |
| group | Appends a default empty group object. For example: |
|  | <code class="igor">AppendToGizmo group, name=group0</code> |
|  | For more information see [Group Objects](/igorpro/graphing/3d-graphics.md#group-objects). |
| <span class="table-cell-nowrap">image = *imageWave*</span> | Appends a Gizmo image object. |
|  | *imageWave* is a 3D unsigned-byte wave. |
|  | For more information see [Gizmo Image Plots](/igorpro/graphing/3d-graphics.md#gizmo-image-plots). |
| <span class="table-cell-nowrap">isosurface = *srcWave*</span> | Appends an isosurface object using *srcWave* as the data wave. For example: |
|  | <code class="igor">Make/O/N=(10,20,30) data=enoise(10)&#10;AppendToGizmo isosurface=data,name=iso0</code> |
|  | For more information see [Isosurface Plots](/igorpro/graphing/3d-graphics.md#isosurface-plots). |
| <span class="table-cell-nowrap">matrix4x4 = *matWave*</span> | Appends a matrix4x4 object based on the 2D (4x4) real data wave *matWave.* |
| <span class="table-cell-nowrap">light = *lightType*</span> | Appends a default light. |
|  | *lightType* is a keyword, either directional or positional. |
|  | For more information see [Gizmo Lights](/igorpro/graphing/3d-graphics.md#gizmo-lights). |
| <span class="table-cell-nowrap">line = {*x1*, *y1*, *z1*, *x2*, *y2*, *z2* }</span> |  |
|  | Appends a line object between the two vertices specified in +/1- display volume coordinates. For example: |
|  | <code class="igor">AppendToGizmo line={-1,-1,-1,1,1,1}, name=line0</code> |
| <span class="table-cell-nowrap">lineWidth = *width* (deprecated)</span> |  |
|  | Appends a line width attribute that sets the width of a line in pixels. |
| <span class="table-cell-nowrap">name = objName</span> | Provides the name for objects that are created with parameters. For example: |
|  | <code class="igor">AppendToGizmo disk={0,1,20,20,0,360},name=disk0</code> |
| <span class="table-cell-nowrap">path = *srcWave*</span> | Appends a path object for the data in the triplet wave *srcWave*. |
|  | For more information see [Path Plots](/igorpro/graphing/3d-graphics.md#path-plots). |
| <span class="table-cell-nowrap">pieWedge = *name*</span> | Appends a piewedge object with the specified name. For example: |
|  | <code class="igor">AppendToGizmo pieWedge=pieWedge0</code> |
|  | For more information see [Pie Wedge Objects](/igorpro/graphing/3d-graphics.md#pie-wedge-objects). |
| <span class="table-cell-nowrap">pointSize = *size* (deprecated)</span> |  |
|  | Appends an attribute that sets the size of a point in pixels. |
| <span class="table-cell-nowrap">quad = {*x1*, *y1*, *z1*, *x2*, *y2*, *z2*, *x3*, *y3*, *z3*, *x4*, *y4*, *z4* }</span> |  |
|  | Appends a quad object spanning the specified +/-1 display coordinates. For example, to append a quad that fills the bottom z-axis of the cube: |
|  | <code class="igor">AppendToGizmo quad={-1,-1,-1,-1,1,-1,1,1,-1,1,-1,-1}, name=quad0</code> |
|  | For more information see [Quad Objects](/igorpro/graphing/3d-graphics.md#quad-objects). |
| <span class="table-cell-nowrap">quadricDrawStyle = *drawStyle* (deprecated)</span> |  |
|  | Appends an attribute that determines the drawing style of quadric objects (spheres, cylinders and disks). Supported draw styles are: |
|  |<table class="nested-table"><tbody><tr><td>100010:</td><td>Point - surface vertices are marked by points.</td></tr><tr><td>100011:</td><td>Line - surface polygons are drawn as lines.</td></tr><tr><td>100012:</td><td>Fill - surfaces are drawn as filled polygons.</td></tr></tbody></table>
| <span class="table-cell-nowrap">quadricOrientation = *orientation* (deprecated)</span> |  |
|  |<table class="nested-table"><tbody><tr><td>100021:</td><td>Inside - normals are drawn inward.</td></tr><tr><td>100122:</td><td>Outside - normals are drawn outward.</td></tr></tbody></table>
| <span class="table-cell-nowrap">quadricNormals = *normals* (deprecated)</span> |  |
|  |<table class="nested-table"><tbody><tr><td>100002:</td><td>None--normals are not computed.</td></tr><tr><td>100001:</td><td>Flat--one normal is generated per polygon.</td></tr><tr><td>100000:</td><td>Smooth--one normal is generated per vertex.</td></tr></tbody></table>
| <span class="table-cell-nowrap">ribbon = *ribbonWave*</span> | Appends a default ribbon object for the triplet wave *ribbonWave.* |
|  | For more information on ribbon objects see [Ribbon Plots](/igorpro/graphing/3d-graphics.md#ribbon-plots). |
| <span class="table-cell-nowrap">scatter = *srcWave*</span> | Appends a scatter object using the 3 column triplet wave *srcWave* as the data wave. For example: |
|  | <code class="igor">Make/N=(20,3) dataWave=gnoise(10)&#10;AppendToGizmo scatter=dataWave, name=scatter0</code> |
|  | For more information on ribbon objects see [3D Scatter Plots](/igorpro/graphing/3d-graphics.md#3d-scatter-plots). |
| <span class="table-cell-nowrap">surface = *srcWave*</span> | Appends a surface object using a 2D *srcWave*. For example: |
|  | <code class="igor">Make/N=(20,30) my2Dwave=x*y&#10;AppendToGizmo surface=my2Dwave, name=surface0</code> |
|  | For more information on ribbon objects see [Surface Plots](/igorpro/graphing/3d-graphics.md#surface-plots). |
| <span class="table-cell-nowrap">sphere = {*radius*, *slices*, *stacks*}</span> |  |
|  | Appends a sphere object. |
|  | *radius* is expressed in +/-1 display volume coordinates. |
|  | *slices* and *stacks* determine how many facets are used to draw the surface. For example: |
|  | <code class="igor">AppendToGizmo sphere={1,10,15}, name=sphere0</code> |
|  | For more information see [Sphere Objects](/igorpro/graphing/3d-graphics.md#sphere-objects). |
| <span class="table-cell-nowrap">string = *strData* (deprecated)</span> |  |
|  | *strData* is the text to display. |
|  | Gizmo strings are deprecated; use standard annotation instead. See [Changes to Gizmo Text](/igorpro/graphing/3d-graphics.md#changes-to-gizmo-text) for details. |
| <span class="table-cell-nowrap">specular = {*R*,  *G*, *B*, *A*, *face* }</span> |  |
|  | Sets material properties. |
|  | RGBA values are in the range [0,1]. |
|  | *face* is one of: |
|  |<table class="nested-table"><tbody><tr><td>0x0404:</td><td>GL_FRONT</td></tr><tr><td>0x0405:</td><td>GL_BACK</td></tr><tr><td>0x0408:</td><td>GL_FRONT_AND_BACK</td></tr></tbody></table>
| <span class="table-cell-nowrap">strFont = *fontName* (deprecated)</span> |  |
|  | Sets the font used for string objects. |
|  | Use standard annotation instead. See [Changes to Gizmo Text](/igorpro/graphing/3d-graphics.md#changes-to-gizmo-text) for details. |
| <span class="table-cell-nowrap">shininess = {*value*, *face* }</span> |  |
|  | Appends an attribute which characterizes material properties. |
|  | *value* is in the range [0,128]. A higher value makes the reflection more specular (shiny). |
|  | *face* is one of: |
|  |<table class="nested-table"><tbody><tr><td>0x0404:</td><td>GL_FRONT</td></tr><tr><td>0x0405:</td><td>GL_BACK</td></tr><tr><td>0x0408:</td><td>GL_FRONT_AND_BACK</td></tr></tbody></table>
| <span class="table-cell-nowrap">tetrahedron = *name*</span> | Appends a tetrahedron with the specified *name*. |
|  | For more information see [Tetrahedron Objects](/igorpro/graphing/3d-graphics.md#tetrahedron-objects). |
| <span class="table-cell-nowrap">triangle = {*x1*, *y1*, *z1*, *x2*, *y2*, *z2*, *x3*, *y3*, *z3* }</span> |  |
|  | Appends a triangle with the specified vertices expressed in +/-1 display volume coordinates. For example: |
|  | <code class="igor">AppendToGizmo triangle={0,0,0,1,1,1,1,-1,-1}</code> |
|  | For more information see [Triangle Objects](/igorpro/graphing/3d-graphics.md#triangle-objects). |
| <span class="table-cell-nowrap">texture = *name*</span> | Appends a texture object with the specified *name*. |
|  | For more information see [Texture Objects](/igorpro/graphing/3d-graphics.md#texture-objects). |
| <span class="table-cell-nowrap">voxelgram = *srcWave*</span> | Appends a voxelgram object using the 3D real-valued wave *srcWave* as the data wave. |
|  | For more information on voxelgrams see [Voxelgram Plots](/igorpro/graphing/3d-graphics.md#voxelgram-plots). |

### *See Also* {#see-also}
[3D Graphics](/igorpro/graphing/3d-graphics.md)

[ModifyGizmo](/igorpro/commands/modifygizmo.md), [NewGizmo](/igorpro/commands/newgizmo.md), [ExportGizmo](/igorpro/commands/exportgizmo.md), [GetGizmo](/igorpro/commands/getgizmo.md), [GizmoInfo](/igorpro/commands/gizmoinfo.md), [RemoveFromGizmo](/igorpro/commands/removefromgizmo.md)