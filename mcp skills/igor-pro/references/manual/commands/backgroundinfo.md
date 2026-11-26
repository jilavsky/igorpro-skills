---
description: "The BackgroundInfo operation returns information about the current unnamed background task."
slug: /commands/backgroundinfo
---

<div className="command-signature">

## <strong>BackgroundInfo</strong> {#backgroundinfo}

</div>

The BackgroundInfo operation returns information about the current unnamed background task.

BackgroundInfo works only with the unnamed background task. New code should used named background tasks instead. See [Background Tasks](/igorpro/advanced-topics.md#background-tasks) for details.

### *Details* {#details}
The information is returned via the following variables:


|  |  |
| --- | --- |
| V_flag |<table class="nested-table"><tbody><tr><td>0:</td><td>If no background task is defined.</td></tr><tr><td>1:</td><td>A background task is defined, but not running (is idle).</td></tr><tr><td>2:</td><td>A background task is defined and is running.</td></tr></tbody></table>
| V_period | The deltaTicks value set by [CtrlBackground](/igorpro/commands/ctrlbackground.md). This is how often the background task runs. |
| V_nextRun | The [ticks](/igorpro/commands/ticks.md) value when the task will run again. 0 if the task is not scheduled to run again. |
| S_value | The text of the numeric expression that the background task executes, as set by [SetBackground](/igorpro/commands/setbackground.md). |

### *See Also* {#see-also}
[Background Tasks](/igorpro/advanced-topics.md#background-tasks)

[SetBackground](/igorpro/commands/setbackground.md), [CtrlBackground](/igorpro/commands/ctrlbackground.md), [KillBackground](/igorpro/commands/killbackground.md), [ticks](/igorpro/commands/ticks.md)