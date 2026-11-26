---
description: "The IgorVersion function returns version number of the Igor application as a floating point number. Igor Pro 8.00 returns 8.00, as does Igor Pro 8.00A."
slug: /commands/igorversion
---

<div className="command-signature">

## <strong>IgorVersion</strong> () {#igorversion}

</div>

The IgorVersion function returns version number of the Igor application as a floating point number. Igor Pro 8.00 returns 8.00, as does Igor Pro 8.00A.

### *Details* {#details}

You can use IgorVersion in conditionally compile code expressions, which can be used to omit calls to new Igor features or to provide backwards compatibility code.

```igor
#if (IgorVersion() >= 8.00) 
	[Code that compiles only on Igor Pro 8.00 or later]
#else
	[Code that compiles only on earlier versions of Igor]
#endif
```

If at all possible, it is better to require your users to use a later version of Igor rather than writing conditional code. Attempting this kind of backward-compatibility multiplies your testing requirements and the chances for bugs.

### *See Also* {#see-also}
[IgorInfo](/igorpro/commands/igorinfo.md), [Conditional Compilation](/igorpro/programming/programming.md#conditional-compilation), [The IgorVersion Pragma](/igorpro/programming/programming.md#the-igorversion-pragma)