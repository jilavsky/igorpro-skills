---
description: "HDF Loader is an external operation that reads data from HDF4 files. This version of HDF Loader requires Igor Pro 7.00 or later."
slug: /extensions/file-loaders/hdf-loader/hdf-loader-xop
---

HDF Loader is an external operation that reads data from HDF4 files.

This version of HDF Loader requires Igor Pro 7.00 or later. It was build with HDF library version 4.2.13.

For information on HDF4, see: [https://support.hdfgroup.org/hdf4/](https://support.hdfgroup.org/hdf4/)

HDF Loader adds the following command line operations:

[HDFInfo](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfinfo), [HDFReadImage](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfreadimage), [HDFReadSDS](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfreadsds), [HDFReadVSet](/igorpro/extensions/file-loaders/hdf-loader/hdf-loader-operations.md#hdfreadvset)

HDF Loader operations sets the following standard Igor file-loader output variables:


|  |  |
| --- | --- |
| S_fileName | Stores the full path to the loaded file. |
| V_Flag | Stores 0 or an error code if the operation failed. This variable is not reliably set by HDF Loader; sometimes it will be set to zero although an error occurred. |

In addition, the HDFReadVSet sets the S_waveNames string variable.

Many of the operations described below result in creating numeric and string variables. When HDF Loader is called from a macro, all variables are created with local scope. When called from the command line or from a function via the [Execute](/igorpro/commands/execute.md) operation, all variables are global.

Due to the many possible variations of HDF files, it is safer to test first that a particular component exists and only then proceed to read it. If you try to read a component that does not exist, the V_flag parameter may return an error code which must be tested separately. Furthermore, the waves, strings and variables which you expect the operation to create, may or may not exist.

## Revision Notes {#revision-notes}

|  |  |
| --- | --- |
| 1.30 | Ported to Carbon. |
|  | Fixed bug when loading 8 bit non-square images. The wrong data was loaded. |
|  | Fixed bug when loading palettes. The wrong data was loaded for the blue component. |
|  | Fixed bug when loading 24-bit images. The blue plane was not being loaded correctly. |
|  | Made all output variables local when called from macros, to match behavior with documentation. |
|  | Removed the SDSLabel, SDSFormat and SDSUnits keywords used with HDFReadSDS. Use the DimStrings keyword instead. |
|  | Revised help file extensively. |
| 1.31 | Macintosh: Ported to Xcode to create a universal version of HDF Loader. It runs on PowerPC and Intel Macintosh. |
| 1.32 | Macintosh: Fixed problem that caused an error if you tried to load a little-endian SDS. |
| 1.33 | Macintosh: Support long file names. |
| 1.34 | Macintosh: Fixed crash when reading 32-bit unsigned data. Improved error reporting. |
| 1.35 | Added a workaround to HDFReadSDS ref=<ref>. If <ref> is negative, it is the index of the SDS data set in the file (-1 means first SDS, -2 means seconds SDS, . . .). This is a workaround for an apparent bug in the HDF4 library SDreftoindex routine. |
| 1.50 | Created 64-bit versions for Macintosh and Windows. |