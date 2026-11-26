---
description: "The ModifyGizmo operation changes Gizmo properties. The syntax for the operation depends on what you want to change."
slug: /commands/modifygizmo
---

<div className="command-signature">

## <strong>ModifyGizmo</strong>  [<em>flags</em>] <em>keyword</em>  [=<em>value</em> ] {#modifygizmo}

</div>

The ModifyGizmo operation changes Gizmo properties. The syntax for the operation depends on what you want to change.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/N = *gizmoName*</span> | Specifies the name of the targeted Gizmo window. If you omit /N then ModifyGizmo operates on the top Gizmo window. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *General Settings* {#general-settings}
To modify general settings that affect the Gizmo as a whole use:


```igor
ModifyGizmo [flags] keyword  [=value ]
```

See [ModifyGizmo General Settings](#modifygizmo-general-settings) for details.

### *Operations* {#operations}
To modify properties of the display list operation use:


```igor
ModifyGizmo opName=operationName, operation=opType, data={data format}
```

See [ModifyGizmo for Operations](#modifygizmo-for-operations) for details.

### *Objects* {#objects}
To modify the properties of an object use:


```igor
ModifyGizmo modifyObject=objName, objectType=type, property={property format}
```

See [ModifyGizmo for Objects](#modifygizmo-for-objects) for general details.  For specific object details see:

[ModifyGizmo for Path Objects](#modifygizmo-for-path-objects)

[ModifyGizmo for Ribbon Objects](#modifygizmo-for-ribbon-objects)

[ModifyGizmo for Surface Objects](#modifygizmo-for-surface-objects)

[ModifyGizmo for Isosurface Objects](#modifygizmo-for-isosurface-objects)

[ModifyGizmo for Voxelgram Objects](#modifygizmo-for-voxelgram-objects)

[ModifyGizmo for Scatter Objects](#modifygizmo-for-scatter-objects)

[ModifyGizmo for 3D Bar Chart Objects](#modifygizmo-for-3d-bar-chart-objects)

[ModifyGizmo for Image Objects](#modifygizmo-for-image-objects)

[ModifyGizmo for Axis Objects](#modifygizmo-for-axis-objects)

[ModifyGizmo for Free Axis Cue Objects](#modifygizmo-for-free-axis-cue-objects)

[ModifyGizmo for Line Objects](#modifygizmo-for-line-objects)

[ModifyGizmo for Triangle Objects](#modifygizmo-for-triangle-objects)

[ModifyGizmo for Quad Objects](#modifygizmo-for-quad-objects)

[ModifyGizmo for Box Objects](#modifygizmo-for-box-objects)

[ModifyGizmo for Sphere Objects](#modifygizmo-for-sphere-objects)

[ModifyGizmo for Cylinder Objects](#modifygizmo-for-cylinder-objects)

[ModifyGizmo for Disk Objects](#modifygizmo-for-disk-objects)

[ModifyGizmo for Tetrahedron Objects](#modifygizmo-for-tetrahedron-objects)

[ModifyGizmo for Pie Wedge Objects](#modifygizmo-for-pie-wedge-objects)

[ModifyGizmo for Light Objects](#modifygizmo-for-light-objects)

[ModifyGizmo for Texture Objects](#modifygizmo-for-texture-objects)

[ModifyGizmo for Matrix4x4 Objects](#modifygizmo-for-matrix4x4-objects)

[ModifyGizmo for String Objects](#modifygizmo-for-string-objects)

[ModifyGizmo for ColorScale Objects](#modifygizmo-for-colorscale-objects)

### *Attributes* {#attributes}
To modify the properties of an attribute use:


```igor
ModifyGizmo attributeType=type, modifyAttribute={attrName,data...}
```

See [ModifyGizmo for Attributes](#modifygizmo-for-attributes) for details.

### *See Also* {#see-also}
[3D Graphics](/igorpro/graphing/3d-graphics.md), [AppendToGizmo](/igorpro/commands/appendtogizmo.md), [NewGizmo](/igorpro/commands/newgizmo.md), [ExportGizmo](/igorpro/commands/exportgizmo.md), [GetGizmo](/igorpro/commands/getgizmo.md), [GizmoInfo](/igorpro/commands/gizmoinfo.md), [RemoveFromGizmo](/igorpro/commands/removefromgizmo.md)


<!-- IndentedSubtopic -->
## ModifyGizmo General Settings {#modifygizmo-general-settings}

The syntax for modifying a general Gizmo setting is:


```igor
ModifyGizmo keyword [=value]
```

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">appendRotation = {*q0*, *q1*, *q2*, *q3*}</span> |  |
|  | Applies a rotation to the current orientation. The rotation is specified by the 4-element quaternion. |
|  | See [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo) for details. |
| <span class="table-cell-nowrap">aspectRatio = *mode*</span> | Specifies the aspect ratio mode for wave-based data objects. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Default. Each dimension is stretched to the full range of the display volume.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>True aspect ratio. The largest data dimension is fills the +/-1 display volume. The other dimensions are scaled to maintain the correct aspect ratio.</td></tr></tbody></table>
| <span class="table-cell-nowrap">attribute = *name*</span> | Identifies a specific attribute by *name*. For example: |
|  | <code class="igor">ModifyGizmo setDisplayList=2, attribute=color0</code> |
| autoScale | Sets scalingOption=63, *autoScaling*=1 and refreshes the display. |
| <span class="table-cell-nowrap">autoScaling = *mode*</span> | Sets the autoscaling mode for wave-based data objects in the Gizmo display. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Turns autoscaling off. Gizmo draws the objects using only the direct transformations that you provide. If an object exceeds the dimensions of the clipping volume it is clipped.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Default. Gizmo finds the minima and maxima of wave-based data objects before drawing and attempts to provide an appropriate axis scaling. Gizmo does not take into account operations such as translation, rotation or scaling. If you use these you must provide your own clipping plane via an operation such as Ortho.</td></tr></tbody></table>
|  | See also keywords: `aspectRatio`, `autoScale`, `scalingOption`, and `setOuterBox`. |
|  | See also [Gizmo Dimensions](/igorpro/graphing/3d-graphics.md#gizmo-dimensions). |
| bringToFront | Brings the Gizmo window to the front. |
|  | You can also use [DoWindow](/igorpro/commands/dowindow.md)/F. |
| clear | Clears both the Gizmo display window and the associated display list in the info window. |
| clearAttributeList | Removes all attributes from the attribute list. Attributes that are associated with other objects or attributes in the display list or object list are also removed. |
| clearDisplayList | Removes all items from the display list. This clears Gizmo display window. |
| clearObjectList | Removes all objects from the object list. Any objects in the display list are also removed. |
| closeInfo | Closes the Info window. |
| compile | Obsolete. Does nothing. |
| <span class="table-cell-nowrap">crystalFlag = *val*</span> | Turns on or off a crystallographic drawing mode for scatter objects. This is an advanced feature that is explained in detail in the crystalDemo experiment. [Open CrystalDemo experiment](#igor-pxp/Examples/Visualization/Advanced/CrystalDemo.pxp) |
| <span class="table-cell-nowrap">currentGroupObject = *groupSpec*</span> |  |
|  | If you create group objects using advanced settings, you need to use this keyword to direct further commands to a group object. |
|  | *groupSpec* is built from the full or relative path to the object. The full path starts from the name of the Gizmo window itself, e.g., Gizmo0, and contains sequential names of all child groups separated with a semicolon. For example: |
|  | <code class="igor">ModifyGizmo currentGroupObject="Gizmo0:group0:subGroup1:subGroup2"</code> |
|  | A relative path starts from the current group object. For example, if the current group object is group0 (from the previous example) then you use: |
|  | <code class="igor">currentGroupObject=":subGroup1:subGroup2"</code> |
|  | If you want to move up one level to a parent group you would use: |
|  |<table class="nested-table"><tbody><tr><td>&lt;code&nbsp;class=&quot;igor&quot;&gt;ModifyGizmo&nbsp;currentGroupObject=&quot;</td><td>&quot;&lt;/code&gt;</td></tr></tbody></table>
| <span class="table-cell-nowrap">defaultLight = *mode*</span> | Turns the default light on or off. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Default light off</td></tr><tr><td>1:</td><td>Default light on</td></tr></tbody></table>
|  | The default light, which is a color-neutral ambient light source, is used if you do not append any light object to the display list. |
|  | The number of light objects is limited by the OpenGL implementation or by hardware. Typically this number is 8 or larger. If you create 8 light objects and none are appended to the display list, Gizmo may be unable to add the automatic default light. |
| displayLastObject | Appends the last object in the object list to the end of the display list. |
| <span class="table-cell-nowrap">edit = {*objType*, *objName*}</span> |  |
|  | Opens Gizmo's standard dialog for editing the properties of the object as if you double-clicked the object's icon in the info window. |
|  | *objType* is one of: `Attribute`, `Object`, `DisplayItem`. |
|  | *objName* is the name of an existing object. |
| endRecMacro | Ends a recreation macro. This affects the timing of updates and redrawing of parsed objects. See `startRecMacro` parameter. |
| <span class="table-cell-nowrap">euler = {*a*, *b*, *c*}</span> | Rotates the display about the specified Euler angles. The angles are in degrees about the X-axis (*a*), the Y-axis (*b*) and the Z-axis (*c*) respectively. The rotation for a positive angle is counterclockwise when looking from the positive side of the axis towards the origin. |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">frameInset = *i*</span> | Specifies the number of pixels by which to inset the frame of the Gizmo subwindow. This is mostly useful for overlaying panels in graphs to give a fake 3D frame a better appearance. |
| <span class="table-cell-nowrap">frameStyle = *f*</span> | Specifies the frame style for a Gizmo subwindow. Values for frameStyle are: |
|  |<table class="nested-table"><tbody><tr><td>*f*&nbsp;=0:</td><td>None</td></tr><tr><td>*f*&nbsp;=1:</td><td>Single</td></tr><tr><td>*f*&nbsp;=2:</td><td>Indented</td></tr><tr><td>*f*&nbsp;=3:</td><td>Raised</td></tr><tr><td>*f*&nbsp;=4:</td><td>Text well</td></tr></tbody></table>
|  | The last three styles are fake 3D and will look good only if the background color of the enclosing space and the panel itself is a light shade of gray. |
| goHome | Rotates the Gizmo display to the home orientation. |
|  | See [Gizmo Object Rotation](/igorpro/graphing/3d-graphics.md#gizmo-object-rotation) for a discussion of the home orientation. |
| <span class="table-cell-nowrap">home = {*a,b,c*}</span> | Defines the home orientation using the Euler angles *a*, *b*, *c* in degrees. You can execute: |
|  | ModifyGizmo home={0,0,0} |
|  | to reset to the default home orientation. |
|  | The initial state of this setting for a given Gizmo window comes from Gizmo miscellanous settings as set via Misc->Miscellaneous Settings. |
|  | See [Gizmo Object Rotation](/igorpro/graphing/3d-graphics.md#gizmo-object-rotation) for a discussion of the home orientation. |
| <span class="table-cell-nowrap">hookEvents = *value*</span> | *value* is a bitwise setting that determine which events activate the hookFunction. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Mouse down</td></tr><tr><td>Bit&nbsp;1:</td><td>Mouse moved</td></tr><tr><td>Bit&nbsp;2:</td><td>Display rotated</td></tr><tr><td>Bit&nbsp;3:</td><td>Window killed</td></tr><tr><td>Bit&nbsp;4:</td><td>Data range changed</td></tr><tr><td>Bit&nbsp;5:</td><td>Mouse wheel moved</td></tr><tr><td>Bit&nbsp;6:</td><td>Projection transformation changed</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | This setting does not affect standard window hooks as described under  [Window Hook Functions](/igorpro/advanced-topics.md#window-hook-functions). It affects only the Gizmo-specific hook function set by the hookFunction keyword. |
| <span class="table-cell-nowrap">hookFunction = *functionName* (obsolete)</span> |  |
|  | Specifies the function to be called when certain events happen. Use hookFunction=$"" to specify no hook function. This sets the unnamed hook function and is analogous to [SetWindow](/igorpro/commands/setwindow.md) hook=procName. |
|  | Unnamed hook functions are obsolete. See [Gizmo Hook Functions](/igorpro/graphing/3d-graphics.md#gizmo-hook-functions) for details. |
| <span class="table-cell-nowrap">idleEventQuaternion = {*q0*, *q1*, *q2*, *q3*}</span> |  |
|  | Starts idle-event rotation. In each idle event Gizmo rotates the display by the specified quaternion. |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">idleEventRotation = {*dx*, *dy*}</span> |  |
|  | Starts idle-event rotation using the equivalent mouse translation increments given by *dx* and *dy* in pixels. |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">idleEventRotation = {*angle*, *axis1*, *axis2*, *axis3*}</span> |  |
|  | Starts and idle-event rotation about an axis specified by three components. The angle, expressed in degrees, determines the amount of rotation between consecutive idle events. For example, to start a clockwise idle-event rotation about the z-axis use: |
|  | <code class="igor">ModifyGizmo idleEventRotation={5,0,0,1}</code> |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">infoWindow [ = {*left*, *top*, *right*, *bottom*}]</span> |  |
|  | Specifies the size and position of the info window. If used without arguments it opens the info window at the top-left corner of the active screen. |
| <span class="table-cell-nowrap">insertDisplayList = *n*</span> | Inserts an item in the display list at zero-based location *n*. For example, this inserts a translation operation at location 2: |
|  | <code class="igor">ModifyGizmo insertDisplayList=2,opName=t0,operation=translate,data={1,1,1}</code> |
| keepPlotSquare=*val* |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>The viewport fills the Gizmo window.</td></tr><tr><td>*val*&nbsp;=1:</td><td>The viewport is the largest square that fits centered in the Gizmo window.</td></tr></tbody></table>
|  | All other values are reserved for future use. |
| <span class="table-cell-nowrap">lockMouseRotation = *val*</span> |  |
|  | Enables or disables rotation using the mouse. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>Enables rotation with the cursor.</td></tr><tr><td>*val*&nbsp;=1:</td><td>Disables rotation using the cursor.</td></tr></tbody></table>
| <span class="table-cell-nowrap">makeSurfaceColorWave = {*srcWave*, *cTabName*, *isInverse*}</span> |  |
| <span class="table-cell-nowrap">makeColorWave = {*srcWave*, *cTabName*, *isInverse*}</span> |  |
|  | *makeColorWave* is a synonym for the preferred *makeSurfaceColorWave* keyword. |
|  | This keyword does not actually modify the display in Gizmo. It is a convenience function that creates a color wave suitable for Gizmo. |
|  | When *srcWave* is a 2D wave, *makeSurfaceColorWave* creates a 3D, 4-layer RGBA color wave specifying the color for each Z value in *srcWave*. If *srcWave* contains NaNs, they are mapped into RGBA with an alpha value of zero. |
|  | When *srcWave* is a 1D wave with n rows, the operation creates an (nx4) RGBA wave using the specified color table. |
|  | The output wave is created in the current data folder and has the same name as *srcWave* with an "_C" suffix. If a wave of that name exists, it is overwritten. |
|  | *cTabName* is the name of one of the built-in color tables, e.g., Grays, Rainbow, etc. |
|  | If *isInverse* is 0, the minimum Z data value in *srcWave* is mapped to the first color in the color table and the maximum Z data value in *srcWave* is mapped to the last color in the color table. If *isInverse* is 1 the mapping is reversed. |
|  | See [Gizmo Colors, Material and Lights[Color Waves]](/igorpro/graphing/3d-graphics.md#color-waves) for further details and for discussion of a situation where this feature is useful. |
| <span class="table-cell-nowrap">makeTripletColorWave = {*srcWave*, *cTabName*, *isInverse*}</span> |  |
|  | This keyword does not actually modify the display in Gizmo. It is a convenience function that creates a color wave suitable for Gizmo. |
|  | If *srcWave* is a triplet wave, the operation uses the data in the Z column of *srcWave.* |
|  | If *srcWave* is not a triplet wave the operation uses the data in the first column of *srcWave.* |
|  | *cTabName* is the name of one of the built-in color tables, e.g., Grays, Rainbow, etc. |
|  | If *isInverse* is 0, the minimum Z data value in *srcWave* is mapped to the first color in the color table and the maximum Z data value in *srcWave* is mapped to the last color in the color table. If *isInverse* is 1 the mapping is reversed. |
|  | The output wave is created in the current data folder and has the same name as *srcWave* with an "_C" suffix. If a wave of that name exists, it is overwritten. |
|  | Despite the name "makeTripletWave", the output wave is a 2D wave with 4 columns having the same number of rows as *srcWave*. Each row contains an RGBA color taken from a built-in color table specified by *cTabName*. Alpha values are set to 1 except when the Z value is NaN, in which case alpha is set to zero. |
| <span class="table-cell-nowrap">mass = *value*</span> | *value* affects the manual rotation of objects by giving the displayed objects "inertia". By default, mass=2. A larger value slows rotation and a smaller value speeds rotation. |
| <span class="table-cell-nowrap">matchRotation = *gizmoName*</span> |  |
|  | Sets the orientation of the target Gizmo window to that of the Gizmo window specified by *gizmoName*. |
| <span class="table-cell-nowrap">namedHook = {*hookName*, *procName*}</span> |  |
|  | *hookName* is the name of the Gizmo window hook you are installing. *procName* is the name of the Igor procedure to which hooks will be sent. |
|  | See [Gizmo Named Hook Functions](/igorpro/graphing/3d-graphics.md#gizmo-named-hook-functions) for details. |
| <span class="table-cell-nowrap">namedHookStr = {*hookName*, *procNameStr*}</span> |  |
|  | Use this version to install a named hook function when your function is part of an independent module and needs to be called using a compound name as in *IM#funcName*. In this case you pass the procedure name as a string. |
| <span class="table-cell-nowrap">object = *name*</span> | Identifies a specific object by name. For example: |
|  | <code class="igor">ModifyGizmo setDisplayList=2, object=surface0</code> |
| <span class="table-cell-nowrap">offsetQuat = {*q0*, *q1*, *q2*, *q3*}</span> |  |
|  | Specifies an offset quaternion for synchronized rotation. When you set Gizmo0 to be synchronized with Gizmo1, using syncRotation, you can add the offset quaternion to Gizmo0 so that whenever Gizmo1 is rotated, Gizmo0 is rotated to the orientation of Gizmo1 and then rotated further by the offset quaternion. You can enable/disable the use of the offset quaternion with the keyword useOffsetQuat. |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">outputResFactor = *f*</span> | Specifies the factor by which the output resolution is greater than screen resolution. The factor affects output copied to the clipboard, printed or exported as an image. By default outputResFactor=2. |
|  | See also [Exporting Gizmo Windows](/igorpro/graphing/3d-graphics.md#exporting-gizmo-windows). |
| <span class="table-cell-nowrap">pan = {*x*, *y*}</span> | Pans the Gizmo display by *x* in the x-direction and *y* in the y-direction. Both *x* and *y* are in +/-1 display volume units. |
| <span class="table-cell-nowrap">pathToRibbon = {*srcTriplet*, *columnNum*, *setValue*}</span> |  |
|  | Creates a triplet wave representing a ribbon from *srcTriplet*, which must be single- or double-precision floating point, by setting alternating values of the specified *columnNum* to the *setValue.* |
| printDrawingTime | Prints a message in the history showing the time that it took to draw the last Gizmo image. |
|  | The last drawing time may be significantly shorter than the initial drawing time because Gizmo attempts to preserve vertex buffer objects when the underlying data waves have not changed. For example, the time it takes to draw a surface on rotation is shorter than the time to draw a surface when the surface data changed. |
| <span class="table-cell-nowrap">removeObjectAttribute = {*objectName*, *attributeName*}</span> |  |
|  | Removes the specified embedded attribute from the named object. |
| resumeUpdates | Use *resumeUpdates* at the end of a sequence of commands to allow the resumption of normal updates. See also stopUpdates below. |
| <span class="table-cell-nowrap">saveGroupRecreation = *macroName*</span> |  |
|  | Saves a recreation macro for the current group object, as set by the *currentGroupObject* keyword. The recreation macro is saved using the specified macro name to the built-in procedure window. |
| <span class="table-cell-nowrap">scalingMode = *m*</span> | Normally you will not need to use this keyword. When you use the *setOuterBox* keyword, Gizmo internally executes scalingMode=8. When you apply autoscaling Gizmo sets scalingMode=2. Other scaling modes are reserved. |
|  | See also [Gizmo Dimensions](/igorpro/graphing/3d-graphics.md#gizmo-dimensions). |
| <span class="table-cell-nowrap">scalingOption = *flag*</span> | *flags* is a bitwise setting that determines whether autoscaling is turned on for each axis end. If a given bit is set, the cooresponding axis end is autoscaled. Otherwise that axis end is controlled by the manual axis range as set by the setOuterBox keyword. |
|  | *flags* is defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>X axis minimum</td></tr><tr><td>Bit&nbsp;1:</td><td>X axis maximum</td></tr><tr><td>Bit&nbsp;2:</td><td>Y axis minimum</td></tr><tr><td>Bit&nbsp;3:</td><td>Y axis maximum</td></tr><tr><td>Bit&nbsp;4:</td><td>Z axis minimum</td></tr><tr><td>Bit&nbsp;5:</td><td>Z axis maximum</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | Using these binary fields a complete auto-scale (for all axes) corresponds to scalingOption=63 and when the range of all axes are specified by the user correspond to scalingOption=0. See also setOuterBox. |
|  | *flags* =63 turns autoscaling on for all axis ends. *flags* =0 turns autoscaling off for all axis ends. |
|  | See also [Gizmo Dimensions](/igorpro/graphing/3d-graphics.md#gizmo-dimensions). |
| <span class="table-cell-nowrap">setAttributeName = {*oldName*, *newName*}</span> |  |
|  | Renames an attribute. *oldName* must be the name of an existing object. *newName* must be valid and unique. |
| <span class="table-cell-nowrap">setDisplayList = *index*</span> | Set operations, objects or attributes in the display list. *index* is a zero-based list index. For example: |
|  | <code class="igor">ModifyGizmo setDisplayList=0, opName=popMatrix0, operation=PopMatrix&#10;ModifyGizmo setDisplayList=1, object=surface0&#10;ModifyGizmo setDisplayList=2, attribute=color0</code> |
|  | If *index* =-1, the specified object is appended to the end of the display list. |
| <span class="table-cell-nowrap">setDisplayListName = {*oldName*, *newName*}</span> |  |
|  | Renames a display list item. *oldName* must be the name of an existing display list item. *newName* must be valid and unique. |
| <span class="table-cell-nowrap">setObjectAttribute = {*objectName*, *attributeName*}</span> |  |
|  | Embeds an attribute, specified by *attributeName*, in the object specified by *objectName*. For example: |
|  | <code class="igor">ModifyGizmo setObjectAttribute={axes0,blueColor}</code> |
| <span class="table-cell-nowrap">setObjectName = {*oldName*, *newName*}</span> |  |
|  | Renames an object list item. *oldName* must be the name of an existing object list item. *newName* must be valid and unique. |
| <span class="table-cell-nowrap">setOuterBox = {*xmin*, *xmax*, *ymin*, *ymax*, *zmin*, *zmax*}</span> |  |
|  | Sets the display range for wave-based data objects to the specified user values. |
|  | This feature is useful if you want to force the limits of the graph in any dimension. To revert to autoscaling, execute: |
|  | <code class="igor">ModifyGizmo scalingMode=2</code> |
|  | You can also use the *scalingOption* keyword to select which of the outer box limits actually affect the display. |
|  | See also [Gizmo Dimensions](/igorpro/graphing/3d-graphics.md#gizmo-dimensions). |
| <span class="table-cell-nowrap">setQuaternion = {*q0*, *q1*, *q2*, *q3*}</span> |  |
|  | Sets the internal quaternion that governs the orientation of the Gizmo display. |
|  | See [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo) for details. |
|  | You may find it easier to use the euler keyword. |
| <span class="table-cell-nowrap">setRotationMatrix = *mWave*</span> |  |
|  | Sets the 16 elements of the rotation matrix to the 2D (4x4) wave *mWave*. The rotation matrix represents the current transformation. |
|  | This is equivalent to setQuaternion above. Gizmo uses quaternions internally. The specified rotation matrix is converted to a quaternion on input. |
|  | If you intend to perform repeated rotation operations you should consider using quaternions instead. |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">setRotationMatrix = {*v0*,... *v15*}</span> |  |
|  | Sets the rotation matrix to the 16 elements specified as {00,01,02,03,10,11,12,13,...} where the first digit specifies the matrix-element's row and the second its column. This is an alternative to setting the rotation matrix using a 4x4 wave. |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">showAxisCue = *val*</span> | Shows or hides the built-in axis cue that indicates the orientation of the X, Y and Z axes. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>Hides the axis cue.</td></tr><tr><td>*val*&nbsp;=1:</td><td>Shows the axis cue.</td></tr></tbody></table>
|  | See also the freeAxesCue keyword in the [AppendToGizmo](/igorpro/commands/appendtogizmo.md) operation. |
| showInfo | Opens the Gizmo info window assocated with the targeted Gizmo display window. If the info window is already open, it just brings it to the front. |
| <span class="table-cell-nowrap">showTime = *mode*</span> | Turns on or off printing into the history area the time it took to complete drawing the Gizmo plot. This is a debugging aid which you will generally not need to use. |
| <span class="table-cell-nowrap">startRecMacro = *version*</span> | Starts a recreation macro for a Gizmo plot. Commands that appear between startRecMacro and endRecMacro are executed without immediate update. |
|  | *version* was added in Igor Pro 7.00. See [Gizmo Recreation Macro Changes](/igorpro/graphing/3d-graphics.md#gizmo-recreation-macro-changes) for details. |
|  | This keyword is automatically generated by Igor when it creates a recreation macro. You should not need to use it. |
| stopRotation | Stops idle-event rotation of the display. |
| stopUpdates | Suspends updating the Gizmo display for subsequent ModifyGizmo commands until resumeUpdates is called. Use this to allow quick execution of multiple ModifyGizmo commands followed by a single update at the end of the process. |
| <span class="table-cell-nowrap">syncRotation = *gizmoName*</span> |  |
|  | Synchronizes the rotation of the targeted Gizmo to that of *gizmoName*. After you execute this command, the targeted Gizmo will rotate in sync with *gizmoName*. To clear this setting use syncRotation=$"". |
|  | It is possibly to cross-synchronize Gizmos as in: |
|  | <code class="igor">ModifyGizmo/N=Gizmo0 syncRotation=gizmo1&#10;ModifyGizmo/N=Gizmo1 syncRotation=gizmo0</code> |
|  | See also the offsetQuat keyword. |
|  | See also [Programming Rotations in Gizmo](/igorpro/graphing/3d-graphics.md#programming-rotations-in-gizmo). |
| <span class="table-cell-nowrap">update = *mode*</span> | Forces an update of the Gizmo Display window. *mode* is: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Performs a silent update mostly during idle events.</td></tr><tr><td>1:</td><td>Checks if any object needs updating or if the rotation changed and updates only if necessary.</td></tr><tr><td>2:</td><td>Forces an immediate update that includes reloading all the waves, finding the minima and maxima, computing their scale factors and redrawing the associated objects.</td></tr></tbody></table>
| <span class="table-cell-nowrap">useOffsetQuat = *mode*</span> | Controls whether the offset quaternion is used during synchronized rotation. *mode* is: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Disable using an offset quaternion.</td></tr><tr><td>1:</td><td>Enable using an offset quaternion when in syncRotation.</td></tr></tbody></table>
|  | See offsetQuat above for details. |
| <span class="table-cell-nowrap">userString = {*name*, *str*}</span> | This keyword is for backward compatibility only. New code should use the more flexible [SetWindow](/igorpro/commands/setwindow.md) with the userData keyword. |
|  | Stores arbitrary user-specified data which can later be retrieved using *name*. This is used by advanced programmers to associate procedure settings with a given Gizmo window. |
|  | *name* is a standard IGOR name. |
|  | *str* is limited to 255 bytes. |
|  | If you issue this command for an existing name, it overwrites the previous value with the new *str*. |
|  | See also [GetGizmo](/igorpro/commands/getgizmo.md) userString. |
| <span class="table-cell-nowrap">zoomMode = *mode*</span> | Determines if the mouse scroll wheel rotates or zooms the Gizmo display: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Mouse wheel rotates.</td></tr><tr><td>1:</td><td>Mouse wheel zooms.</td></tr></tbody></table>
| <span class="table-cell-nowrap">zoomFactor = *f*</span> | Specifies the level of zoom. |
|  | *f* is a positive number with *f*=1.0 giving default zoom. |
|  | *f* > 1 zooms out relative to the default. |
|  | *f* < 1 zooms in relative to the default. |




<!-- IndentedSubtopic -->
## ModifyGizmo for Attributes {#modifygizmo-for-attributes}

The syntax for modifying a Gizmo attribute is:


```igor
ModifyGizmo attributeType=type, modifyAttribute={attrName,data...}
```

*type* is one of the built-in attributes types listed below.

*attrName* is the name of the particular attribute that you want to modify.

*data* depends on the requirements of the specific attribute. The table below lists all of the attribute types and their corresponding data requirements.

### *Keywords* {#modifygizmo-for-attributes-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">attributeType = color, modifyAttribute={*attrName* , *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* are values in the range [0,1] specifying the attribute's color. |
| <span class="table-cell-nowrap">attributeType = ambient, modifyAttribute={*attrName* , *R*, *G*, *B*, *A*, *mode* }</span> |  |
|  | *R*, *G*, *B*, and *A* are values in the range [0,1] specifying the attribute's color. |
|  | *mode* is 1028 (GL_FRONT), 1029 (GL_BACK) or 1032 (GL_FRONT_AND_BACK). |
| <span class="table-cell-nowrap">attributeType = diffuse, modifyAttribute={*attrName* , *R*, *G*, *B*, *A*, *mode* }</span> |  |
|  | *R*, *G*, *B*, and *A* are values in the range [0,1] specifying the attribute's color. |
|  | *mode* is 1028 (GL_FRONT), 1029 (GL_BACK) or 1032 (GL_FRONT_AND_BACK). |
| <span class="table-cell-nowrap">attributeType = specular, modifyAttribute={*attrName* , *R*, *G*, *B*, *A*, *mode* }</span> |  |
|  | *R*, *G*, *B*, and *A* are values in the range [0,1] specifying the attribute's color. |
|  | *mode* is 1028 (GL_FRONT), 1029 (GL_BACK) or 1032 (GL_FRONT_AND_BACK). |
| <span class="table-cell-nowrap">attributeType = shininess, modifyAttribute={*attrName* , *vFront* , *vBack* }</span> |  |
|  | *vFront* and *vBack* are the front and back shininess in the range [0,128]. |
| <span class="table-cell-nowrap">attributeType = emission, modifyAttribute={*attrName* , *R*, *G*, *B*, *A*, *mode* }</span> |  |
|  | *R*, *G*, *B*, and *A* are values in the range [0,1] specifying the attribute's color. |
|  | *mode* is 1028 (GL_FRONT), 1029 (GL_BACK) or 1032 (GL_FRONT_AND_BACK). |
| <span class="table-cell-nowrap">attributeType = blendFunc, modifyAttribute={*attrName* , *srcMode* , *dstMode* }</span> |  |
|  | *srcMode* and *dstMode* are each one of the following constants: |
|  |<table class="nested-table"><tbody><tr><td>0x0000:</td><td>GL_ZERO</td></tr><tr><td>0x0001:</td><td>GL_ONE</td></tr><tr><td>0x0306:</td><td>GL_DST_COLOR</td></tr><tr><td>0x0307:</td><td>GL_ONE_MINUS_DST_COLOR</td></tr><tr><td>0x0302:</td><td>GL_SRC_ALPHA</td></tr><tr><td>0x0303:</td><td>GL_ONE_MINUS_SRC_ALPHA</td></tr><tr><td>0x0305:</td><td>GL_ONE_MINUS_DST_ALPHA</td></tr><tr><td>0x0308:</td><td>GL_SRC_ALPHA_SATURATE</td></tr></tbody></table>
|  | For details see [Gizmo Colors, Material and Lights[Transparency and Translucency]](/igorpro/graphing/3d-graphics.md#transparency-and-translucency). |
| <span class="table-cell-nowrap">attributeType = alphaTestFunc, modifyAttribute={*attrName* , *testFormat* , *ref* }</span> |  |
|  | *testFormat* is one of the following constants: |
|  |<table class="nested-table"><tbody><tr><td>0x0200:</td><td>GL_NEVER</td></tr><tr><td>0x0207:</td><td>GL_ALWAYS</td></tr><tr><td>0x0201:</td><td>GL_LESS</td></tr><tr><td>0x0203:</td><td>GL_LEQUAL</td></tr><tr><td>0x0206:</td><td>GL_GEQUAL</td></tr><tr><td>0x0204:</td><td>GL_GREATER</td></tr><tr><td>0x0205:</td><td>GL_NOTEQUAL</td></tr><tr><td>0x0206:</td><td>GL_GEQUAL</td></tr></tbody></table>
|  | *ref* is a reference value in the range [0,1]. |
| <span class="table-cell-nowrap">attributeType = pointSize, modifyAttribute={*attrName* , *size* } (obsolete)</span> |  |
|  | *size* is a point size in pixels. |
|  | The pointSize attribute is obsolete and does nothing because of changes in OpenGL. |
| <span class="table-cell-nowrap">attributeType = lineWidth, modifyAttribute={*attrName* , *width* }</span> |  |
|  | *width* is a line width in pixels. |
|  | The lineWidth attribute is obsolete and does nothing because of changes in OpenGL. |
| <span class="table-cell-nowrap">attributeType = quadridDrawStyle, modifyAttribute={*attrName* , *style* } (deprecated)</span> |  |
|  | *style* is an OpenGL constant. |
|  | The quadricDrawStyle attribute is deprecated. It is now a built-in attribute of quadric objects. |
| <span class="table-cell-nowrap">attributeType = quadricNormals, modifyAttribute={*attrName* , *normals* } (deprecated)</span> |  |
|  | *normals* is an OpenGL constant. |
|  | The quadricNormals attribute is deprecated. It is now a built-in attribute of quadric objects. |
| <span class="table-cell-nowrap">attributeType = quadricOrientation, modifyAttribute={*attrName* , *orientation* } (deprecated)</span> |  |
|  | *orientation* is an OpenGL constant. |
|  | The quadricOrientation attribute is deprecated. It is now a built-in attribute of quadric objects. |




<!-- IndentedSubtopic -->
## ModifyGizmo for Operations {#modifygizmo-for-operations}

The syntax for modifying a Gizmo operation is:


```igor
ModifyGizmo opName=name, operation=type, data={dataVal [, dataVal]...}
```

The command affects only the particular named operation identified by *name* and *type*. For example, if you added a translate operation which you named "t1" the syntax is:


```igor
ModifyGizmo opName=t1, operation=translate, data={1,1,1}
```

The operation parameter *translate* identifies the type of operation that is to be performed and t1 identifies the specific operation. The data format is unique for each operation.


|  |  |
| --- | --- |
| <span class="table-cell-nowrap">operation = clearColor, data={*R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* are values in the range [0,1] specifying the color of the Gizmo display window background. |
| <span class="table-cell-nowrap">operation = clearTexture</span> |  |
|  | This operation takes no parameters. |
|  | Tests if 1D or 2D textures are enabled and if so they are disabled. Also disabled are S and T texture coordinates generation. |
| <span class="table-cell-nowrap">operation = clipPlane, data={*plane*, *A*, *B*, *C*, *D* }</span> |  |
|  | Creates a user-defined clipping plane. |
|  | *plane* is a plane number in the range [0,5]. |
|  | *A*, *B*, *C*, and *D* are constants that specify the plane as the locus of points (x,y,z) such that Ax+By+Cz+D=0. |
|  | Gizmo assumes that the OpenGL implementation supports a maximum of 6 clipping planes so using setOuterBox (axis range) and user-defined clipping planes are mutually exclusive. |
| <span class="table-cell-nowrap">operation = colorMaterial, data={*face*, *mode* }</span> |  |
|  | Applies color material properties to any face of the object. |
|  | *face* is 1028 (GL_FRONT), 1029 (GL_BACK) or 1032 (GL_FRONT_AND_BACK). |
|  | *mode* is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>0x1600:</td><td>GL_EMISSION - object surfaces emit light of the color specified.</td></tr><tr><td>0x1200:</td><td>GL_AMBIENT - affects only ambient illumination.</td></tr><tr><td>0x1201:</td><td>GL_DIFFUSE - affects only diffuse illumination.</td></tr><tr><td>0x1202:</td><td>GL_SPECULAR - rarely used.</td></tr><tr><td>0x1602:</td><td>GL_AMBIENT_AND_DIFFUSE - most commonly used.</td></tr></tbody></table>
|  | When you add a ColorMaterial operation to the display list, Gizmo automatically enables it so you do not need to precede it with Enable(ColorMaterial). However, you must add to the display list a Disable(colorMaterial) when you do not want it to affect subsequent objects. Disabling colorMaterial also improves display performance. |
| <span class="table-cell-nowrap">operation = dataTranslate, data={*dtx*, *dty*, *dtz* }</span> |  |
|  | Specifies the amount of translation of an object from its initial position in each dimension. |
|  | *dtx*, *dty*, and *dtz* are translation parameters in data coordinates. |
|  | See also translate below for translation in +/-1 display volume units coordinates. |
| <span class="table-cell-nowrap">operation = disable, data={*constant* }</span> |  |
|  | Disables an OpenGL feature. |
|  | *constant* is an OpenGL constant. There are 48 OpenGL constants for the enable and disable keywords. Examples are GL_BLEND, GL_TEXTURE_2D, and GL_LIGHT0. |
| <span class="table-cell-nowrap">operation = enable, data={*constant* }</span> |  |
|  | Disables an OpenGL feature. |
|  | *constant* is an OpenGL constant. There are 48 OpenGL constants for the enable and disable keywords. Examples are GL_BLEND, GL_TEXTURE_2D, and GL_LIGHT0. |
| <span class="table-cell-nowrap">operation = frontFace, data={*direction* }</span> |  |
|  | *direction* is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>0x0900:</td><td>GL_CW</td></tr><tr><td>0x0901:</td><td>GL_CCW</td></tr></tbody></table>
|  | In Igor 6 the default was GL_CW. It is now GL_CCW. |
| <span class="table-cell-nowrap">operation = frustrum, data={*left*, *right*, *bottom*, *top*, *zNear*, *zFar* }</span> |  |
|  | Multiplies the current transformation matrix by a perspective specified by the 6 clipping planes. |
|  | *left*, *right*, *bottom*, *top*, *zNear*, and *zFar* are coordinates in +/-1 display units. |
|  | Frustrum is similar to perspective operation but with slightly different and more flexible choice of parameters. See [Gizmo Projections](/igorpro/graphing/3d-graphics.md#gizmo-projections) for details. |
| <span class="table-cell-nowrap">operation = lightModel, data={*selector*, *p1*, *p2*, *p3*, *p4* }</span> |  |
|  | The meaning of *p1*, *p2*, *p3*, and *p4* depends on *selector* : |
|  | *selector* = 0x0B53 (ambient) |
|  |<table class="nested-table"><tbody><tr><td></td><td>*p1* through *p4* are RGBA values in the range [0,1] of ambient components.</td></tr></tbody></table>
|  | *selector* = 0x81F8 (color control) |
|  |<table class="nested-table"><tbody><tr><td></td><td>*p1* is 0x81F9 for GL_SINGLE_COLOR or 0x81FA for GL_SEPARATE_SPECULAR_COLOR. Pass zero for *p2* , *p3* , and *p4* .</td></tr></tbody></table>
|  | *selector* = 0x0B51 (local viewer) |
|  |<table class="nested-table"><tbody><tr><td></td><td>*p1* is 0 for viewing in the Z direction, 1 for viewing from the origin of the eye coordinate system. Pass zero for *p2* , *p3* , and *p4* .</td></tr></tbody></table>
|  | *selector* = 0x0B52 (two sided) |
|  |<table class="nested-table"><tbody><tr><td></td><td>*p1* is 0 for computing lighting only for the front surface, 1 for computing lighting for both sides of the surface. Pass zero for *p2* , *p3* , and *p4* .</td></tr></tbody></table>
| <span class="table-cell-nowrap">operation = loadIdentity</span> |  |
|  | This operation takes no parameters. |
|  | Replaces the current transformation matrix with an identity matrix; used to initialize matrix transformations. |
| <span class="table-cell-nowrap">operation = loadMatrix, data={*matrixWave* }</span> |  |
|  | Loads *matrixWave* as the current transformation matrix. |
|  | *matrixWave* is a 2D wave with 4 rows and 4 columns. |
| <span class="table-cell-nowrap">operation = lookAt, data={*ex*, *ey*, *ez*, *cx*, *cy*, *cz*, *ux*, *uy*, *uz* }</span> |  |
|  | Defines a viewing transformation defined by the eye position (*ex*,*ey*,*ez*), the position of a reference point (*cx*,*cy*,*cz*) and the up vector (*ux*,*uy*,*uz*). |
|  | *ex*, *ey*, and *ez* are X, Y, and Z components of the eye position expressed in +/-1 display volume coordinates. |
|  | *cx*, *cy*, and *cz* are X, Y, and Z components of the center of the scene (reference point) expressed in +/-1 display volume coordinates. |
|  | *ux*, *uy*, and *uz* are X, Y, and Z components of the up vector expressed in +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">operation = mainTransform</span> |  |
|  | This operation takes no parameters. |
|  | The main transform represents the orientation of the display volume as controlled by the keyboard and mouse. If you insert this operation in the middle of the display list, only items that appear below the main transform will rotate with the mouse while items that appear above it will be unaffected. |
| <span class="table-cell-nowrap">operation = matrixMode, data={*mode* }</span> |  |
|  | Specifies if the current transformation matrix is the model view or the projection matrix. |
|  | *mode* is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>0x1700:</td><td>GL_MODELVIEW</td></tr><tr><td>0x1701:</td><td>GL_PROJECTION</td></tr></tbody></table>
| <span class="table-cell-nowrap">operation = matrixMultiply, data={*matrixWave* }</span> |  |
|  | Multiply the current transformation matrix by the matrix represented by *matrixWave* . |
|  | *matrixWave* is a 2D wave with 4 rows and 4 columns. |
| <span class="table-cell-nowrap">operation = orth, data={*left*, *right*, *bottom*, *top*, *zNear*, *zFar* }</span> |  |
|  | Defines the spatial dimensions of the 3D display volume. You may have to modify them if you experience any unwanted clipping. |
|  | *left*, *right*, *bottom*, *top*, *zNear*, and *zFar* are coordinates in +/-1 display units. |
|  | See [Gizmo Projections](/igorpro/graphing/3d-graphics.md#gizmo-projections) for details. |
| <span class="table-cell-nowrap">operation = perspective, data={*fov*, *aspect*, *zNear*, *zFar* }</span> |  |
|  | Specifies a perspective projection of the viewing volume. This is the default perspective. |
|  | *fov*, *aspect*, *zNear*, and *zFar* are coordinates in +/-1 display units. |
|  | *fov* is the field of view in the Y-direction (angle in degrees), *aspect* is the ratio of the X and Y directions for the clipping planes, and the two Z values specify the front (*zNear* ) and rear (*zFar* ) clipping planes. |
|  | See [Gizmo Projections](/igorpro/graphing/3d-graphics.md#gizmo-projections) for details. |
| <span class="table-cell-nowrap">operation = popAttribute</span> |  |
|  | This operation takes no parameters. |
|  | Pops the top attribute from the attribute stack, reverting to the state as saved by the last pushAttribute operation. |
| <span class="table-cell-nowrap">operation = popMatrix</span> |  |
|  | This operation takes no parameters. |
|  | Pops the top transformation matrix from the transformation matrix stack, reverting to the state as saved by the last pushMatrix operation. |
| <span class="table-cell-nowrap">operation = pushAttribute, data={*mask* }</span> |  |
|  | Specifies the attributes to push onto the attribute stack. This operation is used to save a drawing state for temporary change which can be reverted by a popAttribute operation. |
|  | *mask* is an OpenGL constant. To push all attributes use 0x000FFFFF (GL_ALL_ATTRIB_BITS). |
| <span class="table-cell-nowrap">operation = pushMatrix</span> |  |
|  | This operation takes no parameters. |
|  | Pushes the current transformation matrix to the top of the transformation matrix stack. |
|  | The pushMatrix operation is used for temporary drawing with a different transformation. It pushes the current transformation matrix onto the transformation matrix stack. Follow this by an operation that changes the transformation matrix, such as loadMatrix or matrixMultiply, and some drawing commands. Clean up with a popMatrix operation to restore the original transformation matrix. |
| <span class="table-cell-nowrap">operation = rotate, data={*angle*, *ax*, *ay*, *az* }</span> |  |
|  | Rotates the display. |
|  | *angle* is the angle in degrees about which you want to rotate. |
|  | *ax*, *ay*, and *az* are X, Y, and Z components of a vector about which to perform the rotation. |
| <span class="table-cell-nowrap">operation = scale, data={*sx*, *sy*, *sz* }</span> |  |
|  | Scales the display relative to the current scaling. |
|  | *sx*, *sy*, and *sz* are X, Y, and Z scaling factors. A scaling factor of 1 leaves the scaling unchanged. |
| <span class="table-cell-nowrap">operation = shadingModel, data={*model* }</span> |  |
|  | Specifies the shading model to use. |
|  | *model* is one fo the following: |
|  |<table class="nested-table"><tbody><tr><td>0x1D00:</td><td>GL_FLAT</td></tr><tr><td>0x1D01:</td><td>GL_SMOOTH</td></tr></tbody></table>
|  | By default Gizmo uses smooth shading unless there is a shading model operation in the display list. |
| <span class="table-cell-nowrap">operation = translate, data={*dx*, *dy*, *dz* }</span> |  |
|  | Scales the display relative to the current scaling using +/-1 display volume units. See also dataTranslate. |
|  | *dx*, *dy*, and *dz* are X, Y, and Z translation components in +/-1 display volume units. |
| <span class="table-cell-nowrap">operation = viewport, data={*left*, *bottom*, *width*, *height* }</span> |  |
|  | Specifies the viewport rectangle. |
|  | *left*, *bottom*, *width*, and *height* are coordinates in screen pixels. |
|  | The initial values for *left* and *bottom* are (0,0). |
|  | You should not need to use this operation as Gizmo automatically updates the viewport to the full size of the Gizmo display window. |



<!-- IndentedSubtopic -->
## ModifyGizmo for Objects {#modifygizmo-for-objects}

The syntax for modifying a Gizmo object is:


```igor
ModifyGizmo modifyObject=objName, objectType=type, property={propertyName,data}
```

*objName*  is the name that was assigned to the object.

*type*  is the generic object type, e.g., path, ribbon, surface, etc.

*propertyName*  specifies the property to be modified.

*data*  represents a variable number of parameters that depend on the type of property being modified.

The following sections describe modification of the supported object types. They are arranged in the order of appearance in the object menu (+ icon under the object list) of the Gizmo info window. The sections are:

[ModifyGizmo for Path Objects](#modifygizmo-for-path-objects)

[ModifyGizmo for Ribbon Objects](#modifygizmo-for-ribbon-objects)

[ModifyGizmo for Surface Objects](#modifygizmo-for-surface-objects)

[ModifyGizmo for Isosurface Objects](#modifygizmo-for-isosurface-objects)

[ModifyGizmo for Voxelgram Objects](#modifygizmo-for-voxelgram-objects)

[ModifyGizmo for Scatter Objects](#modifygizmo-for-scatter-objects)

[ModifyGizmo for 3D Bar Chart Objects](#modifygizmo-for-3d-bar-chart-objects)

[ModifyGizmo for Image Objects](#modifygizmo-for-image-objects)

[ModifyGizmo for Axis Objects](#modifygizmo-for-axis-objects)

[ModifyGizmo for Free Axis Cue Objects](#modifygizmo-for-free-axis-cue-objects)

[ModifyGizmo for Line Objects](#modifygizmo-for-line-objects)

[ModifyGizmo for Triangle Objects](#modifygizmo-for-triangle-objects)

[ModifyGizmo for Quad Objects](#modifygizmo-for-quad-objects)

[ModifyGizmo for Box Objects](#modifygizmo-for-box-objects)

[ModifyGizmo for Sphere Objects](#modifygizmo-for-sphere-objects)

[ModifyGizmo for Cylinder Objects](#modifygizmo-for-cylinder-objects)

[ModifyGizmo for Disk Objects](#modifygizmo-for-disk-objects)

[ModifyGizmo for Tetrahedron Objects](#modifygizmo-for-tetrahedron-objects)

[ModifyGizmo for Pie Wedge Objects](#modifygizmo-for-pie-wedge-objects)

[ModifyGizmo for Light Objects](#modifygizmo-for-light-objects)

[ModifyGizmo for Texture Objects](#modifygizmo-for-texture-objects)

[ModifyGizmo for Matrix4x4 Objects](#modifygizmo-for-matrix4x4-objects)

[ModifyGizmo for String Objects](#modifygizmo-for-string-objects)

[ModifyGizmo for ColorScale Objects](#modifygizmo-for-colorscale-objects)



<!-- IndentedSubtopic -->
## ModifyGizmo for Path Objects {#modifygizmo-for-path-objects}

The syntax for modifying a Gizmo path object is:


```igor
ModifyGizmo modifyObject=objName, objectType=path, property={propertyName,data}
```

For background information and examples see [Gizmo Data Objects[Path Plots]](/igorpro/graphing/3d-graphics.md#path-plots).

All of the properties supported for path objects also apply to ribbon objects.

### *Keywords* {#modifygizmo-for-path-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
|  | calcNormals is not relevant if you are drawing a simple line path. It is used in when drawing paths as 3D tubes and for ribbon objects. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the path/ribbon object is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped.</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {CTABAlpha, *alpha* }</span> |  |
|  | Sets the alpha component for colors for the object when those colors are derived from an Igor color table. |
|  | *alpha* is an alpha value the range [0,1]. For more information see [Transparency and Translucency](/igorpro/graphing/3d-graphics.md#transparency-and-translucency). |
| <span class="table-cell-nowrap">property = {CTABScaling, *mode* }</span> |  |
|  | *mode* is a bitwise setting that controls the path coloring when using a color table. |
|  | One and only one bit from bit 0 through 4 must be set. In addition, any of bits 5, 6, 8 or 9 may be set. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>From min X to max X</td></tr><tr><td>Bit&nbsp;1:</td><td>From min Y to max Y</td></tr><tr><td>Bit&nbsp;2:</td><td>From min Z to max Z</td></tr><tr><td>Bit&nbsp;3:</td><td>From 0 to max sqrt(X^2+Y^2)</td></tr><tr><td>Bit&nbsp;4:</td><td>From 0 to max sqrt(X^2+Y^2+Z^2)</td></tr><tr><td>Bit&nbsp;5:</td><td>Minimum value and color specified</td></tr><tr><td>Bit&nbsp;6:</td><td>Maximum value and color specified</td></tr><tr><td>Bit&nbsp;7:</td><td>Not used - set to 0</td></tr><tr><td>Bit&nbsp;8:</td><td>Color table maps plot-global X range</td></tr><tr><td>Bit&nbsp;9:</td><td>Color table maps plot-global Y range</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {drawEndCaps, *mode* }</span> |  |
|  | drawEndCaps applies only when drawing tubes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>The ends of each segment are not capped.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>The ends of segments are capped with a plane perpendicular to the segment.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {drawTube, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Draws a standard path plot.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Draws the path as a tube with a fixed radius.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Draws the path as a tube with user-specified radii at every vertex.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {fixedRadius, *radius* }</span> |  |
|  | When drawing a path as a tube of fixed radius, *radius* is used for every vertex of the tube. *radius* is expressed in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {inverseCTab, *mode* }</span> |  |
|  | Specifies if the color table used to draw the path is inverted. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not inverted.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Inverted.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {linewidth, *width* } (deprecated)</span> |  |
|  | Specifies the line width in points. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {lineWidthType, *type* } (deprecated)</span> |  |
|  | Specifies how line width is determined. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Not specified by this object.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Specified by this object.</td></tr></tbody></table>
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {pathColor, *R*, *G*, *B*, *A* }</span> |  |
|  | R, G, B, A values in the range [0,1] specify a single color for the whole path. |
| <span class="table-cell-nowrap">property = {pathCTab, *name* }</span> |  |
|  | *name* specifies a built-in Igor color table to use for path colors. For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {pathColorType, *type* }</span> |  |
|  | Specifies the type of path coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use pathColor to specify the color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Color wave. Use pathColorWave to specify the color wave.</td></tr><tr><td>*type*&nbsp;=3:</td><td>Color table. Use pathCTab to specify the color table.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {pathColorWave, *wave* }</span> |  |
|  | *wave* contains R, G, B, A values in the range [0,1] specifying the color of each vertex. For more information see [Color Waves](/igorpro/graphing/3d-graphics.md#color-waves). |
| <span class="table-cell-nowrap">property = {pathRadiusWave, *wave* }</span> |  |
|  | *wave* is the name of a 1D SP or DP wave containing the radius of the path tube (see drawTube above). The radius wave provides a single scalar for each vertex in the path. The radius wave may contain arbitrary values for points in the path wave that contain NaN. Although there is a single radius value for each path vertex, the cross-section of the tube is, in general, not circular because of different scaling along the three axes. See also fixedRadius above. |
| <span class="table-cell-nowrap">property = {maxRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled maximum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {minRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled minimum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {numSegments, *n* }</span> |  |
|  | *n* is the number of segments in the cross-section of a tube. *n* must be 4 or more. It is 20 by default. |
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> |  |
|  | *wave* identifies the triplet wave describing the X, Y and Z coordinates for each point on the path. |
| <span class="table-cell-nowrap">property = {quaternary, *mode* }</span> |  |
|  | Used to match a scatter plot quaternary property. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Disables the quaternary display of the data.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Enables quaternary display of data.</td></tr></tbody></table>


<!-- IndentedSubtopic -->
## ModifyGizmo for Ribbon Objects {#modifygizmo-for-ribbon-objects}

The syntax for modifying a Gizmo ribbon object is:


```igor
ModifyGizmo modifyObject=objName, objectType=ribbon, property={propertyName,data}
```

All ribbon object properties are identical to path object properties above. See [ModifyGizmo for Path Objects](#modifygizmo-for-path-objects).

For more information also see [Ribbon Plots](/igorpro/graphing/3d-graphics.md#ribbon-plots).


<!-- IndentedSubtopic -->
## ModifyGizmo for Surface Objects {#modifygizmo-for-surface-objects}

The syntax for modifying a Gizmo surface object is:


```igor
ModifyGizmo modifyObject=objName, objectType=surface, property={propertyName,data}
```

For more information also see [Surface Plots](/igorpro/graphing/3d-graphics.md#surface-plots).

### *Keywords* {#modifygizmo-for-surface-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {backColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of the back side of the surface. |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the surface is clipped by the global clipping planes. |
| <span class="table-cell-nowrap">*mode* = 0:</span> | Not clipped. |
| <span class="table-cell-nowrap">*mode* = 1:</span> | Clipped. |
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {fillMode, *mode* }</span> |  |
|  | Specifies the surface fill mode: |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=1:</td><td>Wireframe or grid</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Color fill</td></tr><tr><td>*mode*&nbsp;=4:</td><td>Point cloud</td></tr><tr><td>*mode*&nbsp;=5:</td><td>Scatter</td></tr><tr><td>*mode*&nbsp;=3:</td><td>Color fill and wireframe</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {frontColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of the front side of the surface. The front color applies when fillMode is set for color fill and when surfaceColorType is set to a constant color. |
| <span class="table-cell-nowrap">property = {inverseLineCTab, *mode* }</span> |  |
|  | Specifies if the color table used to draw the surface grid lines is inverted. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not inverted</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Inverted</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {inverseSurfaceCTab, *mode* }</span> |  |
|  | Specifies if the color table used to draw the surface is inverted. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not inverted</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Inverted</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {lineColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of grid lines. This property applies when drawing a wireframe/grid and when lineColorType is set to a constant color. |
| <span class="table-cell-nowrap">property = {lineColorType, *type* }</span> |  |
|  | Specifies the type of grid line coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use lineColor to specify the color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Color table. Use lineCTab to specify the color table.</td></tr><tr><td>*type*&nbsp;=3:</td><td>Color wave. Use lineColorWave to specify the color wave.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {lineColorWave, *wave* }</span> |  |
|  | *wave* contains R, G, B, A values in the range [0,1] for coloring grid lines. The same wave can be used for grid-line color and for the surface. For more information see [Color Waves](/igorpro/graphing/3d-graphics.md#color-waves). |
| <span class="table-cell-nowrap">property = {lineCTab, *name* }</span> |  |
|  | *name* specifies a built-in Igor color table to use for grid line colors. For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {lineCTABAlpha, *alpha* }</span> |  |
|  | Sets the alpha component for colors for the grid lines when those colors are derived from an Igor color table. |
|  | *alpha* is an alpha value the range [0,1]. For more information see [Transparency and Translucency](/igorpro/graphing/3d-graphics.md#transparency-and-translucency). |
| <span class="table-cell-nowrap">property = {lineCTABScaling, *mode* }</span> |  |
|  | Same as surfaceCTABScaling below but applies to the grid lines. |
| <span class="table-cell-nowrap">property = {lineMaxRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled maximum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {lineMinRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled minimum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {linewidth, *width* } (deprecated)</span> |  |
|  | Specifies the grid line width in points. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {lineWidthType, *type* } (deprecated)</span> |  |
|  | Specifies how grid line width is determined. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Not specified by the surface object</td></tr><tr><td>*type*&nbsp;=1:</td><td>Specified by the surface object</td></tr></tbody></table>
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {plane, *index* }</span> |  |
|  | *index* is a zero-based integer specifying the plane of the volumetric data that is to be displayed. |
|  | This property applies when srcMode=32 (Z slices), 64 (Y slices) or 128 (X slices). For Z slices *index* specifies the layer of the source wave, for Y slices it specifies the column, and for X-slices it specifies the row. |
| <span class="table-cell-nowrap">property = {srcMode, *format* }</span> |  |
|  | Specifies the source wave data format: |
|  |<table class="nested-table"><tbody><tr><td>*format*&nbsp;=0:</td><td>Matrix wave. A 2D wave containing MxN Z values on a rectangular grid. The X and Y dimensions are optionally specified by wave scaling.</td></tr><tr><td>*format*&nbsp;=1:</td><td>Triangles wave. A triplet wave in which each row corresponds to a sequential vertex and the columns correspond to the X, Y and Z components.</td></tr><tr><td>*format*&nbsp;=4:</td><td>Parametric data. A 3D MxNx3 wave where the MxN vertices are specified by the X, Y and Z values in the corresponding layers.</td></tr><tr><td>*format*&nbsp;=8:</td><td>Sequential quads. An Mx4x3 wave that describes M quads, each consisting of 4 vertices and X, Y and Z values in the corresponding layers.</td></tr><tr><td>*format*&nbsp;=16:</td><td>Disjoint quads. An Mx12 wave that describes M quads where the 12 rows correspond to the X, Y and Z components of each quad&#39;s vertices. For the purpose of calculating normals, it is assumed that the order of the vertices is the same throughout the wave.</td></tr><tr><td>*format*&nbsp;=32:</td><td>Z slices of a volumetric (3D) wave.</td></tr><tr><td>*format*&nbsp;=64:</td><td>Y-slices of a volumetric (3D) wave.</td></tr><tr><td>*format*&nbsp;=128:</td><td>X-slices of a volumetric (3D) wave.</td></tr></tbody></table>
|  | For more information see [Gizmo Wave Data Formats](/igorpro/graphing/3d-graphics.md#gizmo-wave-data-formats). |
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> |  |
|  | Specifies the source wave for the surface. |
| <span class="table-cell-nowrap">property = {surfaceColorType, *type* }</span> |  |
|  | Specifies the type of surface coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use frontColor and backColor to specify the surface color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Color table. Use surfaceCTab to specify the color table.</td></tr><tr><td>*type*&nbsp;=3:</td><td>Color wave. Use surfaceColorWave to specify the color wave.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {surfaceColorWave, *wave* }</span> |  |
|  | *wave* contains R, G, B, A values in the range [0,1] for coloring the surface. For more information see [Color Waves](/igorpro/graphing/3d-graphics.md#color-waves). |
| <span class="table-cell-nowrap">property = {surfaceCTab, *name* }</span> |  |
|  | *name* specifies a built-in Igor color table to use for surface colors. For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {surfaceCTABScaling, *mode* }</span> |  |
|  | *mode* is a bitwise setting that controls the surface coloring when using a color table. |
|  | One and only one bit from bit 0 through 4 must be set. In addition, any of bits 5, 6, 7, 8 or 9 may be set. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>From min X to max X</td></tr><tr><td>Bit&nbsp;1:</td><td>From min Y to max Y</td></tr><tr><td>Bit&nbsp;2:</td><td>From min Z to max Z</td></tr><tr><td>Bit&nbsp;3:</td><td>From 0 to max sqrt(X^2+Y^2)</td></tr><tr><td>Bit&nbsp;4:</td><td>From 0 to max sqrt(X^2+Y^2+Z^2)</td></tr><tr><td>Bit&nbsp;5:</td><td>Minimum value and color specified</td></tr><tr><td>Bit&nbsp;6:</td><td>Maximum value and color specified</td></tr><tr><td>Bit&nbsp;7:</td><td>Set for volume slices</td></tr><tr><td>Bit&nbsp;8:</td><td>Color table maps plot-global X range</td></tr><tr><td>Bit&nbsp;9:</td><td>Color table maps plot-global Y range</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {surfaceMaxRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled maximum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {surfaceMinRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled minimum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {surfaceCTABAlpha, *alpha* }</span> |  |
|  | Sets the alpha component for colors for the surface when those colors are derived from an Igor color table. |
|  | *alpha* is an alpha value the range [0,1]. For more information see [Transparency and Translucency](/igorpro/graphing/3d-graphics.md#transparency-and-translucency). |
| <span class="table-cell-nowrap">property = {xStep, *step* }</span> |  |
|  | Specifies the X sampling of the grid lines in a wireframe. Set this to 1 to show all grid lines, 2 to show every other grid line, etc. |
| <span class="table-cell-nowrap">property = {yStep, *step* }</span> |  |
|  | Specifies the Y sampling of the grid lines in a wireframe. Set this to 1 to show all grid lines, 2 to show every other grid line, etc. |



<!-- IndentedSubtopic -->
## ModifyGizmo for Isosurface Objects {#modifygizmo-for-isosurface-objects}

The syntax for modifying a Gizmo isosurface object is:


```igor
ModifyGizmo modifyObject=objName, objectType=isosurface, property={propertyName,data}
```

For more information also see [Isosurface Plots](/igorpro/graphing/3d-graphics.md#isosurface-plots).

### *Keywords* {#modifygizmo-for-isosurface-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {backColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of the back side of the surface. This property applies when fillMode=2 and surfaceColorType=1. |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the surface is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {fillMode, *mode* }</span> |  |
|  | Specifies the surface fill mode The following values may be combined: |
|  |<table class="nested-table"><tbody><tr><td>*mode*=1:</td><td>Wireframe or grid</td></tr><tr><td>*mode*=2:</td><td>Color fill</td></tr><tr><td>*mode*=4:</td><td>Point cloud</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {frontColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of the front side of the surface. The front color applies when *fillMode*=2 and when *surfaceColorType*=1. |
| <span class="table-cell-nowrap">property = {isovalue, *value* }</span> |  |
|  | Specifies a real, finite scalar value at which the surface is formed. |
| <span class="table-cell-nowrap">property = {lineColor, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color of the isosurface point cloud when *lineColorType* is set to 1. *R*, *G*, *B*, and *A* in the range [0,1]. |
| This property was added in Igor Pro 9.00. |  |
| <span class="table-cell-nowrap">property = {lineColorType, *type* }</span> |  |
|  | Specifies the coloring of the isosurface point cloud: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Constant color that is determined by the last color setting in the display list prior to drawing the cloud.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use the *lineColor* property to specify the RGBA components.</td></tr></tbody></table>
| This property was added in Igor Pro 9.00. |  |
| <span class="table-cell-nowrap">property = {surfaceColorType, *type* }</span> |  |
|  | Specifies the type of surface coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Surface color is specified outside the object.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color surface. Use *frontColor* and *backColor* to specify the surface color.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {saveToWave, *outWaveNameStr* }</span> |  |
|  | Creates a wave containing triangles that describe the isosurface. |
|  | *outWaveNameStr* is a string containing the name to use for the output wave. The output wave is a triplet wave created in the current data folder. Each row contains the X, Y and Z coordinates of a single vertex and every three consecutive rows define a triangle from the isosurface. The triangles are not ordered in any way. The DepthSortingDemo experiment illustrates the use of this wave. |
| <span class="table-cell-nowrap">property = {useTBB, *mode* }</span> |  |
|  | Determines if the surface is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Do not use automatic multithreading to compute the surface.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Default. Use automatic multithreading to compute the surface.</td></tr></tbody></table>


<!-- IndentedSubtopic -->
## ModifyGizmo for Voxelgram Objects {#modifygizmo-for-voxelgram-objects}

The syntax for modifying a Gizmo voxelgram object is:


```igor
ModifyGizmo modifyObject=objName, objectType=voxelgram, property={propertyName,data}
```

For more information also see [Voxelgram Plots](/igorpro/graphing/3d-graphics.md#voxelgram-plots).

### *Keywords* {#modifygizmo-for-voxelgram-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {boxSize, *bx*, *by*, *bz* }</span> |  |
|  | When drawing a voxelgram in cubes mode, you can specify the relative size of the cube. By default, *bx* =*by* =*bz* =1 and the cube occupies half the size of the voxel cell in each dimension. You can set *bx* =*by* =*bz* =2 to draw box markers that completely fill the voxel cell. The accepted range for *bx*, *by*, and *bz* is (0,2]. |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the voxelgram is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {mode, *mode* }</span> |  |
|  | Specifies how voxels are displayed: |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Voxels displayed as points</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Voxels displayed as cubes</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> |  |
|  | Specifies the source wave for the voxelgram. This must be a real-valued 3D wave. |
| <span class="table-cell-nowrap">property = {tolerance, *tolValue* }</span> |  |
|  | *tolValue* is a non-negative number which determines the neighborhood around the specified values where accepted voxels are marked. |
|  | If *tolValue* is set to zero then only voxels having exactly the specified values will be marked. This sometimes causes problems when one attempts to mark integer values in an SP or DP wave. |
| <span class="table-cell-nowrap">property = {minRGBA, *levelIndex*, *levelValue*, *R*, *G*, *B*, *A* }</span> |  |
|  | *levelIndex* specifies the index of the level for the color. |
|  | *levelValue* is a real, finite scalar value at which the points or cubes are drawn. |
|  | *R*, *G*, *B*, and *A* are values in the range [0,1] specifying the color to use for voxels. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Scatter Objects {#modifygizmo-for-scatter-objects}

The syntax for modifying a Gizmo scatter object is:


```igor
ModifyGizmo modifyObject=objName, objectType=scatter, property={propertyName,data}
```

For more information also see [3D Scatter Plots](/igorpro/graphing/3d-graphics.md#3d-scatter-plots).

### *Keywords* {#modifygizmo-for-scatter-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {color, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify a single color for all markers. |
| <span class="table-cell-nowrap">property = {CTabAlpha, *alpha* }</span> |  |
|  | Sets the alpha component for colors for the markers when those colors are derived from an Igor color table. |
|  | *alpha* is an alpha value the range [0,1]. For more information see [Transparency and Translucency](/igorpro/graphing/3d-graphics.md#transparency-and-translucency). |
| <span class="table-cell-nowrap">property = {CTABScaling, *mode* }</span> |  |
|  | *mode* is a bitwise setting that controls the marker coloring when using a color table. |
|  | One and only one bit from bit 0 through 4 must be set. In addition, any of bits 5, 6, 8 or 9 may be set. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>From min X to max X</td></tr><tr><td>Bit&nbsp;1:</td><td>From min Y to max Y</td></tr><tr><td>Bit&nbsp;2:</td><td>From min Z to max Z</td></tr><tr><td>Bit&nbsp;3:</td><td>From 0 to max sqrt(X^2+Y^2)</td></tr><tr><td>Bit&nbsp;4:</td><td>From 0 to max sqrt(X^2+Y^2+Z^2)</td></tr><tr><td>Bit&nbsp;5:</td><td>Minimum value and color specified</td></tr><tr><td>Bit&nbsp;6:</td><td>Maximum value and color specified</td></tr><tr><td>Bit&nbsp;7:</td><td>Not used - set to 0</td></tr><tr><td>Bit&nbsp;8:</td><td>Color table maps plot-global X range</td></tr><tr><td>Bit&nbsp;9:</td><td>Color table maps plot-global Y range</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {colorWave, *wave* }</span> |  |
|  | *wave* is a 2D wave containing R, G, B, A values in the range [0,1] specifying the color of each marker. For an Mx3 scatter source wave the colorWave is Mx4 with RGBA values in each row. For more information see [Color Waves](/igorpro/graphing/3d-graphics.md#color-waves). |
| <span class="table-cell-nowrap">property = {dropLines, *val* }</span> |  |
|  | Controls the drawing of drop lines. *val* is a bitwise setting with zero or more of the following bits set: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>To minimum X plane</td></tr><tr><td>Bit&nbsp;1:</td><td>To maximum X plane</td></tr><tr><td>Bit&nbsp;2:</td><td>To minimum Y plane</td></tr><tr><td>Bit&nbsp;3:</td><td>To maximum Y plane</td></tr><tr><td>Bit&nbsp;4:</td><td>To minimum Z plane</td></tr><tr><td>Bit&nbsp;5:</td><td>To maximum Z plane</td></tr><tr><td>Bit&nbsp;6:</td><td>To the X-axis (cube center)</td></tr><tr><td>Bit&nbsp;7:</td><td>To Y-axis</td></tr><tr><td>Bit&nbsp;8:</td><td>To Z-axis</td></tr><tr><td>Bit&nbsp;9:</td><td>To the center of the cube</td></tr><tr><td>Bit&nbsp;10:</td><td>To the origin</td></tr><tr><td>Bit&nbsp;11:</td><td>To a fixed X level</td></tr><tr><td>Bit&nbsp;12:</td><td>To a fixed Y level</td></tr><tr><td>Bit&nbsp;13:</td><td>To a fixed Z level</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">property = {dropLineColorType, *type* }</span> |  |
|  | Specifies the type of drop line coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Same color as the marker object.</td></tr><tr><td>*type*&nbsp;=1:</td><td>R, G, B, A values specified by the dropLineRGBA keyword.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {dropLineLevelX, *level* }</span> |  |
|  | The X value to which the drop line extends when bit 11 of the dropLines keyword is set. |
| <span class="table-cell-nowrap">property = {dropLineLevelY, *level* }</span> |  |
|  | The Y value to which the drop line extends when bit 12 of the dropLines keyword is set. |
| <span class="table-cell-nowrap">property = {dropLineLevelZ, *level* }</span> |  |
|  | The Z value to which the drop line extends when bit 13 of the dropLines keyword is set. |
| <span class="table-cell-nowrap">property = {dropLineRGBA, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of all drop lines. |
| <span class="table-cell-nowrap">property = {dropLineWidth, *width* } (deprecated)</span> |  |
|  | Specifies the drop line width in pixels. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {fontName, *fontNameStr* }</span> |  |
|  | *fontNameStr* is the name of a font, such as "Arial", to use to draw the axis label. |
| <span class="table-cell-nowrap">property = {inverseCTab, *mode* }</span> |  |
|  | Specifies if the color table used to draw the markers is inverted. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not inverted</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Inverted</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {markerCTab, *name* }</span> |  |
|  | *name* specifies a built-in Igor color table to use for marker colors. The scatterColorType property must be set to 3. For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {markerType, *type* }</span> |  |
|  | Specifies how markers are selected: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Constant marker type. Use the shape property to specify the marker.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Marker type specified by a marker wave. Use the typeWave property to identify the wave.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {maxRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled maximum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {minRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | In X, Y, or Z range, use an unscaled minimum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. In radial modes, use scaled [0,1] value followed by R, G, B, A. |
| <span class="table-cell-nowrap">property = {objectName, *name* }</span> |  |
|  | The name of an object in the object list to draw as a marker. |
| <span class="table-cell-nowrap">property = {quadricFacets, *numFacets* }</span> |  |
|  | *numFacets* is the number of facets of a quadric object used as a marker. This applies to sphere, cylinder and disk shapes. The number of facets is used for the slices and stacks of the quadrics. By default, quadricFacets=10. Set the number higher to draw smoother quadrics or lower if you are concerned about performance. |
| <span class="table-cell-nowrap">property = {quaternary, *mode* }</span> |  |
|  | Used to match a scatter plot quaternary property. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Disables quaternary interpretation.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Interprets the triplet source as fractional values of 3 out of 4 mixture components. The internal scaling involves the following transformation for fractional components a,b,c:</td></tr><tr><td></td><td>`d = 1.0-a-b-c`</td></tr><tr><td></td><td>`x = ((a-0.25)+0.5*(b-0.25)+0.5*(d-0.25))/0.8165`</td></tr><tr><td></td><td>`y = ((b-0.25)+(d-0.25)/3)/0.9428`</td></tr><tr><td></td><td>`z = d-0.25`</td></tr><tr><td></td><td>You can create a frame corresponding to the tetrahedron or its vertices by transforming the points corresponding to the triplets {{1,0,0},{0,1,0},{0,0,1},{0,0,0}}. The results are the following XYZ triplets:</td></tr><tr><td></td><td>` 0.61237    -0.353557   -0.25`</td></tr><tr><td></td><td>` 0           0.707114   -0.25`</td></tr><tr><td></td><td>`-0.61237    -0.353557   -0.25`</td></tr><tr><td></td><td>` 0           0           0.75`</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {rotateFirst, *mode* }</span> |  |
|  | Specifies the order of rotate and scale operations. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>First scale the marker and then rotate.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>First rotate the marker and then scale.</td></tr></tbody></table>
|  | This property is useful when scaling is not isotropic. |
| <span class="table-cell-nowrap">property = {rotationType, *type* }</span> |  |
|  | Specifies how markers are rotated. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No rotation.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Rotation specified by the rotationWave property.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {rotationWave, *wave* }</span> |  |
|  | Specifies the 2D Mx4 rotation wave for the markers. For each marker the rotation wave has a corresponding row of data containing four entries in this order: the angle in degrees, the rotation axis components in the X, Y, and Z directions. |
| <span class="table-cell-nowrap">property = {scatterColorType, *type* }</span> |  |
|  | Specifies the type of marker coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Constant color. Use the color property to specify the color of all markers.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Color wave. Use the colorWave property to specify the color wave.</td></tr><tr><td>*type*&nbsp;=2:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=3:</td><td>Color table. Use markerCTab to specify the color table.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {shape, *val* }</span> |  |
|  | Specifies the marker shape. *val* is one of the following: |
|  |<table class="nested-table"><tbody><tr><td>1:</td><td>Point</td></tr><tr><td>2:</td><td>Sphere</td></tr><tr><td>3:</td><td>Cylinder</td></tr><tr><td>4:</td><td>Disk</td></tr><tr><td>5:</td><td>Box</td></tr><tr><td>6:</td><td>Axis object</td></tr><tr><td>7:</td><td>Any other object in the object list.</td></tr></tbody></table>
|  | Not valid for use with markerType=1. |
|  |<table class="nested-table"><tbody><tr><td>8:</td><td>Text. This is not valid for use with markerType=1.</td></tr><tr><td>9:</td><td>Cone</td></tr><tr><td>10:</td><td>Double Cone</td></tr><tr><td>11:</td><td>Cone and Disk</td></tr><tr><td>12:</td><td>Ring</td></tr><tr><td>13:</td><td>Double Ring</td></tr><tr><td>14:</td><td>Sphere shell</td></tr><tr><td>15:</td><td>Cylinder shell</td></tr><tr><td>16:</td><td>Cone shell</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {size, *val* }</span> |  |
|  | Specifies the marker size. *val* is a scalar value relative to the axis coordinate system as set by Gizmo→Axis Range. See also [Gizmo Dimensions](/igorpro/graphing/3d-graphics.md#gizmo-dimensions). |
| <span class="table-cell-nowrap">property = {size, *type* }</span> |  |
|  | Specifies how markers are sized: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Constant size. Use the size property to specify a uniform marker size.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Size wave. Use the sizeWave property to identify the wave.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {sizeWave, *wave* }</span> |  |
|  | *wave* is a 2D 3 column wave specifying the marker size for each scatter point. The three columns contain the scaling factors in the X, Y and Z directions respectively. |
|  | A size of 1 corresponds to a sphere that occupies most of the display volume. Typically, scatter objects are best represented by significantly smaller values. |
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> |  |
|  | *wave* identifies the triplet wave describing the X, Y and Z coordinates for each point in the scatter plot. |
| <span class="table-cell-nowrap">property = {textWave, *wave* }</span> |  |
|  | *wave* identifies wave containing the text to display for each marker when shape=8. The wave must have one row per marker. For practical reasons each text wave point should contain no more than a few characters. |
| <span class="table-cell-nowrap">property = {typeWave, *wave* }</span> |  |
|  | *wave* identifies a 1D wave specifying the integer marker type for each corresponding marker. See the shape property for available marker types and values. *typeWave* should contain the same number of points as in the scatter wave. There is no error if *typeWave* is longer. |



<!-- IndentedSubtopic -->
## ModifyGizmo for 3D Bar Chart Objects {#modifygizmo-for-3d-bar-chart-objects}

The syntax for modifying a Gizmo 3D bar chart object is:


```igor
ModifyGizmo modifyObject=objName, objectType=bar3D, property={propertyName,data}
```

For more information also see [3D Bar Plots](/igorpro/graphing/3d-graphics.md#3d-bar-plots).

### *Keywords* {#modifygizmo-for-3d-bar-chart-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of grid line coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use *colorValue* to specify the color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Color wave. Use *colorWave* to specify the color wave.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {colorValue, *colorNum*, *R*, *G*, *B*, *A* }</span> |  |
|  | Set colorNum to 0; other values are reserved. The remaining components are in the range [0,1]. This color is used when colorType=1 for all bars. |
| <span class="table-cell-nowrap">property = {colorWave, *wave* }</span> |  |
|  | *wave* is a 2D wave containing RGBA values in the range [0,1] specifying the color of each bar. |
|  | The dimensions of the color wave depends on the number of bars and on srcMode. When drawing a basic 3D bar chart (srcMode=0) the color wave is a 4-layer wave with the same number of rows and columns as srcWave. The layers of colorWave contain the color R, G, B, and A components respectively. |
|  | When drawing a refined 3D bar chart (srcMode=1) the color wave is a 4 column 2D wave where the columns contain the R, G, B, and A color components and the rows correspond to the bars (rows of srcWave). |
| <span class="table-cell-nowrap">property = {srcMode, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Basic 3D bar chart</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Refined 3D bar chart</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> |  |
|  | *wave* identifies the source wave for the 3D bar chart chart. |
|  | When srcMode=0 *wave* is a 2D numeric wave containing non-negative entries that represent bar heights. |
|  | When srcMode=1 *wave* is a 6-column numeric wave with columns defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Column&nbsp;0:</td><td>X center of the bar.</td></tr><tr><td>Column&nbsp;1:</td><td>Y center of the bar.</td></tr><tr><td>Column&nbsp;2:</td><td>Lower Z value.</td></tr><tr><td>Column&nbsp;3:</td><td>Upper Z value.</td></tr><tr><td>Column&nbsp;4:</td><td>Width of the bar in the X direction.</td></tr><tr><td>Column&nbsp;5:</td><td>Width of the bar in the Y direction.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {xBarWidth, *width* }</span> |  |
|  | When using basic mode (srcMode=0) this value determines the X direction width of all bars. *width* is a positive value. |
| <span class="table-cell-nowrap">property = {yBarWidth, *width* }</span> |  |
|  | When using basic mode (srcMode=0) this value determines the Y direction width of all bars. *width* is a positive value. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Image Objects {#modifygizmo-for-image-objects}

The syntax for modifying a Gizmo image object is:


```igor
ModifyGizmo modifyObject=objName, objectType=image, property={propertyName,data}
```

For more information also see [Gizmo Image Plots](/igorpro/graphing/3d-graphics.md#gizmo-image-plots).

### *Keywords* {#modifygizmo-for-image-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {alpha, *alpha* }</span> |  |
|  | Sets the alpha component for the whole image. |
|  | *alpha* is an alpha value the range [0,1]. For more information see [Transparency and Translucency](/igorpro/graphing/3d-graphics.md#transparency-and-translucency). |
| <span class="table-cell-nowrap">property = {alphaType, *type* }</span> |  |
|  | Specifies how alpha is determined for the image: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=1:</td><td>Automatically assigned alpha.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Single value alpha for the whole image as specified by the alpha property.</td></tr><tr><td>*type*&nbsp;=3:</td><td>Alpha provided by srcWave.</td></tr></tbody></table>
|  | For more information see [Transparency and Translucency](/igorpro/graphing/3d-graphics.md#transparency-and-translucency). |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {dataMatch, *mode*}</span> |  |
|  | Rotates the image to match the display of numeric data objects (e.g., surface, path, scatter objects): |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>The image is subject to user-specified rotation.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>The image is rotated to match data orientation (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {orientation, *type* }</span> |  |
|  | Sets the orientation of the image: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=1:</td><td>The image is displayed in the XY plane.</td></tr><tr><td>*type*&nbsp;=2:</td><td>The image is displayed in the YZ plane.</td></tr><tr><td>*type*&nbsp;=3:</td><td>The image is displayed in the ZX plane.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {rotation, *angle* , *axisX* , *axisY* , *axisZ* }</span> |  |
|  | Sets the rotation of the image. |
|  | *angle* is in degrees. |
|  | *axisX* , *axisY* , *axisZ* are normalized components of the vector about which the rotation is to be performed. |
| <span class="table-cell-nowrap">property = {rotationType, *type* }</span> |  |
|  | Enables or disables rotation of the image. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Rotation is disabled</td></tr><tr><td>*type*&nbsp;=1:</td><td>Rotation is enabled</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {scale, *scaleX* , *scaleY* , *scaleZ* }</span> |  |
|  | Sets the scaling of the image in the X, Y and Z directions. |
| <span class="table-cell-nowrap">property = {scaleType, *type* }</span> |  |
|  | Enables or disables scaling of the image. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Scaling is disabled</td></tr><tr><td>*type*&nbsp;=1:</td><td>Scaling is enabled</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> |  |
|  | Specifies the source wave for the image. The wave is a 3D unsigned-byte numeric wave and can have 3 layers for RGB or 4 layers for RGBA. |
| <span class="table-cell-nowrap">property = {translate, *tX* , *tY* , *tZ* }</span> |  |
|  | Sets the translation of the image in the X, Y and Z directions relative to the origin. The parameters are translation components in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {translationType, *type* }</span> |  |
|  | Enables or disables translation of the image. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Translation is disabled</td></tr><tr><td>*type*&nbsp;=1:</td><td>Translation is enabled</td></tr></tbody></table>


<!-- IndentedSubtopic -->
## ModifyGizmo for Axis Objects {#modifygizmo-for-axis-objects}

The syntax for modifying a Gizmo axis object is:


```igor
ModifyGizmo modifyObject=objName, objectType=axes, property={axisNumber,propertyName,data}
```

For more information also see [Gizmo Axis and Axis Cue Objects](/igorpro/graphing/3d-graphics.md#gizmo-axis-and-axis-cue-objects).

The property keyword for axis objects is different from other objects. It starts with an axis number that identifies the axis or grid to be modified. This axis number precedes the property name. For example:


```igor
ModifyGizmo ModifyObject=axes0, property={-1,axisColor,0,0,0,1}
```

In this example, the axis number -1 indicates that the axisColor property modification applies to all axes.

This table lists the axes and their corresponding axis numbers:


| Axis | Axis Number |
| --- | --- |
| Any custom axis | 0 |
| All axes | -1 |
| X0 | 0 |
| X1 | 9 |
| X2 | 10 |
| X3 | 11 |
| Y0 | 1 |
| Y1 | 6 |
| Y2 | 7 |
| Y3 | 8 |
| Z0 | 2 |
| Z1 | 3 |
| Z2 | 4 |
| Z3 | 5 |

For grid-related properties, the property keyword starts with a grid number:


| Grid Plane | Grid Number |
| --- | --- |
| All grids | -1 |
| XY Plane min Z | 0 |
| XY Plane max Z | 1 |
| XZ Plane min Y | 2 |
| XZ Plane max Y | 3 |
| YZ Plane min X | 4 |
| YZ Plane max X | 5 |

### *Keywords* {#modifygizmo-for-axis-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {*axisNumber*, *autoTickLength*, *mode*}</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*=0:</td><td>Tick mark lengths are determined by the userTickLength property described below.</td></tr><tr><td>*mode*=1:</td><td>Tick mark lengths are determined automatically (default).</td></tr></tbody></table>
| This property was added in Igor Pro 9.00. |  |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify the axis line color. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabel, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Hide axis label.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Show axis label.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelCenter, *center* }</span> |  |
|  | *center* is a single number designating the offset of the label in the direction of text progression. The label is drawn centered by default. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelDistance, *distance* }</span> |  |
|  | *distance* a single value that is added to the perpendicular distance between the axis and the label. *distance* is in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelFont, *fontNameStr* }</span> |  |
|  | *fontNameStr* is the name of a font, such as "Arial", to use to draw the axis label. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelFlip, *flip* }</span> |  |
|  | Determines if the Z0, Z1, Z2 or Z3 axes only are flipped. The flip is a 180 degree rotation about an axis pointing along the height of the first character. |
|  |<table class="nested-table"><tbody><tr><td>*flip*&nbsp;=0:</td><td>Don&#39;t flip the axis label.</td></tr><tr><td>*flip*&nbsp;=1:</td><td>Flip the axis label.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelRGB, *R*, *G*, *B* }</span> |  |
|  | R, G, B values specifying the axis label color. Values are in the range of [0,1] and alpha is assumed 1. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelRGBA, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify the axis label color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelScale, *scale* } (deprecated)</span> |  |
|  | *scale* is a scale factor for drawing the axis label. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelTilt, *tilt* }</span> |  |
|  | *tilt* is the tilt angle in degrees for rotating the label about the direction of text progression. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisLabelText, *text* }</span> |  |
|  | *text* is the axis label text, limited to 255 bytes. No label is drawn until this property is specified. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisMinValue, *value* }</span> |  |
|  | *value* specifies the scalar value for the start of a custom axis. If tick mark labels are drawn they use the range [axisMinValue,axisMaxValue]. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisMaxValue, *value* }</span> |  |
|  | *value* specifies the scalar value for the end of a custom axis. If tick mark labels are drawn they use the range [axisMinValue,axisMaxValue]. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisMode, *mode* } (deprecated)</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Data object axes.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Drawing non-data objects.</td></tr></tbody></table>
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisRange, *x0*, *y0*, *z0*, *x1*, *y1*, *z1* }</span> |  |
|  | Specifies the XYZ vertices of a custom axis in +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisScale, *scale* }</span> |  |
|  | Specifies the axis scaling, which is 1 by default. Any other value is equivalent to a uniform scaling operation using *scale* in all dimensions. This affects both the axis sizes and the locations of the tick marks and tick mark labels. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisScalingMode, *value* }</span> |  |
|  | Single scalar value that controls the maximum extent of the box frame. By default it is 1, but smaller values may be useful if you are just plotting drawing objects, not wave-based data objects. |
| <span class="table-cell-nowrap">property = {*axisNumber*, axisType, *constant* }</span> |  |
|  | *constant* identifies each axis and the role that it has in the axis object. This may affect other features such as grids or planes. |
|  | To make an axis invisible you, use the visible property. |
|  | Supported axis types are: |
|  |<table class="nested-table"><tbody><tr><td>Custom&nbsp;axis:</td><td>0x00100000</td></tr><tr><td>Triplet&nbsp;axes:</td><td>0x00200000</td></tr><tr><td>Box&nbsp;axes:</td><td>0x00400000</td></tr></tbody></table>
|  | For triplet and box axes the axisType is OR'ed with (1<< axisNumber). For example, to define a triplet axis object use: |
|  | <code class="igor">property={0,axisType,2097153}&#10;property={1,axisType,2097154}&#10;property={2,axisType,2097156}</code> |
|  | The axis constants for triplet axes are: |
|  |<table class="nested-table"><tbody><tr><td>X0:</td><td>2097153</td></tr><tr><td>Y0:</td><td>2097154</td></tr><tr><td>Z0:</td><td>2097156</td></tr></tbody></table>
|  | The axis constants for box axes are: |
|  |<table class="nested-table"><tbody><tr><td>X0:</td><td>4194305</td></tr><tr><td>X1:</td><td>4194816</td></tr><tr><td>X2:</td><td>4195328</td></tr><tr><td>X3:</td><td>4196352</td></tr><tr><td>Y0:</td><td>4194306</td></tr><tr><td>Y1:</td><td>4194368</td></tr><tr><td>Y2:</td><td>4194432</td></tr><tr><td>Y3:</td><td>4194560</td></tr><tr><td>Z0:</td><td>4194308</td></tr><tr><td>Z1:</td><td>4194312</td></tr><tr><td>Z2:</td><td>4194320</td></tr><tr><td>Z3:</td><td>4194336</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {*axisNumber*, canonicalTick, *value* }</span> |  |
|  | Specifies the axis value at which the canonical tick mark is drawn in manual tick marks mode. Starting from this value, tick marks are drawn in both directions at distances specified by canonicalIncrement. If *value* is outside the range of the axis then tick marks are not drawn. |
| <span class="table-cell-nowrap">property = {*axisNumber*, canonicalIncrement, *increment* }</span> |  |
|  | Specifies the tick mark increment in manual tick marks mode. If the increment is too small you could exceed the maximum number of tick marks. |
| <span class="table-cell-nowrap">property = {*axisNumber*, canonicalPower, *power* }</span> |  |
|  | Draws tick marks with a factored 10<sup>power</sup>. |
| <span class="table-cell-nowrap">property = {*axisNumber*, canonicalDigits, *digits* }</span> |  |
|  | *digits* is an integer specifying number of digits used after the decimal point when labeling manual tick marks. |
| <span class="table-cell-nowrap">property = {*axisNumber*, fontName, *fontNameStr* }</span> |  |
|  | *fontNameStr* is the name of a font, such as "Arial", to use to draw tick mark labels. |
| <span class="table-cell-nowrap">property = {*axisNumber*, fontScaleFactor, *scale* }</span> |  |
|  | Controls the font size of tick mark labels. This is equivalent to using the scale operation prior to drawing the text. |
| <span class="table-cell-nowrap">property = {*gridPlaneNumber*, gridLinesColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify the color of grid lines. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {*gridPlaneNumber*, gridLineWidth, *width* } (deprecated)</span> |  |
|  | Specifies the width of the line used to drawing all grid lines for the specified plane. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {*gridPlaneNumber*, gridPlaneColor, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify the color of painted grid plane. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {*gridPlaneNumber*, gridPrimaryCount, *count* }</span> |  |
|  | Specifies the number of grid lines in the primary direction if not attached to tick marks. |
| <span class="table-cell-nowrap">property = {*gridPlaneNumber*, gridSecondaryCount, *count* }</span> |  |
|  | Specifies the number of grid lines in the secondary direction if not attached to tick marks. |
| <span class="table-cell-nowrap">property = {*gridPlaneNumber*, gridType, *type* }</span> |  |
|  | *type* is a bitwise setting. *type* =0 gives no grid. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Painted plane</td></tr><tr><td>Bit&nbsp;1:</td><td>Primary grid lines</td></tr><tr><td>Bit&nbsp;2:</td><td>Primary grids matching tick marks</td></tr><tr><td>Bit&nbsp;3:</td><td>Secondary grids</td></tr><tr><td>Bit&nbsp;4:</td><td>Secondary grids matching tick marks</td></tr><tr><td>Bit&nbsp;5:</td><td>Allow drawing lines</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">property = {*axisNumber*, highTrip, *trip* }</span> |  |
|  | *trip* is the axis value above which tick mark labels are represented in engineering notation. |
| <span class="table-cell-nowrap">property = {*axisNumber*, labelBillboarding, *mode* }</span> |  |
|  | Enables or disables the billboarding of an axis label. Billboarding is an attempt to draw the label facing the viewer. It is on by default. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Disables billboarding</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Enables billboarding</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {*axisNumber*, labelColor, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies tick mark label color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {*axisNumber*, labelOffset, *x*, *y*, *z* }</span> |  |
|  | Offsets tick mark labels. *x*, *y*, and *z* are in +/-1 display volume coordinates. The effect is the same as adding a translate operation before drawing each tick mark label. |
| <span class="table-cell-nowrap">property = {*axisNumber*, labelRotationAxis, *axisX* , *axisY* , *axisZ* } (deprecated)</span> |  |
|  | *axisX* , *axisY* , *axisZ* are normalized components of the vector about which tick mark label rotation is to be performed. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {*axisNumber*, labelRotationAngle, *angle* } (deprecated)</span> |  |
|  | *angle* is the angle in degrees of tick mark label rotation. Positive angles give counterclockwise rotation. You must define the rotation axis before using this property. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {*axisNumber*, lineWidth, *width* } (deprecated)</span> |  |
|  | *width* is the axis line width in points. |
|  | This property is deprecated. |
| <span class="table-cell-nowrap">property = {*axisNumber*, lowTrip, *trip* }</span> |  |
|  | *trip* is the axis value below which tick mark labels are represented in engineering notation. |
| <span class="table-cell-nowrap">property = {*axisNumber*, numTicks, *num* }</span> |  |
|  | *num* is the requested number of tick marks in auto mode. The requested value may not be attained if the resulting intervals do not fall on "nice" limits. |
| <span class="table-cell-nowrap">property = {*axisNumber*, ticks, *mode* }</span> |  |
|  | Controls the display of tick marks and tick mark labels. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Disable tick marks</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Enable tick marks</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Enable tick mark labels</td></tr><tr><td>*mode*&nbsp;=3:</td><td>Enable both tick marks and tick mark labels</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {*axisNumber*, tickEnable, *startValue*, *endValue* }</span> |  |
|  | Sets the axis range within which tick mark labels are drawn. Tick marks outside the specified range are not drawn. |
| <span class="table-cell-nowrap">property = {*axisNumber*, tickScaling, *scale* }</span> |  |
|  | Specifies the axis scaling for tick mark length, which is a function of the maximum dimension of the plot. Default tickmark length is 0.02. |
| <span class="table-cell-nowrap">property = {*axisNumber*, tickLabelWave, *wave* }</span> |  |
|  | *wave* is a text wave containing one column of entries that provide tick mark labels that are drawn at positions specified by *tickLevelWave*. Avoid long strings so that labels do not overlap. |
| <span class="table-cell-nowrap">property = {*axisNumber*, tickLevelWave, *wave* }</span> |  |
|  | *wave* is a numeric wave containing values at which you want to draw tick marks. The number of entries in this wave must match the number of entries in the *tickLabelWave*. Gizmo draws the tick marks for levels between the minimum and maximum values of the data along the particular axis. You must also set *tickmarkType*=3, described below. |
| <span class="table-cell-nowrap">property = {*axisNumber*, tickMarkType, *type* }</span> |  |
|  | Specifies how tick mark positions are determined. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Default. Automatic tick marks.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Manual tick marks using canonical tick mark values.</td></tr><tr><td>*type*&nbsp;=3:</td><td>Manual tick marks specified by *tickLevelWave* and *tickLabelWave*.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {*axisNumber*, userTickLength, *dx*, *dy*, *dz*}</span> |  |
|  | Specifies the 3D size of the tick marks in scaled units (for +-1 box). These values are used only when the autoTickLength is set to 0. |
|  | This property was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">property = {*axisNumber*, visible, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Hides the axis.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Shows the axis.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {-1, volumeGrids, *mode* }</span> |  |
|  | Controls the drawing of volume grids. Volume grids are equally-spaced lines through the volume parallel to the X, Y or Z axis. |
|  | *mode* is a bitwise setting.  *mode* =0 gives no grid. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Draw volume grid parallel to the X axis.</td></tr><tr><td>Bit&nbsp;1:</td><td>Draw volume grid parallel to the Y axis.</td></tr><tr><td>Bit&nbsp;2:</td><td>Draw volume grid parallel to the Z axis.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | Unlike exterior grid lines (see gridType), volume grids are hard wired to the locations of tick marks on the corresponding axes. |
|  | Use -1 for the axis number parameter. |
| <span class="table-cell-nowrap">property = {*axisNumber*, volumeGridsRGBA, *R*, *G*, *B*, *A* }</span> |  |
|  | Controls the color of volume grids. |
|  | *R*, *G*, *B*, and *A* specify the grid line color. Values are in the range of [0,1]. |
|  | *axisNumber* is a bitwise setting. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Apply color to the X axis.</td></tr><tr><td>Bit&nbsp;1:</td><td>Apply color to the Y axis.</td></tr><tr><td>Bit&nbsp;2:</td><td>Apply color to the Z axis.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">property = {*axisNumber*, volumeGridsLineWidth, *width* } (deprecated)</span> |  |
|  | *width* is the volume grid line width in points. |
|  | *axisNumber* is a bitwise setting. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Apply width to the X axis.</td></tr><tr><td>Bit&nbsp;1:</td><td>Apply width to the Y axis.</td></tr><tr><td>Bit&nbsp;2:</td><td>Apply width to the Z axis.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | This property is deprecated. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Free Axis Cue Objects {#modifygizmo-for-free-axis-cue-objects}

The syntax for modifying a Gizmo free axis cue object is:


```igor
ModifyGizmo modifyObject=objName, objectType=freeAxisCue, property={propertyName,data}
```

For more information also see [Gizmo Axis and Axis Cue Objects](/igorpro/graphing/3d-graphics.md#gizmo-axis-and-axis-cue-objects).

### *Keywords* {#modifygizmo-for-free-axis-cue-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of grid line coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Default. The axes are drawn using default colors.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {labels, *val* }</span> | *val* is a binary field flag that controls the display of the X, Y and Z labels on the corresponding axes. |
|  |<table class="nested-table"><tbody><tr><td>***val***</td><td>**labels**</td></tr><tr><td>0</td><td>none</td></tr><tr><td>1</td><td>X-axis label</td></tr><tr><td>2</td><td>Y-axis label</td></tr><tr><td>4</td><td>Z-axis label</td></tr><tr><td>7</td><td>X, Y and Z labels (default)</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {offset, *x*, *y*, *z* }</span> |  |
|  | Offsets the origin of the free axis cue relative to the origin of the display volume. *x*, *y*, and *z*  are in +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">property = {scale, *val* }</span> |  |
|  | Specifies a scaling factor for isotropic scaling. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Line Objects {#modifygizmo-for-line-objects}

The syntax for modifying a Gizmo line object is:


```igor
ModifyGizmo modifyObject=objName, objectType=line, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Line Objects]](/igorpro/graphing/3d-graphics.md#line-objects).

### *Keywords* {#modifygizmo-for-line-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {arrowMode, *mode* }</span> |  |
|  | *mode* is a bitwise setting that controls properties of the line. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Arrowhead at the start point.</td></tr><tr><td>Bit&nbsp;1:</td><td>Arrowhead at the end point.</td></tr><tr><td>Bit&nbsp;2:</td><td>Arrowhead at the center of the segment.</td></tr><tr><td>Bit&nbsp;3:</td><td>Reversed arrowhead at the center of the segment.</td></tr><tr><td>Bit&nbsp;4:</td><td>Line drawn as a cylinder.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of line coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use *colorValue* to specify the color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Full color specified by two sets of RGBA values using the *colorValue* keyword.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {colorValue, *vertex*, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the line color. |
|  | *vertex* is 0 for the start of the line, 1 for the end of the line. |
|  | If *colorType*=1 then setting vertex 0 sets the color for the entire object. If *colorType*=2 then you can set each vertex independently. |
|  | *R*, *G*, *B*, and *A* specify the vertex color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {cylinderEndRadius, *diameter* }</span> |  |
|  | Specifies the ending *diameter* when drawing a line as a cylinder (arrowMode=16). *diameter* is in +/-1 display volume units. The default is 0.03. |
| <span class="table-cell-nowrap">property = {cylinderStartRadius, *diameter* }</span> |  |
|  | Specifies the starting *diameter* when drawing a line as a cylinder (arrowMode=16). *diameter* is in +/-1 display volume units. The default is 0.03. |
| <span class="table-cell-nowrap">property = {endArrowBase, *diameter* }</span> |  |
|  | Specifies the diameter of the base of an end arrow expressed in +/-1 display volume units. The default is 0.04. |
| <span class="table-cell-nowrap">property = {endArrowHeight, *height* }</span> |  |
|  | Specifies the height of an end arrow expressed in +/-1 display volume units. The default is 0.06. |
|  | The arrow cone is set so that the apex position is at the end of the line object and the base is drawn at arrow-height units towards the start of the line. |
| <span class="table-cell-nowrap">property = {midArrowBase, *diameter* }</span> |  |
|  | Specifies the diameter of the base of a midpoint arrow expressed in +/-1 display volume units. The default is 0.04. |
| <span class="table-cell-nowrap">property = {midArrowHeight, *height* }</span> |  |
|  | Specifies the height of a midpoint arrow expressed in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {startArrowBase, *diameter* }</span> |  |
|  | Specifies the diameter of the base of a start arrow expressed in +/-1 display volume units. The default is 0.04. |
| <span class="table-cell-nowrap">property = {startArrowHeight, *height* }</span> |  |
|  | Specifies the height of a start arrow expressed in +/-1 display volume units from the apex (at the start point of the line) in the direction of the end point. |
| <span class="table-cell-nowrap">property = {vertex, *xA*, *yA*, *zA*, *xB*, *yB*, *zB* }</span> |  |
|  | Specifies the start and end vertices of the line expressed in +/-1 XYZ display volume coordinates. |



<!-- IndentedSubtopic -->
## ModifyGizmo for Triangle Objects {#modifygizmo-for-triangle-objects}

The syntax for modifying a Gizmo triangle object is:


```igor
ModifyGizmo modifyObject=objName, objectType=triangle, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Triangle Objects]](/igorpro/graphing/3d-graphics.md#triangle-objects).

### *Keywords* {#modifygizmo-for-triangle-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the triangle object is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of triangle coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use colorValue to specify the color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Full color specified by three sets of RGBA values using the colorValue keyword.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {colorValue, *vertex*, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the triangle color. |
|  | *vertex* is 0, 1 or 2. |
|  | If *colorType*=1 then setting vertex 0 sets the color for the entire object. If *colorType*=2 then you can set each vertex independently. |
|  | *R*, *G*, *B*, and *A* specify the vertex color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {vertex, *xA*, *yA*, *zA*, *xB*, *yB*, *zB*, *xC*, *yC*, *zC* }</span> |  |
|  | Specifies the three vertices of the triangle expressed in +/-1 XYZ display volume coordinates. |



<!-- IndentedSubtopic -->
## ModifyGizmo for Quad Objects {#modifygizmo-for-quad-objects}

The syntax for modifying a Gizmo quad object is:


```igor
ModifyGizmo modifyObject=objName, objectType=quad, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Quad Objects]](/igorpro/graphing/3d-graphics.md#quad-objects).

### *Keywords* {#modifygizmo-for-quad-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the quad object is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of quad coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use *colorValue* to specify the color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Full color specified by four sets of RGBA values using the *colorValue* keyword.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {colorValue, *vertex*, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the quad color. |
|  | *vertex* is 0, 1, 2 or 3. |
|  | If *colorType*=1 then setting vertex 0 sets the color for the entire object. If *colorType*=2 then you can set each vertex independently. |
|  | *R*, *G*, *B*, and *A* specify the vertex color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {vertex, *xA*, *yA*, *zA*, *xB*, *yB*, *zB*, *xC*, *yC*, *zC*, *xD*, *yD*, *zD* }</span> |  |
|  | Specifies the four vertices of the quad expressed in +/-1 XYZ display volume coordinates. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Box Objects {#modifygizmo-for-box-objects}

The syntax for modifying a Gizmo box object is:


```igor
ModifyGizmo modifyObject=objName, objectType=box, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Box Objects]](/igorpro/graphing/3d-graphics.md#box-objects).

### *Keywords* {#modifygizmo-for-box-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the box object is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of box coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use *colorValue* to specify the color.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Full color specified by 24 sets of RGBA values using the *colorValue* keyword.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {vertex, *xA*, *yA*, *zA*, *...* *xX*, *yX*, *zX* }</span> |  |
|  | Specifies the 24 vertices of the box expressed in +/-1 XYZ display volume coordinates. |
| <span class="table-cell-nowrap">property = {colorValue, *vertex*, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the box color. |
|  | *vertex* is a number between 0 and 23. |
|  | If *colorType*=1 then setting vertex 0 sets the color for the entire object. If *colorType*=2 then you can set each vertex independently. |
|  | *R*, *G*, *B*, and *A* specify the vertex color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {faceColor, *faceNum*, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color of a specific face. |
|  | *faceNum* is a number between 0 and 5. |
|  | Note that *colorType* must be set to 2 in order to display the box in more than one color. |
|  | *R*, *G*, *B*, and *A* specify the vertex color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {dimensions, *length*, *width*, *height* }</span> |  |
|  | Specifies the box dimensions in +/-1 XYZ display volume coordinates. |



<!-- IndentedSubtopic -->
## ModifyGizmo for Sphere Objects {#modifygizmo-for-sphere-objects}

The syntax for modifying a Gizmo sphere object is:


```igor
ModifyGizmo modifyObject=objName, objectType=sphere, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Sphere Objects]](/igorpro/graphing/3d-graphics.md#sphere-objects).

### *Keywords* {#modifygizmo-for-sphere-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {color, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify the sphere color if colorType=1. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of sphere coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use color to specify the color.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {drawStyle, *style* }</span> |  |
|  | Specifies the style of sphere drawing: |
|  |<table class="nested-table"><tbody><tr><td>*style*&nbsp;=100010:</td><td>Draw a point at every vertex.</td></tr><tr><td>*style*&nbsp;=100011:</td><td>Draw lines between vertices.</td></tr><tr><td>*style*&nbsp;=100012:</td><td>Fill the polygons (default).</td></tr><tr><td>*style*&nbsp;=100013:</td><td>Draw silhouette (deprecated).</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {normals, *mode* }</span> |  |
|  | Controls the calculation of normals for the object. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=100000:</td><td>Compute smooth normals (default).</td></tr><tr><td>*mode*&nbsp;=100001:</td><td>Compute flat normals.</td></tr><tr><td>*mode*&nbsp;=100002:</td><td>Don&#39;t compute normals.</td></tr></tbody></table>
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {orientation, *type* }</span> |  |
|  | Sets the orientation of the normals: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=100020:</td><td>Normals point outside (default).</td></tr><tr><td>*type*&nbsp;=100021:</td><td>Normals point inside.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {radius, *val* }</span> |  |
|  | *radius* is a positive number specifying the sphere radius. |
| <span class="table-cell-nowrap">property = {slices, *numSlices* }</span> |  |
|  | *numSlices* is a positive number specifying the number of longitudinal divisions. A higher number of slices and stacks produces a smoother sphere. |
| <span class="table-cell-nowrap">property = {stacks, *numStacks* }</span> |  |
|  | *numStacks* is a positive number specifying the number of latitudinal divisions. A higher number of slices and stacks produces a smoother sphere. |
| <span class="table-cell-nowrap">property = {useGlobalAttributes, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Disable global attributes.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Enable global attributes (default).</td></tr></tbody></table>
|  | A sphere object has internal `drawStyle`, `normals`, and `orientation` attributes. To use these internal attributes you must disable global attributes. |



<!-- IndentedSubtopic -->
## ModifyGizmo for Cylinder Objects {#modifygizmo-for-cylinder-objects}

The syntax for modifying a Gizmo cylinder object is:


```igor
ModifyGizmo modifyObject=objName, objectType=cylinder, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Cylinder Objects]](/igorpro/graphing/3d-graphics.md#cylinder-objects).

### *Keywords* {#modifygizmo-for-cylinder-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {baseRadius, *radius* }</span> |  |
|  | *radius* is a positive number specifying the radius of the cylinder's base in +/-1 display volume units. You can create a cone by specifying different values for baseRadius and topRadius. |
| <span class="table-cell-nowrap">property = {color, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify the cylinder color if colorType=1. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of cylinder coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use color to specify the color.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {drawStyle, *style* }</span> |  |
|  | Specifies the style of cylinder drawing: |
|  |<table class="nested-table"><tbody><tr><td>*style*&nbsp;=100010:</td><td>Draw a point at every vertex.</td></tr><tr><td>*style*&nbsp;=100011:</td><td>Draw lines between vertices.</td></tr><tr><td>*style*&nbsp;=100012:</td><td>Fill the polygons (default).</td></tr><tr><td>*style*&nbsp;=100013:</td><td>Draw silhouette (deprecated).</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {colorType, *height* }</span> |  |
|  | Specifies the height of the cylinder in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {normals, *mode* }</span> |  |
|  | Controls the calculation of normals for the object. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=100000:</td><td>Compute smooth normals (default).</td></tr><tr><td>*mode*&nbsp;=100001:</td><td>Compute flat normals.</td></tr><tr><td>*mode*&nbsp;=100002:</td><td>Don&#39;t compute normals.</td></tr></tbody></table>
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {orientation, *type* }</span> |  |
|  | Sets the orientation of the normals: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=100020:</td><td>Normals point outside (default).</td></tr><tr><td>*type*&nbsp;=100021:</td><td>Normals point inside.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {slices, *numSlices* }</span> |  |
|  | *numSlices* is a positive number specifying the number of divisions around the cylinder. A higher number of slices and stacks produces a smoother cylinder. |
| <span class="table-cell-nowrap">property = {stacks, *numStacks* }</span> |  |
|  | *numStacks* is a positive number specifying the number of divisions along the cylinder's height. A higher number of slices and stacks produces a smoother cylinder. |
| <span class="table-cell-nowrap">property = {topRadius, *radius* }</span> |  |
|  | *radius* is a positive number specifying the radius of the cylinder's top in +/-1 display volume units. You can create a cone by specifying different values for baseRadius and topRadius. |
| <span class="table-cell-nowrap">property = {useGlobalAttributes, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Disable global attributes.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Enable global attributes (default).</td></tr></tbody></table>
|  | A cylinder object has internal `drawStyle`, `normals`, and `orientation` attributes. To use these internal attributes you must disable global attributes. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Disk Objects {#modifygizmo-for-disk-objects}

The syntax for modifying a Gizmo disk object is:


```igor
ModifyGizmo modifyObject=objName, objectType=disk, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Disk Objects]](/igorpro/graphing/3d-graphics.md#disk-objects).

### *Keywords* {#modifygizmo-for-disk-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {color, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* specify the disk color if colorType=1. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of disk coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. Use color to specify the color.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {drawStyle, *style* }</span> |  |
|  | Specifies the style of disk drawing: |
|  |<table class="nested-table"><tbody><tr><td>*style*&nbsp;=100010:</td><td>Draw a point at every vertex.</td></tr><tr><td>*style*&nbsp;=100011:</td><td>Draw lines between vertices.</td></tr><tr><td>*style*&nbsp;=100012:</td><td>Fill the polygons (default).</td></tr><tr><td>*style*&nbsp;=100013:</td><td>Draw silhouette (deprecated).</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {innerRadius, *radius* }</span> |  |
|  | *radius* is a positive number, less than outerRadius, specifying the radius of central hole in disk in +/-1 display volume units. Use zero for a disk with no hole. |
| <span class="table-cell-nowrap">property = {normals, *mode* }</span> |  |
|  | Controls the calculation of normals for the object. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=100000:</td><td>Compute smooth normals (default).</td></tr><tr><td>*mode*&nbsp;=100001:</td><td>Compute flat normals.</td></tr><tr><td>*mode*&nbsp;=100002:</td><td>Don&#39;t compute normals.</td></tr></tbody></table>
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {orientation, *type* }</span> |  |
|  | Sets the orientation of the normals: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=100020:</td><td>Normals point outside (default).</td></tr><tr><td>*type*&nbsp;=100021:</td><td>Normals point inside.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {outerRadius, *radius* }</span> |  |
|  | *radius* is a positive number, greater than innerRadius, specifying the radius of disk rim in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {slices, *numSlices* }</span> |  |
|  | *numSlices* is a positive number specifying the number of longitudinal divisions around the disk. A higher number of slices produces a smoother disk. |
| <span class="table-cell-nowrap">property = {startAngle, *angle* }</span> |  |
|  | *angle* is the starting angle of the disk in the range 0 to 360. It is relative to the Y axis specified in degrees clockwise. |
| <span class="table-cell-nowrap">property = {sweepAngle, *angle* }</span> |  |
|  | *angle* is the angular extent of the disk in the range 0 to 360. It is specified in degrees clockwise. |
| <span class="table-cell-nowrap">property = {rings, *numRings* }</span> |  |
|  | *numRings* is a positive number specifying the number of latitudinal divisions in the disk. A higher number of rings produces a smoother disk. |
| <span class="table-cell-nowrap">property = {useGlobalAttributes, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Disable global attributes.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Enable global attributes (default).</td></tr></tbody></table>
|  | A disk object has internal `drawStyle`, `normals`, and `orientation` attributes. To use these internal attributes you must disable global attributes. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Tetrahedron Objects {#modifygizmo-for-tetrahedron-objects}

The syntax for modifying a Gizmo tetrahedron object is:


```igor
ModifyGizmo modifyObject=objName, objectType=tetrahedron, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Tetrahedron Objects]](/igorpro/graphing/3d-graphics.md#tetrahedron-objects).

### *Keywords* {#modifygizmo-for-tetrahedron-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the tetrahedron object is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of tetrahedron line coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color specified by wireRGBA keyword.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {RGBA0, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color for vertex 0. |
|  | *R*, *G*, *B*, and *A* specify the vertex color. Values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {RGBA1, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color for vertex 1. |
|  | R, G, B, A values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {RGBA2, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color for vertex 2. |
|  | R, G, B, A values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {RGBA3, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color for vertex 3. |
|  | R, G, B, A values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {sphereRGBA, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color for spheres drawn at the vertices. |
|  | R, G, B, A values are in the range of [0,1]. |
| <span class="table-cell-nowrap">property = {style, *mode* }</span> |  |
|  | Controls the drawing style for the tetrahedron. |
|  | *mode* is a bitwise setting. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Draw wires (lines) between vertices.</td></tr><tr><td>Bit&nbsp;1:</td><td>Fill the triangle faces.</td></tr><tr><td>Bit&nbsp;2:</td><td>Draw a sphere at each vertex.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">property = {vertex0, *x*, *y*, *z* }</span> |  |
|  | Specifies the X, Y, Z coordinates of vertex 0 using +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">property = {vertex1, *x*, *y*, *z* }</span> |  |
|  | Specifies the X, Y, Z coordinates of vertex 1 using +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">property = {vertex2, *x*, *y*, *z* }</span> |  |
|  | Specifies the X, Y, Z coordinates of vertex 2 using +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">property = {vertex3, *x*, *y*, *z* }</span> |  |
|  | Specifies the X, Y, Z coordinates of vertex 3 using +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">property = {wireRGBA, *R*, *G*, *B*, *A* }</span> |  |
|  | Specifies the color for wires (lines) drawn between the vertices. |
|  | R, G, B, A values are in the range of [0,1]. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Pie Wedge Objects {#modifygizmo-for-pie-wedge-objects}

The syntax for modifying a Gizmo pie wedge object is:


```igor
ModifyGizmo modifyObject=objName, objectType=piewedge, property={propertyName,data}
```

For more information also see [Gizmo Drawing Objects[Pie Wedge Objects]](/igorpro/graphing/3d-graphics.md#pie-wedge-objects).

### *Keywords* {#modifygizmo-for-pie-wedge-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the pie wedge object is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {colorType, *type* }</span> |  |
|  | Specifies the type of pie wedge coloring: |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>No color. Gizmo uses the last color selected in the drawing environment.</td></tr><tr><td>*type*&nbsp;=1:</td><td>Constant color. The top, bottom and sides are drawing using the color set by *topRGBA*.</td></tr><tr><td>*type*&nbsp;=2:</td><td>Separate colors. The top and bottom are drawn using the color set by *topRGBA*. The sides are drawn using the color set by *sideRGBA*.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {endAngle, *angle* }</span> |  |
|  | *angle* is the angle at which the wedge ends. It is relative to the positive X axis specified in degrees counter-clockwise. |
| <span class="table-cell-nowrap">property = {rMax, *radius* }</span> |  |
|  | *radius* is the maximum radius for the wedge. The radius is measured in +/-1 display volume units. A full wedge has a maximum radius of 1. |
| <span class="table-cell-nowrap">property = {rMin, *radius* }</span> |  |
|  | *radius* is the minimum radius for the wedge. The radius is measured in +/-1 display volume units. A full wedge has a minimum radius of 0. |
| <span class="table-cell-nowrap">property = {radialOffset, *offset* }</span> |  |
|  | *offset* is a single offset in +/-1 display volume units along the direction of the radius pointing from the origin and bisecting the wedge angle. The radial offset uses the X and Y components of translate (see below) so the two properties are not independent. |
| <span class="table-cell-nowrap">property = {sideRGBA, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of the sides of the wedge. |
| <span class="table-cell-nowrap">property = {slices, *numSlices* }</span> |  |
|  | *numSlices* is the number of polygonal wedges between startAngle and endAngle. More slices gives a smoother pie wedge. |
| <span class="table-cell-nowrap">property = {startAngle, *angle* }</span> |  |
|  | *angle* is the angle at which the wedge starts. It is relative to the positive X axis specified in degrees counter-clockwise. |
| <span class="table-cell-nowrap">property = {topRGBA, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of the top and bottom of the wedge. |
| <span class="table-cell-nowrap">property = {translate, *tX* , *tY* , *tZ* }</span> |  |
|  | Sets the translation of the pie wedge in the X, Y and Z directions relative to the origin. The parameters are translation components in +/-1 display volume units. See also radialOffset above. |
| <span class="table-cell-nowrap">property = {zMax, *max* }</span> |  |
|  | *max* is the the Z value of the top of the wedge measured in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {zMin, *min* }</span> |  |
|  | *min* is the the Z value of the bottom of the wedge measured in +/-1 display volume units. |


<!-- IndentedSubtopic -->
## ModifyGizmo for Light Objects {#modifygizmo-for-light-objects}

The syntax for modifying a Gizmo light object is:


```igor
ModifyGizmo modifyObject=objName, objectType=light, property={propertyName,data}
```

For more information also see [Gizmo Lights](/igorpro/graphing/3d-graphics.md#gizmo-lights).

### *Keywords* {#modifygizmo-for-light-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {ambient, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of ambient, direction-independent light components. When adding a single light it is helpful to specify minimum ambient components of {0.2,0.2,0.2,1}. |
| <span class="table-cell-nowrap">property = {cutoff, *angle* }</span> |  |
|  | *angle* is the half-angle of the cone of the spotlight in degrees from 0 to 180. This applies to positional light sources only. |
| <span class="table-cell-nowrap">property = {constAttenuation, *attenuation* }</span> |  |
|  | *attenuation* is the light attenuation factor defined as |
|  | 1/(*Kc* +*kl* \* *d* +*Kq* \* *d<sup>2</sup>*) |
|  | where *Kc* is the constant attenuation, *Kl* is the linear attenuation, *Kq* is the quadratic attenuation and *d* is the distance. This applies to positional lights only. |
| <span class="table-cell-nowrap">property = {diffuse, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of diffuse components of a light. Diffuse effects depend on the light direction and on the material properties of the surface. |
| <span class="table-cell-nowrap">property = {direction, *x*, *y*, *z* }</span> |  |
|  | Specifies the X, Y, Z components of a vector specifying the light direction. |
| <span class="table-cell-nowrap">property = {exponent, *exp* }</span> |  |
|  | *exp* is the value of light intensity attenuation. Intensity falloff is given by the cosine of the angle between the direction of the light and the illuminated vertex. The exponent is the power of the cosine in the attenuation factor. |
| <span class="table-cell-nowrap">property = {linearAttenuation, *attenuation* }</span> |  |
|  | See *constAttenuation*. This applies to positional lights only. |
| <span class="table-cell-nowrap">property = {position, *x*, *y*, *z*, *w* }</span> |  |
|  | Specifies the position of the light source using homogeneous coordinates. The light source is directional when W=0 and the position is unimportant. See [Gizmo Positional Lights](/igorpro/graphing/3d-graphics.md#gizmo-positional-lights) for details. |
| <span class="table-cell-nowrap">property = {quadraticAttenuation, *attenuation* }</span> |  |
|  | See *constAttenuation*. This applies to positional lights only. |
| <span class="table-cell-nowrap">property = {specular, *R*, *G*, *B*, *A* }</span> |  |
|  | *R*, *G*, *B*, and *A* in the range [0,1] specify the color of specular components of a light. Specular effects depend both on the direction of the light and on material properties. It is usually difficult to adjust specular components. |



<!-- IndentedSubtopic -->
## ModifyGizmo for Texture Objects {#modifygizmo-for-texture-objects}

The syntax for modifying a Gizmo texture object is:


```igor
ModifyGizmo modifyObject=objName, objectType=texture, property={propertyName,data}
```

For more information also see [Advanced Gizmo Techniques[Texture Objects]](/igorpro/graphing/3d-graphics.md#texture-objects).

### *Keywords* {#modifygizmo-for-texture-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {dim, *mode* }</span> |  |
|  | Specifies the dimensionality of the texture wave. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x0DE1:</td><td>2D texture (default)</td></tr><tr><td>*mode*&nbsp;=0x0DE0:</td><td>1D texture</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {dataFormat, *mode* }</span> |  |
|  | Specifies the the format of the pixel data. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x1903:</td><td>GL_RED</td></tr><tr><td>*mode*&nbsp;=0x1907:</td><td>GL_RGB</td></tr><tr><td>*mode*&nbsp;=0x1908:</td><td>GL_RGBA</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {dataType, *type* }</span> |  |
|  | Specifies the data type of the texture wave. |
|  |<table class="nested-table"><tbody><tr><td>*type*&nbsp;=0:</td><td>Signed byte</td></tr><tr><td>*type*&nbsp;=1:</td><td>Unsigned byte</td></tr><tr><td>*type*&nbsp;=2:</td><td>Signed 16-bit word</td></tr><tr><td>*type*&nbsp;=3:</td><td>Unsigned 16-bit word</td></tr><tr><td>*type*&nbsp;=4:</td><td>Signed 32-bit word</td></tr><tr><td>*type*&nbsp;=5:</td><td>Unsigned 32-bit word</td></tr><tr><td>*type*&nbsp;=6:</td><td>Single-precision floating point</td></tr><tr><td>*type*&nbsp;=10:</td><td>Double-precision floating point</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {direction, *mode* }</span> |  |
|  | Specifies the direction for a 1D texture. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2000:</td><td>GL_S</td></tr><tr><td>*mode*&nbsp;=0x0DE0:</td><td>GL_T</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {envMode, *mode* }</span> |  |
|  | Specifies how the texture parameters are interpreted. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2100:</td><td>GL_MODULATE</td></tr><tr><td>*mode*&nbsp;=0x2101:</td><td>GL_DECAL</td></tr><tr><td>*mode*&nbsp;=0x0BE2:</td><td>GL_BLEND</td></tr><tr><td>*mode*&nbsp;=0x1E01:</td><td>GL_REPLACE</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {height, *value* }</span> |  |
|  | Specifies the height of the source image in pixels. For best performance use a power of 2. |
| <span class="table-cell-nowrap">property = {magMode, *mode* }</span> |  |
|  | Sets the texture magnifying filter. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2601:</td><td>GL_LINEAR (default)</td></tr><tr><td>*mode*&nbsp;=0x2600:</td><td>GL_NEAREST</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {minMode, *mode* }</span> |  |
|  | Sets the texture minifying filter. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2601:</td><td>GL_LINEAR (default)</td></tr><tr><td>*mode*&nbsp;=0x2600:</td><td>GL_NEAREST</td></tr><tr><td>*mode*&nbsp;=0x2700:</td><td>GL_NEAREST_MIPMAP_NEAREST</td></tr><tr><td>*mode*&nbsp;=0x2701:</td><td>GL_LINEAR_MIPMAP_NEAREST</td></tr><tr><td>*mode*&nbsp;=0x2702:</td><td>GL_NEAREST_MIPMAP_LINEAR</td></tr><tr><td>*mode*&nbsp;=0x2703:</td><td>GL_LINEAR_MIPMAP_LINEAR</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {priority, *value* }</span> |  |
|  | *value* is a scalar in the range [0,1] that lets you assign priority to a texture object. 0 indicates lowest priority. Textures with priority 1 are most likely to be resident in memory. |
| <span class="table-cell-nowrap">property = {sCoordinates, *p1*, *p2*, *p3*, *p4* }</span> |  |
|  | *p1*, *p2*, *p3*, and *p4* control the generation of texture coordinates for the S-direction. For example, if the texture generation function is GL_OBJECT_LINEAR the computed S coordinate is: |
|  | <code class="igor">s = p1\*x + p2\*y + p3\*z + p4\*w</code> |
| <span class="table-cell-nowrap">property = {sGenMode, *mode* }</span> |  |
|  | Sets the texture coordinates generation mode for the S-direction. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2400:</td><td>GL_EYE_LINEAR</td></tr><tr><td>*mode*&nbsp;=0x2401:</td><td>GL_OBJECT_LINEAR</td></tr><tr><td>*mode*&nbsp;=0x2402:</td><td>GL_SPHERE_MAP</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> |  |
|  | Specifies the wave containing the texture information. |
|  | IGOR stores images in 3-layer RGB or 4-layer RGBA waves. These are not directly compatible with OpenGL texture formats. Use [ImageTransform](/igorpro/commands/imagetransform.md) with the keyword imageToTexture to convert IGOR image waves to texture waves. |
| <span class="table-cell-nowrap">property = {tCoordinates, *p1*, *p2*, *p3*, *p4* }</span> |  |
|  | *p1*, *p2*, *p3*, and *p4* control the generation of texture coordinates for the T-direction. For example, if the texture generation function is GL_OBJECT_LINEAR the computed S coordinate is: |
|  | <code class="igor">t=p1*x + p2\*y + p3\*z + p4\*w</code> |
| <span class="table-cell-nowrap">property = {tGenMode, *mode* }</span> |  |
|  | Sets the texture coordinates generation mode for the T-direction. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2400:</td><td>GL_EYE_LINEAR</td></tr><tr><td>*mode*&nbsp;=0x2401:</td><td>GL_OBJECT_LINEAR</td></tr><tr><td>*mode*&nbsp;=0x2402:</td><td>GL_SPHERE_MAP</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {width, *value* }</span> |  |
|  | Specifies the width of the source image in pixels. For best performance use a power of 2. |
| <span class="table-cell-nowrap">property = {wrapSMode, *mode* }</span> |  |
|  | Determines how the texture is applied in the S-direction. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2901:</td><td>GL_REPEAT</td></tr><tr><td>*mode*&nbsp;=0x2900:</td><td>GL_CLAMP</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {wrapTMode, *mode* }</span> |  |
|  | Determines how the texture is applied in the T-direction. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0x2901:</td><td>GL_REPEAT</td></tr><tr><td>*mode*&nbsp;=0x2900:</td><td>GL_CLAMP</td></tr></tbody></table>


<!-- IndentedSubtopic -->
## ModifyGizmo for Matrix4x4 Objects {#modifygizmo-for-matrix4x4-objects}

The syntax for modifying a Gizmo 4x4 matrix object is:


```igor
ModifyGizmo modifyObject=objName, objectType=matrix4x4, property={propertyName,data}
```

For more information also see [Advanced Gizmo Techniques[Matrix4x4 Objects]](/igorpro/graphing/3d-graphics.md#matrix4x4-objects).

### *Keywords* {#modifygizmo-for-matrix4x4-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {srcWave, *wave* }</span> | *wave* is a 2D single-precision or double-precision floating point wave with 4 rows and 4 columns. |




<!-- IndentedSubtopic -->
## ModifyGizmo for String Objects {#modifygizmo-for-string-objects}

The syntax for modifying a Gizmo string object is:


```igor
ModifyGizmo modifyObject=objName, objectType=string, property={propertyName,data}
```

String objects are deprecated.

For more information also see [Gizmo Drawing Objects[String Objects]](/igorpro/graphing/3d-graphics.md#string-objects).

### *Keywords* {#modifygizmo-for-string-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {font, *fontNameStr*}</span> |  |
|  | *fontNameStr* is the name of a font, such as "Arial", to use to draw the string. |
| <span class="table-cell-nowrap">property = {size, *value*}</span> |  |
|  | *value* is an integer that specifies the font size for the string. |
| <span class="table-cell-nowrap">property = {string, *text*}</span> |  |
|  | *text* is the string text, limited to 255 bytes. |


<!-- IndentedSubtopic -->
## ModifyGizmo for ColorScale Objects {#modifygizmo-for-colorscale-objects}

The syntax for modifying a Gizmo colorscale object is:


```igor
ModifyGizmo modifyObject=objName, objectType=colorscale, property={propertyName,data}
```

ColorScale objects are deprecated.

For more information also see [Gizmo Drawing Objects[ColorScale Objects]](/igorpro/graphing/3d-graphics.md#colorscale-objects).

### *Keywords* {#modifygizmo-for-colorscale-objects-keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">property = {alpha, *value* }</span> |  |
|  | Sets the alpha the alpha value associated with the color table in the range [0,1]. |
| <span class="table-cell-nowrap">property = {axisRGB, *R*, *G*, *B* }</span> |  |
|  | R, G, B values for painting the axis. Values are in the range of [0,1] and alpha is assumed 1. |
| <span class="table-cell-nowrap">property = {calcNormals, *enable* }</span> |  |
|  | Enables (*enable* =1) or disables (*enable* =0) the calculation of normals for the object. |
|  | Normals are required for lighting/shading and smoothing effects. Calculation of normals takes graphics resources so it should be turned off unless it is needed. |
| <span class="table-cell-nowrap">property = {clipped, *mode* }</span> |  |
|  | Determines if the colorscale is clipped by the global clipping planes. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not clipped</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Clipped</td></tr></tbody></table>
|  | By default clipping is on. For more information see [Gizmo Clipping](/igorpro/graphing/3d-graphics.md#gizmo-clipping). |
| <span class="table-cell-nowrap">property = {colorTable, *name* }</span> |  |
|  | *name* specifies a built-in Igor color table to use for the colorscale colors. For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {colorWave, *wave* }</span> |  |
|  | *wave* is a 2D wave containing RGB or RGBA values in the range [0,1] where each row corresponds to one color. The colorscale is divided into segments representing the total number of rows. There should be more than one valid row. |
| <span class="table-cell-nowrap">property = {CTABScaling, *mode* }</span> |  |
|  | *mode* is a bitwise setting that controls the marker coloring when using a color table. |
|  | One and only one bit from bit 0 through 4 must be set. In addition, any of bits 5, 6, 8 or 9 may be set. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>From min X to max X</td></tr><tr><td>Bit&nbsp;1:</td><td>From min Y to max Y</td></tr><tr><td>Bit&nbsp;2:</td><td>From min Z to max Z</td></tr><tr><td>Bit&nbsp;3:</td><td>From 0 to max sqrt(X^2+Y^2)</td></tr><tr><td>Bit&nbsp;4:</td><td>From 0 to max sqrt(X^2+Y^2+Z^2)</td></tr><tr><td>Bit&nbsp;5:</td><td>Minimum value and color specified</td></tr><tr><td>Bit&nbsp;6:</td><td>Maximum value and color specified</td></tr><tr><td>Bit&nbsp;7:</td><td>Not used - set to 0</td></tr><tr><td>Bit&nbsp;8:</td><td>Color table maps plot-global X range</td></tr><tr><td>Bit&nbsp;9:</td><td>Color table maps plot-global Y range</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
|  | For more information see [Color Tables in Gizmo](/igorpro/graphing/3d-graphics.md#color-tables-in-gizmo). |
| <span class="table-cell-nowrap">property = {drawAxis, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Do not draw an axis.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Draw an axis.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {depth, *value* }</span> |  |
|  | *value* is the depth of the colorscale bar in +/-1 display volume units. It is set to 0 by default. Positive values produce a 3D cube-like colorscale. |
| <span class="table-cell-nowrap">property = {dependsOn, *objectName* }</span> |  |
|  | The colorscale may be independent. Use this keyword if you want to attach it to a particular object for the purposes of obtaining the minimum and maximum values. |
| <span class="table-cell-nowrap">property = {drawFrame, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Do not draw a frame.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Draw a frame.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {frameLineWidth, *width* }</span> |  |
|  | *width* is a positive number. |
| <span class="table-cell-nowrap">property = {inverseCTab, *mode* }</span> |  |
|  | Specifies if the color table used to draw the colorscale is inverted. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not inverted</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Inverted</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {maxRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | Use an unscaled maximum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. |
| <span class="table-cell-nowrap">property = {minRGBA, *value*, *R*, *G*, *B*, *A* }</span> |  |
|  | Use an unscaled minimum value followed by 4 values for *R*, *G*, *B*, and *A* in the range [0,1]. |
| <span class="table-cell-nowrap">property = {mode, *mode* }</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=1:</td><td>The colorscale minimum and maximum values are independent.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>The colorscale minimum and maximum values depend on a single object.</td></tr><tr><td>*mode*&nbsp;=3:</td><td>The colorscale minimum and maximum values depend on all data objects.</td></tr></tbody></table>
| <span class="table-cell-nowrap">property = {translate, *tX*, *tY*, *tZ* }</span> |  |
|  | Sets the translation of the colorscale in the X, Y and Z directions relative to the origin. The parameters are translation components in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {position, *x0*, *y0*, *z0*, *x1*, *y1*, *z1* }</span> |  |
|  | Specifies the XYZ locations of the start and end points of the colorscale in +/-1 display volume coordinates. |
| <span class="table-cell-nowrap">property = {rotation, *rX*, *rY*, *rZ* }</span> |  |
|  | Sets the rotation of the colorscale. |
|  | *rX*, *rY*, *rZ* are the rotations about the X, Y and Z axes in degrees. |
| <span class="table-cell-nowrap">property = {scale, *sX*, *sY*, *sZ* }</span> |  |
|  | Sets the scaling of the colorscale. |
|  | *sX*, *sY*, *sZ* are the scaling factors in the direction of the axes. |
| <span class="table-cell-nowrap">property = {tickLength, *length* }</span> |  |
|  | *length* is the length of the tick marks in +/-1 display volume units. |
| <span class="table-cell-nowrap">property = {tickMarks, *minValue*, *incrementValue*, *numTicks* }</span> |  |
|  | *minValue*, *incrementValue*, and *numTicks* specify the locations of tick marks. These are similar to using canonical tick marks on a regular axis. |
| <span class="table-cell-nowrap">property = {width, *value* }</span> |  |
|  | *value* is the width of the colorscale bar in +/-1 display volume units. The default is 0.1. |