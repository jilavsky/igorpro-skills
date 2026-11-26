---
description: "The UnzipFile operation unzips a file and saves the contents of the file in the specified output directory."
slug: /commands/unzipfile
---

<div className="command-signature">

## <strong>UnzipFile</strong>  [ /O[=<em>mode</em>] /PASS=<em>passwordStr</em> /PIN=<em>inputPathName</em> /POUT=<em>outputPathName</em> /Z[=<em>z</em>] ] <em>inputFileStr</em>, <em>outputFolderStr</em> {#unzipfile}

</div>

The UnzipFile operation unzips a file and saves the contents of the file in the specified output directory.

:::caution
If you specify /O=2 for an output directory that already exists, all previous contents of the directory are deleted.
:::

The UnzipFile operation was added in Igor Pro 9.00.

### *Input File Parameter* {#input-file-parameter}
*inputFileStr* specifies the zip file to unzip. The file name extension is not important but the file must be a zip file.

*inputFileStr* can be a full path to the file, in which case /PIN=*inputPathName* is not needed, a partial path relative to the directory associated with *inputPathName*, or the name of a file in the folder associated with *inputPathName*.

If you use a full or partial path for *inputFileStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

### *Output Folder Parameter* {#output-folder-parameter}
*outputFolderStr* specifies the directory into which the contents of the zip file will be extracted.

*outputFolderStr* can be a full path to the directory, in which case /POUT=*outputPathName* is not needed, a partial path relative to the directory associated with *outputPathName*, or an empty string in which case the directory specified by /POUT=*outputPathName* is used for the output directory.

If *outputFolderStr* is an empty string, the /POUT flag specifies the output directory.

If *outputFolderStr* is not an empty string, it must end with a directory name and not a path separator such as colon or backslash.

If you use a full or partial path for *outputFolderStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

If the output directory does not exist, it is created automatically.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/O[* = mode*]</span> | Controls whether the contents of the output directory are overwritten. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Does not overwrite. If the output directory exists and is not empty, the operation generates an error. This is the default behavior if you omit /O.</td></tr><tr><td>1:</td><td>Merges the contents of the zip file with the existing contents of the output directory. Any existing file with the same name as a file within the zip file is overwritten.</td></tr><tr><td></td><td>Unlike /O=2, the contents of the output directory and any subdirectories are not deleted. If the output directory already contains files whose names do not conflict with files in the zip file, those files remain untouched.</td></tr><tr><td></td><td>/O=1 is the same as /O.</td></tr><tr><td>2:</td><td>Deletes all contents of the output directory before extracting the contents of the zip file. Use this option if you want the contents of the output directory to exactly reflect the contents of the zip file.</td></tr></tbody></table>
|  | <div><Admonition type="caution"><p>If you specify /O=2 for an output directory that already exists, all previous contents of the directory are deleted.</p></Admonition></div> |
| <span class="table-cell-nowrap">/PASS = *passwordStr*</span> | Specifies the password for a password-protected zip file. Only the older ZipCrypto "encryption" algorithm is supported, not the newer and much more secure AES-256 algorithm. |
| <span class="table-cell-nowrap">/PIN = *inputPathName*</span> | Contributes to the specification of the input zip file to be extracted. *inputPathName* is the name of an existing symbolic path. See ***Input File Parameter*** above for details. |
| <span class="table-cell-nowrap">/POUT = *outputPathName*</span> | Contributes to the specification of the output directory into which the zip file's contents will be extracted. *outputPathName* is the name of an existing symbolic path. See ***Output Folder Parameter*** above for details. |
| <span class="table-cell-nowrap">/Z[ = *z*]</span> | Suppress error generation. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Do not suppress errors. If an error occurs, Igor aborts procedure execution. This is the default behavior if you omit /Z.</td></tr><tr><td>/Z=1:</td><td>Suppress errors. Errors do not abort procedure execution. Check the V_Flag output variable to see if an error occurred.</td></tr></tbody></table>
|  | /Z alone has the same effect as /Z=1. |

### *Output Variables* {#output-variables}
UnzipFile sets the following output variables:

|  |  |
| --- | --- |
| V_flag | V_flag is set to zero if the operation succeeds or to a non-zero Igor error code if it fails. You can use V_flag along with the /Z flag to handle errors and prevent them from halting procedure execution. |
| S_outputFullPath | A string containing the full path to the output directory. If the operation fails, S_outputFullPath is set to "". |

### *Limitations* {#limitations}
File and directory names within a zip file that contain non-ASCII characters may not have the correct names after unzipping.

The created and modified timestamps of a file are reconstructed with limited range and precision. Some zip files store these timestamps in an alternative format that allows for greater precision and range, but the current unzip algorithm does not support this newer format.

### *Examples* {#examples}

```igor
// Unzip a file using full paths
String zipFileString = "C:Users:Fred:Documents:Test.zip"
String outputPathString = "C:Users:Fred:Documents:Extracted"
UnzipFile zipFileString, outputPathString

// Unzip a file using symbolic paths
String zipFileName = "Test.zip"
String outputFolderName = ""	// Unzip to folder specified by /POUT
UnzipFile/PIN=home/POUT=home zipFileName, outputFolderName
```