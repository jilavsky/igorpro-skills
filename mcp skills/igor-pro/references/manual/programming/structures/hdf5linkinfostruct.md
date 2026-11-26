---
description: "The HDF5LinkInfoStruct structure is used with the HDF5LinkInfo function. It was added in Igor Pro 9.00."
slug: /programming/structures/hdf5linkinfostruct
---

## HDF5LinkInfoStruct {#hdf5linkinfostruct}

The HDF5LinkInfoStruct structure is used with the [HDF5LinkInfo](/igorpro/commands/hdf5linkinfo.md) function. It was added in Igor Pro 9.00.

The HDF5LinkInfo function is of use only in very rare cases. Most HDF5 users will never need to use it.


```igor
Structure HDF5LinkInfoStruct
   uint32 version                      // Structure version - Set to HDF5LinkInfoStructVersion
	
   // Output fields (outputs from HDF5LinkInfo)
   Int32 linkType                      // H5L_TYPE_ERROR, H5L_TYPE_HARD, H5L_TYPE_SOFT, H5L_TYPE_EXTERNAL or a user-defined link ID
   String linkTypeStr                  // Human-readable string: "hard link", "soft link", "external link", "user-defined link"
   String linkTarget                   // Path to target of link - not used for external links
   String externalLinkTargetFilePath   // Path to file referenced by external link
   String externalLinkTargetObjectPath // Path to object referenced by external link
EndStructure
```

The HDF5LinkInfoStructVersion constant is provided by the "HDF5 Browser.ipf" file.

The constants H5L_TYPE_ERROR, H5L_TYPE_HARD, H5L_TYPE_SOFT, and H5L_TYPE_EXTERNAL are provided by the "HDF5 Browser.ipf" file. See the HDF5 library reference information for a discussion of these constants. See also the HDF5 reference documenation for H5Lget_val and related functions.

The HDF5LinkInfo function sets the linkTarget field only if linkType is H5L_TYPE_HARD or H5L_TYPE_SOFT. The linkTarget field is null otherwise.

The HDF5LinkInfo function sets the externalLinkTargetFilePath and externalLinkTargetObjectPath fields only if linkType is H5L_TYPE_EXTERNAL. These fields are null otherwise.

All of the string fields are null if linkType is other than H5L_TYPE_HARD, H5L_TYPE_SOFT or H5L_TYPE_EXTERNAL.