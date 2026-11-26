---
description: "The CtrlBackground operation controls the unnamed background task. CtrlBackground works only with the unnamed background task."
slug: /commands/ctrlbackground
---

<div className="command-signature">

## <strong>CtrlBackground</strong>  [<em>start</em>[=<em>startTicks</em> ], <em>period</em>=<em>deltaTicks</em>, <em>dialogsOK</em>=<em>d</em>, <em>noBurst</em>=<em>n</em>, <em>stop</em>] {#ctrlbackground}

</div>

The CtrlBackground operation controls the unnamed background task.

CtrlBackground works only with the unnamed background task. New code should used named background tasks instead. See [Background Tasks](/igorpro/advanced-topics.md#background-tasks) for details.

### *Parameters* {#parameters}

|  |  |
| --- | --- |
| <span class="table-cell-nowrap">period = *deltaTicks*</span> | Sets the minimum number of ticks that must pass between invocations of the background task. |
| <span class="table-cell-nowrap">dialogsOK = 1 *or* 0</span> | If 1, your task will be allowed to run while an Igor dialog is present. This can potentially cause crashes unless your task is well behaved. |
| <span class="table-cell-nowrap">noBurst = 1 *or* 0</span> | Normally (or noBurst=0), your task will be called at maximum rate if a delay misses normal run times. Using noBurst=1, will suppress this burst catch up mode. |
| <span class="table-cell-nowrap">start[ = *startTicks* ]</span> | Starts the background task (designated by [SetBackground](/igorpro/commands/setbackground.md)) when the tick count reaches *startTicks*. If you omit *startTicks* the task starts immediately. |
| stop | Stops the background task. |

### *See Also* {#see-also}
[SetBackground](/igorpro/commands/setbackground.md), [KillBackground](/igorpro/commands/killbackground.md), [CtrlNamedBackground](/igorpro/commands/ctrlnamedbackground.md), [BackgroundInfo](/igorpro/commands/backgroundinfo.md)

[Background Tasks](/igorpro/advanced-topics.md#background-tasks)