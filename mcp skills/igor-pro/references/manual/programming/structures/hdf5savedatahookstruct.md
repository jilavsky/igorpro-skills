---
description: "The HDF5SaveDataHook structure has the following members: The current structure version is 1000."
slug: /programming/structures/hdf5savedatahookstruct
---

## HDF5SaveDataHookStruct {#hdf5savedatahookstruct}

The HDF5SaveDataHook structure has the following members:


| Member | Description |
| --- | --- |
| UInt32 version | Structure version = 1000 means "1.000". |
| Int32 operation |<table class="nested-table"><tbody><tr><td>0:</td><td>none (called from UI)</td></tr><tr><td>1:</td><td>HDF5SaveData operation</td></tr><tr><td>2:</td><td>HDF5SaveGroup operation</td></tr></tbody></table>
| WAVE waveToSave | Reference to the wave being saved. |
| Int32 gzipLevel | Level for zip compression from 0 to 9. |
| Int32 shuffle |<table class="nested-table"><tbody><tr><td>0:</td><td>no shuffle</td></tr><tr><td>1:</td><td>shuffle</td></tr></tbody></table>
| Int64 chunkSizes[4] | Chunk size for dimensions 0, 1, 2, and 3 (rows, columns, layers, chunks) |

The current structure version is 1000. If you are called with a version field greater than 1000 but less than 2000, this means that fields were added but that they default to reasonable values. If you are called with a version field 2000 or greater, this means that some incompatible change was made to the structure and your function should return 0.

If operation is 0 then the wave is being saved as a result of a user-interface actions such as File→Save Experiment or File→Save Graph Copy or the HDF5 Browser Save Waves and Save Data Folder buttons or the Data Browser Save Copy button.

If operation is 1 then the wave is being saved by a call to HDF5SaveData. If operation is 2 then the wave is being saved by a call to HDF5SaveGroup. In these cases, you should respect the compression settings specified to those operations unless there is good reason to override them.

If you do not set chunkSizes[dim] or specify chunkSizes[dim]=0, Igor uses the size of the corresponding wave dimension as the chunk size for that dimension. If you specify a chunkSizes[dim] that is greater than the number of elements in the corresponding wave dimension, Igor clips chunkSizes[dim] to that number.

If chunkSizes[dim]==DimSize(dim) for all dimensions that exist in the wave, then the wave is being saved as a single chunk. This may be because HDF5 default compression is being used or because HDF5SaveGroup was called or because HDF5SaveData was called without specifying chunk sizes. In these cases, you may want to override the chunk sizes if you have a good reason to do so.

See [Using HDF5SaveDataHook](/igorpro/data/igor-hdf5-guide.md#using-hdf5savedatahook) for further discussion.