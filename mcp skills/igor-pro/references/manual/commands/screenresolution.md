---
description: "The ScreenResolution function returns the logical resolution of your video display screen in dots per inch (dpi)."
slug: /commands/screenresolution
---

<div className="command-signature">

## <strong>ScreenResolution</strong> {#screenresolution}

</div>

The ScreenResolution function returns the logical resolution of your video display screen in dots per inch (dpi). It is usually 96 (small fonts) or 120 (large fonts).

### *Examples* {#examples}

```igor
// 72 is the number of points in an inch which is constant.
Variable pixels = numPoints * (ScreenResolution/72)	// Convert points to pixels
Variable points = numPixels * (72/ScreenResolution)	// Convert pixels to points
```

### *See Also* {#see-also}
[PanelResolution](/igorpro/commands/panelresolution.md)