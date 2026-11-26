---
description: "The HDF5LibraryInfo function returns information about the HDF5 library used by the currently-running version of Igor."
slug: /commands/hdf5libraryinfo
---

<div className="command-signature">

## <strong>HDF5LibraryInfo</strong> (<em>options</em>) {#hdf5libraryinfo}

</div>

The HDF5LibraryInfo function returns information about the HDF5 library used by the currently-running version of Igor. This is of interest to advanced programmers only.

### *Parameters* {#parameters}
If *options* is 0, HDF5LibraryInfo returns the version of the HDF5 library used by Igor. The version is returned as a single number, interpreted as:


```igor
MMmmrr
```

where MM is the major version, mm is the minor version, and rr is the release (bugfix) version. For example, version 1.10.1 is returned as 011001. To see the result in this format, execute:


```igor
Printf "%06d\r", HDF5LibraryInfo(0)
```

All other values for *options* are reserved for future use.

If you pass an invalid value for *options*, HDF5LibraryInfo returns NaN.