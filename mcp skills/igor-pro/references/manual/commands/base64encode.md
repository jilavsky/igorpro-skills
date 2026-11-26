---
description: "The Base64Encode function returns a copy of inputStr encoded as Base64."
slug: /commands/base64encode
---

<div className="command-signature">

## <strong>Base64Encode</strong> (<em>inputStr</em>) {#base64encode}

</div>

The Base64Encode function returns a copy of *inputStr* encoded as Base64.

The algorithm used to encode Base64-encoded data is defined in RFC 4648 ([http://www.ietf.org/rfc/rfc4648.txt](http://www.ietf.org/rfc/rfc4648.txt)).

For an explanation of Base64 encoding, see [https://en.wikipedia.org/wiki/Base64](https://en.wikipedia.org/wiki/Base64).

The Base64Encode function was added in Igor Pro 8.00.

### *Example* {#example}

```igor
String theString = "Igor is great!"
Print Base64Encode(theString)
  SWdvciBpcyBncmVhdCE=
```

### *See Also* {#see-also}
[Base64Decode](/igorpro/commands/base64decode.md), [URLRequest](/igorpro/commands/urlrequest.md)