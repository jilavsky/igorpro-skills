---
description: "The ThreadGroupRelease function releases the thread group referenced by tgID. tgID is the thread group ID returned by ThreadGroupCreate."
slug: /commands/threadgrouprelease
---

<div className="command-signature">

## <strong>ThreadGroupRelease</strong> (<em>tgID</em> [, <em>beGraceful</em>]) {#threadgrouprelease}

</div>

The ThreadGroupRelease function releases the thread group referenced by *tgID*. *tgID* is the thread group ID returned by [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md). Any data folders remaining in the group's input or output queues are discarded.

Specifying *tgID*=-2 kills all running threads in all thread groups.

Normally you call ThreadGroupRelease after all threads in the group have completed. In the event that threads are still running, they are aborted. An attempt is made to safely stop running threads but, if they continue to run, they are killed.

The *beGraceful* parameter, added in Igor Pro 9.00, affects thread worker functions that include catch blocks to handle aborts gracefully. If *beGraceful* is omitted or is 0, ThreadGroupRelease performs aborts in a way that interferes with such catch blocks. If *beGraceful* is 1, the catch blocks run normally. See [Aborting Threads Gracefully](/igorpro/advanced-topics.md#aborting-threads-gracefully) for details.

ThreadGroupRelease returns zero if successful, -1 if an error occurred (probably invalid *tgID*), or -2 if a force quit was needed, in which case you should restart Igor Pro.

### *See Also* {#see-also}
[ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md), [ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)