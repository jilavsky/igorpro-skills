---
description: "The SetBackground operation sets numericExpression as the current unnamed background task."
slug: /commands/setbackground
---

<div className="command-signature">

## <strong>SetBackground</strong>  <em>numericExpression</em> {#setbackground}

</div>

The SetBackground operation sets *numericExpression* as the current unnamed background task.

SetBackground works only with the unnamed background task. New code should used named background tasks instead. See [Background Tasks](/igorpro/advanced-topics.md#background-tasks) for details.

The background task runs while Igor is not busy with other things. Normally, there won't be a background task. The most common use for the background task is to monitor or drive a continuous data acquisition process.

### *Parameters* {#parameters}
*numericExpression*  is a single precision numeric expression that Igor executes when it isn't doing anything else.

### *Details* {#details}
*numericExpression* is expected to return one of three numeric values:

0:	Background task executed normally.

1:	Background task wants to stop.

2:	Background task encountered error and wants to stop.

Usually the expression will be a call to a user-defined numeric function or external function to drive or monitor data acquisition. The expression should be designed to execute very quickly and it should not present a dialog to the user or create or destroy windows. Generally, it should do nothing more than store data into waves or variables. You can use Igor's dependency mechanism to perform more extensive tasks.

SetBackground designates the background task but you must use CtrlBackground to start it. You can use KillBackground to stop it. You cannot call SetBackground from the background function itself.

### *See Also* {#see-also}
[BackgroundInfo](/igorpro/commands/backgroundinfo.md), [CtrlBackground](/igorpro/commands/ctrlbackground.md), [KillBackground](/igorpro/commands/killbackground.md), [Background Tasks](/igorpro/advanced-topics.md#background-tasks)