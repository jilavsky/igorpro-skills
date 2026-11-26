---
description: "The DelayUpdate operation delays the updating of graphs and tables while executing a macro."
slug: /commands/delayupdate
---

<div className="command-signature">

## <strong>DelayUpdate</strong> {#delayupdate}

</div>

The DelayUpdate operation delays the updating of graphs and tables while executing a macro.

### *Details* {#details}
Use DelayUpdate at the end of a line in a macro if you want the next line in the macro to run before graphs or tables are updated.

This has no effect in user-defined functions. During execution of a user-defined function, Igor updates windows only when you explicitly call the [DoUpdate](/igorpro/commands/doupdate.md) operation.

### *See Also* {#see-also}
[DoUpdate](/igorpro/commands/doupdate.md), [PauseUpdate](/igorpro/commands/pauseupdate.md), [ResumeUpdate](/igorpro/commands/resumeupdate.md)