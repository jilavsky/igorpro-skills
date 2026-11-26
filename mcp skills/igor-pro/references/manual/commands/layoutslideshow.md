---
description: "The LayoutSlideShow operation starts, stops, or modifies a slideshow that displays the pages of a page layout."
slug: /commands/layoutslideshow
---

<div className="command-signature">

## <strong>LayoutSlideShow</strong>  [/W=<em>winName</em> ] [<em>keyword</em> = <em>value</em> ] ... {#layoutslideshow}

</div>

The LayoutSlideShow operation starts, stops, or modifies a slideshow that displays the pages of a page layout.

The LayoutSlideShow operation was added in Igor Pro 7.00.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">autoMode = *a*</span> | Controls whether the presentation will advance between slides automatically (*a* =1) or manually (*a* =0). Use the delay keyword to control the delay between automatic transitions. |
| <span class="table-cell-nowrap">delay = *d*</span> | *d* is the number of seconds to wait between slide transitions when running in auto mode. |
| <span class="table-cell-nowrap">otherScreenContents = *o*</span> |  |
|  | Controls what is displayed on any additional screens that may be connected. |
|  |<table class="nested-table"><tbody><tr><td>*o*=0:</td><td>Other screens show the presentation.</td></tr><tr><td>*o*=1:</td><td>Other screens show a presenter&#39;s view with additional information. Use the *presentersView* keyword to control the contents of this view.</td></tr><tr><td>*o*=2:</td><td>Other screens are not used.</td></tr></tbody></table>
| <span class="table-cell-nowrap">page = *p*</span> | Causes the slideshow to start from page *p*. *p* is a page number starting from 1. This keyword has no effect unless the *start* keyword is also present. |
| <span class="table-cell-nowrap">presentersView = *p*</span> | Controls what is displayed on the screens that show the presenter's view. *p* is a bitfield of flags: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Show the next page.</td></tr><tr><td>Bit&nbsp;1:</td><td>Show the current time.</td></tr><tr><td>Bit&nbsp;2:</td><td>Show the elapsed time.</td></tr></tbody></table>
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">scaleMode = *s*</span> | Specifies how the pages are scaled to fit the screen. |
|  |<table class="nested-table"><tbody><tr><td>*s*=0:</td><td>No scaling. Pages are drawn at actual size even if they are much larger or smaller than the screen size.</td></tr><tr><td>*s*=1:</td><td>All pages are individually scaled to the screen size.</td></tr><tr><td>*s*=2:</td><td>All pages are scaled by the same factor so that the largest page fits on the screen. This preserves the relative sizes of the pages.</td></tr></tbody></table>
| <span class="table-cell-nowrap">screen = *s*</span> | Specifies the screen to be used for the main presentation. Use *s*=1 to use the primary screen. Use [IgorInfo](/igorpro/commands/igorinfo.md) to determine the number of available screens. |
| start | Starts the slideshow. |
| stop | Stops the slideshow. You can also stop it by pressing the escape key. |
| <span class="table-cell-nowrap">wrapMode = *w*</span> | Controls what happens when the presentation reaches the last page in the slideshow. |
|  |<table class="nested-table"><tbody><tr><td>*w*=0:</td><td>Advancing to the next page has no effect.</td></tr><tr><td>*w*=1:</td><td>Advancing to the next page causes the slideshow to wrap around to the first page.</td></tr><tr><td>*w*=2:</td><td>Advancing to the next page causes the slideshow to stop.</td></tr></tbody></table>

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | *winName* is the name of the desired layout window. If /W is omitted or if winName is $"", the top layout window is used. |

### *Details* {#details}
A layout slide show can be used to present an Igor experiment to others, or to run an information kiosk.

Any changes to the layout window during a slide show are automatically reflected in the slides. For example you could use a background task to update a graph so that the slides always show the latest data.

You can control a running slide show by right-clicking on the slideshow. Alternatively, use the arrow keys or a mouse click to advance to the next slide.

Press the space bar to toggle between automatic and manual advancing of the slides.

Press escape to end the slideshow.

### *Example* {#example}

```igor
Function DemoSlideshow()	// Press escape to end the slideshow
	NewLayout
	TextBox/C/N=text0/F=0/A=LB/X=33.57/Y=70.81 "\\Z961"
	LayoutPageAction appendpage
	TextBox/C/N=text0/F=0/A=LB/X=33.57/Y=70.81 "\\Z962"
	LayoutPageAction appendpage
	TextBox/C/N=text0/F=0/A=LB/X=33.57/Y=70.81 "\\Z963"
	LayoutSlideShow autoMode=1,delay=1,page=1,wrapMode=1,start
End
```

### *See Also* {#see-also}
[Page Layouts](/igorpro/graphing/making-figures/page-layouts.md), [NewLayout](/igorpro/commands/newlayout.md), [LayoutPageAction](/igorpro/commands/layoutpageaction.md)