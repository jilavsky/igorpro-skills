---
description: "The FTPDownload operation downloads a file or a directory from an FTP server on the Internet."
slug: /commands/ftpdownload
---

<div className="command-signature">

## <strong>FTPDownload</strong>  [ /D /I/M=<em>messageStr</em> /N=<em>portNumber</em> /O[=<em>mode</em>]/P=<em>pathName</em> /S=<em>showProgress</em> /T=<em>transferType</em> /U=<em>userNameStr</em> /V=<em>diagnosticMode</em> /W=<em>passwordStr</em> /Z ] <em>urlStr</em>, <em>localPathStr</em> {#ftpdownload}

</div>

The FTPDownload operation downloads a file or a directory from an FTP server on the Internet.

:::caution
When you download a file or directory using the path and name of a file or directory that already exists on your local hard disk, all previous contents of the local file or directory are obliterated.
:::

For background information on Igor's FTP capabilities and other important details, see [File Transfer Protocol (FTP)](/igorpro/advanced-topics.md#file-transfer-protocol-ftp).

FTPDownload sets a variable named V_flag to zero if the operation succeeds and to nonzero if it fails. This, in conjunction with the /Z flag, can be used to allow procedures to continue to execute if a FTP error occurs.

If the operation succeeds, FTPDownload sets a string named S_Filename to the full file path of the downloaded file or, if the /D flag was used, the full path to the base directory that was downloaded. This is useful in conjunction with the /I flag.

If the operation fails, S_Filename is set to "".

### *Parameters* {#parameters}
*urlStr* specifies the file or directory to download. It consists of a naming scheme (always "ftp://"), a computer name (e.g., "ftp.wavemetrics.com" or "38.170.234.2"), and a path (e.g., "/Test/TestFile1.txt"). For example: "ftp://ftp.wavemetrics.com/pub/test/TestFile1.txt"

*urlStr* must always end with a file name if you are downloading a file or with a directory name if you are downloading a directory. In the case of a directory, *urlStr* must not end with a slash.

To indicate that *urlStr* contains an absolute path, insert an extra '/' character between the computer name and the path. For example:


```igor
"ftp://ftp.wavemetrics.com//pub/test"
```

If you do not specify that the path in *urlStr* is an absolute path, it is interpreted as a path relative to the FTP user's base directory. Since pub is the base directory for an anonymous user, this URL references the same directory:


```igor
"ftp://ftp.wavemetrics.com/test"
```

Special characters such as punctuation that are used in *urlStr*  may be incorrectly interpreted by the operation. If you get unexpected results and *urlStr* contains such characters, you can try percent-encoding the special characters. See [Percent Encoding](/igorpro/advanced-topics.md#percent-encoding) for additional information.

*localPathStr* and *pathName* specify the name to use for the file or directory that will be created on your hard disk. If you use a full or partial path for *localPathStr*, see [Path Separators](/igorpro/user-interface/platform-related-issues.md#path-separators) for details on forming the path.

*localPathStr* must always end with a file name if you are downloading a file or with a directory name if you are downloading a directory. In the case of a directory, *localPathStr* must not end with a colon or backslash.

FTPDownload displays a dialog through which you can identify the local file or directory in the following cases:

1.	You have used the /I (interactive) flag.
2.	You did not completely specify the location of the local file or directory via *pathName* and *localPathStr*.
3.	There is an error in *localPathStr*. This can be either a syntactical error or a reference to a nonexistent file or directory
4.	The specified local file or directory exists and you have not used the /O (overwrite) flag.

See Examples below for examples of constructing a URL and local path.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Downloads a complete directory. Omit it if you are downloading a file. |
| <span class="table-cell-nowrap">/I</span> | Interactive mode which will prompt you to specify the name and location of the file or directory to be created on the local hard disk. |
| <span class="table-cell-nowrap">/M = *messageStr*</span> | Specifies the prompt message used in the dialog in which you specify the name and location of the file or directory to be created. |
| <span class="table-cell-nowrap">/N = *portNumber*</span> | Specifies the server's TCP/IP port number to use (default is 21). In almost all cases, this will be correct so you won't need to use the /N flag. |
| <span class="table-cell-nowrap">/O[* = mode*]</span> | Controls whether a local file or directory whose name is in conflict with the file or directory being downloaded is overwritten without prompting the user. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Prompts the user to allow the overwrite. This is the default behavior if /O is omitted.</td></tr><tr><td>1:</td><td>Overwrites without prompting the user. If the /D flag is also used, all contents of the destination directory are deleted if it already exists. /O=1 is the same as /O.</td></tr><tr><td>2:</td><td>Merges files and subdirectories downloaded with the contents of the destination directory. Unlike /O=1, the contents of the destination directory are not deleted, however files and directories downloaded from the server will overwrite existing files and directories of the same name. When downloading a file this mode is accepted but has the same effect as /O=1.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/P = *pathName*</span> | Contributes to the specification of the file or directory to be created on your hard disk. *pathName*  is the name of an existing symbolic path. See examples below. |
| <span class="table-cell-nowrap">/S = *showProgress*</span> | Displays a progress dialog. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>No progress dialog.</td></tr><tr><td>1:</td><td>Show a progress dialog (default).</td></tr></tbody></table>
| <span class="table-cell-nowrap">/T = *transferType*</span> | Controls the FTP transfer type. |
|  |<table class="nested-table"><tbody><tr><td>0:</td><td>Image (binary) transfer (default).</td></tr><tr><td>1:</td><td>ASCII transfer.</td></tr></tbody></table>
|  | See [FTP Transfer Types](/igorpro/advanced-topics.md#ftp-transfer-types) for more discussion. |
| <span class="table-cell-nowrap">/U = *userNameStr*</span> | Specifies the user name to be used when logging in to the FTP server. If this flag is omitted or if *userNameStr* is "", the login is done as an anonymous user. Use this flag if you have an account on the FTP server. |
| <span class="table-cell-nowrap">/V = *diagnosticMode*</span> | Determines what kind of diagnostic messages FTPDownload will display in the history area. *diagnosticMode* is a bitwise parameter, with the bits defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Show basic diagnostics. Currently, this displays the URL and the local path in the history.</td></tr><tr><td>Bit&nbsp;1:</td><td>Show errors. This displays additional information when errors occur.</td></tr><tr><td>Bit&nbsp;2:</td><td>Show status. This displays commands sent to the server and the server&#39;s response.</td></tr></tbody></table>
|  | The default value for this parameter is 3 (show basic and error diagnostics). If you are having difficulties, you can try using 7 to show the commands sent to the server and the server's response. |
|  | See [FTP Troubleshooting](/igorpro/advanced-topics.md#ftp-troubleshooting) for other troubleshooting tips. |
| <span class="table-cell-nowrap">/W = *passwordStr*</span> | Specifies the password to be used when logging in to the FTP server. Use this flag if you have an account on the FTP server. |
|  | If this flag is omitted, the login is done using the password "nopassword". This will work with most anonymous FTP servers. Some anonymous FTP servers request that you use your email address as a password. You can do this by including the /W="\<your email address\>" flag. |
|  | If /W is omitted, the login is done using a default password that will work with most anonymous FTP servers. |
|  | <div><Admonition type="note"><p>See [Safe Handling of Passwords](/igorpro/advanced-topics.md#safe-handling-of-passwords) for information on handling sensitive passwords.</p></Admonition></div> |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal. Will not abort procedure execution if an error occurs. |
|  | Your procedure can inspect the V_flag variable to see if the transfer succeeded. V_flag will be zero if it succeeded, -1 if the user canceled in an interactive dialog, or another nonzero value if an error occurred. |

### *Examples* {#examples}

```igor
//	Download a file using a full local path.
String url = "ftp://ftp.wavemetrics.com/pub/test/TestFile1.txt"
String localPath = "hd:Test Folder:TestFile1.txt"
FTPDownload url, localPath

//	Download a file using a local symbolic path and file name.
String url = "ftp://ftp.wavemetrics.com/pub/test/TestFile1.txt"
String pathName = "Igor"	// Igor is the name of a symbolic path.
String fileName = "TestFile1.txt"
FTPDownload/P=$pathName url, fileName

//	Download a directory using a full local path.
String url = "ftp://ftp.wavemetrics.com/pub/test/TestDir1"
String localPath = "hd:Test Folder:TestDir1"
FTPDownload/D url, localPath
```

### *See Also* {#see-also}
[File Transfer Protocol (FTP)](/igorpro/advanced-topics.md#file-transfer-protocol-ftp)

[FTPCreateDirectory](/igorpro/commands/ftpcreatedirectory.md), [FTPDelete](/igorpro/commands/ftpdelete.md), [FTPUpload](/igorpro/commands/ftpupload.md), [URLEncode](/igorpro/commands/urlencode.md), [FetchURL](/igorpro/commands/fetchurl.md)