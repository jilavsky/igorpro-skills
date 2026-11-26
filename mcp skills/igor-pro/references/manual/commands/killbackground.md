---
description: "The KillBackground operation kills the unnamed background task. KillBackground works only with the unnamed background task."
slug: /commands/killbackground
---

<div className="command-signature">

## <strong>KillBackground</strong> {#killbackground}

</div>

The KillBackground operation kills the unnamed background task.

KillBackground works only with the unnamed background task. New code should used named background tasks instead. See [Background Tasks](/igorpro/advanced-topics.md#background-tasks) for details.

### *Details* {#details}
You cannot call KillBackground from within the background function itself. However, if you return 1 from the background function, instead of the normal 0, Igor will terminate the background task.

### *See Also* {#see-also}
[BackgroundInfo](/igorpro/commands/backgroundinfo.md), [SetBackground](/igorpro/commands/setbackground.md), [CtrlBackground](/igorpro/commands/ctrlbackground.md), [Background Tasks](/igorpro/advanced-topics.md#background-tasks)