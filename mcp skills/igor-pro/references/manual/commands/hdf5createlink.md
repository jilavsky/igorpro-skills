---
description: "The HDF5CreateLink operation creates a new hard, soft or external link in an HDF5 file."
slug: /commands/hdf5createlink
---

<div className="command-signature">

## <strong>HDF5CreateLink</strong>  [ /EXT={<em>pathName</em>, <em>filePath</em>} /HARD=<em>makeHardLink</em> /Q /Z ] <em>targetLocationID</em>, <em>targetName</em>, <em>linkLocationID</em>, <em>linkName</em> {#hdf5createlink}

</div>

The HDF5CreateLink operation creates a new hard, soft or external link in an HDF5 file.

Creating links is not necessary for everyday use of HDF5. This is an advanced feature. You can ignore it for most purposes.

### *HDF5 Link Background Information* {#hdf5-link-background-information}
HDF5 links are explained in the HDF5 User Guide chapter on groups. You need to understand the information presented there to effectively use HDF5CreateLink, but here is a brief overview.

HDF5 files are "directed graphs". The objects (groups, datasets and datatypes) in an HDF5 file have no names. A group object can contain links. It is the links that have names, not the objects.

When you create a new object in an HDF5 file, the HDF5 library automatically creates links. For example, consider this arrangement, where we have created two groups and one dataset in an HDF5 file:


```igor
root
	GroupA
		GroupB
			dataset0
```

When we created GroupA, the HDF5 library created a group object and added a link named GroupA to the root object. When we created GroupB in GroupA, the HDF5 library created a group object and added a link named GroupB to the GroupB object. When we created the dataset0 object, the HDF5 library created a dataset object and added a link named dataset0 to the GroupB object. A path like /GroupA/GroupB/dataset0 specifies the links to follow to reach the dataset object which is unnamed.

So far we have discussed automatically-created links only. Now suppose that we want the dataset to appear at another location in the directed graph, for example, /Data/channel0, because some software that we use expects it to be there. We can create a Data group in root and then create there a hard link named channel0 that points to the dataset object. This extra manually-created hard link would be created using HDF5CreateLink. We wind up with this arrangement:


```igor
root
	GroupA
		GroupB
			dataset0
	Data
		channel0
```

We now still have just one dataset in the file but it is accessible using two different paths: /GroupA/GroupB/dataset0 and /Data/channel0. This is possible because datasets, like other objects, do not have names. Instead, paths contain the names of links leading to a dataset.

In addition to hard links, you can create soft links and external links.

The main difference between a hard link and a soft link is that a soft link can point to a non-existent object while a hard link cannot. When the last hard link pointing to an object is deleted, the object is no longer accessible in the file. When the last soft link pointing to an object is deleted, the object still exists.

An external link points to another HDF5 file and makes the contents of that file appear in the original file.

Using links you can create complex, confusing and nasty arrangements, such as circular references. In a circular reference, a group contains a link to its parent or other ancestor. Because of this complication, you should use links only when really necessary.

### *Parameters For Hard Links* {#parameters-for-hard-links}
A hard link is created if you use /HARD=1 or if you omit /HARD (but /EXT overrides /HARD).

*targetLocationID* is an HDF5 file ID or group ID.

*targetName* is a string containing the HDF5 path to the object to which a link is to be created. This can be a full HDF5 path or partial HDF5 path or simple name relative to *targetLocationID*.

*linkLocationID* is an HDF5 file ID or group ID.

*linkName* is a string containing the HDF5 path to the the link to be created and includes the name of the link. This can be a full HDF5 path or partial HDF5 path or simple name relative to *linkLocationID*.

For example:


```igor
// Create a hard link in /Data pointing to a dataset in /GroupA/GroupB.
// GroupA, GroupB and Data (also a group) are assumed to exist.
HDF5CreateLink /HARD=1 fileID, "/GroupA/GroupB/dataset0", fileID, "/Data/channel0"
```

Assuming that you have group IDs for GroupB and Data, you could use relative paths:


```igor
HDF5CreateLink /HARD=1 groupBID, "dataset0", dataID, "channel0"
```

### *Parameters For Soft Links* {#parameters-for-soft-links}
A soft link is created if you use /HARD=0.

*targetLocationID* is ignored when creating a soft link. Pass 0 for it.

*targetName* is a string containing the HDF5 path to the object to which a link is to be created. This can be a full HDF5 path or partial HDF5 path or simple name relative to *linkLocationID*.

*linkLocationID* is an HDF5 file ID or group ID.

*linkName* is a string containing the HDF5 path to the the link to be created and includes the name of the link. This can be a full HDF5 path or partial HDF5 path or simple name relative to *linkLocationID*.

For example:


```igor
// Create a soft link in /Data pointing to a dataset in /GroupA/GroupB.
// GroupA, GroupB and Data (also a group) are assumed to exist.
HDF5CreateLink /HARD=0 0, "/GroupA/GroupB/dataset0", fileID, "/Data/channel0"
```

Assuming that you have a group ID for Data, you could use a relative path for the link name:


```igor
HDF5CreateLink /HARD=0 0, "/GroupA/GroupB/dataset0", dataID, "channel0"
```

### *Parameters For External Links* {#parameters-for-external-links}
An external link is created if you use the /EXT flag. In this case /HARD is ignored and the link is always an external link.

*targetLocationID* is ignored when creating an external link. Pass 0 for it.

*targetName* is a string containing the HDF5 path to the object in the external file to which a link is to be created. This must be a full HDF5 path.

*linkLocationID* is an HDF5 file ID or group ID.

*linkName* is a string containing the HDF5 path to the the link to be created and includes the name of the link. This can be a full HDF5 path or partial HDF5 path or simple name relative to *linkLocationID*.

For example:


```igor
// Create an external link in /Data pointing to a dataset in /GroupA/GroupB in another file
HDF5CreateLink /EXT={"home","Test.h5"} 0, "/GroupA/GroupB/dataset0", fileID, "/Data/channel0"
```

Assuming that you have a group ID for Data, you could use a relative path for the link name:


```igor
HDF5CreateLink /EXT={"home","Test.h5"} 0, "/GroupA/GroupB/dataset0", dataID, "channel0"
```

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/EXT = {*pathName*, *filePath*}</span> |  |
|  | The link will be an external link. If /EXT is used, /HARD is ignored. |
|  | *pathName* is the name of an Igor symbolic path that specifies the directory to look in for the file specified by *filePath.* If *filePath* is a full path then you can pass "" for *pathName*. |
|  | *filePathStr* is a full path to the file or a relative path or simple name starting from the folder specified by *pathName*. |
| <span class="table-cell-nowrap">/HARD = *makeHardLink*</span> |  |
|  |<table class="nested-table"><tbody><tr><td>*makeHardLink*=1:</td><td>The link will be a hard link. This is the default if /HARD is omitted.</td></tr><tr><td>*makeHardLink*=0:</td><td>The link will be a soft link.</td></tr></tbody></table>
|  | If /EXT is used, /HARD is ignored. |
| <span class="table-cell-nowrap">/Q</span> | Be quiet. Suppresses normal diagnostic messages. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |

### *Details* {#details}
An object linked by HDF5CreateLink (or automatically linked by the HDF5 library) can be unlinked using HDF5UnlinkObject. If you remove the last hard link to an object, it is no longer accessible in the file.

### *Output Variables* {#output-variables}
HDFCreateLink sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero if the operation succeeds, non-zero if it fails. |

### *Example* {#example}

```igor
// This example assumes that a symbolic path named home exists.
// It creatse a file containing this arrangement of objects:
//		root
//			GroupA
//				GroupB
//					dataset0
//			Data
//					channel0	// Link to the dataset at /GroupA/GroupB/dataset0
Function DemoCreateHardLink()
	String fileName = "DemoCreateHardLink.h5"
	Variable fileID
	Variable result
	
	// Create the file with overwrite
	HDF5CreateFile /P=home /O fileID as fileName
	if (V_flag != 0)
		Beep
		Print "Error in DemoCreateHardLink"
		return -1
	endif

	// Create GroupA
	Variable groupAID
	HDF5CreateGroup /Q /Z fileID, "GroupA", groupAID
	if (V_flag != 0)
		Beep
		Print "DemoCreateHardLink error: Error creating GroupA"
		HDF5CloseFile fileID
		return -1
	endif

	// Create GroupB
	Variable groupBID
	HDF5CreateGroup /Q /Z groupAID, "GroupB", groupBID
	if (V_flag != 0)
		Beep
		Print "DemoCreateHardLink error: Error creating GroupA"
		HDF5CloseFile fileID
		return -1
	endif

	// Create dataset0 in /GroupA/GroupB
	Make/O/FREE wave0 = p
	HDF5SaveData /O /Q /IGOR=-1 wave0, groupBID, "dataset0"
	
	// Create group at /Data
	Variable DataID
	HDF5CreateGroup fileID, "/Data", DataID
	
	// Create link from /GroupA/GroupB/dataset0 to /Data/channel0
	HDF5CreateLink /HARD=1 fileID, "/GroupA/GroupB/dataset0", DataID, "channel0"
	
	String list, expectedList
	
	// Verify listing
	HDF5ListGroup /F /R=1 /TYPE=3 fileID, "/"
	list = S_HDF5ListGroup
	// Print list
	expectedList = "/Data;/Data/channel0;/GroupA;/GroupA/GroupB;/GroupA/GroupB/dataset0;"
	if (CmpStr(list,expectedList) != 0)
		Beep
		Printf "DemoCreateHardLink error: Expected \"%s\", got \"%s\"\r", expectedList, list
		HDF5CloseFile fileID
		return -1
	endif

	HDF5CloseFile fileID

	return 0
End
```

### *See Also* {#see-also}
[HDF5UnlinkObject](/igorpro/commands/hdf5unlinkobject.md)