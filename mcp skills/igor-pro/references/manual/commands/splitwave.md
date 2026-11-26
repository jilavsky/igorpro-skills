---
description: "The SplitWave operation creates new waves containing subsets of the data in srcWave which must be 2D or greater."
slug: /commands/splitwave
---

<div className="command-signature">

## <strong>SplitWave</strong>  [<em>flags</em>]  <em>srcWave</em> {#splitwave}

</div>

The SplitWave operation creates new waves containing subsets of the data in *srcWave* which must be 2D or greater.

The newly generated waves have lower dimensionality than *srcWave*. The operation is ideal for splitting 2D waves into constituent columns, 3D waves into their layers, etc.

Added in Igor Pro 7.00.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/DDF = *destDataFolder*</span> |  |
|  | Specifies the data folder where the generated waves are created. If the data folder does not exist the operation creates it. If the /DDF flag is not used, output goes into the current data folder. |
| <span class="table-cell-nowrap">/FREE</span> | Generates free output waves. The /OREF flag must also be used when the /FREE flag is used. When you use this flag there is no need to use either /N or /NAME. |
| <span class="table-cell-nowrap">/N = *baseName*</span> | Provides the base name for all output waves. The waves will be named sequentially, i.e., baseName0, baseName1... |
| <span class="table-cell-nowrap">/NAME = *strList*</span> | *strList*,is a semicolon-separated list of wave names to be used as the names of the output waves. |
|  | If *strList*,contains fewer names than the number needed, the operation terminates and returns an error. |
|  | If the output data folder is the data folder containing *srcWave*,then *strList*,must not contain the name of *srcWave*. |
|  | Only simple names, not full paths, are allowed in *strList*. |
| <span class="table-cell-nowrap">/NOTE</span> | Copies the wave note, if any, from *srcWave* to the output waves. The /NOTE flag was added in Igor Pro 8.00. |
| <span class="table-cell-nowrap">/O</span> | Permits overwriting of existing destination waves. Overwriting *srcWave*,is not permitted. |
| <span class="table-cell-nowrap">/OREF = *waveRefWave*</span> |  |
|  | *waveRefWave*,is a wave reference wave. SplitWave stores a wave reference for each of the output waves in *waveRefWave* . |
|  | If the specified *waveRefWave*,already exists it is overwritten and its size is changed as appropriate. If it does not already exist, it is created by the operation. |
| <span class="table-cell-nowrap">/SCL = *val*</span> | Determines whether scaling and labels are copied from the source wave to the destination waves. |
|  |<table class="nested-table"><tbody><tr><td>*val*&nbsp;=0:</td><td>Does not copy scaling and labels (default).</td></tr><tr><td>*val*&nbsp;=1:</td><td>Copies scaling and labels.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/SDIM = *n*</span> | Specifies the dimensionality of the output waves. By default this is 1 less than the dimensionality of *srcWave*. The minimum value is n=1 which results in 1D output waves. |
| <span class="table-cell-nowrap">/Z[ = *z*]</span> | /Z or /Z=1 prevents procedure execution from aborting if there is an error. Use /Z if you want to handle this case in your procedures rather than having execution abort. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Same as no /Z at all. This is the default.</td></tr><tr><td>/Z=1:</td><td>Same as /Z alone.</td></tr></tbody></table>

### *Details* {#details}
The SplitWave operation is in some ways the inverse of the [Concatenate](/igorpro/commands/concatenate.md) operation. *srcWave*,is decomposed into waves of lower dimensionality.

- Splitting a 2D 10x15 wave results in 15 waves of 10 rows each.
- Splitting a 3D 10x15x4 using /SDIM=2 results in 4 2D waves of dimension 10x15.
- Splitting a 3D 10x15x4 using /SDIM=1 results in 60 1D waves of 10 rows each.

The SplitWave operation works on all wave types. *srcWave* must be 2D or greater.

The operation creates the string variable S_waveNames which contains a semicolon-separated list of the names of the output waves. However if you use /FREE then S_waveNames will be empty as free waves cannot be accessed by name; use /OREF to access the created waves.

### *Examples* {#examples}

```igor
// Create sample input
Make/N=(5,4,3,2) wave1 = p + 10*q + 100*r + 1000*s

// Split chunks into 2 3D waves and store them in data folder Chunks
SplitWave/DDF=Chunks/N=chunk wave1 

// Split layers into 6 2D waves and store them in data folder Layers
SplitWave/DDF=Layers/N=Layers/SDIM=2 wave1 

// Split into 24 1D waves and store them in data folder Columns
SplitWave/DDF=Columns/N=Columns/SDIM=1 wave1
```

### *See Also* {#see-also}
[Duplicate](/igorpro/commands/duplicate.md), [Redimension](/igorpro/commands/redimension.md), [Concatenate](/igorpro/commands/concatenate.md)