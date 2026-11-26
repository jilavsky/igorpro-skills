---
description: "The URLDecode function returns a percent-decoded copy of the percent-encoded string inputStr."
slug: /commands/urldecode
---

<div className="command-signature">

## <strong>URLDecode</strong> (<em>inputStr</em>) {#urldecode}

</div>

The URLDecode function returns a percent-decoded copy of the percent-encoded string *inputStr*. It is unlikely that you will need to use this function; it is provided for completeness.

For an explanation of percent-encoding, see [Percent Encoding](/igorpro/advanced-topics.md#percent-encoding).

### *Example* {#example}

```igor
String theURL = "http://google.com?key1=35%25%20larger"
theURL = URLDecode(theURL)
Print theURL
  http://google.com?key1=35% larger
```

### *See Also* {#see-also}
[URLEncode](/igorpro/commands/urlencode.md), [URLRequest](/igorpro/commands/urlrequest.md), [URLs](/igorpro/advanced-topics.md#urls)