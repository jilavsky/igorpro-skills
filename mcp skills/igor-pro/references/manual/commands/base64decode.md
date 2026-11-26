---
description: "The Base64Decode function returns a decoded copy of the Base64-encoded string inputStr. The contents of inputStr are not checked for validity."
slug: /commands/base64decode
---

<div className="command-signature">

## <strong>Base64Decode</strong> (<em>inputStr</em>) {#base64decode}

</div>

The Base64Decode function returns a decoded copy of the Base64-encoded string *inputStr*. The contents of *inputStr* are not checked for validity. Any invalid characters in *inputStr* are skipped, and decoding continues with subsequent characters.

The algorithm used to encode Base64-encoded data is defined in RFC 4648 ([http://www.ietf.org/rfc/rfc4648.txt](http://www.ietf.org/rfc/rfc4648.txt)).

For an explanation of Base64 encoding, see [https://en.wikipedia.org/wiki/Base64](https://en.wikipedia.org/wiki/Base64).

The Base64Decode function was added in Igor Pro 8.00.

### *Example* {#example}

```igor
String encodedString = "SWdvciBpcyBncmVhdCE="
Print Base64Decode(encodedString)
  Igor is great!
```

### *See Also* {#see-also}
[Base64Encode](/igorpro/commands/base64encode.md), [URLRequest](/igorpro/commands/urlrequest.md)