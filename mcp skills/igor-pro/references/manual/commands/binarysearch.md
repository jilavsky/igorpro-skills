---
description: "The BinarySearch function performs a binary search of waveName for the value val."
slug: /commands/binarysearch
---

<div className="command-signature">

## <strong>BinarySearch</strong> (<em>waveName</em>, <em>val</em>) {#binarysearch}

</div>

The BinarySearch function performs a binary search of *waveName* for the value *val*. BinarySearch returns an integer point number p such that *waveName* [p] and *waveName* [p+1] bracket *val*. If *val* is in *waveName*, then *waveName* [p]==*val.*

### *Details* {#details}
BinarySearch is useful for finding the point in an XY pair that corresponds to a particular X coordinate.

*WaveName* must contain monotonically increasing or decreasing values.

BinarySearch returns -1 if *val* is not within the range of values in the wave, but would numerically be placed before the first value in the wave.

BinarySearch returns -2 if *val* is not within the range of values in the wave, but would fall after the last value in the wave.

BinarySearch returns -3 if the wave has zero points.

### *Examples* {#examples}

```igor
Make/O data = {1, 2, 3.3, 4.9}      // Monotonic increasing
Print BinarySearch(data,3)          // Prints 1 

// BinarySearch returns 1 because data[1] <= 3 < data[2].
Make/O data = {9, 4, 3, -6}         // Monotonic decreasing
Print BinarySearch(data,2.5)        // Prints 2 

// BinarySearch returns 2 because data[2] >= 2.5  >  data[3].
Print BinarySearch(data,10)         // Prints -1, precedes first value
Print BinarySearch(data,-99)        // Prints -2, beyond last value
```

### *See Also* {#see-also}
[BinarySearchInterp](/igorpro/commands/binarysearchinterp.md), [FindLevel](/igorpro/commands/findlevel.md)