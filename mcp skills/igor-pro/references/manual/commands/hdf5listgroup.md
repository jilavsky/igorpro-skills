---
description: "The HDF5ListGroup operation returns a list of the names of objects in the HDF5 file or group specified by locationID and nameStr."
slug: /commands/hdf5listgroup
---

<div className="command-signature">

## <strong>HDF5ListGroup</strong>  [ /CONT=<em>continue</em> /ERR=<em>errorFlags</em> /F /R[=<em>mode</em> ] /ORDR=<em>order</em> /SEP=<em>separatorStr</em> /TYPE=<em>typeMask</em> /Z ] <em>locationID</em>, <em>nameStr</em> {#hdf5listgroup}

</div>

The HDF5ListGroup operation returns a list of the names of objects in the HDF5 file or group specified by *locationID* and *nameStr*. The information is returned in the string variable S_HDF5ListGroup. By default the list is semicolon-separated.

The type or types of objects listed is controlled by the /TYPE flag.

### *Parameters* {#parameters}
*locationID* is an HDF5 file ID number obtained from [HDF5CreateFile](/igorpro/commands/hdf5createfile.md) or [HDF5OpenFile](/igorpro/commands/hdf5openfile.md) or an HDF5 group ID obtained from [HDF5CreateGroup](/igorpro/commands/hdf5creategroup.md) or [HDF5OpenGroup](/igorpro/commands/hdf5opengroup.md). If *locationID* is invalid an error is returned.

*nameStr* is a string containing the HDF5 path to the group of interest.

For example, to determine what objects exist in at the root level of the file, you would pass the HDF5 file ID as the *locationID* parameter and "/" as the *nameStr* parameter.

To determine what objects exist in the group "/images", you could pass the HDF5 file ID as the *locationID* parameter and "/images" as the *nameStr* parameter or you could pass an HDF5 group ID obtained from HDF5CreateGroup or HDF5OpenGroup as the *locationID* parameter and "." as the *nameStr* parameter.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/CONT = *continue*</span> | /CONT controls whether iteration continues if an error occurs while listing the contents of a group, for example, if the group contains a link to a non-existent group or dataset. |
|  | *continue*=0:   Iteration stops (default) |
|  | *continue*=1:   Iteration continues |
|  | The /CONT flag was added in Igor Pro 9.00 mainly for use by the HDF5 Browser. Most HDF5 users will not need it. |
|  | See ***HDF5ListGroup Error Handling*** below for further information. |
| <span class="table-cell-nowrap">/ERR = *errorFlags*</span> | /ERR controls error handling while listing the contents the group specified by *locationID* and *nameStr*, for example, if the group contains a link to a non-existent group or dataset. |
|  | The /ERR flag was added in Igor Pro 9.00 mainly for use by the HDF5 Browser. Most HDF5 users will not need it. |
|  | *errorFlags* is a bitwise parameter defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Report errors.</td></tr></tbody></table>
|  | If bit 0 is set, errors are reported to the history area and recorded for retrieval by HDF5DumpErrors. |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;1:</td><td>Treat missing objects as errors.</td></tr></tbody></table>
|  | For backward compatibility, *errorFlags* defaults to 1 if /Z is omitted and to 0 if /Z is present. |
|  | See ***HDF5ListGroup Error Handling*** below for further information. |
| <span class="table-cell-nowrap">/F</span> | Use full paths in the returned list of object names. If omitted, paths relative to *locationID* and *nameStr* are returned. |
| <span class="table-cell-nowrap">/ORDR = *order*</span> | Controls the order of listing of objects. |
|  |<table class="nested-table"><tbody><tr><td>*order*&nbsp;=0:</td><td>List objects in alphabetic order. This is the default if you omit /ORDR.</td></tr><tr><td>*order*&nbsp;=1:</td><td>List objects in creation order if possible or using alphabetic order otherwise.</td></tr></tbody></table>
|  | In order to list objects in creation order, the objects' group must include creation-order information. Most HDF5 files do not include creation-order information. However, HDF5 files written by Igor Pro 9 or later include creation-order information and so are listed in creation order if you use /ORDR=1. |
|  | /ORDR was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/R[ = *mode* ]</span> | Controls recursion of the HDF5ListGroup operation. |
|  |<table class="nested-table"><tbody><tr><td>*mode*&nbsp;=0:</td><td>Not recursive. This is the default if you omit /R.</td></tr><tr><td>*mode*&nbsp;=1:</td><td>Recursive. Do not list the same group more than once. Same as /R by itself.</td></tr><tr><td>*mode*&nbsp;=2:</td><td>Recursive. OK to list the same group more than once.</td></tr></tbody></table>
|  | To get a result that can be meaningfully interpreted /F must be used with /R. |
|  | Because of the way the HDF5 library iterators (H5Giterate and H5Lvisit) work, when using /R the order of the items returned may not be what you expect. |
|  | See ***HDF5ListGroup Recursion Modes*** below for further information. |
| <span class="table-cell-nowrap">/SEP = *separatorStr*</span> |  |
|  | *separatorStr* is a one-byte string that specifies the list separator to use for S_HDF5ListGroup. If you omit /SEP, the separator is semicolon. See ***HDF5ListGroup Separator*** below for details. The /SEP flag was added in Igor Pro 9.00. |
| <span class="table-cell-nowrap">/TYPE = *typeMask*</span> | *typeMask* is a bitwise parameter that specifies which types of objects to list, as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Lists groups</td></tr><tr><td>Bit&nbsp;1:</td><td>Lists datasets (default)</td></tr><tr><td>Bit&nbsp;2:</td><td>Lists named datatypes</td></tr><tr><td>Bit&nbsp;3:</td><td>Lists links</td></tr></tbody></table>
|  | All other bits are reserved and must be set to zero. |
|  | If /TYPE is omitted, HDF5ListGroup lists datasets only. |
|  | See [Setting Bit Parameters](/igorpro/programming/commands.md#setting-bit-parameters) for details about bit settings. |
| <span class="table-cell-nowrap">/Z</span> | Suppress error generation. Use this if you want to handle errors yourself. |
|  | If you omit /ERR, then /Z has two effects: |
|  |<table class="nested-table"><tbody><tr><td>1.</td><td>It suppresses reporting of errors via the history area and recording of errors for retrieval using HDF5DumpErrors</td></tr><tr><td>2.</td><td>It causes HDF5ListGroup to return no errors to Igor even if errors occur</td></tr></tbody></table>
|  | If you include /ERR then /ERR controls the first of these effects and /Z controls only the second. |
|  | See ***HDF5ListGroup Error Handling*** below for further information. |

### *Output Variables* {#output-variables}
HDF5ListGroup sets the following output variables:


|  |  |
| --- | --- |
| V_Flag | Set to zero no errors occurred or to a non-zero error code. |
|  | See ***HDF5ListGroup Error Handling*** below for further information. |
| S_HDF5ListGroup | Set to a list of object names or paths. By default the list separator is semicolon. See ***HDF5ListGroup Separator*** below for details. |

### *HDF5ListGroup Separator* {#hdf5listgroup-separator}
By default, S_HDF5ListGroup is semicolon-separated. This is fine except for the very rare case where an HDF5 object name includes a semicolon character. If you want to handle that very rare case, you can use /SEP="\r" to specify carriage-return as the list separator. The /SEP flag requires Igor Pro 9.00 or later.

### *HDF5ListGroup Recursion Modes* {#hdf5listgroup-recursion-modes}
If you use /R, /R=1 (same as /R) or /R=2, HDF5ListGroup lists the group specified by *locationID* and *nameStr* and any subgroups. Consider this arrangement:


```igor
root
	GroupA
		dataset0
		GroupB
```

This example shows the output from HDF5ListGroup using full paths (/F):


```igor
HDF5ListGroup /F /R=1 /TYPE=3 fileID, "/"
	/GroupA;/GroupA/GroupB;/GroupA/dataset0;
```

Without /F we get paths relative to the target group (/ in this case):


```igor
HDF5ListGroup /R=1 /TYPE=3 fileID, "/"
	GroupA;GroupA/GroupB;GroupA/dataset0;
```

If you are recursively listing groups on your own (without /R) you need to be aware of a potential problem. In HDF5, it is possible to create circular references which will cause infinite recursion unless you are very careful. See the next section for further explanation.

### *HDF5ListGroup and Non-Hierarchical File Arrangements* {#hdf5listgroup-and-non-hierarchical-file-arrangements}
This section deals with HDF5 file organizations that are not hierarchical. This advanced material is of interest only in relatively rare cases and can be skipped for most purposes.

In an HDF5 file, a given group can appear more than once because HDF5 files are "directed graphs", not strict hierarchies. This is explained in the HDF5 User Guide chapter on groups.

As the HDF5 User Guide explains, HDF5 objects do not have names - links have names. This is a confusing concept with subtle ramifications. As a result, HDF5ListGroup does not really list objects - it lists links to objects. This distinction becomes visible only for non-hierarchical files.

When an HDF5 group or dataset is created, a hard link to it is automatically created in its parent group. This type of object creation results in a hierarchy - a tree structure in which there is just one path to any given object.

To create a non-hierarchical file, in which there is more than one path to one or more objects, you need to add a hard or soft link to a group. (Soft links are similar to hard links but can point to non-existent objects.) Most files do not have such links.

If we add to the preceding example a hard link named LinkToGroupA in root pointing to GroupA, we arrive at this arrangement:


```igor
/ (root)
	GroupA
		dataset0
		GroupB
	LinkToGroupA
```

GroupA now appears twice in the directed graph: once at location "/GroupA" and again at location "/LinkToGroupA".

HDF5ListGroup/R=1 on root lists LinkToGroupA but does not recurse into it because it points to a group that was already listed:


```igor
HDF5ListGroup /F /R=1 /TYPE=3 fileID, "/"
/GroupA;/GroupA/GroupB;/GroupA/dataset0;/LinkToGroupA;
```

HDF5ListGroup/R=2 on root lists LinkToGroupA and and also recurses into it, thereby listing its contents:


```igor
HDF5ListGroup /F /R=2 /TYPE=3 fileID, "/"
/GroupA;/GroupA/GroupB;/GroupA/dataset0;/LinkToGroupA;/LinkToGroupA/GroupB;/LinkToGroupA/dataset0;
```

With /R=2, the contents of the group that contains GroupB and dataset0 is listed twice: as "/GroupA/..." and as "/LinkToGroupA/...".

### *HDF5ListGroup and Circular References* {#hdf5listgroup-and-circular-references}
It is possible to add a hard or soft link to a group such that the link points to the group itself or to its ancestor. This creates a circular reference. Most HDF5 files do not have circular references.

If we add to the original example a hard link named LinkToGroupA in GroupB pointing to GroupA, we arrive at this arrangement:


```igor
/ (root)
	GroupA
		dataset0
		GroupB
			LinkToGroupA
```

Since GroupA is an ancestor of LinkToGroupA, the added link creates a circular reference. If this reference were followed, it would create infinite recursion.

HDF5ListGroup/R=1 does not infinitely recurse because it does not list the contents of a given group more than once. HDF5ListGroup/R=2 does not infinitely recurse because it detects circularity and stops recursing.

### *HDF5ListGroup Error Handling* {#hdf5listgroup-error-handling}
In the event of an error, there are some behaviors that you control via the use of /Z, /CONT, and /ERR. /CONT and /ERR were added in Igor Pro 9.00.

The behaviors that you control are:

1. Whether errors are reported in the history area and recorded for retrieval using HDF5DumpErrors
2. Whether errors are returned to Igor
3. Whether a link to a missing object is treated as an error
4. Whether iteration of the objects in the group specified by *locationID* and *nameStr* stops or continues if an error occurs

Prior to Igor Pro 9.00, the /Z flag allowed you to control behaviors 1 and 2. If /Z was omitted, errors were reported and returned to Igor. If /Z was present, errors were not reported and not returned to Igor in which case you used V_Flag to determine if an error occurred. Links to missing objects were never treated as errors.

To provide more flexibility, mainly for the benefit of the HDF5 Browser, Igor Pro 9.00 added the /CONT and /ERR flags. For backward compatibility, if you omit /CONT and /ERR, you get the same behavior as earlier versions of Igor.

If you include the /ERR flag then it controls whether errors are reported and whether a link to a missing object is treated as an error. /Z still controls whether errors are returned to Igor.

The /CONT flag allows you to control whether iteration continues if an error occurs. The main reason for continuing is that some files contain links to external files which may be missing. Without /CONT or with /CONT=0, HDF5ListGroup stops when it encounters such a link. With /CONT=1, it continues to iterate over the other links in the group.

/CONT is not foolproof. There may be some kinds of errors that prevent continuing to list objects despite the use of /CONT=1.

The V_Flag output variable is set to a non-zero value if an error occurred. This is true regardless of what flags you use so you can always test V_Flag to see if an error occurred. With /CONT=1, V_Flag reflects the first error that occurred.