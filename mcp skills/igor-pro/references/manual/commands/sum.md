---
description: "The sum function returns the sum of the wave elements for points from x=x1 to x=x2."
slug: /commands/sum
---

<div className="command-signature">

## <strong>sum</strong> (<em>waveName</em> [, <em>x1</em>, <em>x2</em>]) {#sum}

</div>

The sum function returns the sum of the wave elements for points from x=*x1* to x=*x2*.

### *Details* {#details}
The X scaling of the wave is used only to locate the points nearest to x=*x1* and x=*x2*. To use point indexing, replace *x1* with "pnt2x(*waveName*,*pointNumber1* )", and a similar expression for *x2*.

If *x1* and *x2* are not specified, they default to -[inf](/igorpro/commands/inf.md) and +inf, respectively.

If the points nearest to *x1* or *x2* are not within the point range of 0 to numpnts(*waveName* )-1, sum limits them to the nearest of point 0 or point numpnts(waveName)-1.

If any values in the point range are NaN, sum returns NaN.

sum also accepts text waves. Each text element that can be converted to a number is summed as that number; a text wave containing no numeric elements evaluates to 0. For example:

```igor
Make/T/O tw = {"1", "10"}
Print sum(tw)             // numeric text is converted and summed
  11
Make/T/O twNoNum = {"abcd", "efgh"}
Print sum(twNoNum)        // no elements convert to a number
  0
```

Wave reference and data folder reference waves are not a supported input to sum, but no error is raised; sum simply returns 0 for them.

### *Examples* {#examples}

```igor
Make/O/N=100 data; SetScale/I x 0,Pi,data
data=sin(x)
Print sum(data,0,Pi)      // the entire point range, and no more
Print sum(data)           // same as -infinity to +infinity
Print sum(data,Inf,-Inf)  // +infinity to -infinity
```

The following is printed to the history area:


```igor
Print sum(data,0,Pi)      // the entire point range, and no more
  63.0201
Print sum(data)           // same as -infinity to +infinity
  63.0201
Print sum(data,Inf,-Inf)  // +infinity to -infinity
  63.0201
```

### *See Also* {#see-also}
[mean](/igorpro/commands/mean.md), [area](/igorpro/commands/area.md), [SumDimension](/igorpro/commands/sumdimension.md)