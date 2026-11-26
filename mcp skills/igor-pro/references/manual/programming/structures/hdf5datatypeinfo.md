---
description: "The HDF5DatatypeInfo structure is used with the HDF5TypeInfo function."
slug: /programming/structures/hdf5datatypeinfo
---

## HDF5DatatypeInfo {#hdf5datatypeinfo}

The HDF5DatatypeInfo structure is used with the [HDF5TypeInfo](/igorpro/commands/hdf5typeinfo.md) function.


```igor
Structure HDF5DatatypeInfo
   // Input fields (inputs to HDF5DatatypeInfo)
   uint32 version             // Must be set to kHDF5DataInfoVersion
   char structName[16]        // Must be "HDF5DatatypeInfo"
	
   // Output fields (outputs from HDF5DatatypeInfo)
   double type_class          // e.g., H5T_INTEGER, H5T_FLOAT
   char type_class_str[32]    // String with class spelled out. e.g., "H5T_INTEGER", "H5T_FLOAT"
   int32 type_is_vlen         // 1 if datatype is variable length, 0 if not
   double size                // Size in bytes of one element
   double sign                // H5T_SGN_NONE (unsigned), H5T_SGN_2 (signed), H5T_SGN_ERROR (this type does not 
                              // have a sign, i.e., it is not an integer type)
   double order               // H5T_ORDER_LE, H5T_ORDER_BE, H5T_ORDER_VAX, H5T_ORDER_ERROR (this type 	does not have an order)
   double cset                // H5T_CSET_ASCII, H5T_CSET_UTF8, H5T_CSET_ERROR
   double strpad              // H5T_str_t: H5T_STR_ERROR, H5T_STR_NULLTERM, H5T_STR_NULLPAD, 	H5T_STR_SPACEPAD
   double nmembers            // For enum or compound datatypes only, number of members
   String names               // For enum or compound datatypes only, semicolon-separated list of enum 	names
   int32 values[100]          // For enum datatype only, list of enum values. For compound datatype, list of classes
   String opaque_tag          // For opaque datatypes only, tag name
EndStructure
```

The type_is_vlen field was added in Igor Pro 9.00. If type_is_vlen is non-zero then the size field reflects the size of a pointer in memory, not the size of the data itself. In that case, the size field is of little use.