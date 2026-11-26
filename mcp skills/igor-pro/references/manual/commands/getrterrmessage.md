---
description: "In a user function, GetRTErrMessage returns a string containing the name of the Igor operation that caused the error, a semicolon, and an error message…"
slug: /commands/getrterrmessage
---

<div className="command-signature">

## <strong>GetRTErrMessage</strong> () {#getrterrmessage}

</div>

In a user function, GetRTErrMessage returns a string containing the name of the Igor operation that caused the error, a semicolon, and an error message explaining the cause of the error. This is the same information that appears in the alert dialog displayed by Igor. If no error has occurred, the string will be of zero length. GetRTErrMessage must be called before the error is cleared by calling GetRTError with a nonzero argument.

For an overview of error handling, see [Flow Control for Aborts](/igorpro/programming/programming.md#flow-control-for-aborts).

### *See Also* {#see-also}
[Flow Control for Aborts](/igorpro/programming/programming.md#flow-control-for-aborts), [GetRTError](/igorpro/commands/getrterror.md), [GetErrMessage](/igorpro/commands/geterrmessage.md)