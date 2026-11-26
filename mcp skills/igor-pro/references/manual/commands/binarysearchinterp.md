---
description: "The BinarySearchInterp function performs a binary interpolated search of the named wave for the value val."
slug: /commands/binarysearchinterp
---

<div className="command-signature">

## <strong>BinarySearchInterp</strong> (<em>waveName</em>, <em>val</em>) {#binarysearchinterp}

</div>

The BinarySearchInterp function performs a binary interpolated search of the named wave for the value *val*. The returned value, pt, is a floating-point point index into the named wave such that *waveName* [pt] == *val*.

### *Details* {#details}
BinarySearchInterp is useful for finding the point in an XY pair that corresponds to a particular X coordinate.

*WaveName* must contain monotonically increasing or decreasing values.

When the named wave does not actually contain the value *val*, BinarySearchInterp locates a value below *val* and a value above *val* and uses reverse linear interpolation to figure out where *val* would fall if a straight line were drawn between them. It includes that fractional amount in the resulting point index.

BinarySearchInterp returns NaN if *val* is not within the range of values in the wave, but would numerically be placed before the first value in the wave or after the last value in the wave.

### *Examples* {#examples}

```igor
Make/O data = {1, 2, 3.3, 4.9}      // Monotonic increasing
Print BinarySearchInterp(data,3)    // Prints 1.76923
Print data[1.76923]                 // Prints 3
Make/O data = {9, 4, 3, 1}          // Monotonic decreasing
Print BinarySearchInterp(data,2.5)  // Prints 2.25 
Print data[2.25]                    // Prints 2.5
```

### *See Also* {#see-also}
[Indexing and Subranges](/igorpro/igor-basics/waves.md#indexing-and-subranges)

[BinarySearch](/igorpro/commands/binarysearch.md), [FindLevel](/igorpro/commands/findlevel.md)