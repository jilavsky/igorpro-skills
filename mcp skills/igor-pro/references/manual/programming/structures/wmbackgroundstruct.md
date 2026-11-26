---
description: "See CtrlNamedBackground, Background Tasks, and Preemptive Background Task for further explanation of WMBackgroundStruct."
slug: /programming/structures/wmbackgroundstruct
---

## WMBackgroundStruct {#wmbackgroundstruct}

See [CtrlNamedBackground](/igorpro/commands/ctrlnamedbackground.md), [Background Tasks](/igorpro/advanced-topics.md#background-tasks), and [Preemptive Background Task](/igorpro/advanced-topics.md#preemptive-background-task) for further explanation of WMBackgroundStruct.


```igor
Structure WMBackgroundStruct
   char name[MAX_OBJ_NAME+1]  // Background task name
   UInt32 curRunTicks         // Tick count when task was called
   Int32 started              // TRUE when CtrlNamedBackground start is issued
   UInt32 nextRunTick         // Precomputed value for next run
                              // but user functions may change this
EndStructure
```