---
description: "The URLRequest operation connects to a URL using the specified method and optionally stores the response from the server."
slug: /commands/urlrequest
---

<div className="command-signature">

## <strong>URLRequest</strong>  [ <em>flags</em> ] <em>url</em>=<em>urlStr</em> [<em>method</em>=<em>methodName</em>, <em>headers</em>=<em>headersStr</em>] {#urlrequest}

</div>

The URLRequest operation connects to a URL using the specified method and optionally stores the response from the server. *urlStr* can point to a remote server or to a local file. The server's response is stored in the S_serverResponse output variable or in a file if you use the /FILE flag.

The URLRequest operation was added in Igor Pro 7.00.

### *Keywords* {#keywords}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">The url = *urlStr* keyword is required. All others are optional.</span> |  |
| <span class="table-cell-nowrap">url = *urlStr*</span> | A string containing the URL to retrieve. See [URLs](/igorpro/advanced-topics.md#urls) for details. |
| <span class="table-cell-nowrap">method = *methodName*</span> | Specifies which method to use for the request. The get method is used by default. |
|  | This table shows the valid methods for each supported scheme. Not all servers support all of the listed methods. |
|  |<table class="nested-table"><tbody><tr><td>**Scheme**</td><td>**Supported Methods**</td></tr><tr><td>http,&nbsp;https</td><td>get, post, put, head, delete</td></tr><tr><td>ftp</td><td>get, put</td></tr><tr><td>file</td><td>get, put</td></tr></tbody></table>
|  | Because *methodName* is a name, not a string, you must not enclose it in quotes. |
|  | Before using the post method, you should read ***The HTTP Post Method*** below so that you know how to use the optional headers parameter. |
|  | If you use the head method, URLRequest sets the S_serverResponse output variable to "" because only the headers are retrieved. As with other methods, the headers are stored in the S_headers output variable. |
| <span class="table-cell-nowrap">headers = *headersStr*</span> | Specifies a string containing additional or replacement headers to use with the request. This parameter is ignored unless the scheme is http or https. |
|  | The headers parameter is provided primarily for use with the post method when making HTTP requests and is ignored for schemes other than http/https. The header consists of a colon-separated key:value pair (though see the next paragraph for an exception). Pairs must be separated by a carriage return (\\r) character. |
|  | Certain standard headers (such as Content-Type and User-Agent) may automatically be set when making the request. You can override those default values by using this keyword and setting a different value. If you add a header with no content, as in "Accept:" (there is no data on the right side of the colon), the internally used header is disabled. To actually add a header with no content, use the form "MyHeader;" (note the trailing semicolon). |
|  | Any headers specified with this keyword are sent only to the http server, not to the proxy server, if one is in use. |
|  | See ***The HTTP Post Method*** below for a detailed explanation and examples. |

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/AUTH = {*username*, *password*}</span> |  |
|  | Uses the specified *username* and *password* string parameters for authentication. Values provided here override any username and/or password provided as part of the URL. To specify a username but not a password, pass "" for the *password* parameter. |
|  | <div><Admonition type="note"><p>See [Safe Handling of Passwords](/igorpro/advanced-topics.md#safe-handling-of-passwords) for more information on how to use URLRequest to prevent authentication information, such as passwords, from being accidentally revealed.</p></Admonition></div> |
| <span class="table-cell-nowrap">/DFIL = *dataFileNameStr*</span> | Specifies a file name to use as a source of data. Typically this flag is used only with the put or post methods, but it is accepted with all methods. Unless *dataFileNameStr* is a full path, the /P flag must also be used. When using the post or put methods, one and only one of the /DFIL or /DSTR flags must be used. |
|  | When you use /DFIL and the method is anything other than put, the "Content-Type: application/x-www-form-urlencoded" header is automatically added. If necessary, you can override this behavior using the headers keyword. See ***The HTTP Post Method*** below for more information. |
| <span class="table-cell-nowrap">/DSTR = *dataStr*</span> | Specifies the string to use as a source of data. Typically you use this flag only with the put or post methods, but it is accepted with all methods. When using the post or put methods, one and only one of the /DFIL or /DSTR flags must be used. |
|  | When /DSTR is used and the method is anything other than put, the "Content-Type: application/x-www-form-urlencoded" header is automatically added. If necessary, you can override this behavior using the headers keyword. See **The HTTP Post Method** below for more information. |
| <span class="table-cell-nowrap">/FILE = *destFileNameStr*</span> | If present, URLRequest saves the server's response in a file instead of in the S_serverResponse output variable. |
|  | URLRequest ignores /FILE if you include the /IGN flag and the *ignoreResponse* parameter is not 0. |
|  | *destFileNameStr* can be a full path to the file, in which case /P=*pathName* is not needed, a partial path relative to the folder associated with *pathName*, or the name of a file in the folder associated with *pathName*. If the file already exists, URLRequest returns an error unless you include the /O flag. |
|  | If you include /O and the file already exists, the existing file is overwritten. This happens even in the event of an empty response or transfer error. |
|  | You should consider using the /FILE flag when you are expecting the server to return a large amount of data, such as when downloading a file. |
| <span class="table-cell-nowrap">/IGN[ = *ignoreResponse*]</span> | Ignore and do not store the server's response to the request. /IGN alone has the same effect as /IGN=1. |
|  | If ignore is turned on, URLRequest sets the S_serverResponse output variable to "", regardless of whether the server responded to the request or not. If you include the /FILE flag, URLRequest does not create the output file and sets S_fileName is set to "". |
|  | This flag is useful only when your goal is to establish a connection with a server and the server's response is not important. All error message codes and strings are still set when ignore is on. |
|  |<table class="nested-table"><tbody><tr><td>/IGN=0:</td><td>Same as no /IGN.</td></tr><tr><td>/IGN=1:</td><td>Ignore server response completely. S_headers is set to &quot;&quot;.</td></tr><tr><td>/IGN=2:</td><td>Ignore server response but capture the headers of the response. S_serverResponse is set to &quot;&quot; but S_headers will contain the headers.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/NRED = *maxNumRedirects*</span> |  |
|  | Specifies the maximum number of redirects that are allowed. A redirect means that when a certain URL is requested, the server responds telling the client to try a different URL. Most web browsers automatically follow server redirects, up to a certain limit. For security purposes, it is sometimes useful to prevent redirects from being followed at all. |
|  | *maxNumRedirects* is a number between -1 and 1000. To allow infinite redirection, set *maxNumRedirects* to -1. If you omit the /NRED flag, a moderate value (currently 20, but subject to change in the future) is used. |
| <span class="table-cell-nowrap">/O</span> | Specifies that the file is to be overwritten when you use the /FILE flag and the output file already exists. If you omit /O and the file exists, URLRequest returns an error. |
| <span class="table-cell-nowrap">/P = *pathName*</span> | Specifies the folder to use for the output file, specified by the /FILE flag, and/or the source data file, specified by the /DFIL flag. *pathName* is the name of an existing Igor symbolic path. |
|  | The /P flag affects both the /FILE and /DFIL flags. If you use both flags and want to use different directories, you must provide a full path for one or both of the /FILE and /DFIL flag parameters. |
|  | If the /P flag is used without one or both of the /FILE and /DFIL flags, it is ignored. |
| <span class="table-cell-nowrap">/PROX[ = {*proxyURLStr*, *proxyUserNameStr*, *proxyPassStr*, *proxyOptions*}]</span> |  |
|  | <div><Admonition type="warning"><p>This flag is experimental and has not been extensively tested. The behavior of this flag may change in the future, or it may be eliminated entirely.</p></Admonition></div> |
|  | Designates a proxy server to be used when making the connection. *proxyURLStr* is either the host name or IP address of the proxy server, or a full URL. If a full URL is used, the scheme specifies which kind of proxy is used. Typically the scheme for a proxy server should be either http or socks5. If no scheme is provided, http is assumed. See [URLs](/igorpro/advanced-topics.md#urls) for more information. |
|  | If the proxy server does not require authentication, or if the username and password for the proxy server are specified in *proxyURLStr*, the optional *proxyUserNameStr* and *proxyPassStr* parameters do not need to be provided. The following two examples do the same thing: <br>`/PROX={"http://proxy.example.com:800"}` <br>`/PROX={"http://proxy.example.com:800", "", ""}` |
|  | As with other URLs, you can also provide the username and password as part of the URL itself. The following two examples do the same thing: <br>`/PROX={"http://proxy.example.com:800", "user", "pass"}` <br>`/PROX={"http://user:pass@proxy.example.com:800"}` |
|  | *proxyOptions* is optional and for future use. It is currently ignored. If provided, you must set it to 0. |
|  | If you use the /PROX flag without any parameters, Igor attempts to get proxy information from the operating system's proxy configuration information. If Igor cannot get any proxy server information from the system, no proxy server is used. |
|  | See [Safe Handling of Passwords](/igorpro/advanced-topics.md#safe-handling-of-passwords) for more information on how to use URLRequest to prevent authentication information, such as passwords, from being accidentally revealed. |
| <span class="table-cell-nowrap">/TIME = *timeoutSeconds*</span> | Forces the operation to time out after *timeoutSeconds* seconds if it has not completed by that time. If this flag is not provided, URLRequest runs until the server has finished sending and receiving data. For simple requests a value of a few seconds is appropriate. However, because uploading and/or downloading large amounts of data may take a long time, if *timeoutSeconds* is too small the request might be prematurely terminated. If you omit the /TIME flag, or if *timeoutSeconds* = 0, there is no timeout. |
|  | Regardless of whether or not you include /TIME, you can abort the operation by pressing the [User Abort Key Combinations](/igorpro/programming/programming.md#user-abort-key-combinations). |
| <span class="table-cell-nowrap">/V = *diagnosticMode*</span> | Controls diagnostic messages printed in the history area of the command window. |
|  |<table class="nested-table"><tbody><tr><td>/V=0:</td><td>Do not print any diagnostic messages. This is the default if you omit /V.</td></tr><tr><td>/V=1:</td><td>Prints an error message if a run time error occurs.</td></tr><tr><td>/V=2:</td><td>Prints full debugging information.</td></tr></tbody></table>
| <span class="table-cell-nowrap">/Z[ = *z*]</span> | Suppress error generation. Use this if you want to handle errors yourself. |
|  |<table class="nested-table"><tbody><tr><td>/Z=0:</td><td>Do not suppress errors. This is the default if /Z is omitted.</td></tr><tr><td>/Z=1:</td><td>Any errors generated by Igor do not stop execution. If there is an error the error code is stored in V_Flag.</td></tr></tbody></table>
|  | /Z alone has the same effect as /Z=1. |

### *Output Variables* {#output-variables}
URLRequest sets the following output variables:


|  |  |
| --- | --- |
| V_flag | V_flag is zero if the operation succeeds without an error or a non-zero Igor error code if it fails. |
|  | Note that "succeeds without an error" does not necessarily mean that the operation performed as you intended. For example, if you attempt to connect to a server that requires a username and password for authentication but you do not provide this information, V_flag is likely to be 0, indicating no error. You need to inspect the value of V_responseCode to ensure that it is what you expect. |
| V_responseCode | Contains the status code provided by the server. |
|  | V_responseCode is valid only if V_flag is 0, meaning that no error occured. If V_flag is nonzero, an error occured and V_responseCode will be 0. |
|  | Different schemes use different sets of status codes. |
|  | A list of http/https status codes and their definitions can be found at: |
|  | [http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) |
|  | A list of FTP status codes can be found at: |
|  | [https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes](https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes) |
| S_serverResponse | Contains the server's response to the request. |
|  | S_serverResponse is set to "" if you use the /FILE flag or the /IGN=1 or /IGN=2 flags. |
|  | We recommend that you use the /FILE flag when you expect the size of the server response to be large, such as when downloading a large file. |
| S_headers | Contains a list of all of the headers received as part of the response. Header names are separated from their value by a colon and pairs are separated by a carriage return followed by a line feed (\r\n). For schemes other than http and https, S_headers is set to "". |
| S_fileName | Contains the full Igor-style path to the output file if the /FILE flag was used. If there was an error saving to the specified file, or another kind of error, or if the /FILE flag was not used, S_fileName is set to "". |

### *Basic Examples* {#basic-examples}

```igor
// Retrieve the contents of the WaveMetrics home page.
// Output is stored in S_serverResponse
URLRequest url="http://www.wavemetrics.com"

// Download the Windows Igor9 installer and save it as a file on the desktop.
NewPath/O Desktop, SpecialDirPath("Desktop", 0, 0, 0)
String theURL = "http://www.wavemetrics.net/Downloads/Win/setupIgor9.exe"
URLRequest/FILE="setupIgor9.exe"/P=Desktop url=theURL

// Download a file to the desktop from an FTP server.
NewPath/O Desktop, SpecialDirPath("Desktop", 0, 0, 0)
String theURL = "ftp://ftp.wavemetrics.com/test/test.htm"
URLRequest/O/FILE="test.htm"/P=Desktop url=theURL

// Upload the same file to the FTP server.
theURL = "ftp://user:pass@ftp.wavemetrics.com/test.htm"
URLRequest/DFIL="test.htm"/P=Desktop method=put, url=theURL
```

### *Using the File Scheme* {#using-the-file-scheme}
URLRequest supports the file scheme in URLs. You must provide the full path to the file as a native Windows-style or UNIX-style path, depending on which platform the code is running.

You must specify the schema as "file:///". Note that you must use three front slash characters (/) between the colon and the full file path (for most URL protocols you would only use two slashes).


```igor
URLRequest url="file:///F:\\Test Data\\myData.txt"	// Works on Windows only
URLRequest url="file:///Users/Jim/myData.txt"		// Works on Macintosh only
```

The following example shows how to convert a full Igor file path to a native path suitable for use as a file URL:


```igor
String igorFilePath = "C:User:myName:Documents:myFile.txt" // Mac path syntax
String nativeFilePath = ParseFilePath(5, igorFilePath, "*", 0, 0)
URLRequest url="file:///" + nativeFilePath
```

### *The HTTP POST Method* {#the-http-post-method}
Like the HTTP GET method, the HTTP POST method can be used to transmit information to a web server. When using the GET method, all information must be contained within the URL itself. As an example, making a GET request to the URL [http://www.google.com/search?q=Igor+Pro+WaveMetrics](http://www.google.com/search?q=Igor+Pro+WaveMetrics) searches Google using the keywords "Igor", "Pro", and "WaveMetrics".

Unlike the GET method, the POST method allows the client to send information to the server that is not contained within the URL itself. This is necessary in many situations, such as when uploading a file or transfering a large amount of data. In addition, because the data contained in POST requests is typically not stored in the log files of web servers, it is more appropriate for sending data that is secure, such as login credentials and form submissions which might contain sensitive information.

When using the POST method, the client must encode its data using one of several methods and must tell the server what type of data is being sent and how it is encoded. The client does this by setting the Content-Type header that is part of the request. The most commonly used content type is "application/x-www-form-urlencoded". Unless you provide your own Content-Type header using the optional headers parameter, URLRequest will set this header for you. This is true regardless of which data source (/DSTR for string or /DFIL for file) you use for the POST.

Here is a simple example that uses the POST method with URL encoded data (the default Content-Type).


```igor
String theURL = "http://www.example.com/process.php"
String nameData = URLEncode("name") + "=" + URLEncode("Dan P. Ikes, Jr.")
String address = "650 E. Chicago Ave."
String addressData = URLEncode("address") + "=" + URLEncode(address)
String postData = nameData + "&" + addressData
URLRequest/DSTR=postData method=post, url=theURL
```

There are two things to note in this example.

First, both the key name and value string are passed through [URLEncode](/igorpro/commands/urlencode.md) so that any special characters can be percent-encoded.

Second, keys and values are separated by an equal sign ("=") and key/value pairs are separated by an ampersand ("&"). These characters are not passed through URLEncode because doing so would cause them to lose their meaning as special characters.

For more information on using the application/x-www-form-urlencoded content type, see [http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1](http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1)

It is also possible to transmit more complicated data using the POST method, such as simulating a form that contains regular text fields as well as a file upload field. To do so you must set the Content-Type header using the headers parameter. You must also build your post data using a multi-part header. Here is an example:


```igor
String theURL = "http://www.example.com/process.php"
String postData = ""
// Note: The boundary is arbitrary. It needs to be
// unique enough that it is not contained within any
// of the actual data being transmitted in the post.
String boundary = "AaBbCcDd0987"

// name
postData += "--" + boundary + "\r\n"	// beginning of this part
postData += "Content-Disposition: form-data; name=\"name\"\r\n"
postData += "\r\n"
postData += "Dan P. Ikes, Jr.\r\n"

// address
postData += "--" + boundary + "\r\n"
postData += "Content-Disposition: form-data; name=\"address\"\r\n"
postData += "\r\n"
postData += "650 E. Chicago Ave.\r\n"

// file
// Open the file we plan to send and store the binary
// contents of the file in a string.
Variable refNum
Open/R/Z/P=Igor refNum as "ReadMe.ihf"
FStatus refNum
Variable fileSize = V_logEOF
String fileContents = ""
fileContents = PadString(fileContents, fileSize, 0)
FBinRead refNum, fileContents
Close refNum
postData += "--" + boundary + "\r\n"
postData += "Content-Disposition: form-data; name=\"file\"; filename=\"ReadMe.ihf\"\r\n"
postData += "Content-Type: application/octet-stream\r\n"
postData += "Content-Transfer-Encoding: binary\r\n"
postData += "\r\n"
postData += fileContents + "\r\n"

postData += "--" + boundary + "--\r\n"	// end of this part

String headers
headers = "Content-Type: multipart/form-data; boundary=" + boundary
URLRequest/DSTR=postData method=post, url=theURL, headers=headers
```

For more information on using the multipart/form-data content type, see [http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.2](http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.2)

### *Handling JSON Data* {#handling-json-data}
JSON (JavaScript Object Notation) is a lightweight data-interchange format that is commonly used when interacting with websites - see [https://www.json.org/json-en.html](https://www.json.org/json-en.html). For full read and write JSON support in Igor Pro, we recommend using the JSON XOP, developed byte physics. You can download it from [https://docs.byte-physics.de/json-xop](https://docs.byte-physics.de/json-xop).

### *See Also* {#see-also}
[URLEncode](/igorpro/commands/urlencode.md), [URLDecode](/igorpro/commands/urldecode.md), [Base64Encode](/igorpro/commands/base64encode.md), [Base64Decode](/igorpro/commands/base64decode.md), [FetchURL](/igorpro/commands/fetchurl.md), [BrowseURL](/igorpro/commands/browseurl.md)

[Network Communication](/igorpro/advanced-topics.md#network-communication), [URLs](/igorpro/advanced-topics.md#urls)