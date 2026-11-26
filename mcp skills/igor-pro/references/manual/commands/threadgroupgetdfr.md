---
description: "The ThreadGroupGetDFR function retrieves a data folder reference from a thread group queue and removes the data folder from the queue."
slug: /commands/threadgroupgetdfr
---

<div className="command-signature">

## <strong>ThreadGroupGetDFR</strong> (<em>tgID</em>, <em>waitms</em>) {#threadgroupgetdfr}

</div>

The ThreadGroupGetDFR function retrieves a data folder reference from a thread group queue and removes the data folder from the queue. The data folder becomes a free data folder.

When called from a preemptive thread it returns a data folder from the thread group's input queue. When called from the main thread it returns a data folder from the thread group's output queue.

*tgID* is a thread group ID returned by [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md). You can pass 0 for *tgID* when calling ThreadGroupGetDFR from a preemptive thread. You must pass a valid thread group ID when calling ThreadGroupGetDFR from the main thread.

*waitms* is the maximum number of milliseconds to wait for a data folder to become available in the queue. Pass 0 to test if a data folder is available immediately. Pass INF to wait indefinitely or until a user abort.

ThreadGroupGetDFR returns a NULL data folder reference if the timeout period specified by *waitms* expires and no data folder is available in the queue. You can test for NULL using [DataFolderRefStatus](/igorpro/commands/datafolderrefstatus.md).

### *See Also* {#see-also}
[ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking), [Free Data Folders](/igorpro/programming/programming.md#free-data-folders)