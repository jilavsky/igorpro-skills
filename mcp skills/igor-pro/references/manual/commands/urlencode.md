---
description: "The URLEncode function returns a percent-encoded copy of inputStr. Percent-encoding is useful when encoding the query part of a URL or when the URL contains…"
slug: /commands/urlencode
---

<div className="command-signature">

## <strong>URLEncode</strong> (<em>inputStr</em>) {#urlencode}

</div>

The URLEncode function returns a percent-encoded copy of *inputStr*.

Percent-encoding is useful when encoding the query part of a URL or when the URL contains special characters that might otherwise be misinterpreted by a web server. For an explanation of percent-encoding, see [Percent Encoding](/igorpro/advanced-topics.md#percent-encoding).

### *Example* {#example}

```igor
String baseURL = "http://google.com"
String key1 = "key1"
String value1 = URLEncode("35% larger")
String theURL = ""
sprintf theURL, "%s?%s=%s", baseURL, key1, value1
Print theURL
  http://google.com?key1=35%25%20larger
```

### *See Also* {#see-also}
[URLDecode](/igorpro/commands/urldecode.md), [URLRequest](/igorpro/commands/urlrequest.md), [URLs](/igorpro/advanced-topics.md#urls)