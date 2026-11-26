---
description: "The HDF5DimensionScale operation supports the creation and querying of HDF5 dimension scales."
slug: /commands/hdf5dimensionscale
---

<div className="command-signature">

## <strong>HDF5DimensionScale</strong>  [ /Z ] [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#hdf5dimensionscale}

</div>

The HDF5DimensionScale operation supports the creation and querying of HDF5 dimension scales. Dimension scales are primarily of use in connection with the netCDF-4 format which is based on HDF5. Most Igor users do not need to know about dimension scales. See [HDF5 Dimension Scales](/igorpro/data/igor-hdf5-guide.md#hdf5-dimension-scales) for background information.

The HDF5DimensionScale operation was added in Igor Pro 9.00.

The operation is implemented using keyword=value syntax for setting parameters and simple keywords without values for invoking actions. For example, these commands convert a particular dataset into a dimension scale and then attach that dimension scale to another dataset:


```igor
// Convert a dataset named XScale into a dimension scale with name "X"
HDF5DimensionScale dataset={fileID,"XScale"}, dimName="X", setScale

// Attach dimension scale XScale to dimension 0 of dataset Data0
HDF5DimensionScale scale={fileID,"XScale"}, dataset={fileID,"Data0"}, dimIndex=0, attachScale
```

All keywords except getScaleName require that you specify a target dataset using the dataset keyword. Many of these also require that you specify a dimension using the dimIndex keyword.

Four of the keywords, attachScale, detachScale, isScaleAttached, and getScaleName, require that you specify an existing dimension scale using the scale keyword.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal - if an error occurs, procedure execution continues. You can check the V_Flag output variable to see if an error occurred. |

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">dataset = {*dataLocID*,*dataPath*}</span> |  |
|  | Specifies the dataset that is the target of a subsequent action keyword. |
|  | *dataPath* can be a full path or a partial path or simple name relative to the group specified by *dataLocID*. |
| <span class="table-cell-nowrap">scale = {*dimScaleLocID*,*dimScalePath*}</span> |  |
|  | Specifies the dimension scale that is used by a subsequent action keyword. scale is used with the following action keywords: attachScale, detachScale, isScaleAttached, getScaleName. |
|  | *dimScalePath* can be a full path or a partial path or simple name relative to the group specified by *dimScaleLocID*. |
| <span class="table-cell-nowrap">dimName = *name*</span> | Specifies the dimension name used by the setScale action keyword when converting a dataset to a dimension scale. dimName is used only with the setScale action keyword and *name* defaults to "". |
| <span class="table-cell-nowrap">dimIndex = *index*</span> | Specifies a particular dimension of a dataset. *index* is zero-based and defaults to 0. dimIndex is used with the following action keywords: attachScale, detachScale, isScaleAttached, getNumScales, getScaleList, getDimLabel, setDimLabel. |
| setScale | Converts a dataset specified by the dataset keyword to a dimension scale with a name optionally specified by the dimName keyword. For example: |
|  | <code class="igor">HDF5DimensionScale dataset={fileID,"XScale"}, dimName="X", setScale</code> |
|  | It is OK to call setScale on a dataset that is already a dimension scale. Doing so does may change the dimension name but does not affect the dimension scale's REFERENCE_LIST attribute. |
| isScale | Returns in the output variable V_Value the truth that the specified dataset is a dimension scale. For example: |
|  | <code class="igor">HDF5DimensionScale dataset={fileID,"XScale"}, isScale&#10;Print V_Value		// 1=dataset is a dimension scale, 0=dataset is not a dimension scale</code> |
| attachScale | Attaches a dimension scale specified by the scale keyword to a dataset specified by the dataset keyword. The dimIndex keyword specifies the dimension of the dataset to which the dimension scale is attached. For example: |
|  | <code class="igor">HDF5DimensionScale scale={scaleLocID,scalePath}, dataset={dataLocID,dataPath}, dimIndex=0, attachScale</code> |
|  | It is OK to call attachScale multiple times for the given dimension of a dataset. |
| detachScale | Detaches a dimension scale specified by the scale keyword from a dataset specified by the dataset keyword. The dimIndex keyword specifies the dimension of the dataset from which the dimension scale is detached. For example: |
|  | <code class="igor">HDF5DimensionScale scale={scaleLocID,scalePath}, dataset={dataLocID,dataPath}, dimIndex=0, detachScale</code> |
|  | DetachScale returns an error if the specified scale is not attached to the specified dimension. |
| isScaleAttached | Returns in the output variable V_Value the truth that the specified dimension scale is attached to the specified dimension of the specified dataset. For example: |
|  | <code class="igor">HDF5DimensionScale scale={scaleLocID,scalePath}, dataset={dataLocID,dataPath}, dimIndex=0, isScaleAttached&#10;Print V_Value		// 1=scale is attached, 0=scale not attached</code> |
| getNumScales | Returns in the output variable V_Value the number of dimension scales attached to the specified dimension of the specified dataset. For example: |
|  | <code class="igor">HDF5DimensionScale dataset={dataLocID,dataPath}, dimIndex=0, getNumScales&#10;Print V_Value</code> |
| getScaleList | Returns via the output variable S_Value a list of full HDF5 paths to the dimension scales that are attached to the specified dimension of the specified dataset. For example: |
|  | <code class="igor">HDF5DimensionScale dataset={dataLocID,dataPath}, dimIndex=0, getScaleList&#10;Print S_Value</code> |
|  | Because semicolon is allowed in an HDF5 object name, S_Value is separated by carriage-return characters ("\r") instead of the usual semicolons. |
| getScaleName | Returns via the output variable S_Value the name that was associated with a dimension scale when the dataset was designated as a dimension scale. For example: |
|  | <code class="igor">HDF5DimensionScale dataset={fileID,"XScale"}, dimName="X", setScale&#10;HDF5DimensionScale scale={fileID,"XScale"}, getScaleName&#10;Print S_Value		// Prints "X"</code> |
| <span class="table-cell-nowrap">dimLabel = *label*</span> | Specifies a dimension label to be used by the setDimLabel action keyword. |
| setDimLabel | Sets the dimension label for a dimension of a dataset. For example: |
|  | <code class="igor">HDF5DimensionScale dataset={dataLocID,dataPath}, dimIndex=0, dimLabel="X", setDimLabel</code> |
|  | The HDF5 library allows you to set a dimension label even if there are no dimension scales attached to the target dataset. |
| getDimLabel | Returns via the output variable S_Value the label that is associated with a particular dimension of a dataset by the setDimLabel keyword. For example: |
|  | <code class="igor">HDF5DimensionScale dataset={dataLocID,dataPath}, dimIndex=index, getDimLabel&#10;Print S_Value</code> |
|  | If you call getDimLabel on a dataset dimension for which no label was set, you get S_Value="". |

### *Output Variables* {#output-variables}
HDF5DimensionScale sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |
|  | If a keyword causes an error, HDF5DimensionScale returns an error without executing any subsequent keywords. If you use /Z, the error does not stop procedure execution and you can handle it in your code. |
| V_Value | Set by the isScale, isScaleAttached, and getNumScales action keywords. |
| S_Value | Set by the getScaleList, getScaleName, and getDimLabel action keywords. |

### *Details* {#details}
You can invoke multiple action keywords in a single call to HDF5DimensionScale. However, you should invoke only one action keyword that sets the V_Value or S_Value outputs.

### *See Also* {#see-also}
[HDF5 Dimension Scales](/igorpro/data/igor-hdf5-guide.md#hdf5-dimension-scales)