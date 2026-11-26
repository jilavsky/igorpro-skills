---
description: "The ThreadGroupPutDF operation posts data to a preemptive thread group."
slug: /commands/threadgroupputdf
---

<div className="command-signature">

## <strong>ThreadGroupPutDF</strong>  <em>tgID</em>, <em>datafolder</em> {#threadgroupputdf}

</div>

The ThreadGroupPutDF operation posts data to a preemptive thread group.

### *Parameters* {#parameters}
*tgID* is thread group ID returned by [ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md), *datafolder* is the data folder you wish to send to the thread group.

*datafolder* can be just the name of a child data folder in the current data folder, a partial path (relative to the current data folder) and name or an absolute path (starting from root) and name.

### *Details* {#details}
When you call it from the main thread, [ThreadGroupPutDF](/igorpro/commands/threadgroupputdf.md) removes *datafolder* from the main thread's data hierarchy and posts to the input queue of the thread group specified by *tgID*.

When you call it from a preemptive thread, use 0 for *tgID* and the data folder will be posted to the output queue of thread group to which thread belongs.

Input and output data folders may be retrieved from the queues by calling [ThreadGroupGetDF](/igorpro/commands/threadgroupgetdf.md) or [ThreadGroupGetDFR](/igorpro/commands/threadgroupgetdfr.md).

:::warning
Take care not to use any stale WAVE, NVAR, or SVAR variables that might contain references to objects in the data folder. Use [WAVEClear](/igorpro/programming/keywords/object-reference-keywords.md#waveclear) on all WAVE reference variables that might contain references to waves that are in the data folder being posted before calling [ThreadGroupPutDF](/igorpro/commands/threadgroupputdf.md). An error will occur if any waves in the data folder are in use or referenced in a WAVE variable.
:::

:::warning
Any DFREF variables that refer to the data folder (or any child thereof) must be cleared prior to executing this command. You can clear a DFREF using dfr=$"".
:::

From the standpoint of the source thread, [ThreadGroupPutDF](/igorpro/commands/threadgroupputdf.md) is conceptually similar to [KillDataFolder](/igorpro/commands/killdatafolder.md) and, like KillDataFolder, if the current data folder is within datafolder, the current data folder is set to the parent of *datafolder*. You cannot pass root: as *datafolder*.

### *See Also* {#see-also}
[ThreadGroupCreate](/igorpro/commands/threadgroupcreate.md)

[ThreadSafe Functions](/igorpro/programming/programming.md#threadsafe-functions), [ThreadSafe Functions and Multitasking](/igorpro/advanced-topics.md#threadsafe-functions-and-multitasking)