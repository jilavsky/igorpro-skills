---
description: "TagVal is a very specialized function that is only valid when called from within the text of a tag as part of a \\{} dynamic text escape sequence."
slug: /commands/tagval
---

<div className="command-signature">

## <strong>TagVal</strong> (<em>code</em>) {#tagval}

</div>

TagVal is a very specialized function that is only valid when called from within the text of a tag as part of a \\{} dynamic text escape sequence. It returns a number reflecting some property of the tag and helps you to display information about the tagged wave. The property is selected by the *code* parameter:


|  |  |
| --- | --- |
| 0: | Similar to \\OP, returns the tag attach point number. |
| 1: | Similar to \\OX, returns the X coordinate of tag attachment in the graph. When a tag is attached to an XY pair of traces, the X coordinate will most likely be different than the tag's X scaling attachment value specified in the [Tag](/igorpro/commands/tag.md) command. |
| 2: | Similar to \\OY, returns the Y coordinate of tag attachment in the graph or Y axis value in a Waterfall plot. |
| 3: | Similar to \\OZ, returns the Z coordinate of tag attachment in a contour, image, or Waterfall plot. |
| 4: | Similar to \\Ox, returns the trace x offset. |
| 5: | Similar to \\Oy, returns the trace y offset. |
| 6: | Returns the X muloffset (with the not set value 0 translated to 1). |
| 7: | Returns the Y muloffset (with the not set value 0 translated to 1). |

Because TagVal returns a numeric value, the result can be formatted any way you wish using the [printf](/igorpro/commands/printf.md) formatting codes. In contrast, the \O codes insert preformatted text, and you don't have control over the format.

TagVal is sometimes used in conjunction with the [TagWaveRef](/igorpro/commands/tagwaveref.md)() function. For example, you might write a user-defined function that calculates a value as a function of a wave and a point number.

### *Examples* {#examples}

```igor
Tag wave0, 0, "Y value is \\{\"%g\",TagVal(2)}"
Tag wave0, 0, "Y value is \\{\"%g\",TagWaveRef()[TagVal(0)]}"
Tag wave0, 0, "Y value is \\OY"
```

These examples all produce identical results.

### *See Also* {#see-also}
[Tag](/igorpro/commands/tag.md), [TagWaveRef](/igorpro/commands/tagwaveref.md)