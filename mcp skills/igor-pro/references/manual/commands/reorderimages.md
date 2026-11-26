---
description: "The ReorderImages operation changes the ordering of graph images to that specified in the braces."
slug: /commands/reorderimages
---

<div className="command-signature">

## <strong>ReorderImages</strong>  [/W=<em>winName</em> ] <em>anchorImage</em>, {<em>imageA</em>, <em>imageB</em>,...} {#reorderimages}

</div>

The ReorderImages operation changes the ordering of graph images to that specified in the braces.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/W = *winName*</span> | Reorders images in the named graph window or subwindow. When omitted, action will affect the active window or subwindow. This must be the first flag specified when used in a Proc or Macro or on the command line. |
|  | When identifying a subwindow with *winName*, see [Subwindow Syntax](/igorpro/graphing/making-figures/subwindows.md#subwindow-syntax) for details on forming the window hierarchy. |

### *Details* {#details}
Igor keeps a list of images in a graph and draws the images in the listed order. The first image drawn is consequently at the bottom. All other images are drawn on top of it. The last image is the top one; no other image obscures it.

ReorderImages works by removing the images in the braces from the list and then reinserting them at the location specified by *anchorImage*. If *anchorImage* is not in the braces, the images in braces are placed before *anchorImage*.

If the list of images is A, B, C, D, E, F, G and you execute the command


```igor
ReorderImages F, {B,C}
```

images B and C are placed just before F: A, D, E, **B**,  **C**,  F, G.

The result of


```igor
ReorderImages E, {D,E,C}
```

is to reorder C, D and E and put them where E was. Starting from the initial ordering this gives A, B, **D**, **E**, **C**, F, G.

ReorderImages generates an error if the same image is in the list twice.

In Igor 7 or later, *anchorImage* can be \_front\_ or \_back\_. To move A to the front, you can write:


```igor
ReorderImages _front_, {A}
```

Igor 10 replaced the one image layer with two layers, Layer 0 (below traces and axes) and Layer 1 (above traces and axes). Prior to Igor 10 images could only be drawn below traces and axes, what is now Layer 0. To preserve backward compatibility, if there are no images in Layer 1, the \_front\_ keyword moves an image to the front of Layer 0 (below traces and axes). If there are images in Layer 1 (above traces and axes), \_front\_ moves images to the front of Layer 1.

If the list of images is like this:


```
 A, B, C, <traces and axes>, D, E, F
<Layer 0>                   <Layer 1>
```

and you execute the command


```igor
ReorderImages _front_, {B}
```

then the image list that results is:

```
A, C, <traces and axes>, D, E, F, B
```

However, if you start from this:

```
A, B, C, D, E, F, <traces and axes>, <empty Layer 1>
```

and execute the same command, the result is:

``` 
A, C, D, E, F, B, <traces and axes>, <empty Layer 1>
```

Note that the first situation results in image B being above traces, and in the second image B is below the traces.

In Igor 10 or later, *anchorImage* can be \_belowtraces\_ or \_abovetraces\_ to move images from Layer 0 (below traces and axes) to Layer 1 (above traces and axes) and vice-versa. The insertion positions for these keywords is conceptually like this:


```
        ↓_belowtraces_
A, B, C, <traces and axes>, D, E, F
              _abovetraces_↑
```

For each command below, the result is shown as it would be starting from the configuration here, with three images in Layer 0 and three in Layer 1.


```igor
ReorderImages _abovetraces_, {B}
```

results in:

```
A, C, <traces and axes>, B, D, E, F
```

```igor
ReorderImages _belowtraces_, {E}
```

results in:

```
A, B, C, E, <traces and axes>, D, F
```

### *See Also* {#see-also}
[ReorderTraces](/igorpro/commands/reordertraces.md)