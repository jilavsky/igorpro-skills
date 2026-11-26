---
description: "The BoundingBall operation calculates a bounding circle or the bounding sphere for a set of scatter points."
slug: /commands/boundingball
---

<div className="command-signature">

## <strong>BoundingBall</strong>  [/F/Z] <em>scatterWave</em> {#boundingball}

</div>

The BoundingBall operation calculates a bounding circle or the bounding sphere for a set of scatter points. The operation accepts 2D waves that have two, three or more columns; data in the additional columns are ignored.

When *scatterWave*  consists of two columns the operation computes the bounding circle. Otherwise it computes the bounding 3D sphere.

### *Parameters* {#parameters}
*scatterWave*  is a two-dimensional wave with X coordinates in column 0, Y in column 1, and optional Z coordinates in column 2.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/F</span> | This flag applies to 3D scatter only. It uses an algorithm from "An Efficient Bounding Sphere" by Jack Ritter originally from *Graphics Gems*. Unfortunately it does not give an accurate bounding ball but something that is sufficiently large. This algorithm is less accurate but it produces a ball which is sufficiently large to contain all the points. |
| <span class="table-cell-nowrap">/Z</span> | No error reporting. |

### *Details* {#details}
The center and radius of the bounding sphere are stored in the variables: V_CenterX, V_CenterY, V_CenterZ, and V_Radius.

If you are not using the /F flag, the operation also accepts a 2 column wave consisting of x,y pairs for calculating the center and radius of a bounding circle in the plane.

### *Example* {#example}

```igor
Make/N=(33,2) ddd=enoise(4)	// Create random data
BoundingBall ddd
Display ddd[][1] vs ddd[][0]
ModifyGraph mode=3
Make/n=360 xxx,yyy
yyy=v_centerY+V_radius*cos(p*2*pi/360)
xxx=v_centerX+V_radius*sin(p*2*pi/360)
AppendToGraph yyy vs xxx
```

### *References* {#references}
Glassner, Andrew S. , (Ed.), "Graphics Gems", 864 pp., Morgan Kaufmann Publishers, 1990.