---
description: "The HDF5Control operation provides control of aspects of Igor's use of the HDF5 file format."
slug: /commands/hdf5control
---

<div className="command-signature">

## <strong>HDF5Control</strong>  [ <em>keyword</em> = <em>value</em>  [, <em>keyword</em> = <em>value</em> ...] ] {#hdf5control}

</div>

The HDF5Control operation provides control of aspects of Igor's use of the HDF5 file format.

The HDF5Control operation was added in Igor Pro 9.00.

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">defaultCompression = {*enable, minWaveElements, gzipLevel, shuffle*}</span> |  |
|  | See [HDF5 Default Compression](/igorpro/data/igor-hdf5-guide.md#hdf5-default-compression) for background information. |
|  | *enable* is 1 to enable default compression, 0 to disable it, or -1 to leave the enable state unchanged. |
|  | *minWaveElements* is the minimum number of elements that a wave must have to be eligible for default compression or -1 to leave the *minWaveElements* setting unchanged. |
|  | *gzipLevel* is a compression level value from 0 to 9 or -1 to leave the *gzipLevel* setting unchanged. 0 means no GZIP compression. |
|  | *shuffle* is 0 to turn shuffle off or 1 to turn shuffle on or -1 to leave the *shuffle* setting unchanged. |
|  | You can determine current HDF5 default compression settings using IgorInfo(14). |
|  | Normally you should abstain from using HDF5Control defaultCompression since that overwrites the user's HDF5 default compression settings as entered in the Experiment section of the Miscellaneous Settings dialog. The defaultCompression is provided for advanced Igor programmers writing packages for use by novice Igor users. |

### *See Also* {#see-also}
[HDF5 Default Compression](/igorpro/data/igor-hdf5-guide.md#hdf5-default-compression)