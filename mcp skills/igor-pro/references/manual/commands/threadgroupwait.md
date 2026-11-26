---
description: "The ThreadGroupWait function returns index+1 of the first thread found still running after waitms milliseconds or returns zero if all are done."
slug: /commands/threadgroupwait
---

<div className="command-signature">

## <strong>ThreadGroupWait</strong> (<em>tgID</em>, <em>waitms</em>) {#threadgroupwait}

</div>

The ThreadGroupWait function returns index+1 of the first thread found still running after *waitms* milliseconds or returns zero if all are done.

*tgID* is the thread group ID returned by ThreadGroupCreate and *waitms* is milliseconds to wait.

If any of the threads of the group encountered a runtime error, the first such error will be reported now.

Use zero for *waitms* to just test or provide a large value to cause the main thread to sleep until the threads are finished. You can use INF to wait indefinitely or until a user abort. If you know the maximum time the threads should take, you can use that value so you can print an error message or take other action if the threads don't return in time.

When ThreadGroupWait is called, Igor updates certain internal variables including variables that track whether a thread has finished and what result it returned. Therefore you must call ThreadGroupWait before calling [ThreadReturnValue](/igorpro/commands/threadreturnvalue.md).

ThreadGroupWait updates the internal state of all threads in the group.

### *Finding a Free Thread* {#finding-a-free-thread}
If you pass -2 for *waitms* , ThreadGroupWait returns index+1 of the first free (not running) thread or 0 if all threads in the group are running.

This allows you to dispatch a thread anytime a free thread is available. See [Parallel Processing - Thread-at-a-Time Method](/igorpro/advanced-topics.md#parallel-processing-thread-at-a-time-method) for an example.

### *See Also* {#see-also}
[ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md), [ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)