---
description: "The ParamIsDefault function determines if an optional user function parameter pName was specified during the function call."
slug: /commands/paramisdefault
---

<div className="command-signature">

## <strong>ParamIsDefault</strong> (<em>pName</em>) {#paramisdefault}

</div>

The ParamIsDefault function determines if an optional user function parameter *pName* was specified during the function call. It returns 1 when *pName* is default (not specified) or it returns 0 when it was specified.

### *Details* {#details}
ParamIsDefault works only in the body of a user function and only with optional parameters. The variable name must be valid at compile time; you cannot defer lookup to runtime with $.

### *See Also* {#see-also}
[Optional Parameters](/igorpro/programming/programming.md#optional-parameters), [Using Optional Parameters](/igorpro/programming/programming.md#using-optional-parameters)