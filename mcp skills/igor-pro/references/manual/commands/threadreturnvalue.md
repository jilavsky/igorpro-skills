---
description: "The ThreadReturnValue function returns the value that the specified thread function returned when it exited. Returns NAN if thread is still running."
slug: /commands/threadreturnvalue
---

<div className="command-signature">

## <strong>ThreadReturnValue</strong> (<em>tgID</em>, <em>index</em>) {#threadreturnvalue}

</div>

The ThreadReturnValue function returns the value that the specified thread function returned when it exited. Returns NAN if thread is still running.  *tgID* is the thread group ID returned by [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md) and *index* is the thread number.

When [ThreadGroupWait](/igorpro/commands/threadgroupwait.md) is called, Igor updates certain internal variables including variables that track whether a thread has finished and what result it returned. Therefore you must call ThreadGroupWait before calling ThreadReturnValue.

### *See Also* {#see-also}
[ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md), [ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)