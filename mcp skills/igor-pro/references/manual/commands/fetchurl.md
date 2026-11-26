---
description: "The FetchURL function returns a string containing the server's response to a request to get the contents of the URL specified by urlStr."
slug: /commands/fetchurl
---

<div className="command-signature">

## <strong>FetchURL</strong> (<em>urlStr</em>) {#fetchurl}

</div>

The FetchURL function returns a string containing the server's response to a request to get the contents of the URL specified by *urlStr*. If *urlStr* contains a URL that uses the file:// scheme, the contents of the local file is returned.

### *Parameters* {#parameters}
*urlStr* is a string containing the URL to retrieve.  You can include a username, password, and server port number as part of the URL.

FetchURL expects that *urlStr* has been percent-encoded if it contains reserved characters. See [Percent Encoding](/igorpro/advanced-topics.md#percent-encoding) for additional information on when percent-encoding is necessary and how to do it.

See [URLs](/igorpro/advanced-topics.md#urls) for details about how to correctly specify the URL.

FetchURL supports only the http://, https://, ftp://, and file:// schemes. See [Supported Network Schemes](/igorpro/advanced-topics.md#supported-network-schemes) for details.

There are two special values of *urlStr* that can be used to get information about the network library that Igor uses. The keyword=value pairs returned when *urlStr* is  "curl_version_info" may be useful to programmers in that the features and protocols available in the library are specified.


```igor
FetchURL("curl_version")
FetchURL("curl_version_info")
```

### *Details* {#details}
If FetchURL encounters an error, it returns a NULL string. You should check for errors before using the returned string. In a user-defined function, use the [GetRTError](/igorpro/commands/getrterror.md) function.


```igor
String urlStr = "http://www.badserver"
String response = FetchURL(urlStr)
Variable error = GetRTError(1)	// Check for error before using response
if (error != 0)
    // FetchURL produced an error
    // so don't try to use the response.
endif
```

### *Limitations* {#limitations}
It is possible for FetchURL to return a valid server response even though the URL you requested does not exist on the server or requires a username and password that you did not provide. In this situation, the response returned by the server will usually be a web page stating that the page was not found or another error message. You can check for this kind of error in your own code by examining the response.

FetchURL does not support advanced features such as network proxies, file or data uploads, setting the timeout period, or saving the server's response directly to a file. When using the http:// scheme, only the GET method is supported. This means that you cannot use FetchURL to submit form data to a web server that requires using the http POST method. Use the [URLRequest](/igorpro/commands/urlrequest.md) operation if you need any of these advanced features.

Igor Pro is not capable of displaying the contents of a URL in a rendered form like a web browser.

### *Examples* {#examples}

```igor
// Retrieve the contents of the WaveMetrics home page.
String response
response = FetchURL("http://www.wavemetrics.com")

// Get a binary image file from a web server and then
// save the image to a file on the desktop.
String url = "http://www.wavemetrics.net/images/tbg.gif"
String imageBytes = FetchURL(url)
Variable error = GetRTError(1)
if (error != 0)
	Print "Error downloading image."
else
	Variable refNum
	String localPath = SpecialDirPath("Desktop", 0, 0, 0) + "tbg.gif"
	Open/T=".gif" refNum as localPath
	FBinWrite refNum, imageBytes
	Close refNum
endif
```

### *See Also* {#see-also}
[FTPDownload](/igorpro/commands/ftpdownload.md), [URLEncode](/igorpro/commands/urlencode.md), [URLRequest](/igorpro/commands/urlrequest.md)

[Network Communication](/igorpro/advanced-topics.md#network-communication), [Network Connections from Multiple Threads](/igorpro/advanced-topics.md#network-connections-from-multiple-threads)