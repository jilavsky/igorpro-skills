---
description: "The IndexToScale function returns the scaled coordinate value corresponding to wave element index in the specified dimension."
slug: /commands/indextoscale
---

<div className="command-signature">

## <strong>IndexToScale</strong> (<em>wave</em>, <em>index</em>, <em>dim</em>) {#indextoscale}

</div>

The IndexToScale function returns the scaled coordinate value corresponding to wave element index in the specified dimension.

The IndexToScale function was added in Igor Pro 7.00.

### *Details* {#details}
The function returns the expression:


```igor
DimOffset(wave,dim) + index*DimDelta(wave,dim)
```

*index* is an integer.

*dim* is 0 for rows, 1 for columns, 2 for layers or 3 for chunks.

The function returns NaN if *dim* is not a valid dimension or if *index* is greater than the number of elements in the specified dimension.

### *Examples* {#examples}

```igor
Make/N=(10,20,30,40) w4D
SetScale/P y 2,3,"", w4D
SetScale/P z 4,5,"", w4D 
SetScale/P t 6,7,"", w4D
Print IndexToScale(w4D,1,0)
Print IndexToScale(w4D,1,1)
Print IndexToScale(w4D,1,2)
Print IndexToScale(w4D,1,3)
Print IndexToScale(w4D,1,4)
Print IndexToScale(w4D,-1,0)
Print IndexToScale(w4D,11,0)
```

### *See Also* {#see-also}
[ScaleToIndex](/igorpro/commands/scaletoindex.md), [pnt2x](/igorpro/commands/pnt2x.md), [DimDelta](/igorpro/commands/dimdelta.md), [DimOffset](/igorpro/commands/dimoffset.md)

For an explanation of wave scaling, see [The Waveform Model of Data](/igorpro/igor-basics/waves.md#the-waveform-model-of-data).