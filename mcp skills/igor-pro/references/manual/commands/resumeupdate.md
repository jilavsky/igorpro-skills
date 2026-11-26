---
description: "The ResumeUpdate operation cancels the corresponding PauseUpdate. This operation is of use in macros. It is not allowed from the command line."
slug: /commands/resumeupdate
---

<div className="command-signature">

## <strong>ResumeUpdate</strong> {#resumeupdate}

</div>

The ResumeUpdate operation cancels the corresponding PauseUpdate.

This operation is of use in macros. It is not allowed from the command line. It is allowed but has no effect in user-defined functions. During execution of a user-defined function, windows update only when you explicitly call the DoUpdate operation.

### *See Also* {#see-also}
[DoUpdate](/igorpro/commands/doupdate.md), [DelayUpdate](/igorpro/commands/delayupdate.md), [PauseUpdate](/igorpro/commands/pauseupdate.md)