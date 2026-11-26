---
description: "The FTPDelete operation deletes a file or a directory from an FTP server on the Internet."
slug: /commands/ftpdelete
---

<div className="command-signature">

## <strong>FTPDelete</strong>  [ /D /N=<em>portNumber</em> /U=<em>userNameStr</em> /V=<em>diagnosticMode</em> /W=<em>passwordStr</em> /Z ] <em>urlStr</em> {#ftpdelete}

</div>

The FTPDelete operation deletes a file or a directory from an FTP server on the Internet.

:::caution
If you delete a directory on an FTP server, all contents of that directory and any subdirectories are also deleted.
:::

For background information on Igor's FTP capabilities and other important details, see [File Transfer Protocol (FTP)](/igorpro/advanced-topics.md#file-transfer-protocol-ftp).

FTPDelete sets V_flag to zero if the operation succeeds and to nonzero if it fails. This, in conjunction with the /Z flag, can be used to allow procedures to continue to execute if an FTP error occurs.

### *Parameters* {#parameters}
*urlStr* specifies the file or directory to delete. It consists of a naming scheme (always "ftp://"), a computer name (e.g., "ftp.wavemetrics.com" or "38.170.234.2"), and a path (e.g., "/test/TestFile1.txt"). For example: "ftp://ftp.wavemetrics.com/test/TestFile1.txt"

*urlStr* must always end with a file name if you are deleting a file or with a directory name if you are deleting a directory. In the case of a directory, *urlStr* must not end with a slash.

To indicate that *urlStr* contains an absolute path, insert an extra '/' character between the computer name and the path. For example:

```igor
"ftp://ftp.wavemetrics.com//pub/test"
```

If you do not specify that the path in *urlStr*  is absolute, it is interpreted as relative to the FTP user's base directory. Since pub is the base directory for an anonymous user at wavemetrics.com, these URLs reference the same directory for an anonymous user:

```igor
"ftp://ftp.wavemetrics.com//pub/test"
"ftp://ftp.wavemetrics.com/test"
```

Special characters such as punctuation that are used in *urlStr*  may be incorrectly interpreted by the operation. If you get unexpected results and *urlStr* contains such characters, you can try percent-encoding the special characters. See [Percent Encoding](/igorpro/advanced-topics.md#percent-encoding) for additional information.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/D</span> | Deletes a complete directory and all its contents. Omit /D if you are deleting a file. |
| <span class="table-cell-nowrap">/N = *portNumber*</span> | Specifies the server's TCP/IP port number to use (default is 21). In almost all cases, the default will be correct so you won't need to use the /N flag. |
| <span class="table-cell-nowrap">/U = *userNameStr*</span> | Specifies the user name to be used when logging in to the FTP server. If /U is omitted or if *userNameStr* is "", the login is done as an anonymous user. Use /U if you have an account on the FTP server. |
| <span class="table-cell-nowrap">/V = *diagnosticMode*</span> | Determines what kind of diagnostic messages FTPDelete will display in the history area. *diagnosticMode* is a bitwise parameter, with the bits defined as follows: |
|  |<table class="nested-table"><tbody><tr><td>Bit&nbsp;0:</td><td>Show basic diagnostics. Currently this just displays the URL in the history.</td></tr><tr><td>Bit&nbsp;1:</td><td>Show errors. This displays additional information when errors occur.</td></tr><tr><td>Bit&nbsp;2:</td><td>Show status. This displays commands sent to the server and the server&#39;s response.</td></tr></tbody></table>
|  | The default value for *diagnosticMode*  is 3 (show basic and error diagnostics). If you are having difficulties, you can try using 7 to show the commands sent to the server and the server's response. |
|  | See [FTP Troubleshooting](/igorpro/advanced-topics.md#ftp-troubleshooting) for other troubleshooting tips. |
| <span class="table-cell-nowrap">/W = *passwordStr*</span> | Specifies the password to be used when logging in to the FTP server. Use /W if you have an account on the FTP server. |
|  | If /W is omitted, the login is done using a default password that will work with most anonymous FTP servers. |
|  | <div><Admonition type="note"><p>See [Safe Handling of Passwords](/igorpro/advanced-topics.md#safe-handling-of-passwords) for information on handling sensitive passwords.</p></Admonition></div> |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal. Will not abort procedure execution if an error occurs. |
|  | Your procedure can inspect the V_flag variable to see if the transfer succeeded. V_flag will be zero if it succeeded, or a nonzero value if an error occurred. |

### *Examples* {#examples}

```igor
// Delete a file.
String url = "ftp://ftp.wavemetrics.com/test/TestFile1.txt"
FTPDelete url

// Delete a directory.
String url = "ftp://ftp.wavemetrics.com/test/TestDir1"
FTPDelete/D url
```

### *See Also* {#see-also}
[File Transfer Protocol (FTP)](/igorpro/advanced-topics.md#file-transfer-protocol-ftp)

[FTPCreateDirectory](/igorpro/commands/ftpcreatedirectory.md), [FTPDownload](/igorpro/commands/ftpdownload.md), [FTPUpload](/igorpro/commands/ftpupload.md), [URLEncode](/igorpro/commands/urlencode.md)