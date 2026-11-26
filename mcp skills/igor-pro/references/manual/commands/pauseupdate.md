---
description: "The PauseUpdate operation delays the updating of graphs and tables until you invoke a corresponding ResumeUpdate command."
slug: /commands/pauseupdate
---

<div className="command-signature">

## <strong>PauseUpdate</strong> {#pauseupdate}

</div>

The PauseUpdate operation delays the updating of graphs and tables until you invoke a corresponding ResumeUpdate command.

### *Details* {#details}
PauseUpdate is useful in a macro that changes a number of things relating to the appearance of a graph. It prevents the graph from being updated after each change. Its effect ends when the macro in which it occurs ends. It also affects updating of tables.

This operation is not allowed from the command line. It is allowed but has no effect in user-defined functions. During execution of a user-defined function, windows update only when you explicitly call the DoUpdate operation.

### *See Also* {#see-also}
[DoUpdate](/igorpro/commands/doupdate.md), [DelayUpdate](/igorpro/commands/delayupdate.md), [ResumeUpdate](/igorpro/commands/resumeupdate.md), [Silent](/igorpro/commands/silent.md)