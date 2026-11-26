---
description: "ThreadGroupGetDFR should be used instead of ThreadGroupGetDF which causes memory leaks."
slug: /commands/threadgroupgetdf
---

<div className="command-signature">

## <strong>ThreadGroupGetDF</strong> (<em>tgID</em>, <em>waitms</em>) {#threadgroupgetdf}

</div>

[ThreadGroupGetDFR](/igorpro/commands/threadgroupgetdfr.md) should be used instead of ThreadGroupGetDF which causes memory leaks.

The ThreadGroupGetDF function retrieves a data folder path string from a thread group queue and removes the data folder from the queue.

When called from a preemptive thread it returns a data folder from the thread group's input queue. When called from the main thread it returns a data folder from the thread group's output queue.

*tgID* is a thread group ID returned by [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md). You can pass 0 for *tgID* when calling ThreadGroupGetDF from a preemptive thread. You must pass a valid thread group ID when calling ThreadGroupGetDF from the main thread.

*waitms* is the maximum number of milliseconds to wait for a data folder to become available in the queue. Pass 0 to test if a data folder is available immediately. Pass INF to wait indefinitely or until a user abort.

ThreadGroupGetDF returns "" if the timeout period specified by *waitms* expires and no data folder is available in the queue.

### *See Also* {#see-also}
[ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)

[ThreadGroupGetDFR](/igorpro/commands/threadgroupgetdfr.md)