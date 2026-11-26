---
description: "The HDF5DataInfo structure is used with the HDF5DatasetInfo and HDF5AttributeInfo functions."
slug: /programming/structures/hdf5datainfo
---

## HDF5DataInfo {#hdf5datainfo}

The HDF5DataInfo structure is used with the [HDF5DatasetInfo](/igorpro/commands/hdf5datasetinfo.md) and [HDF5AttributeInfo](/igorpro/commands/hdf5attributeinfo.md) functions.


```igor
Structure HDF5DataInfo
   // Input fields (inputs to HDF5DatasetInfo)
   uint32 version                  // Must be set to kHDF5DataInfoVersion
   char structName[16]             // Must be "HDF5DataInfo"
   
   // Output fields (outputs from HDF5DatasetInfo)
   double datatype_class;          // e.g., H5T_INTEGER, H5T_FLOAT
   char datatype_class_str[32];    // String with class spelled out, e.g., "H5T_INTEGER", "H5T_FLOAT"
   int32 datatype_is_vlen          // 1 if datatype is variable length, 0 if not
   double datatype_size;           // Size in bytes of one element
   double datatype_sign;           // H5T_SGN_NONE (unsigned), H5T_SGN_2 (signed), H5T_SGN_ERROR (this type does
                                   // not have a sign, i.e., it is not an integer type)
   double datatype_order;          // H5T_ORDER_LE, H5T_ORDER_BE, H5T_ORDER_VAX
   char datatype_str[64];          // Human-readable string, e.g., "16-bit unsigned integer"
   double dataspace_type;          // H5S_NO_CLASS, H5S_SCALAR, H5S_SIMPLE
   double ndims;                   // Zero for H5S_SCALAR. Number of dimensions in the dataset for H5S_SIMPLE
   double dims[H5S_MAX_RANK];      // Size of each dimension
   double maxdims[H5S_MAX_RANK];   // Maximum size of each dimension
   
   // Fields added in Igor Pro 9.00 - Set by HDF5DatasetInfo, not by HDF5AttributeInfo
   // These fields are set only if bit 2 of the options parameter to HDF5DatasetInfo is set
   double layout                   // H5D_COMPACT, H5D_CONTIGUOUS, H5D_CHUNKED, H5D_VIRTUAL
   double nchunks                  // Number of chunks if layout is H5D_CHUNKED
   uint64 chunks[32]               // Size of each chunk
   uint64 file_size                // Size of dataset on disk
   uint64 mem_size                 // Size of dataset in memory
   String filters                  // Description of dataset compression filter
EndStructure
```

The datatype_is_vlen field was added in Igor Pro 9.00. If datatype_is_vlen is non-zero then the datatype_size, file_size, and mem_size fields reflect the size of a pointer, not the size of the data itself. In that case, those fields cannot be used for determining compression.

The remaining fields added in Igor Pro 9.00, layout, nchunks, chunks, file_size, mem_size, and filters, are for advanced HDF5 users and are not needed by most applications. These fields are set by [HDF5DatasetInfo](/igorpro/commands/hdf5datasetinfo.md) only if bit 2 of the options parameter is set. They are not set by [HDF5AttributeInfo](/igorpro/commands/hdf5attributeinfo.md).

**Filters Field**

The filters field is "" if the dataset has no compression filters or a semicolon-separated list containing zero or more of the following:

GZIP:\<level\>, SHUFFLE, FLETCHER32, SZIP, NBIT, SCALEOFFSET, USER

For example, for a dataset that is zip-compressed using level 6 compression and shuffle compression, the filters field is: "GZIP:6;SHUFFLE;".

"USER" represents a user-defined filter, i.e., a filter that is not built-in to the HDF5 library.

For further information, see "Data Pipeline Filters" in the HDF5 User's Guide.