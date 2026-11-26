---
description: "The Project operation calculates projections of XY data, which most often are longitude and latitude waves of geographic coordinates."
slug: /commands/project
---

<div className="command-signature">

## <strong>Project</strong>  [/C={<em>long</em>,<em>lat</em> }/M=<em>method</em> /P={<em>p1</em>,<em>p2</em>,...}] <em>longitudeWave</em>, <em>latitudeWave</em> {#project}

</div>

The Project operation calculates projections of XY data, which most often are longitude and latitude waves of geographic coordinates. The output waves are W_XProjection and W_YProjection. Longitude and Latitude are in degrees.

### *Parameters* {#parameters}
*longitudeWave* is the name of the wave supplying the longitude or equivalent coordinates. *latitudeWave* is the name of the wave supplying the latitude or equivalent coordinates.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/C = {*long*,*lat* }</span> | Specifies longitude and latitude center of projection. By default, *long*=0 and *lat*=90. |
| <span class="table-cell-nowrap">/DSTX = *xWave*</span> | Specify the output wave x component of the projection. If you do not specify this flag, the operation saves the data in the wave W_XProjection in the current data folder. |
| This flag was added in Igor Pro 10. |  |
| <span class="table-cell-nowrap">/DSTY = *yWave*</span> | Specify the output wave y component of the projection. If you do not specify this flag, the operation saves the data in the wave W_YProjection in the current data folder. |
| This flag was added in Igor Pro 10. |  |
| <span class="table-cell-nowrap">/FREE</span> | Creates all destination waves as free waves. This flag does not affect an output wave that is created by default without a user-specified destination. |
| <span class="table-cell-nowrap">/FREE</span> is allowed only in functions, and only if the destination waves are simple names or wave reference structure fields. |  |
| See [Free Waves](/igorpro/programming/programming.md#free-waves) for more discussion. |  |
|  | The /FREE flag was added in Igor Pro 10.00. |
| <span class="table-cell-nowrap">/M = *method*</span> | Indicates the type of projection. *method* can be one of the following: |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Orthographic projection (default)</td></tr><tr><td>1:</td><td>Stereographic projection</td></tr><tr><td>2:</td><td>Gnomonic projection</td></tr><tr><td>3:</td><td>General perspective projection</td></tr><tr><td>4:</td><td>Lambert equal area projection</td></tr><tr><td>5:</td><td>Equidistant projection</td></tr><tr><td>6:</td><td>Mercator projection</td></tr><tr><td>7:</td><td>Transverse Mercator projection</td></tr><tr><td>8:</td><td>Albers Equal Area conic</td></tr><tr><td>9:</td><td>Eckert IV (Igor Pro 9.00 or later)</td></tr><tr><td>10:</td><td>Winkel III (Igor Pro 9.00 or later)</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P = {*p1*,*p2*,...}</span> | One or more parameters required by a particular projection. See below for details regarding the individual projection requirements. |

### *Gnomonic* {#gnomonic}
Here there is one extra parameter that defines the boundaries based on the angle. The specific expression for the limit is that cos(c) in Eq. (5-3) of Snyder is greater than the specified parameter:

/P={cos(c)}

The actual transformation uses Eqs. (22-4) and (22-5) with k' given by (22-3).

### *General Perspective* {#general-perspective}
Here there is one extra parameter that defines the boundaries based on the angle. The specific expression for the limit is that cos(c) in Eq. (5-3) of Snyder is greater than the specified parameter.

The actual transformation uses Eqs. (22-4) and (22-5) with k' given by (22-3). Here we specify the height H is units of sphere radius. The tilt of the plane is specified by omega and gamma following the notation of Snyder page 175.

The parameters actually specified by the command are:

/P={*H*,*omega*,*gamma*,*deltax*,*deltay* }

*H* is the height (in radii) above the surface of the earth, *gamma* is the azimuth east of north of the Y axis, and *omega* is the tilt angle or the angle between the projection plane and the tangent plane. The x output will be limited to +/- *deltax* and the y output will be limited to the range +/- *deltay*.

### *Mercator* {#mercator}
This projection requires the following parameters:

/P={*minLong*,*maxLong*,*minLat*,*maxLat* }

If /P is not specified, the default is {0,360,-90,90}

Note that this projection flips the sign of y when cos(longitude-long_0) changes sign. If you are plotting a continuous path in which consecutive points exhibit the sign change, you should add a NaN entry in the wave so that the path does not wrap.

### *Albers Equal Area Conic* {#albers-equal-area-conic}
This projection requires:

/P={*minLong*,*maxLong*,*minLat*,*maxLat*,*Phi1*,*Phi2* }

*Phi1* and *Phi2* are the specification of the two standard parallels, the other four parameters determine the boundary of the map area for display.

### *References* {#references}
Snyder, John P., *Map Projections-A Working Manual*, U.S.G.S. Professional Paper 1395, U.S. Government Printing Office, Washington D.C., 1987, reprinted 1989, 1994, 1997 with corrections.

### *Demos* {#demos}
[Open Project Demo](#igor-pxp/Examples/Feature__Demos__2/Map__Projections__Demo.pxp)