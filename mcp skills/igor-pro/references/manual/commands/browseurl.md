---
description: "The BrowseURL operation opens the web browser or FTP browser on your computer and asks it to display a particular web page or to connect to an FTP server."
slug: /commands/browseurl
---

<div className="command-signature">

## <strong>BrowseURL</strong>  [/Z ] <em>urlStr</em> {#browseurl}

</div>

The BrowseURL operation opens the web browser or FTP browser on your computer and asks it to display a particular web page or to connect to an FTP server.

BrowseURL sets a variable named V_flag to zero if the operation succeeds and to nonzero if it fails. This, in conjunction with the /Z flag, can be used to allow procedures to continue to execute if an error occurs.

### *Parameters* {#parameters}
*urlStr* specifies the web page or FTP server directory to be browsed. It is constructed of a naming scheme (such as "http://" or "ftp://"), a computer name (e.g., "www.wavemetrics.com" or "ftp.wavemetrics.com" or "38.170.234.2"), and a path (e.g., "/Test/TestFile1.txt"). See below for examples.

### *Flags* {#flags}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">/Z</span> | Errors are not fatal. Will not abort procedure execution if the URL is bad or if the server is down. Your procedure can inspect the V_flag variable to see if the transfer succeeded. V_flag will be zero if it succeeded or nonzero if it failed. |
|  | Syntactic errors, such as omitting the URL altogether or omitting quotes, are still fatal. |

### *Examples* {#examples}

```igor
//	Browse a web page.
	String url = "http://www.wavemetrics.com/News/index.html"
	BrowseURL url
//	Browse an FTP server.
	String url = "ftp://ftp.wavemetrics.com/pub/test"
	BrowseURL url
```

### *See Also* {#see-also}
[URLRequest](/igorpro/commands/urlrequest.md)