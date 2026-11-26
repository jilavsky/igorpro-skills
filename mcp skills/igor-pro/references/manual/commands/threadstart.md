---
description: "The ThreadStart operation starts the specified function running in a preemptive thread."
slug: /commands/threadstart
---

<div className="command-signature">

## <strong>ThreadStart</strong>  <em>tgID</em>, <em>index</em>, <em>WorkerFunc</em> (<em>param1</em>, <em>param2</em>,...) {#threadstart}

</div>

The ThreadStart operation starts the specified function running in a preemptive thread.

### *Parameters* {#parameters}
*tgID* is thread group ID returned by [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md), *index* is the desired thread of the group to set up to execute the specified ThreadSafe WorkerFunc.

### *Details* {#details}
The worker function starts running immediately.

The worker function must be defined as ThreadSafe and must return a real or complex numeric result.

The worker function's return value can be obtained after the function finishes by calling [ThreadReturnValue](/igorpro/commands/threadreturnvalue.md). Igor records the fact that a thread has terminated when you call ThreadGroupWait so you must call [ThreadGroupWait](/igorpro/commands/threadgroupwait.md) before calling ThreadReturnValue.

The worker function can take variable and wave parameters. It cannot take pass-by-reference parameters or data folder reference parameters.

Any waves you pass to the worker are accessible to both the main thread and to your preemptive thread. Such waves are marked as being in use by a thread and Igor will refuse to perform any manipulations that could change the size of the wave.

### *See Also* {#see-also}
[ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md), [ThreadReturnValue](/igorpro/commands/threadreturnvalue.md)

[ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)